---

layout: post
title: "Lesson learn_1"
date: 2020-07-09
tag: 车身电子


---

### 问题描述：

某平台配置PEPS车辆，停车熄火，6S内无法再次启动车辆

### 问题原因分析：

车辆启动逻辑：SSB开关按下，PEPS检测钥匙，检测到钥匙，电源模式变为ON，PEPS检测刹车开关硬线信号和P/N档信号，等待EMS challenge请求，2S内收到challenge请求后，PEPS与EMS进行防盗认证，认证通过PEPS发送response数据给EMS，EMS进行防盗认证，PEPS等待EMS防盗认证结果，认证通过，PEPS收到防盗认证标志pass，PEPS&BCM切换档位CRANK，PEPS发出CRANK Request给EMS启动发动机，PEPS在15S内收到发动机Running信号电源切换档位至RUN。

防盗规范逻辑：车辆熄火，6S内，SSB开关启动车辆，EMS不发起挑战，无需鉴权；6S之后启动车辆EMS需发起挑战，然后鉴权通过之后，启动发动机；

**问题原因：**EMS按照防盗逻辑开发，但是PEPS并未未严格按照防盗规范逻辑开发，这导致在熄火之后，PEPS一直等待EMS发起挑战，然而EMS在6S内不发挑战；

### 不足分析：

1、P造车软件仅针对变更点测试，测试不够充分，且测试经验不足，造成问题遗漏；

2、其他平台出现问题，未同步测试，造成问题保持至今；

3、供应商未提供自检报告（当时未严格执行自检报告制度）；

### 改进的方向：

1、收到软件，严格考核release note及自检报告；

2、测试计划安排，保证关键开阀节点进行全功能测试；

3、所有平台溢出问题共享，溢出问题在其他平台进行同步测试；

### 团队建议:

1、积极参与问题共享，针对共享问题多思考，负责项目有没有该类问题；

 2、测试不能放松，对于软件时刻提高警惕，有客户意识；