---
title: KubeDNS动态添加自定义DNS解析记录
date: 2019-12-19 20:55:33
tags: k8s
---

## kubedns: kubedns/dnsmasq/sidecar

### 前言

需要在容器内添加自定义DNS解析记录，无非是1. 在上游DNS添加，2. 在kubedns添加，3. 改容器内/etc/hosts也勉强能满足。但上游DNS很可能你无法操作，一个个改容器内hosts未免也太丑太麻烦。研究了下如何在kubedns中动态添加。


### 采用ConfigMap将hosts.dnsmasq挂载到dnsmasq容器

kubedns-hosts-cm.yml

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: kube-dns-hosts
  namespace: kube-system
  labels:
    addonmanager.kubernetes.io/mode: EnsureExists
data:
  hosts.dnsmasq: |
    127.0.0.1 haha.mashaz.com
```

### dnsmasq启动参数--addon-hosts指定到hosts.dnsmasq

kubedns-controller.yml

```
apiVersion: extensions/v1beta1
kind: Deployment
...
spec:
  ...
    spec:
      restartPolicy: Always
      ...
      volumes:
      - name: kube-dns-hosts
        configMap:
          name: kube-dns-hosts
          optional: true
      containers:
      ...
      - name: dnsmasq
        ...
        args:
        ...
        - --server=/cluster.local./127.0.0.1#10053
        - --server=/in-addr.arpa/127.0.0.1#10053
        - --server=/ip6.arpa/127.0.0.1#10053
        - --addn-hosts=/root/hosts.dnsmasq
        ...
        volumeMounts:
        - name: kube-dns-hosts
          mountPath: /root
```

### 更新dnsmasq

dnsmasq不会主动监听hosts内容变更。所以在变更后，需主动通知dnsmasq更新，通过发送SIGHUP信号到dnsmasq同志其变更重新加载配置但不重启。

ref: http://www.thekelleys.org.uk/dnsmasq/docs/dnsmasq-man.html

```
When it receives a SIGHUP, dnsmasq clears its cache and then re-loads /etc/hosts and /etc/ethers and any 
file given by --dhcp-hostsfile, --dhcp-hostsdir, --dhcp-optsfile, --dhcp-optsdir, --addn-hosts or --
hostsdir. The dhcp lease change script is called for all existing DHCP leases. If --no-poll is set SIGHUP 
also re-reads /etc/resolv.conf. SIGHUP does NOT re-read the configuration file.
```

宿主机执行
```
kill -1 $(ps -ef | grep "sbin/dnsmasq" | grep -v grep | awk '{print $2}')
```



### 问题: configmap更新延迟

ConfigMap更新频率被 kubelet --sync-frequency 控制。默认1 min, 更新生效通常在0~1 min之间。 


```
--sync-frequency duration
Max period between synchronizing running containers and config (default 1m0s) (DEPRECATED: This parameter should be set via the config file specified by the Kubelet's --config flag. See https://kubernetes.io/docs/tasks/administer-cluster/kubelet-config-file/ for more information.)
```



