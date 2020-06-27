---
linkTitle: "k3s"
title: "k3s"
weight: 1
description: "安装 k3s。"
---

因为使用习惯问题，我们使用 Docker 作为 Kubernetes 容器运行时（k3s 默认使用 `containerd`），并缺省安装 `traefik`、`servicelb`、`coredns`、`local-storage`、`metrics-server` 等。

## 准备

安装 k3s 前需要先开启 cgroup memory。

```bash
echo "cgroup_memory=1 cgroup_enable=memory">>/boot/cmdline.txt
```

中国大陆用户执行下面的命令安装：

```bash
curl -sfL https://docs.rancher.cn/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn K3S_KUBECONFIG_MODE="666" INSTALL_K3S_EXEC="server --docker" sh -
```

其他地区的用户使用下面的命令安装：

```bash
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="666" INSTALL_K3S_EXEC="server --docker" sh -
```

安装完成后 k3s 会自动启动，并为你安装好了 `kubectl`，现在你可以使用 `kubectl` 来访问和管理你的 Kubernetes 集群了。

## 卸载

执行下面的卸载 k3s 及相关容器。

```bash
k3s-uninstall.sh
docker rm -f $(docker ps -qa)
```

## 参考

- [k3s - 5 less than k8s - docs.rancher.cn](https://docs.rancher.cn/k3s/)
