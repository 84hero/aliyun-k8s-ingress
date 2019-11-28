# 阿里云创建基于私网`SLB`的 `Ingress`

- `ingress-controller.yml.j2` 基于阿里云官方模板

- `ingress-controller.yml` 基于阿里云官方模板创建的`ingress` `yml`文件

- `ingress-controller-kube-system-vpc.yml` 基于`ingress-controller.yml`修改的`ingress` `yml`文件
   在 `kube-system`命名空间下面创建了一个基于私网`SLB`的`Ingress`
   通过修改相关资源名称，增加唯一后缀，实现相同`namespace`多个`Ingress`并存。


# 使用方法

- 基于官方模板生成`ingress-controller.yml`文件

```
jinja2 -D Namespace='NAMESPACE' -D LoadbalancerID='SLB_ID' -D IngressClass='INGRESS_CLASS' ingress-controller-template.yml.j2 > ingress-controller.yml
```

- 或者使用现有的`ingress-controller-kube-system-vpc.yml`

```
   namespace: kube-system 替换成 namespace: 你的命名空间
```

```
   lb-xxxxxxxxxx 替换成你的私网 SLB 实例 ID
```

```
   k8s-ingress-ali-slb 替换成你希望定义的 Ingress-class 名称
```

```
   ali-slb 替换成你的唯一后缀
```

## 有时间的朋友可以修改官方的`j2`模板，增加个后缀或者前缀，就不需要手动修改生成后的模板

## 副作用暂时没发现，有了解的麻烦告知我。

## 来自阿里教程

```
https://yq.aliyun.com/articles/645856
```
