---
layout: layout.pug
navigationTitle:  服务
title: 服务
menuWeight: 2
excerpt: 使用“服务”菜单
render: mustache
model：/mesosphere/dcos/1.13/data.yml
---

“服务”页面为本地 DC/OS Marathon 实例提供了完整的功能界面。其全面展示正在运行的所有服务。您可以按健康状况、状态或服务名称筛选服务。

![Services](/mesosphere/dcos/1.13/img/services-ee.png)

图 1 - 服务页面

默认显示所有服务，并按服务名称排序。也可以按运行状况、版本、区域、实例、CPU、磁盘空间或 GPU 的使用情况对服务进行排序。

| 名称 | 说明 |
|----------------|------------------|
| 名称 | 服务的 DC/OS 服务名称 |
| [状态](#service-status) | 服务状态。请参阅下表中的详细信息。|
| 版本 | 服务版本 |
| 地区 | 服务分域 |
| 实例 | 服务实例的数量|
| CPU | 使用的 CPU 数量 |
| 内存 | 使用的内存量 |
| 磁盘 | 使用的磁盘空间量 |
| GPU | 使用的 GPU 数量 |

## 服务状态

| 状态 | 描述 |
|----------|----------------|
| 运行 | 服务报告为运行，且没有报告为部署或恢复的实例。 |
| 部署 | 当您请求更改服务时，DC/OS 会执行尚未完成的必要操作。如果服务难以进入运行状态，就会显示警告图标。这表示服务正在等待其运行所需的资源邀约，或者短时间内有过多任务失败。可以从 [调试](#debug) 选项卡获取更多信息。 |
| 恢复| 当 DC/OS 请求对服务进行更改时，实例都将被关闭并启动新实例。与部署相似，DC/OS 正在执行规定操作，但尚未完成。 |
| 已停止 | 目标实例为 0 且运行任务计数为 0 的服务。此状态之前在 UI 中被称为“暂停”。 |

## SDK 服务状态 

基于 [DC/OS SDK](https://mesosphere.github.io/dcos-commons/) 的调度程序任务正在利用 Mesos 本地检查，以便提供比上述 [服务状态](#service-status) 更详细的有关其状态的信息。这些状态特定于基于 SDK 的调度程序及其生命周期。

| 状态 | 描述 |
|----------|----------------|
| 正在初始化 | 调度程序正在初始化。 |
| 运行 | 所有受监控计划均已完成。 |
| 创建服务时出错 | 调度程序在创建服务时遇到错误。 |
| 部署（等待资源） | 一个或多个受监控计划正在部署（等待资源）。|
| 部署 | 一个或多个受监控计划正在部署。 |
| 部署（等待用户输入） | 一个或多个受监控计划在等待用户输入。 |
| 已降级（等待资源） | 一个或多个受监控计划已降级（等待资源）。|
|已降级（正在恢复） | 一个或多个受监控计划已降级（正在恢复）。|
| 备份 | 一个或多个受监控的备份计划正在进行中。 |
| 恢复 | 一个或多个受监控的恢复计划正在进行中。 |
| 服务不可用 | 调度程序遇到一个或多个受监控计划的错误。 |

## 选项卡

单击服务名称，打开“服务实例”页面。“服务实例”页面将有关服务的信息组织在五个选项卡下方。每个选项卡都以易于查看的列表形式列出了服务的配置和性能信息。

![Instances](/mesosphere/dcos/1.13/img/services-instances-panel.png)

图 2 - 服务实例 



| 选项卡 | 描述 |
|------------------|----------------|
| 任务 | 对于每个任务，还有关于其分区、分域、状态、运行状况以及最后更新时间的信息。单击任务以查看其完整配置、工作目录和日志。  |
| 配置 | 服务和网络配置变量。 |
| <a name="debug"></a>调试 |  显示任务统计信息以帮助您排除群集问题。 |
| 端点 | 服务配置变量，例如容器镜像、容器运行时和高级网络设置。 |
| 计划 | 显示服务的所有部署计划，以便跟踪当前运行或已完成服务的状态。下拉菜单可让您在计划之间切换。 |

对于带有 UI 的服务，将鼠标悬停在服务名称上并单击 ![open service](/mesosphere/dcos/1.13/img/open-service.png) 查看服务。您可以在 `<hostname>/mesos` 访问 Mesos UI。

# 使用 UI 调试服务部署

**服务 > 调试** 选项卡显示上次更改、任务故障以及其他状态消息，这有助于调试服务部署的问题。

在下图中，Marathon 无法启动服务；DC/OS 显示警告消息，然后一条消息表示错误已清除，服务现在正在启动。

![故障警告](/mesosphere/dcos/1.13/img/GUI-Services-Failure-To-Launch.png)

图 3 - 显示警告的调试选项卡