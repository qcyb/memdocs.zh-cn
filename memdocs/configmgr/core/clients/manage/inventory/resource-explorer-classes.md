---
title: 资源浏览器默认清单类
titleSuffix: Configuration Manager
description: 显示资源浏览器中显示的类
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690175"
---
# <a name="resource-explorer-default-inventory-classes"></a>资源浏览器默认清单类

适用范围：  Configuration Manager (Current Branch)

本文介绍资源浏览器中的默认清单类。

以下是默认清单类：

## <a name="1394-controller"></a>1394 控制器

命名空间：root\cimv2

Win32_1394Controller 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MaxNumberControlled

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="account-sid"></a>帐户 SID

命名空间：root\cimv2

Win32_AccountSID 类

- (字符串) Element

- (字符串) Setting



## <a name="activesync-service"></a>ActiveSync 服务

命名空间：root\SmsDm

SMS_ActiveSyncService 类


- (UInt32) MajorVersion

- (UInt32) MinorVersion

- (字符串) LastSyncTime



## <a name="amt-agent"></a>AMT 代理

命名空间：root\cimv2\sms

SMS_AMTObject 类


- (UInt32) DeviceID

- (字符串) AMT

- (字符串) AMTApps

- (字符串) BiosVersion

- (字符串) BuildNumber

- (字符串) Flash

- (字符串) LegacyMode

- (字符串) Netstack

- (UInt32) ProvisionMode

- (UInt32) ProvisionState

- (字符串) RecoveryBuildNum

- (字符串) RecoveryVersion

- (字符串) Sku

- (UInt32) TLSMode

- (字符串) VendorID

- (UInt32) ZTCEnabled



## <a name="appv-client-application"></a>AppV 客户端应用程序

命名空间：root\AppV

AppvClientApplication 类


- (字符串) ApplicationId

- (字符串) PackageId

- (字符串) PackageVersionId

- (布尔值) EnabledForUser

- (布尔值) EnabledGlobally

- (字符串) Name

- (字符串) TargetPath

- (字符串) Version



## <a name="appv-client-package"></a>AppV 客户端包

命名空间：root\AppV

AppvClientPackage 类


- (字符串) PackageId

- (字符串) VersionId

- (字符串) Assets[]

- (字符串) DeploymentMachineData

- (字符串) DeploymentUserData

- (布尔值) HasAssetIntelligence

- (布尔值) InUse

- (布尔值) IsPublishedGlobally

- (布尔值) IsPublishedToUser

- (字符串) Name

- (UInt64) PackageSize

- (字符串) Path

- (UInt16) PercentLoaded

- (字符串) UserConfigurationData

- (字符串) Version



## <a name="autostart-software"></a>自动启动软件

命名空间：root\cimv2\sms

SMS_AutoStartSoftware 类


- (字符串) FilePropertiesHash

- (字符串) BinFileVersion

- (字符串) BinProductVersion

- (字符串) Description

- (字符串) FileName

- (字符串) FilePropertiesHashEx

- (字符串) FileVersion

- (字符串) Location

- (字符串) Product

- (字符串) ProductVersion

- (字符串) Publisher

- (字符串) StartupType

- (字符串) StartupValue



## <a name="baseboard"></a>基板

命名空间：root\cimv2

Win32_BaseBoard 类


- (字符串) Tag

- (字符串) Caption

- (字符串) ConfigOptions[]

- (字符串) Description

- (布尔值) HostingBoard

- (布尔值) HotSwappable

- (日期/时间) InstallDate

- (字符串) Manufacturer

- (字符串) Model

- (字符串) Name

- (字符串) OtherIdentifyingInfo

- (字符串) PartNumber

- (布尔值) PoweredOn

- (字符串) Product

- (布尔值) Removable

- (布尔值) Replaceable

- (字符串) RequirementsDescription

- (布尔值) RequiresDaughterBoard

- (字符串) SerialNumber

- (字符串) SKU

- (字符串) SlotLayout

- (布尔值) SpecialRequirements

- (字符串) Status

- (字符串) Version



## <a name="battery"></a>电池

命名空间：root\cimv2

Win32_Battery 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt16) BatteryStatus

- (字符串) Caption

- (UInt16) Chemistry

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt32) DesignCapacity

- (UInt64) DesignVoltage

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) ExpectedLife

- (UInt32) FullChargeCapacity

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxRechargeTime

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) SmartBatteryVersion

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (UInt32) TimeOnBattery

- (UInt32) TimeToFullCharge



## <a name="bitlocker"></a>BitLocker

命名空间：root\cimv2\security\MicrosoftVolumeEncryption

Win32_EncryptableVolume 类


- (字符串) DeviceID

- (字符串) DriveLetter

- (字符串) PersistentVolumeID

- (UInt32) ProtectionStatus



## <a name="bitlocker-encryption-details"></a>BitLocker Encryption Details

命名空间：root\cimv2

Win32_BitLockerEncryptionDetails 类


- (字符串) BitlockerPersistentVolumeId

- (SInt32) Compliant

- (SInt32) ConversionStatus

- (字符串) DeviceId

- (字符串) DriveLetter

- (SInt32) EncryptionMethod

- (字符串) EnforcePolicyDate

- (布尔值) IsAutoUnlockEnabled

- (SInt32) KeyProtectorTypes[]

- (字符串) MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- (字符串) NoncomplianceDetectedDate

- (SInt32) ProtectionStatus

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>BitLocker 策略

命名空间：root\cimv2

Win32Reg_MBAMPolicy 类


- (字符串) EncodedComputerName

- (UInt32) EncryptionMethod

- (UInt32) FixedDataDriveAutoUnlock

- (UInt32) FixedDataDriveEncryption

- (UInt32) FixedDataDrivePassphrase

- (字符串) KeyName

- (字符串) LastConsoleUser

- (UInt32) MBAMMachineError

- (UInt32) MBAMPolicyEnforced

- (UInt32) OsDriveEncryption

- (UInt32) OsDriveProtector

- (日期/时间) UserExemptionDate



## <a name="boot-configuration"></a>启动配置

命名空间：root\cimv2

Win32_BootConfiguration 类


- (字符串) Name

- (字符串) BootDirectory

- (字符串) ConfigurationPath

- (字符串) Description

- (字符串) LastDrive

- (字符串) ScratchDirectory

- (字符串) SettingID

- (字符串) TempDirectory



## <a name="browser-helper-object"></a>浏览器帮助程序对象

命名空间：root\cimv2\sms

SMS_BrowserHelperObject 类


- (字符串) FilePropertiesHash

- (字符串) BinFileVersion

- (字符串) BinProductVersion

- (字符串) CLSID

- (字符串) Description

- (字符串) FileName

- (字符串) FilePropertiesHashEx

- (字符串) FileVersion

- (字符串) Product

- (字符串) ProductVersion

- (字符串) Publisher

- (字符串) Version



## <a name="ccm_rax"></a>CCM_RAX

命名空间：root\ccm\cimodels

CCM_RAXInfo 类


- (字符串) AppID

- (字符串) FeedURL

- (字符串) UserSID



## <a name="cd-rom"></a>CD-ROM

命名空间：root\cimv2

Win32_CDROMDrive 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (字符串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字符串) Description

- (字符串) Drive

- (布尔值) DriveIntegrity

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (UInt16) FileSystemFlags

- (UInt32) FileSystemFlagsEx

- (字符串) ID

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt32) MaximumComponentLength

- (UInt64) MaxMediaSize

- (布尔值) MediaLoaded

- (字符串) MediaType

- (UInt64) MinBlockSize

- (字符串) Name

- (布尔值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) RevisionLevel

- (UInt32) SCSIBus

- (UInt16) SCSILogicalUnit

- (UInt16) SCSIPort

- (UInt16) SCSITargetId

- (UInt64) Size

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (字符串) VolumeName

- (字符串) VolumeSerialNumber



## <a name="client-events"></a>客户端事件

命名空间：root\ccm\invagt

ClientEvents 类


- (字符串) EventName

- (UInt16) Count



## <a name="computer-system"></a>计算机系统

命名空间：root\cimv2

Win32_ComputerSystem 类


- (字符串) Name

- (UInt16) AdminPasswordStatus

- (布尔值) AutomaticResetBootOption

- (布尔值) AutomaticResetCapability

- (UInt16) BootOptionOnLimit

- (UInt16) BootOptionOnWatchDog

- (布尔值) BootROMSupported

- (字符串) BootupState

- (字符串) Caption

- (UInt16) ChassisBootupState

- (SInt16) CurrentTimeZone

- (布尔值) DaylightInEffect

- (字符串) Description

- (字符串) Domain

- (UInt16) DomainRole

- (UInt16) FrontPanelResetStatus

- (布尔值) InfraredSupported

- (字符串) InitialLoadInfo[]

- (日期/时间) InstallDate

- (UInt16) KeyboardPasswordStatus

- (字符串) LastLoadInfo

- (字符串) Manufacturer

- (字符串) Model

- (字符串) NameFormat

- (布尔值) NetworkServerModeEnabled

- (UInt32) NumberOfProcessors

- (字符串) OEMLogoBitmap

- (字符串) OEMStringArray[]

- (SInt64) PauseAfterReset

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) PowerOnPasswordStatus

- (UInt16) PowerState

- (UInt16) PowerSupplyState

- (字符串) PrimaryOwnerContact

- (字符串) PrimaryOwnerName

- (UInt16) ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- (字符串) Roles[]

- (字符串) Status

- (字符串) SupportContactDescription[]

- (UInt16) SystemStartupDelay

- (字符串) SystemStartupOptions[]

- (UInt8) SystemStartupSetting

- (字符串) SystemType

- (UInt16) ThermalState

- (UInt64) TotalPhysicalMemory

- (字符串) UserName

- (UInt16) WakeUpType



## <a name="computer-system-ex"></a>计算机系统扩展

命名空间：root\cimv2

CCM_ComputerSystemExtended 类


- (字符串) Name

- (UInt16) PCSystemType



## <a name="computer-system-product"></a>计算机系统产品

命名空间：root\cimv2

Win32_ComputerSystemProduct 类


- (字符串) IdentifyingNumber

- (字符串) Name

- (字符串) Version

- (字符串) Caption

- (字符串) Description

- (字符串) SKUNumber

- (字符串) UUID

- (字符串) Vendor



## <a name="sms-advanced-client-ports"></a>SMS 高级客户端端口

命名空间：root\cimv2

Win32Reg_SMSAdvancedClientPorts 类


- (字符串) InstanceKey

- (UInt32) HttpsPortName

- (UInt32) PortName



## <a name="sms-advanced-client-ssl-configurations"></a>SMS 高级客户端 SSL 配置

命名空间：root\cimv2

Win32Reg_SMSAdvancedClientSSLConfiguration 类


- (字符串) InstanceKey

- (字符串) CertificateSelectionCriteria

- (字符串) CertificateStore

- (UInt32) ClientAlwaysOnInternet

- (UInt32) HttpsStateFlags

