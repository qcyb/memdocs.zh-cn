---
title: 状态消息
titleSuffix: Configuration Manager
description: 受支持版本的 Configuration Manager 中的状况消息说明。
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704585"
---
# <a name="state-messages-in-configuration-manager"></a>Configuration Manager 中的状况消息 

适用范围：  Configuration Manager (Current Branch)

状况消息包含有关 Configuration Manager 客户端状况的简明信息。 状况消息传递系统由 Configuration Manager 的特定组件（如软件更新和配置设置）使用。

Configuration Manager 客户端向回退状态点或管理点站点系统发送状况消息，报告操作的当前状态。 可以创建报表以查看由 Configuration Manager 客户端发送的状况消息。

使用状况消息的各个 Configuration Manager 功能通过状况消息的主题类型进行标识。 本文中列出的状况消息主题类型可用于定义状况消息相关的 Configuration Manager 功能。

> [!NOTE]  
> 状况消息 ID 的值为零 (0) 通常表示主题类型状态未知。

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 | 符合性状态未知|
| 1 | 合规 | 
| 2 | 不符合 | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0  | 强制状态未知 |
| 1  | 正在安装更新        | 
| 2  | 正在等待重新启动          | 
| 3  | 正在等待另一安装过程完成         | 
| 4  | 已成功安装更新 (2)          | 
| 5  | 正在等待系统重启         | 
| 6  | 安装更新失败         | 
| 7  | 正在下载更新   | 
| 8  | 已下载更新    | 
| 9  | 未能下载更新     | 
| 10 | 正在等待安装之前的维护时段         | 
| 11 | 等待业务流程         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|      
| 0 | 评估状态未知|                 
| 1 |评估已激活      |
| 2 |评估成功      |
| 3 |评估失败      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 | 检测状态未知|
| 1 | 不需要   |
| 2 | 未检测到    |
| 3 | 已检测   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 | 符合性状态未知|
| 1 |合规     |
| 2 |不符合     |
| 3 |检测到冲突    |
| 4 |错误      |
| 5 |Unknown     |
| 6 |部分符合   |
| 7 |符合性未配置    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0  | 强制状态未知|
| 1  |强制执行已启动          |
| 2  |强制执行正在等待内容         |
| 3  | 正在等待另一安装过程完成        |
| 4  |正在等待安装之前的维护时段         |
| 5  |安装之前要求重新启动         |
| 6  |常规失败        |
| 7  |等待的安装         |
| 8  |正在安装更新          |
| 9  |正在等待系统重启        |
| 10 |已成功安装更新         |
| 11 |未能安装更新        |
| 12 |正在下载更新        |
| 13 | 已下载更新        |
| 14 |未能下载更新        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
|0 |检测状态未知|
| 1 | 不需要更新  |
| 2 | 需要更新   |
| 3 | 已安装更新  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 |扫描状态未知|
| 1 | 扫描正在等待内容   |
| 2 | 扫描正在运行    |
| 3 | 扫描完毕    |
| 4 | 扫描正在等待重试   |
| 5 | 扫描失败   |
| 6 | 扫描已完成，但有错误 |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

无状态 ID。

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

无状态 ID。

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
无状态 ID。

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 100 |客户端部署已启动      |       
| 101 |正在等待下载       |       
| 102 |已计划部署       |       
| 103 | 正在等待部署前的时段 |
| 104 |部署已跳过       |       
| 301 |未知的客户端部署失败 |       
| 302 |未能创建 ccmsetup 服务  |       
| 303 |未能删除 ccmsetup 服务 |       
| 304 |无法在系统驱动器上启用了基于文件的写入筛选器 (FBWF) 的嵌入式操作系统上安装 |       
| 305 |纯安全模式在 Windows 2000 上无效  |       
| 306 |未能启动 ccmsetup 下载进程  |       
| 307 |无效的 ccmsetup 命令行 |       
| 308 |未能通过 WINHTTP 在下列地址下载文件 |       
| 309 |未能通过 BITS 在下列地址下载文件 |       
| 310 |未能安装 BITS 版本 |       
| 311 |无法验证必备文件是否是 MS 签名文件  |       
| 312 |磁盘已满，复制文件失败 |       
| 313 |Client.msi 安装失败，出现 MSI 错误 |       
| 314 |未能加载 ccmsetup.xml 清单文件 |       
| 315 |获取客户端证书失败  |       
| 316 |必备文件不是 MS 签名文件 |       
| 317 |需要重新启动才能继续安装  |       
| 318 |由于 MP 与客户端版本不匹配，无法在 MP 上安装客户端 |       
| 319 |不支持该操作系统或 Service Pack  |       
| 320 |不支持部署       |       
| 321 |缺少位        |       
| 322 |源文件夹不可用       |       
| 323 |不支持 Appv              |       
| 324 |站点版本不正确              |       
| 325 |必备的哈希不匹配       |       
| 326 |MDM 取消注册失败      |       
| 327 |检测到 MDM 注册      |       
| 328 |检测到 Intune       |       
| 329 |不允许使用按流量计费的网络      |       
| 400 |客户端部署成功 |  
| 401 |部署成功，需要重新启动     |       
| 402 |部署成功，重新启动成功     |
| 500 |客户端分配已启动|
| 601 |未知的客户端分配失败|
| 602 |下列站点代码无效|
| 603 |未能分配到 MP|
| 604 |未能发现默认管理点|
| 605 |未能下载站点签名证书|
| 606 |未能自动发现站点代码|
| 607 |站点分配失败；客户端版本高于站点版本|
| 608 |未能从 Active Directory 域服务和 SLP 获取站点版本|
| 609 |未能获取客户端版本|
| 700 |客户端分配成功|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

