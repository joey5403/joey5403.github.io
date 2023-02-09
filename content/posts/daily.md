+++
title = "2023工作日志"
date = 2023-01-03T00:00:00+08:00
draft = false
+++

## 2023 JANUARY {#2023-january}


### 0103 TUE {#0103-tue}


#### 灰度推进进度计划 <span class="tag"><span class="____">技术文档</span></span> {#灰度推进进度计划}


#### 专利文档 {#专利文档}


### 0104 WED {#0104-wed}


#### 投标会 <span class="tag"><span class="__">会议</span></span> {#投标会}


#### 灰度平台讨论会 <span class="tag"><span class="__">会议</span></span> {#灰度平台讨论会}


### 0105 THU {#0105-thu}


#### 接口测试讨论会 <span class="tag"><span class="__">会议</span></span> {#接口测试讨论会}


#### 对公平台微服务讨论 <span class="tag"><span class="__">会议</span></span> {#对公平台微服务讨论}


#### organization-rest服务CPU满载问题分析 <span class="tag"><span class="____">问题分析</span></span> {#organization-rest服务cpu满载问题分析}


#### travel-server编译问题分析 <span class="tag"><span class="____">问题分析</span></span> {#travel-server编译问题分析}


### 0106 FRI {#0106-fri}


#### 灰度后续推进计划讨论 <span class="tag"><span class="__">会议</span></span> {#灰度后续推进计划讨论}


#### 配置平台功能点讨论 <span class="tag"><span class="__">会议</span></span> {#配置平台功能点讨论}


#### 迭代周期统一后的发版逻辑讨论 <span class="tag"><span class="__">会议</span></span> {#迭代周期统一后的发版逻辑讨论}


#### 线上注入异常问题支持 <span class="tag"><span class="____">问题分析</span></span> {#线上注入异常问题支持}


#### 流量染色机制设计及调研 <span class="tag"><span class="____">技术预研</span></span> {#流量染色机制设计及调研}


### 0109 MON {#0109-mon}


#### EntityList分表查询异常分析 <span class="tag"><span class="____">协助研发</span><span class="____">问题分析</span></span> {#entitylist分表查询异常分析}

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2023-01-09 Mon 15:22] </span></span> <br />
    找不到datalink_dataLink表对应的分表，
    因为没有指定corporationId或者没有指定context.CorporationId
    问题原因：
    定时任务中使用分表的entityList不能自动传入corporationId
    解决办法:

    1.  在查询前用

    contextCorporationId.set(staff.corporationId())
    设置contextCorporationId

    1.  改用querybuilder,使用from的时候传corporationId


#### $creatTime字段查询分析 {#creattime字段查询分析}

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2023-01-09 Mon 15:25] </span></span> <br />
    不支持使用$createTime字段查询


#### swagger-ui请求404分析 {#swagger-ui请求404分析}

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2023-01-09 Mon 15:25] </span></span> <br />
    配置需放在jersey内
    已修改使用手册


#### 合同变更技术方案沟通确认 <span class="tag"><span class="__">会议</span></span> {#合同变更技术方案沟通确认}


#### release环境rpc请求异常分析 {#release环境rpc请求异常分析}


#### hw环境maxwell配置确认 {#hw环境maxwell配置确认}


### 0110 TUE {#0110-tue}


#### 灰度系统讨论会 {#灰度系统讨论会}


#### 分布式事务讨论会 {#分布式事务讨论会}


### 0111 WED {#0111-wed}


#### 电档测试环境启动失败分析 {#电档测试环境启动失败分析}


#### 二航局请求失败分析 {#二航局请求失败分析}


#### 原生环境release-rest-server出现CPU满载 {#原生环境release-rest-server出现cpu满载}


### 0112 THU {#0112-thu}


#### porlarDB沟通会 {#porlardb沟通会}


#### swagger返回值支持 {#swagger返回值支持}


#### 灰度定时任务执行异常处理 {#灰度定时任务执行异常处理}