- (字符串) InternetMPHostName

- (UInt32) SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>SMS 高级客户端状态

命名空间：root\ccm

CCM_InstalledComponent 类


- (字符串) Name

- (字符串) DisplayName

- (字符串) Version



## <a name="connected-device"></a>已连接的设备

命名空间：root\SmsDm

SMS_ActiveSyncConnectedDevice 类


- (字符串) DeviceOEMInfo

- (字符串) DeviceType

- (字符串) OS_Major

- (字符串) OS_Minor

- (字符串) OS_Platform

- (字符串) ProcessorArchitecture

- (字符串) ProcessorLevel

- (字符串) ProcessorRevision

- (字符串) InstalledClientID

- (字符串) InstalledClientServer

- (字符串) InstalledClientVersion

- (字符串) LastSyncTime

- (字符串) OS_AdditionalInfo

- (字符串) OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

命名空间：root\cimv2\sms

SMS_DefaultBrowser 类


- (字符串) BrowserProgId



## <a name="desktop"></a>“桌面”

命名空间：root\cimv2

Win32_Desktop 类


- (字符串) Name

- (UInt32) BorderWidth

- (字符串) Caption

- (布尔值) CoolSwitch

- (UInt32) CursorBlinkRate

- (字符串) Description

- (布尔值) DragFullWindows

- (UInt32) GridGranularity

- (UInt32) IconSpacing

- (字符串) IconTitleFaceName

- (UInt32) IconTitleSize

- (布尔值) IconTitleWrap

- (字符串) Pattern

- (布尔值) ScreenSaverActive

- (字符串) ScreenSaverExecutable

- (布尔值) ScreenSaverSecure

- (UInt32) ScreenSaverTimeout

- (字符串) SettingID

- (字符串) Wallpaper

- (布尔值) WallpaperStretched

- (布尔值) WallpaperTiled



## <a name="desktop-monitor"></a>桌面监视器

命名空间：root\cimv2

Win32_DesktopMonitor 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt32) Bandwidth

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt16) DisplayType

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (布尔值) IsLocked

- (UInt32) LastErrorCode

- (字符串) MonitorManufacturer

- (字符串) MonitorType

- (字符串) Name

- (UInt32) PixelsPerXLogicalInch

- (UInt32) PixelsPerYLogicalInch

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt32) ScreenHeight

- (UInt32) ScreenWidth

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName



## <a name="device-info"></a>设备信息

命名空间：保留

Device_Info 类


- (字符串) CertExpiry

- (字符串) DeviceName

- (字符串) Manufacturer

- (字符串) Model

- (字符串) OS



## <a name="mdm-devdetail"></a>MDM DevDetail

命名空间：root\cimv2\mdm\dmmap

MDM_DevDetail_Ext01 类


- (字符串) InstanceID

- (字符串) ParentID

- (字符串) DeviceHardwareData

- (字符串) WLANMACAddress



## <a name="disk"></a>磁盘和分区

命名空间：root\cimv2

Win32_DiskDrive 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt32) BytesPerSector

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (字符串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (UInt32) Index

- (日期/时间) InstallDate

- (字符串) InterfaceType

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt64) MaxMediaSize

- (布尔值) MediaLoaded

- (字符串) MediaType

- (UInt64) MinBlockSize

- (字符串) Model

- (字符串) Name

- (布尔值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (UInt32) Partitions

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt32) SCSIBus

- (UInt16) SCSILogicalUnit

- (UInt16) SCSIPort

- (UInt16) SCSITargetId

- (UInt32) SectorsPerTrack

- (UInt64) Size

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (UInt64) TotalCylinders

- (UInt32) TotalHeads

- (UInt64) TotalSectors

- (UInt64) TotalTracks

- (UInt32) TracksPerCylinder



## <a name="partition"></a>分区

命名空间：root\cimv2

Win32_DiskPartition 类


- (字符串) DeviceID

- (UInt16) Access

- (UInt16) Availability

- (UInt64) BlockSize

- (布尔值) Bootable

- (布尔值) BootPartition

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt32) DiskIndex

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (UInt32) HiddenSectors

- (UInt32) Index

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Name

- (UInt64) NumberOfBlocks

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (布尔值) PrimaryPartition

- (字符串) Purpose

- (布尔值) RewritePartition

- (UInt64) Size

- (UInt64) StartingOffset

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (字符串) Type



## <a name="dma"></a>DMA

命名空间：root\cimv2

Win32_DeviceMemoryAddress 类

- (UInt64) StartingAddress

- (字符串) Caption

- (字符串) Description

- (UInt64) EndingAddress

- (日期/时间) InstallDate

- (字符串) MemoryType

- (字符串) Name

- (字符串) Status



## <a name="dma-channel"></a>DMA 通道

命名空间：root\cimv2

Win32_DMAChannel 类


- (UInt32) DMAChannel

- (UInt16) AddressSize

- (UInt16) Availability

- (布尔值) BurstMode

- (UInt16) ByteMode

- (字符串) Caption

- (UInt16) ChannelTiming

- (字符串) Description

- (日期/时间) InstallDate

- (UInt32) MaxTransferSize

- (字符串) Name

- (UInt32) Port

- (字符串) Status

- (UInt16) TransferWidths[]

- (UInt16) TypeCTiming

- (UInt16) WordMode



## <a name="driver---vxd"></a>驱动程序 - VxD

命名空间：root\cimv2

Win32_DriverVXD 类


- (字符串) Name

- (字符串) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) TargetOperatingSystem

- (字符串) Version

- (字符串) BuildNumber

- (字符串) Caption

- (字符串) CodeSet

- (字符串) Control

- (字符串) Description

- (字符串) DeviceDescriptorBlock

- (字符串) IdentificationCode

- (日期/时间) InstallDate

- (字符串) LanguageEdition

- (字符串) Manufacturer

- (字符串) OtherTargetOS

- (字符串) PM_API

- (字符串) SerialNumber

- (UInt32) ServiceTableSize

- (字符串) Status

- (字符串) V86_API



## <a name="embedded-device-information"></a>嵌入式设备信息

命名空间：root\cimv2\sms

CCM_EmbeddedDeviceInformation 类


- (字符串) DeviceType

- (字符串) Model

- (字符串) OEMName



## <a name="environment"></a>环境

命名空间：root\cimv2

Win32_Environment 类


- (字符串) Name

- (字符串) UserName

- (字符串) Caption

- (字符串) Description

- (日期/时间) InstallDate

- (字符串) Status

- (布尔值) SystemVariable

- (字符串) VariableValue



## <a name="firmware"></a>固件

命名空间：root\cimv2\sms

SMS_Firmware 类


- (布尔值) UEFI

- (布尔值) SecureBoot



## <a name="usm-folder-redirection-health"></a>USM 文件夹重定向运行状况

命名空间：root\cimv2\sms

SMS_FolderRedirectionHealth 类


- (字符串) FolderName

- (字符串) SID

- (UInt8) HealthStatus

- (日期/时间) LastSuccessfulSyncTime

- (UInt8) LastSyncStatus

- (日期/时间) LastSyncTime

- (布尔值) OfflineAccessEnabled

- (字符串) OfflineFileNameFolderGUID

- (布尔值) Redirected



## <a name="ide-controller"></a>IDE 控制器

命名空间：root\cimv2

Win32_IDEController 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MaxNumberControlled

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="add-remove-programs-64"></a>添加/删除程序(64)

命名空间：root\cimv2

Win32Reg_AddRemovePrograms64 类


- (字符串) ProdID

- (字符串) DisplayName

- (字符串) InstallDate

- (字符串) Publisher

- (字符串) Version



## <a name="add-remove-programs"></a>添加/删除程序

命名空间：root\cimv2

Win32Reg_AddRemovePrograms 类


- (字符串) ProdID

- (字符串) DisplayName

- (字符串) InstallDate

- (字符串) Publisher

- (字符串) Version



## <a name="installed-executable"></a>已安装可执行文件

命名空间：root\cimv2\sms

SMS_InstalledExecutable 类


- (字符串) ExecutableName

- (字符串) ProductCode

- (字符串) BinFileVersion

- (字符串) BinProductVersion

- (字符串) Description

- (字符串) FilePropertiesHash

- (字符串) FilePropertiesHashEx

- (UInt32) FileSize

- (字符串) FileVersion

- (布尔值) HasPatchAdded

- (字符串) InstalledFilePath

- (布尔值) IsSystemFile

- (布尔值) IsVitalFile

- (UInt32) Language

- (字符串) Product

- (字符串) ProductVersion

- (字符串) Publisher



## <a name="installed-software"></a>已安装的软件

命名空间：root\cimv2\sms

SMS_InstalledSoftware 类


- (字符串) SoftwareCode

- (字符串) ARPDisplayName

- (字符串) ChannelCode

- (字符串) ChannelID

- (字符串) CM_DSLID

- (字符串) EvidenceSource

- (日期/时间) InstallDate

- (UInt32) InstallDirectoryValidation

- (字符串) InstalledLocation

- (字符串) InstallSource

- (UInt32) InstallType

- (UInt32) Language

- (字符串) LocalPackage

- (字符串) MPC

- (UInt32) OsComponent

- (字符串) PackageCode

- (字符串) ProductID

- (字符串) ProductName

- (字符串) ProductVersion

- (字符串) Publisher

- (字符串) RegisteredUser

- (字符串) ServicePack

- (字符串) SoftwarePropertiesHash

- (字符串) SoftwarePropertiesHashEx

- (字符串) UninstallString

- (字符串) UpgradeCode

- (UInt32) VersionMajor

- (UInt32) VersionMinor



## <a name="irq-table"></a>IRQ 表

命名空间：root\cimv2

Win32_IRQResource 类


- (UInt32) IRQNumber

- (UInt16) Availability

- (字符串) Caption

- (字符串) Description

- (布尔值) Hardware

- (日期/时间) InstallDate

- (字符串) Name

- (布尔值) Shareable

- (字符串) Status

- (UInt16) TriggerLevel

- (UInt16) TriggerType

- (UInt32) Vector



## <a name="keyboard"></a>键盘

命名空间：root\cimv2

Win32_Keyboard 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (布尔值) IsLocked

- (UInt32) LastErrorCode

- (字符串) Layout

- (字符串) Name

- (UInt16) NumberOfFunctionKeys

- (UInt16) Password

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName



## <a name="load-order-group"></a>加载顺序组

命名空间：root\cimv2

Win32_LoadOrderGroup 类


- (字符串) Name

- (字符串) Caption

- (字符串) Description

- (布尔值) DriverEnabled

- (UInt32) GroupOrder

- (日期/时间) InstallDate

- (字符串) Status



## <a name="logical-disk"></a>逻辑磁盘

命名空间：root\cimv2\sms

SMS_LogicalDisk 类


- (字符串) DeviceID

- (UInt16) Access

- (UInt16) Availability

- (UInt64) BlockSize

- (字符串) Caption

- (布尔值) Compressed

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt32) DriveType

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (字符串) FileSystem