无状态 ID。

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 100 | 注册状态   |
| 101 | 已计划注册   |
| 102 | 已取消注册   |
| 105 | 已开始注册   |
| 106 | 注册成功，但未预配
| 107 | 注册成功且已预配
| 108 | 注册不活动用户   |
| 110 | 注册失败   |


## <a name="820--state_topictype_client_wufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 适用于企业的 Windows 更新客户端状态| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 磁盘空间   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

无状态 ID。

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

无状态 ID。

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

无状态 ID。

## <a name="1000--state_topictype_client_framework_comm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 客户端与管理点通信成功 |
| 2 | 客户端无法与管理点通信 |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |客户端已成功从本地证书存储检索证书    |
| 2 |客户端未能从本地证书存储检索证书 |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

无状态 ID。

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

无状态 ID。

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

无状态 ID。

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

无状态 ID。

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

无状态 ID。

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

无状态 ID。

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

无状态 ID。

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

无状态 ID。

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

无状态 ID。

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

无状态 ID。

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

无状态 ID。

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

无状态 ID。

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

无状态 ID。

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

无状态 ID。

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |客户端尚未就绪，无法进入纯模式  |
| 2 |客户端已就绪，可以进入纯模式     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 成功|
| 2 | 未成功 |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

无状态 ID。

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

无状态 ID。

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

无状态 ID。

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

无状态 ID。 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |用户关联已设置       |
| 2 |用户关联已删除       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

无状态 ID。

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

无状态 ID。

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1000  |配置项目成功           |
| 1001 |配置项目成功并已安装         |
| 1002 |配置项目成功并预检          |
| 1003 |配置项目快速状态成功          |
| 2000 |正在配置项目           |
| 2001 |正在配置项目，正在等待内容         |
| 2002 |正在配置项目，正在安装          |
| 2003 |正在配置项目，正在等待重新启动         |
| 2004 |正在配置项目，正在等待维护时段        |
| 2005 |正在配置项目，正在等待计划         |
| 2006 |正在配置项目，正在下载从属内容     |
| 2007 |正在配置项目，正在安装依赖项        |
| 2008 |正在配置项目，正在等待重新启动         |
| 2009 |正在配置项目，内容已下载         |
| 2010 |正在配置项目，正在等待更新         |
| 2011 |正在配置项目，正在等待用户重新连接        |
| 2012 |正在配置项目，正在等待用户注销         |
| 2013 |正在配置项目，正在等待用户登录         |
| 2014 |正在配置项目，正在等待安装         |
| 2015 |正在配置项目，正在等待重试         |
| 2016 |正在配置项目，正在等待 presmode         |
| 2017 |正在配置项目，正在等待业务流程        |
| 2018 |正在配置项目，正在等待网络         |
| 2019 |正在配置项目，正在等待更新 VE         |
| 2020 |正在配置项目，正在更新 VE         |
| 3000 |配置项目不符合要求           |
| 3001 |配置项目不符合要求，主机不适用        |
| 4000 |配置项目未知           |
| 5000 |配置项目出错            |
| 5001 |配置项目出错，正在评估          |
| 5002 |配置项目出错，正在安装          |
| 5003 |配置项目出错，正在检索内容         |
| 5004 |配置项目出错，正在安装依赖项         |
| 5005 |配置项目出错，正在检索内容依赖项        |
| 5006 |配置项目出错，规则冲突          |
| 5007 |配置项目出错，正在等待重试          |
| 5008 |配置项目出错，正在卸载取代        |
| 5009 |配置项目出错，正在下载取代         |
| 5010 |配置项目出错，正在更新 VE          |
| 5011 |配置项目出错，正在安装许可证         |
| 5012 |配置项目出错，正在检索允许的所有受信任的应用       |
| 5013 |配置项目出错，没有可用的许可证         |
| 5014 |配置项目出错，不支持该 OS          |
| 6000 |配置项目启动成功            |
| 6010 |配置项目启动出错            |
| 6020 |配置项目启动状态未知|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

无状态 ID。

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

无状态 ID。

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

无状态 ID。

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

无状态 ID。

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

无状态 ID。

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

无状态 ID。

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

无状态 ID。

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

