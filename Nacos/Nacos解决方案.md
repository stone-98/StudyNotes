# Nacos-Client移除Prometheus依赖方案

## 引言

### 背景与目的

目前Nacos-Client作为一个SDK应用，它与Prometheus依赖强行绑定。对于一个SDK插件应尽量减少依赖第三方依赖的可能性，使得SDK更加精简并且减少依赖冲突的可能性。此设计的目的则是为了解除Nacos-Client与Prometheus依赖依赖的强行绑定关系。

### 设计思路

目前开源领域关于Metrics已有许多实现，例如：
- Micrometer
- Netflix-Spectator
- Dropwizard-Metrics
- Dubbo-Metrics
- ...

这些度量指标实现在设计和功能上各有特点，以满足不同的应用场景和需求。它们旨在提供简单易用、高效可靠的度量指标收集和报告机制。

#### metrics-plugin

基于Nacos Plugin机制新增Nacos-SDK指标插件（metrics-plugin），用于定义公共接口以及实现，如下：

- Metric：用于标识度量器，以及提供度量器公共的抽象
- Gauge：用于表示一个可变的数值。它通常用于表示系统的当前状态或某个指标的实时值。
- Counter：Counter是一个简单的累加器，用于记录一个事件发生的次数或某个操作执行的次数。
- Histogram：用于度量和统计数据分布的工具。它将一组数据分成不同的桶（buckets），每个桶代表一个数值范围，并记录落入该范围的数据点数量。直方图可以用于测量数据的分布情况，
- 其他度量器接口
- Registry：定义公共的指标注册器，用于注册和获取指标。
- MetricsAdapter：定义适配器接口，用于将自定义的Metric转化为第三方监控系统的Metrics。
- MetricManager：用于加载以及获取Metric的实现。
- RegistryManager：用于加载以及获取Registry的实现。
- MetricsAdapterManager：用于加载以及获取MetricsAdapter的实现。
- CompactGauge：提供默认实现。
- CompactCounter：提供默认实现。
- CompactHistogram：提供默认实现。
- 其他默认实现
- CompactRegistry：提供默认实现。

对于度量器的具体实现暂未给出更详细的描述，主要参考一些开源的实现。

#### 提供对metrics-plugin插件的实现prometheus-metrics-adapter：

- PrometheusMetricsAdapter：提供对MetricsAdapter的实现，用于将CompactMetrics转化为PrometheusMetrics

#### 如何使用

Nacos-Client默认不引入插件的实现，也就是用户在不使用相关的指标时，不对样本进行存储，如需要使用相关指标数据，例如用户需要获取Nacos-Client的指标数据导出到Prometheus时，用户自行导入相关依赖，通过PrometheusAdapter将数据转为Prometheus的指标结构用于导出。

#### 流程图

![img.png](https://cxyzyw-site.oss-cn-beijing.aliyuncs.com/images202307172205630.png)

Nacos-Client通过Metric将指标记录到MetricRegistry，然后根据对应的Adapter将Metric适配成第三方需要的指标结构，以便用户使用

### 如何扩展

#### 如果需要支持将自定义的Metrics转化为其他第三方的Metrics

自行实现MetricsAdapter

#### 后期如果需要支持其他度量类型

实现Metric接口进行扩展

#### 如果不希望使用CompactRegistry

对Registry进行实现扩展一个新的Registry库，