- (UInt64) FreeSpace

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaximumComponentLength

- (UInt32) MediaType

- (字符串) Name

- (UInt64) NumberOfBlocks

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) ProviderName

- (字符串) Purpose

- (UInt64) Size

- (字符串) Status

- (UInt16) StatusInfo

- (布尔值) SupportsFileBasedCompression

- (字符串) SystemName

- (字符串) VolumeName

- (字符串) VolumeSerialNumber



## <a name="memory"></a>内存

命名空间：root\cimv2

CCM_LogicalMemoryConfiguration 类


- (字符串) Name

- (UInt64) AvailableVirtualMemory

- (UInt64) TotalPageFileSpace

- (UInt64) TotalPhysicalMemory

- (UInt64) TotalVirtualMemory



## <a name="device-bluetooth"></a>设备蓝牙

命名空间：保留

Device_Bluetooth 类


- (布尔值) Enabled



## <a name="device-camera"></a>设备相机

命名空间：保留

Device_Camera 类


- (布尔值) Enabled



## <a name="device-certificates"></a>设备证书

命名空间：保留

Device_Certificates 类


- (字符串) Thumbprint

- (字符串) Type

- (字符串) IssuedBy

- (字符串) IssuedTo

- (日期/时间) ValidFrom

- (日期/时间) ValidTo



## <a name="device-client"></a>设备客户端

命名空间：保留

Device_Client 类


- (布尔值) DownloadWhenRoaming

- (布尔值) SyncWhenRoaming



## <a name="device-client-agent-version"></a>设备客户端代理版本

命名空间：保留

Device_ClientAgentVersion 类


- (字符串) Version



## <a name="device-computer-system"></a>设备计算机系统

命名空间：保留

Device_ComputerSystem 类


- (字符串) CellularTechnology

- (字符串) DeviceClientID

- (字符串) DeviceManufacturer

- (字符串) DeviceModel

- (字符串) DMVersion

- (字符串) FirmwareVersion

- (字符串) HardwareVersion

- (字符串) IMEI

- (字符串) IMSI

- (UInt8) IsActivationLockEnabled

- (UInt8) Jailbroken

- (字符串) MEID

- (字符串) OEM

- (字符串) PhoneNumber

- (字符串) PlatformType

- (UInt32) ProcessorArchitecture

- (UInt32) ProcessorLevel

- (UInt32) ProcessorRevision

- (字符串) Product

- (字符串) ProductVersion

- (字符串) SerialNumber

- (字符串) SoftwareVersion

- (字符串) SubscriberCarrierNetwork



## <a name="device-display"></a>设备显示

命名空间：保留

Device_Display 类


- (UInt32) HorizontalResolution

- (UInt64) NumberOfColors

- (UInt32) VerticalResolution



## <a name="device-email"></a>设备电子邮件

命名空间：保留

Device_Email 类


- (字符串) OwnerEmailAddress

- (字符串) SyncDomain

- (字符串) SyncServer

- (字符串) SyncUser

- (字符串) Type



## <a name="device-encryption"></a>设备加密

命名空间：保留

Device_Encryption 类


- (UInt32) EmailEncryptionAlgorithm

- (UInt32) EmailEncryptionNegotiation

- (布尔值) EmailEncryptionRequired

- (布尔值) EmailSigningAlgorithm

- (布尔值) EmailSigningRequired

- (布尔值) EncryptionCompliance

- (布尔值) PhoneMemoryEncrypted

- (布尔值) StorageCardEncrypted



## <a name="device-exchange"></a>设备 Exchange

命名空间：保留

Device_Exchange 类


- (布尔值) ConflictResolution

- (SInt32) HTMLEmailTruncation

- (UInt32) MailFormat

- (UInt32) MaxCalendarAge

- (UInt32) MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- (UInt32) OffPeakSyncFrequency

- (UInt32) PeakDays

- (字符串) PeakEndTime

- (字符串) PeakStartTime

- (UInt32) PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- (布尔值) SendEmailImmediately

- (布尔值) SyncCalendar

- (布尔值) SyncContacts

- (布尔值) SyncEmail

- (布尔值) SyncTasks

- (布尔值) SyncWhenRoaming



## <a name="device-installed-applications"></a>设备已安装应用程序

命名空间：保留

Device_InstalledApplications 类


- (字符串) Name

- (字符串) Version



## <a name="device-irda"></a>设备 IrDA

命名空间：保留

Device_IrDA 类


- (布尔值) Enabled



## <a name="mobile-device-location"></a>移动设备位置

命名空间：保留

MDM_RemoteFind 类


- (Real32) Latitude

- (Real32) Longitude



## <a name="device-memory"></a>设备内存

命名空间：保留

Device_Memory 类


- (UInt64) ProgramFree

- (UInt64) ProgramTotal

- UInt64RemovableStorageFree

- (UInt64) RemovableStorageTotal

- (UInt64) StorageFree

- (UInt64) StorageTotal



## <a name="device-os-information"></a>设备 OS 信息

命名空间：保留

Device_OSInformation 类


- (字符串) Language

- (字符串) Platform

- (字符串) Version



## <a name="device-password"></a>设备密码

命名空间：保留

Device_Password 类


- (布尔值) AllowRecoveryPassword

- (UInt32) AutolockTimeout

- (布尔值) Enabled

- (UInt32) Expiration

- (UInt32) History

- (UInt32) MaxAttemptsBeforeWipe

- (UInt32) MinComplexChars

- (UInt32) MinLength

- (UInt8) PasswordQuality

- (UInt32) Type



## <a name="device-policy"></a>设备策略

命名空间：保留

Device_Policy 类


- (字符串) Name

- (布尔值) Enforced



## <a name="device-power"></a>设备电源

命名空间：保留

Device_Power 类


- (UInt32) BacklightACTimeout

- (UInt32) BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) BatteryPercent



## <a name="mobile-device-security-status"></a>移动设备安全状态

命名空间：保留

MDM_SecurityStatus 类


- (UInt32) HardwareEncryptionCaps

- (UInt8) PasscodeCompliant

- (UInt8) PasscodeCompliantWithProfiles

- (UInt8) PasscodePresent

- (UInt8) RequireEncryption



## <a name="device-windows-security-policy"></a>设备 Windows 安全策略

命名空间：保留

Device_WindowsSecurityPolicy 类


- (UInt32) ID

- (字符串) Name

- (UInt32) Value



## <a name="device-wlan"></a>设备 WLAN

命名空间：保留

Device_WLAN 类


- (布尔值) Enabled

- (字符串) EthernetMAC

- (字符串) WiFiMAC



## <a name="modem"></a>调制解调器

命名空间：root\cimv2

Win32_POTSModem 类


- (字符串) DeviceID

- (UInt16) AnswerMode

- (字符串) AttachedTo

- (UInt16) Availability

- (字符串) BlindOff

- (字符串) BlindOn

- (字符串) Caption

- (字符串) CompatibilityFlags

- (UInt16) CompressionInfo

- (字符串) CompressionOff

- (字符串) CompressionOn

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) ConfigurationDialog

- (字符串) CountriesSupported[]

- (字符串) CountrySelected

- (字符串) CurrentPasswords[]

- (字符串) DCB

- (字符串) Default

- (字符串) Description

- (字符串) DeviceLoader

- (字符串) DeviceType

- (UInt16) DialType

- (日期/时间) DriverDate

- (布尔值) ErrorCleared

- (字符串) ErrorControlForced

- (UInt16) ErrorControlInfo

- (字符串) ErrorControlOff

- (字符串) ErrorControlOn

- (字符串) ErrorDescription

- (字符串) FlowControlHard

- (字符串) FlowControlOff

- (字符串) FlowControlSoft

- (字符串) InactivityScale

- (UInt32) InactivityTimeout

- (UInt32) Index

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxBaudRateToPhone

- (UInt32) MaxBaudRateToSerialPort

- (UInt16) MaxNumberOfPasswords

- (字符串) Model

- (字符串) ModemInfPath

- (字符串) ModemInfSection

- (字符串) ModulationBell

- (字符串) ModulationCCITT

- (UInt16) ModulationScheme

- (字符串) Name

- (字符串) PNPDeviceID

- (字符串) PortSubClass

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) Prefix

- (字符串) Properties

- (字符串) ProviderName

- (字符串) Pulse

- (字符串) Reset

- (字符串) ResponsesKeyName

- (UInt8) RingsBeforeAnswer

- (字符串) SpeakerModeDial

- (字符串) SpeakerModeOff

- (字符串) SpeakerModeOn

- (字符串) SpeakerModeSetup

- (字符串) SpeakerVolumeHigh

- (UInt16) SpeakerVolumeInfo

- (字符串) SpeakerVolumeLow

- (字符串) SpeakerVolumeMed

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) StringFormat

- (布尔值) SupportsCallback

- (布尔值) SupportsSynchronousConnect

- (字符串) SystemName

- (字符串) Terminator

- (日期/时间) TimeOfLastReset

- (字符串) Tone

- (字符串) VoiceSwitchFeature



## <a name="motherboard"></a>母板

命名空间：root\cimv2

Win32_MotherboardDevice 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) PrimaryBusType

- (字符串) RevisionNumber

- (字符串) SecondaryBusType

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName


## <a name="nap-client"></a>NAP 客户端

命名空间：root\Nap

NAP_Client 类


- (字符串) name

- (字符串) description

- (字符串) fixupURL

- (布尔值) napEnabled

- (字符串) napProtocolVersion

- (字符串) probationTime

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>NAP系统健康代理

命名空间：root\Nap

NAP_SystemHealthAgent 类


- (UInt32) ID

- (字符串) description

- (UInt32) fixupState

- (字符串) friendlyName

- (字符串) infoClsid

- (布尔值) isBound

- (UInt8) percentage

- (字符串) registrationDate

- (字符串) vendorName

- (字符串) version



## <a name="network-adapter"></a>网络适配器

命名空间：root\cimv2

Win32_NetworkAdapter 类


- (字符串) DeviceID

- (字符串) AdapterType

- (布尔值) AutoSense

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt32) Index

- (日期/时间) InstallDate

- (布尔值) Installed

- (UInt32) LastErrorCode

- (字符串) MACAddress

- (字符串) Manufacturer

- (UInt32) MaxNumberControlled

- (UInt64) MaxSpeed

- (字符串) Name

- (字符串) NetworkAddresses[]

- (字符串) PermanentAddress

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) ProductName

- (字符串) ServiceName

- (UInt64) Speed

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="network-adapter-configuration"></a>网络适配器配置

命名空间：root\cimv2

Win32_NetworkAdapterConfiguration 类


- (UInt32) Index

- (布尔值) ArpAlwaysSourceRoute

- (布尔值) ArpUseEtherSNAP

- (字符串) Caption

- (字符串) DatabasePath

- (布尔值) DeadGWDetectEnabled

- (字符串) DefaultIPGateway[]

- (UInt8) DefaultTOS

- (UInt8) DefaultTTL

