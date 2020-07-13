# 说明
通过 Filebeat 收集 Pod 日志

## 先决条件
- Kubernetes 1.10+ 

## 使用 helm 安装

安装名称为：`my-release`:
```
helm install --name my-release Helm-Filebeat_Pod_Logs
```

此命令默认安装部署 akiraka 与 filebeat 容器
> 列出所有使用的版本 `helm list`

## 卸载
卸载名称为：`my-release`:
```bash
$ helm uninstall my-release
```

## 配置
下表列出可配置参数及其默认值。

参数                                       | 描述                                                         | 默认
------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------
`shareConfig.affinity`                     | 亲和性                                                       | `{}`
`shareConfig.tolerations`                  | 配置可以容忍的节点                                           | `[]`
`shareConfig.replicaCount`                 | 副本数量                                                     | `1`
`shareConfig.nodeSelector`                 | 配置节点调度                                                 | `{}`
`nameOverride`                             | 名称                                                         | `""`
`serviceAccount`                           | 认证信息                                                     | `""`
`ingress.enabled`                          | 是否启用 ingress                                             | `false`
`imagePullSecrets`                         | 私有仓库秘钥                                                 | `[]`
`fullnameOverride`                         | 则默认为".Release.Name-.Values.nameOverride 或 .Chart.Name"  | `""`
`customApp.enabled`                        | 是否启用 customApp                                           | `true`
`customApp.appName`                        | 应用名称                                                     | `tomcat`
`customApp.image.repository`               | 使用镜像名称                                                 | `akiraka`
`customApp.image.tag`                      | 镜像版本                                                     | `8.5.51`
`customApp.image.pullPolicy`               | 镜像拉取策略                                                 | `IfNotPresent`
`customApp.service.type`                   | Kubernetes service type                                      |  `ananwaresystems/webarchive`
`customApp.service.port`                   | Kubernetes service port                                      | `ClusterIP`
`cystomAPP.extraPorts`                     | 额外端口，端口不够额外端口来凑                               | `详情查看 values.yaml`
`customApp.livenessProbe`                  | 判断容器是否存活                                             | `详情查看 values.yaml`
`customApp.readinessProbe`                 | 判断容器是否启动完成                                         | `详情查看 values.yaml`
`customApp.extraVolumeMounts`              | 容器内挂载点，名称                                           | `null`
`customApp.extraVolumeMounts.name`         | 容器内挂载点，将日志目录挂载给 Filebeat                      | `akiraka-logs`
`customApp.extraVolumeMounts.mountPath`    | 容器内挂载点，挂载目录                                       | `/usr/local/akiraka/logs`
`customApp.extraVolumeMounts.readOnly`     | 容器内挂载点，是否只读                                       | `false`
`customApp.resources`                      | CPU 内存 资源设置                                            | `{}`
`customApp.securityContext`                | 定义 Pod 安全上下文                                          | `fsGroup: 1000`
`customApp.containerEnv`                   | 定义 Pod 环境变量                                          | `详情查看 values.yaml`
`filebeat.enabled`                         | 是否启用 Filebeat                                            | `true`
`filebeat.appName`                         | 应用名称                                                     | `tomcat`
`filebeat.image.repository`                | Filebeat 镜像名称                                            | `elastic/akiraka`
`filebeat.image.tag`                       | Filebeat 镜像版本                                            | `7.6.1`
`filebeat.image.pullPolicy`                | 镜像拉取策略                                                 | `IfNotPresent`
`filebeat.filebeatConfig`                  | filebeat.yaml                                                | `详情查看 values.yaml`
`filebeat.enabled`                         | 是否启用 Filebeat                                            | `true`
`filebeat.extraVolumeMounts`               | 容器内挂载点，名称                                           | `null`
`filebeat.extraVolumeMounts.name`          | 容器内挂载点，将日志目录挂载给 Filebeat                      | `akiraka-logs`
`filebeat.extraVolumeMounts.mountPath`     | 容器内挂载点，挂载目录                                       | `/usr/local/akiraka/logs`
`filebeat.extraVolumeMounts.readOnly`      | 容器内挂载点，是否只读                                       | `true`
`filebeat.resources`                       | CPU 内存 资源设置                                            | `{}`
`filebeat.securityContext`                 | 定义 Pod 安全上下文                                          | `fsGroup: 1000`
`filebeat.livenessProbe`                   | 判断容器是否存活                                             | `详情查看 values.yaml`
`filebeat.livenessProbe.enabled`           | 是否开启容器存活检测                                         | `false`
`filebeat.readinessProbe`                  | 判断容器是否启动完成                                         | `详情查看 values.yaml`
`filebeat.readinessProbe.enabled`          | 是否开启容器存活检测                                         | `false`