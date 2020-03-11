# Kubernetes学习笔记

> 参考书籍：[《Kubernetes in Action中文版》](https://book.douban.com/subject/30418855/)。

[TOC]

## 1. 介绍

### 1.1. 定义

Kubernetes是一个容器的自动调度、配置、监管、故障处理工具。

### 1.2 Kubernetes集群架构
- 主节点：
    - API Server。
    - Scheculer：调度器。
    - Controller
    - Manager：执行集群级别的功能。
    - etcd：持久化配置存储。
- 工作节点：
    - 容器（Docker、rtk）。
    - kubelet：与API 
    - Server通信，管理所在节点的容器。
    - kube-proxy：负载均衡、网络流量。

## 2. 容器

### 2.1. 容器的定义

1. 基于Linux。
2. 类似虚拟机，开销＜虚拟机。
3. 容器进程实际运行在宿主机，但对进程本身，自身为宿主机唯一进程。
4. 无须硬件（如CPU）虚拟化；不支持跨内核、平台（x86/ARM）兼容。

### 2.2. 容器隔离原理

1. Linux命名空间。
2. Linux控制租（资源限制）。

## 2. Pod

### 2.1. Pod的定义

一个Pod是一组紧密相关的容器，总是运行在同一个工作节点上，以及同一个Linux命名空间中；Pod类似独立逻辑机器，拥有自己的IP、主机名、进程等。

#### 2.2. 使用Pod的原因

- 进程间通信。
- 进程间资源共享。
- 单个进程中运行多个进程不合理。

#### 2.3 Pod的基本用法

- YAML定义：

    ```yaml
    apiVersion: V1
    kind: Pod
    metadata:
      name: kubia-manaual
    spsc:
      containiers:
        - image: luksa/kubia
          name: kubia
          port:
            - containerPort: 8080
              protocol: TCP
    ```
- 创建：
    ```bash
    kubectl create -f kubia-manual.yaml
    ```
- 导出：
    ```bash
    kubectl get po kubia-manual -o yaml
    ```
- 获取列表：
    ```bash
    kubectl get pods
    ```
- 查看日志：
    ```bash
    kubectl logs kubia-manaual -c kubia
    ```
- 转发请求（主要用于测试）：
    ```bash
    kubectl port-forward kubia-manual 8888:8080
    ```
## 3. 标签

### 3.1. 定义

标签可以组织Pod和其他资源。

### 3.2. 标签的基本用法

1. **YAML：**
    ```yaml
    metadata:
      labels:
        creation_method: manual
        env: prod
    ```
2. **获取Pod的标签：**
    ```bash
    kubectl get po --show-labels
    ```
    列出指定标签：
    ```bash
    kubectl get po -L creation_method,env
    ```
3. **添加标签**：
    ```bash
    kubectl label po kubia-manual gpu＝true
    ```
4. **修改标签**:
    ```bash
    kubectl label po kubia-manual env=debug --overwrite
    ```
5. **标签选择器**：
    - 常规：`env=prod`
    - 包含：`env`
    - 不含：`'!env'`
    - 非非：`'env!=prod'`
    - 属于：`'env in (prod,debug)'`
    - 不属：`'env notin (prod,debug)'`
6. **将Pod调度至指定节点**
    ```yaml
    ...
    spec:
      nodeSelector:
        gpu: "true"
    ...
    ```
## 4. 命名空间

### 4.1 命名空间的基本用法、

1. YAML定义：
    ```yaml
    apiVersion: v1
    kinds: Namespsce
    metadata:
      name: custom-namespace
    ```
2. 命令创建命名空间：
    ```bash
    kubectl create namespace custom-namespace
    ```
3. 在指定的命名空间创建资源：
    ```bash
    kubtctl create -f kubia-manual.yaml -n namespace
    ```
4. 获取命名空间列表：
    ```bash
    kubectl get ns
    ```
5. 获取指定命名空间中的资源列表：
    ```bash
    kubectl get po -n kubia-system
    ```
6. 删除命名空间（会删除里面的资源)：
    ```bash
    kubectl delete ns custonm-namespace
    ```