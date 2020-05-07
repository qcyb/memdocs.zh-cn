---
title: 客户端事件日志
titleSuffix: Configuration Manager
description: 关于 Windows 事件日志中可能出现的 BitLocker (MBAM) 客户端条目的技术参考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705965"
---
# <a name="client-event-logs"></a>客户端事件日志

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

在部署有 BitLocker 管理策略的 Configuration Manager 客户端上，使用 Windows 事件查看器来查看 BitLocker 客户端事件日志。 对于[“管理”](#admin)和[“操作”](#operational)事件日志，依次转到“应用程序和服务日志”  、“Microsoft”  、“Windows”  和“MBAM”  。

## <a name="admin"></a>管理员

### <a name="2-volumeenactmentfailed"></a>2：VolumeEnactmentFailed

应用 MBAM 策略时发生错误。

#### <a name="error-code--2144272219"></a>错误代码：-2144272219

详细信息:BitLocker 驱动器加密只支持对精简预配的存储使用仅加密已用空间。

如果你尝试使用 BitLocker 对运行 Windows 10 版本 1803 或更低版本的虚拟机进行加密，就会出现此错误。 旧版 Windows 10 不支持全磁盘加密。 BitLocker 管理策略强制执行全磁盘加密。

#### <a name="error-code--2147024774"></a>错误代码：-2147024774

详细信息:传递给系统调用的数据区域太小。

若要解决此问题，重新启动计算机。

### <a name="4-transferstatusdatafailed"></a>4：TransferStatusDataFailed

发送加密状态数据时发生错误。

### <a name="8-systemvolumenotfound"></a>8：SystemVolumeNotFound

缺少系统卷。 对操作系统驱动器进行加密需要 SystemVolume。

### <a name="9-tpmnotfound"></a>9：TPMNotFound

缺少 TPM 硬件。 若要使用 TPM 保护程序对操作系统驱动器进行加密，需要 TPM。

### <a name="10-machinehwexempted"></a>10：MachineHWExempted

计算机已免除加密。 计算机的硬件状态：已豁免

### <a name="11-machinehwunknown"></a>11：MachineHWUnknown

计算机已免除加密。 计算机的硬件状态：Unknown

### <a name="12-hwcheckfailed"></a>12：HWCheckFailed

硬件免除检查失败。

### <a name="13-userisexempted"></a>13：UserIsExempted

用户已免除加密。

### <a name="14-useriswaiting"></a>14：UserIsWaiting

用户请求了免除。

### <a name="15-userexemptioncheckfailed"></a>15：UserExemptionCheckFailed

用户免除检查失败。

### <a name="16-userpostponed"></a>16：UserPostponed

用户推迟了加密过程。

### <a name="17-tpminitializationfailed"></a>17：TPMInitializationFailed

TPM 初始化失败。 用户拒绝了 BIOS 更改。

### <a name="18-coreservicedown"></a>18：CoreServiceDown

无法连接到 MBAM 恢复和硬件服务。

#### <a name="error-code--2147024809"></a>错误代码：-2147024809

详细信息:参数不正确。

如果网站不是 HTTPS，或者客户端没有 PKI 证书，就会出现此错误。

### <a name="20-policymismatch"></a>20：PolicyMismatch

BitLocker 管理策略存在冲突或损坏。

### <a name="21-conflictingosvolumepolicies"></a>21：ConflictingOSVolumePolicies

检测到操作系统卷加密策略冲突。 检查与操作系统驱动器保护程序相关的 BitLocker 策略。

### <a name="22-conflictingfddvolumepolicies"></a>22：ConflictingFDDVolumePolicies

检测到固定数据驱动器卷加密策略冲突。 请检查与固定数据驱动器保护程序相关的 BitLocker 策略。

### <a name="27-encryptionfailednodra"></a>27：EncryptionFailedNoDra

加密时发生错误。 对于 Windows 8.1 之前的计算机，FIPS 模式下需要数据恢复代理 (DRA) 保护程序。

### <a name="34-tpmlockoutresetfailed"></a>34：TpmLockOutResetFailed

无法重置 TPM 锁定。

### <a name="36-tpmownerauthretrievalfailed"></a>36：TpmOwnerAuthRetrievalFailed

无法从 MBAM 服务检索 TPM OwnerAuth。

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37：WmiProviderDllSearchPathUpdateFailed

无法更新 WMI 提供程序的 DLL 搜索路径。

### <a name="38-timedoutwaitingforwmiprovider"></a>38：TimedOutWaitingForWmiProvider

代理正在停止运行。 等待 MBAM WMI 提供程序实例超时。

## <a name="operational"></a>操作

### <a name="1-volumeenactmentsuccessful"></a>1：VolumeEnactmentSuccessful

已成功应用 BitLocker 管理策略。

### <a name="3-transferstatusdatasuccessful"></a>3：TransferStatusDataSuccessful

加密状态数据已成功发送。

### <a name="19-coreserviceup"></a>19：CoreServiceUp

已成功连接到 MBAM 恢复和硬件服务。

### <a name="28-tpmownerauthescrowed"></a>28：TpmOwnerAuthEscrowed

TPM OwnerAuth 已托管。

### <a name="29-recoverykeyescrowed"></a>29：RecoveryKeyEscrowed

卷的 BitLocker 恢复密钥已托管。

### <a name="30-recoverykeyreset"></a>30：RecoveryKeyReset

卷的 BitLocker 恢复密钥已更新。

### <a name="31-enforcepolicydateset"></a>31：EnforcePolicyDateSet

为卷设置了强制执行策略日期

### <a name="32-enforcepolicydatecleared"></a>32：EnforcePolicyDateCleared

为卷清除了强制执行策略日期。

### <a name="33-tpmlockoutresetsucceeded"></a>33：TpmLockOutResetSucceeded

已成功重置 TPM 锁定。

### <a name="35-tpmownerauthretrievalsucceeded"></a>35：TpmOwnerAuthRetrievalSucceeded

已成功从 MBAM 服务检索 TPM OwnerAuth。

### <a name="39-removabledrivemounted"></a>39：RemovableDriveMounted

已装载可移动驱动器。

### <a name="40-removabledrivedismounted"></a>40：RemovableDriveDismounted

已卸载可移动驱动器。

### <a name="41-failedtoenactendpointunreachable"></a>41：FailedToEnactEndpointUnreachable

无法连接到 MBAM 恢复和硬件服务，导致 BitLocker 管理策略无法成功应用到卷。

### <a name="42-failedtoenactlockedvolume"></a>42：FailedToEnactLockedVolume

锁定的卷状态导致 BitLocker 管理策略无法成功应用到卷。

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43：TransferStatusDataFailedEndpointUnreachable

无法连接到 MBAM 符合性和状态服务，导致加密状态数据无法传输。

## <a name="see-also"></a>另请参阅

若要详细了解如何使用这些日志，请参阅 [BitLocker 事件日志](about-event-logs.md)。

若要详细了解如何排除故障，请参阅[排除 BitLocker 故障](troubleshoot.md)。