- (字符串) Description

- (布尔值) DHCPEnabled

- (日期/时间) DHCPLeaseExpires

- (日期/时间) DHCPLeaseObtained

- (字符串) DHCPServer

- (字符串) DNSDomain

- (字符串) DNSDomainSuffixSearchOrder[]

- (布尔值) DNSEnabledForWINSResolution

- (字符串) DNSHostName

- (字符串) DNSServerSearchOrder[]

- (布尔值) DomainDNSRegistrationEnabled

- (UInt32) ForwardBufferMemory

- (布尔值) FullDNSRegistrationEnabled

- (UInt16) GatewayCostMetric[]

- (UInt8) IGMPLevel

- (字符串) IPAddress[]

- (UInt32) IPConnectionMetric

- (布尔值) IPEnabled

- (布尔值) IPFilterSecurityEnabled

- (布尔值) IPPortSecurityEnabled

- (字符串) IPSecPermitIPProtocols[]

- (字符串) IPSecPermitTCPPorts[]

- (字符串) IPSecPermitUDPPorts[]

- (字符串) IPSubnet[]

- (布尔值) IPUseZeroBroadcast

- (字符串) IPXAddress

- (布尔值) IPXEnabled

- (字符串) IPXFrameType

- (UInt32) IPXMediaType

- (字符串) IPXNetworkNumber[]

- (字符串) IPXVirtualNetNumber

- (UInt32) KeepAliveInterval

- (UInt32) KeepAliveTime

- (字符串) MACAddress

- (UInt32) MTU

- (UInt32) NumForwardPackets

- (布尔值) PMTUBHDetectEnabled

- (布尔值) PMTUDiscoveryEnabled

- (字符串) ServiceName

- (字符串) SettingID

- (UInt32) TcpipNetbiosOptions

- (UInt32) TcpMaxConnectRetransmissions

- (UInt32) TcpMaxDataRetransmissions

- (UInt32) TcpNumConnections

- (布尔值) TcpUseRFC1122UrgentPointer

- (UInt16) TcpWindowSize

- (布尔值) WINSEnableLMHostsLookup

- (字符串) WINSHostLookupFile

- (字符串) WINSPrimaryServer

- (字符串) WINSScopeID

- (字符串) WINSSecondaryServer



## <a name="network-client"></a>网络客户端

命名空间：root\cimv2

Win32_NetworkClient 类


- (字符串) Name

- (字符串) Caption

- (字符串) Description

- (日期/时间) InstallDate

- (字符串) Manufacturer

- (字符串) Status



## <a name="network-login-profile"></a>网络登录配置文件

命名空间：root\cimv2

Win32_NetworkLoginProfile 类


- (字符串) Name

- (日期/时间) AccountExpires

- (UInt32) AuthorizationFlags

- (UInt32) BadPasswordCount

- (字符串) Caption

- (UInt32) CodePage

- (字符串) Comment

- (UInt32) CountryCode

- (字符串) Description

- (UInt32) Flags

- (字符串) FullName

- (字符串) HomeDirectory

- (字符串) HomeDirectoryDrive

- (日期/时间) LastLogoff

- (日期/时间) LastLogon

- (字符串) LogonHours

- (字符串) LogonServer

- (UInt64) MaximumStorage

- (UInt32) NumberOfLogons

- (字符串) Parameters

- (日期/时间) PasswordAge

- (日期/时间) PasswordExpires

- (UInt32) PrimaryGroupId

- (UInt32) Privileges

- (字符串) Profile

- (字符串) ScriptPath

- (字符串) SettingID

- (UInt32) UnitsPerWeek

- (字符串) UserComment

- (UInt32) UserId

- (字符串) UserType

- (字符串) Workstations



## <a name="nt-eventlog-file"></a>NT 事件日志文件

命名空间：root\cimv2

Win32_NTEventlogFile 类


- (字符串) Name

- (UInt32) AccessMask

- (布尔值) Archive

- (字符串) Caption

- (布尔值) Compressed

- (字符串) CompressionMethod

- (日期/时间) CreationDate

- (字符串) Description

- (字符串) Drive

- (字符串) EightDotThreeFileName

- (布尔值) Encrypted

- (字符串) EncryptionMethod

- (字符串) Extension

- (字符串) FileName

- (UInt64) FileSize

- (字符串) FileType

- (字符串) FSName

- (布尔值) Hidden

- (日期/时间) InstallDate

- (UInt64) InUseCount

- (日期/时间) LastAccessed

- (日期/时间) LastModified

- (字符串) LogfileName

- (字符串) Manufacturer

- (UInt32) MaxFileSize

- (UInt32) NumberOfRecords

- (UInt32) OverwriteOutDated

- (字符串) OverWritePolicy

- (字符串) Path

- (布尔值) Readable

- (字符串) Sources[]

- (字符串) Status

- (布尔值) System

- (字符串) Version

- (布尔值) Writeable



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

命名空间：root\cimv2

Office365ProPlusConfigurations 类


- (字符串) KeyName

- (字符串) AutoUpgrade

- (字符串) CCMManaged

- (字符串) CDNBaseUrl

- (字符串) cfgUpdateChannel

- (字符串) ClientCulture

- (字符串) ClientFolder

- (字符串) GPOChannel

- (字符串) GPOOfficeMgmtCOM

- (字符串) InstallationPath

- (字符串) LastScenario

- (字符串) LastScenarioResult

- (字符串) OfficeMgmtCOM

- (字符串) Platform

- (字符串) SharedComputerLicensing

- (字符串) UpdateChannel

- (字符串) UpdatePath

- (字符串) UpdatesEnabled

- (字符串) UpdateUrl

- (字符串) VersionToReport



## <a name="office-addin"></a>Office 加载项

命名空间：root\ccm\InvAgt

CCM_OfficeAddin 类


- (字符串) Architecture

- (字符串) ID

- (字符串) OfficeApp

- (字符串) Type

- (UInt32) AverageLoadTimeInMilliseconds

- (字符串) CLSID

- (字符串) CompanyName

- (UInt32) CrashCount

- (字符串) Description

- (UInt32) ErrorCount

- (字符串) FileName

- (UInt64) FileSize

- (UInt32) FileTimestamp

- (字符串) FileVersion

- (字符串) FriendlyName

- (字符串) FriendlyNameHash

- (字符串) IdHash

- (UInt32) LoadBehavior

- (UInt32) LoadCount

- (UInt32) LoadFailCount

- (字符串) ProductName

- (字符串) ProductVersion



## <a name="office-client-metric"></a>Office 客户端指标

命名空间：root\ccm\InvAgt

CCM_OfficeClientMetric 类


- (字符串) OfficeApp

- (UInt32) CompatibilityErrorCount

- (UInt32) CrashedSessionCount

- (UInt32) MacroCompileErrorCount

- (UInt32) MacroRuntimeErrorCount

- (UInt32) SessionCount



## <a name="office-device-summary"></a>Office 设备摘要

命名空间：root\ccm\InvAgt

CCM_OfficeDeviceSummary 类


- (布尔值) IsProPlusInstalled

- (布尔值) IsTelemetryEnabled



## <a name="office-document-metric"></a>Office 文档指标

命名空间：root\ccm\InvAgt

CCM_OfficeDocumentMetric 类


- (字符串) OfficeApp

- (UInt32) TotalCloudDocs

- (UInt32) TotalLegacyDocs

- (UInt32) TotalLocalDocs

- (UInt32) TotalMacroDocs

- (UInt32) TotalNonMacroDocs

- (UInt32) TotalUncDocs



## <a name="office-document-solution"></a>Office 文档解决方案

命名空间：root\ccm\InvAgt

CCM_OfficeDocumentSolution 类


- (字符串) DocumentSolutionId

- (字符串) OfficeApp

- (UInt32) CompatibilityErrorCount

- (UInt32) CrashCount

- (字符串) ExampleFileName

- (UInt32) LoadCount

- (UInt32) LoadFailCount

- (UInt32) MacroCompileErrorCount

- (UInt32) MacroRuntimeErrorCount

- (字符串) Type



## <a name="office-macro-error"></a>Office 宏错误

命名空间：root\ccm\InvAgt

CCM_OfficeMacroError 类


- (字符串) DocumentSolutionId

- (UInt32) ErrorCode

- (UInt32) Count

- (UInt64) LastOccurrence

- (字符串) Type



## <a name="office-product-info"></a>Office 产品信息

命名空间：root\ccm\InvAgt

CCM_OfficeProductInfo 类


- (字符串) ProductName

- (字符串) ProductVersion

- (字符串) Architecture

- (字符串) Channel

- (UInt32) IsProPlusInstalled

- (字符串) Language

- (字符串) LicenseState



## <a name="office-vba-rule-violation"></a>Office Vba 规则冲突

命名空间：root\ccm\InvAgt

CCM_OfficeVbaRuleViolation 类


- (UInt32) RuleId

- (UInt32) FileCount

- (字符串) OfficeApp



## <a name="office-vbasummary"></a>Office VbaSummary

命名空间：root\ccm\InvAgt

CCM_OfficeVbaScanResultsSummary 类


- (UInt32) Design

- (UInt32) Design64

- (UInt32) DuplicateVba

- (布尔值) HasResults

- (UInt32) HasVba

- (UInt32) Inaccessible

- (UInt32) Issues

- (UInt32) Issues64

- (UInt32) IssuesNone

- (UInt32) IssuesNone64

- (UInt32) Locked

- (UInt32) NoVba

- (UInt32) Protected

- (UInt32) RemLimited

- (UInt32) RemLimited64

- (UInt32) RemSignificant

- (UInt32) RemSignificant64

- (UInt32) Score

- (UInt32) Score64

- (UInt32) Total

- (UInt32) Validation

- (UInt32) Validation64



## <a name="operating-system"></a>操作系统

命名空间：root\cimv2

Win32_OperatingSystem 类


- (字符串) Name

- (字符串) BootDevice

- (字符串) BuildNumber

- (字符串) BuildType

- (字符串) Caption

- (字符串) CodeSet

- (字符串) CountryCode

- (字符串) CSDVersion

- (SInt16) CurrentTimeZone

- (布尔值) Debug

- (字符串) Description

- (布尔值) Distributed

- (UInt8) ForegroundApplicationBoost

- (UInt64) FreePhysicalMemory

- (UInt64) FreeSpaceInPagingFiles

- (UInt64) FreeVirtualMemory

- (日期/时间) InstallDate

- (日期/时间) LastBootUpTime

- (日期/时间) LocalDateTime

- (字符串) Locale

- (字符串) Manufacturer

- (UInt32) MaxNumberOfProcesses

- (UInt64) MaxProcessMemorySize

- (字符串) MUILanguages[]

- (UInt32) NumberOfLicensedUsers

- (UInt32) NumberOfProcesses

- (UInt32) NumberOfUsers

- (UInt32) OperatingSystemSKU

- (字符串) Organization

- (字符串) OSArchitecture

- (UInt32) OSLanguage

- (UInt32) OSProductSuite