无状态 ID。

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |Endpoint Protection 未托管   |
| 2 |Endpoint Protection 正在等待安装  |
| 3 |Endpoint Protection 已托管   |
| 4 |Endpoint Protection 安装失败  |
| 5 |Endpoint Protection 重新启动挂起  |
| 6 |不支持 Endpoint Protection   |
| 7 |Endpoint Protection 已共同管理   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 |Endpoint Protection 策略应用程序状态未知    |
| 1 |Endpoint Protection 策略应用程序已成功    |
| 2 |Endpoint Protection 策略应用程序失败    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 0 |  Unknown    |
| 1 |  活动    |
| 2 |  非活动    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 唤醒代理未安装    |
| 2 | 唤醒代理正在等待安装   |
| 3 | 唤醒代理已安装    |
| 4 | 唤醒代理安装失败   |
| 5 | 唤醒代理正在等待重新启动   |
| 6 | 此 OS 上不支持唤醒代理  |
| 7 | 唤醒代理服务器选择退出   |
| 8 | 唤醒代理卸载失败   |
| 9 | 不支持唤醒代理运行时   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

无状态 ID。

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

无状态 ID。

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

无状态 ID。

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
|0 | Windows 推送通知服务通道已设置|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

无状态 ID。

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

无状态 ID。

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

无状态 ID。

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

无状态 ID。

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

无状态 ID。

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

无状态 ID。

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

无状态 ID。

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

无状态 ID。

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

无状态 ID。

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

无状态 ID。

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

无状态 ID。

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

无状态 ID。

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |已发出质询         |
| 2 |质询发出失败        |
| 3 |请求创建失败        |
| 4 |请求提交失败        |
| 5 |质询验证成功       |
| 6 |质询验证失败       |
| 7 |发出失败         |
| 8 |问题挂起         |
| 9 |已发出          |
| 10 |响应处理失败       |
| 11 |响应挂起         |
| 12 |注册成功         |
| 13 |无需注册         |
| 14 |已吊销          |
| 15 |已从集合中删除        |
| 16 |已验证续订         |
| 17 |安装失败        |
| 18 |已安装         |
| 19 |删除失败         |
| 20 |已删除         |
| 21 |已请求续订        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |已发出质询         |
| 2 |质询发出失败        |
| 3 |请求创建失败        |
| 4 |请求提交失败        |
| 5 |质询验证成功       |
| 6 |质询验证失败       |
| 7 |发出失败         |
| 8 |问题挂起         |
| 9 |已发出          |
| 10 |响应处理失败       |
| 11 |响应挂起         |
| 12 |注册成功         |
| 13 |无需注册         |
| 14 |已吊销          |
| 15 |已从集合中删除        |
| 16 |已验证续订         |
| 17 |安装失败        |
| 18 |已安装         |
| 19 |删除失败         |
| 20 |已删除         |
| 21 |已请求续订        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 | 状态 PIN 设置成功       |
| 2 | 状态 PIN 设置失败       |
| 3 | 不支持状态 PIN 设置      |
| 4 | 正在进行状态 PIN 设置      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

无状态 ID。

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

无状态 ID。

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

无状态 ID。

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

无状态 ID。

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

无状态 ID。

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

无状态 ID。

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |已发出质询    |
| 2 |质询发出失败   |
| 3 |请求创建失败   |
| 4 |请求提交失败   |
| 5 |质询验证成功  |
| 6 |质询验证失败  |
| 7 |发出失败    |
| 8 |问题挂起    |
| 9 |已发出     |
| 10 |响应处理失败  |
| 11 |响应挂起    |
| 12 |注册成功    |
| 13 |无需注册    |
| 14 |已吊销     |
| 15 |已从集合中删除   |
| 16 |已验证续订    |
| 17 |安装失败   |
| 18 |已安装    |
| 19 |删除失败    |
| 20 |已删除    |
| 21 |已请求续订   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
|| 1 | 符合性成功    |
| 2 | MP 符合性失败   |
| 3 | 客户端符合性失败   |
| 4 | Intune 符合性失败   |
| 5 | AAD 符合性失败   |
| 6 | 符合性 comgmt Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |已添加对等缓存源       |
| 2 |已删除对等缓存源      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |已停用对等缓存源       |
| 2 |已启用对等缓存源       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |下载聚合数据上传       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |对等源拒绝数据上传     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

无状态 ID。

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

无状态 ID。

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

无状态 ID。

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

无状态 ID。

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     状态消息 ID     |  状态消息描述 |
|:-------------|:------|
| 1 |支持运行状况证明      |
| 2 |不支持运行状况证明      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

无状态 ID。

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

无状态 ID。

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

无状态 ID。

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

无状态 ID。

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

无状态 ID。

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

无状态 ID。

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

无状态 ID。

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

无状态 ID。

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

无状态 ID。

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

无状态 ID。

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

无状态 ID。

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

无状态 ID。

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

无状态 ID。

## <a name="next-steps"></a>后续步骤

- [Configuration Manager 中的状况消息传递说明](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Configuration Manager 的软件更新管理白皮书](https://www.microsoft.com/download/details.aspx?id=44578)
