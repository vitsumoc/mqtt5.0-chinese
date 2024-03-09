---
title: MQTT 5.0 中文文档
url: mqtt-v5-0-chinese
date: 2024-01-06 10:14:39
categories:
- MQTT
tags:
- MQTT
- 网络协议
---

> 原文 [MQTT Version 5.0](https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html)
> **\[mqtt-v5.0]**
> MQTT Version 5.0. Edited by Andrew Banks, Ed Briggs, Ken Borgendale, and Rahul Gupta. 07 March 2019. OASIS Standard. https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html. Latest version: https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html.

<!-- more -->

<head>
  <style>
    :root {
      --vc-marked: #ffc107;
      --vc-referred: #EE0000;
    }
    [data-user-color-scheme="dark"] {
      --vc-marked: #886c57;
      --vc-referred: #EE0000;
    }
    .bold {
      font-weight: bold;
    }
    .vcLinked {
      color: var(--post-link-color);
    }
    .vcMarked {
      background: var(--vc-marked);
    }
    .vcReferred {
      color: var(--vc-referred);
    }
    .vcTrans {
      font-size: 0.8rem;
      font-style: italic;
    }
  </style>
</head>

# MQTT 5.0

OASIS 标准

2019年3月7日

## 规范 URIs

### 此版本

https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.docx (权威性)
https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html
https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.pdf

### 前一版本

http://docs.oasis-open.org/mqtt/mqtt/v5.0/cos01/mqtt-v5.0-cos01.docx (权威性)
http://docs.oasis-open.org/mqtt/mqtt/v5.0/cos01/mqtt-v5.0-cos01.html
http://docs.oasis-open.org/mqtt/mqtt/v5.0/cos01/mqtt-v5.0-cos01.pdf

### 最新版本

https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.docx (权威性)
https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html
https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.pdf

### 技术委员会

[OASIS Message Queuing Telemetry Transport (MQTT) TC](https://www.oasis-open.org/committees/mqtt/)

### 主席

Richard Coppen (coppen@uk.ibm.com), [IBM](http://www.ibm.com/)

### 编辑

Andrew Banks (andrew_banks@uk.ibm.com), [IBM](http://www.ibm.com/)
Ed Briggs (edbriggs@microsoft.com), [Microsoft](http://www.microsoft.com/)
Ken Borgendale (kwb@us.ibm.com), [IBM](http://www.ibm.com/)
Rahul Gupta (rahul.gupta@us.ibm.com), [IBM](http://www.ibm.com/)
  
### 相关工作

本规范取代：

- *MQTT 3.1.1*  由 Andrew Banks 和 Rahul Gupta 编辑发布与 2014年10月29日。 OASIS 标准 http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html 最新版本：http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html

本规范涉及：

- *MQTT and the NIST Cybersecurity Framework Version 1.0* 由 Geoff Brown 和 Louis-Philippe Lamoureux 编辑发布。最新版本： http://docs.oasis-open.org/mqtt/mqtt-nist-cybersecurity/v1.0/mqtt-nist-cybersecurity-v1.0.html

### 简介

MQTT 是一个 客户端/服务器 架构，采用 订阅/发布 模式的消息传输协议。是一套轻量级的、开放的、简单且易于实现的标准。这些特性使得他适用于多种场景，包括一些资源受限的场景比如机器和机器之间的通信（M2M）或是物联网（IoT）场景，这些场景要求较小的代码空间占用，或是网络带宽非常珍贵。

MQTT 基于 TCP/IP 或其他提供了顺序、无包丢失、双向链接的网络协议。MQTT 的特性包括：

- 通过 订阅/发布 模式实现一对多的消息传输和应用程序解耦。
- 与负载内容无关的消息传输。
- 三种不同服务质量(QoS)的消息传输：
  - 至多一次(At most once)，根据操作环境情况尽最大努力来传输消息，消息可能会丢失。例如这种模式可以用于传感器数据采集，单次的消息的丢失并不重要，因为下一个消息很快就会到来。
  - 至少一次(At least once)，可以确保消息到达，但是可能会造成消息重复。
  - 确保一次(Exactly once)，可以确保消息只到达一次，例如这种消息可以用于账单交易信息，在交易场景下消息的丢失或者重复处理都会带来糟糕的后果。
- 小型的协议头，用来降低网络负载。
- 当发生异常断开时通知相关方的机制。

### 状态

本文档最后一次修订的日期和级别都已经在前文中描述。检查[最新版本](#最新版本)位置了解本文档后续可能的修订版。技术委员会(TC)制作的其他版本文档或其他技术项目均在此提供 https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt#technical

技术委员会成员应将对此文档的评论发送至技术委员会邮件列表，其他人需在技术委员会的网站(https://www.oasis-open.org/committees/mqtt/)订阅公共评论列表后，通过点击[发送评论](https://www.oasis-open.org/committees/comments/index.php?wg_abbrev=mqtt)将评论发送至公共评论列表。

本规范是在 OASIS [知识产权政策](https://www.oasis-open.org/policies-guidelines/ipr)的 [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode)模式下提供的，该模式是技术委员会成立时选择的。关于是否有实施本规范依赖的已经披露的专利信息或是关于任何专利许可条款的信息，请参考技术委员会网站中的知识产权部分(https://www.oasis-open.org/committees/mqtt/ipr.php)。

请注意，本工作产品声明为规范的任何机器可读内容（[计算机语言定义](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsCompLang)）均以单独的纯文本文件提供。 如果任何此类纯文本文件与工作产品的散文叙述性文档中的显示内容之间存在差异，则以单独的纯文本文件中的内容为准。

### 引用格式

引用本规范时，需要使用如下引用格式：

**\[mqtt-v5.0]**

MQTT Version 5.0. Edited by Andrew Banks, Ed Briggs, Ken Borgendale, and Rahul Gupta. 07 March 2019. OASIS Standard. https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html. Latest version: https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html.

# 提示

Copyright © OASIS Open 2019. All Rights Reserved.

以下文本中所有 `大写` 术语均具有 `OASIS` 知识产权政策（the `OASIS IPR Policy`）中指定的含义。 完整的[政策](https://www.oasis-open.org/policies-guidelines/ipr)可以在 `OASIS` 网站上找到。

本文档及其译本可以被复制并提供给其他人，本文档的原文或对本文档的部分引用、评论、解释说明等衍生品的制作、复制、出版和分发均没有限制，但上述许可的前提条件是上述的版权说明和本节内容必须包括在此类副本和衍生品内。并且，对于本文档本身的内容不得做任何修改，包括删除版权申明或对 `OASIS` 的引用，除非是为了 `OASIS` 技术委员会为了制作某些文件或者交付成果的需要（在这种情况下，必须遵守 OASIS 知识产权政策中规定的适用于版权的规则）或是将本文档翻译为英语之外的其他语言。

上述授予的有限权限是永久性的，`OASIS` 或其继承者或受让人不会撤销。

本文档和此处包含的信息均按`原样`提供，`OASIS 不承担任何明示或暗示的保证，包括但不限于使用此处信息不会侵犯任何所有权的任何保证或任何暗示的保证商用能力或特定用途的适用性`。

`OASIS` 要求任何 `OASIS` 方或任何其他方认为其专利主张必然会因实施本 `OASIS` 委员会规范或 `OASIS` 标准而受到侵犯时，通知 OASIS 技术委员会管理员并表明其愿意向此类人员授予专利许可。 专利权利要求的方式与制定本规范的 `OASIS` 技术委员会的 IPR 模式一致。

`OASIS` 邀请任何一方联系 `OASIS` 技术委员会管理员，如果它知道任何专利权利要求的所有权主张，如果专利持有者不愿意使用与制定本规范的 `OASIS` 技术委员会的 `IPR` 模式一致的方式。 `OASIS` 可能会在其网站上包含此类声明，但不承担任何这样做的义务。

对于可能声称与本文档中描述的技术的实施或使用有关的任何知识产权或其他权利的有效性或范围，或者此类权利下的任何许可可能或可能不可用的范围，`OASIS` 不持任何立场 ; 他也不代表他已做出任何努力来确定任何此类权利。 有关 `OASIS` 与 `OASIS` 技术委员会制定的任何文件或交付物的权利有关的程序的信息，请参见 `OASIS` 网站。 可供发布的权利主张的副本以及可供使用的许可证的任何保证，或者本 `OASIS` 委员会规范的实施者或用户尝试获得使用此类专有权利的一般许可证或许可的结果，或 `OASIS` 标准，可从 `OASIS` 技术委员会管理员处获取。 `OASIS` 不声明任何信息或知识产权列表在任何时候都是完整的，也不声明该列表中的任何权利要求实际上是基本权利要求。

名称`“OASIS”`是 `OASIS`（本规范的所有者和开发者）的商标，仅用于指代该组织及其官方输出。 `OASIS` 欢迎参考、实施和使用规范，同时保留强制执行其标记以防止误导性使用的权利。 请参阅 https://www.oasis-open.org/policies-guidelines/trademark 了解上述指南。

# 目录

- 1 [介绍](#1-介绍)
  - 1.0 [知识产权政策](#1-0-知识产权政策)
  - 1.1 [MQTT规范结构](#1-1-MQTT规范结构)
  - 1.2 [术语表](#1-2-术语表)
  - 1.3 [规范性引用](#1-3-规范性引用)
  - 1.4 [非规范性引用](#1-4-非规范性引用)
  - 1.5 [数据表示](#1-5-数据表示)
    - 1.5.1 [比特位](#1-5-1-比特位)
    - 1.5.2 [2字节整数](#1-5-2-2字节整数)
    - 1.5.3 [4字节整数](#1-5-3-4字节整数)
    - 1.5.4 [UTF-8字符串](#1-5-4-UTF-8字符串)
    - 1.5.5 [变长整数](#1-5-5-变长整数)
    - 1.5.6 [二进制数据](#1-5-6-二进制数据)
    - 1.5.7 [UTF-8字符串对](#1-5-7-UTF-8字符串对)
  - 1.6 [安全性](#1-6-安全性)
  - 1.7 [编辑约定](#1-7-编辑约定)
  - 1.8 [变更历史](#1-8-变更历史)
    - 1.8.1 [MQTT v3.1.1](#1-8-1-MQTT-v3-1-1)
    - 1.8.2 [MQTT v5.0](#1-8-2-MQTT-v5-0)
- 2 [MQTT包格式](#2-MQTT包格式)
  - 2.1 [MQTT包结构](#2-1-MQTT包结构)
    - 2.1.1 [固定头](#2-1-1-固定头)
    - 2.1.2 [MQTT包类型](#2-1-2-MQTT包类型)
    - 2.1.3 [控制标识](2-1-3-控制标识)
    - 2.1.4 [剩余长度](#2-1-4-剩余长度)
  - 2.2 [可变头](#2-2-可变头)
    - 2.2.1 [包ID](#2-2-1-包ID)
    - 2.2.2 [属性集](#2-2-2-属性集)
      - 2.2.2.1 [属性长度](#2-2-2-1-属性长度)
      - 2.2.2.2 [属性](#2-2-2-2-属性)
  - 2.3 [载荷](#2-3-载荷)
  - 2.4 [原因码](#2-4-原因码)
- 3 [MQTT包](#3-MQTT包)
  - 3.1 [CONNECT - 连接请求](#3-1-CONNECT-连接请求)
    - 3.1.1 [CONNECT固定头](#3-1-1-CONNECT固定头)
    - 3.1.2 [CONNECT可变头](#3-1-2-CONNECT可变头)
      - 3.1.2.1 [协议名](#3-1-2-1-协议名)
      - 3.1.2.2 [协议版本](#3-1-2-2-协议版本)
      - 3.1.2.3 [连接标识](#3-1-2-3-连接标识)
      - 3.1.2.4 [全新开始](#3-1-2-4-全新开始)
      - 3.1.2.5 [遗嘱标识](#3-1-2-5-遗嘱标识)
      - 3.1.2.6 [遗嘱QoS](#3-1-2-6-遗嘱QoS)
      - 3.1.2.7 [遗嘱保留消息](#3-1-2-7-遗嘱保留消息)
      - 3.1.2.8 [用户名标识](#3-1-2-8-用户名标识)
      - 3.1.2.9 [密码标识](#3-1-2-9-密码标识)
      - 3.1.2.10 [保活时间](#3-1-2-10-保活时间)
      - 3.1.2.11 [CONNECT属性集](#3-1-2-11-CONNECT属性集)
        - 3.1.2.11.1 [属性长度](#3-1-2-11-1-属性长度)
        - 3.1.2.11.2 [会话过期间隔](#3-1-2-11-2-会话过期间隔)
        - 3.1.2.11.3 [接收最大值](#3-1-2-11-3-接收最大值)
        - 3.1.2.11.4 [最大包尺寸](#3-1-2-11-4-最大包尺寸)
        - 3.1.2.11.5 [主题别名最大值](#3-1-2-11-5-主题别名最大值)
        - 3.1.2.11.6 [请求响应信息](#3-1-2-11-6-请求响应信息)
        - 3.1.2.11.7 [请求问题信息](#3-1-2-11-7-请求问题信息)
        - 3.1.2.11.8 [用户属性](#3-1-2-11-8-用户属性)
        - 3.1.2.11.9 [认证方式](#3-1-2-11-9-认证方式)
        - 3.1.2.11.10 [认证数据](#3-1-2-11-10-认证数据)
      - 3.1.2.12 [可变头非规范性示例](#3-1-2-12-可变头非规范性示例)
    - 3.1.3 [CONNECT载荷](#3-1-3-CONNECT载荷)
      - 3.1.3.1 [客户端ID](#3-1-3-1-客户端ID)
      - 3.1.3.2 [遗嘱属性集](#3-1-3-2-遗嘱属性集)
        - 3.1.3.2.1 [属性长度](#3-1-3-2-1-属性长度)
        - 3.1.3.2.2 [遗嘱延迟间隔](#3-1-3-2-2-遗嘱延迟间隔)
        - 3.1.3.2.3 [载荷格式标识](#3-1-3-2-3-载荷格式标识)
        - 3.1.3.2.4 [消息过期间隔](#3-1-3-2-4-消息过期间隔)
        - 3.1.3.2.5 [内容类型](#3-1-3-2-5-内容类型)
        - 3.1.3.2.6 [响应主题](#3-1-3-2-6-响应主题)
        - 3.1.3.2.7 [关联数据](#3-1-3-2-7-关联数据)
        - 3.1.3.2.8 [用户属性](#3-1-3-2-8-用户属性)
      - 3.1.3.3 [遗嘱主题](#3-1-3-3-遗嘱主题)
      - 3.1.3.4 [遗嘱载荷](3-1-3-4-遗嘱载荷)
      - 3.1.3.5 [用户名](#3-1-3-5-用户名)
      - 3.1.3.6 [密码](#3-1-3-6-密码)
    - 3.1.4 [CONNECT动作](#3-1-4-CONNECT动作)
  - 3.2 [CONNACK - 连接确认](#3-2-CONNACK-连接确认)
    - 3.2.1 [CONNACK固定头](#3-2-1-CONNACK固定头)
    - 3.2.2 [CONNACK可变头](#3-2-2-CONNACK可变头)
      - 3.2.2.1 [连接回复标识](#3-2-2-1-连接回复标识)
        - 3.2.2.1.1 [会话展示](#3-2-2-1-1-会话展示)
      - 3.2.2.2 [连接原因码](#3-2-2-2-连接原因码)
      - 3.2.2.3 [CONNACK属性集](#3-2-2-3-CONNACK属性集)
        - 3.2.2.3.1 [属性长度](#3-2-2-3-1-属性长度)
        - 3.2.2.3.2 [会话过期间隔](#3-2-2-3-2-会话过期间隔)
        - 3.2.2.3.3 [接收最大值](#3-2-2-3-3-接收最大值)
        - 3.2.2.3.4 [最大QoS](#3-2-2-3-4-最大QoS)
        - 3.2.2.3.5 [保留消息可用](#3-2-2-3-5-保留消息可用)
        - 3.2.2.3.6 [最大包尺寸](#3-2-2-3-6-最大包尺寸)
        - 3.2.2.3.7 [分配的客户端ID](#3-2-2-3-7-分配的客户端ID)
        - 3.2.2.3.8 [主题别名最大值](#3-2-2-3-8-主题别名最大值)
        - 3.2.2.3.9 [原因字符串](#3-2-2-3-9-原因字符串)
        - 3.2.2.3.10 [用户属性](#3-2-2-3-10-用户属性)
        - 3.2.2.3.11 [通配符订阅可用](#3-2-2-3-11-通配符订阅可用)
        - 3.2.2.3.12 [订阅ID可用](#3-2-2-3-12-订阅ID可用)
        - 3.2.2.3.13 [共享订阅可用](#3-2-2-3-12-共享订阅可用)
        - 3.2.2.3.14 [服务器保活时间](#3-2-2-3-14-服务器保活时间)
        - 3.2.2.3.15 [响应信息](#3-2-2-3-15-响应信息)
        - 3.2.2.3.16 [服务引用](#3-2-2-3-16-服务引用)
        - 3.2.2.3.17 [认证方式](#3-2-2-3-17-认证方式)
        - 3.2.2.3.18 [认证数据](#3-2-2-3-18-认证数据)
    - 3.2.3 [CONNACK载荷](#3-2-3-CONNACK载荷)
  - 3.3 [PUBLISH - 发布消息](#3-3-PUBLISH-发布消息)
    - 3.3.1 [PUBLISH 固定头](#3-3-1-PUBLISH-固定头)
      - 3.3.1.1 [重复标识](#3-3-1-1-重复标识)
      - 3.3.1.2 [QoS](#3-3-1-2-QoS)
      - 3.3.1.3 [保留消息](#3-3-1-3-保留消息)
      - 3.3.1.4 [剩余长度](#3-3-1-4-剩余长度)
    - 3.3.2 [PUBLISH可变头](#3-3-2-PUBLISH可变头)
      - 3.3.2.1 [主题名称](#3-3-2-1-主题名称)
      - 3.3.2.2 [包ID](#3-3-2-2-包ID)
      - 3.3.2.3 [PUBLISH属性集](#3-3-2-3-PUBLISH属性集)
        - 3.3.2.3.1 [属性长度](#3-3-2-3-1-属性长度)
        - 3.3.2.3.2 [载荷格式标识](#3-3-2-3-2-载荷格式标识)
        - 3.3.2.3.3 [消息过期间隔](#3-3-2-3-3-消息过期间隔)
        - 3.3.2.3.4 [主题别名](#3-3-2-3-4-主题别名)
        - 3.3.2.3.5 [响应主题](#3-3-2-3-5-响应主题)
        - 3.3.2.3.6 [关联数据](#3-3-2-3-6-关联数据)
        - 3.3.2.3.7 [用户属性](#3-3-2-3-7-用户属性)
        - 3.3.2.3.8 [订阅ID](#3-3-2-3-8-订阅ID)
        - 3.3.2.3.9 [内容类型](#3-3-2-3-9-内容类型)
    - 3.3.3 [PUBLISH载荷](#3-3-3-PUBLISH载荷)
    - 3.3.4 [PUBLISH动作](#3-3-4-PUBLISH动作)
  - 3.4 [PUBACK - 发布确认](#3-4-PUBACK-发布确认)
    - 3.4.1 [PUBACK固定头](#3-4-1-PUBACK固定头)
    - 3.4.2 [PUBACK可变头](#3-4-2-PUBACK可变头)
      - 3.4.2.1 [PUBACK原因码](#3-4-2-1-PUBACK原因码)
      - 3.4.2.2 [PUBACK属性集](#3-4-2-2-PUBACK属性集)
        - 3.4.2.2.1 [属性集长度](#3-4-2-2-1-属性集长度)
        - 3.4.2.2.2 [原因字符串](#3-4-2-2-2-原因字符串)
        - 3.4.2.2.3 [用户属性](#3-4-2-2-3-用户属性)
    - 3.4.3 [PUBACK载荷](#3-4-3-PUBACK载荷)
    - 3.4.4 [PUBACK动作](#3-4-4-PUBACK动作)
  - 3.5 [PUBREC - 发布签收（QoS 2 交付第一部分）](#3-5-PUBREC-发布签收（QoS-2-交付第一部分）)
    - 3.5.1 [PUBREC固定头](#3-5-1-PUBREC固定头)
    - 3.5.2 [PUBREC可变头](#3-5-2-PUBREC可变头)
      - 3.5.2.1 [PUBREC原因码](#3-5-2-1-PUBREC原因码)
      - 3.5.2.2 [PUBREC属性集](#3-5-2-2-PUBREC属性集)
        - 3.5.2.2.1 [属性长度](#3-5-2-2-1-属性长度)
        - 3.5.2.2.2 [原因字符串](#3-5-2-2-2-原因字符串)
        - 3.5.2.2.3 [用户属性](#3-5-2-2-3-用户属性)
    - 3.5.3 [PUBREC载荷](#3-5-3-PUBREC载荷)
    - 3.5.4 [PUBREC动作](#3-5-4-PUBREC动作)
  - 3.6 [PUBREL - 发布释放（QoS-2-交付第二部分）](#3-6-PUBREL-发布释放（QoS-2-交付第二部分）)
    - 3.6.1 [PUBREL固定头](#3-6-1-PUBREL固定头)
    - 3.6.2 [PUBREL可变头](#3-6-2-PUBREL可变头)
      - 3.6.2.1 [PUBREL原因码](#3-6-2-1-PUBREL原因码)
      - 3.6.2.2 [PUBREL属性集](#3-6-2-2-PUBREL属性集)
        - 3.6.2.2.1 [属性长度](#3-6-2-2-1-属性长度)
        - 3.6.2.2.2 [原因字符串](#3-6-2-2-2-原因字符串)
        - 3.6.2.2.3 [用户属性](#3-6-2-2-3-用户属性)
    - 3.6.3 [PUBREL载荷](#3-6-3-PUBREL载荷)
    - 3.6.4 [PUBREL动作](#3-6-4-PUBREL动作)
  - 3.7 [PUBCOMP - 发布完成（QoS-2-交付第三部分）](#3-7-PUBCOMP-发布完成（QoS-2-交付第三部分）)
    - 3.7.1 [PUBCOMP固定头](#3-7-1-PUBCOMP固定头)
    - 3.7.2 [PUBCOMP可变头](#3-7-2-PUBCOMP可变头)
      - 3.7.2.1 [PUBCOMP原因码](#3-7-2-1-PUBCOMP原因码)
      - 3.7.2.2 [PUBCOMP属性集](#3-7-2-2-PUBCOMP属性集)
        - 3.7.2.2.1 [属性长度](#3-7-2-2-1-属性长度)
        - 3.7.2.2.2 [原因字符串](#3-7-2-2-2-原因字符串)
        - 3.7.2.2.3 [用户属性](#3-7-2-2-3-用户属性)
    - 3.7.3 [PUBCOMP载荷](#3-7-3-PUBCOMP载荷)
    - 3.7.4 [PUBCOMP动作](#3-7-4-PUBCOMP动作)
  - 3.8 [SUBSCRIBE - 订阅请求](#3-8-SUBSCRIBE-订阅请求)
    - 3.8.1 [SUBSCRIBE固定头](#3-8-1-SUBSCRIBE固定头)
    - 3.8.2 [SUBSCRIBE可变头](#3-8-2-SUBSCRIBE可变头)
      - 3.8.2.1 [SUBSCRIBE属性集](#3-8-2-1-SUBSCRIBE属性集)
        - 3.8.2.1.1 [属性长度](#3-8-2-1-1-属性长度)
        - 3.8.2.1.2 [订阅ID](#3-8-2-1-2-订阅ID)
        - 3.8.2.1.3 [用户属性](#3-8-2-1-3-用户属性)
    - 3.8.3 [SUBSCRIBE载荷](#3-8-3-SUBSCRIBE载荷)
      - 3.8.3.1 [订阅选项](#3-8-3-1-订阅选项)
    - 3.8.4 [SUBSCRIBE动作](#3-8-4-SUBSCRIBE动作)
  - 3.9 [SUBACK - 订阅确认](#3-9-SUBACK-–-订阅确认)
    - 3.9.1 [SUBACK固定头](#3-9-1-SUBACK固定头)
    - 3.9.2 [SUBACK可变头](#3-9-2-SUBACK可变头)
      - 3.9.2.1 [SUBACK属性集](#3-9-2-1-SUBACK属性集)
        - 3.9.2.1.1 [属性长度](#3-9-2-1-1-属性长度)
        - 3.9.2.1.2 [原因字符串](#3-9-2-1-2-原因字符串)
        - 3.9.2.1.3 [用户属性](#3-9-2-1-3-用户属性)
    - 3.9.3 [SUBACK载荷](#3-9-3-SUBACK载荷)
  - 3.10 [UNSUBSCRIBE - 取消订阅请求](#3-10-UNSUBSCRIBE-取消订阅请求)
    - 3.10.1 [UNSUBSCRIBE固定头](#3-10-1-UNSUBSCRIBE固定头)
    - 3.10.2 [UNSUBSCRIBE可变头](#3-10-2-UNSUBSCRIBE可变头)
      - 3.10.2.1 [UNSUBSCRIBE属性集](#3-10-2-1-UNSUBSCRIBE属性集)
        - 3.10.2.1.1 [属性长度](#3-10-2-1-1-属性长度)
        - 3.10.2.1.2 [用户属性](#3-10-2-1-2-用户属性)
    - 3.10.3 [UNSUBSCRIBE载荷](#3-10-3-UNSUBSCRIBE载荷)
    - 3.10.4 [UNSUBSCRIBE动作](#3-10-4-UNSUBSCRIBE动作)
  - 3.11 [UNSUBACK - 取消订阅确认](#3-11-UNSUBACK-取消订阅确认)
    - 3.11.1 [UNSUBACK固定头](#3-11-1-UNSUBACK固定头)
    - 3.11.2 [UNSUBACK可变头](#3-11-2-UNSUBACK可变头)
      - 3.11.2.1 [UNSUBACK属性集](#3-11-2-1-UNSUBACK属性集)
        - 3.11.2.1.1 [属性长度](#3-11-2-1-1-属性长度)
        - 3.11.2.1.2 [原因字符串](#3-11-2-1-2-原因字符串)
        - 3.11.2.1.3 [用户属性](#3-11-2-1-3-用户属性)
    - 3.11.3 [UNSUBACK载荷](#3-11-3-UNSUBACK载荷)
  - 3.12 [PINGREQ - PING请求](#3-12-PINGREQ-PING请求)
    - 3.12.1 [PINGREQ固定头](#3-12-1-PINGREQ固定头)
    - 3.12.2 [PINGREQ可变头](#3-12-2-PINGREQ可变头)
    - 3.12.3 [PINGREQ载荷](#3-12-3-PINGREQ载荷)
    - 3.12.4 [PINGREQ动作](#3-12-4-PINGREQ动作)
  - 3.13 [PINGRESP - PING响应](#3-13-PINGRESP-PING响应)
    - 3.13.1 [PINGRESP固定头](#3-13-1-PINGRESP固定头)
    - 3.13.2 [PINGRESP可变头](#3-13-2-PINGRESP可变头)
    - 3.13.3 [PINGRESP载荷](#3-13-3-PINGRESP载荷)
    - 3.13.4 [PINGRESP动作](#3-13-4-PINGRESP动作)
  - 3.14 [DISCONNECT - 断开通知](#3-14-DISCONNECT-断开通知)
    - 3.14.1 [DISCONNECT固定头](#3-14-1-DISCONNECT固定头)
    - 3.14.2 [DISCONNECT可变头](#3-14-2-DISCONNECT可变头)
      - 3.14.2.1 [断开原因码](#3-14-2-1-断开原因码)
      - 3.14.2.2 [DISCONNECT属性集](#3-14-2-2-DISCONNECT属性集)
        - 3.14.2.2.1 [属性长度](#3-14-2-2-1-属性长度)
        - 3.14.2.2.2 [会话过期间隔](#3-14-2-2-2-会话过期间隔)
        - 3.14.2.2.3 [原因字符串](#3-14-2-2-3-原因字符串)
        - 3.14.2.2.4 [用户属性](#3-14-2-2-4-用户属性)
        - 3.14.2.2.5 [服务引用](#3-14-2-2-5-服务引用)
    - 3.14.3 [DISCONNECT载荷](#3-14-3-DISCONNECT载荷)
    - 3.14.4 [DISCONNECT动作](#3-14-4-DISCONNECT动作)
  - 3.15 [AUTH - 认证交换](#3-15-AUTH-认证交换)
    - 3.15.1 [AUTH固定头](#3-15-1-AUTH固定头)
    - 3.15.2 [AUTH可变头](#3-15-2-AUTH可变头)
      - 3.15.2.1 [认证原因码](#3-15-2-1-认证原因码)
      - 3.15.2.2 [AUTH属性集](#3-15-2-2-AUTH属性集)
        - 3.15.2.2.1 [属性长度](#3-15-2-2-1-属性长度)
        - 3.15.2.2.2 [认证方式](#3-15-2-2-2-认证方式)
        - 3.15.2.2.3 [认证数据](#3-15-2-2-3-认证数据)
        - 3.15.2.2.4 [原因字符串](#3-15-2-2-4-原因字符串)
        - 3.15.2.2.5 [用户属性](#3-15-2-2-5-用户属性)
    - 3.15.3 [AUTH载荷](#3-15-3-AUTH载荷)
    - 3.15.4 [AUTH动作](#3-15-3-AUTH动作)
- 4 [操作行为](#4-操作行为)
  - 4.1 [会话状态](#4-1-会话状态)
    - 4.1.1 [存储会话状态](#4-1-1-存储会话状态)
    - 4.1.2 [会话状态非规范性示例](#4-1-2-会话状态非规范性示例)
  - 4.2 [网络连接](#4-2-网络连接)
  - 4.3 [QoS和协议流程](#4-3-QoS和协议流程)
    - 4.3.1 [QoS 0：至多一次](#4-3-1-QoS-0：至多一次)
    - 4.3.2 [Qos-1：至少一次](#4-3-2-Qos-1：至少一次)
    - 4.3.3 [QoS 2：确保一次](#4-3-3-Qos-2：确保一次)
  - 4.4 [消息传递重试](#4-4-消息传递重试)
  - 4.5 [消息接收](#4-5-消息接收)
  - 4.6 [消息顺序](#4-6-消息顺序)
  - 4.7 [主题名和主题过滤器](#4-7-主题名和主题过滤器)
    - 4.7.1 [主题通配符](#4-7-1-主题通配符)
      - 4.7.1.1 [主题级别分隔符](#4-7-1-1-主题级别分隔符)
      - 4.7.1.2 [多级通配符](#4-7-1-2-多级通配符)
      - 4.7.1.3 [单级通配符](#4-7-1-3-单级通配符)
    - 4.7.2 [$开头的主题](#4-7-2-开头的主题)
    - 4.7.3 [主题语义和使用](#4-7-3-主题语义和使用)
  - 4.8 [订阅](#4-8-订阅)
    - 4.8.1 [非共享订阅](#4-8-1-非共享订阅)
    - 4.8.2 [共享订阅](#4-8-2-共享订阅)
  - 4.9 [流量控制](#4-9-流量控制)
  - 4.10 [请求 / 响应](#4-10-请求-响应)
    - 4.10.1 [基础请求响应（非规范性）](#4-10-1-基础请求响应（非规范性）)
    - 4.10.2 [确定响应主题的值（非规范性）](#4-10-2-确定响应主题的值（非规范性）)
  - 4.11 [服务重定向](#4-11-服务重定向)
  - 4.12 [增强认证](#4-12-增强认证)
    - 4.12.1 [重新认证](#4-12-1-重新认证)
  - 4.13 [错误处理](#4-13-错误处理)
    - 4.13.1 [格式错误的包和协议错误](#4-13-1-格式错误的包和协议错误)
    - 4.13.2 [其他错误](#4-13-2-其他错误)
- 5 [安全性（非规范性）](#5-安全性（非规范性）)
  - 5.1 [介绍](#5-1-介绍)
  - 5.2 [MQTT解决方案：安全和认证](#5-2-MQTT解决方案：安全和认证)
  - 5.3 [轻量级密码学和受限设备](#5-3-轻量级密码学和受限设备)
  - 5.4 [实施说明](#5-4-实施说明)
    - 5.4.1 [服务器对客户端进行身份验证](#5-4-1-服务器对客户端进行身份验证)
    - 5.4.2 [服务器对客户端进行授权](#5-4-2-服务器对客户端进行授权)
    - 5.4.3 [客户端对服务器进行身份验证](#5-4-3-客户端对服务器进行身份验证)
    - 5.4.4 [应用消息和MQTT包的完整性](#5-4-4-应用消息和MQTT包的完整性)
    - 5.4.5 [应用消息和MQTT包的隐私](#5-4-5-应用消息和MQTT包的隐私)
    - 5.4.6 [消息传输的不可否认性](#5-4-6-消息传输的不可否认性)
    - 5.4.7 [检测客户端和服务器是否被入侵](#5-4-7-检测客户端和服务器是否被入侵)
    - 5.4.8 [检测异常行为](#5-4-8-检测异常行为)
    - 5.4.9 [处理禁止的Unicode码段](#5-4-9-处理禁止的Unicode码段)
      - 5.4.9.1 [关于使用禁止的Unicode码段的考虑](#5-4-9-1-关于使用禁止的Unicode码段的考虑)
      - 5.4.9.2 [发布者和订阅者之间的交互](#5-4-9-2-发布者和订阅者之间的交互)
      - 5.4.9.3 [补救措施](#5-4-9-3-补救措施)
    - 5.4.10 [其他安全注意事项](#5-4-10-其他安全注意事项)
    - 5.4.11 [使用SOCKS代理](#5-4-11-使用SOCKS代理)
    - 5.4.12 [安全配置](#5-4-12-安全配置)
      - 5.4.12.1 [透明通信配置](#5-4-12-1-透明通信配置)
      - 5.4.12.2 [安全网络通信配置](#5-4-12-2-安全网络通信配置)
      - 5.4.12.3 [安全传输配置](#5-4-12-3-安全传输配置)
      - 5.4.12.4 [行业特定的安全配置](#5-4-12-4-行业特定的安全配置)
- 6 [使用WebSocket作为传输层](#6-使用WebSocket作为传输层)
  - 6.1 [IANA注意事项](#6-1-IANA注意事项)
- 7 [一致性](#7-一致性)
  - 7.1 [一致性条款](#7-1-一致性条款)
    - 7.1.1 [MQTT服务器一致性条款](#7-1-1-MQTT服务器一致性条款)
    - 7.1.2 [MQTT客户端一致性条款](#7-1-2-MQTT客户端一致性条款)
- 附录 A. [致谢](#附录-A-致谢)
- 附录 B. [强制性规范性声明（非规范性）](#附录-B-强制性规范性声明（非规范性）)
- 附录 C. [MQTT v5.0 新特性汇总（非规范性）](#附录-C-MQTT-v5-0-新特性汇总（非规范性）)

# 1 介绍

## 1.0 知识产权政策

本规范是在 OASIS [知识产权政策](https://www.oasis-open.org/policies-guidelines/ipr)的 [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode)模式下提供的，该模式是技术委员会成立时选择的。关于是否有实施本规范依赖的已经披露的专利信息或是关于任何专利许可条款的信息，请参考技术委员会网站中的知识产权部分(https://www.oasis-open.org/committees/mqtt/ipr.php)。

## 1.1 MQTT规范结构

本规范分为七个章节：

- 第一章 - [介绍](#1-介绍)
- 第二章 - [MQTT包格式](#2-MQTT包结构)
- 第三章 - [MQTT包](#3-MQTT包)
- 第四章 - [操作行为](#4-操作行为)
- 第五章 - [安全性](#5-安全性（非规范性）)
- 第六章 - [使用Websocket作为传输层](#6-使用WebSocket作为传输层)
- 第七章 - [一致性目标](#7-一致性)

## 1.2 术语表

本文档中的关键字 **必须(MUST)**，**必须不(MUST NOT)**，**需要(REQUIRED)**，**应该(SHALL)**，**不应该(SHALL NOT)**，**理应(SHOULD)**，**理应不(SHOULD NOT)**，**推荐(RECOMMENDED)**，**可以(MAY)**，和**可选(OPTIONAL)**按照IETF [RFC 2119](#1.3-RFC2119)的定义阐释，除非在此类关键字出现的地方明确被标记为非规范性。

**网络连接:**

**由 MQTT 使用的传输协议提供的构造。**

- 他在客户端与服务器之间提供连接。
- 他提供了有序、无丢失、双向传输数据流的能力。

参考 [4.2 网络连接](#4-2-网络连接) 中提供的非规范性示例。

**应用消息**

提供应用程序使用的通过MQTT协议携带的消息。当应用消息通过MQTT传输时，他包含载荷，服务质量，属性集合和主题名称。

<span id="1.2-client">**客户端**</span>

一个使用了 MQTT 的程序或设备。一个客户端往往：

- 打开通往服务器的网络连接
- 发布其他客户端可能会感兴趣的应用消息
- 通过订阅来接收自己感兴趣的应用消息
- 通过取消订阅，不再接收应用消息
- 关闭通过服务器的网络连接

<span id="1.2-server">**服务器**</span>

一个在发布应用消息的客户端和订阅应用消息的客户端之间充当转发中介的程序或设备。一个服务器往往：

- 接收来自客户端的网络连接
- 接收客户端发布的应用消息
- 处理客户端的订阅和取消订阅请求
- 根据客户端的订阅情况匹配转发应用消息
- 关闭和客户端的网络连接

**会话**

服务器和客户端之间的有状态交互。有些会话仅和单次网络连接持续一样长的时间，有些会话则能够跨越多次连续的网络断开和连接持续保持。

**订阅**

订阅包括了主题过滤器和最大QoS。订阅只关联到一个会话。一个会话可以包括多个订阅。会话中的每个订阅都拥有一个不同的主题过滤器。

**共享订阅**

共享订阅包括了主题过滤器和最大QoS。共享订阅可以与多个会话关联，以便使用更加宽泛的信息交换模式。匹配到共享订阅的应用消息只会发送到被关联的会话其中之一对应的客户端。一个会话可以同时持有多个共享订阅，也可以同时持有共享订阅和普通订阅。

**通配订阅**

通配订阅指的是主题过滤器中包括了一个或多个通配符的订阅。通配订阅允许此订阅匹配多个主题名。参考 [4.7](#4-7-主题名和主题过滤器) 来了解通配符如何在主题过滤器中起作用。

**主题名**

附加到应用消息的文字标签，用于与服务器已知的订阅相匹配。

**主题过滤器**

订阅中包含的一种表达式，用于指示对一个或多个主题的兴趣。主题过滤器可以包含通配符。

**MQTT包**

通过网络连接发送的数据包。MQTT规范定义了十五中不同类型的MQTT包，例如 `发布` 包用来承载应用消息。

**格式错误的包**

一个不能通过本规范解析的数据包。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

**协议错误**

数据包被解析后发现的不符合协议规范的数据内容或客户端与服务器状态不一致的数据。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

**遗嘱**

当网络连接非正常关闭后，由服务器发布的应用消息。参考 [3.1.2.5](#3-1-2-5-遗嘱标识) 查看关于遗嘱的消息。

**禁止的 Unicode 码段**
 
在 UTF-8 字符串中不应出现的 Unicode 控制代码和 Unicode 非字符集。参考 [1.5.4](#1-5-4-UTF-8字符串) 查看更多关于禁止的 Unicode 码段的信息。

## 1.3 规范性引用

<span id="1.3-RFC2119" class="bold">[RFC2119]</span>

Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,

http://www.rfc-editor.org/info/rfc2119

<span id="1.3-RFC3629" class="bold">[RFC3629]</span>

Yergeau, F., "UTF-8, a transformation format of ISO 10646", STD 63, RFC 3629, DOI 10.17487/RFC3629, November 2003,

http://www.rfc-editor.org/info/rfc3629

<span id="1.3-RFC6455" class="bold">[RFC6455]</span>

Fette, I. and A. Melnikov, "The WebSocket Protocol", RFC 6455, DOI 10.17487/RFC6455, December 2011,

http://www.rfc-editor.org/info/rfc6455

<span id="1.3-Unicode" class="bold">[Unicode]</span>

The Unicode Consortium. The Unicode Standard,

http://www.unicode.org/versions/latest/

## 1.4 非规范性引用

<span id="1.4-RFC0793" class="bold">[RFC0793]</span>

Postel, J., "Transmission Control Protocol", STD 7, RFC 793, DOI 10.17487/RFC0793, September 1981, http://www.rfc-editor.org/info/rfc793

<span id="1.4-RFC5246" class="bold">[RFC5246]</span>

Dierks, T. and E. Rescorla, "The Transport Layer Security (TLS) Protocol Version 1.2", RFC 5246, DOI 10.17487/RFC5246, August 2008,

http://www.rfc-editor.org/info/rfc5246

<span id="1.4-AES" class="bold">[AES]</span>

Advanced Encryption Standard (AES) (FIPS PUB 197).

https://csrc.nist.gov/csrc/media/publications/fips/197/final/documents/fips-197.pdf

<span id="1.4-CHACHA20" class="bold">[CHACHA20]</span>

ChaCha20 and Poly1305 for IETF Protocols

https://tools.ietf.org/html/rfc7539

<span id="1.4-FIPS1402" class="bold">[FIPS1402]</span>

Security Requirements for Cryptographic Modules (FIPS PUB 140-2)

https://csrc.nist.gov/csrc/media/publications/fips/140/2/final/documents/fips1402.pdf

<span id="1.4-IEEE 802.1AR" class="bold">[IEEE 802.1AR]</span>

IEEE Standard for Local and metropolitan area networks - Secure Device Identity

http://standards.ieee.org/findstds/standard/802.1AR-2009.html

<span id="1.4-ISO29192" class="bold">[ISO29192]</span>

ISO/IEC 29192-1:2012 Information technology -- Security techniques -- Lightweight cryptography -- Part 1: General

https://www.iso.org/standard/56425.html

<span id="1.4-MQTT NIST" class="bold">[MQTT NIST]</span>

MQTT supplemental publication, MQTT and the NIST Framework for Improving Critical Infrastructure Cybersecurity

http://docs.oasis-open.org/mqtt/mqtt-nist-cybersecurity/v1.0/mqtt-nist-cybersecurity-v1.0.html

<span id="1.4-MQTTV311" class="bold">[MQTTV311]</span>

MQTT V3.1.1 Protocol Specification

http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html

<span id="1.4-ISO20922" class="bold">[ISO20922]</span>

MQTT V3.1.1 ISO Standard (ISO/IEC 20922:2016)

https://www.iso.org/standard/69466.html

<span id="1.4-NISTCSF" class="bold">[NISTCSF]</span>

Improving Critical Infrastructure Cybersecurity Executive Order 13636

https://www.nist.gov/sites/default/files/documents/itl/preliminary-cybersecurity-framework.pdf

<span id="1.4-NIST7628" class="bold">[NIST7628]</span>

NISTIR 7628 Guidelines for Smart Grid Cyber Security Catalogue

https://www.nist.gov/sites/default/files/documents/smartgrid/nistir-7628_total.pdf

<span id="1.4-NSAB" class="bold">[NSAB]</span>

NSA Suite B Cryptography

http://www.nsa.gov/ia/programs/suiteb_cryptography/

<span id="1.4-PCIDSS" class="bold">[PCIDSS]</span>

PCI-DSS Payment Card Industry Data Security Standard

https://www.pcisecuritystandards.org/pci_security/

<span id="1.4-RFC1928" class="bold">[RFC1928]</span>

Leech, M., Ganis, M., Lee, Y., Kuris, R., Koblas, D., and L. Jones, "SOCKS Protocol Version 5", RFC 1928, DOI 10.17487/RFC1928, March 1996,

http://www.rfc-editor.org/info/rfc1928

<span id="1.4-RFC4511" class="bold">[RFC4511]</span>

Sermersheim, J., Ed., "Lightweight Directory Access Protocol (LDAP): The Protocol", RFC 4511, DOI 10.17487/RFC4511, June 2006,

http://www.rfc-editor.org/info/rfc4511

<span id="1.4-RFC5280" class="bold">[RFC5280]</span>

Cooper, D., Santesson, S., Farrell, S., Boeyen, S., Housley, R., and W. Polk, "Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile", RFC 5280, DOI 10.17487/RFC5280, May 2008,

http://www.rfc-editor.org/info/rfc5280

<span id="1.4-RFC6066" class="bold">[RFC6066]</span>

Eastlake 3rd, D., "Transport Layer Security (TLS) Extensions: Extension Definitions", RFC 6066, DOI 10.17487/RFC6066, January 2011,

http://www.rfc-editor.org/info/rfc6066

<span id="1.4-RFC6749" class="bold">[RFC6749]</span>

Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012,

http://www.rfc-editor.org/info/rfc6749

<span id="1.4-RFC6960" class="bold">[RFC6960]</span>

Santesson, S., Myers, M., Ankney, R., Malpani, A., Galperin, S., and C. Adams, "X.509 Internet Public Key Infrastructure Online Certificate Status Protocol - OCSP", RFC 6960, DOI 10.17487/RFC6960, June 2013,

http://www.rfc-editor.org/info/rfc6960

<span id="1.4-SARBANES" class="bold">[SARBANES]</span>

Sarbanes-Oxley Act of 2002.

http://www.gpo.gov/fdsys/pkg/PLAW-107publ204/html/PLAW-107publ204.htm

<span id="1.4-USEUPRIVSH" class="bold">[USEUPRIVSH]</span>

U.S.-EU Privacy Shield Framework

https://www.privacyshield.gov

<span id="1.4-RFC3986" class="bold">[RFC3986]</span>

Berners-Lee, T., Fielding, R., and L. Masinter, "Uniform Resource Identifier (URI): Generic Syntax", STD 66, RFC 3986, DOI 10.17487/RFC3986, January 2005,

http://www.rfc-editor.org/info/rfc3986

<span id="1.4-RFC1035" class="bold">[RFC1035]</span>

Mockapetris, P., "Domain names - implementation and specification", STD 13, RFC 1035, DOI 10.17487/RFC1035, November 1987,

http://www.rfc-editor.org/info/rfc1035

<span id="1.4-RFC2782" class="bold">[RFC2782]</span>

Gulbrandsen, A., Vixie, P., and L. Esibov, "A DNS RR for specifying the location of services (DNS SRV)", RFC 2782, DOI 10.17487/RFC2782, February 2000,

http://www.rfc-editor.org/info/rfc2782

## 1.5 数据表示

### 1.5.1 比特位

字节中的比特位被标记为7-0，最高位为7，最低位为0。

### 1.5.2 2字节整数

2字节整数指16位的大端表示的无符号整数：高位字节在低位字节之前。这意味着在网络中传输的2字节整数先传输高有效字节(MSB)，后传输低有效字节(LSB)。

### 1.5.3 4字节整数

4字节整数指32位的大端表示的无符号整数：高位字节先于连续的低位字节。这意味着在网络中传输的4字节整数先传输最高有效字节(MSB)，再传输次高有效字节(MSB)，再传输次高有效字节(MSB)，最后传输低有效字节(LSB)。

### 1.5.4 UTF-8字符串

MQTT包中使用的文本类型字段均采用 UTF-8 编码。UTF-8 [RFC3629](#1.3-RFC3629) 是一种高效的 [Unicode](#1.3-Unicode) 编码，他优化了 ACSII 的编码以用来支持基于文本的通信。

每个 UTF-8 编码的字符串都使用开头的 `2字节整数` 表示字符串的长度，就像下方的 <span class="vcLinked">图1-1 UTF-8 字符串结构</span> 示意的那样。因此，UTF-8 字符串的最大长度为65535字节。

除非另有说明，否则所有 UTF-8 编码字符串可以具有 0 到 65,535 字节范围内的任意长度。

图1-1 UTF-8 字符串结构
<table>
  <thead>
    <tr>
      <th>Bit</th>
      <th>7</th>
      <th>6</th>
      <th>5</th>
      <th>4</th>
      <th>3</th>
      <th>2</th>
      <th>1</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>byte 1</td>
      <td colspan="8">字符串长度高字节(MSB)</td>
    </tr>
    <tr>
      <td>byte 2</td>
      <td colspan="8">字符串长度低字节(LSB)</td>
    </tr>
    <tr>
      <td>byte 3 ...</td>
      <td colspan="8">当长度 > 0 时, UTF-8 编码的字符数据</td>
    </tr>
  </tbody>
</table>

<span class="vcMarked">在 UTF-8 编码字符串中的字符**必须**为 <a href="#1.3-Unicode">[Unicode]</a> 和 <a href="#1.3-RFC3629">[RFC3629]</a> 中所定义的，格式正确的字符编码。**必须不**使用U+D800 至 U+DFFF之间的编码</span> <span class="vcReferred">[MQTT-1.5.4-1]</span>。如果客户端或服务器接收到的 MQTT 包中包括了非法 UTF-8 编码，将其视为一个格式错误的包。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

<span class="vcMarked">UTF-8 编码字符串**必须**不包含空字符 U+0000</span> <span class="vcReferred">[MQTT-1.5.4-2]</span>。如果一个接收者（服务器或客户端）接收的 MQTT 包其中有空字符 U+0000 ，将其视为一个格式错误的包。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

数据不应该包括下方列表中的 Unicode 码段，如果一个接收者（服务器或客户端）接受的 MQTT 包其中有此类字符，接收者可以将此包视为一个格式错误的包。这些是禁止使用的 Unicode 码段。参考 [5.4.9](#5-4-9-处理禁止的Unicode码段) 查看关于错误处理的信息。

- U+0001..U+001F 控制字符
- U+007F..U+009F 控制字符
- [Unicode](#1.3-Unicode) 规范中定义的非文本字符（例如 U+0FFFF）

<span class="vcMarked">无论 UTF-8 编码序列 0xEF 0xBB 0xBF 出现在字符串的何处，他永远被解释为 U+FEFF (0宽无换行空格) 而且**必须**不能被数据包的接收者跳过或剥离</span> <span class="vcReferred">[MQTT-1.5.4-3]</span>。

**非规范性示例**

例如，字符串 A𪛔 的第一个字符是拉丁文大写字母A，第二个字符是码点 U+2A6D4 （代表 CJK IDEOGRAPH EXTENSION B 字符），他是这样编码的：

图1‑2 UTF-8 编码字符串非规范性示例
<table>
  <thead>
    <tr>
      <th>Bit</th>
      <th>7</th>
      <th>6</th>
      <th>5</th>
      <th>4</th>
      <th>3</th>
      <th>2</th>
      <th>1</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>byte 1</td>
      <td colspan="8">字符串长度高字节(MSB)(0x00)</td>
    </tr>
    <tr>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>byte 2</td>
      <td colspan="8">字符串长度低字节(LSB)(0x05)</td>
    </tr>
    <tr>
      <td></td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>byte 3</td>
      <td colspan="8">‘A’ (0x41)</td>
    </tr>
    <tr>
      <td></td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>byte 4</td>
      <td colspan="8">(0xF0)</td>
    </tr>
    <tr>
      <td></td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>byte 5</td>
      <td colspan="8">(0xAA)</td>
    </tr>
    <tr>
      <td></td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>byte 6</td>
      <td colspan="8">(0x9B)</td>
    </tr>
    <tr>
      <td></td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>byte 7</td>
      <td colspan="8">(0x94)</td>
    </tr>
    <tr>
      <td></td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

### 1.5.5 变长整数

变长整数中将一个字节的最大值视为 127，更大的值采用如下方式处理。每个字节中较低的七位用来存储数字的值，最高位用来表示是否有后续的字节。因此，每个字节都编码了128个可能的值和一个 “后续位”。变长整数的最大字节数是4。<span class="vcMarked">变长整数编码时**必须**使用能够表示数字值的最小长度来进行编码</span> <span class="vcReferred">[MQTT-1.5.5-1]</span>。表1-1 中展示了变长整数可以表示的值。

表1-1 变长整数的值
| 位数 | 最小值 | 最大值 |
| --- | --- | --- |
| 1 | 0 (0x00) | 127 (0x7F) |
| 2 | 128 (0x80, 0x01) | 16,383 (0xFF, 0x7F) |
| 3 | 16,384 (0x80, 0x80, 0x01) | 2,097,151 (0xFF, 0xFF, 0x7F) |
| 4 | 2,097,152 (0x80, 0x80, 0x80, 0x01) | 268,435,455 (0xFF, 0xFF, 0xFF, 0x7F) |

**非规范性示例**

将非负整数 X 编码为变长整数的伪代码：

```text
do
   encodedByte = X MOD 128
   X = X DIV 128
   // if there are more data to encode, set the top bit of this byte
   if (X > 0)
      encodedByte = encodedByte OR 128
   endif
   'output' encodedByte
while (X > 0)
```

上例中的 MOD 表示取模（C语言中的 %），DIV表示整数除法（C语言中的 /），OR表示位运算中的或（C语言中的 |）。

**非规范性示例**

解码变长整数的伪代码：

```text
multiplier = 1
value = 0
do
   encodedByte = 'next byte from stream'
   value += (encodedByte AND 127) * multiplier
   if (multiplier > 128*128*128)
      throw Error(Malformed Variable Byte Integer)
   multiplier *= 128
while ((encodedByte AND 128) != 0)
```

上例中的 AND 表示位运算中的且（C语言中的 &）。

当该算法完成时，value的值即是变长整数表示的值。

### 1.5.6 二进制数据

二进制数据由 `2字节整数` 表示的字节流长度加上实际的字节流内容组成。因此，二进制数据的长度范围是 0-65535 字节。

### 1.5.7 UTF-8字符串对

UT-8 字符串对包括两个 `UTF-8字符串`。这种数据类型用来存储 键-值 对。第一个字符串表示键，第二个字符串表示值。

<span class="vcMarked">UTF-8字符串对中的两个字符串都**必须**遵守 `UTF-8字符串` 的需求</span> <span class="vcReferred">[MQTT-1.5.7-1]</span>。如果一个接收者（客户端或服务器）接收到的键值对没有遵守这些需求，则被视为一个格式错误的数据包。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

## 1.6 安全性

MQTT 的客户端和服务器实现应该提供认证、授权和加密传输选项，这一部分在第五章讨论。强烈建议与关键基础设施、个人身份信息或其他个人或敏感信息相关的应用程序使用这些安全功能。

## 1.7 编辑约定

本规范中以<span class="vcMarked">黄色</span>突出显示的文本标识了一致性声明。每个一致性声明都被分配了一个格式为 <span class="vcReferred">[MQTT-x.x.x-y]</span> 的引用，其中 <span class="vcReferred">x.x.x</span> 是章节序号，<span class="vcReferred">y</span> 是章节内的序号。

## 1.8 变更历史

### 1.8.1 MQTT v3.1.1

MQTT v3.1.1 是 OASIS 提出的第一个 MQTT 标准 **\[MQTTV311]** 。

MQTT v3.1.1 同时也是 ISO/IEC 20922:2016 标准 [ISO20922](#1.4-ISO20922)。

### 1.8.2 MQTT v5.0

MQTT v5.0 为 MQTT 添加了大量新功能，同时保留了大部分核心功能。主要功能目标是：

- 可扩展性和大型系统的增强
- 改进错误报告能力
- 将常见用法规范化，包括功能发现和请求响应
- 包括用户属性在内的拓展机制
- 性能改进，增强对小型客户端的支持

参考 [附录 C](#附录-C-MQTT-v5-0-新特性汇总（非规范性）) 查阅 MQTT v5.0 的变更汇总。

# 2 MQTT包格式

## 2.1 MQTT包结构

MQTT 协议操作通过一系列的 MQTT 包交互来实现。本章用来描述这些 MQTT 包的结构。

一个 MQTT 包由三部分构成，顺序固定，参考下图：

<table>
  <tbody>
    <tr><td>固定头，所有的 MQTT 包都必须持有</td><tr>
    <tr><td>可变头，部分 MQTT 包持有</td></tr>
    <tr><td>载荷，部分 MQTT 包持有</td></tr>
  </tbody>
</table>

### 2.1.1 固定头

每个 MQTT 包都包含着一个下图所示的固定头：

图2-2 固定头格式

<table>
  <thead>
    <tr>
      <th>Bit</th>
      <th>7</th>
      <th>6</th>
      <th>5</th>
      <th>4</th>
      <th>3</th>
      <th>2</th>
      <th>1</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>byte 1</td>
      <td colspan="4">MQTT包类型</td>
      <td colspan="4">针对不同包类型的控制标识</td>
    </tr>
    <tr>
      <td>byte 2...</td>
      <td colspan="8">剩余长度</td>
    </tr>
  </tbody>
</table>

### 2.1.2 MQTT包类型

**位置：**第一个Byte，比特位7-4。

表示为 4bit 的无符号整数，数值的含义如下表所示：

表2-1 MQTT包类型

| Name | Value | Direction of flow | Description |
| --- | --- | --- | --- |
| 保留 | 0 | 禁止 | 保留 |
| CONNECT | 1 | 客户端到服务器 | 连接请求 |
| CONNACK | 2 | 服务器到客户端 | 连接回复 |
| PUBLISH | 3 | 双向 | 消息发布 |
| PUBACK | 4 | 双向 | 消息回复（QoS1） |
| PUBREC | 5 | 双向 | 消息已接收（QoS2交付第 1 部分） |
| PUBREL | 6 | 双向 | 消息释放（QoS2交付第 2 部分） |
| PUBCOMP | 7 | 双向 | 消息完成（QoS2交付第 3 部分） |
| SUBSCRIBE | 8 | 客户端到服务器 | 订阅请求 |
| SUBACK | 9 | 服务器到客户端 | 订阅回复 |
| UNSUBSCRIBE | 10 | 客户端到服务器 | 取消订阅请求 |
| UNSUBACK | 11 | 服务器到客户端 | 取消订阅回复 |
| PINGREQ | 12 | 客户端到服务器 | PING 请求 |
| PINGRESP | 13 | 服务器到客户端 | PING 响应 |
| DISCONNECT | 14 | 双向 | 断开连接通知 |
| AUTH | 15 | 双向 | 认证交换 |

### 2.1.3 控制标识

固定头第一个 byte 中剩下的四个bit \[3-0]包括了基于不同 MQTT 包类型的控制标识。<span class="vcMarked">当一个比特位被标记为 “保留” 时，他的意义被保留到未来使用而他的值**必须**按照下表设置</span> <span class="vcReferred">[MQTT-2.1.3-1]</span>。如果接收到的控制标志不符合规范，则被认为是一个格式错误的数据包。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

表2‑2 控制标志

<table>
  <thead>
    <tr>
      <td>MQTT包</td>
      <td>控制标志</td>
      <td>Bit 3</td>
      <td>Bit 2</td>
      <td>Bit 1</td>
      <td>Bit 0</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CONNECT</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>CONNACK</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PUBLISH</td>
      <td>MQTT 5.0版本使用</td>
      <td>DUP</td>
      <td colspan="2">QoS</td>
      <td>RETAIN</td>
    </tr>
    <tr>
      <td>PUBACK</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PUBREC</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PUBREL</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PUBCOMP</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>SUBSCRIBE</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>SUBACK</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>UNSUBSCRIBE</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>UNSUBACK</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PINGREQ</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>PINGRESP</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>DISCONNECT</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>AUTH</td>
      <td>Reserved</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

DUP = 重复发送的 PUBLISH 包
QoS = PUBLISH 包的服务质量标识
RETAIN = PUBLISH 保留消息标识

参考 [3.3.1](#3-3-1-PUBLISH-固定头) 了解更多关于 DUP，QoS 和 RETAIN 标识在 PUBLISH 中的使用方式。

### 2.1.4 剩余长度

**位置：**从第二个Byte开始。

剩余长度是一个变长整数，用来表示当前包剩余的字节数，包括可变头和载荷。剩余长度的值不包括剩余长度自己本身占用的字节数。一个 MQTT 包完整的字节数等于固定头的长度加上剩余长度的值。

## 2.2 可变头

某些类型的 MQTT 包包含可变头。他位于固定头和载荷之间。可变头的内容根据数据包的类型变化。可变头中的包ID字段多种类型的数据包中都存在。

### 2.2.1 包ID

很多类型的 MQTT 包都在其可变头中包含了 2byte 的包ID字段。这些 MQTT 包是 PUBLISH （当 QoS > 0时），PUBACK，PUBREC，PUBREL，PUBCOMP，SUBSCRIBE，SUBACK，UNSUBSCRIBE，UNSUBACK。

需要包ID的 MQTT 包类型如下表所示：

表2-3 包含包ID的 MQTT 包类型

| MQTT 包 | 包ID字段 |
| --- | --- |
| CONNECT | 否 |
| CONNACK | 否 |
| PUBLISH | 是（仅当 QoS > 0 时） |
| PUBACK | 是 |
| PUBREC | 是 |
| PUBREL | 是 |
| PUBCOMP | 是 |
| SUBSCRIBE | 是 |
| SUBACK | 是 |
| UNSUBSCRIBE | 是 |
| UNSUBACK | 是 |
| PINGREQ | 否 |
| PINGRESP | 否 |
| DISCONNECT | 否 |
| AUTH | 否 |

<span class="vcMarked">当 PUBLISH 包的 QoS 值为 0 时，**必须不**包含 包ID 字段</span> <span class="vcReferred">[MQTT-2.2.1-2]</span>。

<span class="vcMarked">每当客户端发送新的 SUBSCRIBE 包，UNSUBSCRIBE 包 或 QoS > 0 的 PUBLISH 包，**必须**携带一个非零且当前未被使用的包ID</span> <span class="vcReferred">[MQTT-2.2.1-3]</span>。

<span class="vcMarked">每当服务器发送新的 QoS > 0 的 PUBLISH 包，**必须**携带一个非零且当前未被使用的包ID</span> <span class="vcReferred">[MQTT-2.2.1-4]</span>。

包ID仅在发送者处理了对应的回复后可重新使用，定义如下。对于 QoS = 1 的 PUBLISH，对应的回复是 PUBACK；对于 QoS = 2 的PUBLISH，对应的回复是 PUBCOMP 或当原因码为 128 或更大时为 PUBREC。对于 SUBSCRIBE 或 UNSUBSCRIBE，对应的回复是 SUBACK 或 UNSUBACK。

在一个会话中，客户端与服务器分别使用一个单独、统一的集合用作提供 PUBLISH、SUBSCRIBE 和 UNSUBSCRIBE 的包ID。包ID在任何时候都不能被多个命令使用。

<span class="vcMarked">PUBACK，PUBREC，PUBREL 或 PUBCOMP 包**必须**携带和 PUBLISH 相同的包ID</span> <span class="vcReferred">[MQTT-2.2.1-5]</span>。<span class="vcMarked">SUBACK 和 UNSUBACK **必须**携带和其对应的 SUBSCRIBE 和 UNSUBSCRIBE 包相同的包ID</span> <span class="vcReferred">[MQTT-2.2.1-6]</span>。

客户端与服务器各自独立的维护包ID分配。因此，客户端与服务器可以同时使用同样的包ID发送信息。

**非规范性示例**

客户端发送一个包ID为 0x1234 的 PUBLISH 包，之后在其接收到对应的 PUBACK 之前，从服务器接收到一个 包ID 为 0x1234 的 PUBLISH 包。这样的情况是合理而且完全有可能的。

```text
Client                                                   Server
PUBLISH 包ID=0x1234 ‒→
                                                    ←‒ PUBLISH 包ID=0x1234
PUBACK 包ID=0x1234 ‒→
                                                    ←‒ PUBACK 包ID=0x1234
```

### 2.2.2 属性集

在 CONNECT，CONNACK，PUBLISH，PUBACK，PUBREC，PUBREL，PUBCOMP，SUBSCRIBE，SUBACK，UNSUBSCRIBE，UNSUBACK，DISCONNECT 和 AUTH 包的可变头中的最后一个字段是属性集。在 CONNECT 的载荷中也存在着一组可选的遗嘱属性集。

属性集由属性长度和属性组成。

#### 2.2.2.1 属性长度

属性长度是一个变长整数。属性长度的值不包括自己所占用的字节数，但包括了后续所有属性占用的字节数。<span class="vcMarked">如果没有属性，**必须**通过一个 0 值的属性长度来明确表示</span> <span class="vcReferred">[MQTT-2.2.2-1]</span>。

#### 2.2.2.2 属性

属性由一个标识了其用途和数据类型的ID和一个后续的值组成。属性ID是一个变长整数。当一个数据包使用的属性ID和其包类型不一致，或属性的值和ID指明的类型不一致时，视为一个格式错误的包。如果收到，需使用带有原因码为 0x81 的 CONNACK 或 DISCONNECT 数据包，采用 [4.13](#4-13-错误处理) 描述的方法处理此错误。不同ID的属性没有顺序要求。

表2-4 属性
<table>
  <thead>
    <tr>
      <th colspan="2">ID</th>
      <th rowspan="2">名称（用途）</th>
      <th rowspan="2">数据类型</th>
      <th rowspan="2">包类型 / 遗嘱属性</th>
    </tr>
    <tr>
      <th>十进制</th><th>十六进制</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>1</td><td>0x01</td><td>载荷格式标识</td><td>单字节</td><td>PUBLISH，Will Properties</td></tr>
    <tr><td>2</td><td>0x02</td><td>消息过期间隔</td><td>4字节整数</td><td>PUBLISH，Will Properties</td></tr>
    <tr><td>3</td><td>0x03</td><td>内容类型</td><td>UTF-8字符串</td><td>PUBLISH，Will Properties</td></tr>
    <tr><td>8</td><td>0x08</td><td>响应主题</td><td>UTF-8字符串</td><td>PUBLISH，Will Properties</td></tr>
    <tr><td>9</td><td>0x09</td><td>关联数据</td><td>二进制数据</td><td>PUBLISH，Will Properties</td></tr>
    <tr><td>11</td><td>0x0B</td><td>订阅ID</td><td>变长整数</td><td>PUBLISH，SUBSCRIBE</td></tr>
    <tr><td>17</td><td>0x11</td><td>会话过期间隔</td><td>4字节整数</td><td>CONNECT，CONNACK，DISCONNECT</td></tr>
    <tr><td>18</td><td>0x12</td><td>分配的客户端ID</td><td>UTF-8字符串</td><td>CONNACK</td></tr>
    <tr><td>19</td><td>0x13</td><td>服务器保活时间</td><td>2字节整数</td><td>CONNACK</td></tr>
    <tr><td>21</td><td>0x15</td><td>认证方式</td><td>UTF-8字符串</td><td>CONNECT，CONNACK，AUTH</td></tr>
    <tr><td>22</td><td>0x16</td><td>认证数据</td><td>二进制数据</td><td>CONNECT，CONNACK，AUTH</td></tr>
    <tr><td>23</td><td>0x17</td><td>请求问题信息</td><td>单字节</td><td>CONNECT</td></tr>
    <tr><td>24</td><td>0x18</td><td>遗嘱延迟间隔</td><td>4字节整数</td><td>Will Properties</td></tr>
    <tr><td>25</td><td>0x19</td><td>请求响应信息</td><td>单字节</td><td>CONNECT</td></tr>
    <tr><td>26</td><td>0x1A</td><td>响应信息</td><td>UTF-8字符串</td><td>CONNACK</td></tr>
    <tr><td>28</td><td>0x1C</td><td>服务引用</td><td>UTF-8字符串</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>31</td><td>0x1F</td><td>原因字符串</td><td>UTF-8字符串</td><td>CONNACK，PUBACK，PUBREC，PUBREL，PUBCOMP，SUBACK，UNSUBACK，DISCONNECT，AUTH</td></tr>
    <tr><td>33</td><td>0x21</td><td>接收最大值</td><td>2字节整数</td><td>CONNECT，CONNACK</td></tr>
    <tr><td>34</td><td>0x22</td><td>主题别名最大值</td><td>2字节整数</td><td>CONNECT，CONNACK</td></tr>
    <tr><td>35</td><td>0x23</td><td>主题别名</td><td>2字节整数</td><td>PUBLISH</td></tr>
    <tr><td>36</td><td>0x24</td><td>QoS最大值</td><td>单字节</td><td>CONNACK</td></tr>
    <tr><td>37</td><td>0x25</td><td>保留消息可用</td><td>单字节</td><td>CONNACK</td></tr>
    <tr><td>38</td><td>0x26</td><td>用户属性</td><td>UTF-8字符串对</td><td>CONNECT，CONNACK，PUBLISH，Will Properties，PUBACK，PUBREC，PUBREL，PUBCOMP，SUBSCRIBE，SUBACK，UNSUBSCRIBE，UNSUBACK，DISCONNECT，AUTH</td></tr>
    <tr><td>39</td><td>0x27</td><td>最大包尺寸</td><td>4字节整数</td><td>CONNECT，CONNACK</td></tr>
    <tr><td>40</td><td>0x28</td><td>通配符订阅可用</td><td>单字节</td><td>CONNACK</td></tr>
    <tr><td>41</td><td>0x29</td><td>订阅ID可用</td><td>单字节</td><td>CONNACK</td></tr>
    <tr><td>42</td><td>0x2A</td><td>共享订阅可用</td><td>单字节</td><td>CONNACK</td></tr>
  </tbody>
</table>

*非规范性评论*

*虽然属性ID被定义为一个变长整数，但在规范的此版本中所有的属性ID都只有一个字节的长度。*

## 2.3 载荷

有些 MQTT 包的尾部是载荷。在 PUBLISH 包中的载荷就是应用消息。

表2-5 包含载荷的 MQTT 包

| MQTT 包 | 载荷 |
| --- | --- |
| CONNECT | 有 |
| CONNACK | 无 |
| PUBLISH | 可选 |
| PUBACK | 无 |
| PUBREC | 无 |
| PUBREL | 无 |
| PUBCOMP | 无 |
| SUBSCRIBE | 有 |
| SUBACK | 有 |
| UNSUBSCRIBE | 有 |
| UNSUBACK | 有 |
| PINGREQ | 无 |
| PINGRESP | 无 |
| DISCONNECT | 无 |
| AUTH | 无 |

## 2.4 原因码

原因码是一个单字节的无符号整数值，用来表示一个操作的结果。小于 0x80 的原因码用来表示操作成功，最常见的表示成功的原因码是 0x00。0x80或更大的原因码表示失败。

在 CONNACK，PUBACK，PUBREC，PUBREL，PUBCOMP，DISCONNECT 和 AUTH 包的可变头中有一个原因码字段。在 SUBACK 和 UNSUBACK 的载荷中包一个列表，其中有一个或多个原因码字段。

原因码字段值的通用定义如下：

表2-6 原因码

<table>
  <thead>
    <tr>
      <th colspan="2">原因码</th>
      <th rowspan="2">名称</th>
      <th rowspan="2">包类型</th>
    </tr>
    <tr>
      <th>十进制</th><th>十六进制</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>0</td><td>0x00</td><td>成功</td><td>CONNACK，PUBACK，PUBREC，PUBREL，PUBCOMP，UNSUBACK，AUTH</td></tr>
    <tr><td>0</td><td>0x00</td><td>普通断开</td><td>DISCONNECT</td></tr>
    <tr><td>0</td><td>0x00</td><td>授予 QoS 0</td><td>SUBACK</td></tr>
    <tr><td>1</td><td>0x01</td><td>授予 QoS 1</td><td>SUBACK</td></tr>
    <tr><td>2</td><td>0x02</td><td>授予 QoS 2</td><td>SUBACK</td></tr>
    <tr><td>4</td><td>0x04</td><td>携带遗嘱的断开链接</td><td>DISCONNECT</td></tr>
    <tr><td>16</td><td>0x16</td><td>没有匹配的订阅者</td><td>PUBACK，PUBREC</td></tr>
    <tr><td>17</td><td>0x11</td><td>没有存在的订阅</td><td>UNSUBACK</td></tr>
    <tr><td>24</td><td>0x18</td><td>继续认证</td><td>AUTH</td></tr>
    <tr><td>25</td><td>0x19</td><td>重新认证</td><td>AUTH</td></tr>
    <tr><td>128</td><td>0x80</td><td>未指定错误</td><td>CONNACK，PUBACK，PUBREC，SUBACK，UNSUBACK，DISCONNECT</td></tr>
    <tr><td>129</td><td>0x81</td><td>格式错误的包</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>130</td><td>0x82</td><td>协议错误</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>131</td><td>0x83</td><td>特定实现错误</td><td>CONNACK，PUBACK，PUBREC，SUBACK，UNSUBACK，DISCONNECT</td></tr>
    <tr><td>132</td><td>0x84</td><td>协议版本不支持</td><td>CONNACK</td></tr>
    <tr><td>133</td><td>0x85</td><td>客户端ID不可用</td><td>CONNACK</td></tr>
    <tr><td>134</td><td>0x86</td><td>用户名或密码错误</td><td>CONNACK</td></tr>
    <tr><td>135</td><td>0x87</td><td>未经授权</td><td>CONNACK，PUBACK，PUBREC，SUBACK，UNSUBACK，DISCONNECT</td></tr>
    <tr><td>136</td><td>0x88</td><td>服务器不可用</td><td>CONNACK</td></tr>
    <tr><td>137</td><td>0x89</td><td>服务器忙</td><td>CONNACK</td></tr>
    <tr><td>138</td><td>0x8A</td><td>被禁止</td><td>CONNACK</td></tr>
    <tr><td>139</td><td>0x8B</td><td>服务器关闭</td><td>DISCONNECT</td></tr>
    <tr><td>140</td><td>0x8C</td><td>认证方式错误</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>141</td><td>0x8D</td><td>保活超时</td><td>DISCONNECT</td></tr>
    <tr><td>142</td><td>0x8E</td><td>会话被接管</td><td>DISCONNECT</td></tr>
    <tr><td>143</td><td>0x8F</td><td>主题过滤器不可用</td><td>SUBACK，UNSUBACK，DISCONNECT</td></tr>
    <tr><td>144</td><td>0x90</td><td>主题名不可用</td><td>CONNACK，PUBACK，PUBREC，DISCONNECT</td></tr>
    <tr><td>145</td><td>0x91</td><td>包ID已被使用</td><td>PUBACK，PUBREC，SUBACK，UNSUBACK</td></tr>
    <tr><td>146</td><td>0x92</td><td>包ID未找到</td><td>PUBREL，PUBCOMP</td></tr>
    <tr><td>147</td><td>0x93</td><td>超出接收最大值</td><td>DISCONNECT</td></tr>
    <tr><td>148</td><td>0x94</td><td>主题别名不可用</td><td>DISCONNECT</td></tr>
    <tr><td>149</td><td>0x95</td><td>包过大</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>150</td><td>0x96</td><td>消息频率过高</td><td>DISCONNECT</td></tr>
    <tr><td>151</td><td>0x97</td><td>超限</td><td>CONNACK，PUBACK，PUBREC，SUBACK，DISCONNECT</td></tr>
    <tr><td>152</td><td>0x98</td><td>管理员行为</td><td>DISCONNECT</td></tr>
    <tr><td>153</td><td>0x99</td><td>载荷格式错误</td><td>CONNACK，PUBACK，PUBREC，DISCONNECT</td></tr>
    <tr><td>154</td><td>0x9A</td><td>不支持保留消息</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>155</td><td>0x9B</td><td>不支持的 QoS</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>156</td><td>0x9C</td><td>使用另一台服务器</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>157</td><td>0x9D</td><td>服务器迁移</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>158</td><td>0x9E</td><td>不支持共享订阅</td><td>SUBACK，DISCONNECT</td></tr>
    <tr><td>159</td><td>0x9F</td><td>连接频率超限</td><td>CONNACK，DISCONNECT</td></tr>
    <tr><td>160</td><td>0xA0</td><td>最大连接时间</td><td>DISCONNECT</td></tr>
    <tr><td>161</td><td>0xA1</td><td>不支持订阅ID</td><td>SUBACK，DISCONNECT</td></tr>
    <tr><td>162</td><td>0xA2</td><td>不支持通配符订阅</td><td>SUBACK，DISCONNECT</td></tr>
  </tbody>
</table>

*非规范性评论*

*对于 0x91（包ID已被使用）的原因码，对此的处理应是处理重复状态，或是使用 Clean Start 为 1 的标识重新创建连接来重置会话，或是检查客户端或服务器的实现是否有缺陷。*

# 3 MQTT包

## 3.1 CONNECT - 连接请求

<span class="vcMarked">当客户端和服务器的网络连接建立后，客户端向服务器发送的第一个数据包**必须**是 CONNECT 包</span> <span class="vcReferred">[MQTT-3.1.0-1]</span>。

一个客户端在一次网络连接中只能发送一个 CONNECT 包。<span class="vcMarked">服务器**必须**将客户端发送的第二个 CONNECT 包视为协议错误并关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.0-2]</span>。参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

CONNECT 的载荷包含一个或更多的字段，包括唯一的客户端ID，遗嘱主题，遗嘱载荷，用户名和密码。除了客户端ID以外的字段都可以省略，他们的存在与否根据可变头中的标识确定。

### 3.1.1 CONNECT固定头

图3‑1 CONNECT 包固定头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（1）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2...</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度**

表示可变头长度和载荷长度的总和，使用变长整数表示。

### 3.1.2 CONNECT可变头

CONNECT 包中的可变头按固定顺序提供下列字段：协议名、协议版本、连接标识、保活时间和属性集。属性集的编码方式请参考 [2.2.2](#2-2-2-属性集)。

#### 3.1.2.1 协议名

图3-2 协议名字节

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">协议名</td></tr>
    <tr><td>byte 1</td><td>长度高位（MSB）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td>长度低位（LSB）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
    <tr><td>byte 3</td><td>'M'</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td></tr>
    <tr><td>byte 4</td><td>'Q'</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
    <tr><td>byte 5</td><td>'T'</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
    <tr><td>byte 6</td><td>'T'</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
  </tbody>
</table>

协议名是 UTF-8字符串表示的大写 “MQTT”，就像上图所示。这个字符串、他的位置和他的长度在未来的 MQTT 规范版本中永远不会改变。

支持多种协议的服务器可以通过协议名称来判断收到的数据是否是 MQTT 数据。<span class="vcMarked">协议名称**必须**是 `UTF-8字符串`表示的 “MQTT”。如果服务器不想接收此连接，同时又想告知客户端服务器是一个 MQTT 服务器，**可以**发送一个带有 0x84（协议版本不支持）原因码的 CONNACK，随后服务器**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.2-1]</span>。
 
*非规范性评论*

*数据包检查器（例如防火墙）可以使用协议名称来识别 MQTT 流量。*

#### 3.1.2.2 协议版本

图3‑3 协议版本字节

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">协议版本</td></tr>
    <tr><td>byte 7</td><td>版本（5）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  </tbody>
</table>

此处的单字节无符号值表示了客户端使用的协议的版本。MQTT 5.0 版本的协议版本的值应为 5（0x05）。

支持多个协议版本的服务器可以通过协议版本字段来判断客户端使用何种版本的 MQTT 协议。<span class="vcMarked">如果客户端使用的协议版本不为 5 而且服务器不想接受此 CONNECT 包，服务器**可以**发送一个带有 0x84（协议版本不支持）原因码的 CONNACK，随后服务器**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.2-2]</span>。

#### 3.1.2.3 连接标识

连接标志字节包含了几个指定 MQTT 连接行为的参数。他还用来指示载荷中的某些字段是否存在。

图3‑4 连接标识位

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td></td><td>用户名标识</td><td>密码标识</td><td>遗嘱保留消息</td><td colspan="2">遗嘱QoS</td><td>遗嘱标识</td><td>全新开始</td><td>保留</td></tr>
    <tr><td>byte 8</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>0</td></tr>
  </tbody>
</table>

<span class="vcMarked">服务器**必须**验证 CONNECT 包中的保留位的值是 0</span> <span class="vcReferred">[MQTT-3.1.2-3]</span>。如果保留位的值非 0，则视为一个格式错误的包，参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

#### 3.1.2.4 全新开始

**位置：**连接标识字节中的比特位 1。

这个比特位指定了此连接是一个全新的会话还是一个已经存在会话的延续。参考 [4.1](#4-1-会话状态) 了解关于会话状态的定义。

<span class="vcMarked">如果接收到全新开始值置为 1 的 CONNECT 包，客户端和服务器**必须**丢弃任何已经存在的会话并开始一个新的会话</span> <span class="vcReferred">[MQTT-3.1.2-4]</span>。因此，当 CONNECT 包中的全新开始值置为 1 时，对应的 CONNACK 包中的会话存在总是会被至为0。

<span class="vcMarked">如果服务器接收到的 CONNECT 包中的全新开始被置为 0 并且服务器中已经存在和客户端ID关联的会话，服务器**必须**基于已经存在的会话状态恢复客户端的连接</span> <span class="vcReferred">[MQTT-3.1.2-5]</span>。<span class="vcMarked">如果服务器接收到的 CONNECT 包中的全新开始被置为 0 并且服务器中没有和客户端ID关联的会话，服务器**必须**创建一个新的会话</span> <span class="vcReferred">[MQTT-3.1.2-6]</span>。

#### 3.1.2.5 遗嘱标识

**位置：**连接标识字节中的比特位 2。

<span class="vcMarked">如果遗嘱标识被置为 1，则表示遗嘱消息**必须**被存储在服务器中，并且关联到此会话</span> <span class="vcReferred">[MQTT-3.1.2-7]</span>。遗嘱消息由 CONNECT 载荷中的遗嘱属性集、遗嘱主题和遗嘱载荷组成。<span class="vcMarked">遗嘱消息**必须**在网络连接断开后的遗嘱延迟间隔时间过期后或会话结束时发布，除非由于服务器接收到一个带有 0x00（普通断开）原因码的 DISCONNECT 包从而删除了遗嘱消息，或是在遗嘱延迟间隔时间过期前接收了一个带有相同客户端ID的连接</span> <span class="vcReferred">[MQTT-3.1.2-8]</span>。

遗嘱消息被发布的场景包括不限于：

- 服务器检测到了 I/O 错误或网络故障
- 客户端没有成功在保活时间内通信
- 客户端在没有发送原因码为 0x00（普通断开）的 DISCONNECT 包的前提下断开网络连接
- 服务器在没有收到原因码为 0x00（普通断开）的 DISCONNECT 包的前提下断开网络连接

<span class="vcMarked">当遗嘱标识被置为 1 时，载荷中**必须**包括遗嘱属性集、遗嘱主题和遗嘱载荷字段</span> <span class="vcReferred">[MQTT-3.1.2-9]</span>。<span class="vcMarked">当服务器发布遗嘱后或服务器从客户端收到了原因码为 0x00（普通断开）的 DISCONNECT 包后，服务器**必须**从会话状态中删除遗嘱消息</span> <span class="vcReferred">[MQTT-3.1.2-10]</span>。

服务器应该在下列两种情况中的某一种先发生时发布遗嘱消息：网络连接断开后经过了遗嘱延迟间隔时间、会话结束。如果发生了服务器关闭或故障，服务器也许可以在随后的重启之后发布遗嘱消息。当此种情况发生时，服务器故障发生的时间和遗嘱消息发布的时间之间可能会有延迟。

参考 [3.1.3.2](#3-1-3-2-遗嘱属性集) 了解关于遗嘱延迟间隔的消息。

*非规范性评论*

*客户端可以设置遗嘱延迟间隔大于会话过期间隔，再发送带有原因码 0x04（携带遗嘱的断开链接）的 DISCONNECT 断开连接。这样可以使用遗嘱消息来通知会话已过期。*

#### 3.1.2.6 遗嘱QoS

**位置：**连接标识字节中的比特位 4 和 3。

这两个比特位指定了发布遗嘱消息时使用的 QoS 等级。

<span class="vcMarked">当遗嘱标识被置为 0 时，遗嘱 QoS **必须**被置为 0（0x00）</span> <span class="vcReferred">[MQTT-3.1.2-11]</span>。

<span class="vcMarked">当遗嘱标识被置为 1 时，遗嘱QoS的值可以是 0（0x00），1（0x01）或 2（0x02）</span> <span class="vcReferred">[MQTT-3.1.2-12]</span>。当值为 3（0x03）时视为格式错误的包，参考 [4.13](#4-13-错误处理) 查看关于错误处理的信息。

#### 3.1.2.7 遗嘱保留消息

**位置：**连接标识字节中的比特位 5。

这个比特位指定了当遗嘱消息发布时是否会被保留。

<span class="vcMarked">当遗嘱标识被置为 0 时，遗嘱保留消息的值**必须**被置为 0</span> <span class="vcReferred">[MQTT-3.1.2-13]</span>。<span class="vcMarked">当遗嘱标识被置为 1 且遗嘱保留消息被置为 0 时，服务器**必须**将遗嘱消息作为一个非保留消息发布</span> <span class="vcReferred">[MQTT-3.1.2-14]</span>。<span class="vcMarked">当遗嘱标识被置为 1 且遗嘱保留消息被置为 1 时，服务器**必须**将遗嘱消息作为一个保留消息发布</span> <span class="vcReferred">[MQTT-3.1.2-15]</span>。

#### 3.1.2.8 用户名标识

**位置：**连接标识字节中的比特位 7。

<span class="vcMarked">当用户名标识被置为 0 时，载荷中**必须不**存在用户名</span> <span class="vcReferred">[MQTT-3.1.2-16]</span>。<span class="vcMarked">当用户名标识被置为 1 时，载荷中**必须**存在用户名</span> <span class="vcReferred">[MQTT-3.1.2-17]</span>。

#### 3.1.2.9 密码标识

**位置：**连接标识字节中的比特位 6。

<span class="vcMarked">当密码标识被置为 0 时，载荷中**必须不**存在密码</span> <span class="vcReferred">[MQTT-3.1.2-18]</span>。<span class="vcMarked">当密码标识被置为 1 时，载荷中**必须**存在密码</span> <span class="vcReferred">[MQTT-3.1.2-19]</span>。

*非规范性评论*

*本版协议允许在不使用用户名时使用密码，和 MQTT v3.1.1 不同。这反映了密码作为密码以外的凭证的常见用途。*

#### 3.1.2.10 保活时间

图3-5 保活时间字节

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 9</td><td colspan="8">保活时间高位（MSB）</td></tr>
    <tr><td>byte 10</td><td colspan="8">保活时间地位（LSB）</td></tr>
  </tbody>
</table>

保活时间是一个表示时间间隔秒数的 2字节整数。他是允许客户端在发送一个 MQTT 包后到发送下一个数据包之间的最大时间间隔。客户端有责任确保两个 MQTT 包之间的时间间隔不超过保活时间。<span class="vcMarked">如果保活时间不为 0 且没有任何其他需要发送的数据包，客户端**必须**发送 PINGREQ 包</span> <span class="vcReferred">[MQTT-3.1.2-20]</span>。

<span class="vcMarked">如果服务器在 CONNACK 中提供了服务器保活时间，则客户端**必须**采用服务器保活时间的值来替代自己发送的保活时间的值</span> <span class="vcReferred">[MQTT-3.1.2-21]</span>。

不论保活时间的值如何设置，客户端可以在任何时间发送 PINGREQ，并通过检查相应的 PINGRESP 来确认服务器与网络是否可用。

<span class="vcMarked">如果保活时间为非零值且服务器在 1.5 倍的保活时间内没有收到来自客户端的任何 MQTT 包，服务器**必须**断开到客户端的网络连接并视为网络连接故障</span> <span class="vcReferred">[MQTT-3.1.2-22]</span>。

如果客户端在发送 PINGREQ 的合理时间后依然没有收到 PINGRESP，客户端应断开到服务器的网络连接。

保活时间的值为 0 表示关闭保活机制。当保活时间为 0 时客户端没有义务按任何特定时间发送 MQTT 包。

*非规范性评论*

*服务器可能会因为其他原因关闭向客户端的连接，例如服务器关机。设置保活时间并非意味着客户端可以持续保持连接。*

*非规范性评论*

*保活时间的具体值是由应用程序设置的，通常来说，是几分钟。保活时间的最大值 65535 表示 18小时12分钟15秒。*

#### 3.1.2.11 CONNECT属性集

##### 3.1.2.11.1 属性长度

CONNECT 包可变头中的属性集长度，使用变长整数编码。

##### 3.1.2.11.2 会话过期间隔

会话过期间隔的属性ID是**17 (0x11) Byte**。

随后跟随 4字节整数 用来表示会话过期间隔，单位为秒。在属性集中出现超过一次会话过期间隔视为协议错误。

当没有设置会话过期间隔是使用 0 作为默认值。如果会话过期间隔的值为 0 或者没有设置，当网络连接断开时会话立即结束。

如果会话过期间隔被设置为 0xFFFFFFFF (UINT_MAX)，表示会话不会过期。

<span class="vcMarked">当会话过期间隔的值大于 0 时，客户端和服务器都**必须**在网络连接断开后存储会话状态</span> <span class="vcReferred">[MQTT-3.1.2-23]</span>。

*非规范性评论*

*客户端或服务器的时钟可能在某些时间内没有运行，例如当客户端或服务器被关闭时。这可能会导致状态被延迟删除。*

参考 [4.1](#4-1-会话状态) 了解更多关于会话的信息。参考 [4.1.1](#4-1-1-存储会话状态) 了解更多关于会话状态存储的细节和限制。

当会话过期时，客户端与服务器不需要自动删除会话状态。

*非规范性评论*

*将全新开始标识设置为 1 并将会话过期间隔设置为 0，等同于在 MQTT v3.1.1 规范中将 CleanSession 设置为 1。将全新开始标识设置为 0 且不设置会话过期间隔，等同于在 MQTT v3.1.1 规范中将 CleanSession 设置为 0。*

*非规范性评论*

*一个只想处理其在线时消息的客户端可以将全新开始标识设置为 1 同时将会话过期间隔设置为 0。这样他将不会收到任何在他离线时产生的消息，并且他必须在每次连接后重新订阅所有他需要的主题。*

*非规范性评论*

*当客户端使用一个间歇性可用的网络连接服务器时，客户端可以设置一个较短的会话过期间隔这样每当网络连接可用时他都会重连并继续进行可靠的消息传递。而当客户端没有重连时，允许会话超时，这样应用消息就会丢失。*

*非规范性评论*

*当一个客户端使用较长的会话过期间隔连接服务器时，这意味着他希望服务器能够在他断开连接后的较长时间里维护会话状态。客户端只有在明确的意识到自己会在某个时间点重连时才使用这种较长的会话过期间隔。当一个客户端决定未来不再使用此会话，他应该在断开时将会话过期间隔设置为0。*

*非规范性评论*

*客户端总是应该基于 CONNACK 中的会话存在标识来判断服务器是否保存有该客户端的会话状态。*

*非规范性评论*

*客户端可以依赖服务器返回的会话存在标识来判断会话是否过期，而不必自己实现会话过期机制。如果客户端自己实现了会话过期机制，那么则必须在自己的会话状态中记录何时该会话状态需要被删除。*

##### 3.1.2.11.3 接收最大值

接收最大值的属性ID是**33 (0x21) Byte**。

随后跟随 2字节整数 用来表示有状态数据接收的最大值。接收最大值在属性集中出现超过一次，或接收最大值的值为0，均为协议错误。

客户端使用此值限制他同时处理的 QoS1 和 QoS2 包发布动作数量。没有任何机制限制服务器可能尝试的对 QoS0 包的发布。

接收最大值的值仅对当前网络连接有效。如果没有设置接收最大值那么他的默认值是 65535。

参考 [4.9 流量控制](#4-9-流量控制) 了解关于接收最大值的使用细节。

##### 3.1.2.11.4 最大包尺寸

最大包尺寸的属性ID是**33 (0x21) Byte**。

随后跟随 4字节整数 用来表示客户端可以接受的最大包尺寸。如果没有设置最大包尺寸，则其受限于固定头中的剩余长度限制，除此外并没有其他限制。

在属性集中出现超过一次最大包尺寸或其值为 0 均视为协议错误。

*非规范性评论*

*当包的尺寸需要被限制时，应用程序有责任选择一个合适的最大包尺寸的值。*

最大包尺寸表示 **MQTT 包完整的字节数**，其定义参考 [2.1.4](#2-1-4-剩余长度)。客户端使用最大包尺寸告知服务器，客户端不会处理超过此尺寸限制的信息。

<span class="vcMarked">服务器**必须不**向客户端发送超过最大包尺寸的数据包</span> <span class="vcReferred">[MQTT-3.1.2-24]</span>。如果客户端收到了超过其最大包尺寸限制的包，这被视为一个协议错误，客户端需要使用带有原因码 0x95（包过大）的 DISCONNECT 包来中断连接，参考 [4.13](#4-13-错误处理) 的描述。

<span class="vcMarked">当一个包因超过最大包尺寸而无法发送，服务器**必须**将其丢弃，并视为发送成功</span> <span class="vcReferred">[MQTT-3.1.2-25]</span>。

当某个包的尺寸大于共享订阅中的部分客户端的最大包尺寸，而又可以被另外的某些客户端接收时，服务器可以决定丢弃此包或者将其发送到可以接收此包的客户端。

*非规范性评论*

*当一个包未被发送即被丢弃时，服务器可以将其放入“丢包队列”或者提供其他的诊断机制。此类行为实现不属于本规范的范畴。*

##### 3.1.2.11.5 主题别名最大值

主题别名最大值的属性ID是**34 (0x22) Byte**。

随后跟随 2字节整数 表示主题别名的最大值。在属性集中出现超过一次主题别名最大值视为协议错误。如果主题别名最大值没有设置，则采用默认值 0。

主题别名最大值表示了客户端可以接受的来自服务器发送的主题别名的最大数量。客户端使用此值来约束他在本次连接中可以持有的主题别名数量。<span class="vcMarked">服务器**必须不**发送一个主题别名的值大于客户端设置的主题别名最大值的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.1.2-26]</span>。主题别名最大值的值为 0 表示客户端在本次连接中不支持任何主题别名。<span class="vcMarked">如果主题别名最大值未设置或值为 0，服务器**必须不**向客户端发送主题别名</span> <span class="vcReferred">[MQTT-3.1.2-27]</span>。

##### 3.1.2.11.6 请求响应信息

请求响应信息的属性ID是**25 (0x19) Byte**。

随后跟随一个值为 0 或 1 的字节。在属性集中出现超过一次请求响应信息，或其值不为 1 或 0，均视为协议错误。如果请求响应信息没有设置，则采用默认值 0。

客户端通过此值请求服务器，希望服务器在 CONNACK 中回复响应信息。<span class="vcMarked">此值为 0 表示服务器**必须不**在 CONNACK 中回复响应信息</span> <span class="vcReferred">[MQTT-3.1.2-28]</span>。此值为 1 表示服务器可以在 CONNACK 中回复响应信息。

*非规范性评论*

*即使客户端请求了，服务器也可以不在 CONNACK 中回复响应信息。*

参考 [4.10](#4-10-请求-响应) 了解关于 请求/响应 的更多信息。

##### 3.1.2.11.7 请求问题信息

请求问题信息的属性ID是**23 (0x17) Byte**。

随后跟随一个值为 0 或 1 的字节。在属性集中出现超过一次请求问题信息，或其值不为 1 或 0，均视为协议错误。如果请求问题信息没有设置，则采用默认值 0。

客户端通过此值表示服务器是是否应该在故障时发送原因字符串或用户属性。

<span class="vcMarked">如果请求问题信息的值为 0，服务器可以在 CONNACK 或 DISCONNECT 包中携带原因字符串或用户属性，但**必须不**在除 PUBLISH，CONNACK，DISCONNECT 之外的包中携带原因字符串或用户属性</span> <span class="vcReferred">[MQTT-3.1.2-29]</span>。如果请求问题信息的值为 0 且客户端接收到除 PUBLISH，CONNACK，DISCONNECT 之外的包中带有了原因字符串或用户属性，客户端使用带有原因码 0x82（协议错误）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理) 了解更多信息。

如果请求问题信息的值为 1，服务器可以在任何允许的包中返回原因字符串或用户属性。

##### 3.1.2.11.8 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 UTF-8字符串对。

用户属性可以出现多次，用来携带多个 键-值 对。同样的 键 允许出现超过一次。

*非规范性评论*

CONNECT 包中的用户属性可以用来从客户端向服务器发送连接过程中依赖的属性。这些属性的含义超出了本规范的范围。

##### 3.1.2.11.9 认证方式

认证方式的属性ID是**21 (0x15) Byte**。

随后跟随 UTF-8字符串，其中包括了使用的增强认证方式的名称。认证方式在属性集中出现超过一次视为协议错误。

如果没有设置认证方式，将不会执行增强认证。参考 [4.12](#4-12-增强认证)。

<span class="vcMarked">如果客户端再 CONNECK 包中设置了认证方式，那么在其收到 CONNACK 包之前，客户端**必须不**发送除了 AUTH 和 DISCONNECT 包之外的任何类型的包</span> <span class="vcReferred">[MQTT-3.1.2-30]</span>。

##### 3.1.2.11.10 认证数据

认证数据的属性ID是**22 (0x16) Byte**。

随后跟随 二进制数据 其中包括认证数据。当认证方式不存在是提供认证数据，或是在任何情况下提供超过一次的认证数据，均视为协议错误。

认证数据的内容由认证方式决定。参考 [4.12](#4-12-增强认证) 了解更多关于增强认证的信息。

#### 3.1.2.12 可变头非规范性示例

图3-6 可变头示例

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">协议名称</td></tr>
    <tr>
      <td>byte 1</td><td>长度高字节（MSB）（0）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 2</td><td>长度低字节（LSB）（4）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 3</td><td>‘M’</td>
      <td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 4</td><td>‘Q’</td>
      <td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 5</td><td>‘T’</td>
      <td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 6</td><td>‘T’</td>
      <td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td>
    </tr>
    <tr><td colspan="10">协议版本</td></tr>
    <tr>
      <td>byte 7</td><td>版本（5）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td>
    </tr>
    <tr><td colspan="10">连接标识</td></tr>
    <tr>
      <td>byte 8</td>
      <td>
        用户名标识（1）</br>
        密码标识（1）</br>
        遗嘱保留消息（0）</br>
        遗嘱QoS（01）</br>
        遗嘱标识（1）</br>
        全新开始（1）</br>
        保留（0）
      </td>
      <td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td>
    </tr>
    <tr><td colspan="10">保活时间</td></tr>
    <tr>
      <td>byte 9</td><td>保活时间高位（MSB）（0）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 10</td><td>保活时间低位（LSB）（10）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td>
    </tr>
    <tr><td colspan="10">属性集</td></tr>
    <tr>
      <td>byte 11</td><td>长度（5）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 12</td><td>属性ID：会话过期间隔（17）</td>
      <td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 13</td><td rowspan="4">会话过期间隔（10）</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 14</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 15</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 16</td>
      <td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td>
    </tr>
  </tbody>
</table>

### 3.1.3 CONNECT载荷

<span class="vcMarked">CONNECT 中的载荷包含了一个或多个 长度 + 内容 格式的字段，这些字段的存在与否由可变头中的标志位决定。这些字段的顺序是固定的，如果存在的话，**必须**按照 客户端ID，遗嘱属性集，遗嘱主题，遗嘱载荷，用户名，密码 这样的顺序出现</span> <span class="vcReferred">[MQTT-3.1.3-1]</span>。

#### 3.1.3.1 客户端ID

客户端ID用来在服务器端区分不同的客户端。每个连向服务器的客户端都拥有一个唯一的客户端ID。<span class="vcMarked">客户端ID**必须**被客户端和服务器用于关联客户端和服务器之间的会话状态</span> <span class="vcReferred">[MQTT-3.1.3-2]</span>。参考 [4.1](#4-1-会话状态) 了解更多关于会话状态的信息。

<span class="vcMarked">客户端ID**必须**作为 CONNECT 包载荷中的第一个字段出现</span> <span class="vcReferred">[MQTT-3.1.3-3]</span>。

<span class="vcMarked">客户端ID**必须**被编码为一个 `UTF-8字符串`</span>，该数据类型的定义在 [1.5.4](#1-5-4-UTF-8字符串) <span class="vcReferred">[MQTT-3.1.3-4]</span>。

<span class="vcMarked">服务器**必须**允许客户端ID是长度为 1 到 23 个字节之间的 `UTF-8字符串`，且仅包含下列字符：“0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ”</span> <span class="vcReferred">[MQTT-3.1.3-5]</span>。

服务器可以允许客户端ID的长度超过23字节。服务器可以允许客户端ID的内容包含上述以外的内容。

<span class="vcMarked">服务器**可以**允许客户端传递长度为 0 的客户端ID，当此情况发生时，服务器**必须**将此情况作为一个特殊情况对待，并为客户端分配一个唯一的客户端ID</span> <span class="vcReferred">[MQTT-3.1.3-6]</span>。<span class="vcMarked">服务器之后**必须**正常处理此 CONNECT 包，就如同客户端本身携带了这个唯一的客户端ID一样，而且**必须**在 CONNACK 包中返回这个分配的客户端ID</span> <span class="vcReferred">[MQTT-3.1.3-7]</span>。

<span class="vcMarked">如果服务器拒绝了客户端ID，服务器**可以**使用一个带有原因码 0x85（客户端ID不可用）的 CONNACK 包作为对客户端 CONNECT 包的响应，如同 [4.13](#4-13-错误处理) 中描述的那样，之后服务器**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.3-8]</span>。

*非规范性评论*

*客户端实现可以提供一个方便的生成随机客户端ID的方法。使用这种方法的客户端应该注意避免创建长期存在的孤立会话。*

#### 3.1.3.2 遗嘱属性集

如果遗嘱标识被置为 1，载荷中的下一个字段会是遗嘱属性集。遗嘱属性集决定了当遗嘱消息被发布时所使用的应用消息属性集，还决定了何时发布遗嘱消息。遗嘱属性集包含了属性长度和属性集内容。

##### 3.1.3.2.1 属性长度

遗嘱属性集中的属性集长度是一个变长整数。

##### 3.1.3.2.2 遗嘱延迟间隔

遗嘱延迟间隔的属性ID是**24 (0x18) Byte**。

随后跟随 4字节整数，表示遗嘱延迟间隔时间，单位为秒。遗嘱延迟间隔在属性集中出现超过一次视为协议错误。如果遗嘱延迟间隔未设置，默认值为0，表示遗嘱发布前没有间隔时间。

服务器在遗嘱延迟间隔结束或是会话结束时发布遗嘱，这两种条件以先触发的为准。<span class="vcMarked">如果在遗嘱延迟间隔结束前，该会话被新的网络连接延续，服务器**必须不**发送遗嘱</span> <span class="vcReferred">[MQTT-3.1.3-9]</span>。

*非规范性评论*

*遗嘱延迟间隔的一个作用是，当使用周期性可用的网络进行通信时，客户端使用遗嘱延迟间隔可以在遗嘱发布前重新连接并使用会话，而非每次连接断开后都发布遗嘱。*

*非规范性评论*

*当客户端和服务器的网络连接存在时，如果客户端再次使用相同的客户端ID连接到服务器，现有网络连接的遗嘱消息会被发布，除非新连接将 全新开始 标识置为 0 且遗嘱延迟间隔的值大于 0。如果遗嘱延迟间隔的值为 0，遗嘱消息会因为原有网络连接的关闭而发布，如果 全新开始 标识为 1 ，遗嘱消息会因为原有会话的结束而发布。*

##### 3.1.3.2.3 载荷格式标识

载荷格式标识的属性ID是**1 (0x01) Byte**。

随后的值表示遗嘱载荷的格式：

- 0（0x00）Byte 表示遗嘱消息是未指定的字节流，这等同于没有发送载荷格式标识。
- 1（0x01）Byte 表示遗嘱消息是 UTF-8字符串。载荷中的 UTF-8 数据必须符合 [Unicode](#1.3-Unicode) 和 [RFC3629](#1.3-RFC3629) 规范。

载荷格式标识在属性集中出现超过一次视为协议错误。服务器可以验证遗嘱消息是否符合载荷格式标识指定的格式，如果不符合则发送一个带有原因码 0x99（载荷格式错误）的 CONNACK 报文，详情参考 4.13。

##### 3.1.3.2.4 消息过期间隔

消息过期间隔的属性ID是**2 (0x02) Byte**。

随后跟随 4字节整数 用来表示消息过期间隔。消息过期间隔在属性集中出现超过一次视为协议错误。

当消息过期间隔存在时，此四字节的整数表示遗嘱消息的存活时间（单位秒），同时也是服务器发送此遗嘱消息时使用的发布过期时间。
 
如果没有设置此值，服务器发布遗嘱消息时不设置消息过期时间。

##### 3.1.3.2.5 内容类型

内容类型的属性ID是**3 (0x03) Byte**。

随后跟随 UTF-8字符串，表示遗嘱消息的内容类型。内容类型在属性集中出现超过一次视为协议错误。内容类型的值由发送方和接收方的应用程序定义。

##### 3.1.3.2.6 响应主题

响应主题的属性ID是**8 (0x08) Byte**。

随后跟随 UTF-8字符串，作为响应消息的主题名称。响应主题在属性集中出现超过一次视为协议错误。响应主题的存在表示将遗嘱消息视为一个请求。

参考 [4.10](#4-10-请求-响应) 了解关于 请求/响应 的更多信息。

##### 3.1.3.2.7 关联数据

关联数据的属性ID是**9 (0x09) Byte**。

随后跟随 二进制数据。请求消息的发送者使用关联数据来识别接收到的响应消息针对哪个请求。关联数据在属性集中出现超过一次视为协议错误。如果关联数据未设置，请求方无需携带任何关联数据。

关联数据的值仅对请求消息的发送者和响应消息的接收者有意义。

参考 [4.10](#4-10-请求-响应) 了解关于 请求/响应 的更多信息。

##### 3.1.3.2.8 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 UTF-8字符串对。用户属性允许出现多次来表示多个键值对。同样的键允许出现多次。

<span class="vcMarked">服务器**必须**在发布遗嘱消息时维持用户属性的顺序</span> <span class="vcReferred">[MQTT-3.1.3-10]</span>。

*非规范性评论*

*这个属性只是提供一种传输键值对的方式，键值对的含义和解释只有负责发送和接收该属性的应用程序了解。*

#### 3.1.3.3 遗嘱主题

如果遗嘱标识被置为 1，载荷中的下一个字段会是遗嘱主题。<span class="vcMarked">遗嘱主题**必须**是一个 `UTF-8字符串`</span>，参考 [1.5.4](#1-5-4-UTF-8字符串) 中的定义<span class="vcReferred">[MQTT-3.1.3-11]</span>。

#### 3.1.3.4 遗嘱载荷

如果遗嘱标识被置为 1，载荷中的下一个字段会是遗嘱载荷。如同 [3.1.2.5](#3-1-2-5-遗嘱标识) 的定义，遗嘱载荷是会被发布遗嘱主题中的应用消息。遗嘱载荷字段内含有二进制数据。

#### 3.1.3.5 用户名

如果用户名标识被置为 1，载荷中的下一个字段会是用户名。<span class="vcMarked">用户名**必须**是一个 `UTF-8字符串`</span>，参考 [1.5.4](#1-5-4-UTF-8字符串) 中的定义<span class="vcReferred">[MQTT-3.1.3-12]</span>。用户名可以被服务器用作认证和授权。

#### 3.1.3.6 密码

如果密码标识被置为 1，载荷中的下一个字段会是密码。密码字段内容是 二进制数据。虽然此字段被称为密码，但此字段实际上可以携带任何形式的凭据信息。

### 3.1.4 CONNECT动作

请注意，服务器可以在同一 TCP 端口或其他网络端点上支持多个协议（包括其他版本的 MQTT 协议）。如果服务器确定协议是 MQTT v5.0，则它会按如下方式验证连接尝试。

1. 如果服务器在客户端的网络连接建立后的一段合理时间内没有收到 CONNECT 包，服务器应该关闭网络连接。
2. <span class="vcMarked">服务器**必须**验证 CONNECT 包的格式符合 [3.1](#3-1-CONNECT-连接请求) 中的描述，如不符合则关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.4-1]</span>。服务器可以参考 4.13 在关闭网络连接前使用带有 0x80 或更高值的原因码的 CONNACK 通知客户端。
3. <span class="vcMarked">服务器**可以**检查 CONNECT 包中的内容是否满足更进一步的限制要求，并且**应该**进行认证和授权检查。如果其中任何检查失败，服务器**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.1.4-2]</span>。在关闭网络连接前，服务器可以参考 [3.2](#3-2-CONNACK-–-连接回复) 和 [4.13](#4-13-错误处理) 发送一个带有 0x80 或更高值的原因码的符合情况的 CONNACK 包。

如果验证成功，服务器施行下列动作。

1. <span class="vcMarked">如果客户端ID代表了一个已经连接到服务器的客户端，服务器参考 [4.13](#4-13-错误处理) 发送一个带有原因码 0x8E（会话被接管）的 DISCONNECT 包到当前已有连接的客户端，且**必须**关闭当前已有连接客户端的网络连接</span> <span class="vcReferred">[MQTT-3.1.4-3]</span>。如果已有连接的客户端包含遗嘱，遗嘱的发布情况参考 3.1.2.5。

*非规范性评论*

*如果已有连接的遗嘱延迟间隔值为0且存在遗嘱消息，遗嘱消息会因为网络连接断开的原因发布。当已有连接的会话过期间隔值为0，或是新连接的全新开始标识被置为 1时，如果已有连接存在遗嘱消息，那么遗嘱消息会被发布，因为原有会话已经在接管时结束。*

2.  <span class="vcMarked">服务器**必须**参考 [3.1.2.4](#3-1-2-4-全新开始) 中的描述处理全新开始标识</span> <span class="vcReferred">[MQTT-3.1.4-4]</span>。
3.  <span class="vcMarked">服务器**必须**使用带有原因码为 0x00（成功）的 CONNACK 回复 CONNECT 包</span> <span class="vcReferred">[MQTT-3.1.4-5]</span>。

*非规范性评论*

*如果服务器用于处理任何形式的业务关键数据，建议执行身份验证和授权检查。如果这些检查通过，服务器会使用带有原因码 0x00（成功）的 CONNACK 回复。如果检查失败，建议服务器根本不发送 CONNACK，因为这可能会提醒潜在攻击者 MQTT 服务器的存在，并鼓励此类攻击者发起拒绝服务或密码猜测攻击。*

4. 启动消息传递和保活监控。

客户端可以在发送 CONNECT 包之后立刻发送其他 MQTT 包；客户端无需等待接收到来自服务器的 CONNACK 包。<span class="vcMarked">如果服务器拒绝了 CONNECT，服务器**必须不**处理客户端在 CONNECT 包之后发送的任何除了 AUTH 以外的包</span> <span class="vcReferred">[MQTT-3.1.4-6]</span>。

*非规范性评论*

*客户端通常会等待 CONNACK 数据包，然而，客户端可以选择在接受 CONNACK 前发送其他 MQTT 数据包，这样做可能会简化客户端实现，因为客户端无需监管连接状态。客户端需要接受在其收到 CONNACK 前，如果服务器拒绝了连接，其发送的数据都不会被服务器处理。*

*非规范性评论*

*在接收 CONNACK 之前发送其他 MQTT 包的客户端将不知道服务器约束以及是否正在使用任何现有会话。*

*非规范性评论*
 
*如果客户端在认证完成前就发送了过多的数据，服务器可以限制从网络连接读取数据或关闭网络连接。建议将此作为避免拒绝服务攻击的一种方法。*

## 3.2 CONNACK - 连接确认

CONNACK 包是由服务器发送用来响应客户端发送的 CONNECT 包的MQTT包。<span class="vcMarked">服务器**必须**在发送除 AUTH 外的其他任何MQTT包之前使用带有响应码 0x00（成功）的 CONNACK 包回复客户端</span> <span class="vcReferred">[MQTT-3.2.0-1]</span>。<span class="vcMarked">服务器**必须不**在一次网络连接中发送超过一个 CONNACK 包</span> <span class="vcReferred">[MQTT-3.2.0-2]</span>。

如果客户端没有在合理的时间内收到来自服务器的 CONNACK 包，客户端**应该**断开网络连接。一个“合理”的时间取决于应用程序的类型和通信基础设施。

### 3.2.1 CONNACK固定头

固定头格式参考 图3-7。

*图3-7 CONNACK包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（2）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度字段**

这是使用可变整数编码的值，代表可变头的长度。

### 3.2.2 CONNACK可变头

CONNACK 包中的可变头按序包括了下列字段：连接回复标识，连接原因码，属性集。属性集的编码方式参考 [2.2.2](#2-2-2-属性集)。

#### 3.2.2.1 连接回复标识

<span class="vcMarked">Byte 1 是 “连接回复标识”。Bits 7-1 是保留字段，**必须**被置为 0</span> <span class="vcReferred">[MQTT-3.2.2-1]</span>。

Bit 0 是会话展示标识。

##### 3.2.2.1.1 会话展示

会话展示标识位于连接回复标识的 bit 0。

会话展示标识向客户端通知服务器是否在使用一个与客户端有相同客户端ID的连接的会话状态。这允许客户端和服务器对会话状态是否存在有一致的观点。

<span class="vcMarked">如果服务器接收连接的全新开始标识被置为 1，服务器**必须**在带有 0x00（成功）的原因码的 CONNACK 包中将会话展示置为 0</span> <span class="vcReferred">[MQTT-3.2.2-2]</span>。

<span class="vcMarked">如果服务器接收到的连接中全新开始位被置为 0，且服务器持有对此客户端ID的会话状态，服务器**必须**在 CONNACK 包中将会话展示标识置为 1，其他情况下，服务器都**必须**在 CONNACK 包中将会话展示标识置为 0。这两种情况下服务器都**必须**在 CONNACK 中使用原因码 0x00（成功）</span> <span class="vcReferred">[MQTT-3.2.2-3]</span>。

如果客户端从服务器接收到的会话展示的值不符合预期，客户端按照如下步骤继续：

- <span class="vcMarked">如果客户端不持有会话状态，且接收到的会话展示值为 1，客户端**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.2.2-4]</span>。如果客户端想要使用新的会话重启，客户端可以将全新开始标识置为 1 然后重新连接。
- <span class="vcMarked">如果客户端持有会话状态且收到的会话展示值为 0，如果客户端继续使用此网络连接，客户端**必须**丢弃会话状态</span> <span class="vcReferred">[MQTT-3.2.2-5]</span>。

<span class="vcMarked">如果服务器使用非 0 原因码的 CONNACK 包，服务器**必须**将会话展示的值置为 0</span> <span class="vcReferred">[MQTT-3.2.2-6]</span>。

#### 3.2.2.2 连接原因码

可变头中的 Byte 2 是连接原因码。

连接原因码的值如下表所示。当服务器收到一个格式正确的 CONNECT 包，但服务器无法完成连接时，服务器**可以**发送一个带有下表中合适原因码的 CONNACK 包。<span class="vcMarked">如果服务器发送的 CONNACK 包带有一个值为 128 或更高的原因码，服务器**必须**随后关闭网络连接</span> <span class="vcReferred">[MQTT-3.2.2-7]</span>。

*表 3-1 原因码值*

| 值 | Hex制值 | 原因码名称 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 连接被接受。 |
| 128 | 0x80 | 未指定错误 | 服务器不希望透露失败的原因，或者其他原因代码均不适用。 |
| 129 | 0x81 | 格式错误的包 | 无法正确解析 CONNECT 包中的数据。 |
| 130 | 0x82 | 协议错误 | CONNECT 包中的数据不符合此规范。 |
| 131 | 0x83 | 特定实现错误 | CONNECT 有效，但未被该服务器接受。 |
| 132 | 0x84 | 不支持的协议版本 | 服务器不支持客户端请求的 MQTT 协议版本。 |
| 133 | 0x85 | 客户端ID无效 | 客户端标识符是有效的字符串，但不被服务器允许。 |
| 134 | 0x86 | 用户名或密码错误 | 服务器不接受客户端指定的用户名或密码 |
| 135 | 0x87 | 未经授权 | 客户端无权连接。 |
| 136 | 0x88 | 服务器无法使用 | MQTT 服务器不可用。 |
| 137 | 0x89 | 服务器忙 | 服务器忙。稍后再试。 |
| 138 | 0x8A | 禁止 | 该客户端已被管理员禁止。请联系服务器管理员。 |
| 140 | 0x8C | 错误的身份验证方法 | 该身份验证方法不受支持或与当前使用的身份验证方法不匹配。 |
| 144 | 0x90 | 主题名称无效 | 遗嘱主题名称格式正确，但不被该服务器接受。 |
| 149 | 0x95 | 数据包太大 | CONNECT 数据包超出了最大允许大小。 |
| 151 | 0x97 | 超出配额 | 已超出实现或管理员设定的限制。 |
| 153 | 0x99 | 载荷格式错误 | 遗嘱载荷与指定的载荷格式标识不匹配。 |
| 154 | 0x9A | 不支持保留消息 | 服务器不支持保留消息，且遗嘱保留消息被置为 1。 |
| 155 | 0x9B | 不支持 QoS | 服务器不支持 QoS，且遗嘱 QoS 被置为 1。 |
| 156 | 0x9C | 使用另一台服务器 | 客户端应暂时使用另一台服务器。 |
| 157 | 0x9D | 服务器已迁移 | 客户端应永久使用另一台服务器。 |
| 159 | 0x9F | 连接频率超限 | 已超出连接速率限制。 |

<span class="vcMarked">服务器发送的 CONNACK 包**必须**使用上表中之一的原因码</span> <span class="vcReferred">[MQTT-3.2.2-7]</span>。

*非规范性评论*

*原因码 0x80（未指定错误）可以用在服务器了解故障原因，但不想透露给客户端的时候，或没有其他合适原因码可用的时候。*

*当在 CONNECT 中发现错误时，服务器可以选择不发送 CONNACK 而直接关闭连接，用以提升安全性。例如，当在一个公共网络中，且连接没有被授权，向客户端透露服务器是 MQTT 服务器可能是不明智的。*

#### 3.2.2.3 CONNACK属性集

##### 3.2.2.3.1 属性长度

属性长度是变长整数编码的表示 CONNACK 中属性集长度的值。

##### 3.2.2.3.2 会话过期间隔

会话过期间隔的属性ID是**17 (0x11) Byte**。

随后跟随 `4字节整数` 用来表示会话过期间隔，单位为秒。在属性集中出现超过一次会话过期间隔视为协议错误。

如果会话过期间隔未设置，则使用 CONNECT 包中的值。服务器通过在 CONNACK 中的此属性告知客户端使用非客户端设置的值。参考 3.1.2.11.2 了解关于会话过期间隔的描述。

##### 3.2.2.3.3 接收最大值

接收最大值的属性ID是**33 (0x21) Byte**。

随后跟随 `2字节整数` 用来表示有状态数据接收的最大值。接收最大值在属性集中出现超过一次，或接收最大值的值为0，均为协议错误。

服务器使用此值限制他同时处理的 QoS1 和 QoS2 包发布动作数量。没有任何机制限制客户端可能尝试的对 QoS0 包的发布。

接收最大值的值仅对当前网络连接有效。如果没有设置接收最大值那么他的默认值是 65535。

参考 [4.9 流量控制](#4-9-流量控制) 了解关于接收最大值的使用细节。

##### 3.2.2.3.4 最大QoS

最大QoS的属性ID是**36 (0x24) Byte**。

随后跟随值为 0 或 1 的 `Byte`。最大QoS在属性集中出现超过一次，或最大QoS的值不为 0 或 1，均为协议错误。如果接收最大值未设置，客户端可以使用的最大QoS值为 2。

<span class="vcMarked">如果服务器不支持 QoS 1 或 QoS 2 的 PUBLISH，服务器**必须**发送一个带有其可以支持的最大QoS的 CONNACK 包</span> <span class="vcReferred">[MQTT-3.2.2-9]</span>。<span class="vcMarked">一个不支持 QoS 1 或 QoS 2 PUBLISH 的服务器**必须**依然接收包含 QoS 0、1 或 2 的 SUBSCRIBE 包</span> <span class="vcReferred">[MQTT-3.2.2-10]</span>。

<span class="vcMarked">如果客户端从服务器接收了最大QoS，客户端**必须不**发送 QoS 等级超过最大QoS的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.2.2-11]</span>。服务器收到了超过已指定最大QoS等级的 PUBLISH 包视为协议错误。这种情况下需使用带有原因码 0x9B（不支持的 QoS）的 DISCONNECT 断开连接，参考 [4.13](#4-13-错误处理) 错误处理。

<span class="vcMarked">如果服务器收到包含超过其能力的遗嘱QoS的 CONNECT 数据包，服务器**必须**拒绝连接。服务器**应该**回复带有原因码 0x9B（不支持的 QoS）的 CONNACK 包，参考 [4.13](#4-13-错误处理) 错误处理，且随后**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.2.2-12]</span>。

*非规范性评论*

*客户端不必须支持 QOS 1 或 QOS 2 的 PUBLISH 包。在这种情况下，客户端只需简单的在 SUBSCRIBE 中将最大QoS字段设置为其可支持的值。*

##### 3.2.2.3.5 保留消息可用

保留消息可用的属性ID是**37 (0x25) Byte**。

随后跟随一个 `Byte`。当此字段存在时，此 Byte 表示服务器是否支持保留消息。值为 0 表示不支持保留消息。值为 1 表示支持保留消息。如果此字段不存在，默认表示支持保留消息。保留消息可用在属性集中出现超过一次，或保留消息可用的值不为 0 或 1，均为协议错误。

<span class="vcMarked">如果服务器接收到的 CONNECT 包中包含遗嘱消息，且遗嘱保留消息的值为 1，同时服务器不支持保留消息，服务器**必须**拒绝此连接请求。服务器**应该**发送带有原因码 0x9A（不支持保留消息）的 CONNACK 且随后**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.2.2-13]</span>。

<span class="vcMarked">一个收到了服务器发送的保留消息可用值为 0 的客户端，**必须不**发送带有保留消息标识为 1 的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.2.2-14]</span>。如果服务器收到了此种包，视为协议错误。服务器**应该**发送带有原因码为 0x9A（不支持保留消息）的 DISCONNECT 包，参考 [4.13](#4-13-错误处理)。

##### 3.2.2.3.6 最大包尺寸

最大包尺寸的属性ID是**33 (0x21) Byte**。

随后跟随 `4字节整数` 用来表示服务器可以接受的最大包尺寸。如果没有设置最大包尺寸，则其受限于固定头中的剩余长度限制，除此外并没有其他限制。

在属性集中出现超过一次最大包尺寸或其值为 0 均视为协议错误。
 
最大包尺寸表示 **MQTT 包完整的字节数**，其定义参考 [2.1.4](#2-1-4-剩余长度)。服务器使用最大包尺寸告知客户端，服务器不会处理超过此尺寸限制的信息。

<span class="vcMarked">客户端**必须不**向服务器发送超过最大包尺寸的数据包</span> <span class="vcReferred">[MQTT-3.2.2-15]</span>。如果服务器收到了超过其最大包尺寸限制的包，这被视为一个协议错误，服务器需要使用带有原因码 0x95（包过大）的 DISCONNECT 包来中断连接，参考 [4.13](#4-13-错误处理) 的描述。
 
##### 3.2.2.3.7 分配的客户端ID

分配的客户端ID的属性ID是**18 (0x12) Byte**。

随后跟随 `UTF-8字符串` 表示被分配的客户端ID。分配的客户端ID在属性集中出现超过一次视为协议错误。

由于在客户端发送的 CONNECT 包中的客户端ID长度为0，因此由服务器来分配客户端ID。

<span class="vcMarked">如果客户端使用长度为 0 的客户端ID连接，服务器**必须**使用带有分配的客户端ID的 CONNACK 回复。分配的客户端ID**必须**是一个当前所有会话都没有使用的全新ID</span> <span class="vcReferred">[MQTT-3.2.2-16]</span>。

##### 3.2.2.3.8 主题别名最大值

主题别名最大值的属性ID是**34 (0x22) Byte**。

随后跟随 `2字节整数` 表示主题别名的最大值。在属性集中出现超过一次主题别名最大值视为协议错误。如果主题别名最大值没有设置，则采用默认值 0。

主题别名最大值表示了服务器可以接受的来自客户端发送的主题别名的最大数量。服务器使用此值来约束他在本次连接中可以持有的主题别名数量。<span class="vcMarked">客户端**必须不**能发送一个主题别名的值大于服务器设置的主题别名最大值的 PUBLISH 包 </span> <span class="vcReferred">[MQTT-3.2.2-17]</span>。主题别名最大值的值为 0 表示服务器在本次连接中不支持任何主题别名。<span class="vcMarked">如果主题别名最大值未设置或值为 0，客户端**必须不**向服务器发送主题别名</span> <span class="vcReferred">[MQTT-3.2.2-18]</span>。

##### 3.2.2.3.9 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示本次响应的原因。原因字符串是一个被设计用来诊断问题的人类可读的字符串，原因字符串**不应该**被客户端解析。

服务器使用本字段向客户端提供课外的信息。<span class="vcMarked">如果因为添加原因字符串会导致 CONNACK 的包尺寸超过了客户端限制的最大包尺寸，服务器**必须不**发送此属性</span> <span class="vcReferred">[MQTT-3.2.2-19]</span>。原因字符串在属性出现超过一次视为协议错误。

*非规范性评论*

*客户端使用原因字符串的正确用法包括将其在异常中抛出或将其写入日志。*

##### 3.2.2.3.10 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用来向客户端提供包括诊断消息在内的扩展信息。<span class="vcMarked">如果添加该属性会导致 CONNACK 的包尺寸大于客户端设置的最大包尺寸，服务器**必须不**添加此属性</span> <span class="vcReferred">[MQTT-3.2.2-20]</span>。用户属性可以出现多次，用来携带多个 键-值 对。同样的 键 允许出现超过一次。

本属性的内容和含义不由本规范定义。CONNACK 的接收者在接收到本属性后**可以**选择忽略。

##### 3.2.2.3.11 通配符订阅可用

通配符订阅可用的属性ID是**40 (0x28) Byte**。

随后跟随一个 `Byte`。当该字段存在时，该 byte 表示服务器是否支持通配符订阅。值为 0 表示不支持通配符订阅。值为 1 表示支持通配符订阅。当该字段不存在时，默认表示支持通配符订阅。通配符订阅可用在属性集中出现超过一次，或其值不为 0 或者 1，均视为协议错误。
 
如果服务器不支持通配符订阅，但接收到了一个包含通配符的 SUBSCRIBE 包，则视为一个协议错误。服务器需要使用带有原因码 0xA2（不支持通配符订阅）的 DISCONNECT 包断开连接，具体参考 [4.13](#4-13-错误处理)。

如果服务器支持通配符订阅，他仍然可以拒绝包含某种特别通配符的订阅请求。在这种情况下服务器**可以**发送一个带有原因码 0xA2（不支持通配符订阅）的 SUBACK包。

##### 3.2.2.3.12 订阅ID可用

订阅ID可用的属性ID是**41 (0x29) Byte**。

随后跟随一个 `Byte`。当该字段存在时，该 byte 表示服务器是否支持订阅ID。值为 0 表示不支持订阅ID。值为 1 表示支持订阅ID。当该字段不存在时，默认表示支持订阅ID。订阅ID可用在属性集中出现超过一次，或其值不为 0 或者 1，均视为协议错误。

如果服务器不支持订阅ID，但接收到了一个包含订阅ID的 SUBSCRIBE 包，则视为一个协议错误。服务器需要使用带有原因码 0xA1（不支持订阅ID）的 DISCONNECT 包断开连接，具体参考 [4.13](#4-13-错误处理)。

##### 3.2.2.3.13 共享订阅可用

共享订阅可用的属性ID是**42 (0x2A) Byte**。

随后跟随一个 `Byte`。当该字段存在时，该 byte 表示服务器是否支持共享订阅。值为 0 表示不支持共享订阅。值为 1 表示支持共享订阅。当该字段不存在时，默认表示支持共享订阅。共享订阅可用在属性集中出现超过一次，或其值不为 0 或者 1，均视为协议错误。
 
如果服务器不支持共享订阅，但接收到了一个包含共享订阅的 SUBSCRIBE 包，则视为一个协议错误。服务器要使用带有原因码 0x9E（不支持共享订阅）的 DISCONNECT 包断开连接，具体参考 [4.13](#4-13-错误处理)。

##### 3.2.2.3.14 服务器保活时间

服务器保活时间的属性ID是**19 (0x13) Byte**。

随后跟随一个 `2字节整数` 表示服务器指定的保活时间。<span class="vcMarked">如果服务器在 CONNACK 中发送了服务器保活时间，客户端**必须**使用此值代替其在 CONNECT 中发送的保活时间</span> <span class="vcReferred">[MQTT-3.2.2-21]</span>。<span class="vcMarked">如果服务器没有设置服务器保活时间，服务器**必须**使用客户端在 CONNECT 包中设置的保活时间</span> <span class="vcReferred">[MQTT-3.2.2-22]</span>。服务器保活时间在属性集中出现超过一次视为协议错误。

*非规范性评论*

*服务器保活时间的主要用途是让服务器通知客户端，他将比客户端指定的保活时间更早地断开与客户端的不活动连接。*

##### 3.2.2.3.15 响应信息

响应信息的属性ID是**26 (0x1A) Byte**。

随后跟随一个 `UTF-8字符串` 用来表示构建响应主题的基础。客户端如何通过响应信息构建响应主题不由本规范定义。响应信息在属性集中出现超过一次视为协议错误。

如果客户端发送的请求响应信息值为 1，服务器**可选**则是否在 CONNACK 中包括响应信息。

*非规范性评论*

*响应信息的常见用法是将响应信息作为响应主题中的某一部分，该部分为此客户端在其会话周期内保留。这一部分往往不能是一个随机的名称，因为请求客户端和响应客户端都需要通过授权才能使用此主题。这部分通常特定客户端的主题树的跟。为了让服务器能够返回此信息，通常需要进行一些正确的配置。使用本机制可以在服务端一次性配置响应信息，而非是在请求客户端和响应客户端中各自完成。*

参考 [4.10](#4-10-请求-响应) 了解更多关于 请求/响应 的信息。

##### 3.2.2.3.16 服务引用

服务引用的属性ID是**28 (0x1C) Byte**。

随后跟随 `UTF-8字符串`，可被客户端用于定位到另一台服务器。服务引用在属性集中出现超过一次视为协议错误。

服务器在原因码为 0x9C（使用另一台服务器）或 0x9D（服务器迁移）的 CONNACK 或 DISCONNECT 包中使用服务引用，具体用法参考 [4.13](#4-13-错误处理)。

参考 [4.11](#4-11-服务重定向) 了解服务引用的用法。

##### 3.2.2.3.17 认证方式

认证方式的属性ID是**21 (0x15) Byte**。

随后跟随 `UTF-8字符串`，内含认真方式的名称。认证方式在属性集中出现超过一次视为协议错误。参考 [4.12](#4-12-增强认证) 了解跟多关于增强认证的信息。

##### 3.2.2.3.18 认证数据

认证数据的属性ID是**22 (0x16) Byte**。

随后跟随 `二进制数据`，内含认证数据。数据的内容由认证方式和当然交换状态定义。认证数据在属性集中出现超过一次视为协议错误。参考 [4.12](#4-12-增强认证) 了解跟多关于增强认证的信息。

### 3.2.3 CONNACK载荷

CONNACK 没有载荷。

## 3.3 PUBLISH - 发布消息

PUBLISH 包可以由客户端发往服务端，或由服务端发往客户端，用于传输应用消息。

### 3.3.1 PUBLISH 固定头

*图 3‑8 – PUBLISH 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（3）</td><td>重复标识</td><td colspan="2">QoS等级</td><td>保留消息</td></tr>
    <tr><td></td><td>0</td><td>0</td><td>1</td><td>1</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
    <tr><td>byte 2...</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

#### 3.3.1.1 重复标识

**位置：** byte 1，bit 3。

如果重复标识的值为 0，这表示这是客户端或服务器第一次尝试发送此 PUBLISH 包。如果重复标识的值为 1，这表示本包可能是之前尝试发送包的重传。

<span class="vcMarked">当客户端或服务器尝试重传 PUBLISH 包时，他们**必须**把重复标志置为 1</span> <span class="vcReferred">[MQTT-3.3.1-1]</span>。<span class="vcMarked">对于 QoS 0 的消息，重复标识**必须**被置为 0</span> <span class="vcReferred">[MQTT-3.3.1-2]</span>。

当服务器将 PUBLISH 包转发给订阅者时，来自传入 PUBLISH 包的重复标识不会传播。<span class="vcMarked">转发的 PUBLISH 包的重复标识独立于接收的 PUBLISH 包，此值仅被本次转发包是否为重传独立决定</span> <span class="vcReferred">[MQTT-3.3.1-3]</span>。

*非规范性评论*

*MQTT包的接收方接收到重复标志为 1 的包并不能假设他已经接收到了此包的早期副本。*

*非规范性评论* 

*需要注意的是，重复标识仅表示 MQTT 包的重复，并不能表示其中应用消息的重复。当使用 QoS 1 时，客户端有可能接收到重复标志为 0 的包，但其中包含的应用消息却是早已接收的，只是包ID不同。章节 [2.2.1](#2-2-1-包ID) 提供了更多关于包ID的信息。*

#### 3.3.1.2 QoS

**位置：** byte 1，bit 2-1。

该字段表示应用消息传送的保障级别。QoS 级别如下表所示。

表 3-2 QoS 定义

| QoS 值 | bit 2 | bit 1 | 描述 |
| --- | --- | --- | --- |
| 0 | 0 | 0 | 至多一次 |
| 1 | 0 | 1 | 至少一次 |
| 2 | 1 | 0 | 确保一次 |
| - | 1 | 1 | 保留 - 不可使用 |

如果客户端在 CONNACK 中向服务器提示了最大QoS，之后收到了超过最大QoS值的 PUBLISH 包，服务器使用带有原因码 0x9B（不支持的QoS）的 DISCONNECT 包断开连接，如同 [4.13](#4-13-错误处理) 中的描述。

<span class="vcMarked">PUBLISH 包**必须不**能将 QoS 的两个 bit 都设置为 1</span> <span class="vcReferred">[MQTT-3.3.1-4]</span>。如果服务器或者客户端接收到了两个 bit 都为 1 的 PUBLISH 包，视为格式错误的包，使用带有原因码 0x81（格式错误的包）的 DISCONNECT 断开连接，参考 [4.13](#4-13-错误处理)。

#### 3.3.1.3 保留消息

**位置：** byte 1，bit 0。

<span class="vcMarked">当客户端向服务器发送的 PUBLISH 包中的保留消息被置为 1 时，服务器**必须**在此主题下保存此应用消息，替换任何已经存在的消息</span> <span class="vcReferred">[MQTT-3.3.1-5]</span>，之后该保留消息可以被发布给订阅该主题的订阅者。<span class="vcMarked">如果载荷为空，服务器照常处理，只不过该同名主题下现有的保留消息**必须**被移除，未来的订阅者也不会再收到保留消息</span> <span class="vcReferred">[MQTT-3.3.1-6]</span>。<span class="vcMarked">带有空载荷的保留消息**必须不**被服务器作为保留消息存储</span> <span class="vcReferred">[MQTT-3.3.1-7]</span>。

<span class="vcMarked">如果客户端发送到服务器的 PUBLISH 包中的保留消息值为 0，服务器**必须不**将该消息作为保留消息存储且**必须不**删除或替换已经存在的保留消息</span> <span class="vcReferred">[MQTT-3.3.1-8]</span>。

如果服务器回复的 CONNACK 带有保留消息可用标识且其值为 0，此时服务器又收到了带有保留消息值为 1 的 PUBLISH 包，服务器需使用带有原因码 0x9A（不支持保留消息）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理)。

当一个新的非共享订阅创建时，如果存在保留消息，每个匹配主题名上的保留消息都按照订阅选项中的保留消息处理标识的指示发往客户端。这些消息发送时的保留消息标识都置为 1。保留消息是否发送由订阅选项中的保留消息处理字段控制。当客户端进行订阅时：

- <span class="vcMarked">如果保留消息处理值为 0，服务器**必须**将匹配订阅主题过滤器的保留消息发送给客户端</span> <span class="vcReferred">[MQTT-3.3.1-9]</span>。
- <span class="vcMarked">如果保留消息处理值为 1，当该订阅之前不存在时，服务器**必须**将匹配订阅主题过滤器的保留消息发送给客户端，反之当该订阅之前存在时，服务器**必须不**发送保留消息</span> <span class="vcReferred">[MQTT-3.3.1-10]</span>。
- <span class="vcMarked">如果保留消息处理值为 2，服务器**必须不**发送保留消息</span> <span class="vcReferred">[MQTT-3.3.1-11]</span>。

参考 [3.8.3.1](#3-8-3-1-订阅选项) 了解关于订阅选项的定义。

当服务器接收到保留消息值为 1，QoS 值为 0 的 PUBLISH 包，服务器**应该**存储这个新的 QoS 值为 0 的消息作为该主题新的保留消息，但是**可以**在任何时候丢弃他。如果服务器丢弃了该消息，该主题下将没有保留消息。

如果主题下的保留消息过期，他将会被丢弃且主题下将没有保留消息。

服务器向已经建立的连接转发的应用消息中保留消息的值是由订阅选项中的保留消息引用发布选项决定的。参考 [3.8.3.1](#3-8-3-1-订阅选项) 了解关于订阅选项的定义。

- <span class="vcMarked">如果保留消息引用发布的值为 0，服务器**必须**在转发应用消息时将保留消息值置为 0，无论其收到的 PUBLISH 包中的保留消息值如何设置</span> <span class="vcReferred">[MQTT-3.3.1-12]</span>。
- <span class="vcMarked">如果保留消息引用发布的值为 1，服务器**必须**使用和收到的 PUBLISH 包中保留消息值相同的保留消息值</span> <span class="vcReferred">[MQTT-3.3.1-13]</span>。

*非规范性评论*

*当发布者不规律的发布状态消息时，保留消息非常有用。新的非共享订阅者会受到最新的状态。*

#### 3.3.1.4 剩余长度

剩余长度是 `变长整数`，表示可变头与载荷的总长度。

### 3.3.2 PUBLISH可变头

PUBLISH 可变头按顺序包含下列字段：主题名称，包ID，属性集。属性集的编码规则参考 [2.2.2](#2-2-2-属性集)。

#### 3.3.2.1 主题名称

主题名称决定了载荷发布的信息通道。

<span class="vcMarked">主题名称**必须**作为 PUBLISH 包可变头的第一个字段。他**必须**采用 `UTF-8字符串` 编码</span>，定义参考 [1.5.4](#1-5-4-UTF-8字符串) <span class="vcReferred">[MQTT-3.3.2-1]</span>。

<span class="vcMarked">PUBLISH 包中的主题名称**必须不**包含通配符</span> <span class="vcReferred">[MQTT-3.3.2-2]</span>。

<span class="vcMarked">服务器发往客户端的 PUBLISH 包中的主题名称必须匹配订阅者的主题过滤器</span>，匹配流程参考 [4.7](#4-7-主题名和主题过滤器) <span class="vcReferred">[MQTT-3.3.2-3]</span>。然而，考虑到服务器允许进行主题名称映射，转发的 PUBLISH 包的主题名称可以与原始 PUBLISH 包的主题名称不同。

为了减少 PUBLISH 包的尺寸，发送者可以使用主题别名。主题别名的描述参考 [3.3.2.3.4](#3-3-2-3-4-主题别名)。主题名称长度为 0 且没有主题别名视为协议错误。

#### 3.3.2.2 包ID

仅当 QoS 等级为 1 或 2 的 PUBLISH 包中存在包ID字段，章节 [2.2.1](#2-2-1-包ID) 提供了更多关于包ID的信息。

#### 3.3.2.3 PUBLISH属性集

##### 3.3.2.3.1 属性长度

属性长度是变长整数编码的表示 PUBLISH 中属性集长度的值。

##### 3.3.2.3.2 载荷格式标识

载荷格式标识的属性ID是**1 (0x01) Byte**。

随后跟随的值表示载荷格式，二选其一：

- 0（0x00）Byte 表示载荷格式未指定，等同于没有发送载荷格式字段。
- 1（0x01）Byte 表示载荷是UTF-8编码的字符数据。载荷中的UTF-8数据**必须**是编码良好的UTF-8格式，符合 [Unicode](#1.3-Unicode) 规范和 [RFC3629](#1.3-RFC3629)。

<span class="vcMarked">服务器**必须**将载荷格式标识原封不动的发送给所有应用消息的接收者</span> <span class="vcReferred">[MQTT-3.3.2-4]</span>。接收者**可以**验证载荷是否和更是标志匹配，当不匹配时，发送带有原因码 0x99（载荷格式错误）的 PUBACK、PUBREC 或 DISCONNECT，参考 [4.13](#4-13-错误处理)。参考 [5.4.9](#5-4-9-处理禁止的Unicode码段) 了解关于验证载荷格式的安全建议。

##### 3.3.2.3.3 消息过期间隔

载荷格式标识的属性ID是**2 (0x02) Byte**。

随后跟随 `4字节整数`，表示消息过期间隔。

<span class="vcMarked">当该字段存在时，此四字节的值表示以秒为单位的应用消息生命时间。如果消息过期间隔已经超时，且服务器尚未设法开始向前传递到匹配的订阅者，服务器**必须**删除面向该订阅者的该消息的副本</span> <span class="vcReferred">[MQTT-3.3.2-5]</span>。

如果该字段不存在，应用消息不会过期。

<span class="vcMarked">客户端发送给服务器的 PUBLISH 包中的消息过期间隔**必须**被设置为服务器接收的消息过期间隔的值减去消息在服务器中等待的时间</span> <span class="vcReferred">[MQTT-3.3.2-6]</span>。参考 [4.1](#4-1-会话状态) 了解关于存储状态的更多细节和限制。

##### 3.3.2.3.4 主题别名

主题别名的属性ID是**35 (0x23) Byte**。

随后跟随 `2字节整数` 表示主题别名的值。主题别名在属性集中出现超过一次视为协议错误。

主题别名是一个用于替代主题名来区分主题的整数值。使用主题别名可以减少 PUBLISH 包的尺寸，主题别名在主题名较长且同一个主题名被反复使用的网络连接中有很大作用。

发送者可以决定是否使用主题别名，以及主题别名的值。他在 PUBLISH 包中创建了一个非零长度主题名和主题别名值的映射。接收者正常处理 PUBLISH 包，但需要同样添加该主题别名到主题名的映射。

一旦接收者设置了主题别名的映射，发送者可以发送包含主图别名的 PUBLISH 包，其中主题名可以为零长度。接收者将按照其中包含正常主题名的方式对待此 PUBLISH 包。

发送者可以在同一网络连接中通过再次发送一个带有相同的主题别名和不同的主题名 PUBLISH 包的方式改变主题别名的映射。
 
主题别名映射仅在单次网络连接中存在，其生命周期等同于网络连接的生命周期。<span class="vcMarked">接收者**必须不**能将主题别名从一个网络连接转发到另一个网络连接</span> <span class="vcReferred">[MQTT-3.3.2-7]</span>。

主题别名的值不可为 0。<span class="vcMarked">发送者**必须不**能发送一个包含主题别名值为 0 的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.3.2-8]</span>。

<span class="vcMarked">客户端**必须不**发送包含主题别名值超过服务器 CONNACK 中设置的主题别名最大值的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.3.2-9]</span>。<span class="vcMarked">客户端**必须**接收所有大于 0 且小于或等于其 CONNECT 包中设置的主题别名最大值的主题别名</span> <span class="vcReferred">[MQTT-3.3.2-10]</span>。

<span class="vcMarked">服务器**必须不**发送包含主题别名值超过客户端 CONNECT 包中设置的主题别名最大值的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.3.2-11]</span>。<span class="vcMarked">服务器**必须**接收所有大于 0 且小于等于其 CONNACK 包中设置的主题别名最大值的主题别名</span> <span class="vcReferred">[MQTT-3.3.2-12]</span>。

客户端和服务器使用的主题别名映射是互相独立的。因此，当一个客户端发送的 PUBLISH 包中的主题别名为 1，同时服务器发送的 PUBLISH 包中的主题别名也为 1 一般来说引用了不同的主题。

##### 3.3.2.3.5 响应主题

响应主题的属性ID是**8 (0x08) Byte**。

随后跟随 `UTF-8字符串` 作为响应消息的主题名。<span class="vcMarked">响应主题**必须**使用 `UTF-8字符串` 格式</span>，其定义参考 [1.5.4](#1-5-4-UTF-8字符串) <span class="vcReferred">[MQTT-3.3.2-13]</span>。<span class="vcMarked">响应主题**必须不**包含通配符</span> <span class="vcReferred">[MQTT-3.3.2-14]</span>。响应主题在属性集中出现超过一次视为协议错误。响应主题的出现表示该消息是一个请求。

参考 [4.10](#4-10-请求-响应) 了解更多关于 请求/响应 的信息。

<span class="vcMarked">服务器**必须**向所有接收该应用消息的订阅者原封不动的转发响应主题</span> <span class="vcReferred">[MQTT-3.3.2-15]</span>。

*非规范性评论*

*带有响应主题的应用消息的接收者通过使用响应主题作为 PUBLISH 的主题名称来发送响应。如果请求消息包含关联数据，则响应方还应该将该关联数据作为响应消息的 PUBLISH 数据包中的属性。*

##### 3.3.2.3.6 关联数据

关联数据的属性ID是**9 (0x09) Byte**。

随后跟随 `二进制数据`。关联数据是由发送方添加在请求消息里，用于在响应消息中确定响应消息和请求消息的关联关系。关联数据在属性集中出现超过一次视为协议错误。如果没有设置关联数据，表示请求者无需任何关联数据。

<span class="vcMarked">服务器**必须**将关联数据原封不动的转发给接收应用消息的订阅者</span> <span class="vcReferred">[MQTT-3.3.2-16]</span>。关联数据的值仅对请求的发送者和响应的接收者有意义。

*非规范性评论*

*接受了包含响应主题和关联数据的应用消息的接收者，通过响应主题发送 PUBLISH 包作为响应。同时也应该在响应的 PUBLISH 包中原封不动的设置关联数据。*

*非规范性评论*

*如果响应中的关联数据内容改变会导致应用程序故障，那么此数据应该通过加密、哈希等手段来确保其改变可以被监测。*

参考 [4.10](#4-10-请求-响应) 了解更多关于 请求/响应 的信息。

##### 3.3.2.3.7 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。用户属性可以出现多次，用来携带多个 键-值 对。同样的 键 允许出现超过一次。

<span class="vcMarked">服务器**必须**将 PUBLISH 包中的所有用户属性原封不动的转发给客户端</span> <span class="vcReferred">[MQTT-3.3.2-17]</span>。<span class="vcMarked">服务器**必须**在转发应用消息时维护用户属性的顺序</span> <span class="vcReferred">[MQTT-3.3.2-18]</span>。

*非规范性评论*

*该属性旨在提供一种传输应用层键-值对的方法，其含义和解释只有负责发送和接收它们的应用程序了解。*

##### 3.3.2.3.8 订阅ID

订阅ID的属性ID是**11 (0x0B) Byte**。

随后跟随 `变长整数` 表示订阅动作的ID。

订阅ID的取值范围是 1 到 268435455。订阅ID的值为0视为协议错误。如果本次发布是匹配了多次重复订阅的发布，属性集中出现多次订阅ID也是合理的，此种情况下他们的顺序不重要。

##### 3.3.2.3.9 内容类型

内容类型的属性ID是**3 (0x03) Byte**。

随后跟随 `UTF-8字符串` 描述了应用消息的内容类型。<span class="vcMarked">内容类型**必须**是 `UTF-8字符串` 格式</span>，其定义参考 [1.5.4](#1-5-4-UTF-8字符串) <span class="vcReferred">[MQTT-3.3.2-19]</span>。

内容格式在属性集中出现超过一次视为协议错误。内容格式的值由发送方和接收方定义。

<span class="vcMarked">服务器**必须**将内容格式原封不动的转发给所有接收应用消息的订阅者</span> <span class="vcReferred">[MQTT-3.3.2-20]</span>。

*非规范性评论*

*这个UTF-8编码的字符串可以使用 MIME 类型字符串来描述应用消息的类型。当然，由于该字段由发送方和接收方负责定义和解释，MQTT不会检查该字段的内容或格式。*

*非规范性示例*

*图 3-9 展示了一个 PUBLISH 包的例子，其主题名为 “a/b”，其包ID为10，且没有属性集。*

图 3-9 PUBLISH 包可变头非规范性示例

<table>
  <thead>
    <tr>
      <td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="10">主题名称</td>
    </tr>
    <tr>
      <td>byte 1</td><td>长度高位（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 2</td><td>长度低位（LSB）（3）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td>
    </tr>
    <tr>
      <td>byte 3</td><td>'a'（0x61）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 4</td><td>'/'（0x2F）</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td>
    </tr>
    <tr>
      <td>byte 5</td><td>'b'（0x62）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td>
    </tr>
    <tr>
      <td colspan="10">包ID</td>
    </tr>
    <tr>
      <td>byte 6</td><td>包ID高位（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 7</td><td>包ID低位（LSB）（10）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td>
    </tr>
    <tr>
      <td colspan="10">属性集长度</td>
    </tr>
    <tr>
      <td>byte 8</td><td>无属性</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
  </tbody>
</table>

### 3.3.3 PUBLISH载荷

载荷包含着被发布的应用消息。其内容和格式是由应用程序选择的。载荷的长度可由可变头中的剩余长度字段减去可变头长度计算所得。PUBLISH 包携带 0 长度的载荷也是合法的。

### 3.3.4 PUBLISH动作

<span class="vcMarked">PUBLISH 包的接收者**必须**使用 PUBLISH 包中 QoS 对应的方式响应此包</span> <span class="vcReferred">[MQTT-3.3.4-1]</span>。

表 3-3 PUBLISH 包响应方式

| Qos等级 | 响应方式 |
| --- | --- |
| QoS 0 | 无 |
| QoS 1 | PUBACK 包 |
| QoS 2 | PUBREC 包 |

客户端使用 PUBLISH 包将应用消息发送给服务器，以便由服务器转发给相关订阅者。

服务器使用 PUBLISH 包将应用消息发给每个匹配的订阅者客户端。如果订阅时的 SUBSCRIBE 包携带有订阅ID，则 PUBLISH 包也携带此订阅ID。

当客户端使用带有通配符的主题过滤器订阅时，客户端的订阅可能会重叠，因此一次消息发布可能匹配多个过滤器。<span class="vcMarked">在这种情况下服务器**必须**使用这些重叠订阅中最高的 QoS 等级来发布此数据</span> <span class="vcReferred">[MQTT-3.3.4-2]</span>。此外，服务器可以发送此信息的多个副本，每个额外的订阅发送一个副本，且采用每个订阅建立时的 QoS 设置。

如果客户端收到一个不请自来的应用消息（并非来自其订阅的频道），其中包括了超过客户端最大 QoS 的 QoS，客户端将使用带有原因码 0x9B（不支持的 QoS）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理) 中的描述。

<span class="vcMarked">如果客户端在重叠订阅时设置了订阅ID，服务器**必须**在为该订阅发布消息时将订阅ID放入消息中</span> <span class="vcReferred">[MQTT-3.3.4-3]</span>。<span class="vcMarked">如果服务器发送该消息的单一副本，服务器**必须**将所有包含订阅ID的订阅动作的订阅ID放入 PUBLISH 包中，他们的顺序不重要</span> <span class="vcReferred">[MQTT-3.3.4-4]</span>。<span class="vcMarked">如果服务器发送该消息的多个副本，服务器**必须**在每个副本中放入对应订阅动作的订阅ID</span> <span class="vcReferred">[MQTT-3.3.4-5]</span>。

客户端可能对某个发布动作进行了多次订阅，且使用相同的订阅ID。在这种情况下，PUBLISH 包将携带多个相同的订阅ID。

PUBLISH 包因接收 SUBSCRIBE 包携带的订阅ID之外，通过其他方式携带订阅ID视为协议错误。<span class="vcMarked">从客户端发往服务器的 PUBLISH 包**必须不**携带订阅ID</span> <span class="vcReferred">[MQTT-3.3.4-6]</span>。

如果是共享订阅，则只有正在接收消息的客户端发送的 SUBSCRIBE 包中的订阅ID会在 PUBLISH 包中返回。

PUBLISH 包的接收者基于QoS等级的动作描述参考 [4.3](#4-3-QoS和协议流程)。

如果 PUBLISH 包包含主题别名，接收者按照如下流程处理：

1. 主题别名值为 0 或大于主题别名最大值视为协议错误，接收者使用带有原因码 0x94（主题别名不可用）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理)。
2. 如果接收者已经建立了对该主题别名的映射，则
  - 如果包中的主题名长度为 0，则接收者使用主题别名对应的主题名
  - 如果包中的主题名长度不为 0，则接收者使用该主题名处理此包，随后更新主题别名映射，将主题别名与主题名关联
3. 如果接收者尚未建立对该主题别名的映射，则
  - 如果包中的主题名长度为 0，则视为一个协议错误，使用带有原因码 0x82（协议错误）的 DISCONNECT 包断开连接，参考 [4.3](#4-3-QoS和协议流程)
  - 如果包中的主题名长度不为 0，则接收者使用该主题名处理此包，随后更新主题别名映射，将主题别名与主题名关联

*非规范性评论*

*如果服务器向采用其他版本的客户端（例如 MQTT V3.1.1）发送应用消息，这些客户端可能不支持属性集或者本协议中的其他特性，有些应用消息中的信息可能会丢失，依赖于这些信息的应用程序可能无法正常工作。*

<span class="vcMarked">当客户端没有接收到足够的 PUBACK、PUBCOMP 或带有大于等于 128 原因码的 PUBREC 时，客户端**必须不**发送QoS 1 或 QoS 2 的 PUBLISH 包导致其需接收的返回数量超过接收最大值</span> <span class="vcReferred">[MQTT-3.3.4-7]</span>。如果服务器接收且未使用 PUBACK 或 PUBCOMP 返回的 QoS 1 或 QoS 2 的包超过其接收最大值时，服务器使用带有原因码 0x93（超出接收最大值）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理)。参考 [4.9](#4-9-流量控制) 了解更多关于流量控制的信息。

<span class="vcMarked">客户端不能延迟任何包的发送，除了因未收到接受回复而达到接收最大值因此未能发送的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.3.4-8]</span>。接受最大值的值仅对当前网络连接有效。

*非规范性评论*

*客户端可以选择发送小于接受最大值的包让服务器处理，即使客户端实际上有更多的消息需要发送。*

*非规范性评论*

*客户端可以选择在其停发 QoS 1 和 QoS 2 的 PUBLISH 包时，同时停发 QoS 0 的 PUBLISH 包。*

*非规范性评论*

*如果客户端在接收到 CONNACK 前就发送 QoS 1 或 QoS 2 的 PUBLISH包，可能存在断开连接的风险，因为他的发送可能超过接受最大值。*

<span class="vcMarked">当服务器没有接收到足够的 PUBACK、PUBCOMP 或带有大于等于 128 原因码的 PUBREC 时，服务器**必须不**发送QoS 1 或 QoS 2 的 PUBLISH 包导致其需接收的返回数量超过接收最大值</span> <span class="vcReferred">[MQTT-3.3.4-9]</span>。如果客户端接收且未使用 PUBACK 或 PUBCOMP 返回的 QoS 1 或 QoS 2 的包超过其接收最大值时，客户端使用带有原因码 0x93（超出接收最大值）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理)。参考 [4.9](#4-9-流量控制) 了解更多关于流量控制的信息。

<span class="vcMarked">服务器不能延迟任何包的发送，除了因未收到接受回复而达到接收最大值因此未能发送的 PUBLISH 包</span> <span class="vcReferred">[MQTT-3.3.4-10]</span>。

*非规范性评论*

*服务器可以选择发送小于接受最大值的包让客户端处理，即使服务器实际上有更多的消息需要发送。*

*非规范性评论*

*服务器可以选择在其停发 QoS 1 和 QoS 2 的 PUBLISH 包时，同时停发 QoS 0 的 PUBLISH 包。*

## 3.4 PUBACK - 发布确认

PUBACK 包是 QoS 1 的 PUBLISH 包的响应。

### 3.4.1 PUBACK固定头

*图 3‑10 PUBACK 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（4）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度字段**

表示可变头的长度，采用 `变长整数` 编码。

### 3.4.2 PUBACK可变头

PUBACK 包的可变头按序包含下列字段：对应 PUBLISH 包的包ID，PUBACK 原因码，属性集长度，属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

图 3-11 PUBACK 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
    <tr><td>byte 3</td><td colspan="8">PUBACK 原因码</td></tr>
    <tr><td>byte 4</td><td colspan="8">属性集长度</td></tr>
  </tbody>
</table>

#### 3.4.2.1 PUBACK原因码

可变头中的 Byte 3 是 PUBACK 原因码。如果剩余长度的值为 2，表示没有设置原因码，采用默认值 0x00（成功）。

表 3‑4 PUBACK 原因码

| 值 | Hex | 原因码名称 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 消息已接收。继续处理 QoS 1 消息。 |
| 16 | 0x10 | 没有匹配的订阅者 | 消息已接收但没有订阅者。此内容只由服务器发送。如果服务器了解没有匹配的订阅者，服务器**可以**使用此原因码代替 0x00（成功）。 |
| 128 | 0x80 | 未指定错误 | 接收者没有接收消息，接收者不想透露原因或原因与其他原因码不匹配。 |
| 131 | 0x83 | 特定实现错误 | PUBLISH 包合法但接收者不想接收。 |
| 135 | 0x87 | 未经授权 | PUBLISH 包未经授权。 |
| 144 | 0x90 | 主题名不可用 | 主题名格式正确，但不被此客户端或服务器接受。 |
| 145 | 0x91 | 包ID已被使用 | 包ID已经被使用。这可能表示客户端与服务器之间的会话状态不匹配。 |
| 151 | 0x97 | 超限 | 超出了实现或管理员设置的限制。 |
| 153 | 0x99 | 载荷格式错误 | 载荷格式与载荷格式标识不匹配。 |

<span class="vcMarked">客户端或服务器发送的 PUBACK 包**必须**采用上述之一的 PUBACK 原因码</span> <span class="vcReferred">[MQTT-3.4.2-1]</span>。当原因码为 0x00（成功）且没有属性集时，原因码与属性集长度可以省略。此时 PUBACK 的剩余长度值为 2。

#### 3.4.2.2 PUBACK属性集

##### 3.4.2.2.1 属性集长度

表示 PUBACK 可变头中属性集长度的值，采用 `变长整数` 编码。如果剩余长度的值小于 4，表示没有属性集长度，其值视为 0。

##### 3.4.2.2.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，没有义务被接收端解析。

发送方使用此字段向接收方传递额外的信息。<span class="vcMarked">如果添加此字段会导致 PUBACK 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.4.2-2]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.4.2.2.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 PUBACK 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.4.2-3]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.4.3 PUBACK载荷

PUBACK 包没有载荷。

### 3.4.4 PUBACK动作

这部分在 [4.3.2](#4-3-2-Qos-1：至少一次) 中描述。

## 3.5 PUBREC - 发布签收（QoS 2 交付第一部分）

PUBREC 包是对 QoS 2 的 PUBLISH 包的响应。这是 QoS 2 协议交换的第二个包。

### 3.5.1 PUBREC固定头

*图 3‑12 PUBREC固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（5）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度**

表示可变头的长度，采用 `变长整数` 编码。

### 3.5.2 PUBREC可变头

PUBREC 可变头按序包括下列字段：对应 PUBLISH 包的包ID、PUBREC 原因码、属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

图 3-13 PUBREC 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
    <tr><td>byte 3</td><td colspan="8">PUBREC 原因码</td></tr>
    <tr><td>byte 4</td><td colspan="8">属性集长度</td></tr>
  </tbody>
</table>

#### 3.5.2.1 PUBREC原因码

可变头中的 Byte 3 是 PUBREC 原因码。如果剩余长度的值为 2，表示没有设置原因码，采用默认值 0x00（成功）。

表 3‑5 PUBREC 原因码

| 值 | Hex | 原因码名称 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 消息已接收。继续处理 QoS 1 消息。 |
| 16 | 0x10 | 没有匹配的订阅者 | 消息已接收但没有订阅者。此内容只由服务器发送。如果服务器了解没有匹配的订阅者，服务器**可以**使用此原因码代替 0x00（成功）。 |
| 128 | 0x80 | 未指定错误 | 接收者没有接收消息，接收者不想透露原因或原因与其他原因码不匹配。 |
| 131 | 0x83 | 特定实现错误 | PUBLISH 包合法但接收者不想接收。 |
| 135 | 0x87 | 未经授权 | PUBLISH 包未经授权。 |
| 144 | 0x90 | 主题名不可用 | 主题名格式正确，但不被此客户端或服务器接受。 |
| 145 | 0x91 | 包ID已被使用 | 包ID已经被使用。这可能表示客户端与服务器之间的会话状态不匹配。 |
| 151 | 0x97 | 超限 | 超出了实现或管理员设置的限制。 |
| 153 | 0x99 | 载荷格式错误 | 载荷格式与载荷格式标识不匹配。 |

<span class="vcMarked">客户端或服务器发送的 PUBREC 包**必须**采用上述之一的 PUBREC 原因码</span> <span class="vcReferred">[MQTT-3.5.2-1]</span>。当原因码为 0x00（成功）且没有属性集时，原因码与属性集长度可以省略。此时 PUBREC 的剩余长度值为 2。

#### 3.5.2.2 PUBREC属性集

##### 3.5.2.2.1 属性长度

属性长度是采用 `变长整数` 编码的 PUBREC 可变头中的属性集长度。如果剩余长度的值小于 4，表示没有属性长度字段，其值视为 0。

##### 3.5.2.2.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

发送方使用此字段向接收方传递额外的信息。<span class="vcMarked">如果添加此字段会导致 PUBREC 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.5.2-2]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.5.2.2.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 PUBREC 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.5.2-3]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.5.3 PUBREC载荷

PUBREC 包没有载荷。

### 3.5.4 PUBREC动作

这部分在 [4.3.3](#4-3-3-Qos-2：确保一次) 中描述。

## 3.6 PUBREL - 发布释放（QoS 2 交付第二部分）

PUBREL 包是对 PUBREC 包的响应。这是 QoS 2 协议交换的第三个包。

### 3.6.1 PUBREL固定头

*图 3‑14 PUBREL固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（6）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

<span class="vcMarked">PUBREL 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接</span> <span class="vcReferred">[MQTT-3.6.1-1]</span>。

**剩余长度**

表示可变头的长度，采用 `变长整数` 编码。

### 3.6.2 PUBREL可变头

PUBREL 可变头按序包括下列字段：对应 PUBLISH 包的包ID、PUBREL 原因码、属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。


图 3-15 PUBREL 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
    <tr><td>byte 3</td><td colspan="8">PUBREL 原因码</td></tr>
    <tr><td>byte 4</td><td colspan="8">属性集长度</td></tr>
  </tbody>
</table>

#### 3.6.2.1 PUBREL原因码

可变头中的 Byte 3 是 PUBREL 原因码。如果剩余长度的值为 2，表示没有设置原因码，采用默认值 0x00（成功）。

表 3‑6 PUBREL 原因码

| 值 | Hex | 原因码名称 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 消息已接收。继续处理 QoS 1 消息。 |
| 146 | 0x92 | 包ID未找到 | 未知的包ID。在恢复期间这不是错误，但在其他时间则表示客户端和服务器上的会话状态不匹配。 |

<span class="vcMarked">客户端或服务器发送的 PUBREL 包**必须**采用上述之一的 PUBREL 原因码</span> <span class="vcReferred">[MQTT-3.6.2-1]</span>。当原因码为 0x00（成功）且没有属性集时，原因码与属性集长度可以省略。此时 PUBREL 的剩余长度值为 2。

#### 3.6.2.2 PUBREL属性集

##### 3.6.2.2.1 属性长度

属性长度是采用 `变长整数` 编码的 PUBREL 可变头中的属性集长度。如果剩余长度的值小于 4，表示没有属性长度字段，其值视为 0。

##### 3.6.2.2.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

发送方使用此字段向接收方传递额外的信息。<span class="vcMarked">如果添加此字段会导致 PUBREL 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.6.2-2]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.6.2.2.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 PUBREL 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.6.2-3]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.6.3 PUBREL载荷

PUBREL 包没有载荷。

### 3.6.4 PUBREL动作

这部分在 [4.3.3](#4-3-3-Qos-2：确保一次) 中描述。

## 3.7 PUBCOMP - 发布完成（QoS 2 交付第三部分）

PUBCOMP 包是对 PUBREL 包的响应。这是 QoS 2 协议交换的第四个包，也是最后一个包。

### 3.7.1 PUBCOMP固定头

*图 3‑16 PUBCOMP固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（7）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度**

表示可变头的长度，采用 `变长整数` 编码。

### 3.7.2 PUBCOMP可变头

PUBREL 可变头按序包括下列字段：对应 PUBLISH 包的包ID、PUBCOMP 原因码、属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

图 3-17 PUBCOMP 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
    <tr><td>byte 3</td><td colspan="8">PUBCOMP 原因码</td></tr>
    <tr><td>byte 4</td><td colspan="8">属性集长度</td></tr>
  </tbody>
</table>

#### 3.7.2.1 PUBCOMP原因码

可变头中的 Byte 3 是 PUBCOMP 原因码。如果剩余长度的值为 2，表示没有设置原因码，采用默认值 0x00（成功）。

表 3‑3 PUBCOMP 原因码

| 值 | Hex | 原因码名称 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 消息已接收。继续处理 QoS 1 消息。 |
| 146 | 0x92 | 包ID未找到 | 未知的包ID。在恢复期间这不是错误，但在其他时间则表示客户端和服务器上的会话状态不匹配。 |

<span class="vcMarked">客户端或服务器发送的 PUBCOMP 包**必须**采用上述之一的 PUBCOMP 原因码</span> <span class="vcReferred">[MQTT-3.7.2-1]</span>。当原因码为 0x00（成功）且没有属性集时，原因码与属性集长度可以省略。此时 PUBCOMP 的剩余长度值为 2。

#### 3.7.2.2 PUBCOMP属性集

##### 3.7.2.2.1 属性长度

属性长度是采用 `变长整数` 编码的 PUBCOMP 可变头中的属性集长度。如果剩余长度的值小于 4，表示没有属性长度字段，其值视为 0。

##### 3.7.2.2.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

发送方使用此字段向接收方传递额外的信息。<span class="vcMarked">如果添加此字段会导致 PUBCOMP 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.7.2-2]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.7.2.2.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 PUBCOMP 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.7.2-3]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.7.3 PUBCOMP载荷

PUBCOMP 包没有载荷。

### 3.7.4 PUBCOMP动作

这部分在 [4.3.3](#4-3-3-Qos-2：确保一次) 中描述。

## 3.8 SUBSCRIBE - 订阅请求

SUBSCRIBE 包由客户端发送到服务器，用来创建一个或多个订阅。每个订阅将客户端注册到一个或多个其感兴趣的主题。服务器将到达该客户端订阅匹配的主题的应用消息使用 PUBLISH 包转发给客户端。SUBSCRIBE 包也基于每个订阅指定了服务器向客户端发送应用消息的最大QoS。

### 3.8.1 SUBSCRIBE固定头

*图 3‑18 SUBSCRIBE固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（8）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

<span class="vcMarked">SUBSCRIBE 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接</span> <span class="vcReferred">[MQTT-3.8.1-1]</span>。

**剩余长度**

表示可变头和载荷的长度，采用 `变长整数` 编码。

### 3.8.2 SUBSCRIBE可变头

SUBSCRIBE 可变头按序包括下列字段：包ID、属性集。[2.2.1](#2-2-1-包ID) 提供了更多关于包ID的信息。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

*非规范性示例*

*图 3-19 是一个 SUBSCRIBE 可变头的示例，其包ID为 10 且没有属性集。*

图 3-19 SUBSCRIBE 可变头示例

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">包ID</td></tr>
    <tr><td>byte 1</td><td>包ID高位（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td>包ID低位（LSB）（10）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td>byte 3</td><td>属性集长度（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
  </tbody>
</table>

#### 3.8.2.1 SUBSCRIBE属性集

##### 3.8.2.1.1 属性长度

属性长度是采用 `变长整数` 编码的 SUBSCRIBE 可变头中的属性集长度。如果剩余长度的值小于 4，表示没有属性长度字段，其值视为 0。

##### 3.8.2.1.2 订阅ID

订阅ID属性ID是**11 (0x0B) Byte**。

随后跟随 `变长整数` 表示订阅ID。订阅ID的取值范围是 1 至 268435455。订阅ID的值为0视为协议错误。订阅ID在属性集中出现超过一次视为协议错误。

订阅ID将与此 SUBSCRIBE 包创建或修改的任何订阅关联。如果有订阅ID，他将存储在订阅中，如果没有订阅ID，将不会有订阅ID存储在订阅中。

参考 [3.8.3.1](#3-8-3-1-订阅选项) 了解更多关于订阅ID处理的信息。

##### 3.8.2.1.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。

用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

*非规范性评论*

*SUBSCRIBE 中的用户属性可以被客户端用来向服务器发送一些订阅依赖的属性。这意味着这些属性并非本规范定义的。*

### 3.8.3 SUBSCRIBE载荷

SUBSCRIBE 包的载荷内含一个主题过滤器列表，指定了客户端想要订阅的主题。<span class="vcMarked">主题过滤器**必须**是一个 `UTF-8字符串`</span> <span class="vcReferred">[MQTT-3.8.3-1]</span>。每个主题过滤器之后都跟随着一个 byte 的订阅选项 。

<span class="vcMarked">载荷**必须**至少包含一个主题过滤器和订阅选项对</span> <span class="vcReferred">[MQTT-3.8.3-2]</span>。没有载荷的 SUBSCRIBE 视为协议错误。参考 [4.13](#4-13-错误处理) 了解关于错误处理的信息。

#### 3.8.3.1 订阅选项

订阅选项中的 Bit 0 和 Bit 1 表示最大QoS字段。这表示了服务器可以法相客户端的最大QoS等级。最大QoS的值为3视为协议错误。

<span class="vcMarked">订阅选项中的 Bit 2 表示非本地选项。如果其值为 1，服务器**必须不**将应用消息转发给与发布者客户端ID相同的订阅者</span> <span class="vcReferred">[MQTT-3.8.3-3]</span>。<span class="vcMarked">在共享订阅中非本地选项值为 1 视为协议错误</span> <span class="vcReferred">[MQTT-3.8.3-4]</span>。

订阅选项中的 Bit 3 表示保留消息引用发布选项。其值为 1 时，向该订阅转发的应用消息保留其原本发布时的保留消息标识。其值为 0 时，向该订阅转发的应用消息的保留标志置为 0。订阅建立时发布的保留消息的保留消息标识值为 1。

订阅选项中的 Bit 4 和 Bit 5 表示保留消息处理选项。这个选项决定了当订阅建立时保留消息是否发送。这个选项不会对连接建立后的保留消息发送有任何影响。如果该主题过滤器下没有匹配的保留消息，该选项的所有值的表现都一致。该选项的值包括：

0 = 在订阅建立后发送保留消息

1 = 只有建立全新的订阅而非重复订阅时发送保留消息

2 = 订阅建立时不发送保留消息

保留消息处理的值为 3 视为协议错误。

订阅选项中的 Bit 6 和 Bit 7 被保留以后使用。<span class="vcMarked">服务器**必须**将载荷中保留字段值非 0 的 SUBSCRIBE 包视为格式错误的包</span> <span class="vcReferred">[MQTT-3.8.3-5]</span>。

*非规范性评论*

*非本地选项和保留消息引用发布选项可以用来将客户端的消息桥接到另一台服务器。*

*非规范性评论*

*当发生重连且客户端无法确定上次连接会话中订阅是否完成的时候，不对重复订阅发送保留消息的功能是很有用的。*

*非规范性评论*

*当客户端希望获得变化提醒且不关心初始状态时，不对新的订阅发送保留消息的功能是很有用的。*

*非规范性评论*

*对于不支持保留消息的服务器，所有的保留消息引用发布选项和保留消息处理选项的值结果都是相同的，订阅后服务器不会发送任何保留消息，且后续所有消息的保留消息标识的值都为 0。*

图 3‑20 SUBSCRIBE 包载荷格式

<table>
  <thead>
    <tr><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="9">主题过滤器</td></tr>
    <tr><td>byte 1</td><td colspan="8">长度高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">长度低位（LSB）</td></tr>
    <tr><td>byte 3..N</td><td colspan="8">主题过滤器</td></tr>
    <tr><td colspan="9">订阅选项</td></tr>
    <tr><td></td><td colspan="2">保留</td><td colspan="2">保留消息处理</td><td>RAP</td><td>NL</td><td colspan="2">QoS</td></tr>
    <tr><td>byte N+1</td><td>0</td><td>0</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
  </tbody>
</table>

RAP 表示保留消息引用发布。
NL 表示非本地。

*非规范性示例*

*图 3.21 展示了 SUBSCRIBE 载荷中包含两个主题过滤器的示例。第一个是“a/b”其 QoS 值为 1，第二个是 “c/d”其 QoS 值为 2。*

图 3‑21 - 载荷字节格式非规范性示例

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">主题过滤器</td></tr>
    <tr><td>byte 1</td><td>长度高字节（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td>长度低字节（LSB）（3）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 3</td><td>'a'（0x61）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
    <tr><td>byte 4</td><td>'/'（0x2F）</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr><td>byte 5</td><td>'b'（0x62）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td colspan="10">订阅选项</td></tr>
    <tr><td>byte 6</td><td>订阅选项（1）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
    <tr><td colspan="10">主题过滤器</td></tr>
    <tr><td>byte 7</td><td>长度高字节（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 8</td><td>长度低字节（LSB）（3）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 9</td><td>'c'（0x63）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 10</td><td>'/'（0x2F）</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr><td>byte 11</td><td>'d'（0x64）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
    <tr><td colspan="10">订阅选项</td></tr>
    <tr><td>byte 12</td><td>订阅选项（2）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
  </tbody>
</table>

### 3.8.4 SUBSCRIBE动作

<span class="vcMarked">当服务器从客户端收到 SUBSCRIBE 包，服务器**必须**使用 SUBACK 响应</span> <span class="vcReferred">[MQTT-3.8.4-1]</span>。<span class="vcMarked">SUBACK 中的包ID**必须**和其对应的 SUBSCRIBE 包中的包ID一致</span> <span class="vcReferred">[MQTT-3.8.4-2]</span>。

服务器允许在发送 SUBACK 之前就转发订阅所匹配的 PUBLISH 包。

<span class="vcMarked">如果服务器接收到一个 SUBSCRIBE 包，其中包含的主题过滤器和现在会话中的一个订阅完全相同，服务器**必须**使用新订阅取代现有的订阅</span> <span class="vcReferred">[MQTT-3.8.4-3]</span>。新订阅的主题过滤器和原有订阅的完全相同，虽然其订阅选项可能不同。<span class="vcMarked">如果他的保留消息处理选项值为 0，且主题过滤器中现在有匹配的保留消息，服务器**必须**重新发送，但是服务器**必须不**能因为订阅的替换导致应用消息的丢失</span> <span class="vcReferred">[MQTT-3.8.4-4]</span>。

如果服务器接收到一个 SUBSCRIBE 包，其中包含的主题过滤器和现在会话中的订阅都不同，服务器创建一个新的非共享订阅。如果保留消息处理选项的值非 2，所有匹配的保留消息都要发往此客户端。

如果服务器接收到一个 SUBSCRIBE 包，其中包含的主题过滤器和服务器中已经存在的共享订阅相同，将该会话作为订阅者加入共享订阅。无需发送保留消息。

如果服务器接收到一个 SUBSCRIBE 包，其中包含共享订阅主题过滤器且和现有的共享订阅主题过滤器都不同，服务器创建一个新的共享订阅。该会话作为订阅者加入共享订阅。无需发送保留消息。

参考 [4.8](#4-8-订阅) 了解更多关于共享订阅的细节。

<span class="vcMarked">如果一个服务器接受的 SUBSCRIBE 包包含有多个订阅主题，服务器**必须**像接收了多个独立的 SUBSCRIBE 包一个逐个处理，唯一的不同是服务器将所有订阅请求的响应放入一个 SUBACK 包中回复</span> <span class="vcReferred">[MQTT-3.8.4-5]</span>。

<span class="vcMarked">服务器发往客户端的 SUBACK **必须**为每一个 主题过滤器/订阅选项 对提供一个原因码</span> <span class="vcReferred">[MQTT-3.8.4-6]</span>。<span class="vcMarked">这个原因码**必须**提供服务器为此次订阅分配的最大QoS或是指明本次订阅失败</span> <span class="vcReferred">[MQTT-3.8.4-7]</span>。服务器也许会提供一个比订阅者请求的更低的最大QoS。<span class="vcMarked">发送给订阅者的应用消息中的QoS**必须**是原始 PUBLISH 包中的QoS和服务器分配的最大QoS两者中的较小值</span> <span class="vcReferred">[MQTT-3.8.4-8]</span>。当原始消息的QoS值为 1 且服务器分配的最大QoS值为 0 时，服务器被允许向订阅者发布消息的多个副本。

*非规范性评论*

*如果订阅客户端对于某个特定主题被分配的最大QoS值为 1，QoS 值为 0 的应用消息通过该主题转发到客户端时QoS值为 0。这意味着客户端至多只能接收到此消息一次。另一方面，QoS 值为 2 的应用消息通过该主题转发，会被服务器降级为 QoS 1，因此客户端可能会多次收到该消息。*

*非规范性评论*

*如果订阅客户端被分配的最大QoS值为 0，随后原始 QoS 值为 2 的应用消息也可能在发往此客户端的路上丢失，但是服务器不应多次发送此消息。而同主题下 QoS 1 的消息则可能会丢失，也可能多次发给客户端。*

*非规范性评论*

*采用 QoS 2 订阅一个主题过滤器等同于宣布“我将使用该主题下所有发布消息的原始 QoS 值来接收消息”。这意味着发送者有责任决定被转发的应用消息的最大QoS等级，但是订阅者可以要求服务器将QoS降级到更适合其使用的级别。*

订阅ID是服务器中会话状态的一部分，并在接收到匹配的 PUBLISH 包时在转发时返回给客户端。订阅ID在下面三种情况下被删除或修改：当服务器接收到 UNSUBSCRIBE 包时，当服务器再次收到相同主题过滤器的 SUBSCRIBE 包，其中订阅ID不同或未设置时，当服务器发送 CONNACK，其中的会话展示值为 0 时。

订阅ID并非是客户端会话状态的一部分。在一个有用的实现中，客户端会将订阅ID关联到其他的客户端侧状态，这个状态一般会在下面三种情况下被删除或修改：客户端取消订阅时，客户端再次订阅相同主题但使用不同的订阅ID或不使用订阅ID时，客户端接收到 CONNACK，且其中会话展示值为 0 时。

服务器不需要在重传的 PUBLISH 数据包中使用相同的订阅标识符集。 客户端可以通过发送包含主题过滤器的订阅数据包来重新创建订阅，该主题过滤器与当前会话中现有订阅的主题过滤器相同。 如果客户端在首次传输 PUBLISH 数据包后重新进行订阅并使用不同的订阅标识符，则允许服务器在任何重传中使用第一次传输中的标识符。 或者，允许服务器在重传期间使用新的标识符。 服务器在发送包含新标识符的 PUBLISH 数据包后，不允许恢复为旧标识符。

服务器无需在重传 PUBLISH 时保持相同的订阅ID。客户端可以通过发送和现有会话中订阅的主题过滤器完全相同的 SUBSCRIBE 包来重新订阅。如果客户端在服务器发送某个 PUBLISH 包后重新订阅了该主题并使用了不同的订阅ID，服务器可以使用第一次发送 PUBLISH 包时使用的订阅ID来进行重传。或者，服务器也可以使用新的订阅ID进行重传。但是服务器不允许在使用新的订阅ID发送 PUBLISH 包后再使用旧的订阅ID。

*非规范性评论*

*用于说明订阅ID的使用场景*

- *客户端实现可以通过其编程接口意识到收到的某一次发布可能与其多次订阅匹配。客户端实现在每次订阅时创建一个新的订阅ID。当返回的发布消息携带多个订阅ID时，表示该消息匹配了多次订阅。*

- *客户端实现可以在订阅中让订阅者将消息指向某个回调。客户端实现创建唯一的订阅ID并将其映射到回调。当收到发布时使用其中携带的订阅ID来决定调用哪个回调。*

- *客户端实现可以在收到发布消息时返回订阅该消息的主题字符串。为了实现这一点，客户端生成一个唯一订阅ID和主题过滤器匹配。当收到应用消息时，客户都安时间使用订阅ID查找到原始的主题字符串，并返回给客户端应用程序。*

- *网关将从服务器接收到的发布转发到已订阅网关的客户端时。网关实现可以维护一个包含客户端ID到订阅ID的映射。网关为其转发到服务器的每个主题过滤器生成唯一ID。当收到发布消息时，网关查找其收到的订阅ID用以匹配客户端ID。并将客户端ID添加到发送给客户端的 PUBLISH 包中。如果上游服务器因为消息匹配多个订阅而发送多个 PUBLISH 数据包，则此行为将镜像到客户端。*

## 3.9 SUBACK - 订阅确认

SUBACK 包由服务器发往客户端，用以确认 SUBSCRIBE 包的接收和处理。

SUBACK 包包含一个原因码列表，其内容是对 SUBSCRIBE 中每个订阅请求的答复，要么是分配的最大QoS值，要么是错误返回。

### 3.9.1 SUBACK固定头

*图 3-22 SUBACK包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（9）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度**

表示可变头和载荷的长度，采用 `变长整数` 编码。

### 3.9.2 SUBACK可变头

SUBACK 可变头按序包括下列字段：对应 SUBSCRIBE 包的包ID，属性集。

#### 3.9.2.1 SUBACK属性集

##### 3.9.2.1.1 属性长度

属性长度是采用 `变长整数` 编码的 SUBACK 可变头中的属性集长度。

##### 3.9.2.1.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

服务器使用此字段向客户端传递额外的信息。<span class="vcMarked">如果添加此字段会导致 SUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.9.2-1]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.9.2.1.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 SUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.9.2-2]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

图 3‑23 SUBACK 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
  </tbody>
</table>

<span class="vcTrans">译者认为这里缺失了属性长度</span>

### 3.9.3 SUBACK载荷

载荷中包含一组原因码列表。每个原因码回复 SUBSCRIBE 包中一个对应的主题过滤器。<span class="vcMarked">SUBACK 中原因码的顺序**必须**与 SUBSCRIBE 中主题过滤器的顺序匹配</span> <span class="vcReferred">[MQTT-3.9.3-1]</span>。

表 3‑8 - 订阅原因码

| 值 | Hex | 原因码名 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | 授予 QoS 0 | 订阅已被接收，向其发送的最大 QoS 值为 0。这个值可能会小于其请求时的值。 |
| 1 | 0x01 | 授予 QoS 1 | 订阅已被接收，向其发送的最大 QoS 值为 1。这个值可能会小于其请求时的值。 |
| 2 | 0x02 | 授予 QoS 2 | 订阅已被接收，服务器接收到的所有 QoS 值都会向其转发。 |
| 128 | 0x80 | 未指定错误 | 订阅未被接收，服务器不愿透露原因或其他原因码不匹配。 |
| 131 | 0x83 | 特定实现错误 | SUBSCRIBE 合法，但服务器未接收。 |
| 135 | 0x87 | 未经授权 | 客户端未被授予创建此订阅的权力。 |
| 143 | 0x8F | 主题过滤器不可用 | 主题过滤器格式正确，但不允许此客户端使用。 |
| 145 | 0x91 | 包ID已被使用 | 所选的包ID已经在使用中。 |
| 151 | 0x97 | 超限 | 超过了实现或管理员规定的限制。 |
| 158 | 0x9E | 不支持共享订阅 | 服务器对此客户端不支持共享订阅。 |
| 161 | 0xA1 | 不支持订阅ID | 服务器不支持订阅ID；订阅未被接收。 |
| 162 | 0xA2 | 不支持通配符订阅 | 服务器不支持通配符订阅；订阅未被接收。 |

<span class="vcMarked">服务器发送的 SUBACK 包**必须**对每个收到的主题过滤器使用上表列出的原因码进行回复</span> <span class="vcReferred">[MQTT-3.9.3-2]</span>。

*非规范性评论*
 
*SUBSCRIBE 包中的每个订阅主题总是会有一个对应的原因码。如果原因码的内容不是针对某个订阅主题的（例如 0x91（包ID已被使用）），此原因码需要被设置到对每一个订阅主题的回复上。*

## 3.10 UNSUBSCRIBE - 取消订阅请求

UBSUBSCRIBE 包由客户端发往服务器，用来取消对主题的订阅。

### 3.10.1 UNSUBSCRIBE固定头

*图 3‑28 UNSUBSCRIBE固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（10）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

<span class="vcMarked">UNSUBSCRIBE 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接</span> <span class="vcReferred">[MQTT-3.10.1-1]</span>。

**剩余长度**

表示可变头（2 bytes）和载荷的长度，采用 `变长整数` 编码。

### 3.10.2 UNSUBSCRIBE可变头

UNSUBSCRIBE 可变头按序包括下列字段：包ID，属性集。[2.2.1](#2-2-1-包ID) 提供了更多关于包ID的信息。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

#### 3.10.2.1 UNSUBSCRIBE属性集

##### 3.10.2.1.1 属性长度

属性长度是采用 `变长整数` 编码的 UNSUBSCRIBE 可变头中的属性集长度。

##### 3.10.2.1.2 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。

用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

*非规范性评论*

*UNSUBSCRIBE 中的用户属性可以被客户端用来向服务器发送一些订阅依赖的属性。这意味着这些属性并非本规范定义的。*

### 3.10.3 UNSUBSCRIBE载荷

UNSUBSCRIBE 的载荷中包含着一组客户端希望取消订阅的主题过滤器列表。<span class="vcMarked">UNSUBSCRIBE 中的主题过滤器**必须**是 `UTF-8字符串`</span> <span class="vcReferred">[MQTT-3.10.3-1]</span>，其定义参考 [1.5.4](#1-5-4-UTF-8字符串)，这些字符串逐个排放。

<span class="vcMarked">UNSUBSCRIBE 包的载荷中**必须**至少包含一个主题过滤器</span> <span class="vcReferred">[MQTT-3.10.3-2]</span>。不携带载荷的 UNSUBSCRIBE 包视为协议错误。参考 [4.13](#4-13-错误处理) 了解关于错误处理的信息。

*非规范性示例*

*图 3.30 展示了 UNSUBSCRIBE 载荷中包含两个主题过滤器的示例。第一个是“a/b”，第二个是 “c/d”。*

图 3‑30 - 载荷字节格式非规范性示例

<table>
  <thead>
    <tr><td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td colspan="10">主题过滤器</td></tr>
    <tr><td>byte 1</td><td>长度高字节（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td>长度低字节（LSB）（3）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 3</td><td>'a'（0x61）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td></tr>
    <tr><td>byte 4</td><td>'/'（0x2F）</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr><td>byte 5</td><td>'b'（0x62）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
    <tr><td colspan="10">主题过滤器</td></tr>
    <tr><td>byte 7</td><td>长度高字节（MSB）（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 8</td><td>长度低字节（LSB）（3）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 9</td><td>'c'（0x63）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td><td>1</td></tr>
    <tr><td>byte 10</td><td>'/'（0x2F）</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
    <tr><td>byte 11</td><td>'d'（0x64）</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td></tr>
  </tbody>
</table>

### 3.10.4 UNSUBSCRIBE动作

<span class="vcMarked">服务器**必须**逐字符的核对 UNSUBSCRIBE 包中提供的主题过滤器（无论其是否包含通配符）是否与其持有的当前客户端的订阅相同。如果任何过滤器被精确匹配，那么其拥有的订阅**必须**被删除</span> <span class="vcReferred">[MQTT-3.10.4-1]</span>，除此之外没有额外处理。

当服务器接收到 UNSUBSCRIBE 时：

- <span class="vcMarked">服务器**必须**停止向该主题过滤器添加新的发往客户端的消息</span> <span class="vcReferred">[MQTT-3.10.4-2]</span>。
- <span class="vcMarked">服务器**必须**完成匹配该主题过滤器的，且已经开始发往客户端的 QoS 1 和 QoS 2 消息的交付</span> <span class="vcReferred">[MQTT-3.10.4-3]</span>。
- 服务器**可以**继续向客户端交付一些现有缓存中的消息。

<span class="vcMarked">服务器**必须**使用 UNSUBACK 包响应 UNSUBSCRIBE 请求</span> <span class="vcReferred">[MQTT-3.10.4-4]</span>。<span class="vcMarked">UNSUBACK 包**必须**和 UNSUBSCRIBE 包有相同的包ID。即使没有主题订阅被删除，服务器也**必须**使用 UNSUBACK 回复</span> <span class="vcReferred">[MQTT-3.10.4-5]</span>。

<span class="vcMarked">如果服务器收到的 UNSUBSCIRIBE 包包含有多个主题过滤器，服务器**必须**按序处理就如同他按序逐个收到了 UNSUBSCRIBE 包，唯一不同是服务器仅需要使用一个 UNSUBACK 回复</span> <span class="vcReferred">[MQTT-3.10.4-6]</span>。

如果主题过滤器表示一个共享订阅，此会话需要被从共享订阅中移除。如果此会话是共享订阅关联的唯一一个会话，共享订阅需要被删除。参考 [4.8.2](#4-8-2-共享订阅) 了解关于共享订阅处理的描述。

## 3.11 UNSUBACK - 取消订阅确认

UNSUBACK 包由服务器发往客户端，用于确认 UNSUBSCRIBE 包的接收和处理。

### 3.11.1 UNSUBACK固定头

*图 3-31 UNSUBACK包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（11）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>0</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

**剩余长度字段**

表示可变头和载荷的长度，采用 `变长整数` 编码。

### 3.11.2 UNSUBACK可变头

UNSUBACK 可变头按序包括下列字段：与其回复的 UNSUBSCRIBE 对应的包ID，属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

图 3-32 UNSUBACK 包可变头

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="8">包ID高位（MSB）</td></tr>
    <tr><td>byte 2</td><td colspan="8">包ID低位（LSB）</td></tr>
  </tbody>
</table>

<span class="vcTrans">译者认为这里缺失了属性长度</span>

#### 3.11.2.1 UNSUBACK属性集

##### 3.11.2.1.1 属性长度

属性长度是采用 `变长整数` 编码的 UNSUBACK 可变头中的属性集长度。
 

##### 3.11.2.1.2 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示此响应关联的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

服务器使用此字段向客户端传递额外的信息。<span class="vcMarked">如果添加此字段会导致 UNSUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.11.2-1]</span>。原因字符串在属性集中出现超过一次视为协议错误。


##### 3.11.2.1.3 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 UNSUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.11.2-2]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.11.3 UNSUBACK载荷

载荷带有一个原因码列表。每个原因码和 UNSUBSCRIBE 包中的一个主题过滤器对应。<span class="vcMarked">UNSUBACK 包中的原因码顺序**必须**和 UNSUBSCRIBE 包中的主题过滤器顺序一致</span> <span class="vcReferred">[MQTT-3.11.3-1]</span>。

无符号一字节的取消订阅原因码参见下表。<span class="vcMarked">服务器发送的 UNSUBACK 包**必须**对每个收到的主题过滤器使用下表之一的原因码</span> <span class="vcReferred">[MQTT-3.11.3-2]</span>。

表 3‑9 - 取消订阅原因码

| 值 | Hex | 原因码名 | 描述 |
| --- | --- | --- | --- |
| 0 | 0x00 | Success | 订阅已被删除。 |
| 17 | 0x11 | 没有存在的订阅 | 没有匹配到客户端使用的主题过滤器。 |
| 2 | 0x02 | 授予 QoS 2 | 订阅已被接收，服务器接收到的所有 QoS 值都会向其转发。 |
| 128 | 0x80 | 未指定错误 | 订阅未被接收，服务器不愿透露原因或其他原因码不匹配。 |
| 131 | 0x83 | 特定实现错误 | UNSUBSCRIBE 合法，但服务器未接收。 |
| 135 | 0x87 | 未经授权 | 客户端未被授予取消此订阅的权力。 |
| 143 | 0x8F | 主题过滤器不可用 | 主题过滤器格式正确，但不允许此客户端使用。 |
| 145 | 0x91 | 包ID已被使用 | 所选的包ID已经在使用中。 |

*非规范性评论*
 
*UNSUBSCRIBE 包中的每个主题过滤器总是会有一个对应的原因码。如果原因码的内容不是针对某个主题过滤器的（例如 0x91（包ID已被使用）），此原因码需要被设置到对每一个主题过滤器的回复上。*

## 3.12 PINGREQ - PING请求

PINGREQ 包由客户端发往服务器。可以用于：

- 在没有其他 MQTT 包需要被发往服务器时，使用 PINGREQ 向服务器表明客户端依然在线。
- 请求服务器的响应，用来确认服务器是否在线。
- 测试网络连接，确保网络通讯正常。

PINGREQ 包用于保活处理。参考 [3.1.2.10](#3-1-2-10-保活时间) 了解更多细节。

### 3.12.1 PINGREQ固定头

*图 3.33 – PINGREQ 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（12）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度（0）</td></tr>
    <tr><td></td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
  </tbody>
</table>

### 3.12.2 PINGREQ可变头

PINGRESP 包没有可变头。

### 3.12.3 PINGREQ载荷

PINGREQ 包没有载荷。

### 3.12.4 PINGREQ动作

<span class="vcMarked">服务器**必须**发送 PINGRESP 包用来响应 PINGREQ 包</span> <span class="vcReferred">[MQTT-3.12.4-1]</span>。

## 3.13 PINGRESP - PING响应

PINGRESP 包由服务器发往客户端，用于响应 PINGREQ 包。他表示服务器处于可用状态。

PINGRESP 包用于保活处理。参考 [3.1.2.10](#3-1-2-10-保活时间) 了解更多细节。

### 3.13.1 PINGRESP固定头

*图 3.34 – PINGRESP 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（13）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度（0）</td></tr>
    <tr><td></td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
  </tbody>
</table>

### 3.13.2 PINGRESP可变头

PINGRESP 包没有可变头。

### 3.13.3 PINGRESP载荷

PINGRESP 包没有载荷。

### 3.13.3 PINGRESP动作

客户端收到此包后无动作。

## 3.14 DISCONNECT - 断开通知

DISCONNECT 包是客户端或服务器发送的最后一个 MQTT 包。他表示了网络连接中断的原因。客户端或服务器**可以**在断开网络连接前发送 DISCONNECT 包。如果网络连接并非在客户端发送原因码 0x00（普通断开）的 DISCONNECT 后关闭，且连接持有遗嘱消息，遗嘱消息将被发布。参考 [3.1.2.5](#3-1-2-5-遗嘱标识) 了解更多细节。

<span class="vcMarked">服务器**必须不**发送 DISCONNECT 包，除非在其发送了一个原因码小于 0x80 的 CONNACK 之后</span> <span class="vcReferred">[MQTT-3.14.0-1]</span>。

### 3.14.1 DISCONNECT固定头

*图 3.35 – DISCONNECT 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（14）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

<span class="vcMarked">客户端或服务器必须确认保留字段值为 0。如果非 0，客户端或服务器发送一个带有原因码 0x81（格式错误的包）的 DISCONNECT 包，参考 [4.13](#4-13-错误处理) 中的描述</span> <span class="vcReferred">[MQTT-3.14.1-1]</span>。

**剩余长度字段**

表示可变头长度，采用 `变长整数` 编码。

### 3.14.2 DISCONNECT可变头

DISCONNECT 包可变头按序包括下列字段：断开原因码、属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

#### 3.14.2.1 断开原因码

可变头中的 Byte 1 是断开原因码。如果剩余长度的值小于 1，表示没有设置原因码，采用默认值 0x00（普通断开）。

一个 byte 的无符号断开原因码字段参考下表。

表 3‑10 断开原因码

| 值 | Hex | 原因码名称 | 发送方 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 0x00 | 普通断开 | 客户端或服务器 | 普通断开连接。无需发布遗嘱。 |
| 4 | 0x04 | 携带遗嘱的断开链接 | 客户端 | 客户端希望断开连接，但要求服务器发布遗嘱。 |
| 128 | 0x80 | 未指定错误 | 客户端或服务器 | 连接被断开，发送方不想透露原因，或没有匹配原因的原因码。 |
| 129 | 0x81 | 格式错误的包 | 客户端或服务器 | 收到的包不符合本规范。 |
| 130 | 0x82 | 协议错误 | 客户端或服务器 | 收到非预期的或顺序错误的包。 |
| 131 | 0x83 | 特定实现错误 | 客户端或服务器 | 收到的包正确，但不能被本实现处理。 |
| 135 | 0x87 | 未经授权 | 服务器 | 请求未经授权。 |
| 137 | 0x89 | 服务器忙 | 服务器 | 服务器繁忙，无法继续处理该客户端的请求。 |
| 139 | 0x8B | 服务器关闭 | 服务器 | 服务器已经关闭。 |
| 141 | 0x8D | 保活超时 | 服务器 | 因在保活时间 1.5 倍的时间内未收到包，连接已经关闭。 |
| 142 | 0x8E | 会话被接管 | 服务器 | 其他使用同样客户端ID的连接已连接，导致此连接关闭。 |
| 143 | 0x8F | 主题过滤器不可用	 | 服务器 | 主题过滤器格式正确，但不被服务器接受。 |
| 144 | 0x90 | 主题名不可用 | 客户端或服务器 | 主题名格式正确，但不被客户端或服务器接受。 |
| 147 | 0x93 | 超出接收最大值 | 客户端或服务器 | 客户端或服务器接受而未发送 PUBACK 或 PUBCOMP 的包超过了其接收最大值。 |
| 148 | 0x94 | 主题别名不可用 | 客户端或服务器 | 客户端或服务器接收的 PUBLISH 包中设置的主题别名大于其在 CONNECT 或 CONNACK 中设置的主题别名最大值。 |
| 149 | 0x95 | 包过大 | 客户端或服务器 | 包尺寸大于客户端或服务器设置的最大包尺寸。 |
| 150 | 0x96 | 消息频率过高 | 客户端或服务器 | 接收的数据频率过高。 |
| 151 | 0x97 | 超限 | 客户端或服务器 | 超出了该实现或管理员设置的限制。 |
| 152 | 0x98 | 管理员行为 | 客户端或服务器 | 连接被管理员关闭。 |
| 153 | 0x99 | 载荷格式错误 | 客户端或服务器 | 载荷格式与载荷格式标志不匹配。 |
| 154 | 0x9A | 不支持保留消息 | 服务器 | 服务器不支持保留消息。 |
| 155 | 0x9B | 不支持的 QoS | 服务器 | 客户端选择的 QoS 大于 CONNACK 中设置的最大QoS。 |
| 156 | 0x9C | 使用另一台服务器 | 服务器 | 客户端需要临时使用其他服务器。 |
| 157 | 0x9D | 服务器迁移 | 服务器 | 服务器已经迁移，客户端需要永久改变其服务器地址。 |
| 158 | 0x9E | 不支持共享订阅 | 服务器 | 服务器不支持共享订阅。 |
| 159 | 0x9F | 连接频率超限 | 服务器 | 因连接频率过高，连接被关闭。 |
| 160 | 0xA0 | 最大连接时间 | 服务器 | 此链接超过了其被授予的最大连接时间。 |
| 161 | 0xA1 | 不支持订阅ID | 服务器 | 服务器不支持订阅ID，订阅未被接受。 |
| 162 | 0xA2 | 不支持通配符订阅 | 服务器 | 服务器不支持通配符订阅，订阅未被接受。 |

<span class="vcMarked">客户端或服务器发送的 DISCONNECT 包**必须**使用上表之一的断开原因码</span> <span class="vcReferred">[MQTT-3.14.2-1]</span>。如果断开原因码的值是 0x00（普通断开）且没有属性集，原因码和属性长度可以被省略。此时 DISCONNECT 固定头中的剩余长度值为 0。

*非规范性评论*

*DISCONNECT 包用来在没有响应包的情况下表示断开连接的原因（比如 QoS 0 的发布），或是当客户端或服务器无法继续处理连接时用以断开连接。*

*非规范性评论*

*DISCONNECT 提供的信息可以被客户端用来判断是否需要重连，或是等待多久以后尝试重连。*

#### 3.14.2.2 DISCONNECT属性集

##### 3.14.2.2.1 属性长度

使用 `变长整数` 编码的 DISCONNECT 可变头中的属性集长度。如果剩余长度的值小于 2，表示属性集的长度为 0。

##### 3.14.2.2.2 会话过期间隔

会话过期间隔的属性ID是**17 (0x11) Byte**。

随后跟随 `4字节整数` 用来表示会话过期间隔，单位为秒。在属性集中出现超过一次会话过期间隔视为协议错误。

如果会话过期间隔未设置，则使用 CONNECT 包中的值。

<span class="vcMarked">服务器发送的 DISCONNECT 包中**必须不**包括会话过期间隔</span> <span class="vcReferred">[MQTT-3.14.2-2]</span>。

如果 CONNECT 包中的会话过期间隔值为 0，客户端在 DISCONNECT 包中包括一个非 0 值的会话过期间隔视为协议错误。如果这样一个非 0 值的会话过期间隔的包被服务器接收，服务器无需将他作为一个合法的 DISCONNECT 包对待。服务器使用带有原因码 0x82（协议错误）的 DISCONNECT 包断开连接，参考 [4.13](#4-13-错误处理)。

##### 3.14.2.2.3 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示断开连接的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

<span class="vcMarked">如果添加此字段会导致 DISCONNECT 的尺寸大于接收者的最大包尺寸，发送者**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.14.2-3]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.14.2.2.4 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 DISCONNECT 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.14.2-4]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

##### 3.14.2.2.5 服务引用

服务引用的属性ID是**28 (0x1C) Byte**。

随后跟随 `UTF-8字符串` 表示客户都安可以使用的其他服务器。服务引用在属性集中出现超过一次视为协议错误。

服务器发送原因码为 0x9C（使用另一台服务器）或 0x9D（服务器迁移）的 DISCONNECT 包时包括服务引用字段，参考 [4.13](#4-13-错误处理)。

参考 [4.11](#4-11-服务重定向) 服务重定向了解如何使用服务引用的信息。

图 3‑24 DISCONNECT 包可变头非规范性示例

<table>
  <thead>
    <tr>
      <td></td><td>描述</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="10">断开原因码</td>
    </tr>
    <tr>
      <td>byte 1</td><td></td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td colspan="10">属性集</td>
    </tr>
    <tr>
      <td>byte 2</td><td>属性长度（5）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 3</td><td>会话过期间隔标志（17）</td><td>0</td><td>0</td><td>0</td><td>1</td><td>0</td><td>0</td><td>0</td><td>1</td>
    </tr>
    <tr>
      <td>byte 4</td><td rowspan="4">会话过期间隔（0）</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 5</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 6</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
    <tr>
      <td>byte 7</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td>
    </tr>
  </tbody>
</table>

### 3.14.3 DISCONNECT载荷

DISCONNECT 包没有载荷。

### 3.14.4 DISCONNECT动作

<span class="vcMarked">发送 DISCONNECT 后，发送方将</span>：

- <span class="vcMarked">**必须不**在此网络连接中再发送任何 MQTT 包</span> <span class="vcReferred">[MQTT-3.14.4-1]</span>。
- <span class="vcMarked">**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-3.14.4-2]</span>。

<span class="vcMarked">当接收到带有原因码 0x00（成功） 的 DISCONNECT 包后，服务器将</span>：

- <span class="vcMarked">**必须**不发送改连接的遗嘱消息，并丢弃</span> <span class="vcReferred">[MQTT-3.14.4-3]</span>，参考 [3.1.2.5](#3-1-2-5-遗嘱标识) 中的描述。

当接收到 DISCONNECT 后，接收者将：

- **应该**关闭网络连接。

## 3.15 AUTH - 认证交换

AUTH 包由客户端发送到服务器，或有服务器发送到客户端，作为增强认证交换的一部分，类似 挑战/响应 的认证方式。当服务器或客户端的 CONNECT 包中没有包含相同的认证方式时，发送 AUTH 包视为协议错误。

### 3.15.1 AUTH固定头

*图 3.35 – AUTH 包固定头*

<table>
  <thead>
    <tr><td>Bit</td><td>7</td><td>6</td><td>5</td><td>4</td><td>3</td><td>2</td><td>1</td><td>0</td></tr>
  </thead>
  <tbody>
    <tr><td>byte 1</td><td colspan="4">MQTT包类型（15）</td><td colspan="4">保留</td></tr>
    <tr><td></td><td>1</td><td>1</td><td>1</td><td>1</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
    <tr><td>byte 2</td><td colspan="8">剩余长度</td></tr>
  </tbody>
</table>

<span class="vcMarked">AUTH 包固定头中的 Bit 3、2、1、0 的内容保留且值必须为 0。客户端或服务器**必须**将任何其他值视为格式错误的包并断开网络连接</span> <span class="vcReferred">[MQTT-3.15.1-1]</span>。

**剩余长度字段**

使用 `变长整数` 编码的可变头长度。

### 3.15.2 AUTH可变头

AUTH 包的可变头按序包括下列字段：认证原因码、属性集。属性集的编码规则和描述参考 [2.2.2](#2-2-2-属性集)。

#### 3.15.2.1 认证原因码

可变头中的 Byte 0 是认证原因码。一个 byte 的无符号断开原因码字段参考下表。<span class="vcMarked">AUTH 包的发送者**必须**使用下表之一的认证原因码</span> <span class="vcReferred">[MQTT-3.15.2-1]</span>。

表 3‑11 认证原因码

| 值 | Hex | 原因码名称 | 发送方 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 0x00 | 成功 | 服务器 | 认证成功。 |
| 24 | 0x18 | 继续认证 | 客户端或服务器 | 使用下个步骤继续认证。 |
| 25 | 0x19 | 重新认证 | 客户端 | 初始化重新认证。 |

如果认证原因码的值是 0x00（成功）且没有属性集，原因码和属性长度可以被省略。此时 AUTH 固定头中的剩余长度值为 0。

#### 3.15.2.2 AUTH属性集

##### 3.15.2.2.1 属性长度

使用 `变长整数` 编码的 AUTH 包中的属性集长度。

##### 3.15.2.2.2 认证方式

认证方式的属性ID是**21 (0x15) Byte**。

随后跟随 `UTF-8字符串` 包含认证方式字符串。认证方式的缺失或出现超过一次均视为协议错误。参考 [4.12](#4-12-增强认证) 了解更多关于增强认证的信息。

##### 3.15.2.2.3 认证数据

认证数据的属性ID是**22 (0x16) Byte**。

随后跟随 `二进制数据`，其中包括认证数据。认证数据在属性集中出现超过一次视为协议错误。认证数据的内容是由认证方式决定的。参考 [4.12](#4-12-增强认证) 了解更多关于增强认证的信息。

##### 3.15.2.2.4 原因字符串

原因字符串的属性ID是**31 (0x1F) Byte**。

随后跟随 `UTF-8字符串` 表示断开连接的原因。原因字符串是人类可读的用于诊断故障的字符串，**不应该**被接收方解析。

<span class="vcMarked">如果添加此字段会导致 AUTH 的尺寸大于接收者的最大包尺寸，发送者**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.15.2-2]</span>。原因字符串在属性集中出现超过一次视为协议错误。

##### 3.15.2.2.5 用户属性

用户属性的属性ID是**38 (0x26) Byte**。

随后跟随 `UTF-8字符串对`。这个属性可以用于提供额外的诊断信息或者其他信息。<span class="vcMarked">如果添加此字段会导致 AUTH 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段</span> <span class="vcReferred">[MQTT-3.15.2-3]</span>。用户属性可以出现多次用以发送多个键-值对。同样的键允许出现超过一次。

### 3.15.3 AUTH载荷

AUTH 包没有载荷。

### 3.15.4 AUTH动作

参考 [4.12](#4-12-增强认证) 了解更多关于增强认证的信息。

# 4 操作行为

## 4.1 会话状态

为了实现 QoS 1 和 QoS 2 的协议流程，客户端和服务器需要设置一些与客户端ID关联的状态，这被称为会话状态。服务器同时也将订阅信息作为会话状态的一部分存储。

会话状态可以跨连续的多个网络连接持续保持。会话状态的持续时间为最近的一次网络连接存在时间加上会话过期间隔。

客户端的会话状包括：

- 已经发送给服务器，但没有完成的 QoS 1 和 QoS 2 消息。
- 从服务器收到，但没有完成的 QoS 2 消息。

服务器的会话状态包括：

- 会话的存在，即便会话中其余所有内容均为空。
- 客户端订阅，包括所有订阅ID。
- 已经发送给服务器，但没有完成的 QoS 1 和 QoS 2 消息。
- 等待传输到客户端的 QoS 1 和 QoS 2 消息，**可选**的等待传输到客户端的 QoS 0 消息。
- 从客户端收到的，但没有完成的 QoS 2 消息。遗嘱消息和遗嘱延迟间隔。
- 如果会话当前未连接，存储会话结束和被丢弃的时间。

保留消息在服务器中不做为会话状态的一部分，保留消息不会在会话结束时被删除。

### 4.1.1 存储会话状态

<span class="vcMarked">客户端和服务器**必须不**在网络连接打开时丢弃会话状态</span> <span class="vcReferred">[MQTT-4.1.0-1]</span>。<span class="vcMarked">服务器**必须**在网络连接关闭且会话过期间隔到期后丢弃会话状态</span> <span class="vcReferred">[MQTT-4.1.0-2]</span>。

*非规范性评论*

*客户端与服务器实现的存储能力当然会受到容量限制，并且可能受到管理策略的限制。存储的会话状态可以被管理员行为丢弃，也可以被一些自动机制丢弃。这具有终止会话的效果。这些操作可能是由资源限制或其他操作原因引起的。硬件或软件故障可能会导致客户端或服务器存储的会话状态丢失或损坏。谨慎评估客户端和服务器的存储能力以确保他们足以承载业务。*

### 4.1.2 会话状态非规范性示例

例如，电表抄表解决方案可能使用 QoS 1 消息来保护读数免遭网络丢失。解决方案开发人员可能已经确定电源足够可靠，在这种情况下，客户端和服务器中的数据可以存储在易失性存储器中，而不会带来太大的丢失风险。

相反，停车计时器支付应用程序提供商可能会决定支付消息不应因网络或客户端故障而丢失。因此，它们要求所有数据在通过网络传输之前都写入非易失性存储器。

## 4.2 网络连接

MQTT 协议依赖于一个有序、无损、基于数据流的双向底层传输协议。本规范并不指定特定的传输层协议。

MQTT 协议需要一个底层传输来提供从客户端到服务器以及从服务器到客户端的有序、无损的字节流。 该规范不需要任何特定传输协议的支持。 客户端或服务器可以支持此处列出的任何传输协议，或满足本节要求的任何其他传输协议。客户端或服务器**可以**选择下表中的任意传输协议，或选择符合本 [章节](#4-2-网络连接) 要求的任意传输协议。

*非规范性评论*

*[RFC0793](#1.4-RFC0793) 中定义的 TCP/IP 可以被用于 MQTT 5.0。下列传输协议也可以：*

- *TLS [RFC5246](#1.4-RFC5246)*
- *WebSocket [RFC6455](#1.3-RFC6455)*

*非规范性评论*

*TCP 端口 8883 和 1883 已经向 IANA 注册为 MQTT TLS 端口和 MQTT 非 TLS 端口。*

*非规范性评论*

*无连接的网络传输如 UDP，不适用于 MQTT，因为这些协议可能造成丢包或乱序。*

## 4.3 QoS和协议流程

MQTT 协议根据本章中定义的服务质量（QoS）交付应用消息。交付协议是对称的，在下面的描述中，客户端和服务器各自可以充当发送者或接收者的角色。传输协议仅涉及将应用消息从单个发送方传交付到接收方。当服务器向多个客户端交付应用消息时，每个客户端会被分别处理。用于发往客户端的出站消息的 QoS 等级可能和入站消息的 QoS 等级不同。

### 4.3.1 QoS 0：至多一次

消息根据底层网络的能力进行交付。接收方不发送任何响应，发送方也不执行重试。消息要么到达接收者一次，要么不到达。

<span class="vcMarked">在 QoS 0 交付协议中，发送方</span>

- <span class="vcMarked">**必须**发送 QoS 0 且重复标志值为 0 的 PUBLISH 包。</span> <span class="vcReferred">[MQTT-4.3.1-1]</span>.

在 QoS 0 交付协议中，接收方

- 在收到 PUBLISH 包时获得消息的所有权

图 4.1 – QoS 0 协议流图，非规范性示例

| 发送方动作 | 数据包 | 接收方动作 |
| --- | --- | --- |
| PUBLISH QoS 0，DUP=0 |  |  |
|  | ----------> |  |
|  |  | 将消息传递给适当的接收者 |


### 4.3.2 Qos 1：至少一次

QoS 1 保证消息至少到达接收方一次。QoS 1 需要在 PUBLISH 可变头中携带一个包ID，并且这个包ID也会在回复的 PUBACK 中使用。[2.2.1](#2-2-1-包ID) 提供了更多关于包ID的信息。

<span class="vcMarked">在 QoS 1 交付协议中，发送方</span>

- <span class="vcMarked">**必须**在每次发布新消息时选择一个未被使用的包ID</span> <span class="vcReferred">[MQTT-4.3.2-1]</span>。
- <span class="vcMarked">**必须**发送包含此包ID，且重复标志值为 0 的 PUBLISH 包</span> <span class="vcReferred">[MQTT-4.3.2-2]</span>。
- <span class="vcMarked">**必须**将此 PUBLISH 包视为 “未回复的” 直到从接收方收到了正确的 PUBACK</span>。参考 [4.4](#4-4-消息传递重试) 了解关于未回复消息的讨论 <span class="vcReferred">[MQTT-4.3.2-3]</span>。

发送方接收到 PUBACK 包后，此包ID可被重用。

需要注意，发送者被允许在等待接收回复时发送更多带有不同包ID的 PUBLISH 包。

<span class="vcMarked">在 QoS 1 交付协议中，接收方</span>

- <span class="vcMarked">**必须**使用包含 PUBLISH 包中包ID的 PUBACK 包进行响应，拥有收到的消息的所有权</span> <span class="vcReferred">[MQTT-4.3.2-4]</span>。
- <span class="vcMarked">在发送 PUBACK 包后，接收方**必须**将到来的带有相同包ID的 PUBLISH 包视为新的应用消息，无论其重复标志如何设置</span> <span class="vcReferred">[MQTT-4.3.2-5]</span>。

图 4.2 – QoS 1 协议流图，非规范性示例

| 发送方动作 | 数据包 | 接收方动作 |
| --- | --- | --- |
| 存储消息 |  |  |
| 发送 PUBLISH QoS 1，DUP=0，<包ID> | ----------> |  |
|  |  | 开始转发应用消息<sup>1</sup> |
|  | <---------- | 发送 PUBACK <包ID> |
| 丢弃消息 |  |  |

<sup>1</sup>接收方无需在发送 PUBACK 前完成应用消息的转发。当原有的发送方收到 PUBACK 时，应用消息的所有权已经转移到了接收方。

### 4.3.3 Qos 2：确保一次

QoS 2 是最高级的 QoS，用于消息既不能丢失又不能重复的场合。使用 QoS 2 会带来额外的开销。

QoS 2 消息的可变头中带有包ID。章节 [2.2.1](#2-2-1-包ID) 提供了关于包ID的更多信息。QOS 2 PUBLISH 包的接收方使用两步确认过程来确认接收。

<span class="vcMarked">在 QoS 2 交付协议中，发送方</span>：

- <span class="vcMarked">**必须**在发布新消息时分配一个未使用的包ID</span> <span class="vcReferred">[MQTT-4.3.3-1]</span>。
- <span class="vcMarked">**必须**发送 QoS 2，重复标志值为 0，携带此包ID的 PUBLISH 包</span> <span class="vcReferred">[MQTT-4.3.3-2]</span>。
- <span class="vcMarked">**必须**在收到接收方发来的对应的 PUBREC 之前将此 PUBLISH 包视为 “未回复的”</span> <span class="vcReferred">[MQTT-4.3.3-3]</span>。参考 [4.4](#4-4-消息传递重试) 了解关于未回复消息的讨论。
- <span class="vcMarked">**必须**在收到接收方发来的原因码小于 0x80 的 PUBREC 后，发送 PUBREL 包。此 PUBREL 包**必须**包含和原始 PUBLISH 包相同的包ID</span> <span class="vcReferred">[MQTT-4.3.3-4]</span>。
- <span class="vcMarked">**必须**在收到接收方发来的对应 PUBCOMP 之前将此 PUBREL 包视为 “未回复的”</span> <span class="vcReferred">[MQTT-4.3.3-5]</span>。
- <span class="vcMarked">**必须不**在发送 PUBREL 之后重发 PUBLISH 包</span> <span class="vcReferred">[MQTT-4.3.3-6]</span>。
- <span class="vcMarked">**必须不**在发送 PUBLISH 包之后使此应用消息过期</span> <span class="vcReferred">[MQTT-4.3.3-7]</span>。

当发送者收到 PUBCOMP 包或原因码大于等于 0x80 的 PUBREC 包后，此包ID可被重用。

需要注意，发送者被允许在等待接收回复时发送更多带有不同包ID的 PUBLISH 包，关于流量控制的主题在 [4.9](#4-9-流量控制) 中描述。

<span class="vcMarked">在 QoS 2 交付协议中，接收方</span>：

- <span class="vcMarked">**必须**使用和收到 PUBLISH 包相同的包ID的 PUBREC 包响应，拥有收到的消息的所有权</span> <span class="vcReferred">[MQTT-4.3.3-8]</span>。
- <span class="vcMarked">如果已经使用带有 0x80 或更大值的原因码的 PUBREC 包回复，接收方**必须**将后续带有相同包ID的 PUBLISH 包视为新应用消息</span> <span class="vcReferred">[MQTT-4.3.3-9]</span>。
- <span class="vcMarked">直到收到对应的 PUBREL 包为止，接收方**必须**使用 PUBREC 回复后续任何带有相同包ID的 PUBLISH 包。在此情形下**必须不**把重复的包转发给更进一步的消息使用者</span> <span class="vcReferred">[MQTT-4.3.3-10]</span>。
- <span class="vcMarked">**必须**使用和收到 PUBREL 包相同的包ID的 PUBCOMP 包响应 PUBREL 包</span> <span class="vcReferred">[MQTT-4.3.3-11]</span>。
- <span class="vcMarked">发送 PUBCOMP 包之后，接收方**必须**将后续带有相同包ID的 PUBLISH 包视为新应用消息</span> <span class="vcReferred">[MQTT-4.3.3-12]</span>。
- <span class="vcMarked">即使消息已经过期，也**必须**继续 QoS 2 的响应动作</span> <span class="vcReferred">[MQTT-4.3.3-13]</span>。

## 4.4 消息传递重试

<span class="vcMarked">当客户端使用全新开始值为 0 重连且存在会话时，客户端和服务器都**必须**使用原始的包ID重传所有未确认的 PUBLISH 包（其 QoS > 0）和 PUBREL 包。这是客户端或服务器**需要**重传消息的唯一场景。客户端和服务器**必须不**在其他任何时间重传消息</span> <span class="vcReferred">[MQTT-4.4.0-1]</span>。

<span class="vcMarked">如果接收到的 PUBACK 或 PUBREC 包含 0x80 或更大的原因代码，则相应的 PUBLISH 数据包将被视为已确认，且**必须不**被重传</span> <span class="vcReferred">[MQTT-4.4.0-2]</span>。

图 4.3 – QoS 2 协议流图，非规范性示例

| 发送方动作 | 数据包 | 接收方动作 |
| --- | --- | --- |
| 存储消息 |  |  |
| 发送 PUBLISH QoS 2，DUP=0，<包ID> |  |  |
|  | ----------> |  |
|  |  | 存储<包ID>，之后开始转发应用消息<sup>1</sup> |
|  |  | PUBREC <包ID> <原因码> |
|  | <---------- |  |
| 丢弃消息，存储收到的  PUBREC <包ID> |  |  |
| PUBREL <包ID> |  |  |
|  | ----------> |  |
|  |  | 丢弃 <包ID> |
|  |  | 发送 PUBCOMP <包ID> |
|  | <---------- |  |
| 丢弃存储的状态 |  |  |

<sup>1</sup>接收方无需再发送 PUBREC 或 PUBCOMP 前完成消息交付。当原始的发送方收到 PUBREC 包时，应用消息的所有权转移给接收者。然而，接收者需要在接收所有权之前对所有可能导致转发失败的条件（例如限额、授权等）进行检查。接收者使用 PUBREC 中的原因码来表示接收成功或失败。

## 4.5 消息接收

<span class="vcMarked">当服务器得到输入应用消息的所有权时，他**必须**把消息放入所有匹配订阅的客户端的会话状态</span> <span class="vcReferred">[MQTT-4.5.0-1]</span>。匹配规则在 [4.7](#4-7-主题名和主题过滤器) 中定义。

在正常情况下，客户端会收到来自他已创建订阅中的消息。客户端还可能收到与他任何显式订阅不匹配的消息。这会在自动向客户端分配订阅时发生。客户端还可能在 UNSUBSCRIBE 包处理的过程中收到消息。<span class="vcMarked">无论何种情况，客户端**必须**按照匹配的 QoS 规则确认其收到包，无论客户端对包中的消息内容选择处理还是丢弃</span> <span class="vcReferred">[MQTT-4.5.0-2]</span>。

## 4.6 消息顺序

在实现第 [4.3](#4-3-QoS和协议流程) 中定义的协议流时，以下这些规则适用于客户端

- <span class="vcMarked">当客户端重传 PUBLISH 包时，其必须按照原始 PUBLISH 包的顺序发送（包括 QoS 1 和 QoS 2 消息）</span> <span class="vcReferred">[MQTT-4.6.0-1]</span>。
- <span class="vcMarked">客户端**必须**按照接收 PUBLSIH 包的顺序发送 PUBACK 包（QoS 1 消息）</span> <span class="vcReferred">[MQTT-4.6.0-2]</span>。
- <span class="vcMarked">客户端**必须**按照接收 PUBLSIH 包的顺序发送 PUBREC 包（QoS 2 消息）</span> <span class="vcReferred">[MQTT-4.6.0-3]</span>。
- <span class="vcMarked">客户端**必须**按照接收 PUBREC 包的顺序发送 PUBREL 包（QoS 2 消息）</span> <span class="vcReferred">[MQTT-4.6.0-4]</span>。

有序主题指的是客户端可以确定接收到该主题下的同一客户端发送的相同 QoS 的消息，其接收顺序和发送方的发送顺序是相同的。<span class="vcMarked">当服务器处理发布到有序主题的消息时，服务器**必须**保证其对消费者发送的 PUBLISH 包（对于相同主题和相同 QoS）的顺序和服务器从客户端接收这些包时相同</span> <span class="vcReferred">[MQTT-4.6.0-5]</span>。这是对上面列出规则的补充。

<span class="vcMarked">默认情况下，服务器在转发非共享订阅上的消息时**必须**将每个主题视为有序主题。</span> <span class="vcReferred">[MQTT-4.6.0-6]</span>。 服务器**可以**提供管理或其他机制，以允许一个或多个主题不被视为有序主题。

*非规范性评论*

*上面列出的规则确保当消息流发布到 QoS 1 的有序主题，订阅者收到的每条消息的副本最终将按照它们发布的顺序排列。如果重传，则可能先收到早已收到的重复消息。例如，发布者可能会按照 1，2，3，4 的顺序发送消息，但如果发送消息 3 后出现网络断开，订阅者可能会按照 1，2，3，2，3，4 的顺序接收消息 。*

*如果客户端和服务器都将接收最大值设置为 1，则它们会确保在任何时间 “正在发送” 的消息不超过一条。在这种情况下，即使在重新连接时，也不会在收到后发出的消息后重复收到先前的消息。例如，订户可能会按 1，2，3，3，4 的顺序接收它们，但不会按 1，2，3，2，3，4 的顺序接收它们。有关如何使用接收最大值的详细信息，请参考 [4.9](#4-9-流量控制) 流量控制。*

## 4.7 主题名和主题过滤器

### 4.7.1 主题通配符

主题级别分隔符用于结构化的主题名称。当使用主题级别分隔符时，他将主题名称分为多个 “主题级别”。

订阅用的主题过滤器可以包含特殊的通配符，这允许客户端一次订阅多个主题。

<span class="vcMarked">通配符可以在主题过滤器中使用，但**必须不**在主题名称中使用</span> <span class="vcReferred">[MQTT-4.7.0-1]</span>。

#### 4.7.1.1 主题级别分隔符

正斜杠（'/' U+002F）用于在主题树中区分各个层级，且提供一个具有层级结构的主题名称。当订阅客户端在主题过滤器中使用了通配符时，主题级别分隔符十分重要。主题级别分隔符可以出现在主题过滤器或主题名称中的任何位置。响铃到主题级别分隔符表示零长度主题级别。

#### 4.7.1.2 多级通配符

井号（'#' U+0023）是在主题中匹配任意数量层级的通配符。多级通配符可以表示父级和任意数量的子级。<span class="vcMarked">多级通配符**必须**单独使用或在主题级别分隔符后使用。在任意情况下他都**必须**是主题过滤器中的最后一个字符</span> <span class="vcReferred">[MQTT-4.7.1-1]</span>。

*非规范性评论*

*例如，当客户端订阅了 “sport/tennis/player1/#”，他将会收到下列主题中的消息：*

- *sport/tennis/player1*
- *sport/tennis/player1/ranking*
- *sport/tennis/player1/score/wimbledon*

*非规范性评论*

- *“sport/#” 可以匹配到 “sport”，因为 # 的匹配包括父级。*
- *“#” 是合法的，将会接收到所有的消息。*
- *“sport/tennis/#” 是合法的*
- *“sport/tennis#” 是非法的*
- *“sport/tennis/#/ranking” 是非法的*

#### 4.7.1.3 单级通配符

加号（'+' U+002B）实在主题中匹配单个层级的通配符。

单级通配符可以被用在主题过滤器中的任意层级，包括第一层和最后一层。<span class="vcMarked">当他被使用时，他**必须**占据过滤器中一个完整的级别</span> <span class="vcReferred">[MQTT-4.7.1-2]</span>。他可以在主题过滤器中的多个层级使用，也可以结合多级通配符共同使用。

*非规范性评论*

*例如，“sport/tennis/+” 可以匹配 “sport/tennis/player1” 和 “sport/tennis/player2”，但是不能匹配 “sport/tennis/player1/ranking”。同样，由于单级通配符只能匹配一个层级，“sport/+” 无法匹配 “sport”，但可以匹配 “sport/”。*

- *“+” 是合法的。*
- *“+/tennis/#” 是合法的。*
- *“sport+” 是非法的。*
- *“sport/+/player1” 是合法的。*
- *“/finance” 可以被 “+/+” 和 “/+” 匹配，但不能被 “+” 匹配。*

### 4.7.2 $开头的主题

<span class="vcMarked">服务器**必须不**将以通配符（# 或 +）开始的主题过滤器与以 $ 开头的主题名匹配</span> <span class="vcReferred">[MQTT-4.7.2-1]</span>。服务器**应该**防止客户端使用此类主题名称与其他客户端交换信息。服务器实现**可以**将 $ 开头的主题名称用于其他目的。

*非规范性评论*

- *$SYS/ 已被广泛采用作为包含服务器特定信息或控制 API 的主题的前缀*
- *应用程序不得将 $ 开头的主题用于私有目的*

*非规范性评论*

- *订阅 “#” 不会收到任何 $ 开头主题的消息。*
- *订阅 “+/monitor/Clients” 不会收到任何 “$SYS/monitor/Clients” 主题的消息。*
- *订阅 “$SYS/#” 会收到所有以 “$SYS/” 开头的消息。*
- *订阅 “$SYS/monitor/+” 会收到 “$SYS/monitor/Clients” 主题的消息。*
- *如果客户端想要接收所有 $SYS/ 开头的消息和所有其他非 $ 开头的消息，他需要同时订阅 “#” 和 “$SYS/#”。*

### 4.7.3 主题语义和使用

下列规则适用于主题名称和主题过滤器：

- <span class="vcMarked">所有的主题名称和主题过滤器**必须**至少包含一个字符</span> <span class="vcReferred">[MQTT-4.7.3-1]</span>
- 主题名称和主题过滤器大小写敏感
- 主题名称和主题过滤器可以包含空格
- 添加前导的 '/' 或结尾的 '/' 会创建不同的主题名称或主题过滤器
- 只有 '/' 字符的主题名称或主题过滤器是合法的
- <span class="vcMarked">主题名称和主题过滤器中必须不能包括 null 字符（Unicode U+0000）</span> [Unicode](#1.3-Unicode) <span class="vcReferred">[MQTT-4.7.3-2]</span>
- <span class="vcMarked">主题名称和主题过滤器是 `UTF-8字符串`；**必须不**超过 65535 字节</span> <span class="vcReferred">[MQTT-4.7.3-3]</span>。参考 [1.5.4](#1-5-4-UTF-8字符串)

主题名称和主题过滤器的层级数没有限制，换句话说其受到 `UTF-8字符串` 的限制。

<span class="vcMarked">当进行订阅匹配时，服务器**必须不**对主题名称或主题过滤器执行任何标准化处理，或对无法识别的字符进行任何修改或替换</span> <span class="vcReferred">[MQTT-4.7.3-4]</span>。主题过滤器中的每个非通配符级别必须与主题名称中的相应级别逐个匹配，匹配才能成功。

*非规范性评论*

*UTF-8 编码规则意味着主题过滤器和主题名称的比较可以通过比较编码的 UTF-8 字节来执行，或是通过比较解码的 Unicode 字符来执行。*

*非规范性评论*

- *“ACCOUNTS” 和 “Accounts” 是两个不同的主题名称*
- *“Accounts payable” 是合法的主题名称*
- *“/finance” 和 “finance” 是不同的主题名称*

应用消息会发送到客户端订阅的主题过滤器与该消息发送的主题名称匹配的所有客户端。主题资源**可以**有管理员在服务器中预定义，也**可以**被服务器自动创建，当服务器第一次收到关于该主题的订阅或收到发往该主题的应用消息时。服务器也**可以**使用安全组件来授权某客户端对主题资源进行特定操作。

## 4.8 订阅

MQTT 提供了两种订阅，共享订阅和非共享订阅。

*非规范性评论*

*在较早版本的 MQTT 中，所有的订阅都是非共享订阅。*

### 4.8.1 非共享订阅

非共享订阅仅与创建他的 MQTT 会话关联。每个订阅包含一个主题过滤器，决定了拿些主题的消息会被转发到此会话，还包括订阅选项。服务器负责收集匹配过滤器的消息，并在 MQTT 连接可用时将这些消息转发到此会话的 MQTT 连接。

一个会话不能对同主题名持有超过一个的非共享订阅，所以在会话中可以将主题过滤器用作区分订阅的键。

如果有多个客户端，都对相同的主题各自进行非共享订阅，每个客户端都会从主题中获得自己的应用消息副本。这意味着非共享订阅不能用于跨客户端之间的应用消息负载均衡，因为每个消息都会被发到所有的订阅客户端。

### 4.8.2 共享订阅

共享订阅可以与多个订阅 MQTT 会话关联。与非共享订阅一样，持有主题过滤器和订阅选项；然而，发布到其主题过滤器的消息仅被转发到其中之一的订阅会话。当多个消费者客户端并发进行消息处理时，共享订阅非常有用。

共享订阅是用一种特殊格式的主题过滤器实现的。该过滤器的格式是：

\$share/{ShareName}/{filter}

- $share 是小写字符串，表示此主题过滤器是一个共享订阅主题过滤器。
- {ShareName} 是不包括 '/' '+' '#' 的字符串
- {filter} 字符串的剩余部分的格式和语义与非共享订阅中的主题过滤器相同。参考 [4.7](#4-7-主题名和主题过滤器)。

<span class="vcMarked">共享订阅的主题过滤器**必须**以 $share/ 开始且**必须**包括至少一字符的共享名称</span> <span class="vcReferred">[MQTT-4.8.2-1]</span>。<span class="vcMarked">共享名称**必须不**包含字符 '/'、'+'、'#'，但**必须**在其后跟随 '/' 字符。此 '/' 字符后**必须**跟随主题过滤器</span> <span class="vcReferred">[MQTT-4.8.2-2]</span>，主题过滤器的描述参考 [4.7](#4-7-主题名和主题过滤器)。

*非规范性评论*

*共享订阅在 MQTT 服务器范围内定义，而非在会话内定义。共享名称包含在共享订阅的主题过滤器中，因此一台服务器上可以有多个具有相同 {filter} 的不同共享订阅。通常来说，应用程序使用共享名称表示共享订阅的会话组。*

*例子：*

- *共享订阅 "$share/consumer1/sport/tennis/+" 和 "$share/consumer2/sport/tennis/+" 是不同的共享订阅，他们可以被关联到不同的会话组。这两个订阅都可以匹配到与非共享订阅 "sport/tennis/+" 相同的内容。*

*如果有消息被发布到 "sport/tennis/+"，那么会有一个消息副本被发送至 "$share/consumer1/sport/tennis/+"，还会有一个消息副本被发送至 "$share/consumer2/sport/tennis/+"，另外还会有更多的消息副本被发往使用非共享订阅 "sport/tennis/+" 的客户端。*

- *共享订阅 "$share/consumer1//finance" 和非共享订阅 "/finance" 匹配相同的主题。*

*需要注意 "$share/consumer1//finance" 和 "$share/consumer1/sport/tennis/+" 是不同的共享订阅，虽然他们有相同的共享名称。虽然它们可能以某种方式相关，但它们具有相同的共享名并不意味着它们之间存在特定关系。*

共享订阅通过在 SUBSCRIBE 中使用共享订阅主题过滤器创建。当只有一个会话使用某个共享订阅时，共享订阅的行为就像非共享订阅一样，不同之处在于：

- 当与发布消息进行匹配时，不会考虑 $share 和 {ShareName} 部分的内容。
- 当订阅初次建立时不会有保留消息被发送至会话。保留消息会在其发布时像其他匹配消息一样被发送到会话。

一旦共享订阅存在，其他会话都可以使用同样的共享订阅主题过滤器加入订阅。新的会话将成为此共享订阅新关联的订阅者。保留消息不会发送给新的订阅者。之后每个匹配共享订阅的应用消息都会发给共享订阅的订阅者中的有且仅有一个的某个会话。

会话可以通过发送包含完整共享订阅主题过滤器的 UNSUBSCRIBE 包来显式的退出共享订阅。当会话终止时也会退出共享订阅。

共享订阅只要与至少一个会话关联（即已向其主题过滤器发出成功的订阅请求但尚未完成相应的取消订阅的会话），就会持续存在。当最初创建共享订阅的会话取消订阅时，共享订阅将继续存在，除非其取消时共享订阅中已经没有其他的会话。当不再有任何会话订阅共享订阅时，共享订阅就会结束，并且与其关联的任何未传递的消息都将被删除。

共享订阅注意事项

- 如果有超过一个会话加入了共享订阅，服务器实现在每一条消息上都有自由选择使用哪个会话，并有自由制定选择会话的标准。
- 不同的订阅客户端可以在其 SUBSCRIBE 中请求不同的 QoS 等级。服务器可以决定向每个客户端授权的最大 QoS 等级，而且服务器被允许向不同的订阅者授予不同的 QoS 等级。当向客户端发送应用消息时，<span class="vcMarked">服务器**必须**遵守客户端订阅时授予的 QoS 等级</span> <span class="vcReferred">[MQTT-4.8.2-3]</span>，就像服务器向订阅者发布消息一样。
- 如果服务器正在向其选择的客户端发送 QoS 2 消息，而客户端的连接在消息完成前断开了，<span class="vcMarked">服务器**必须**在客户端重新连接时完成该消息的交付</span> <span class="vcReferred">[MQTT-4.8.2-4]</span>，如同 [4.3.3](#4-3-3-Qos-2：确保一次) 中的描述。<span class="vcMarked">如果该客户端的会话在其重连成功前终止了，服务器**必须不**将此应用消息发送给其他的订阅客户端</span> <span class="vcReferred">[MQTT-4.8.2-5]</span>。
- 如果服务器正在向其选择的客户端发送 QoS 1 消息，而在收到回复前客户端的连接中止了，服务器**可以**等待客户端重连之后重传消息给客户端。如果该客户端的会话在其重连成功前终止了，服务器**应该**将此应用消息发给此共享订阅中的其他客户端。一旦失去与第一个客户端的连接，服务器就**可以**尝试将消息发送到另一个客户端。
- <span class="vcMarked">如果客户端使用带有 0x80 或更大原因码的 PUBACK 或 PUBREC 响应来自服务器的 PUBLISH 包，服务器**必须**丢弃应用消息，并且不再尝试将消息发给其他订阅者</span> <span class="vcReferred">[MQTT-4.8.2-6]</span>。
- 客户端被允许在同一个会话上已经存在共享订阅的情况下向此共享订阅发送第二个 SUBSCRIBE 请求。例如，客户端这样做也许是为了修改订阅请求的 QoS 或是由于客户端不确定上一次连接断开前是否已经完成了订阅。这个操作不会增加会话与共享订阅的关联次数，因此只需发送一个 UNSUBSCRIBE 包会话即可离开共享订阅。
- 每个共享订阅都独立于其他共享订阅。可以有两个过滤器一致的共享订阅。在这种情况下，消息会同时匹配到两个共享订阅并且由他们各自处理。如果客户端同时使用了共享订阅和非共享订阅，且消息和两个订阅都匹配，客户端会因为非共享订阅收到消息的副本。消息的第二个副本会被交付到共享订阅中的其中一个订阅者，这可能会导致此客户端收到两份消息的副本。

## 4.9 流量控制

客户端和服务器通过使用 [3.1.2.11.3](#3-1-2-11-3-接收最大值) 和 [3.2.2.3.3](#3-2-2-3-3-接收最大值) 中描述的接受最大值来控制其接收并未处理的 PUBLISH 包的数量。接受最大值创建了一个限制消息的发送配额，用来限制 QOS > 0 的 PUBLISH 包，可以是未收到 PUBACK （针对 QoS 1）或未收到 PUBCOMP（针对 QoS 2）的 PUBLISH 包。PUBACK 和 PUBCOMP 会按照下述方式补充配额。

<span class="vcMarked">客户端或服务器**必须**将其发送配额初始化为不超过接收最大值的非零值</span> <span class="vcReferred">[MQTT-4.9.0-1]</span>。

<span class="vcMarked">每当客户端或服务器发送 QoS > 0 的 PUBLISH 包，降低配额。如果发送配额值达到 0，客户端或服务器**必须不**再发送任何 QoS > 0 的 PUBLISH 包</span> <span class="vcReferred">[MQTT-4.9.0-2]</span>。他**可以**继续发送 QoS 值为 0 的 PUBLISH 包，或是**可以**选择同样暂停发送这些包。<span class="vcMarked">即使配额值为 0，客户端和服务器**必须**继续处理和响应其他类型的 MQTT 包</span> <span class="vcReferred">[MQTT-4.9.0-3]</span>。

发送配额加 1：

- 每当收到 PUBACK 包或 PUBCOMP 包，无论 PUBACK 包或 PUBCOMP 包是否携带错误码。
- 每当收到带有原因码大于等于 0x80 的 PUBREC 包。

如果发送配额已等于初始发送配额，则不会增加。尝试增加超过初始发送配额可能是由于建立新的网络连接后重新传输 PUBREL 数据包造成的。

参考 [3.3.4](#3-3-4-PUBLISH动作) 的描述了解当客户端或服务器发送的 PUBLISH 包超过被允许的接受最大值后会如果反应。

发送配额和接受最大值不会跨网络连接保留，而是如上文所述在每个新的网络连接中重新初始化。他们不是会话状态的一部分。

## 4.10 请求 / 响应

有些应用程序或是标准可能希望通过 MQTT 实现请求/响应式的交互。此版本的 MQTT 包括了四个可以用于实现此目的的属性：

- 响应主题，参考 [3.3.2.3.5](#3-3-2-3-5-响应主题)
- 关联数据，参考 [3.3.2.3.6](#3-3-2-3-6-关联数据)
- 请求响应信息，参考 [3.1.2.11.6](#3-1-2-11-6-请求响应信息)
- 响应信息，参考 [3.2.2.3.15](#3-2-2-3-15-响应信息)

随后的非规范性章节描述了如何使用这些属性。

客户端通过发送带有 [3.3.2.3.5](#3-3-2-3-5-响应主题) 中描述的响应主题的应用消息来发送请求。请求中可以包括在 [3.3.2.3.6](#3-3-2-3-6-关联数据) 中描述的关联数据。

### 4.10.1 基础请求响应（非规范性）

请求/响应交互过程如下：

1. 一个 MQTT 客户端（请求方）向主题发送请求信息。请求信息指带有响应主题的应用消息。
2. 另一个 MQTT 客户端（响应方）已经订阅了请求方发布时所用的主题，因此收到了请求消息。可能会有多个响应方订阅了此主题，也可能没有。
3. 响应方根据请求消息采取适当的操作，然后向请求消息中携带的响应主题中的主题名称发布响应消息。
4. 在通常用法中，请求者已经订阅了响应主题，从而接收响应消息。然而，其他客户端可能也订阅了响应主题，因此响应消息也会由这些客户端接收和处理。与请求消息一样，响应消息的主题可以被多个客户端订阅，也可能没有客户端订阅。

如果请求消息包含关联数据，响应方会在响应信息中复制此数据，这些数据被响应消息的接收方用来将响应消息和原始请求进行关联。响应消息不包括响应主题属性。

如果请求消息包含关联数据属性，则响应方将此属性复制到响应消息中，并且响应消息的接收方使用该属性将响应消息与原始请求关联起来。 响应消息不包括响应主题属性。

MQTT 服务器转发请求消息中的响应主题和关联数据，以及响应消息中的关联数据。服务器将请求消息和响应消息当作其他应用消息一样对待。

请求方往往在发布请求消息之前就订阅响应主题。如果当响应消息发布时响应主题没有订阅者，响应消息将不会被交付到任何客户端。

请求消息和响应消息可以使用任意等级的 QoS，且响应方可以使用一个会话过期间隔非 0 的会话。通常来说会先确认响应方在线，然后使用 QoS 0 等级发送请求消息。当然，这不是必须的。

响应方可以使用共享订阅来创建响应客户端池。但请主题，使用共享订阅时，消息在多个客户端之间的交付顺序是无法保证的。

请求者有责任确保其具有发布请求主题以及订阅其设置的响应主题的必要权限。响应者有责任确保其有订阅请求主题和发布到响应主题的权限。虽然主题授权不在本规范范围内，但建议服务器实现此类授权。

### 4.10.2 确定响应主题的值（非规范性）

请求方可以使用任何方式（包括本地配置）确定响应主题的主题名称。为了避免不同请求方之间的冲突，最好能确保请求方使用的响应主题对于该客户端来说是唯一的。由于请求方和响应方通常需要获得这些主题的授权，使用随机主题名称对于授权来说可能是个挑战。

为了帮助解决这个问题，本规范在 CONNACK 数据包中定义了一个称为响应信息的属性。服务器可以使用此属性来指导客户端选择要使用的响应主题。该机制对于客户端和服务器都是可选的。在连接时，客户端通过设置 CONNECT 数据包中的请求响应信息属性来请求服务器发送响应信息。之后服务器会在 CONNACK 数据包中发送响应信息属性（格式为 `UTF-8字符串`）。

本规范没有定义响应信息的内容，但它可用于传递主题树的全局唯一部分，该部分至少在其会话的生命周期内为该客户端保留。使用此机制允许此配置在服务器中完成一次，而不是在每个客户端中完成。

参考 [3.1.2.11.6](#3-1-2-11-6-请求响应信息) 了解关于响应信息的定义。

## 4.11 服务重定向

服务器可以通过发送带有原因码 0x9C（使用另一台服务器）或 0x9D（服务器迁移）的 CONNACK 包或 DISCONNECT 包通知客户端使用另一台服务器，参考 [4.13](#4-13-错误处理) 中的描述。当发送这类的原因码时，服务器**可以**包括服务引用属性，用来携带客户端**应该**使用的服务器地址。

原因码 0x9C（使用另一台服务器）表示客户端**应该**临时性的切换到另一台服务器。另一台服务器要么是客户端已知的，要么是写在服务引用中。

原因码 0x9D（服务器迁移）表示客户端**应该**永久性的切换到另一台服务器。另一台服务器要么是客户端已知的，要么是写在服务引用中。

服务引用是 `UTF-8字符串`。其值是空格分隔引用列表。引用的格式不在此处规范。

*非规范性评论*

*建议每个引用都包含一个名称，其后可选的包含冒号和端口号。如果名称包含冒号，则名称字符串可以括在方括号内（'\['和'\]'）。方括号括起来的名称不能包含右方括号 ('\]') 字符。这用于表示使用冒号分隔符的 IPv6 文字地址。 这是 [RFC3986](#1.4-RFC3986) 中描述的 URI 授权的简化版本。*

*非规范性评论*

*服务引用中的名称通常表示主机名、DNS 名称 [RFC1035](#1.4-RFC1035)、SRV 名称 [RFC2782](#1.4-RFC2782) 或文字 IP 地址。冒号分隔符后面的值通常是十进制的端口号。如果端口信息来自名称解析（例如使用 SRV）或者是默认的，无需携带端口号。*

*非规范性评论*

*如果提供多个服务引用，则期望客户选择其中之一。*

*非规范性评论*

*服务引用的例子：*

*myserver.xyz.org*

*myserver.xyz.org:8883*

*10.10.151.22:8883 [fe80::9610:3eff:fe1c]:1883*

## 4.12 增强认证

MQTT CONNECT 包支持使用用户名和密码字段对网络连接进行基本身份验证。虽然这些字段是为简单的密码身份验证而命名的，但它们可用于携带其他形式的身份验证，例如传递 token。

增强认证扩展了这种基础的认证方式，添加了挑战/响应式的认证。他可能涉及在 CONNECT 后， CONNACK 前，在客户端和服务器之间交换 AUTH 数据包。

为了开始增强认证，客户端需要在 CONNECT 包属性集中携带认证方式属性。他选择了需要使用的认证方式。<span class="vcMarked">如果服务器不支持客户端提供的认证方式，服务器**可以**发送带有原因码 0x8C（认证方式错误）或原因码 0x87（未经授权）的 CONNACK 包，并**必须**关闭网络连接，参考 [4.13](#4-13-错误处理) 中的描述</span> <span class="vcReferred">[MQTT-4.12.0-1]</span>。

认证方法是客户端和服务器之间就 CONNECT 数据包中的认证数据和其他字段的含义、以及完成认证所需的客户端和服务器交换和处理达成的协议。

*非规范性评论*

*通常情况下，认证方法采用 SASL 机制，使用注册名称有助于相互交流。但是，认证方法并不局限于使用注册的 SASL 机制。*

如果客户端选择的认证方法规定客户端先发送数据，则客户端应在 CONNECT 数据包中包含认证数据属性。该属性可用于根据认证方法提供数据。认证数据的内容由认证方法定义。

<span class="vcMarked">如果服务器需要额外信息来完成认证，他可以向客户端发送一个 AUTH 数据包。此数据包**必须**包含原因码 0x18（继续认证）</span> <span class="vcReferred">[MQTT-4.12.0-2]</span>。如果认证方法要求服务器向客户端发送认证数据，则会在认证数据属性中发送。

<span class="vcMarked">客户端通过发送另一个 AUTH 包来响应来自服务器的 AUTH 包。此包必须包含原因码 0x18（继续认证）</span> <span class="vcReferred">[MQTT-4.12.0-3]</span>。如果认证方法要求客户端向服务器发送认证数据，则会在认证数据属性中发送。

客户端和服务器会根据需要交换 AUTH 数据包，直到服务器通过发送原因码为 0 的 CONNACK 包接受认证。如果接受认证需要向客户端发送数据，则会在认证数据属性中发送。

客户端可以在认证过程中的任何时候关闭连接。他**可以**在此之前发送一个 DISCONNECT 数据包。<span class="vcMarked">服务器可以在认证过程的任何点拒绝认证。他**可以**根据 [4.13](#4-13-错误处理) 的描述发送一个原因码为 0x80 或以上的 CONNACK 数据包，并**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-4.12.0-4]</span>。

<span class="vcMarked">如果初始 CONNECT 包包含认证方法，则所有 AUTH 包和任何成功的 CONNACK 包都必须包含和 CONNECT 包中相同值的 认证方法</span> <span class="vcReferred">[MQTT-4.12.0-5]</span>。

增强认证的实现对于客户端和服务器都是**可选**的。<span class="vcMarked">如果客户端没有在 CONNECT 包中包含认证方法，则服务器**必须不**发送 AUTH 包，也**必须不**在 CONNACK 包中包含认证方法</span> <span class="vcReferred">[MQTT-4.12.0-6]</span>。<span class="vcMarked">如果客户端没有在 CONNECT 包中包含认证方法，则客户端**必须不**向服务器发送 AUTH 包</span> <span class="vcReferred">[MQTT-4.12.0-7]</span>。

如果客户端没有在 CONNECT 包中包含认证方法属性，服务器**应该**使用 CONNECT 数据包、TLS 会话和网络连接中的一些或所有信息进行认证。

*SCRAM挑战的非规范性示例*

- *客户端到服务器：CONNECT Authentication Method="SCRAM-SHA-1" Authentication Data=client-first-data*
- *服务器到客户端：AUTH rc=0x18 Authentication Method="SCRAM-SHA-1" Authentication Data=server-first-data*
- *客户端到服务器：AUTH rc=0x18 Authentication Method="SCRAM-SHA-1" Authentication Data=client-final-data*
- *服务器到客户端：CONNACK rc=0 Authentication Method="SCRAM-SHA-1" Authentication Data=server-final-data*
Non-normative example showing a SCRAM challenge

*Kerberos挑战的非规范性示例* 

- *客户端到服务器：CONNECT Authentication Method="GS2-KRB5*
- *服务器到客户端：AUTH rc=0x18 Authentication Method="GS2-KRB5*
- *客户端到服务器：AUTH rc=0x18 Authentication Method="GS2-KRB5" Authentication Data=initial context token*
- *服务器到客户端：AUTH rc=0x18 Authentication Method="GS2-KRB5" Authentication Data=reply context token*
- *客户端到服务器：AUTH rc=0x18 Authentication Method="GS2-KRB5*
- *服务器到客户端：CONNACK rc=0 Authentication Method="GS2-KRB5" Authentication Data=outcome of authentication*

### 4.12.1 重新认证

<span class="vcMarked">如果客户端在 CONNECT 包中提供了认证方法，则可以在收到 CONNACK 后随时启动重新认证。通过发送原因码为 0x19（重新认证）的 AUTH 包来实现。客户端**必须**将认证方法设置为与最初用于认证网络连接的认证方法相同的值</span> <span class="vcReferred">[MQTT-4.12.1-1]</span>。如果认证方法要求客户端先发送数据，则此 AUTH 数据包通过认证数据属性携带第一份数据。

服务器通过发送原因码为 0x00（成功）的 AUTH 包来响应此重新认证请求，表示重新认证已完成，或原因码为 0x18（继续认证）来表示需要更多认证数据。客户端可以通过发送原因码为 0x18（继续认证）的 AUTH 数据包来响应并提供额外的认证数据。此流程像初始认证一样继续进行，直到重新认证完成或重新认证失败。

<span class="vcMarked">如果重新认证失败，客户端或服务器**应该**带有合适原因码的 DISCONNECT 包，且**必须**断开网络连接，参考 [4.13](#4-13-错误处理) 中的描述</span> <span class="vcReferred">[MQTT-4.12.1-2]</span>。

在重新认证过程中，客户端和服务器之间的其他数据包流可以继续使用之前的认证方式。

*非规范性评论*

*服务器可能会通过拒绝重新认证来限制客户端在重新认证中可以尝试的更改范围。例如，如果服务器不允许更改用户名，它可以拒绝任何更改用户名的重新认证尝试。*

## 4.13 错误处理

### 4.13.1 格式错误的包和协议错误

格式错误的包和协议错误的定义包含在 [1.2](#1-2-术语表) 术语表中，一些，但不是全部的此类错误在整个规范中都有著名。客户端或服务器检查收到 MQTT 包的严格程度是下列各项的折中：

- 客户端或服务器的实现规模。
- 实现所支持的功能。
- 接收方信任发送方发送正确 MQTT 包的程度。
- 接收方信任网络正确传递 MQTT 包的程度。
- 继续处理错误包带来的后果。

如果发送方符合此规范，他将不会发送格式错误的包或造成协议错误。然而，如果客户端在收到 CONNACK 前发送 MQTT 包，可能会导致协议错误因为他可能对服务器的能力做了错误的假设。参考 [3.1.4](#3-1-4-CONNECT动作) CONNECT动作。

用于格式错误的包和协议错误的原因码包括：

- 0x81 格式错误的包
- 0x82 协议错误
- 0x93 超出接收最大值
- 0x95 包过大
- 0x9A 不支持保留消息
- 0x9B 不支持的 QoS
- 0x9E 不支持共享订阅
- 0xA1 不支持订阅ID
- 0xA2 不支持通配符订阅

当客户端检测到格式错误的包或协议错误，且给出了规范中的原因码后，他**应该**关闭网络连接。当错误发生在 AUTH 包中时，他**可以**发先发送包含原因码的**DISCONNECT**包，再关闭网络连接。当错误发生在任何其他种类的包时，他**应该**发送带有原因码的 DISCONNECT 包，再关闭网络连接。可以使用原因码 0x81（格式错误的包）或 0x82（协议错误）或是 [3.14.2.1](#3-14-2-1-断开原因码) 中定义的更详细的断开原因。

<span class="vcMarked">当服务器检测到格式错误的包或协议错误，且给出了规范中的原因码后，他**必须**断开网络连接</span> <span class="vcReferred">[MQTT-4.13.1-1]</span>。如果错误发生在 CONNECT 包中，服务器**可以**发送带有原因码的 CONNACK 包，再关闭网络连接。当错误发生在任何其他种类的包时，他**应该**发送带有原因码的 DISCONNECT 包再关闭网络连接。可以使用原因码 0x81（格式错误的包）或 0x82（协议错误）或是 [3.2.2.2](#3-2-2-2-连接原因码) 中定义的连接原因码或是 [3.14.2.1](#3-14-2-1-断开原因码) 中定义的更详细的断开原因码。对其他会话没有影响。

如果服务器和客户端都没有对 MQTT 包进行检查，可能导致错误无法被测出，从而可能造成对数据的伤害。

### 4.13.2 其他错误

除了格式错误的包和协议错误外，发送方无法提前预见其他错误，因为接收方可能存在一些限制条件，而这些限制条件未通知给发送方。录入，接收方的客户端或服务器可能会遇到瞬态错误，如内存不足，从到导致某个 MQTT 包处理失败。

带有 0x80 或更高原因码的确认包 PUBACK、PUBREC、PUBREL、PUBCOMP、SUBACK、UNSUBACK 表示由包ID标识的已接收包存在错误。此错误不会影响其他会话或同一会话中的其他包。

<span class="vcMarked">CONNACK 和 DISCONNECT 包允许使用原因码为 0x80 或更高来指示网络连接将被关闭。如果指定了 0x80 或更高的原因码，则无论是否发送了 CONNACK 或 DISCONNECT 包，都**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-4.13.2-1]</span>。发送这些原因码中的任何一个不会对任何其他会话产生影响。

如果 MQTT 包包含多个错误，接收方可以按任意顺序验证包，并对发现的任何错误采取适当的措施。

参考 [5.4.9](#5-4-9-处理禁止的Unicode码段) 了解关于处理禁止的 Unicode 码段的信息。

# 5 安全性（非规范性）

## 5.1 介绍

MQTT 是一种消息传输的传输协议规范，允许其实现选择网络、隐私、身份验证和授权技术。由于所选的具体安全技术将根据具体情况而定，因此实现者有责任在其设计中包含适当的功能。

MQTT 实现很可能需要紧跟不断变化的安全形势。

本章提供了一些通用的实现指导，为了不限制可做的选择，本章是非规范性的。但这不影响本章的重要性。

强烈建议提供了 TLS [RFC5246](#1.4-RFC5246) 实现的服务器应使用 TCP 端口 8883（IANA 服务名：secure-mqtt）。

存在多种解决方案提供商需要考虑的威胁。例如：

- 设备可能被入侵
- 静态数据可能被访问
- 协议行为可能存在副作用（例如 “定时攻击”）
- 拒绝服务（DoS）攻击
- 通信可能会被拦截、篡改、重定向或泄露
- 注入伪造的 MQTT 包

MQTT 解决方案通常部署在具有潜在威胁的通信环境中。在这种情况下，实施方案通常需要提供以下机制：

- 用户和设备的身份验证
- 访问服务器资源的授权
- MQTT包和应用程序数据的完整性
- MQTT包和应用程序数据的隐私
 
除了技术安全问题之外，还可能存在地理（例如，美国-欧盟隐私盾框架 [USEUPRIVSH](#1.4-USEUPRIVSH)）、行业特定（例如，支付卡行业数据安全标准 [PCIDSS](#1.4-PCIDSS)）和监管方面的考虑（例如，萨班斯-奥克斯利法案 [SARBANES](#1.4-SARBANES)）。

## 5.2 MQTT解决方案：安全和认证

实现 MQTT 解决方案时，可能需要符合特定的行业安全标准，例如美国国家标准与技术研究院网络安全框架 (NIST Cyber Security Framework) [NISTCSF](#1.4-NISTCSF)、支付卡行业数据安全标准 (PCI-DSS) [PCIDSS](#1.4-PCIDSS)、联邦信息处理标准 140-2 (FIPS-140-2) [FIPS1402](#1.4-FIPS1402) 和美国国家安全局套件 B (NSA Suite B) [NSAB](#1.4-NSAB)。

关于在 NISTCSF 中使用 MQTT 的指南，可以在 MQTT 补充出版物《MQTT 和 NIST 关键基础设施网络安全改进框架》[MQTTNIST](#1.4-MQTTV311) 中找到。使用经过行业验证、独立验证和认证的技术将有助于满足合规性要求。

## 5.3 轻量级密码学和受限设备

高级加密标准 [AES](#1.4-AES) 是目前最广泛采用的加密算法。许多处理器都支持硬件加速 AES，但嵌入式处理器通常不支持。[CHACHA20](#1.4-CHACHA20) 加密算法在软件中加密和解密的速度要快得多，但没有 AES 那么广泛使用。

[ISO29192](#1.4-ISO29192) 针对性能受限的 "低端" 设备，推荐了一些专门调整过的密码原语。

## 5.4 实施说明

MQTT 实施和使用时需要考虑多个安全方面。以下部分并不应该被视为 “检查清单”。

实现可能希望实现以下部分或全部内容：

### 5.4.1 服务器对客户端进行身份验证

CONNECT 包包含用户名和密码字段。实现可以选择如何利用这些字段的内容。实现可以提供自己的认证机制，使用类似 LDAP [RFC4511](#1.4-RFC4511) 或 OAuth [RFC6749](#1.4-RFC6749) token 之类的外部认证系统，或借用操作系统的认证机制。

MQTT v5.0 提供了增强认证机制，参考 [4.12](#4-12-增强认证) 中的描述。使用此机制需要客户端和服务器同时支持。

以明文传递认证数据，混淆此类数据元素或是不需要身份验证数据的实现应该意识到这可能会引起中间人攻击和数据重放攻击。[5.4.5](#5-4-5-应用消息和MQTT包的隐私) 介绍了确保数据隐私的方法。

客户端和服务器之间的虚拟专用网络 (VPN) 可以确保数据仅从授权客户端接收。

当使用 TLS [RFC5246](#1.4-RFC5246) 时，服务器可以使用客户端发送的 TLS 证书对客户端进行认证。

实现可能允许使用客户端发送到服务器的应用消息进行身份认证。

### 5.4.2 服务器对客户端进行授权

如果客户端已成功通过身份验证，服务器实现应在接受其连接之前检查其是否已获得授权。

授权可能基于客户端提供的信息，例如用户名、客户端的主机名/IP 地址或身份验证机制的结果。

特别是，实现应检查客户端是否有权使用客户端ID，因为这可以访问 MQTT 会话状态（[4.1](#4-1-会话状态) 中描述）。此授权检查是为了防止一个客户端意外或恶意地使用已被其他客户端使用的客户端ID的情况。

实现应该提供在 CONNECT 之后发生的访问控制，以限制客户端发布到特定主题或使用特定主题过滤器订阅的能力。实现应考虑限制对具有广泛范围的主题过滤器的访问，例如 # 主题过滤器。

### 5.4.3 客户端对服务器进行身份验证

MQTT 协议不是信任对称的。在使用基本身份验证的情况下，没有客户端对服务器进行身份验证的机制。某些增强认证确实允许进行相互身份验证。

在使用 TLS [RFC5246](#1.4-RFC5246) 的情况下，客户端可以使用服务器发送的 TLS 证书来对服务器进行身份验证。

从单个 IP 地址为多个主机名提供 MQTT 服务的实现应注意 [RFC6066](#1.4-RFC6066) 第 3 节中定义的 TLS 服务器名称指示扩展 (Server Name Indication，SNI)。 这允许客户端告诉服务器它试图连接的服务器的主机名。

一些 MQTT 实现允许通过服务器发送给客户端的应用消息进行身份验证。MQTT v5.0 引入了增强身份验证机制（详细见 [4.12](#4-12-增强认证)），该机制可以用于服务器对客户端进行身份验证。但前提是客户端和服务器都支持此机制。

客户端与服务器之间使用 VPN 可以增強客户端连接到预期的服务器的可信度。

### 5.4.4 应用消息和MQTT包的完整性

应用程序可以独立地在其应用消息中包含哈希值。这可以在网络传输过程中和静止状态下提供发布数据包内容的完整性。

TLS [RFC5246](#1.4-RFC5246) 提供了哈希算法来验证通过网络发送的数据的完整性。

使用 VPN 连接客户端和服务器可以提供 VPN 覆盖的网络部分的数据完整性。

### 5.4.5 应用消息和MQTT包的隐私

TLS [RFC5246](#1.4-RFC5246) 可以对通过网络发送的数据进行加密。一些有效的 TLS 密码套件包含不加密数据的 NULL 加密算法。为确保隐私，客户端和服务器应避免使用这些密码套件。

应用程序可以独立加密其应用消息的内容。这可以为应用消息在网络传输过程中和静止状态下提供隐私保护。但这并不能为应用消息的其他属性（例如主题名称）提供隐私保护。

客户端和服务器实现可以为静止数据（例如作为会话的一部分存储的应用程序消息）提供加密存储。

使用 VPN 连接客户端和服务器可以提供 VPN 覆盖的网络部分的数据隐私。

### 5.4.6 消息传输的不可否认性

应用程序设计者可能需要考虑适当的策略来实现端到端的不可否认性。

### 5.4.7 检测客户端和服务器是否被入侵

使用 TLS [RFC5246](#1.4-RFC5246) 的客户端和服务器实现应提供功能，以确保在建立 TLS 连接时提供的任何 TLS 证书与连接的客户端或被连接的服务器的主机名相关联。

使用 TLS 的客户端和服务器实现可以选择提供检查证书吊销列表 (CRL [RFC5280](#1.4-RFC5280)) 和在线证书状态协议 (OSCP [RFC6960](#1.4-RFC6960)) 的功能，以防止使用已吊销的证书。

物理部署可能将防篡改硬件与应用消息中特定数据的传输相结合。例如，仪表可能嵌入 GPS 以确保它不会在未经授权的位置使用。[IEEE8021AR](#1.4-IEEE 802.1AR) 是使用加密绑定标识符实现设备身份验证机制的标准。

### 5.4.8 检测异常行为

服务器实现可以监控客户端行为以检测潜在的安全事件。例如：

- 重复连接尝试
- 重复身份验证尝试
- 异常终止连接
- 主题扫描（尝试发送或订阅许多主题）
- 发送无法投递的消息（没有订阅者订阅该主题）
- 连接但不发送数据的客户端

服务器实现可能会关闭违反其安全规则的客户端的网络连接。

服务器实现检测到可疑行为可能会基于诸如 IP 地址或客户端标识符之类的标识符实施动态阻止列表。

部署可以使用网络级控制（如果可用）基于 IP 地址或其他信息实施速率限制或阻止。

### 5.4.9 处理禁止的Unicode码段

[1.5.4](#1-5-4-UTF-8字符串) 描述了禁止的 Unicode 码段，这些码段不应包含在 UTF-8 编码的字符串中。客户端或服务器实现可以选择是否验证这些码段未在 `UTF-8字符串`（例如主题名称或属性）中使用。

如果服务器不验证 `UTF-8字符串` 中的码段，但订阅的客户端会验证，则第二个客户端可能能够通过发布包含禁止的 Unicode 码段的主题名称或使用属性来导致订阅客户端关闭网络连接。本节建议采取一些步骤来防止此问题。

当客户端验证载荷是否与载荷格式标志匹配而服务器不验证时，可能会发生类似的问题。对此的考虑和补救措施类似于处理禁止的 Unicode 码段的措施。

#### 5.4.9.1 关于使用禁止的Unicode码段的考虑

通常，实现会选择验证 `UTF-8字符串`，检查是否未使用禁止的Unicode码段。这样可以避免实现面对以下难题，例如需要使用对这些码段铭感的库，或是避免了应用程序需要处理这些码段。

验证是否未使用这些码段可以消除一些安全风险。一些可能的安全漏洞是利用日志文件中的控制字符来掩盖日志中的条目或混淆处理日志文件的工具。Unicode Noncharacters 通常用作特殊标记，允许它们进入 `UTF-8字符串`可能会导致此类漏洞利用。

#### 5.4.9.2 发布者和订阅者之间的交互

发布应用程序消息的发布者通常期望服务器将消息转发给订阅者，并且这些订阅者能够处理消息。

以下是一些发布客户端可能导致订阅客户端关闭网络连接的条件：

- 发布客户端使用包含禁止的Unicode码段的主题名称发布应用程序消息。
- 发布客户端库允许在主题名称中使用禁止的Unicode码段，而不是拒绝他。
- 发布客户端被授权发送发布。
- 订阅客户端被授权使用匹配主题名称的主题过滤器。请注意，禁止的Unicode码段可能出现在主题名称的一部分，该部分与主题过滤器中的通配符字符匹配。
- 服务器将消息转发给匹配的订阅者，而不是断开发布者的连接。
- 在这种情况下，订阅客户端可能：
  - 关闭网络连接，因为它不允许使用禁止的Unicode码段，可能在这样做之前发送 DISCONNECT 消息。对于 QoS 1 和 QoS 2 消息，这可能导致服务器再次发送消息，导致客户端再次关闭网络连接。
  - 通过在 PUBACK (QoS 1) 或 PUBREC (QoS 2) 中发送大于或等于 0x80 的原因码来拒绝应用程序消息。
  - 接受应用程序消息，但无法处理它，因为它包含禁止的Unicode码段。
  - 成功处理应用程序消息。

客户端关闭网络连接的可能性可能直到发布者使用一个禁止的Unicode码段点才会被注意到。

#### 5.4.9.3 补救措施

如果存在将禁止的Unicode码段包含在主题名称或传递给客户端的其他属性中的可能性，解决方案所有者可以采用以下建议之一：

1. 将服务器实现更改为拒绝禁止的Unicode码段的 `UTF-8字符串` 的实现，服务器可以通过发送大于或等于 0x80 的原因代码或关闭网络连接来拒绝这些消息。
2. 将订阅者使用的客户端库更改为可以容忍禁止的Unicode码段的库。客户端可以处理或丢弃包含禁止的Unicode码段的 `UTF-8字符串` 的消息，只要它继续遵循协议即可。

### 5.4.10 其他安全注意事项

证书安全:

如果客户端或服务器 TLS 证书丢失或被认为可能泄露，则应将其吊销（使用 CRL [RFC5280](#1.4-RFC5280) 和/或 OSCP [RFC6960](#1.4-RFC6960)）。

丢失或被认为泄露的客户端或服务器身份验证凭证（例如用户名和密码）应予以撤销和/或重新颁发。

长连接安全:

- 使用 TLS [RFC5246](#1.4-RFC5246) 的客户端和服务器实现应允许会话重新协商以建立新的加密参数（替换会话密钥、更改密码套件、更改身份验证凭证）。
- 服务器可能会关闭客户端的网络连接，并要求他们使用新凭证重新验证身份。
- 服务器可能要求其客户端使用 [4.12.1](#4-12-1-重新认证) 节中描述的机制定期重新验证身份。

受限设备和受限网络上的客户端可以使用 TLS [RFC5246](#1.4-RFC5246) 会话恢复，以降低重新连接 TLS [RFC5246](#1.4-RFC5246) 会话的成本。

连接到服务器的客户端与连接到同一服务器并具有在相同主题上发布数据的权限的其他客户端具有传递信任关系。

### 5.4.11 使用SOCKS代理

客户端实现应该注意，某些环境需要使用 SOCKSv5 [RFC1928](#1.4-RFC1928) 代理进行外部网络连接。一些 MQTT 实现可以通过使用 SOCKS，利用替代的安全隧道（例如 SSH）进行连接。如果实现选择使用 SOCKS，他们应该支持匿名和用户名/密码认证的 SOCKS 代理。后一种情况下，实现应该注意 SOCKS 认证可能以明文进行，因此应避免使用与连接 MQTT 服务器相同的凭证。

### 5.4.12 安全配置

实现者和解决方案设计人员可以将安全性视为一组可应用于 MQTT 协议的配置。下面展示了分层安全体系结构的一个示例。

#### 5.4.12.1 透明通信配置

这种配置没有额外的安全机制，MQTT 协议直接运行在开放网络上。

#### 5.4.12.2 安全网络通信配置

这种配置使用具有安全控制措施的物理或虚拟网络，例如 VPN 或物理安全网络。

#### 5.4.12.3 安全传输配置

当使用安全传输配置时，MQTT 协议运行在一个物理网络或是虚拟网络中，使用 TLS [RFC5246](#1.4-RFC5246) 加密 MQTT 协议传输，提供身份验证、完整性保护和隐私保护。

TLS [RFC5246](#1.4-RFC5246) 客户端身份验证可以作为用户名和密码字段提供的 MQTT 客户端身份验证的补充或替代使用。

#### 5.4.12.4 行业特定的安全配置

预计 MQTT 协议将被设计到行业特定的应用配置中，每个配置都定义了一个威胁模型和用于解决这些威胁的具体安全机制。特定安全机制的建议通常会参考现有工作，包括：

[NISTCSF](#1.4-NISTCSF) NIST 网络安全框架
[NIST7628](#1.4-NIST7628) NISTIR 7628 智能电网网络安全指南
[FIPS1402](#1.4-FIPS1402) 安全模块的安全要求 (FIPS PUB 140-2)
[PCIDSS](#1.4-PCIDSS) PCI-DSS 支付卡行业数据安全标准
[NSAB](#1.4-NSAB) 美国国家安全局 Suite B 加密

# 6 使用WebSocket作为传输层

如果 MQTT 通过 WebSocket [RFC6455](#1.3-RFC6455) 连接进行传输，则适用以下条件：

- <span class="vcMarked">MQTT 包**必须**在 WebSocket 二进制数据帧中发送。 如果收到任何其他类型的数据帧，接收方**必须**关闭网络连接</span> <span class="vcReferred">[MQTT-6.0.0-1]</span>。
- <span class="vcMarked">单个 WebSocket 数据帧可以包含多个或部分 MQTT 包。 接收方不得假定 MQTT 包与 WebSocket 帧边界对齐</span> <span class="vcReferred">[MQTT-6.0.0-2]</span>。
- <span class="vcMarked">客户端**必须**在其提供的 WebSocket 子协议列表中包含“mqtt”</span> <span class="vcReferred">[MQTT-6.0.0-3]</span>。
- <span class="vcMarked">服务器选择并返回的 WebSocket 子协议名称**必须**为“mqtt”</span> <span class="vcReferred">[MQTT-6.0.0-4]</span>。
- 用于连接客户端和服务器的 WebSocket URI 对 MQTT 协议没有影响。

## 6.1  IANA注意事项

本规范要求 IANA 修改 “WebSocket 子协议名称” 注册表下 WebSocket MQTT 子协议的注册，并使用以下数据：

图 6.6‑1 - IANA WebSocket Identifier

<table>
  <tbody>
    <tr><td>Subprotocol Identifier</td><td>mqtt</td><tr>
    <tr><td>Subprotocol Common Name</td><td>mqtt</td><tr>
    <tr><td>Subprotocol Definition</td><td>http://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html</td><tr>
  </tbody>
<table>

# 7 一致性

MQTT 规范定义了 MQTT 客户端实现和 MQTT 服务器实现的一致性。 MQTT 实现既可以作为 MQTT 客户端，也可以作为 MQTT 服务器。

## 7.1 一致性条款

### 7.1.1 MQTT服务器一致性条款

服务器的定义请参考术语表中的 [服务器](#1.2-server)。

一个 MQTT 服务器仅在满足以下所有陈述时才符合本规范：

1. 服务器发送的所有 MQTT 包的格式必须与 [第 2 章](#2-MQTT包格式) 和 [第 3 章](#3-MQTT包) 描述的格式相匹配。
2. 它遵循第 [4.7 节](#4-7-主题名和主题过滤器) 描述的主题匹配规则和第 [4.8 节](#4-8-订阅) 描述的订阅规则。
3. 它满足以下章节中已标识的**必须**级别要求，但仅适用于客户端的除外：
  - [第一章 - 简介](#1-介绍)
  - [第二章 - MQTT包格式](#2-MQTT包格式)
  - [第三章 - MQTT包](#3-MQTT包)
  - [第四章 - 操作行为](#4-操作行为)
  - [第六章 - 使用WebSocket作为传输层](#6-使用WebSocket作为传输层)
- 不需要使用规范之外定义的任何扩展即可与任何其他符合标准的实现进行互操作。

### 7.1.2 MQTT客户端一致性条款

客户端的定义请参考术语表中的 [客户端](#1.2-client)。

MQTT 客户端仅在满足以下所有陈述时才符合本规范：

1. 客户端发送的所有 MQTT 包的格式必须与[第 2 章](#2-MQTT包格式) 和 [第 3 章](#3-MQTT包)描述的格式相匹配。
2. 客户端必须满足以下章节中已标识的**必须**级别要求，但仅适用于服务器的除外：
  - [第一章 - 简介](#1-介绍)
  - [第二章 - MQTT包格式](#2-MQTT包格式)
  - [第三章 - MQTT包](#3-MQTT包)
  - [第四章 - 操作行为](#4-操作行为)
  - [第六章 - 使用WebSocket作为传输层](#6-使用WebSocket作为传输层)
3. 不需要使用规范之外定义的任何扩展即可与任何其他符合标准的实现进行互操作。

# 附录 A. 致谢

MQTT 技术委员会 (TC) 特别感谢 MQTT 协议的最初发明者 Andy Stanford-Clark 博士和 Arlen Nipper，以及他们对标准化过程的持续支持。

技术委员会感谢 Brian Raymor (前微软员工)，他在 5.0 版本标准的大部分开发过程中担任 MQTT 技术委员会的联合主席。

以下个人是 OASIS 技术委员会在创建本标准期间的成员，他们的贡献得到了热烈的认可：

参与者：
- Senthil Nathan Balasubramaniam (Infiswift)
- Dr. Andrew Banks, 编辑 (IBM)
- Ken Borgendale, 编辑 (IBM)
- Ed Briggs, 编辑 (微软)
- Raphael Cohn (个人)
- Richard Coppen, 主席 (IBM)
- William Cox (个人)
- Ian Craggs , 秘书 (IBM)
- Konstantin Dotchkoff (微软)
- Derek Fu (IBM)
- Rahul Gupta, 编辑 (IBM)
- Stefan Hagen (个人)
- David Horton (Solace Systems)
- Alex Kritikos (Software AG, Inc.)
- Jonathan Levell (IBM)
- Shawn McAllister (Solace Systems)
- William McLane (TIBCO Software Inc.)
- Peter Niblett (IBM)
- Dominik Obermaier (dc-square GmbH)
- Nicholas O'Leary (IBM)
- Brian Raymor (微软)
- Andrew Schofield (IBM)
- Tobias Sommer (Cumulocity)
- Joe Speed (IBM)
- Dr Andy Stanford-Clark (IBM)
- Allan Stockdill-Mander (IBM)
- Stehan Vaillant (Cumulocity)
 
有关对 MQTT 早期版本做出贡献的人员列表，请参考 MQTT v3.1.1 规范 [MQTTV311](#1.4-MQTTV311) 的附录 A。

# 附录 B. 强制性规范性声明（非规范性）

本附录是非规范性的，是作为本文档主体中编号的一致性声明的方便摘要而提供的。有关一致性要求的明确列表，请参阅[第 7 章](#7-一致性)。

| 规范性声明编号 | 规范性声明 |
| --- | --- |
| [MQTT-1.5.4-1] | 在 UTF-8 编码字符串中的字符**必须**为 [Unicode] 和 [RFC3629] 中所定义的，格式正确的字符编码。**必须不**使用U+D800 至 U+DFFF之间的编码 |
| [MQTT-1.5.4-2] | UTF-8 编码字符串**必须**不包含空字符 U+0000 |
| [MQTT-1.5.4-3] | 无论 UTF-8 编码序列 0xEF 0xBB 0xBF 出现在字符串的何处，他永远被解释为 U+FEFF (0宽无换行空格) 而且**必须**不能被数据包的接收者跳过或剥离 |
| [MQTT-1.5.5-1] | 变长整数编码时**必须**使用能够表示数字值的最小长度来进行编码 |
| [MQTT-1.5.7-1] | UTF-8字符串对中的两个字符串都**必须**遵守 UTF-8 字符串的需求 |
| [MQTT-2.1.3-1] | 当一个比特位被标记为 “保留” 时，他的意义被保留到未来使用而他的值**必须**按照下表设置 |
| [MQTT-2.2.1-2] | 当 PUBLISH 包的 QoS 值为 0 时，**必须不**包含 包ID 字段 |
| [MQTT-2.2.1-3] | 每当客户端发送新的 SUBSCRIBE 包，UNSUBSCRIBE 包 或 QoS > 0 的 PUBLISH 包，**必须**携带一个非零且当前未被使用的包ID |
| [MQTT-2.2.1-4] | 每当服务器发送新的 QoS > 0 的 PUBLISH 包，**必须**携带一个非零且当前未被使用的包ID |
| [MQTT-2.2.1-5] | PUBACK，PUBREC，PUBREL 或 PUBCOMP 包**必须**携带和 PUBLISH 相同的包ID |
| [MQTT-2.2.1-6] | SUBACK 和 UNSUBACK **必须**携带和其对应的 SUBSCRIBE 和 UNSUBSCRIBE 包相同的包ID |
| [MQTT-2.2.2-1] | 如果没有属性，**必须**通过一个 0 值的属性长度来明确表示 |
| [MQTT-3.1.0-1] | 当客户端和服务器的网络连接建立后，客户端向服务器发送的第一个数据包**必须**是 CONNECT 包 |
| [MQTT-3.1.0-2] | 服务器**必须**将客户端发送的第二个 CONNECT 包视为协议错误并关闭网络连接 |
| [MQTT-3.1.2-1] | 协议名称**必须**是 `UTF-8字符串`表示的 “MQTT”。如果服务器不想接收此连接，同时又想告知客户端服务器是一个 MQTT 服务器，**可以**发送一个带有 0x84（协议版本不支持）原因码的 CONNACK，随后服务器**必须**关闭网络连接 |
| [MQTT-3.1.2-2] | 如果客户端使用的协议版本不为 5 而且服务器不想接受此 CONNECT 包，服务器**可以**发送一个带有 0x84（协议版本不支持）原因码的 CONNACK，随后服务器**必须**关闭网络连接 |
| [MQTT-3.1.2-3] | 服务器**必须**验证 CONNECT 包中的保留位的值是 0 |
| [MQTT-3.1.2-4] | 如果接收到全新开始值置为 1 的 CONNECT 包，客户端和服务器**必须**丢弃任何已经存在的会话并开始一个新的会话 |
| [MQTT-3.1.2-5] | 如果服务器接收到的 CONNECT 包中的全新开始被置为 0 并且服务器中已经存在和客户端ID关联的会话，服务器**必须**基于已经存在的会话状态恢复客户端的连接 |
| [MQTT-3.1.2-6] | 如果服务器接收到的 CONNECT 包中的全新开始被置为 0 并且服务器中没有和客户端ID关联的会话，服务器**必须**创建一个新的会话 |
| [MQTT-3.1.2-7] | 如果遗嘱标识被置为 1，则表示遗嘱消息**必须**被存储在服务器中，并且关联到此会话 |
| [MQTT-3.1.2-8] | 遗嘱消息**必须**在网络连接断开后的遗嘱延迟间隔时间过期后或会话结束时发布，除非由于服务器接收到一个带有 0x00（普通断开）原因码的 DISCONNECT 包从而删除了遗嘱消息，或是在遗嘱延迟间隔时间过期前接收了一个带有相同客户端ID的连接 |
| [MQTT-3.1.2-9] | 当遗嘱标识被置为 1 时，服务器需采用连接标志中的遗嘱 QoS 和遗嘱保留消息字段，载荷中**必须**包括遗嘱属性集、遗嘱主题和遗嘱载荷字段 |
| [MQTT-3.1.2-10] | 当服务器发布遗嘱后或服务器从客户端收到了原因码为 0x00（普通断开）的 DISCONNECT 包后，服务器**必须**从会话状态中删除遗嘱消息 |
| [MQTT-3.1.2-11] | 当遗嘱标识被置为 0 时，遗嘱 QoS **必须**被置为 0（0x00） |
| [MQTT-3.1.2-12] | 当遗嘱标识被置为 1 时，遗嘱QoS的值可以是 0（0x00），1（0x01）或 2（0x02） |
| [MQTT-3.1.2-13] | 当遗嘱标识被置为 0 时，遗嘱保留消息的值**必须**被置为 0 |
| [MQTT-3.1.2-14] | 当遗嘱标识被置为 1 且遗嘱保留消息被置为 0 时，服务器**必须**将遗嘱消息作为一个非保留消息发布 |
| [MQTT-3.1.2-15] | 当遗嘱标识被置为 1 且遗嘱保留消息被置为 1 时，服务器**必须**将遗嘱消息作为一个保留消息发布 |
| [MQTT-3.1.2-16] | 当用户名标识被置为 0 时，载荷中**必须不**存在用户名 |
| [MQTT-3.1.2-17] | 当用户名标识被置为 1 时，载荷中**必须**存在用户名 |
| [MQTT-3.1.2-18] | 当密码标识被置为 0 时，载荷中**必须不**存在密码 |
| [MQTT-3.1.2-19] | 当密码标识被置为 1 时，载荷中**必须**存在密码 |
| [MQTT-3.1.2-20] | 如果保活时间不为 0 且没有任何其他需要发送的数据包，客户端**必须**发送 PINGREQ 包 |
| [MQTT-3.1.2-21] | 如果服务器在 CONNACK 中提供了服务器保活时间，则客户端**必须**采用服务器保活时间的值来替代自己发送的保活时间的值 |
| [MQTT-3.1.2-22] | 如果保活时间为非零值且服务器在 1.5 倍的保活时间内没有收到来自客户端的任何 MQTT 包，服务器**必须**断开到客户端的网络连接并视为网络连接故障 |
| [MQTT-3.1.2-23] | 当会话过期间隔的值大于 0 时，客户端和服务器都**必须**在网络连接断开后存储会话状态 |
| [MQTT-3.1.2-24] | 服务器**必须不**向客户端发送超过最大包尺寸的数据包 |
| [MQTT-3.1.2-25] | 当一个包因超过最大包尺寸而无法发送，服务器**必须**将其丢弃，并视为发送成功 |
| [MQTT-3.1.2-26] | 服务器**必须不**发送一个主题别名的值大于客户端设置的主题别名最大值的 PUBLISH 包 |
| [MQTT-3.1.2-27] | 如果主题别名最大值未设置或值为 0，服务器**必须不**向客户端发送主题别名 |
| [MQTT-3.1.2-28] | 此值为 0 表示服务器**必须不**在 CONNACK 中回复响应信息 |
| [MQTT-3.1.2-29] | 如果请求问题信息的值为 0，服务器可以在 CONNACK 或 DISCONNECT 包中携带原因字符串或用户属性，但**必须不**在除 PUBLISH，CONNACK，DISCONNECT 之外的包中携带原因字符串或用户属性 |
| [MQTT-3.1.2-30] | 如果客户端再 CONNECK 包中设置了认证方式，那么在其收到 CONNACK 包之前，客户端**必须不**发送除了 AUTH 和 DISCONNECT 包之外的任何类型的包 |
| [MQTT-3.1.3-1] | CONNECT 中的载荷包含了一个或多个 长度 + 内容 格式的字段，这些字段的存在与否由可变头中的标志位决定。这些字段的顺序是固定的，如果存在的话，**必须**按照 客户端ID，遗嘱属性集，遗嘱主题，遗嘱载荷，用户名，密码 这样的顺序出现 |
| [MQTT-3.1.3-2] | 客户端ID**必须**被客户端和服务器用于关联客户端和服务器之间的会话状态 |
| [MQTT-3.1.3-3] | 客户端ID**必须**作为 CONNECT 包载荷中的第一个字段出现 |
| [MQTT-3.1.3-4] | 客户端ID**必须**被编码为一个 `UTF-8字符串` |
| [MQTT-3.1.3-5] | 服务器**必须**允许客户端ID是长度为 1 到 23 个字节之间的 `UTF-8字符串`，且仅包含下列字符：“0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ” |
| [MQTT-3.1.3-6] | 服务器**可以**允许客户端传递长度为 0 的客户端ID，当此情况发生时，服务器**必须**将此情况作为一个特殊情况对待，并为客户端分配一个唯一的客户端ID |
| [MQTT-3.1.3-7] | 服务器之后**必须**正常处理此 CONNECT 包，就如同客户端本身携带了这个唯一的客户端ID一样，而且**必须**在 CONNACK 包中返回这个分配的客户端ID |
| [MQTT-3.1.3-8] | 如果服务器拒绝了客户端ID，服务器**可以**使用一个带有原因码 0x85（客户端ID不可用）的 CONNACK 包作为对客户端 CONNECT 包的响应，如同 [4.13] 中描述的那样，之后服务器**必须**关闭网络连接 |
| [MQTT-3.1.3-9] | 如果在遗嘱延迟间隔结束前，该会话被新的网络连接延续，服务器**必须不**发送遗嘱 |
| [MQTT-3.1.3-10] | 服务器**必须**在发布遗嘱消息时维持用户属性的顺序 |
| [MQTT-3.1.3-11] | 遗嘱主题**必须**是一个 `UTF-8字符串` |
| [MQTT-3.1.3-12] | 用户名**必须**是一个 `UTF-8字符串` |
| [MQTT-3.1.4-1] | 服务器**必须**验证 CONNECT 包的格式符合 [3.1] 中的描述，如不符合则关闭网络连接 |
| [MQTT-3.1.4-2] | 服务器**可以**检查 CONNECT 包中的内容是否满足更进一步的限制要求，并且**应该**进行认证和授权检查。如果其中任何检查失败，服务器**必须**关闭网络连接 |
| [MQTT-3.1.4-3] | 如果客户端ID代表了一个已经连接到服务器的客户端，服务器参考 [4.13] 发送一个带有原因码 0x8E（会话被接管）的 DISCONNECT 包到当前已有连接的客户端，且**必须**关闭当前已有连接客户端的网络连接 |
| [MQTT-3.1.4-4] | 服务器**必须**参考 [3.1.2.4] 中的描述处理全新开始标识 |
| [MQTT-3.1.4-5] | 服务器**必须**使用带有原因码为 0x00（成功）的 CONNACK 回复 CONNECT 包 |
| [MQTT-3.1.4-6] | 如果服务器拒绝了 CONNECT，服务器**必须不**处理客户端在 CONNECT 包之后发送的任何除了 AUTH 以外的包 |
| [MQTT-3.2.0-1] | 服务器**必须**在发送除 AUTH 外的其他任何MQTT包之前使用带有响应码 0x00（成功）的 CONNACK 包回复客户端 |
| [MQTT-3.2.0-2] | 服务器**必须不**在一次网络连接中发送超过一个 CONNACK 包 |
| [MQTT-3.2.2-1] | Byte 1 是 “连接回复标识”。Bits 7-1 是保留字段，**必须**被置为 0 |
| [MQTT-3.2.2-2] | 如果服务器接收连接的全新开始标识被置为 1，服务器**必须**在带有 0x00（成功）的原因码的 CONNACK 包中将会话展示置为 0 |
| [MQTT-3.2.2-3] | 如果服务器接收到的连接中全新开始位被置为 0，且服务器持有对此客户端ID的会话状态，服务器**必须**在 CONNACK 包中将会话展示标识置为 1，其他情况下，服务器都**必须**在 CONNACK 包中将会话展示标识置为 0。这两种情况下服务器都**必须**在 CONNACK 中使用原因码 0x00（成功） |
| [MQTT-3.2.2-4] | 如果客户端不持有会话状态，且接收到的会话展示值为 1，客户端**必须**关闭网络连接 |
| [MQTT-3.2.2-5] | 如果客户端持有会话状态且收到的会话展示值为 0，如果客户端继续使用此网络连接，客户端**必须**丢弃会话状态 |
| [MQTT-3.2.2-6] | 如果服务器使用非 0 原因码的 CONNACK 包，服务器**必须**将会话展示的值置为 0 |
| [MQTT-3.2.2-7] | 如果服务器发送的 CONNACK 包带有一个值为 128 或更高的原因码，服务器**必须**随后关闭网络连接 |
| [MQTT-3.2.2-8] | 服务器发送的 CONNACK **必须**使用下述之一的原因码 |
| [MQTT-3.2.2-9] | 如果服务器不支持 QoS 1 或 QoS 2 的 PUBLISH，服务器**必须**发送一个带有其可以支持的最大QoS的 CONNACK 包 |
| [MQTT-3.2.2-10] | 一个不支持 QoS 1 或 QoS 2 PUBLISH 的服务器**必须**依然接收包含 QoS 0、1 或 2 的 SUBSCRIBE 包 |
| [MQTT-3.2.2-11] | 如果客户端从服务器接收了最大QoS，客户端**必须不**发送QoS等级超过最大QoS的 PUBLISH 包 |
| [MQTT-3.2.2-12] | 如果服务器收到包含超过其能力的遗嘱QoS的 CONNECT 数据包，服务器**必须**拒绝连接。服务器**应该**回复带有原因码 0x9B（不支持的 QoS）的 CONNACK 包，参考 [4.13] 错误处理，且随后**必须**关闭网络连接 |
| [MQTT-3.2.2-13] | 如果服务器接收到的 CONNECT 包中包含遗嘱消息，且遗嘱保留消息的值为 1，同时服务器不支持保留消息，服务器**必须**拒绝此连接请求。服务器**应该**发送带有原因码 0x9A（不支持保留消息）的 CONNACK 且随后**必须**关闭网络连接 |
| [MQTT-3.2.2-14] | 一个收到了服务器发送的保留消息可用值为 0 的客户端，**必须不**发送带有保留消息标识为 1 的 PUBLISH 包 |
| [MQTT-3.2.2-15] | 客户端**必须不**向服务器发送超过最大包尺寸的数据包 |
| [MQTT-3.2.2-16] | 如果客户端使用长度为 0 的客户端ID连接，服务器**必须**使用带有分配的客户端ID的 CONNACK 回复。分配的客户端ID**必须**是一个当前所有会话都没有使用的全新ID |
| [MQTT-3.2.2-17] | 客户端**必须不**能发送一个主题别名的值大于服务器设置的主题别名最大值的 PUBLISH 包 |
| [MQTT-3.2.2-18] | 如果主题别名最大值未设置或值为 0，客户端**必须不**向服务器发送主题别名 |
| [MQTT-3.2.2-19] | 如果因为添加原因字符串会导致 CONNACK 的包尺寸超过了客户端限制的最大包尺寸，服务器**必须不**发送此属性 |
| [MQTT-3.2.2-20] | 如果添加该属性会导致 CONNACK 的包尺寸大于客户端设置的最大包尺寸，服务器**必须不**添加此属性 |
| [MQTT-3.2.2-21] | 如果服务器在 CONNACK 中发送了服务器保活时间，客户端**必须**使用此值代替其在 CONNECT 中发送的保活时间 |
| [MQTT-3.2.2-22] | 如果服务器没有设置服务器保活时间，服务器**必须**使用客户端在 CONNECT 包中设置的保活时间 |
| [MQTT-3.3.1-1] | 当客户端或服务器尝试重传 PUBLISH 包时，他们**必须**把重复标志置为 1 |
| [MQTT-3.3.1-2] | 对于 QoS 0 的消息，重复标识**必须**被置为 0 |
| [MQTT-3.3.1-3] | 转发的 PUBLISH 包的重复标识独立于接收的 PUBLISH 包，此值仅被本次转发包是否为重传独立决定 |
| [MQTT-3.3.1-4] | PUBLISH 包**必须不**能将 QoS 的两个 bit 都设置为 1 |
| [MQTT-3.3.1-5] | 当客户端向服务器发送的 PUBLISH 包中的保留消息被置为 1 时，服务器**必须**在此主题下保存此应用消息，替换任何已经存在的消息 |
| [MQTT-3.3.1-6] | 如果载荷为空，服务器照常处理，只不过该同名主题下现有的保留消息**必须**被移除，未来的订阅者也不会再收到保留消息 |
| [MQTT-3.3.1-7] | 带有空载荷的保留消息**必须不**被服务器作为保留消息存储 |
| [MQTT-3.3.1-8] | 如果客户端发送到服务器的 PUBLISH 包中的保留消息值为 0，服务器**必须不**将该消息作为保留消息存储且**必须不**删除或替换已经存在的保留消息 |
| [MQTT-3.3.1-9] | 如果保留消息处理值为 0，服务器**必须**将匹配订阅主题过滤器的保留消息发送给客户端 |
| [MQTT-3.3.1-10] | 如果保留消息处理值为 1，当该订阅之前不存在时，服务器**必须**将匹配订阅主题过滤器的保留消息发送给客户端，反之当该订阅之前存在时，服务器**必须不**发送保留消息 |
| [MQTT-3.3.1-11] | 如果保留消息处理值为 2，服务器**必须不**发送保留消息 |
| [MQTT-3.3.1-12] | 如果保留消息引用发布的值为 0，服务器**必须**在转发应用消息时将保留消息值置为 0，无论其收到的 PUBLISH 包中的保留消息值如何设置 |
| [MQTT-3.3.1-13] | 如果保留消息引用发布的值为 1，服务器**必须**使用和收到的 PUBLISH 包中保留消息值相同的保留消息值 |
| [MQTT-3.3.2-1] | 主题名称**必须**作为 PUBLISH 包可变头的第一个字段。他**必须**采用 `UTF-8字符串` 编码 |
| [MQTT-3.3.2-2] | PUBLISH 包中的主题名称**必须不**包含通配符 |
| [MQTT-3.3.2-3] | 服务器发往客户端的 PUBLISH 包中的主题名称必须匹配订阅者的主题过滤器 |
| [MQTT-3.3.2-4] | 服务器**必须**将载荷格式标识原封不动的发送给所有应用消息的接收者 |
| [MQTT-3.3.2-5] | 当该字段存在时，此四字节的值表示以秒为单位的应用消息生命时间。如果消息过期间隔已经超时，且服务器尚未设法开始向前传递到匹配的订阅者，服务器**必须**删除面向该订阅者的该消息的副本 |
| [MQTT-3.3.2-6] | 客户端发送给服务器的 PUBLISH 包中的消息过期间隔**必须**被设置为服务器接收的消息过期间隔的值减去消息在服务器中等待的时间 |
| [MQTT-3.3.2-7] | 接收者**必须不**能将主题别名从一个网络连接转发到另一个网络连接 |
| [MQTT-3.3.2-8] | 发送者**必须不**能发送一个包含主题别名值为 0 的 PUBLISH 包 |
| [MQTT-3.3.2-9] | 客户端**必须不**发送包含主题别名值超过服务器 CONNACK 中设置的主题别名最大值的 PUBLISH 包 |
| [MQTT-3.3.2-10] | 客户端**必须**接收所有大于 0 且小于或等于其 CONNECT 包中设置的主题别名最大值的主题别名 |
| [MQTT-3.3.2-11] | 服务器**必须不**发送包含主题别名值超过客户端 CONNECT 包中设置的主题别名最大值的 PUBLISH 包 |
| [MQTT-3.3.2-12] | 服务器**必须**接收所有大于 0 且小于等于其 CONNACK 包中设置的主题别名最大值的主题别名 |
| [MQTT-3.3.2-13] | 响应主题**必须**使用 `UTF-8字符串` 格式 |
| [MQTT-3.3.2-14] | 响应主题**必须不**包含通配符 |
| [MQTT-3.3.2-15] | 服务器**必须**向所有接收该应用消息的订阅者原封不动的转发响应主题 |
| [MQTT-3.3.2-16] | 服务器**必须**将关联数据原封不动的转发给接收应用消息的订阅者 |
| [MQTT-3.3.2-17] | 服务器**必须**将 PUBLISH 包中的所有用户属性原封不动的转发给客户端 |
| [MQTT-3.3.2-18] | 服务器**必须**在转发应用消息时维护用户属性的顺序 |
| [MQTT-3.3.2-19] | 内容类型**必须**是 `UTF-8字符串` 格式 |
| [MQTT-3.3.2-20] | 服务器**必须**将内容格式原封不动的转发给所有接收应用消息的订阅者 |
| [MQTT-3.3.4-1] | PUBLISH 包的接收者**必须**使用 PUBLISH 包中 QoS 对应的方式响应此包 |
| [MQTT-3.3.4-2] | 在这种情况下服务器**必须**使用这些重叠订阅中最高的 QoS 等级来发布此数据 |
| [MQTT-3.3.4-3] | 如果客户端在重叠订阅时设置了订阅ID，服务器**必须**在为该订阅发布消息时将订阅ID放入消息中 |
| [MQTT-3.3.4-4] | 如果服务器发送该消息的单一副本，服务器**必须**将所有包含订阅ID的订阅动作的订阅ID放入 PUBLISH 包中，他们的顺序不重要 |
| [MQTT-3.3.4-5] | 如果服务器发送该消息的多个副本，服务器**必须**在每个副本中放入对应订阅动作的订阅ID |
| [MQTT-3.3.4-6] | 从客户端发往服务器的 PUBLISH 包**必须不**携带订阅ID |
| [MQTT-3.3.4-7] | 当客户端没有接收到足够的 PUBACK、PUBCOMP 或带有大于等于 128 原因码的 PUBREC 时，客户端**必须不**发送QoS 1 或 QoS 2 的 PUBLISH 包导致其需接收的返回数量超过接收最大值 |
| [MQTT-3.3.4-8] | 客户端不能延迟任何包的发送，除了因未收到接受回复而达到接收最大值因此未能发送的 PUBLISH 包 |
| [MQTT-3.3.4-9] | 当服务器没有接收到足够的 PUBACK、PUBCOMP 或带有大于等于 128 原因码的 PUBREC 时，服务器**必须不**发送QoS 1 或 QoS 2 的 PUBLISH 包导致其需接收的返回数量超过接收最大值 |
| [MQTT-3.3.4-10] | 服务器不能延迟任何包的发送，除了因未收到接受回复而达到接收最大值因此未能发送的 PUBLISH 包 |
| [MQTT-3.4.2-1] | 客户端或服务器发送的 PUBACK 包**必须**采用上述之一的 PUBACK 原因码 |
| [MQTT-3.4.2-2] | 如果添加此字段会导致 PUBACK 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.4.2-3] | 如果添加此字段会导致 PUBACK 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.5.2-1] | 客户端或服务器发送的 PUBREC 包**必须**采用上述之一的 PUBREC 原因码 |
| [MQTT-3.5.2-2] | 如果添加此字段会导致 PUBREC 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.5.2-3] | 如果添加此字段会导致 PUBREC 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.6.1-1] | PUBREL 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接 |
| [MQTT-3.6.2-1] | 客户端或服务器发送的 PUBREL 包**必须**采用上述之一的 PUBREL 原因码 |
| [MQTT-3.6.2-2] | 如果添加此字段会导致 PUBREL 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.6.2-3] | 如果添加此字段会导致 PUBREL 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.7.2-1] | 客户端或服务器发送的 PUBCOMP 包**必须**采用上述之一的 PUBCOMP 原因码 |
| [MQTT-3.7.2-2] | 如果添加此字段会导致 PUBCOMP 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.7.2-3] | 如果添加此字段会导致 PUBCOMP 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.8.1-1] | SUBSCRIBE 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接 |
| [MQTT-3.8.3-1] | 主题过滤器**必须**是一个 `UTF-8字符串` |
| [MQTT-3.8.3-2] | 载荷**必须**至少包含一个主题过滤器和订阅选项对 |
| [MQTT-3.8.3-3] | 订阅选项中的 Bit 2 表示非本地选项。如果其值为 1，服务器**必须不**将应用消息转发给与发布者客户端ID相同的订阅者 |
| [MQTT-3.8.3-4] | 在共享订阅中非本地选项值为 1 视为协议错误 |
| [MQTT-3.8.3-5] | 服务器**必须**将载荷中保留字段值非 0 的 SUBSCRIBE 包视为格式错误的包 |
| [MQTT-3.8.4-1] | 当服务器从客户端收到 SUBSCRIBE 包，服务器**必须**使用 SUBACK 响应 |
| [MQTT-3.8.4-2] | SUBACK 中的包ID**必须**和其对应的 SUBSCRIBE 包中的包ID一致 |
| [MQTT-3.8.4-3] | 如果服务器接收到一个 SUBSCRIBE 包，其中包含的主题过滤器和现在会话中的一个订阅完全相同，服务器**必须**使用新订阅取代现有的订阅 |
| [MQTT-3.8.4-4] | 如果他的保留消息处理选项值为 0，且主题过滤器中现在有匹配的保留消息，服务器**必须**重新发送，但是服务器**必须不**能因为订阅的替换导致应用消息的丢失 |
| [MQTT-3.8.4-5] | 如果一个服务器接受的 SUBSCRIBE 包包含有多个订阅主题，服务器**必须**像接收了多个独立的 SUBSCRIBE 包一个逐个处理，唯一的不同是服务器将所有订阅请求的响应放入一个 SUBACK 包中回复 |
| [MQTT-3.8.4-6] | 服务器发往客户端的 SUBACK **必须**为每一个 主题过滤器/订阅选项 对提供一个原因码 |
| [MQTT-3.8.4-7] | 这个原因码**必须**提供服务器为此次订阅分配的最大QoS或是指明本次订阅失败 |
| [MQTT-3.8.4-8] | 发送给订阅者的应用消息中的QoS**必须**是原始 PUBLISH 包中的QoS和服务器分配的最大QoS两者中的较小值 |
| [MQTT-3.9.2-1] | 如果添加此字段会导致 SUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段 |
| [MQTT-3.9.2-2] | 如果添加此字段会导致 SUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段 |
| [MQTT-3.9.3-1] | SUBACK 中原因码的顺序**必须**与 SUBSCRIBE 中主题过滤器的顺序匹配 |
| [MQTT-3.9.3-2] | 服务器发送的 SUBACK 包**必须**对每个收到的主题过滤器使用上表列出的原因码进行回复 |
| [MQTT-3.10.1-1] | UNSUBSCRIBE 包固定头中的 Bit 3、2、1、0 为保留字段，其值必须被分别设置为 0、0、1、0。服务器**必须**将其他值视为格式错误的包并关闭网络连接 |
| [MQTT-3.10.3-1] | UNSUBSCRIBE 中的主题过滤器**必须**是 `UTF-8字符串` |
| [MQTT-3.10.3-2] | UNSUBSCRIBE 包的载荷中**必须**至少包含一个主题过滤器 |
| [MQTT-3.10.4-1] | 服务器**必须**逐字符的核对 UNSUBSCRIBE 包中提供的主题过滤器（无论其是否包含通配符）是否与其持有的当前客户端的订阅相同。如果任何过滤器被精确匹配，那么其拥有的订阅**必须**被删除 |
| [MQTT-3.10.4-2] | 服务器**必须**停止向该主题过滤器添加新的发往客户端的消息 |
| [MQTT-3.10.4-3] | 服务器**必须**完成匹配该主题过滤器的，且已经开始发往客户端的 QoS 1 和 QoS 2 消息的交付 |
| [MQTT-3.10.4-4] | 服务器**必须**使用 UNSUBACK 包响应 UNSUBSCRIBE 请求 |
| [MQTT-3.10.4-5] | UNSUBACK 包**必须**和 UNSUBSCRIBE 包有相同的包ID。即使没有主题订阅被删除，服务器也**必须**使用 UNSUBACK 回复 |
| [MQTT-3.10.4-6] | 如果服务器收到的 UNSUBSCIRIBE 包包含有多个主题过滤器，服务器**必须**按序处理就如同他按序逐个收到了 UNSUBSCRIBE 包，唯一不同是服务器仅需要使用一个 UNSUBACK 回复 |
| [MQTT-3.11.2-1] | 如果添加此字段会导致 UNSUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段 |
| [MQTT-3.11.2-2] | 如果添加此字段会导致 UNSUBACK 的尺寸大于客户端的最大包尺寸，服务器**必须不**添加此字段 |
| [MQTT-3.11.3-1] | UNSUBACK 包中的原因码顺序**必须**和 UNSUBSCRIBE 包中的主题过滤器顺序一致 |
| [MQTT-3.11.3-2] | 服务器发送的 UNSUBACK 包**必须**对每个收到的主题过滤器使用下表之一的原因码 |
| [MQTT-3.12.4-1] | 服务器**必须**发送 PINGRESP 包用来响应 PINGREQ 包 |
| [MQTT-3.14.0-1] | 服务器**必须不**发送 DISCONNECT 包，除非在其发送了一个原因码小于 0x80 的 CONNACK 之后 |
| [MQTT-3.14.1-1] | 客户端或服务器必须确认保留字段值为 0。如果非 0，客户端或服务器发送一个带有原因码 0x81（格式错误的包）的 DISCONNECT 包，参考 [4.13] 中的描述 |
| [MQTT-3.14.2-1] | 客户端或服务器发送的 DISCONNECT 包**必须**使用上表之一的断开原因码 |
| [MQTT-3.14.2-2] | 服务器发送的 DISCONNECT 包中**必须不**包括会话过期间隔 |
| [MQTT-3.14.2-3] | 如果添加此字段会导致 DISCONNECT 的尺寸大于接收者的最大包尺寸，发送者**必须不**添加此字段 |
| [MQTT-3.14.2-4] | 如果添加此字段会导致 DISCONNECT 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-3.14.4-1] | 发送 DISCONNECT 后，发送方**必须不**在此网络连接中再发送任何 MQTT 包 |
| [MQTT-3.14.4-2] | 发送 DISCONNECT 后，发送方**必须**关闭网络连接 |
| [MQTT-3.14.4-3] | 当接收到带有原因码 0x00（成功） 的 DISCONNECT 包后，服务器**必须**不发送改连接的遗嘱消息，并丢弃 |
| [MQTT-3.15.1-1] | AUTH 包固定头中的 Bit 3、2、1、0 的内容保留且值必须为 0。客户端或服务器**必须**将任何其他值视为格式错误的包并断开网络连接 |
| [MQTT-3.15.2-1] | AUTH 包的发送者**必须**使用下表之一的认证原因码 |
| [MQTT-3.15.2-2] | 如果添加此字段会导致 AUTH 的尺寸大于接收者的最大包尺寸，发送者**必须不**添加此字段 |
| [MQTT-3.15.2-3] | 如果添加此字段会导致 AUTH 的尺寸大于接收方的最大包尺寸，发送方**必须不**添加此字段 |
| [MQTT-4.1.0-1] | 客户端和服务器**必须不**在网络连接打开时丢弃会话状态 |
| [MQTT-4.2.0-1] | 客户端或服务器**必须**支持使用一种或多种底层传输协议，这些协议提供从客户端到服务器以及服务器到客户端的有序、无损的字节流。 |
| [MQTT-4.1.0-2] | 服务器**必须**在网络连接关闭且会话过期间隔到期后丢弃会话状态 |
| [MQTT-4.3.1-1] | 在 QoS 0 交付协议中，发送方**必须**发送 QoS 0 且重复标志值为 0 的 PUBLISH 包 |
| [MQTT-4.3.2-1] | 在 QoS 1 交付协议中，发送方**必须**在每次发布新消息时选择一个未被使用的包ID |
| [MQTT-4.3.2-2] | 在 QoS 1 交付协议中，发送方**必须**发送包含此包ID，且重复标志值为 0 的 PUBLISH 包 |
| [MQTT-4.3.2-3] | 在 QoS 1 交付协议中，发送方**必须**将此 PUBLISH 包视为 “未回复的” 直到从接收方收到了正确的 PUBACK |
| [MQTT-4.3.2-4] | 在 QoS 1 交付协议中，接收方**必须**使用包含 PUBLISH 包中包ID的 PUBACK 包进行响应，拥有收到的消息的所有权 |
| [MQTT-4.3.2-5] | 在 QoS 1 交付协议中，接收方在发送 PUBACK 包后，接收方**必须**将到来的带有相同包ID的 PUBLISH 包视为新的应用消息，无论其重复标志如何设置 |
| [MQTT-4.3.3-1] | 在 QoS 2 交付协议中，发送方**必须**在发布新消息时分配一个未使用的包ID |
| [MQTT-4.3.3-2] | 在 QoS 2 交付协议中，发送方**必须**发送 QoS 2，重复标志值为 0，携带此包ID的 PUBLISH 包 |
| [MQTT-4.3.3-3] | 在 QoS 2 交付协议中，发送方**必须**在收到接收方发来的对应的 PUBREC 之前将此 PUBLISH 包视为 “未回复的” |
| [MQTT-4.3.3-4] | 在 QoS 2 交付协议中，发送方**必须**在收到接收方发来的原因码小于 0x80 的 PUBREC 后，发送 PUBREL 包。此 PUBREL 包**必须**包含和原始 PUBLISH 包相同的包ID |
| [MQTT-4.3.3-5] | 在 QoS 2 交付协议中，发送方**必须**在收到接收方发来的对应 PUBCOMP 之前将此 PUBREL 包视为 “未回复的” |
| [MQTT-4.3.3-6] | 在 QoS 2 交付协议中，发送方**必须不**在发送 PUBREL 之后重发 PUBLISH 包 |
| [MQTT-4.3.3-7] | 在 QoS 2 交付协议中，发送方**必须不**在发送 PUBLISH 包之后使此应用消息过期 |
| [MQTT-4.3.3-8] | 在 QoS 2 交付协议中，接收方**必须**使用和收到 PUBLISH 包相同的包ID的 PUBREC 包响应，拥有收到的消息的所有权 |
| [MQTT-4.3.3-9] | 在 QoS 2 交付协议中，接收方如果已经使用带有 0x80 或更大值的原因码的 PUBREC 包回复，接收方**必须**将后续带有相同包ID的 PUBLISH 包视为新应用消息 |
| [MQTT-4.3.3-10] | 在 QoS 2 交付协议中，接收方直到收到对应的 PUBREL 包为止，接收方**必须**使用 PUBREC 回复后续任何带有相同包ID的 PUBLISH 包。在此情形下**必须不**把重复的包转发给更进一步的消息使用者 |
| [MQTT-4.3.3-11] | 在 QoS 2 交付协议中，接收方**必须**使用和收到 PUBREL 包相同的包ID的 PUBCOMP 包响应 PUBREL 包 |
| [MQTT-4.3.3-12] | 在 QoS 2 交付协议中，接收方发送 PUBCOMP 包之后，接收方**必须**将后续带有相同包ID的 PUBLISH 包视为新应用消息发送 PUBCOMP 包之后，接收方**必须**将后续带有相同包ID的 PUBLISH 包视为新应用消息 |
| [MQTT-4.3.3-13] | 在 QoS 2 交付协议中，接收方即使消息已经过期，也**必须**继续 QoS 2 的响应动作 |
| [MQTT-4.4.0-1] | 当客户端使用全新开始值为 0 重连且存在会话时，客户端和服务器都**必须**使用原始的包ID重传所有未确认的 PUBLISH 包（其 QoS > 0）和 PUBREL 包。这是客户端或服务器**需要**重传消息的唯一场景。客户端和服务器**必须不**在其他任何时间重传消息 |
| [MQTT-4.4.0-2] | 如果接收到的 PUBACK 或 PUBREC 包含 0x80 或更大的原因代码，则相应的 PUBLISH 数据包将被视为已确认，且**必须不**被重传 |
| [MQTT-4.5.0-1] | 当服务器得到输入应用消息的所有权时，他**必须**把消息放入所有匹配订阅的客户端的会话状态 |
| [MQTT-4.5.0-2] | 无论何种情况，客户端**必须**按照匹配的 QoS 规则确认其收到包，无论客户端对包中的消息内容选择处理还是丢弃 |
| [MQTT-4.6.0-1] | 当客户端重传 PUBLISH 包时，其必须按照原始 PUBLISH 包的顺序发送（包括 QoS 1 和 QoS 2 消息） |
| [MQTT-4.6.0-2] | 客户端**必须**按照接收 PUBLSIH 包的顺序发送 PUBACK 包（QoS 1 消息） |
| [MQTT-4.6.0-3] | 客户端**必须**按照接收 PUBLSIH 包的顺序发送 PUBREC 包（QoS 2 消息） |
| [MQTT-4.6.0-4] | 客户端**必须**按照接收 PUBREC 包的顺序发送 PUBREL 包（QoS 2 消息） |
| [MQTT-4.6.0-5] | 当服务器处理发布到有序主题的消息时，服务器**必须**保证其对消费者发送的 PUBLISH 包（对于相同主题和相同 QoS）的顺序和服务器从客户端接收这些包时相同 |
| [MQTT-4.6.0-6] | 默认情况下，服务器在转发非共享订阅上的消息时**必须**将每个主题视为有序主题。 |
| [MQTT-4.7.0-1] | 通配符可以在主题过滤器中使用，但**必须不**在主题名称中使用 |
| [MQTT-4.7.1-1] | 多级通配符**必须**单独使用或在主题级别分隔符后使用。在任意情况下他都**必须**是主题过滤器中的最后一个字符 |
| [MQTT-4.7.1-2] | 当他被使用时，他**必须**占据过滤器中一个完整的级别 |
| [MQTT-4.7.2-1] | 服务器**必须不**将以通配符（# 或 +）开始的主题过滤器与以 $ 开头的主题名匹配 |
| [MQTT-4.7.3-1] | 所有的主题名称和主题过滤器**必须**至少包含一个字符 |
| [MQTT-4.7.3-2] | 主题名称和主题过滤器中必须不能包括 null 字符（Unicode U+0000） |
| [MQTT-4.7.3-3] | 主题名称和主题过滤器是 `UTF-8字符串`；**必须不**超过 65535 字节 |
| [MQTT-4.7.3-4] | 当进行订阅匹配时，服务器**必须不**对主题名称或主题过滤器执行任何标准化处理，或对无法识别的字符进行任何修改或替换 |
| [MQTT-4.8.2-1] | 共享订阅的主题过滤器**必须**以 $share/ 开始且**必须**包括至少一字符的共享名称 |
| [MQTT-4.8.2-2] | 共享名称**必须不**包含字符 '/'、'+'、'#'，但**必须**在其后跟随 '/' 字符。此 '/' 字符后**必须**跟随主题过滤器 |
| [MQTT-4.8.2-3] | 服务器**必须**遵守客户端订阅时授予的 QoS 等级 |
| [MQTT-4.8.2-4] | 服务器**必须**在客户端重新连接时完成该消息的交付 |
| [MQTT-4.8.2-5] | 如果该客户端的会话在其重连成功前终止了，服务器**必须不**将此应用消息发送给其他的订阅客户端 |
| [MQTT-4.8.2-6] | 如果客户端使用带有 0x80 或更大原因码的 PUBACK 或 PUBREC 响应来自服务器的 PUBLISH 包，服务器**必须**丢弃应用消息，并且不再尝试将消息发给其他订阅者 |
| [MQTT-4.9.0-1] | 客户端或服务器**必须**将其发送配额初始化为不超过接收最大值的非零值 |
| [MQTT-4.9.0-2] | 每当客户端或服务器发送 QoS > 0 的 PUBLISH 包，降低配额。如果发送配额值达到 0，客户端或服务器**必须不**再发送任何 QoS > 0 的 PUBLISH 包 |
| [MQTT-4.9.0-3] | 即使配额值为 0，客户端和服务器**必须**继续处理和响应其他类型的 MQTT 包 |
| [MQTT-4.12.0-1] | 如果服务器不支持客户端提供的认证方式，服务器**可以**发送带有原因码 0x8C（认证方式错误）或原因码 0x87（未经授权）的 CONNACK 包，并**必须**关闭网络连接，参考 [4.13] 中的描述 |
| [MQTT-4.12.0-2] | 如果服务器需要额外信息来完成认证，他可以向客户端发送一个 AUTH 数据包。此数据包**必须**包含原因码 0x18（继续认证） |
| [MQTT-4.12.0-3] | 客户端通过发送另一个 AUTH 包来响应来自服务器的 AUTH 包。此包必须包含原因码 0x18（继续认证） |
| [MQTT-4.12.0-4] | 服务器可以在认证过程的任何点拒绝认证。他**可以**根据 [4.13] 的描述发送一个原因码为 0x80 或以上的 CONNACK 数据包，并**必须**关闭网络连接 |
| [MQTT-4.12.0-5] | 如果初始 CONNECT 包包含认证方法，则所有 AUTH 包和任何成功的 CONNACK 包都必须包含和 CONNECT 包中相同值的 认证方法 |
| [MQTT-4.12.0-6] | 如果客户端没有在 CONNECT 包中包含认证方法，则服务器**必须不**发送 AUTH 包，也**必须不**在 CONNACK 包中包含认证方法 |
| [MQTT-4.12.0-7] | 如果客户端没有在 CONNECT 包中包含认证方法，则客户端**必须不**向服务器发送 AUTH 包 |
| [MQTT-4.12.1-1] | 如果客户端在 CONNECT 包中提供了认证方法，则可以在收到 CONNACK 后随时启动重新认证。通过发送原因码为 0x19（重新认证）的 AUTH 包来实现。客户端**必须**将认证方法设置为与最初用于认证网络连接的认证方法相同的值 |
| [MQTT-4.12.1-2] | 如果重新认证失败，客户端或服务器**应该**带有合适原因码的 DISCONNECT 包，且**必须**断开网络连接，参考 [4.13] 中的描述 |
| [MQTT-4.13.1-1] | 当服务器检测到格式错误的包或协议错误，且给出了规范中的原因码后，他**必须**断开网络连接 |
| [MQTT-4.13.2-1] | CONNACK 和 DISCONNECT 包允许使用原因码为 0x80 或更高来指示网络连接将被关闭。如果指定了 0x80 或更高的原因码，则无论是否发送了 CONNACK 或 DISCONNECT 包，都**必须**关闭网络连接 |
| [MQTT-6.0.0-1] | MQTT 包**必须**在 WebSocket 二进制数据帧中发送。 如果收到任何其他类型的数据帧，接收方**必须**关闭网络连接 |
| [MQTT-6.0.0-2] | 单个 WebSocket 数据帧可以包含多个或部分 MQTT 包。 接收方不得假定 MQTT 包与 WebSocket 帧边界对齐 |
| [MQTT-6.0.0-3] | 客户端**必须**在其提供的 WebSocket 子协议列表中包含“mqtt” |
| [MQTT-6.0.0-4] | 服务器选择并返回的 WebSocket 子协议名称**必须**为“mqtt” |

# 附录 C. MQTT v5.0 新特性汇总（非规范性）

下列新特性被引入了 MQTT v5.0

- 会话过期机制
将 Clean Session 拆分为全新开始会话和会话过期间隔，全新开始会话指示是否应在不使用现有会话的情况下启动会话，会话过期间隔指示断开连接后保留会话的时间长短。会话过期间隔可以在断开连接时修改。将全新开始会话设置为 1 且将会话过期间隔设置为 0 等同于在 MQTT v3.1.1 中将 Clean Session 设置为 1。

- 消息过期
允许发布消息时设置过期时间。

- 所有 ACK 的原因码
将所有响应包都改为带有原因码的包。包括 CONNACK，PUBACK，PUBREL，PUBCOMP，SUBACK，UNSUBACK，DISCONNECT 和 AUTH。这使得调用者可以判断请求的函数是否成功。

- 所有 ACK 的原因字符串
将所有响应包都改为带有原因码的包，同时也允许带原因字符串。这被设计用于问题定位，且不应被接收者解析。

- 服务器断开
允许服务器发送 DISCONNECT 包以指示断开的原因。

- 载荷格式和内容类型
允许在发布消息时指定有效负载格式（二进制、文本）和 MIME 样式内容类型，这些被转发到消息的接收者。

- 请求/响应
在 MQTT 中形式化请求/响应模式，并提供响应主题和关联数据属性，以允许将响应消息路由回请求的发布者。另外，添加客户端从服务器获取有关如何构建响应主题的配置信息的功能。

- 共享订阅
添加共享订阅支持，实现消费者对订阅的负载均衡。

- 订阅ID
允许在 SUBSCRIBE 上指定数字订阅标识符，并在传递消息时在消息上返回该标识符。 这允许客户端确定哪个或哪些订阅导致消息被传递。

- 主题别名
通过允许主题名称映射为整数来减少 MQTT 数据包开销的大小。客户端和服务器独立指定它们允许的主题别名数量。

- 流量控制
允许客户端和服务器独立指定它们允许的未完成可靠消息的数量（QoS>0）。发送方通过暂停发送使未处理消息总量低于此配额。这用于限制可靠消息的速率，并限制“正在处理”的消息数量。

- 用户属性
将用户属性添加到大多数包中。PUBLISH 上的用户属性包含在消息中，并由客户端应用程序定义。PUBLISH 和遗嘱属性集上的用户属性由服务器转发给消息的接收者。 CONNECT、SUBSCRIBE 和 UNSUBSCRIBE 数据包上的用户属性由服务器实现定义。 CONNACK、PUBACK、PUBREC、PUBREL、PUBCOMP、SUBACK、UNSUBACK 和 AUTH 数据包上的用户属性由发送方定义，并且对于发送方实现而言是唯一的。MQTT 未定义用户属性的含义。

- 最大包尺寸
允许客户端和服务器各自独立选择能支持的最大包尺寸。会话的对端发送超过尺寸的包是一种错误。

- 可选的服务器特性
定义一组服务器不允许的功能，且提供了一种机制让服务器向客户端指定这些功能。可以使用这种方式选择的功能包括：最大QoS，保留消息可用，通配符订阅可用，订阅ID可用，共享订阅。当服务器宣称这些特性不可用后服务器使用这些功能是一种错误。

在早期版本的 MQTT 中，服务器通过声明客户端无权限来避免这些未实现的功能。此功能允许这种可选行为被声明，并在客户端仍使用这些功能时添加对应的原因码。

- 增强认证
提供了一种启用挑战/响应式身份验证（包括双向认证）的机制。如果客户端和服务器都支持，则允许使用 SASL 风格的身份验证，并且客户端可以在连接中重新进行身份验证。

- 订阅选项
提供订阅选项，主要用于消息桥接应用程序。包括不发送源于自身的消息（非本地）（noLocal），如何处理保留消息（保留消息处理）。

- 遗嘱延迟
添加了指定连接结束和发送遗嘱消息之间延迟的功能。此功能旨在当会话的连接重新建立时不发送遗嘱消息。这允许短暂中断连接而无需通知其他人。

- 服务端保活
允许服务器指定希望客户端用作保活的值。这使服务器可以设置允许的最大保活时间，并确保客户端遵守该时间。

- 分配客户端ID
如果客户端ID是服务器分配的，返回分配的ID，这也解除了服务器分配的 ClientID 只能与 Clean Session=1 连接一起使用的限制。

- 服务器引用
允许服务器在 CONNACK 或 DISCONNECT 上指定要使用的备用服务器，可以用作重定向或进行服务配置。