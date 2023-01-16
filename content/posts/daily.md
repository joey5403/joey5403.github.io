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