#### 数科ruby插件打包处理 {#数科ruby插件打包处理}


### 0113 FRI {#0113-fri}


#### 数科ruby插件打包处理 {#数科ruby插件打包处理}


### 0116 MON {#0116-mon}


#### swagger压测 {#swagger压测}


#### 档案关系回滚会 {#档案关系回滚会}


#### 1:1沟通会 {#1-1沟通会}


### 0117 TUE {#0117-tue}


#### organization后续优化分析 {#organization后续优化分析}


#### swagger相关代码改动测试方案确定 {#swagger相关代码改动测试方案确定}


### 0118 WED {#0118-wed}


#### swagger注解导致多语言检查失败 {#swagger注解导致多语言检查失败}


#### grayCheck检查失败 {#graycheck检查失败}


#### hotfix环境任务执行失败排查 {#hotfix环境任务执行失败排查}


### 0131 TUE {#0131-tue}


#### 线上UNKNOWN报错分析 {#线上unknown报错分析}


#### 灰度一天的方案讨论 {#灰度一天的方案讨论}


#### OKR准备 {#okr准备}


#### exile架构讲解 {#exile架构讲解}


#### release环境升级maxwell解析 {#release环境升级maxwell解析}


#### 华为环境割接方案讨论 {#华为环境割接方案讨论}


### 0201 WED {#0201-wed}


#### maxwell代码合并 {#maxwell代码合并}


#### maxwell打包、测试 {#maxwell打包-测试}


#### polarDB沟通会 {#polardb沟通会}

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2023-02-01 Wed 19:58] </span></span> <br />
    1.  polarDB 8.0.2
    2.  dts 经常断联
    3.  源地址切换一直卡在切换中
    4.  在正式切换时可以申请阿里支援
    5.  切换maxwell 三清
    6.  使用期间的扩容
    7.  并行度在页面中的设置实时生效，在参数中的设置需要重新建立链接生效
    8.  创建虚拟列&amp;创建索引的速度测试
    9.  分区表分区测试
    10. 私有化场景，可以提供部署


#### 灰度一天的方案讨论会 {#灰度一天的方案讨论会}


### 0202 THU {#0202-thu}


#### maxwell启动异常处理 {#maxwell启动异常处理}


#### OKR讨论会 {#okr讨论会}


#### gradle覆盖率检查支持 {#gradle覆盖率检查支持}


### 0203 FRI {#0203-fri}


#### 华为云沟通会 {#华为云沟通会}


#### gaussDB兼容性问题排查 {#gaussdb兼容性问题排查}


#### 双周会 {#双周会}


### 0206 MON {#0206-mon}


#### swagger response上线及回滚 {#swagger-response上线及回滚}


#### gaussDB兼容性问题支持 {#gaussdb兼容性问题支持}


#### 分区表设计文档 {#分区表设计文档}


### 0207 TUE {#0207-tue}


#### 分区表设计文档 {#分区表设计文档}


#### org缩容分析 {#org缩容分析}


#### 分区表讨论 {#分区表讨论}


### 0208 WED {#0208-wed}


#### swagger问题压测支持 {#swagger问题压测支持}


#### polarDB升级方案讨论 {#polardb升级方案讨论}


#### gaussDB需求讨论 {#gaussdb需求讨论}


#### 架构讲解文档准备 {#架构讲解文档准备}


#### 架构讲解 {#架构讲解}

-   Note taken on <span class="timestamp-wrapper"><span class="timestamp">[2023-02-09 Thu 15:36] </span></span> <br />
    创建业务对象大图
    链路大图
    对象模型合理性
    框架&amp;detail规范


### 0209 THU {#0209-thu}


#### 商城酒店最低价问题讨论 {#商城酒店最低价问题讨论}


#### OB分区表测试 {#ob分区表测试}


#### 绩效结果沟通 {#绩效结果沟通}


####  {#d41d8c}