- (UInt16) OSType

- (字符串) OtherTypeDescription

- (字符串) PlusProductID

- (字符串) PlusVersionNumber

- (布尔值) Primary

- (UInt32) ProductType

- (字符串) RegisteredUser

- (字符串) SerialNumber

- (UInt16) ServicePackMajorVersion

- (UInt16) ServicePackMinorVersion

- (UInt64) SizeStoredInPagingFiles

- (字符串) Status

- (字符串) SystemDevice

- (字符串) SystemDirectory

- (UInt64) TotalSwapSpaceSize

- (UInt64) TotalVirtualMemorySize

- (UInt64) TotalVisibleMemorySize

- (字符串) Version

- (字符串) WindowsDirectory



## <a name="operating-system-ex"></a>操作系统扩展

命名空间：root\cimv2

CCM_OperatingSystemExtended 类


- (字符串) Name

- (UInt32) SKU



## <a name="operating-system-recovery-configuration"></a>操作系统恢复配置

命名空间：root\cimv2

Win32_OSRecoveryConfiguration 类


- (字符串) Name

- (布尔值) AutoReboot

- (字符串) Caption

- (字符串) DebugFilePath

- (字符串) Description

- (布尔值) KernelDumpOnly

- (布尔值) OverwriteExistingDebugFile

- (布尔值) SendAdminAlert

- (字符串) SettingID

- (布尔值) WriteDebugInfo

- (布尔值) WriteToSystemLog



## <a name="optional-feature"></a>可选功能

命名空间：root\cimv2

Win32_OptionalFeature 类


- (字符串) Name

- (字符串) Caption

- (字符串) Description

- (日期/时间) InstallDate

- (UInt32) InstallState

- (字符串) Status



## <a name="page-file-setting"></a>页面文件设置

命名空间：root\cimv2

Win32_PageFileSetting 类


- (字符串) Name

- (字符串) Caption

- (字符串) Description

- (UInt32) InitialSize

- (UInt32) MaximumSize

- (字符串) SettingID



## <a name="parallel-port"></a>并行端口

命名空间：root\cimv2

Win32_ParallelPort 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) DMASupport

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxNumberControlled

- (字符串) Name

- (布尔值) OSAutoDiscovered

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="bios"></a>BIOS

命名空间：root\cimv2

Win32_BIOS 类


- (字符串) Name

- (字符串) SoftwareElementID

- (UInt16) SoftwareElementState

- (UInt16) TargetOperatingSystem

- (字符串) Version

- (UInt16) BiosCharacteristics[]

- (字符串) BIOSVersion[]

- (字符串) BuildNumber

- (字符串) Caption

- (字符串) CodeSet

- (字符串) CurrentLanguage

- (字符串) Description

- (字符串) IdentificationCode

- (UInt16) InstallableLanguages

- (日期/时间) InstallDate

- (字符串) LanguageEdition

- (字符串) ListOfLanguages[]

- (字符串) Manufacturer

- (字符串) OtherTargetOS

- (布尔值) PrimaryBIOS

- (日期/时间) ReleaseDate

- (字符串) SerialNumber

- (字符串) SMBIOSBIOSVersion

- (UInt16) SMBIOSMajorVersion

- (UInt16) SMBIOSMinorVersion

- (布尔值) SMBIOSPresent

- (字符串) Status



## <a name="pcmcia-controller"></a>PCMCIA 控制器

命名空间：root\cimv2

Win32_PCMCIAController 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MaxNumberControlled

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="physical-memory"></a>物理内存

命名空间：root\cimv2

Win32_PhysicalMemory 类


- (字符串) CreationClassName

- (字符串) Tag

- (字符串) BankLabel

- (UInt64) Capacity

- (字符串) Caption

- (UInt16) DataWidth

- (字符串) Description

- (字符串) DeviceLocator

- (UInt16) FormFactor

- (布尔值) HotSwappable

- (日期/时间) InstallDate

- (UInt16) InterleaveDataDepth

- (UInt32) InterleavePosition

- (字符串) Manufacturer

- (UInt16) MemoryType

- (字符串) Model

- (字符串) Name

- (字符串) OtherIdentifyingInfo

- (字符串) PartNumber

- (UInt32) PositionInRow

- (布尔值) PoweredOn

- (布尔值) Removable

- (布尔值) Replaceable

- (字符串) SerialNumber

- (字符串) SKU

- (UInt32) Speed

- (字符串) Status

- (UInt16) TotalWidth

- (UInt16) TypeDetail

- (字符串) Version



## <a name="physicaldisk"></a>物理磁盘

命名空间：root\microsoft\windows\storage

MSFT_PhysicalDisk 类


- (字符串) ObjectId

- (UInt64) AllocatedSize

- (UInt16) BusType

- (UInt16) CannotPoolReason[]

- (布尔值) CanPool

- (字符串) Description

- (字符串) DeviceId

- (UInt16) EnclosureNumber

- (字符串) FirmwareVersion

- (字符串) FriendlyName

- (UInt16) HealthStatus

- (布尔值) IsIndicationEnabled

- (布尔值) IsPartial

- (UInt64) LogicalSectorSize

- (字符串) Manufacturer

- (UInt16) MediaType

- (字符串) Model

- (UInt16) OperationalStatus[]

- (字符串) OtherCannotPoolReasonDescription

- (字符串) PartNumber

- (字符串) PhysicalLocation

- (UInt64) PhysicalSectorSize

- (字符串) SerialNumber

- (UInt64) Size

- (UInt16) SlotNumber

- (字符串) SoftwareVersion

- (UInt32) SpindleSpeed

- (UInt16) SupportedUsages[]

- (字符串) UniqueId

- (UInt16) Usage



## <a name="pnp-device-driver"></a>PNP 设备驱动程序

命名空间：root\cimv2

Win32_PnpEntity 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (字符串) ClassGuid

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) CreationClassName

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) Service

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemCreationClassName

- (字符串) SystemName



## <a name="pointing-device"></a>指针设备

命名空间：root\cimv2

Win32_PointingDevice 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt16) DeviceInterface

- (UInt32) DoubleSpeedThreshold

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt16) Handedness

- (字符串) HardwareType

- (字符串) InfFileName

- (字符串) InfSection

- (日期/时间) InstallDate

- (布尔值) IsLocked

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (字符串) Name

- (UInt8) NumberOfButtons

- (字符串) PNPDeviceID

- (UInt16) PointingType

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt32) QuadSpeedThreshold

- (UInt32) Resolution

- (UInt32) SampleRate

- (字符串) Status

- (UInt16) StatusInfo

- (UInt32) Synch

- (字符串) SystemName



## <a name="portable-battery"></a>便携式电池

命名空间：root\cimv2

Win32_PortableBattery 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt16) BatteryStatus

- (UInt16) CapacityMultiplier

- (字符串) Caption

- (UInt16) Chemistry

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt32) DesignCapacity

- (UInt64) DesignVoltage

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) ExpectedLife

- (UInt32) FullChargeCapacity

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Location

- (字符串) ManufactureDate

- (字符串) Manufacturer

- (UInt16) MaxBatteryError

- (UInt32) MaxRechargeTime

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) SmartBatteryVersion

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (UInt32) TimeOnBattery

- (UInt32) TimeToFullCharge



## <a name="ports"></a>端口

命名空间：root\cimv2

Win32_PortResource 类

- (UInt64) StartingAddress

- (布尔值) Alias

- (字符串) Caption

- (字符串) Description

- (UInt64) EndingAddress

- (日期/时间) InstallDate

- (字符串) Name

- (字符串) Status



## <a name="power-capabilities"></a>电源功能

命名空间：root\CCM\powermanagementagent

CCM_PwrMgmtSystemPowerCapabilities 类


- (UInt32) PreferredPMProfile

- (布尔值) ApmPresent

- (布尔值) BatteriesAreShortTerm

- (布尔值) FullWake

- (布尔值) LidPresent

- (字符串) MinDeviceWakeState

- (布尔值) ProcessorThrottle

- (字符串) RtcWake

- (布尔值) SystemBatteriesPresent

- (布尔值) SystemS1

- (布尔值) SystemS2

- (布尔值) SystemS3

- (布尔值) SystemS4

- (布尔值) SystemS5

- (布尔值) UpsPresent

- (布尔值) VideoDimPresent



## <a name="power-configurations"></a>电源配置

命名空间：root\CCM\policy\machine\actualconfig

CCM_PowerConfig 类


- (字符串) PowerConfigID

- (UInt32) DurationInSec

- (字符串) NonPeakPowerPlan

- (字符串) NonPeakPowerPlanName

- (字符串) PeakPowerPlan

- (字符串) PeakPowerPlanName

- (字符串) PeakStartTimeHoursMin

- (字符串) WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>电源管理失眠原因

命名空间：root\CCM\powermanagementagent

CCM_PwrMgmtLastSuspendError 类


- (字符串) Requester

- (字符串) RequesterType

- (字符串) RequestType

- (日期/时间) Time

- (UInt32) AdditionalCode

- (字符串) AdditionalInfo

- (字符串) RequesterInfo

- (布尔值) UnknownRequester



## <a name="power-management-daily"></a>每日电源管理

命名空间：root\CCM\powermanagementagent

CCM_PwrMgmtActualDay 类


- (日期/时间) Date

- (字符串) TypeOfEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutesTotal



## <a name="power-client-opt-out-settings"></a>电源客户端禁用设置

命名空间：root\ccm\ClientSDK

CCM_PowerManagementClientOptoutSetting 类


- (布尔值) AdminAllowOptout

- (布尔值) EffectiveClientOptOut

- (布尔值) IsClientOptOut



## <a name="power-management-monthly"></a>每月电源管理

命名空间：root\CCM\powermanagementagent

CCM_PwrMgmtMonth 类


- (日期/时间) MonthStart

- (UInt32) minutesComputerActive

- (UInt32) minutesComputerOn

- (UInt32) minutesComputerShutdown

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- (字符串) TypeOfEvent



## <a name="power-settings"></a>电源设置

命名空间：root\cimv2\sms

SMS_PowerSettings 类


- (字符串) GUID

- (字符串) ACSettingIndex

- (字符串) ACValue

- (字符串) DCSettingIndex

- (字符串) DCValue

- (字符串) Name

- (字符串) UnitSpecifier



## <a name="print-jobs"></a>打印作业

命名空间：root\cimv2

Win32_PrintJob 类


- (字符串) Name

- (字符串) Caption

- (字符串) DataType

- (字符串) Description

- (字符串) Document

- (字符串) DriverName

- (日期/时间) ElapsedTime

- (字符串) HostPrintQueue

- (日期/时间) InstallDate

- (UInt32) JobId

- (字符串) JobStatus

- (字符串) Notify

- (字符串) Owner

- (UInt32) PagesPrinted

- (字符串) Parameters

- (字符串) PrintProcessor

- (UInt32) Priority

- (UInt32) Size

- (日期/时间) StartTime

- (字符串) Status

- (UInt32) StatusMask

- (日期/时间) TimeSubmitted

- (UInt32) TotalPages

- (日期/时间) UntilTime



## <a name="printer-configuration"></a>打印机配置

命名空间：root\cimv2

Win32_PrinterConfiguration 类


- (字符串) Name

- (UInt32) BitsPerPel

- (字符串) Caption

- (布尔值) Collate

- (UInt32) Color

- (UInt32) Copies

- (字符串) Description

- (字符串) DeviceName

- (UInt32) DisplayFlags

- (UInt32) DisplayFrequency

- (UInt32) DitherType

- (UInt32) DriverVersion

- (布尔值) Duplex

- (字符串) FormName

- (UInt32) HorizontalResolution

- (UInt32) ICMIntent

- (UInt32) ICMMethod

- (UInt32) LogPixels

- (UInt32) MediaType

- (UInt32) Orientation

- (UInt32) PaperLength

- (字符串) PaperSize

- (UInt32) PaperWidth

- (UInt32) PelsHeight

- (UInt32) PelsWidth

- (UInt32) PrintQuality

- (UInt32) Scale

- (字符串) SettingID

- (UInt32) SpecificationVersion

- (UInt32) TTOption

- (UInt32) VerticalResolution

- (UInt32) XResolution

- (UInt32) YResolution



## <a name="printer-device"></a>打印机设备

命名空间：root\cimv2

Win32_Printer 类


- (字符串) DeviceID

- (UInt32) Attributes

- (UInt16) Availability

- (UInt32) AveragePagesPerMinute

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt32) DefaultPriority

- (字符串) Description

- (UInt16) DetectedErrorState

- (字符串) DriverName

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt32) HorizontalResolution

- (日期/时间) InstallDate

- (UInt32) JobCountSinceLastReset

- (UInt16) LanguagesSupported[]

- (UInt32) LastErrorCode

- (字符串) Location

- (字符串) Name

- (UInt16) PaperSizesSupported[]

- (字符串) PNPDeviceID

- (字符串) PortName

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) PrinterPaperNames[]

- (UInt32) PrinterState

- (UInt16) PrinterStatus

- (字符串) PrintJobDataType

- (字符串) PrintProcessor

- (字符串) SeparatorFile

- (字符串) ServerName

- (字符串) ShareName

- (布尔值) SpoolEnabled

- (日期/时间) StartTime

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset

- (日期/时间) UntilTime

- (UInt32) VerticalResolution



## <a name="process"></a>过程

命名空间：root\cimv2

Win32_Process 类


- (字符串) Handle

- (字符串) Caption

- (日期/时间) CreationDate

- (字符串) Description

- (字符串) ExecutablePath

- (UInt16) ExecutionState

- (UInt32) HandleCount

- (日期/时间) InstallDate

- (UInt64) KernelModeTime

- (UInt32) MaximumWorkingSetSize

- (UInt32) MinimumWorkingSetSize

- (字符串) Name

- (字符串) OSName

- (UInt64) OtherOperationCount

- (UInt64) OtherTransferCount

- (UInt32) PageFaults

- (UInt32) PageFileUsage

- (UInt32) ParentProcessId

- (UInt32) PeakPageFileUsage

- (UInt64) PeakVirtualSize

- (UInt32) PeakWorkingSetSize

- (UInt32) Priority

- (UInt64) PrivatePageCount

- (UInt32) ProcessId

- (UInt32) QuotaNonPagedPoolUsage

- (UInt32) QuotaPagedPoolUsage

- (UInt32) QuotaPeakNonPagedPoolUsage

- (UInt32) QuotaPeakPagedPoolUsage

- (UInt64) ReadOperationCount

- (UInt64) ReadTransferCount

- (UInt32) SessionId

- (字符串) Status

- (日期/时间) TerminationDate

- (UInt32) ThreadCount

- (UInt64) UserModeTime

- (UInt64) VirtualSize

- (字符串) WindowsVersion

- (UInt64) WorkingSetSize

- (UInt64) WriteOperationCount

- (UInt64) WriteTransferCount



## <a name="processor"></a>处理器

命名空间：root\cimv2\sms

SMS_Processor 类


- (字符串) DeviceID

- (UInt16) AddressWidth

- (UInt16) Architecture

- (UInt16) Availability

- (UInt16) BrandID

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) CPUHash

- (字符串) CPUKey

- (UInt16) CpuStatus

- (UInt32) CurrentClockSpeed

- (UInt16) CurrentVoltage

- (UInt16) DataWidth

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt32) ExtClock

- (UInt16) Family

- (日期/时间) InstallDate

- (布尔值) Is64Bit

- (布尔值) IsHyperthreadCapable

- (布尔值) IsHyperthreadEnabled

- (布尔值) IsMobile

- (布尔值) IsTrustedExecutionCapable

- (布尔值) IsVitualizationCapable

- (UInt32) L2CacheSize

- (UInt32) L2CacheSpeed

- (UInt32) L3CacheSize

- (UInt32) L3CacheSpeed

- (UInt32) LastErrorCode

- (UInt16) Level

- (UInt16) LoadPercentage

- (字符串) Manufacturer

- (UInt32) MaxClockSpeed

- (字符串) Name

- (UInt32) NormSpeed

- (UInt32) NumberOfCores

- (UInt32) NumberOfLogicalProcessors

- (字符串) OtherFamilyDescription

- (布尔值) PartOfDomain

- (UInt32) PCache

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) ProcessorId

- (UInt16) ProcessorType

- (UInt16) Revision

- (字符串) Role

- (字符串) SocketDesignation

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) Stepping

- (字符串) SystemName

- (字符串) UniqueId

- (UInt16) UpgradeMethod

- (字符串) Version

- (UInt32) VoltageCaps

- (字符串) Workgroup



## <a name="protected-volume-information"></a>受保护的卷信息

命名空间：root\cimv2\sms

CCM_ProtectedVolumeInfo 类


- (字符串) Name

- (字符串) DriveLetter

- (UInt32) ProtectionType



## <a name="protocol"></a>协议

命名空间：root\cimv2

Win32_NetworkProtocol 类


- (字符串) Name

- (字符串) Caption

- (布尔值) ConnectionlessService

- (字符串) Description

- (布尔值) GuaranteesDelivery

- (布尔值) GuaranteesSequencing

- (日期/时间) InstallDate

- (UInt32) MaximumAddressSize

- (UInt32) MaximumMessageSize

- (布尔值) MessageOriented

- (UInt32) MinimumAddressSize

- (布尔值) PseudoStreamOriented

- (字符串) Status

- (布尔值) SupportsBroadcasting

- (布尔值) SupportsConnectData

- (布尔值) SupportsDisconnectData

- (布尔值) SupportsEncryption

- (布尔值) SupportsExpeditedData

- (布尔值) SupportsFragmentation

- (布尔值) SupportsGracefulClosing

- (布尔值) SupportsGuaranteedBandwidth

- (布尔值) SupportsMulticasting

- (布尔值) SupportsQualityofService



## <a name="quick-fix-engineering"></a>快速修补工程

命名空间：root\cimv2

Win32_QuickFixEngineering 类


- (字符串) HotFixID

- (字符串) ServicePackInEffect

- (字符串) Caption

- (字符串) Description

- (字符串) FixComments

- (日期/时间) InstallDate

- (字符串) InstalledBy

- (字符串) InstalledOn

- (字符串) Name

- (字符串) Status



## <a name="ccm-recently-used-applications"></a>CCM 最近使用过的应用程序

命名空间：root\cimv2\sms

CCM_RecentlyUsedApps 类


- (字符串) ExplorerFileName

- (字符串) FolderPath

- (字符串) LastUserName

- (字符串) AdditionalProductCodes

- (字符串) CompanyName

- (字符串) FileDescription

- (字符串) FilePropertiesHash

- (UInt32) FileSize

- (字符串) FileVersion

- (日期/时间) LastUsedTime

- (UInt32) LaunchCount

- (字符串) msiDisplayName

- (字符串) msiPublisher

- (字符串) msiVersion

- (字符串) OriginalFileName

- (字符串) ProductCode

- (UInt32) ProductLanguage

- (字符串) ProductName

- (字符串) ProductVersion

- (字符串) SoftwarePropertiesHash



## <a name="registry"></a>注册表

命名空间：root\cimv2

Win32_Registry 类


- (字符串) Name

- (字符串) Caption

- (UInt32) CurrentSize

- (字符串) Description

- (日期/时间) InstallDate

- (UInt32) MaximumSize

- (UInt32) ProposedSize

- (字符串) Status



## <a name="scsi-controller"></a>SCSI 控制器

命名空间：root\cimv2

Win32_SCSIController 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt32) ControllerTimeouts

- (字符串) Description

- (字符串) DeviceMap

- (字符串) DriverName

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) HardwareVersion

- (UInt32) Index

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MaxDataWidth

- (UInt32) MaxNumberControlled

- (UInt64) MaxTransferRate

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtectionManagement

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="serial-port-configuration"></a>串行端口配置

命名空间：root\cimv2

Win32_SerialPortConfiguration 类


- (字符串) Name

- (布尔值) AbortReadWriteOnError

- (UInt32) BaudRate

- (布尔值) BinaryModeEnabled

- (UInt32) BitsPerByte

- (字符串) Caption

- (布尔值) ContinueXMitOnXOff

- (布尔值) CTSOutflowControl

- (字符串) Description

- (布尔值) DiscardNULLBytes

- (布尔值) DSROutflowControl

- (布尔值) DSRSensitivity

- (字符串) DTRFlowControlType

- (UInt32) EOFCharacter

- (UInt32) ErrorReplaceCharacter

- (布尔值) ErrorReplacementEnabled

- (UInt32) EventCharacter

- (布尔值) IsBusy

- (字符串) Parity

- (布尔值) ParityCheckEnabled

- (字符串) RTSFlowControlType

- (字符串) SettingID

- (字符串) StopBits

- (UInt32) XOffCharacter

- (UInt32) XOffXMitThreshold

- (UInt32) XOnCharacter

- (UInt32) XOnXMitThreshold

- (UInt32) XOnXOffInFlowControl

- (UInt32) XOnXOffOutFlowControl



## <a name="serial-ports"></a>串行端口

命名空间：root\cimv2

Win32_SerialPort 类


- (字符串) DeviceID

- (UInt16) Availability

- (布尔值) Binary

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (UInt32) MaxBaudRate

- (UInt32) MaximumInputBufferSize

- (UInt32) MaximumOutputBufferSize

- (UInt32) MaxNumberControlled

- (字符串) Name

- (布尔值) OSAutoDiscovered

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) ProviderType

- (布尔值) SettableBaudRate

- (布尔值) SettableDataBits

- (布尔值) SettableFlowControl

- (布尔值) SettableParity

- (布尔值) SettableParityCheck

- (布尔值) SettableRLSD

- (布尔值) SettableStopBits

- (字符串) Status

- (UInt16) StatusInfo

- (布尔值) Supports16BitMode

- (布尔值) SupportsDTRDSR

- (布尔值) SupportsElapsedTimeouts

- (布尔值) SupportsIntTimeouts

- (布尔值) SupportsParityCheck

- (布尔值) SupportsRLSD

- (布尔值) SupportsRTSCTS

- (布尔值) SupportsSpecialCharacters

- (布尔值) SupportsXOnXOff

- (布尔值) SupportsXOnXOffSet

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="server-feature"></a>服务器功能

命名空间：root\cimv2

Win32_ServerFeature 类


- (UInt32) ID

- (字符串) Name

- (UInt32) ParentID



## <a name="services"></a>服务

命名空间：root\cimv2

Win32_Service 类


- (字符串) Name

- (布尔值) AcceptPause

- (布尔值) AcceptStop

- (字符串) Caption

- (UInt32) CheckPoint

- (字符串) Description

- (布尔值) DesktopInteract

- (字符串) DisplayName

- (字符串) ErrorControl

- (UInt32) ExitCode

- (日期/时间) InstallDate

- (字符串) PathName

- (UInt32) ProcessId

- (UInt32) ServiceSpecificExitCode

- (字符串) ServiceType

- (布尔值) Started

- (字符串) StartMode

- (字符串) StartName

- (字符串) State

- (字符串) Status

- (字符串) SystemName

- (UInt32) TagId

- (UInt32) WaitHint



## <a name="shares"></a>共享

命名空间：root\cimv2

Win32_Share 类


- (字符串) Name

- (UInt32) AccessMask

- (布尔值) AllowMaximum

- (字符串) Caption

- (字符串) Description

- (日期/时间) InstallDate

- (UInt32) MaximumAllowed

- (字符串) Path

- (字符串) Status

- (UInt32) Type



## <a name="sw-licensing-product"></a>SW 授权产品

命名空间：root\cimv2

SoftwareLicensingProduct 类


- (字符串) ID

- (字符串) ApplicationID

- (字符串) Description

- (日期/时间) EvaluationEndDate

- (UInt32) GracePeriodRemaining

- (UInt32) LicenseStatus

- (字符串) MachineURL

- (字符串) Name

- (字符串) OfflineInstallationId

- (字符串) PartialProductKey

- (字符串) ProcessorURL

- (字符串) ProductKeyID

- (字符串) ProductKeyURL

- (字符串) UseLicenseURL



## <a name="sw-licensing-service"></a>SW 授权服务

命名空间：root\cimv2

SoftwareLicensingService 类


- (字符串) Version

- (字符串) ClientMachineID

- (UInt32) IsKeyManagementServiceMachine

- (UInt32) KeyManagementServiceCurrentCount

- (字符串) KeyManagementServiceMachine

- (字符串) KeyManagementServiceProductKeyID

- (UInt32) PolicyCacheRefreshRequired

- (UInt32) RequiredClientCount

- (UInt32) VLActivationInterval

- (UInt32) VLRenewalInterval



## <a name="software-shortcut"></a>软件快捷方式

命名空间：root\cimv2\sms

SMS_SoftwareShortcut 类


- (字符串) ShortcutKey

- (字符串) BinFileVersion

- (字符串) BinProductVersion

- (字符串) Description

- (字符串) FilePropertiesHash

- (字符串) FilePropertiesHashEx

- (UInt32) FileSize

- (字符串) FileVersion

- (UInt32) Language

- (字符串) ParentName

- (字符串) Product

- (字符串) ProductCode

- (字符串) ProductVersion

- (字符串) Publisher

- (字符串) ShortcutName

- (UInt32) ShortcutType

- (字符串) TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

命名空间：root\cimv2\sms

SMS_SoftwareTag 类


- (字符串) TagCreatorRegid

- (字符串) UniqueID

- (字符串) DisplayVersion

- (布尔值) EntitlementRequired

- (字符串) ProductName

- (字符串) SoftwareCreator

- (字符串) SoftwareCreatorRegid

- (字符串) SoftwareLicensor

- (字符串) SoftwareLicensorRegid

- (字符串) TagCreator

- (SInt32) VersionMajor

- (SInt32) VersionMinor



## <a name="sound-devices"></a>声音设备

命名空间：root\cimv2

Win32_SoundDevice 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (UInt16) DMABufferSize

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MPU401Address

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) ProductName

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName



## <a name="system-account"></a>系统帐户

命名空间：root\cimv2

Win32_SystemAccount 类


- (字符串) Domain

- (字符串) Name

- (字符串) Caption

- (字符串) Description

- (日期/时间) InstallDate

- (字符串) SID

- (UInt8) SIDType

- (字符串) Status



## <a name="system-boot-data"></a>系统启动数据

命名空间：root\CCM

CCM_SystemBootData 类


- (UInt64) SystemStartTime

- (UInt32) BiosDuration

- (UInt16) BootDiskMediaType

- (UInt32) BootDuration

- (UInt32) EventLogStart

- (UInt32) GPDuration

- (字符串) OSVersion

- (UInt32) UpdateDuration



## <a name="system-boot-summary"></a>系统启动摘要

命名空间：root\CCM

CCM_SystemBootSummary 类


- (UInt32) AverageBootFrequency

- (UInt32) LatestBiosDuration

- (UInt32) LatestBootDuration

- (UInt32) LatestCoreBootDuration

- (UInt32) LatestEventLogStart

- (UInt32) LatestGPDuration

- (UInt32) LatestUpdateDuration

- (UInt32) MaxBiosDuration

- (UInt32) MaxBootDuration

- (UInt32) MaxCoreBootDuration

- (UInt32) MaxEventLogStart

- (UInt32) MaxGPDuration

- (UInt32) MaxUpdateDuration

- (UInt32) MedianBiosDuration

- (UInt32) MedianBootDuration

- (UInt32) MedianCoreBootDuration

- (UInt32) MedianEventLogStart

- (UInt32) MedianGPDuration

- (UInt32) MedianUpdateDuration



## <a name="system-console-usage"></a>系统控制台使用情况

命名空间：root\cimv2\sms

SMS_SystemConsoleUsage 类


- (日期/时间) SecurityLogStartDate

- (字符串) TopConsoleUser

- (UInt32) TotalConsoleTime

- (UInt32) TotalConsoleUsers

- (UInt32) TotalSecurityLogTime



## <a name="system-console-user"></a>系统控制台用户

命名空间：root\cimv2\sms

SMS_SystemConsoleUser 类


- (字符串) SystemConsoleUser

- (日期/时间) LastConsoleUse

- (UInt32) NumberOfConsoleLogons

- (UInt32) TotalUserConsoleMinutes



## <a name="system-devices"></a>系统设备

命名空间：root\cimv2\sms

CCM_SystemDevices 类


- (字符串) Name

- (字符串) CompatibleIDs[]

- (字符串) DeviceID

- (字符串) HardwareIDs[]

- (布尔值) IsPnP



## <a name="system-drivers"></a>系统驱动程序

命名空间：root\cimv2

Win32_SystemDriver 类


- (字符串) Name

- (布尔值) AcceptPause

- (布尔值) AcceptStop

- (字符串) Caption

- (字符串) Description

- (布尔值) DesktopInteract

- (字符串) DisplayName

- (字符串) ErrorControl

- (UInt32) ExitCode

- (日期/时间) InstallDate

- (字符串) PathName

- (UInt32) ServiceSpecificExitCode

- (字符串) ServiceType

- (布尔值) Started

- (字符串) StartMode

- (字符串) StartName

- (字符串) State

- (字符串) Status

- (字符串) SystemName

- (UInt32) TagId



## <a name="system-enclosure"></a>系统机箱

命名空间：root\cimv2

Win32_SystemEnclosure 类


- (字符串) Tag

- (布尔值) AudibleAlarm

- (字符串) BreachDescription

- (字符串) CableManagementStrategy

- (字符串) Caption

- (UInt16) ChassisTypes[]

- (SInt16) CurrentRequiredOrProduced

- (字符串) Description

- (UInt16) HeatGeneration

- (布尔值) HotSwappable

- (日期/时间) InstallDate

- (布尔值) LockPresent

- (字符串) Manufacturer

- (字符串) Model

- (字符串) Name

- (UInt16) NumberOfPowerCords

- (字符串) OtherIdentifyingInfo

- (字符串) PartNumber

- (布尔值) PoweredOn

- (布尔值) Removable

- (布尔值) Replaceable

- (UInt16) SecurityBreach

- (UInt16) SecurityStatus

- (字符串) SerialNumber

- (字符串) ServiceDescriptions[]

- (UInt16) ServicePhilosophy[]

- (字符串) SKU

- (字符串) SMBIOSAssetTag

- (字符串) Status

- (字符串) TypeDescriptions[]

- (字符串) Version

- (布尔值) VisibleAlarm



## <a name="tape-drive"></a>磁带驱动器

命名空间：root\cimv2

Win32_TapeDrive 类


- (字符串) DeviceID

- (UInt16) Availability

- (UInt16) Capabilities[]

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (UInt32) Compression

- (字符串) CompressionMethod

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt64) DefaultBlockSize

- (字符串) Description

- (UInt32) ECC

- (UInt32) EOTWarningZoneSize

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (UInt32) FeaturesHigh

- (UInt32) FeaturesLow

- (字符串) ID

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt64) MaxBlockSize

- (UInt64) MaxMediaSize

- (UInt32) MaxPartitionCount

- (字符串) MediaType

- (UInt64) MinBlockSize

- (字符串) Name

- (布尔值) NeedsCleaning

- (UInt32) NumberOfMediaSupported

- (UInt32) Padding

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt32) ReportSetMarks

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName



## <a name="time-zone"></a>时区

命名空间：root\cimv2

Win32_TimeZone 类


- (字符串) StandardName

- (SInt32) Bias

- (字符串) Caption

- (SInt32) DaylightBias

- (UInt32) DaylightDay

- (UInt8) DaylightDayOfWeek

- (UInt32) DaylightHour

- (UInt32) DaylightMillisecond

- (UInt32) DaylightMinute

- (UInt32) DaylightMonth

- (字符串) DaylightName

- (UInt32) DaylightSecond

- (UInt32) DaylightYear

- (字符串) Description

- (字符串) SettingID

- (UInt32) StandardBias

- (UInt32) StandardDay

- (UInt8) StandardDayOfWeek

- (UInt32) StandardHour

- (UInt32) StandardMillisecond

- (UInt32) StandardMinute

- (UInt32) StandardMonth

- (UInt32) StandardSecond

- (UInt32) StandardYear



## <a name="tpm"></a>TPM

命名空间：root\CIMv2\Security\MicrosoftTpm

Win32_Tpm 类


- (布尔值) IsActivated_InitialValue

- (布尔值) IsEnabled_InitialValue

- (布尔值) IsOwned_InitialValue

- (UInt32) ManufacturerId

- (字符串) ManufacturerVersion

- (字符串) ManufacturerVersionInfo

- (字符串) PhysicalPresenceVersionInfo

- (字符串) SpecVersion



## <a name="tpm-status"></a>TPM 状态

命名空间：root\cimv2\sms

SMS_TPM 类


- (布尔值) IsReady

- (UInt32) Information

- (布尔值) IsApplicable



## <a name="ts-issued-license"></a>TS 颁发的许可证

命名空间：root\cimv2

Win32_TSIssuedLicense 类


- (UInt32) LicenseId

- (日期/时间) ExpirationDate

- (日期/时间) IssueDate

- (UInt32) KeyPackId

- (UInt32) LicenseStatus

- (字符串) sHardwareId

- (字符串) sIssuedToComputer

- (字符串) sIssuedToUser



## <a name="ts-license-key-pack"></a>TS 许可证密钥包

命名空间：root\cimv2

Win32_TSLicenseKeyPack 类


- (UInt32) KeyPackId

- (UInt32) AvailableLicenses

- (字符串) Description

- UInt32IssuedLicenses

- (UInt32) KeyPackType

- (UInt32) ProductType

- (字符串) ProductVersion

- (UInt32) TotalLicenses



## <a name="uninterruptible-power-supply"></a>不间断电源

命名空间：root\cimv2

Win32_UninterruptiblePowerSupply 类


- (字符串) DeviceID

- (UInt16) ActiveInputVoltage

- (UInt16) Availability

- (布尔值) BatteryInstalled

- (布尔值) CanTurnOffRemotely

- (字符串) Caption

- (字符串) CommandFile

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt16) EstimatedChargeRemaining

- (UInt32) EstimatedRunTime

- (UInt32) FirstMessageDelay

- (日期/时间) InstallDate

- (布尔值) IsSwitchingSupply

- (UInt32) LastErrorCode

- (布尔值) LowBatterySignal

- (UInt32) MessageInterval

- (字符串) Name

- (字符串) PNPDeviceID

- (布尔值) PowerFailSignal

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt32) Range1InputFrequencyHigh

- (UInt32) Range1InputFrequencyLow

- (UInt32) Range1InputVoltageHigh

- (UInt32) Range1InputVoltageLow

- (UInt32) Range2InputFrequencyHigh

- (UInt32) Range2InputFrequencyLow

- (UInt32) Range2InputVoltageHigh

- (UInt32) Range2InputVoltageLow

- (UInt16) RemainingCapacityStatus

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (UInt32) TimeOnBackup

- (UInt32) TotalOutputPower

- (UInt16) TypeOfRangeSwitching

- (字符串) UPSPort



## <a name="usb-controller"></a>USB 控制器

命名空间：root\cimv2

Win32_USBController 类


- (字符串) DeviceID

- (UInt16) Availability

- (字符串) Caption

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) Description

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (日期/时间) InstallDate

- (UInt32) LastErrorCode

- (字符串) Manufacturer

- (UInt32) MaxNumberControlled

- (字符串) Name

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (日期/时间) TimeOfLastReset



## <a name="usb-device"></a>USB 设备

命名空间：root\cimv2

Win32_USBDevice 类


- (字符串) DeviceID

- (字符串) Caption

- (字符串) ClassGuid

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) CreationClassName

- (字符串) Description

- (字符串) Manufacturer

- (字符串) Name

- (字符串) PNPDeviceID

- (字符串) Service

- (字符串) Status

- (字符串) SystemCreationClassName

- (字符串) SystemName



## <a name="usm-user-profile"></a>USM 用户配置文件

命名空间：root\cimv2

Win32_UserProfile 类


- (字符串) SID

- (UInt8) HealthStatus

- (字符串) LastAttemptedProfileDownloadTime

- (字符串) LastAttemptedProfileUploadTime

- (字符串) LastBackgroundRegistryUploadTime

- (日期/时间) LastDownloadTime

- (日期/时间) LastUploadTime

- (日期/时间) LastUseTime

- (布尔值) Loaded

- (字符串) LocalPath

- (UInt32) RefCount

- (布尔值) RoamingConfigured

- (字符串) RoamingPath

- (布尔值) RoamingPreference

- (布尔值) Special

- (UInt32) Status



## <a name="video-controller"></a>视频控制器

命名空间：root\cimv2

Win32_VideoController 类


- (字符串) DeviceID

- (UInt16) AcceleratorCapabilities[]

- (字符串) AdapterCompatibility

- (字符串) AdapterDACType

- (UInt32) AdapterRAM

- (UInt16) Availability

- (字符串) CapabilityDescriptions[]

- (字符串) Caption

- (UInt32) ColorTableEntries

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (UInt32) CurrentBitsPerPixel

- (UInt32) CurrentHorizontalResolution

- (UInt64) CurrentNumberOfColors

- (UInt32) CurrentNumberOfColumns

- (UInt32) CurrentNumberOfRows

- (UInt32) CurrentRefreshRate

- (UInt16) CurrentScanMode

- (UInt32) CurrentVerticalResolution

- (字符串) Description

- (UInt32) DeviceSpecificPens

- (UInt32) DitherType

- (日期/时间) DriverDate

- (字符串) DriverVersion

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (UInt32) ICMIntent

- (UInt32) ICMMethod

- (字符串) InfFilename

- (字符串) InfSection

- (日期/时间) InstallDate

- (字符串) InstalledDisplayDrivers

- (UInt32) LastErrorCode

- (UInt32) MaxMemorySupported

- (UInt32) MaxNumberControlled

- (UInt32) MaxRefreshRate

- (UInt32) MinRefreshRate

- (布尔值) Monochrome

- (字符串) Name

- (UInt16) NumberOfColorPlanes

- (UInt32) NumberOfVideoPages

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (UInt16) ProtocolSupported

- (UInt32) ReservedSystemPaletteEntries

- (UInt32) SpecificationVersion

- (字符串) Status

- (UInt16) StatusInfo

- (字符串) SystemName

- (UInt32) SystemPaletteEntries

- (日期/时间) TimeOfLastReset

- (UInt16) VideoArchitecture

- (UInt16) VideoMemoryType

- (UInt16) VideoMode

- (字符串) VideoModeDescription

- (字符串) VideoProcessor



## <a name="virtual-application-packages"></a>虚拟应用程序包

命名空间：root\Microsoft\appvirt\client

Package 类


- (字符串) PackageGUID

- (UInt64) CachedLaunchSize

- (UInt16) CachedPercentage

- (UInt64) CachedSize

- (UInt64) LaunchSize

- (字符串) Name

- (字符串) SftPath

- (UInt64) TotalSize

- (字符串) Version

- (字符串) VersionGUID



## <a name="virtual-applications"></a>虚拟应用程序

命名空间：root\Microsoft\appvirt\client

Application 类


- (字符串) Name

- (字符串) Version

- (字符串) CachedOsdPath

- (UInt32) GlobalRunningCount

- (日期/时间) LastLaunchOnSystem

- (布尔值) Loading

- (字符串) OriginalOsdPath

- (字符串) PackageGUID



## <a name="virtual-machine-64"></a>虚拟机 (64)

命名空间：root\cimv2

Win32Reg_SMSGuestVirtualMachine64 类


- (字符串) InstanceKey

- (字符串) PhysicalHostName

- (字符串) PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>虚拟机

命名空间：root\cimv2

Win32Reg_SMSGuestVirtualMachine 类


- (字符串) InstanceKey

- (字符串) PhysicalHostName

- (字符串) PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>虚拟机详细信息

命名空间：root\vm\VirtualServer

VirtualMachine 类


- (字符串) Name

- (UInt32) CpuUtilization

- (UInt64) DiskBytesRead

- (UInt64) DiskBytesWritten

- (UInt64) DiskSpaceUsed

- (UInt64) HeartbeatCount

- (UInt32) HeartbeatInterval

- (UInt32) HeartbeatPercentage

- (UInt32) HeartbeatRate

- (UInt64) NetworkBytesReceived

- (UInt64) NetworkBytesSent

- (UInt64) PhysicalMemoryAllocated

- (UInt32) Uptime



## <a name="volume"></a>Volume

命名空间：root\cimv2

Win32_Volume 类


- (字符串) DeviceID

- (UInt16) Access

- (布尔值) Automount

- (UInt16) Availability

- (UInt64) BlockSize

- (UInt64) Capacity

- (字符串) Caption

- (布尔值) Compressed

- (UInt32) ConfigManagerErrorCode

- (布尔值) ConfigManagerUserConfig

- (字符串) CreationClassName

- (字符串) Description

- (布尔值) DirtyBitSet

- (字符串) DriveLetter

- (UInt32) DriveType

- (布尔值) ErrorCleared

- (字符串) ErrorDescription

- (字符串) ErrorMethodology

- (字符串) FileSystem

- (UInt64) FreeSpace

- (布尔值) IndexingEnabled

- (日期/时间) InstallDate

- (字符串) Label

- (UInt32) LastErrorCode

- (UInt32) MaximumFileNameLength

- (字符串) Name

- (UInt64) NumberOfBlocks

- (字符串) PNPDeviceID

- (UInt16) PowerManagementCapabilities[]

- (布尔值) PowerManagementSupported

- (字符串) Purpose

- (布尔值) QuotasEnabled

- (布尔值) QuotasIncomplete

- (布尔值) QuotasRebuilding

- (UInt32) SerialNumber

- (字符串) Status

- (UInt16) StatusInfo

- (布尔值) SupportsDiskQuotas

- (布尔值) SupportsFileBasedCompression

- (字符串) SystemCreationClassName

- (字符串) SystemName



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

命名空间：root\ccm\cimodels

CCM_WebAppInstallInfo 类


- (字符串) AppDeliveryTypeId

- (UInt32) AppDtRevision

- (字符串) TargetURL

- (字符串) UserSID

- (字符串) URLFileName

- (字符串) URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

命名空间：root\cimv2\sms

SMS_Windows8Application 类


- (字符串) FullName

- (字符串) ApplicationName

- (字符串) Architecture

- (布尔值) ConfigMgrManaged

- (字符串) DependencyApplicationNames

- (字符串) FamilyName

- (字符串) InstalledLocation

- (布尔值) IsFramework

- (字符串) Publisher

- (字符串) PublisherId

- (字符串) Version



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

命名空间：root\cimv2\sms

SMS_Windows8ApplicationUserInfo 类


- (字符串) FullName

- (字符串) UserSecurityId

- (字符串) InstallState

- (字符串) UserAccountName



## <a name="windows-update"></a>Windows 更新

命名空间：root\cimv2

Win32Reg_SMSWindowsUpdate 类


- (字符串) InstanceKey

- (UInt32) AUOptions

- (UInt32) NoAutoUpdate

- (UInt32) UseWUServer



## <a name="windows-update-agent-version"></a>Windows 更新代理版本

命名空间：root\cimv2\sms

Win32_WindowsUpdateAgentVersion 类


- (字符串) Version



## <a name="write-filter-state"></a>写入筛选器状态

命名空间：root\cimv2\sms

CCM_WriteFilterState 类


- (布尔值) WriteFilterEnabled
