---
title: Průzkumník prostředků výchozí třídy inventáře
titleSuffix: Configuration Manager
description: Zobrazuje třídy, které se zobrazují v Průzkumník prostředků
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
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710731"
---
# <a name="resource-explorer-default-inventory-classes"></a>Průzkumník prostředků výchozí třídy inventáře

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje výchozí třídy inventáře v Průzkumník prostředků.

Jedná se o výchozí třídy inventáře:

## <a name="1394-controller"></a>řadič 1394

Obor názvů: root\cimv2

Win32_1394Controller třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="account-sid"></a>SID účtu

Obor názvů: root\cimv2

Win32_AccountSID třídy

- Řetezce Objekt

- Řetezce Nastavením



## <a name="activesync-service"></a>Služba ActiveSync

Obor názvů: root\SmsDm

SMS_ActiveSyncService třídy


- UInt32 MajorVersion

- UInt32 Podverze

- Řetezce LastSyncTime



## <a name="amt-agent"></a>Agent AMT

Obor názvů: Root\Cimv2\Sms

SMS_AMTObject třídy


- UInt32 DeviceID

- Řetezce ADJ

- Řetezce AMTApps

- Řetezce BiosVersion

- Řetezce BuildNumber

- Řetezce Blikající

- Řetezce LegacyMode

- Řetezce Netstack

- UInt32 ProvisionMode

- UInt32 ProvisionState

- Řetezce RecoveryBuildNum

- Řetezce RecoveryVersion

- Řetezce Skladové

- UInt32 TLSMode

- Řetezce VendorID

- UInt32 ZTCEnabled



## <a name="appv-client-application"></a>Klientská aplikace AppV

Obor názvů: root\AppV

AppvClientApplication třídy


- Řetezce ApplicationId

- Řetezce PackageId

- Řetezce PackageVersionId

- Datového EnabledForUser

- Datového EnabledGlobally

- Řetezce Jméno

- Řetezce TargetPath

- Řetezce Znění



## <a name="appv-client-package"></a>Klientský balíček AppV

Obor názvů: root\AppV

AppvClientPackage třídy


- Řetezce PackageId

- Řetezce VersionId

- Řetezce Prostředky []

- Řetezce DeploymentMachineData

- Řetezce DeploymentUserData

- Datového HasAssetIntelligence

- Datového Používané

- Datového IsPublishedGlobally

- Datového IsPublishedToUser

- Řetezce Jméno

- UInt64 PackageSize

- Řetezce Dílčí

- UInt16 PercentLoaded

- Řetezce UserConfigurationData

- Řetezce Znění



## <a name="autostart-software"></a>Software pro automatické spuštění

Obor názvů: Root\Cimv2\Sms

SMS_AutoStartSoftware třídy


- Řetezce FilePropertiesHash

- Řetezce BinFileVersion

- Řetezce BinProductVersion

- Řetezce Název

- Řetezce Bitmap

- Řetezce FilePropertiesHashEx

- Řetezce FileVersion

- Řetezce Oblasti

- Řetezce Produktu

- Řetezce ProductVersion

- Řetezce Microsoft

- Řetezce StartupType

- Řetezce StartupValue



## <a name="baseboard"></a>Základní

Obor názvů: root\cimv2

Win32_BaseBoard třídy


- Řetezce Inteligentní

- Řetezce Popisku

- Řetezce ConfigOptions[]

- Řetezce Název

- Datového HostingBoard

- Datového HotSwappable

- Hodnotu InstallDate

- Řetezce Výrobců

- Řetezce Vzorový

- Řetezce Jméno

- Řetezce OtherIdentifyingInfo

- Řetezce PartNumber

- Datového PoweredOn

- Řetezce Produktu

- Datového Disket

- Datového Replaceable

- Řetezce RequirementsDescription

- Datového RequiresDaughterBoard

- Řetezce Sériové

- Řetezce SKLADOVÉ

- Řetezce SlotLayout

- Datového SpecialRequirements

- Řetezce Stav

- Řetezce Znění



## <a name="battery"></a>Baterie

Obor názvů: root\cimv2

Win32_Battery třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt16 BatteryStatus

- Řetezce Popisku

- UInt16 Složení

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime (

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- Hodnotu InstallDate

- UInt32 LastErrorCode

- UInt32 MaxRechargeTime

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce SmartBatteryVersion

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="bitlocker"></a>BitLocker

Obor názvů: root\cimv2\security\MicrosoftVolumeEncryption

Win32_EncryptableVolume třídy


- Řetezce DeviceID

- Řetezce Písmeno_jednotky

- Řetezce PersistentVolumeID

- UInt32 ProtectionStatus



## <a name="bitlocker-encryption-details"></a>Podrobnosti šifrování BitLockeru

Obor názvů: root\cimv2

Win32_BitLockerEncryptionDetails třídy


- Řetezce BitlockerPersistentVolumeId

- (SInt32) Kompatibilní

- (SInt32) ConversionStatus

- Řetezce DeviceId

- Řetezce Písmeno_jednotky

- (SInt32) EncryptionMethod

- Řetezce EnforcePolicyDate

- Datového IsAutoUnlockEnabled

- (SInt32) KeyProtectorTypes[]

- Řetezce MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- Řetezce NoncomplianceDetectedDate

- (SInt32) ProtectionStatus

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>Zásada BitLockeru

Obor názvů: root\cimv2

Win32Reg_MBAMPolicy třídy


- Řetezce EncodedComputerName

- UInt32 EncryptionMethod

- UInt32 FixedDataDriveAutoUnlock

- UInt32 FixedDataDriveEncryption

- UInt32 FixedDataDrivePassphrase

- Řetezce Klíče

- Řetezce LastConsoleUser

- UInt32 MBAMMachineError

- UInt32 MBAMPolicyEnforced

- UInt32 OsDriveEncryption

- UInt32 OsDriveProtector

- Hodnotu UserExemptionDate



## <a name="boot-configuration"></a>Konfigurace spouštění

Obor názvů: root\cimv2

Win32_BootConfiguration třídy


- Řetezce Jméno

- Řetezce BootDirectory

- Řetezce ConfigurationPath

- Řetezce Název

- Řetezce LastDrive

- Řetezce ScratchDirectory

- Řetezce Vlastnost SettingId

- Řetezce TempDirectory



## <a name="browser-helper-object"></a>Objekt pomocníka prohlížeče

Obor názvů: Root\Cimv2\Sms

SMS_BrowserHelperObject třídy


- Řetezce FilePropertiesHash

- Řetezce BinFileVersion

- Řetezce BinProductVersion

- Řetezce CLSID

- Řetezce Název

- Řetezce Bitmap

- Řetezce FilePropertiesHashEx

- Řetezce FileVersion

- Řetezce Produktu

- Řetezce ProductVersion

- Řetezce Microsoft

- Řetezce Znění



## <a name="ccm_rax"></a>CCM_RAX

Obor názvů: root\ccm\cimodels

CCM_RAXInfo třídy


- Řetezce Identifikátor

- Řetezce FeedURL

- Řetezce Identifikátor UserSID



## <a name="cd-rom"></a>DISK CD-ROM

Obor názvů: root\cimv2

Win32_CDROMDrive třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- Řetezce CompressionMethod

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Řetezce Název

- Řetezce Disky

- Datového DriveIntegrity

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- UInt16 FileSystemFlags

- UInt32 FileSystemFlagsEx

- Řetezce ÚČET

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt64 MaxBlockSize

- UInt32 MaximumComponentLength

- UInt64 MaxMediaSize

- Datového MediaLoaded

- Řetezce Média

- UInt64 MinBlockSize

- Řetezce Jméno

- Datového NeedsCleaning

- UInt32 NumberOfMediaSupported

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce RevisionLevel

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt64 Hodnota

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Řetezce VolumeName

- Řetezce VolumeSerialNumber



## <a name="client-events"></a>Události klienta

Obor názvů: root\ccm\invagt

ClientEvents třídy


- Řetezce EventName

- UInt16 Výpočtu



## <a name="computer-system"></a>Systém počítače

Obor názvů: root\cimv2

Win32_ComputerSystem třídy


- Řetezce Jméno

- UInt16 AdminPasswordStatus

- Datového AutomaticResetBootOption

- Datového AutomaticResetCapability

- UInt16 BootOptionOnLimit

- UInt16 BootOptionOnWatchDog

- Datového BootROMSupported

- Řetezce BootupState

- Řetezce Popisku

- UInt16 ChassisBootupState

- (SInt16) CurrentTimeZone

- Datového DaylightInEffect

- Řetezce Název

- Řetezce Domain

- UInt16 Doménové role

- UInt16 FrontPanelResetStatus

- Datového InfraredSupported

- Řetezce InitialLoadInfo[]

- Hodnotu InstallDate

- UInt16 KeyboardPasswordStatus

- Řetezce LastLoadInfo

- Řetezce Výrobců

- Řetezce Vzorový

- Řetezce NameFormat

- Datového NetworkServerModeEnabled

- UInt32 NumberOfProcessors

- Řetezce OEMLogoBitmap

- Řetezce OEMStringArray[]

- (SInt64) PauseAfterReset

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 PowerOnPasswordStatus

- UInt16 PowerState

- UInt16 PowerSupplyState

- Řetezce PrimaryOwnerContact

- Řetezce PrimaryOwnerName

- UInt16 ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- Řetezce Role []

- Řetezce Stav

- Řetezce SupportContactDescription[]

- UInt16 SystemStartupDelay

- Řetezce SystemStartupOptions[]

- Uint8 SystemStartupSetting

- Řetezce SystemType

- UInt16 ThermalState

- UInt64 TotalPhysicalMemory

- Řetezce Jmen

- UInt16 WakeUpType



## <a name="computer-system-ex"></a>Počítačový systém ex

Obor názvů: root\cimv2

CCM_ComputerSystemExtended třídy


- Řetezce Jméno

- UInt16 PCSystemType



## <a name="computer-system-product"></a>Produkt počítačového systému

Obor názvů: root\cimv2

Win32_ComputerSystemProduct třídy


- Řetezce IdentifyingNumber

- Řetezce Jméno

- Řetezce Znění

- Řetezce Popisku

- Řetezce Název

- Řetezce SKUNumber

- Řetezce IDENTIFIKÁTOR

- Řetezce Dodavatelské



## <a name="sms-advanced-client-ports"></a>Rozšířený klient porty serveru SMS

Obor názvů: root\cimv2

Win32Reg_SMSAdvancedClientPorts třídy


- Řetezce Klíč InstanceKey

- UInt32 HttpsPortName

- UInt32 Vlastnost PortName



## <a name="sms-advanced-client-ssl-configurations"></a>Konfigurace serveru SMS Rozšířený klient SSL

Obor názvů: root\cimv2

Win32Reg_SMSAdvancedClientSSLConfiguration třídy


- Řetezce Klíč InstanceKey

- Řetezce CertificateSelectionCriteria

- Řetezce CertificateStore

- UInt32 ClientAlwaysOnInternet

- UInt32 HttpsStateFlags

- Řetezce InternetMPHostName

- UInt32 SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>Stav Rozšířený klient SMS

Obor názvů: root\ccm

CCM_InstalledComponent třídy


- Řetezce Jméno

- Řetezce DisplayName

- Řetezce Znění



## <a name="connected-device"></a>Připojené zařízení

Obor názvů: root\SmsDm

SMS_ActiveSyncConnectedDevice třídy


- Řetezce DeviceOEMInfo

- Řetezce DeviceType

- Řetezce OS_Major

- Řetezce OS_Minor

- Řetezce OS_Platform

- Řetezce ProcessorArchitecture

- Řetezce Processorlevel není

- Řetezce ProcessorRevision není

- Řetezce InstalledClientID

- Řetezce InstalledClientServer

- Řetezce InstalledClientVersion

- Řetezce LastSyncTime

- Řetezce OS_AdditionalInfo

- Řetezce OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

Obor názvů: Root\Cimv2\Sms

SMS_DefaultBrowser třídy


- Řetezce BrowserProgId



## <a name="desktop"></a>Aplikace klasické pracovní plochy

Obor názvů: root\cimv2

Win32_Desktop třídy


- Řetezce Jméno

- UInt32 Hodnota BorderWidth

- Řetezce Popisku

- Datového CoolSwitch

- UInt32 CursorBlinkRate

- Řetezce Název

- Datového DragFullWindows

- UInt32 GridGranularity

- UInt32 IconSpacing

- Řetezce IconTitleFaceName

- UInt32 IconTitleSize

- Datového IconTitleWrap

- Řetezce Vzorku

- Datového ScreenSaverActive

- Řetezce ScreenSaverExecutable

- Datového ScreenSaverSecure

- UInt32 ScreenSaverTimeout

- Řetezce Vlastnost SettingId

- Řetezce Lock

- Datového WallpaperStretched

- Datového WallpaperTiled



## <a name="desktop-monitor"></a>Stolní monitor

Obor názvů: root\cimv2

Win32_DesktopMonitor třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt32 Připojení

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt16 DisplayType

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- Datového IsLocked –

- UInt32 LastErrorCode

- Řetezce MonitorManufacturer

- Řetezce Elementu MonitorType

- Řetezce Jméno

- UInt32 PixelsPerXLogicalInch

- UInt32 PixelsPerYLogicalInch

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt32 ScreenHeight

- UInt32 ScreenWidth

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový



## <a name="device-info"></a>Informace o zařízení

Obor názvů: rezervovaný

Device_Info třídy


- Řetezce Platnost certifikátu

- Řetezce DeviceName

- Řetezce Výrobců

- Řetezce Vzorový

- Řetezce JINÉHO



## <a name="mdm-devdetail"></a>DevDetail MDM

Obor názvů: root\cimv2\mdm\dmmap

MDM_DevDetail_Ext01 třídy


- Řetezce InstanceID

- Řetezce ParentID

- Řetezce DeviceHardwareData

- Řetezce WLANMACAddress



## <a name="disk"></a>Disk

Obor názvů: root\cimv2

Win32_DiskDrive třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt32 BytesPerSector

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- Řetezce CompressionMethod

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- UInt32 Indexovacím

- Hodnotu InstallDate

- Řetezce InterfaceType

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- Datového MediaLoaded

- Řetezce Média

- UInt64 MinBlockSize

- Řetezce Vzorový

- Řetezce Jméno

- Datového NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Disk

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt32 SectorsPerTrack

- UInt64 Hodnota

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- UInt64 TotalCylinders

- UInt32 TotalHeads

- UInt64 TotalSectors

- UInt64 TotalTracks

- UInt32 TracksPerCylinder



## <a name="partition"></a>Oddíl

Obor názvů: root\cimv2

Win32_DiskPartition třídy


- Řetezce DeviceID

- UInt16 Stoupit

- UInt16 Dostupnosti

- UInt64 Velikostí bloku

- Datového Možností

- Datového BootPartition

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt32 DiskIndex

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- UInt32 HiddenSectors

- UInt32 Indexovacím

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Jméno

- UInt64 NumberOfBlocks

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Datového PrimaryPartition

- Řetezce Cílem

- Datového RewritePartition

- UInt64 Hodnota

- UInt64 StartingOffset

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Řetezce Textový



## <a name="dma"></a>DMA

Obor názvů: root\cimv2

Win32_DeviceMemoryAddress třídy

- UInt64 StartingAddress

- Řetezce Popisku

- Řetezce Název

- UInt64 EndingAddress

- Hodnotu InstallDate

- Řetezce MemoryType

- Řetezce Jméno

- Řetezce Stav



## <a name="dma-channel"></a>Kanál DMA

Obor názvů: root\cimv2

Win32_DMAChannel třídy


- UInt32 DMAChannel

- UInt16 AddressSize

- UInt16 Dostupnosti

- Datového BurstMode

- UInt16 ByteMode

- Řetezce Popisku

- UInt16 ChannelTiming

- Řetezce Název

- Hodnotu InstallDate

- UInt32 MaxTransferSize

- Řetezce Jméno

- UInt32 Přístavní

- Řetezce Stav

- UInt16 TransferWidths[]

- UInt16 TypeCTiming

- UInt16 WordMode



## <a name="driver---vxd"></a>Ovladač-VxD

Obor názvů: root\cimv2

Win32_DriverVXD třídy


- Řetezce Jméno

- Řetezce SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Řetezce Znění

- Řetezce BuildNumber

- Řetezce Popisku

- Řetezce CodeSet

- Řetezce Nad

- Řetezce Název

- Řetezce DeviceDescriptorBlock

- Řetezce IdentificationCode

- Hodnotu InstallDate

- Řetezce LanguageEdition

- Řetezce Výrobců

- Řetezce OtherTargetOS

- Řetezce PM_API

- Řetezce Sériové

- UInt32 ServiceTableSize

- Řetezce Stav

- Řetezce V86_API



## <a name="embedded-device-information"></a>Informace o integrovaném zařízení

Obor názvů: Root\Cimv2\Sms

CCM_EmbeddedDeviceInformation třídy


- Řetezce DeviceType

- Řetezce Vzorový

- Řetezce OEMName



## <a name="environment"></a>Prostředí

Obor názvů: root\cimv2

Win32_Environment třídy


- Řetezce Jméno

- Řetezce Jmen

- Řetezce Popisku

- Řetezce Název

- Hodnotu InstallDate

- Řetezce Stav

- Datového SystemVariable

- Řetezce VariableValue



## <a name="firmware"></a>Firmware

Obor názvů: Root\Cimv2\Sms

SMS_Firmware třídy


- Datového UEFI

- Datového Funkce SecureBoot



## <a name="usm-folder-redirection-health"></a>Stav přesměrování složky USM

Obor názvů: Root\Cimv2\Sms

SMS_FolderRedirectionHealth třídy


- Řetezce FolderName

- Řetezce ID

- Uint8 Funkčnosti

- Hodnotu LastSuccessfulSyncTime

- Uint8 LastSyncStatus

- Hodnotu LastSyncTime

- Datového OfflineAccessEnabled

- Řetezce OfflineFileNameFolderGUID

- Datového Přesměrován



## <a name="ide-controller"></a>Kontroler IDE

Obor názvů: root\cimv2

Win32_IDEController třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="add-remove-programs-64"></a>Přidat odebrat programy (64)

Obor názvů: root\cimv2

Win32Reg_AddRemovePrograms64 třídy


- Řetezce ProdID

- Řetezce DisplayName

- Řetezce InstallDate

- Řetezce Microsoft

- Řetezce Znění



## <a name="add-remove-programs"></a>Přidat nebo odebrat programy

Obor názvů: root\cimv2

Win32Reg_AddRemovePrograms třídy


- Řetezce ProdID

- Řetezce DisplayName

- Řetezce InstallDate

- Řetezce Microsoft

- Řetezce Znění



## <a name="installed-executable"></a>Instalovaný spustitelný soubor

Obor názvů: Root\Cimv2\Sms

SMS_InstalledExecutable třídy


- Řetezce Spustitelný soubor

- Řetezce ProductCode

- Řetezce BinFileVersion

- Řetezce BinProductVersion

- Řetezce Název

- Řetezce FilePropertiesHash

- Řetezce FilePropertiesHashEx

- UInt32 Velikost souboru

- Řetezce FileVersion

- Datového HasPatchAdded

- Řetezce InstalledFilePath

- Datového IsSystemFile

- Datového IsVitalFile

- UInt32 Language

- Řetezce Produktu

- Řetezce ProductVersion

- Řetezce Microsoft



## <a name="installed-software"></a>Nainstalovaný software

Obor názvů: Root\Cimv2\Sms

SMS_InstalledSoftware třídy


- Řetezce SoftwareCode

- Řetezce ARPDisplayName

- Řetezce ChannelCode

- Řetezce ChannelID

- Řetezce CM_DSLID

- Řetezce EvidenceSource

- Hodnotu InstallDate

- UInt32 InstallDirectoryValidation

- Řetezce InstalledLocation

- Řetezce InstallSource

- UInt32 InstallType

- UInt32 Language

- Řetezce LocalPackage

- Řetezce MPC

- UInt32 OsComponent

- Řetezce PackageCode

- Řetezce ProductID

- Řetezce NázevVýrobku

- Řetezce ProductVersion

- Řetezce Microsoft

- Řetezce RegisteredUser

- Řetezce ServicePack

- Řetezce SoftwarePropertiesHash

- Řetezce SoftwarePropertiesHashEx

- Řetezce UninstallString

- Řetezce UpgradeCode

- UInt32 VersionMajor

- UInt32 VersionMinor



## <a name="irq-table"></a>Tabulka IRQ

Obor názvů: root\cimv2

Win32_IRQResource třídy


- UInt32 IRQNumber

- UInt16 Dostupnosti

- Řetezce Popisku

- Řetezce Název

- Datového Zařízení

- Hodnotu InstallDate

- Řetezce Jméno

- Datového Ke sdílení

- Řetezce Stav

- UInt16 TriggerLevel

- UInt16 TriggerType

- UInt32 Vektorový



## <a name="keyboard"></a>Klávesnice

Obor názvů: root\cimv2

Win32_Keyboard třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- Datového IsLocked –

- UInt32 LastErrorCode

- Řetezce Rozložení

- Řetezce Jméno

- UInt16 NumberOfFunctionKeys

- UInt16 Zadáno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový



## <a name="load-order-group"></a>Skupina pořadí načtení

Obor názvů: root\cimv2

Win32_LoadOrderGroup třídy


- Řetezce Jméno

- Řetezce Popisku

- Řetezce Název

- Datového DriverEnabled

- UInt32 GroupOrder

- Hodnotu InstallDate

- Řetezce Stav



## <a name="logical-disk"></a>Logický disk

Obor názvů: Root\Cimv2\Sms

SMS_LogicalDisk třídy


- Řetezce DeviceID

- UInt16 Stoupit

- UInt16 Dostupnosti

- UInt64 Velikostí bloku

- Řetezce Popisku

- Datového Komprimován

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt32 DriveType

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- Řetezce Systému souborů

- UInt64 FreeSpace

- Hodnotu InstallDate

- UInt32 LastErrorCode

- UInt32 MaximumComponentLength

- UInt32 Média

- Řetezce Jméno

- UInt64 NumberOfBlocks

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce ProviderName

- Řetezce Cílem

- UInt64 Hodnota

- Řetezce Stav

- UInt16 StatusInfo

- Datového SupportsFileBasedCompression

- Řetezce Systémový

- Řetezce VolumeName

- Řetezce VolumeSerialNumber



## <a name="memory"></a>Memory (Paměť)

Obor názvů: root\cimv2

CCM_LogicalMemoryConfiguration třídy


- Řetezce Jméno

- UInt64 AvailableVirtualMemory

- UInt64 TotalPageFileSpace

- UInt64 TotalPhysicalMemory

- UInt64 TotalVirtualMemory



## <a name="device-bluetooth"></a>Bluetooth zařízení

Obor názvů: rezervovaný

Device_Bluetooth třídy


- Datového Umožněn



## <a name="device-camera"></a>Kamera zařízení

Obor názvů: rezervovaný

Device_Camera třídy


- Datového Umožněn



## <a name="device-certificates"></a>Certifikáty zařízení

Obor názvů: rezervovaný

Device_Certificates třídy


- Řetezce Kryptografický

- Řetezce Textový

- Řetezce IssuedBy

- Řetezce IssuedTo

- Hodnotu ValidFrom

- Hodnotu ValidTo



## <a name="device-client"></a>Klient zařízení

Obor názvů: rezervovaný

Device_Client třídy


- Datového DownloadWhenRoaming

- Datového SyncWhenRoaming



## <a name="device-client-agent-version"></a>Verze klientského agenta zařízení

Obor názvů: rezervovaný

Device_ClientAgentVersion třídy


- Řetezce Znění



## <a name="device-computer-system"></a>Počítačový systém zařízení

Obor názvů: rezervovaný

Device_ComputerSystem třídy


- Řetezce CellularTechnology

- Řetezce DeviceClientID

- Řetezce DeviceManufacturer

- Řetezce DeviceModel

- Řetezce DMVersion

- Řetezce FirmwareVersion

- Řetezce HardwareVersion

- Řetezce IMEI

- Řetezce IMSI

- Uint8 IsActivationLockEnabled

- Uint8 Jailbreak

- Řetezce MEID

- Řetezce OEM

- Řetezce PhoneNumber

- Řetezce PlatformType

- UInt32 ProcessorArchitecture

- UInt32 Processorlevel není

- UInt32 ProcessorRevision není

- Řetezce Produktu

- Řetezce ProductVersion

- Řetezce Sériové

- Řetezce SoftwareVersion

- Řetezce SubscriberCarrierNetwork



## <a name="device-display"></a>Zobrazení zařízení

Obor názvů: rezervovaný

Device_Display třídy


- UInt32 HorizontalResolution

- UInt64 NumberOfColors

- UInt32 VerticalResolution



## <a name="device-email"></a>E-mail zařízení

Obor názvů: rezervovaný

Device_Email třídy


- Řetezce OwnerEmailAddress

- Řetezce SyncDomain

- Řetezce SyncServer

- Řetezce SyncUser

- Řetezce Textový



## <a name="device-encryption"></a>Šifrování zařízení

Obor názvů: rezervovaný

Device_Encryption třídy


- UInt32 EmailEncryptionAlgorithm

- UInt32 EmailEncryptionNegotiation

- Datového EmailEncryptionRequired

- Datového EmailSigningAlgorithm

- Datového EmailSigningRequired

- Datového EncryptionCompliance

- Datového PhoneMemoryEncrypted

- Datového StorageCardEncrypted



## <a name="device-exchange"></a>Výměna zařízení

Obor názvů: rezervovaný

Device_Exchange třídy


- Datového ConflictResolution

- (SInt32) HTMLEmailTruncation

- UInt32 MailFormat

- UInt32 MaxCalendarAge

- UInt32 MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- UInt32 OffPeakSyncFrequency

- UInt32 PeakDays

- Řetezce PeakEndTime

- Řetezce PeakStartTime

- UInt32 PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- Datového SendEmailImmediately

- Datového SyncCalendar

- Datového SyncContacts

- Datového SyncEmail

- Datového SyncTasks

- Datového SyncWhenRoaming



## <a name="device-installed-applications"></a>Instalované aplikace zařízení

Obor názvů: rezervovaný

Device_InstalledApplications třídy


- Řetezce Jméno

- Řetezce Znění



## <a name="device-irda"></a>Zařízení IrDA

Obor názvů: rezervovaný

Device_IrDA třídy


- Datového Umožněn



## <a name="mobile-device-location"></a>Umístění mobilního zařízení

Obor názvů: rezervovaný

MDM_RemoteFind třídy


- (Real32) Šířce

- (Real32) Bodu



## <a name="device-memory"></a>Paměť zařízení

Obor názvů: rezervovaný

Device_Memory třídy


- UInt64 ProgramFree

- UInt64 ProgramTotal

- UInt64 RemovableStorageFree

- UInt64 RemovableStorageTotal

- UInt64 StorageFree

- UInt64 StorageTotal



## <a name="device-os-information"></a>Informace o operačním systému zařízení

Obor názvů: rezervovaný

Device_OSInformation třídy


- Řetezce Language

- Řetezce Platformy

- Řetezce Znění



## <a name="device-password"></a>Heslo zařízení

Obor názvů: rezervovaný

Device_Password třídy


- Datového AllowRecoveryPassword

- UInt32 AutolockTimeout

- Datového Umožněn

- UInt32 Vypršení platnosti

- UInt32 Historie

- UInt32 MaxAttemptsBeforeWipe

- UInt32 MinComplexChars

- UInt32 MinLength

- Uint8 PasswordQuality

- UInt32 Textový



## <a name="device-policy"></a>Zásady zařízení

Obor názvů: rezervovaný

Device_Policy třídy


- Řetezce Jméno

- Datového Vynucuje



## <a name="device-power"></a>Výkon zařízení

Obor názvů: rezervovaný

Device_Power třídy


- UInt32 BacklightACTimeout

- UInt32 BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) BatteryPercent



## <a name="mobile-device-security-status"></a>Stav zabezpečení mobilního zařízení

Obor názvů: rezervovaný

MDM_SecurityStatus třídy


- UInt32 HardwareEncryptionCaps

- Uint8 PasscodeCompliant

- Uint8 PasscodeCompliantWithProfiles

- Uint8 PasscodePresent

- Uint8 RequireEncryption



## <a name="device-windows-security-policy"></a>Zásady zabezpečení pro zařízení se systémem Windows

Obor názvů: rezervovaný

Device_WindowsSecurityPolicy třídy


- UInt32 ÚČET

- Řetezce Jméno

- UInt32 Osa



## <a name="device-wlan"></a>SÍŤ WLAN zařízení

Obor názvů: rezervovaný

Device_WLAN třídy


- Datového Umožněn

- Řetezce EthernetMAC

- Řetezce WiFiMAC



## <a name="modem"></a>Údajů

Obor názvů: root\cimv2

Win32_POTSModem třídy


- Řetezce DeviceID

- UInt16 AnswerMode

- Řetezce AttachedTo

- UInt16 Dostupnosti

- Řetezce BlindOff

- Řetezce BlindOn

- Řetezce Popisku

- Řetezce CompatibilityFlags

- UInt16 CompressionInfo

- Řetezce CompressionOff

- Řetezce CompressionOn

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce ConfigurationDialog

- Řetezce CountriesSupported[]

- Řetezce CountrySelected

- Řetezce CurrentPasswords[]

- Řetezce DCB

- Řetezce Výchozí

- Řetezce Název

- Řetezce DeviceLoader

- Řetezce DeviceType

- UInt16 DialType

- Hodnotu DriverDate

- Datového ErrorCleared

- Řetezce ErrorControlForced

- UInt16 ErrorControlInfo

- Řetezce ErrorControlOff

- Řetezce ErrorControlOn

- Řetezce ErrorDescription

- Řetezce FlowControlHard

- Řetezce FlowControlOff

- Řetezce FlowControlSoft

- Řetezce InactivityScale

- UInt32 InactivityTimeout

- UInt32 Indexovacím

- Hodnotu InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRateToPhone

- UInt32 MaxBaudRateToSerialPort

- UInt16 MaxNumberOfPasswords

- Řetezce Vzorový

- Řetezce ModemInfPath

- Řetezce ModemInfSection

- Řetezce ModulationBell

- Řetezce ModulationCCITT

- UInt16 ModulationScheme

- Řetezce Jméno

- Řetezce PNPDeviceID

- Řetezce PortSubClass

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce Směr

- Řetezce Vlastnosti

- Řetezce ProviderName

- Řetezce Volba

- Řetezce Nové

- Řetezce ResponsesKeyName

- Uint8 RingsBeforeAnswer

- Řetezce SpeakerModeDial

- Řetezce SpeakerModeOff

- Řetezce SpeakerModeOn

- Řetezce SpeakerModeSetup

- Řetezce SpeakerVolumeHigh

- UInt16 SpeakerVolumeInfo

- Řetezce SpeakerVolumeLow

- Řetezce SpeakerVolumeMed

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce StringFormat –

- Datového SupportsCallback

- Datového SupportsSynchronousConnect

- Řetezce Systémový

- Řetezce Koncové

- Hodnotu TimeOfLastReset

- Řetezce Oznamovací

- Řetezce VoiceSwitchFeature



## <a name="motherboard"></a>Základní desky

Obor názvů: root\cimv2

Win32_MotherboardDevice třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce PrimaryBusType

- Řetezce RevisionNumber

- Řetezce SecondaryBusType

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový


## <a name="nap-client"></a>Klient NAP

Obor názvů: root\Nap

NAP_Client třídy


- (Řetězec) název

- (Řetězec) Popis

- (String) fixupURL

- (Boolean) napEnabled

- (String) napProtocolVersion

- (String) probationTime

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>Agent stavu systému NAP

Obor názvů: root\Nap

NAP_SystemHealthAgent třídy


- UInt32 ÚČET

- (Řetězec) Popis

- (UInt32) fixupState

- (String) friendlyName

- (String) infoClsid

- (Logická) omezení

- (UInt8) procento

- (String) registrationDate

- (String) dodavatel

- (Řetězec) verze



## <a name="network-adapter"></a>Síťový adaptér

Obor názvů: root\cimv2

Win32_NetworkAdapter třídy


- Řetezce DeviceID

- Řetezce AdapterType

- Datového Automatické rozpoznávání

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt32 Indexovacím

- Hodnotu InstallDate

- Datového Instalovat

- UInt32 LastErrorCode

- Řetezce MACAddress

- Řetezce Výrobců

- UInt32 MaxNumberControlled

- UInt64 MaxSpeed

- Řetezce Jméno

- Řetezce NetworkAddresses []

- Řetezce PermanentAddress

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce NázevVýrobku

- Řetezce ServiceName

- UInt64 Takt

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="network-adapter-configuration"></a>Konfigurace síťového adaptéru

Obor názvů: root\cimv2

Win32_NetworkAdapterConfiguration třídy


- UInt32 Indexovacím

- Datového ArpAlwaysSourceRoute

- Datového ArpUseEtherSNAP

- Řetezce Popisku

- Řetezce DatabasePath

- Datového DeadGWDetectEnabled

- Řetezce DefaultIPGateway[]

- Uint8 DefaultTOS

- Uint8 DefaultTTL

- Řetezce Název

- Datového DHCPEnabled

- Hodnotu DHCPLeaseExpires

- Hodnotu DHCPLeaseObtained

- Řetezce DHCPServer

- Řetezce DNSDomain

- Řetezce DNSDomainSuffixSearchOrder[]

- Datového DNSEnabledForWINSResolution

- Řetezce Atribut

- Řetezce DNSServerSearchOrder[]

- Datového DomainDNSRegistrationEnabled

- UInt32 ForwardBufferMemory

- Datového FullDNSRegistrationEnabled

- UInt16 GatewayCostMetric[]

- Uint8 IGMPLevel

- Řetezce IPAddress []

- UInt32 IPConnectionMetric

- Datového IPEnabled

- Datového IPFilterSecurityEnabled

- Datového IPPortSecurityEnabled

- Řetezce IPSecPermitIPProtocols[]

- Řetezce IPSecPermitTCPPorts[]

- Řetezce IPSecPermitUDPPorts[]

- Řetezce Podsítě IPSubnet prostřednictvím []

- Datového IPUseZeroBroadcast

- Řetezce IPXAddress

- Datového IPXEnabled

- Řetezce IPXFrameType

- UInt32 IPXMediaType

- Řetezce IPXNetworkNumber[]

- Řetezce IPXVirtualNetNumber

- UInt32 KeepAliveInterval

- UInt32 KeepAliveTime

- Řetezce MACAddress

- UInt32 HODNOTU

- UInt32 NumForwardPackets

- Datového PMTUBHDetectEnabled

- Datového PMTUDiscoveryEnabled

- Řetezce ServiceName

- Řetezce Vlastnost SettingId

- UInt32 TcpipNetbiosOptions

- UInt32 TcpMaxConnectRetransmissions

- UInt32 TcpMaxDataRetransmissions

- UInt32 TcpNumConnections

- Datového TcpUseRFC1122UrgentPointer

- UInt16 TcpWindowSize

- Datového WINSEnableLMHostsLookup

- Řetezce WINSHostLookupFile

- Řetezce WINSPrimaryServer

- Řetezce WINSScopeID

- Řetezce WINSSecondaryServer



## <a name="network-client"></a>Síťový klient

Obor názvů: root\cimv2

Win32_NetworkClient třídy


- Řetezce Jméno

- Řetezce Popisku

- Řetezce Název

- Hodnotu InstallDate

- Řetezce Výrobců

- Řetezce Stav



## <a name="network-login-profile"></a>Profil přihlášení k síti

Obor názvů: root\cimv2

Win32_NetworkLoginProfile třídy


- Řetezce Jméno

- Hodnotu AccountExpires

- UInt32 AuthorizationFlags

- UInt32 BadPasswordCount

- Řetezce Popisku

- UInt32 Stránky

- Řetezce Vytvořena

- UInt32 CountryCode

- Řetezce Název

- UInt32 Flag

- Řetezce FullName

- Řetezce HomeDirectory

- Řetezce HomeDirectoryDrive

- Hodnotu LastLogoff

- Hodnotu LastLogon

- Řetezce LogonHours

- Řetezce LogonServer

- UInt64 MaximumStorage

- UInt32 NumberOfLogons

- Řetezce Ukazatelů

- Hodnotu Heslo

- Hodnotu PasswordExpires

- UInt32 PrimaryGroupId

- UInt32 Požadovaná

- Řetezce Profilu

- Řetezce ScriptPath

- Řetezce Vlastnost SettingId

- UInt32 UnitsPerWeek

- Řetezce UserComment

- UInt32 UserId

- Řetezce UserType

- Řetezce Výběru



## <a name="nt-eventlog-file"></a>Soubor protokolu událostí NT

Obor názvů: root\cimv2

Win32_NTEventlogFile třídy


- Řetezce Jméno

- UInt32 AccessMask

- Datového Zálohovat

- Řetezce Popisku

- Datového Komprimován

- Řetezce CompressionMethod

- Hodnotu CreationDate

- Řetezce Název

- Řetezce Disky

- Řetezce EightDotThreeFileName

- Datového Šifrovaná

- Řetezce EncryptionMethod

- Řetezce Klapk

- Řetezce Bitmap

- UInt64 Velikost souboru

- Řetezce FileType

- Řetezce FSName

- Datového Neobsahuje

- Hodnotu InstallDate

- UInt64 InUseCount

- Hodnotu LastAccessed

- Hodnotu LastModified

- Řetezce Logfile

- Řetezce Výrobců

- UInt32 MaxFileSize

- UInt32 PočetZáznamů

- UInt32 OverwriteOutDated

- Řetezce OverWritePolicy

- Řetezce Dílčí

- Datového Čitelný

- Řetezce Zdroje []

- Řetezce Stav

- Datového Souborů

- Řetezce Znění

- Datového Zapisovatelné



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

Obor názvů: root\cimv2

Office365ProPlusConfigurations třídy


- Řetezce Klíče

- Řetezce AutoUpgrade

- Řetezce CCMManaged

- Řetezce CDNBaseUrl

- (String) cfgUpdateChannel

- Řetezce ClientCulture

- Řetezce ClientFolder

- Řetezce GPOChannel

- Řetezce GPOOfficeMgmtCOM

- Řetezce InstallationPath

- Řetezce LastScenario

- Řetezce LastScenarioResult

- Řetezce OfficeMgmtCOM

- Řetezce Platformy

- Řetezce Sdílení počítačových licencí

- Řetezce UpdateChannel

- Řetezce UpdatePath

- Řetezce UpdatesEnabled

- Řetezce UpdateUrl

- Řetezce VersionToReport



## <a name="office-addin"></a>Doplněk Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeAddin třídy


- Řetezce Architektura

- Řetezce ÚČET

- Řetezce OfficeApp

- Řetezce Textový

- UInt32 AverageLoadTimeInMilliseconds

- Řetezce CLSID

- Řetezce Společnosti

- UInt32 CrashCount

- Řetezce Název

- UInt32 ErrorCount

- Řetezce Bitmap

- UInt64 Velikost souboru

- UInt32 Časové razítko

- Řetezce FileVersion

- Řetezce FriendlyName

- Řetezce FriendlyNameHash

- Řetezce IdHash

- UInt32 LoadBehavior

- UInt32 LoadCount

- UInt32 LoadFailCount

- Řetezce NázevVýrobku

- Řetezce ProductVersion



## <a name="office-client-metric"></a>Metrika klienta Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeClientMetric třídy


- Řetezce OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashedSessionCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- UInt32 SessionCount



## <a name="office-device-summary"></a>Souhrn zařízení Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeDeviceSummary třídy


- Datového IsProPlusInstalled

- Datového IsTelemetryEnabled



## <a name="office-document-metric"></a>Metrika dokumentů Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeDocumentMetric třídy


- Řetezce OfficeApp

- UInt32 TotalCloudDocs

- UInt32 TotalLegacyDocs

- UInt32 TotalLocalDocs

- UInt32 TotalMacroDocs

- UInt32 TotalNonMacroDocs

- UInt32 TotalUncDocs



## <a name="office-document-solution"></a>Řešení dokumentu Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeDocumentSolution třídy


- Řetezce DocumentSolutionId

- Řetezce OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashCount

- Řetezce ExampleFileName

- UInt32 LoadCount

- UInt32 LoadFailCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- Řetezce Textový



## <a name="office-macro-error"></a>Chyba makra Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeMacroError třídy


- Řetezce DocumentSolutionId

- UInt32 ErrorCode

- UInt32 Výpočtu

- UInt64 LastOccurrence

- Řetezce Textový



## <a name="office-product-info"></a>Informace o produktu Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeProductInfo třídy


- Řetezce NázevVýrobku

- Řetezce ProductVersion

- Řetezce Architektura

- Řetezce Kanál

- UInt32 IsProPlusInstalled

- Řetezce Language

- Řetezce LicenseState



## <a name="office-vba-rule-violation"></a>Porušení pravidel Office VBA

Obor názvů: root\ccm\InvAgt

CCM_OfficeVbaRuleViolation třídy


- UInt32 RuleId

- UInt32 FileCount

- Řetezce OfficeApp



## <a name="office-vbasummary"></a>VbaSummary Office

Obor názvů: root\ccm\InvAgt

CCM_OfficeVbaScanResultsSummary třídy


- UInt32 Vytvořit

- UInt32 Design64

- UInt32 DuplicateVba

- Datového HasResults

- UInt32 HasVba

- UInt32 Nepřístupný

- UInt32 Chyba

- UInt32 Issues64

- UInt32 IssuesNone

- UInt32 IssuesNone64

- UInt32 Uzamčení

- UInt32 NoVba

- UInt32 Proti

- UInt32 RemLimited

- UInt32 RemLimited64

- UInt32 RemSignificant

- UInt32 RemSignificant64

- UInt32 Podtržítk

- UInt32 Score64

- UInt32 Čtení

- UInt32 Export

- UInt32 Validation64



## <a name="operating-system"></a>Operační systém

Obor názvů: root\cimv2

Win32_OperatingSystem třídy


- Řetezce Jméno

- Řetezce BootDevice

- Řetezce BuildNumber

- Řetezce BuildType

- Řetezce Popisku

- Řetezce CodeSet

- Řetezce CountryCode

- Řetezce CSDVersion

- (SInt16) CurrentTimeZone

- Datového Ladí

- Řetezce Název

- Datového Místě

- Uint8 ForegroundApplicationBoost

- UInt64 FreePhysicalMemory

- UInt64 FreeSpaceInPagingFiles

- UInt64 FreeVirtualMemory

- Hodnotu InstallDate

- Hodnotu LastBootUpTime

- Hodnotu LocalDateTime

- Řetezce Jazyka

- Řetezce Výrobců

- UInt32 MaxNumberOfProcesses

- UInt64 MaxProcessMemorySize

- Řetezce MUILanguages[]

- UInt32 NumberOfLicensedUsers

- UInt32 NumberOfProcesses

- UInt32 NumberOfUsers

- UInt32 OperatingSystemSKU

- Řetezce Vaší

- Řetezce OSArchitecture

- UInt32 OSLanguage

- UInt32 OSProductSuite

- UInt16 OSType

- Řetezce OtherTypeDescription

- Řetezce PlusProductID

- Řetezce PlusVersionNumber

- Datového Primární

- UInt32 ProductType

- Řetezce RegisteredUser

- Řetezce Sériové

- UInt16 ServicePackMajorVersion

- UInt16 ServicePackMinorVersion

- UInt64 SizeStoredInPagingFiles

- Řetezce Stav

- Řetezce SystemDevice

- Řetezce SystemDirectory

- UInt64 TotalSwapSpaceSize

- UInt64 TotalVirtualMemorySize

- UInt64 TotalVisibleMemorySize

- Řetezce Znění

- Řetezce WindowsDirectory



## <a name="operating-system-ex"></a>Operační systém ex

Obor názvů: root\cimv2

CCM_OperatingSystemExtended třídy


- Řetezce Jméno

- UInt32 SKLADOVÉ



## <a name="operating-system-recovery-configuration"></a>Konfigurace obnovení operačního systému

Obor názvů: root\cimv2

Win32_OSRecoveryConfiguration třídy


- Řetezce Jméno

- Datového AutoRestart

- Řetezce Popisku

- Řetezce DebugFilePath

- Řetezce Název

- Datového KernelDumpOnly

- Datového OverwriteExistingDebugFile

- Datového SendAdminAlert

- Řetezce Vlastnost SettingId

- Datového WriteDebugInfo

- Datového WriteToSystemLog



## <a name="optional-feature"></a>Volitelná funkce

Obor názvů: root\cimv2

Win32_OptionalFeature třídy


- Řetezce Jméno

- Řetezce Popisku

- Řetezce Název

- Hodnotu InstallDate

- UInt32 InstallState

- Řetezce Stav



## <a name="page-file-setting"></a>Nastavení stránkovacího souboru

Obor názvů: root\cimv2

Win32_PageFileSetting třídy


- Řetezce Jméno

- Řetezce Popisku

- Řetezce Název

- UInt32 InitialSize

- UInt32 MaximumSize objektu Form

- Řetezce Vlastnost SettingId



## <a name="parallel-port"></a>Paralelní port

Obor názvů: root\cimv2

Win32_ParallelPort třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového DMASupport

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Datového OSAutoDiscovered

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="bios"></a>SYSTÉMU BIOS

Obor názvů: root\cimv2

Win32_BIOS třídy


- Řetezce Jméno

- Řetezce SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Řetezce Znění

- UInt16 BiosCharacteristics[]

- Řetezce BIOSVersion[]

- Řetezce BuildNumber

- Řetezce Popisku

- Řetezce CodeSet

- Řetezce CurrentLanguage

- Řetezce Název

- Řetezce IdentificationCode

- UInt16 InstallableLanguages

- Hodnotu InstallDate

- Řetezce LanguageEdition

- Řetezce ListOfLanguages[]

- Řetezce Výrobců

- Řetezce OtherTargetOS

- Datového PrimaryBIOS

- Hodnotu ReleaseDate

- Řetezce Sériové

- Řetezce SMBIOSBIOSVersion

- UInt16 SMBIOSMajorVersion

- UInt16 SMBIOSMinorVersion

- Datového SMBIOSPresent

- Řetezce Stav



## <a name="pcmcia-controller"></a>Řadič PCMCIA

Obor názvů: root\cimv2

Win32_PCMCIAController třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="physical-memory"></a>Fyzická paměť

Obor názvů: root\cimv2

Win32_PhysicalMemory třídy


- Řetezce CreationClassName

- Řetezce Inteligentní

- Řetezce BankLabel

- UInt64 Klíčivost

- Řetezce Popisku

- UInt16 Šířka DataWidth

- Řetezce Název

- Řetezce DeviceLocator

- UInt16 FormFactor

- Datového HotSwappable

- Hodnotu InstallDate

- UInt16 InterleaveDataDepth

- UInt32 InterleavePosition

- Řetezce Výrobců

- UInt16 MemoryType

- Řetezce Vzorový

- Řetezce Jméno

- Řetezce OtherIdentifyingInfo

- Řetezce PartNumber

- UInt32 PositionInRow

- Datového PoweredOn

- Datového Disket

- Datového Replaceable

- Řetezce Sériové

- Řetezce SKLADOVÉ

- UInt32 Takt

- Řetezce Stav

- UInt16 TotalWidth

- UInt16 TypeDetail

- Řetezce Znění



## <a name="physicaldisk"></a>PhysicalDisk

Obor názvů: root\microsoft\windows\storage

MSFT_PhysicalDisk třídy


- Řetezce Objektu

- UInt64 AllocatedSize

- UInt16 BusType

- UInt16 CannotPoolReason[]

- Datového CanPool

- Řetezce Název

- Řetezce DeviceId

- UInt16 Pole enclosurenumber

- Řetezce FirmwareVersion

- Řetezce FriendlyName

- UInt16 Funkčnosti

- Datového IsIndicationEnabled

- Datového Částečně

- UInt64 LogicalSectorSize

- Řetezce Výrobců

- UInt16 Média

- Řetezce Vzorový

- UInt16 Provozním []

- Řetezce OtherCannotPoolReasonDescription

- Řetezce PartNumber

- Řetezce PhysicalLocation

- UInt64 PhysicalSectorSize

- Řetezce Sériové

- UInt64 Hodnota

- UInt16 SlotNumber

- Řetezce SoftwareVersion

- UInt32 SpindleSpeed

- UInt16 SupportedUsages[]

- Řetezce Identifikátor

- UInt16 Využívání



## <a name="pnp-device-driver"></a>OVLADAČ ZAŘÍZENÍ PNP

Obor názvů: root\cimv2

Win32_PnpEntity třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- Řetezce ClassGuid

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce CreationClassName

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce Službám

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce SystemCreationClassName

- Řetezce Systémový



## <a name="pointing-device"></a>Polohovací zařízení

Obor názvů: root\cimv2

Win32_PointingDevice třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt16 DeviceInterface

- UInt32 DoubleSpeedThreshold

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt16 Levé

- Řetezce HardwareType

- Řetezce InfFileName

- Řetezce InfSection

- Hodnotu InstallDate

- Datového IsLocked –

- UInt32 LastErrorCode

- Řetezce Výrobců

- Řetezce Jméno

- Uint8 NumberOfButtons

- Řetezce PNPDeviceID

- UInt16 PointingType

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt32 QuadSpeedThreshold

- UInt32 Rozhodnutí

- UInt32 SampleRate

- Řetezce Stav

- UInt16 StatusInfo

- UInt32 Synchronizace

- Řetezce Systémový



## <a name="portable-battery"></a>Přenosná baterie

Obor názvů: root\cimv2

Win32_PortableBattery třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt16 BatteryStatus

- UInt16 CapacityMultiplier

- Řetezce Popisku

- UInt16 Složení

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime (

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Oblasti

- Řetezce ManufactureDate

- Řetezce Výrobců

- UInt16 MaxBatteryError

- UInt32 MaxRechargeTime

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce SmartBatteryVersion

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="ports"></a>Porty

Obor názvů: root\cimv2

Win32_PortResource třídy

- UInt64 StartingAddress

- Datového Zástupný

- Řetezce Popisku

- Řetezce Název

- UInt64 EndingAddress

- Hodnotu InstallDate

- Řetezce Jméno

- Řetezce Stav



## <a name="power-capabilities"></a>Možnosti napájení

Obor názvů: root\CCM\powermanagementagent

CCM_PwrMgmtSystemPowerCapabilities třídy


- UInt32 PreferredPMProfile

- Datového ApmPresent

- Datového BatteriesAreShortTerm

- Datového FullWake

- Datového LidPresent

- Řetezce MinDeviceWakeState

- Datového ProcessorThrottle

- Řetezce RtcWake

- Datového SystemBatteriesPresent

- Datového SystemS1

- Datového SystemS2

- Datového SystemS3

- Datového SystemS4

- Datového SystemS5

- Datového UpsPresent

- Datového VideoDimPresent



## <a name="power-configurations"></a>Konfigurace napájení

Obor názvů: root\CCM\policy\machine\actualconfig

CCM_PowerConfig třídy


- Řetezce PowerConfigID

- UInt32 DurationInSec

- Řetezce NonPeakPowerPlan

- Řetezce NonPeakPowerPlanName

- Řetezce PeakPowerPlan

- Řetezce PeakPowerPlanName

- Řetezce PeakStartTimeHoursMin

- Řetezce WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>Důvody režimu spánku řízení spotřeby

Obor názvů: root\CCM\powermanagementagent

CCM_PwrMgmtLastSuspendError třídy


- Řetezce Žadatel

- Řetezce RequesterType

- Řetezce Třídy

- Hodnotu Interval

- UInt32 AdditionalCode

- Řetezce AdditionalInfo

- Řetezce RequesterInfo

- Datového UnknownRequester



## <a name="power-management-daily"></a>Denní řízení spotřeby

Obor názvů: root\CCM\powermanagementagent

CCM_PwrMgmtActualDay třídy


- Hodnotu Datum

- Řetezce TypeOfEvent

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



## <a name="power-client-opt-out-settings"></a>Nastavení odhlášení z klienta Power Client

Obor názvů: root\ccm\ClientSDK

CCM_PowerManagementClientOptoutSetting třídy


- Datového AdminAllowOptout

- Datového EffectiveClientOptOut

- Datového IsClientOptOut



## <a name="power-management-monthly"></a>Řízení spotřeby měsíčně

Obor názvů: root\CCM\powermanagementagent

CCM_PwrMgmtMonth třídy


- Hodnotu MonthStart

- (UInt32) minutesComputerActive

- (UInt32) minutesComputerOn

- (UInt32) minutesComputerShutdown

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- Řetezce TypeOfEvent



## <a name="power-settings"></a>Nastavení napájení

Obor názvů: Root\Cimv2\Sms

SMS_PowerSettings třídy


- Řetezce HLAVNÍCH

- Řetezce ACSettingIndex

- Řetezce ACValue

- Řetezce DCSettingIndex

- Řetezce DCValue

- Řetezce Jméno

- Řetezce UnitSpecifier



## <a name="print-jobs"></a>Tiskové úlohy

Obor názvů: root\cimv2

Win32_PrintJob třídy


- Řetezce Jméno

- Řetezce Popisku

- Řetezce Programátor

- Řetezce Název

- Řetezce Dokumentů

- Řetezce Ovladač ovladače

- Hodnotu ElapsedTime

- Řetezce HostPrintQueue

- Hodnotu InstallDate

- UInt32 Úlohy

- Řetezce Element JobStatus

- Řetezce Upozorněn

- Řetezce Owner

- UInt32 PagesPrinted

- Řetezce Ukazatelů

- Řetezce PrintProcessor

- UInt32 Upřednostněn

- UInt32 Hodnota

- Hodnotu Spuštění

- Řetezce Stav

- UInt32 StatusMask

- Hodnotu TimeSubmitted

- UInt32 TotalPages

- Hodnotu UntilTime



## <a name="printer-configuration"></a>Konfigurace tiskárny

Obor názvů: root\cimv2

Win32_PrinterConfiguration třídy


- Řetezce Jméno

- UInt32 BitsPerPel

- Řetezce Popisku

- Datového COLLATE

- UInt32 Barevných

- UInt32 Zkopíruje

- Řetezce Název

- Řetezce DeviceName

- UInt32 DisplayFlags

- UInt32 DisplayFrequency

- UInt32 DitherType

- UInt32 DriverVersion

- Datového Přenos

- Řetezce Formace

- UInt32 HorizontalResolution

- UInt32 ICMIntent

- UInt32 ICMMethod

- UInt32 LogPixels

- UInt32 Média

- UInt32 Změny

- UInt32 PaperLength

- Řetezce Papíru

- UInt32 PaperWidth

- UInt32 PelsHeight

- UInt32 PelsWidth

- UInt32 PrintQuality

- UInt32 Kapacity

- Řetezce Vlastnost SettingId

- UInt32 SpecificationVersion

- UInt32 TTOption

- UInt32 VerticalResolution

- UInt32 XResolution

- UInt32 YResolution



## <a name="printer-device"></a>Zařízení tiskárny

Obor názvů: root\cimv2

Win32_Printer třídy


- Řetezce DeviceID

- UInt32 Atribut

- UInt16 Dostupnosti

- UInt32 AveragePagesPerMinute

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt32 DefaultPriority

- Řetezce Název

- UInt16 DetectedErrorState

- Řetezce Ovladač ovladače

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt32 HorizontalResolution

- Hodnotu InstallDate

- UInt32 JobCountSinceLastReset

- UInt16 LanguagesSupported[]

- UInt32 LastErrorCode

- Řetezce Oblasti

- Řetezce Jméno

- UInt16 PaperSizesSupported[]

- Řetezce PNPDeviceID

- Řetezce Vlastnost PortName

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce PrinterPaperNames[]

- UInt32 PrinterState

- UInt16 PrinterStatus

- Řetezce PrintJobDataType

- Řetezce PrintProcessor

- Řetezce SeparatorFile

- Řetezce ServerName

- Řetezce ShareName

- Datového SpoolEnabled

- Hodnotu Spuštění

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset

- Hodnotu UntilTime

- UInt32 VerticalResolution



## <a name="process"></a>Proces

Obor názvů: root\cimv2

Win32_Process třídy


- Řetezce Popisovač

- Řetezce Popisku

- Hodnotu CreationDate

- Řetezce Název

- Řetezce ExecutablePath

- UInt16 ExecutionState

- UInt32 HandleCount

- Hodnotu InstallDate

- UInt64 KernelModeTime

- UInt32 MaximumWorkingSetSize

- UInt32 MinimumWorkingSetSize

- Řetezce Jméno

- Řetezce OSName

- UInt64 OtherOperationCount

- UInt64 OtherTransferCount

- UInt32 PageFaults

- UInt32 PageFileUsage

- UInt32 ParentProcessId

- UInt32 PeakPageFileUsage

- UInt64 PeakVirtualSize

- UInt32 PeakWorkingSetSize

- UInt32 Upřednostněn

- UInt64 PrivatePageCount

- UInt32 ID

- UInt32 QuotaNonPagedPoolUsage

- UInt32 QuotaPagedPoolUsage

- UInt32 QuotaPeakNonPagedPoolUsage

- UInt32 QuotaPeakPagedPoolUsage

- UInt64 ReadOperationCount

- UInt64 ReadTransferCount

- UInt32 SessionId

- Řetezce Stav

- Hodnotu TerminationDate

- UInt32 ThreadCount

- UInt64 UserModeTime

- UInt64 VirtualSize

- Řetezce WindowsVersion

- UInt64 WorkingSetSize

- UInt64 WriteOperationCount

- UInt64 WriteTransferCount



## <a name="processor"></a>Procesor

Obor názvů: Root\Cimv2\Sms

SMS_Processor třídy


- Řetezce DeviceID

- UInt16 AddressWidth

- UInt16 Architektura

- UInt16 Dostupnosti

- UInt16 BrandID

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce CPUHash

- Řetezce CPUKey

- UInt16 CpuStatus

- UInt32 CurrentClockSpeed

- UInt16 CurrentVoltage

- UInt16 Šířka DataWidth

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt32 ExtClock

- UInt16 Rodiny

- Hodnotu InstallDate

- Datového Is64Bit

- Datového IsHyperthreadCapable

- Datového IsHyperthreadEnabled

- Datového Mobilní zařízení

- Datového IsTrustedExecutionCapable

- Datového IsVitualizationCapable

- UInt32 L2CacheSize

- UInt32 L2CacheSpeed

- UInt32 L3CacheSize

- UInt32 L3CacheSpeed

- UInt32 LastErrorCode

- UInt16 Obsah

- UInt16 LoadPercentage

- Řetezce Výrobců

- UInt32 MaxClockSpeed

- Řetezce Jméno

- UInt32 NormSpeed

- UInt32 NumberOfCores

- UInt32 NumberOfLogicalProcessors

- Řetezce OtherFamilyDescription

- Datového PartOfDomain

- UInt32 PCache

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce ProcessorId

- UInt16 ProcessorType

- UInt16 Revize

- Řetezce Role

- Řetezce SocketDesignation

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Pokusný

- Řetezce Systémový

- Řetezce Identifikátor

- UInt16 UpgradeMethod

- Řetezce Znění

- UInt32 VoltageCaps

- Řetezce Skupinì



## <a name="protected-volume-information"></a>Informace o chráněném svazku

Obor názvů: Root\Cimv2\Sms

CCM_ProtectedVolumeInfo třídy


- Řetezce Jméno

- Řetezce Písmeno_jednotky

- UInt32 Typ ochrany replik



## <a name="protocol"></a>Protocol (Protokol)

Obor názvů: root\cimv2

Win32_NetworkProtocol třídy


- Řetezce Jméno

- Řetezce Popisku

- Datového ConnectionlessService

- Řetezce Název

- Datového GuaranteesDelivery

- Datového GuaranteesSequencing

- Hodnotu InstallDate

- UInt32 MaximumAddressSize

- UInt32 MaximumMessageSize

- Datového MessageOriented

- UInt32 MinimumAddressSize

- Datového PseudoStreamOriented

- Řetezce Stav

- Datového SupportsBroadcasting

- Datového SupportsConnectData

- Datového SupportsDisconnectData

- Datového SupportsEncryption

- Datového SupportsExpeditedData

- Datového SupportsFragmentation

- Datového SupportsGracefulClosing

- Datového SupportsGuaranteedBandwidth

- Datového SupportsMulticasting

- Datového SupportsQualityofService



## <a name="quick-fix-engineering"></a>Technik rychlé opravy

Obor názvů: root\cimv2

Win32_QuickFixEngineering třídy


- Řetezce HotFixID

- Řetezce ServicePackInEffect

- Řetezce Popisku

- Řetezce Název

- Řetezce FixComments

- Hodnotu InstallDate

- Řetezce InstalledBy

- Řetezce InstalledOn

- Řetezce Jméno

- Řetezce Stav



## <a name="ccm-recently-used-applications"></a>Nedávno použité aplikace CCM

Obor názvů: Root\Cimv2\Sms

CCM_RecentlyUsedApps třídy


- Řetezce ExplorerFileName

- Řetezce FolderPath

- Řetezce LastUserName

- Řetezce AdditionalProductCodes

- Řetezce Společnosti

- Řetezce Popis.

- Řetezce FilePropertiesHash

- UInt32 Velikost souboru

- Řetezce FileVersion

- Hodnotu LastUsedTime

- UInt32 LaunchCount

- (String) msiDisplayName

- (String) msiPublisher

- (String) msiVersion

- Řetezce OriginalFileName

- Řetezce ProductCode

- UInt32 ProductLanguage

- Řetezce NázevVýrobku

- Řetezce ProductVersion

- Řetezce SoftwarePropertiesHash



## <a name="registry"></a>Registr

Obor názvů: root\cimv2

Win32_Registry třídy


- Řetezce Jméno

- Řetezce Popisku

- UInt32 CurrentSize

- Řetezce Název

- Hodnotu InstallDate

- UInt32 MaximumSize objektu Form

- UInt32 ProposedSize

- Řetezce Stav



## <a name="scsi-controller"></a>Řadič SCSI

Obor názvů: root\cimv2

Win32_SCSIController třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt32 ControllerTimeouts

- Řetezce Název

- Řetezce DeviceMap

- Řetezce Ovladač ovladače

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce HardwareVersion

- UInt32 Indexovacím

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 MaxDataWidth

- UInt32 MaxNumberControlled

- UInt64 MaxTransferRate

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtectionManagement

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="serial-port-configuration"></a>Konfigurace sériového portu

Obor názvů: root\cimv2

Win32_SerialPortConfiguration třídy


- Řetezce Jméno

- Datového AbortReadWriteOnError

- UInt32 Rychlostí

- Datového BinaryModeEnabled

- UInt32 BitsPerByte

- Řetezce Popisku

- Datového ContinueXMitOnXOff

- Datového CTSOutflowControl

- Řetezce Název

- Datového DiscardNULLBytes

- Datového DSROutflowControl

- Datového DSRSensitivity

- Řetezce DTRFlowControlType

- UInt32 EOFCharacter

- UInt32 ErrorReplaceCharacter

- Datového ErrorReplacementEnabled

- UInt32 EventCharacter

- Datového Zaneprázdněný

- Řetezce Parita

- Datového ParityCheckEnabled

- Řetezce RTSFlowControlType

- Řetezce Vlastnost SettingId

- Řetezce StopBits

- UInt32 XOffCharacter

- UInt32 XOffXMitThreshold

- UInt32 XOnCharacter

- UInt32 XOnXMitThreshold

- UInt32 XOnXOffInFlowControl

- UInt32 XOnXOffOutFlowControl



## <a name="serial-ports"></a>Sériové porty

Obor názvů: root\cimv2

Win32_SerialPort třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Datového Tvaru

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRate

- UInt32 MaximumInputBufferSize

- UInt32 MaximumOutputBufferSize

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Datového OSAutoDiscovered

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce ProviderType

- Datového SettableBaudRate

- Datového SettableDataBits

- Datového SettableFlowControl

- Datového SettableParity

- Datového SettableParityCheck

- Datového SettableRLSD

- Datového SettableStopBits

- Řetezce Stav

- UInt16 StatusInfo

- Datového Supports16BitMode

- Datového SupportsDTRDSR

- Datového SupportsElapsedTimeouts

- Datového SupportsIntTimeouts

- Datového SupportsParityCheck

- Datového SupportsRLSD

- Datového SupportsRTSCTS

- Datového SupportsSpecialCharacters

- Datového SupportsXOnXOff

- Datového SupportsXOnXOffSet

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="server-feature"></a>Serverová součást

Obor názvů: root\cimv2

Win32_ServerFeature třídy


- UInt32 ÚČET

- Řetezce Jméno

- UInt32 ParentID



## <a name="services"></a>Služby

Obor názvů: root\cimv2

Win32_Service třídy


- Řetezce Jméno

- Datového AcceptPause

- Datového AcceptStop

- Řetezce Popisku

- UInt32 Kontrolní bod

- Řetezce Název

- Datového DesktopInteract

- Řetezce DisplayName

- Řetezce ErrorControl

- UInt32 ExitCode

- Hodnotu InstallDate

- Řetezce Název

- UInt32 ID

- UInt32 ServiceSpecificExitCode

- Řetezce ServiceType

- Datového Začínáme

- Řetezce StartMode

- Řetezce StartName

- Řetezce Státech

- Řetezce Stav

- Řetezce Systémový

- UInt32 TagId

- UInt32 WaitHint



## <a name="shares"></a>Sdílené složky

Obor názvů: root\cimv2

Win32_Share třídy


- Řetezce Jméno

- UInt32 AccessMask

- Datového AllowMaximum

- Řetezce Popisku

- Řetezce Název

- Hodnotu InstallDate

- UInt32 MaximumAllowed

- Řetezce Dílčí

- Řetezce Stav

- UInt32 Textový



## <a name="sw-licensing-product"></a>Produkt pro licencování SW

Obor názvů: root\cimv2

SoftwareLicensingProduct třídy


- Řetezce ÚČET

- Řetezce ApplicationID

- Řetezce Název

- Hodnotu EvaluationEndDate

- UInt32 GracePeriodRemaining

- UInt32 LicenseStatus

- Řetezce MachineURL

- Řetezce Jméno

- Řetezce OfflineInstallationId

- Řetezce PartialProductKey

- Řetezce ProcessorURL

- Řetezce ProductKeyID

- Řetezce ProductKeyURL

- Řetezce UseLicenseURL



## <a name="sw-licensing-service"></a>Služba licencování SW

Obor názvů: root\cimv2

SoftwareLicensingService třídy


- Řetezce Znění

- Řetezce ClientMachineID

- UInt32 IsKeyManagementServiceMachine

- UInt32 KeyManagementServiceCurrentCount

- Řetezce KeyManagementServiceMachine

- Řetezce KeyManagementServiceProductKeyID

- UInt32 PolicyCacheRefreshRequired

- UInt32 RequiredClientCount

- UInt32 VLActivationInterval

- UInt32 VLRenewalInterval



## <a name="software-shortcut"></a>Zástupce softwaru

Obor názvů: Root\Cimv2\Sms

SMS_SoftwareShortcut třídy


- Řetezce ShortcutKey

- Řetezce BinFileVersion

- Řetezce BinProductVersion

- Řetezce Název

- Řetezce FilePropertiesHash

- Řetezce FilePropertiesHashEx

- UInt32 Velikost souboru

- Řetezce FileVersion

- UInt32 Language

- Řetezce ParentName

- Řetezce Produktu

- Řetezce ProductCode

- Řetezce ProductVersion

- Řetezce Microsoft

- Řetezce Zkratka

- UInt32 ShortcutType

- Řetezce TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

Obor názvů: Root\Cimv2\Sms

SMS_SoftwareTag třídy


- Řetezce TagCreatorRegid

- Řetezce Identifikátor

- Řetezce DisplayVersion

- Datového EntitlementRequired

- Řetezce NázevVýrobku

- Řetezce SoftwareCreator

- Řetezce SoftwareCreatorRegid

- Řetezce SoftwareLicensor

- Řetezce SoftwareLicensorRegid

- Řetezce TagCreator

- (SInt32) VersionMajor

- (SInt32) VersionMinor



## <a name="sound-devices"></a>Zvuková zařízení

Obor názvů: root\cimv2

Win32_SoundDevice třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- UInt16 DMABufferSize

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 Adresa MPU401

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce NázevVýrobku

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový



## <a name="system-account"></a>Systémový účet

Obor názvů: root\cimv2

Win32_SystemAccount třídy


- Řetezce Domain

- Řetezce Jméno

- Řetezce Popisku

- Řetezce Název

- Hodnotu InstallDate

- Řetezce ID

- Uint8 SIDType

- Řetezce Stav



## <a name="system-boot-data"></a>Systémová data spuštění

Obor názvů: root\CCM

CCM_SystemBootData třídy


- UInt64 SystemStartTime

- UInt32 BiosDuration

- UInt16 BootDiskMediaType

- UInt32 BootDuration

- UInt32 EventLogStart

- UInt32 GPDuration

- Řetezce OSVersion

- UInt32 UpdateDuration



## <a name="system-boot-summary"></a>Souhrn spuštění systému

Obor názvů: root\CCM

CCM_SystemBootSummary třídy


- UInt32 AverageBootFrequency

- UInt32 LatestBiosDuration

- UInt32 LatestBootDuration

- UInt32 LatestCoreBootDuration

- UInt32 LatestEventLogStart

- UInt32 LatestGPDuration

- UInt32 LatestUpdateDuration

- UInt32 MaxBiosDuration

- UInt32 MaxBootDuration

- UInt32 MaxCoreBootDuration

- UInt32 MaxEventLogStart

- UInt32 MaxGPDuration

- UInt32 MaxUpdateDuration

- UInt32 MedianBiosDuration

- UInt32 MedianBootDuration

- UInt32 MedianCoreBootDuration

- UInt32 MedianEventLogStart

- UInt32 MedianGPDuration

- UInt32 MedianUpdateDuration



## <a name="system-console-usage"></a>Využití systémové konzoly

Obor názvů: Root\Cimv2\Sms

SMS_SystemConsoleUsage třídy


- Hodnotu SecurityLogStartDate

- Řetezce TopConsoleUser

- UInt32 TotalConsoleTime

- UInt32 TotalConsoleUsers

- UInt32 TotalSecurityLogTime



## <a name="system-console-user"></a>Uživatel konzoly systému

Obor názvů: Root\Cimv2\Sms

SMS_SystemConsoleUser třídy


- Řetezce SystemConsoleUser

- Hodnotu LastConsoleUse

- UInt32 NumberOfConsoleLogons

- UInt32 TotalUserConsoleMinutes



## <a name="system-devices"></a>Systémová zařízení

Obor názvů: Root\Cimv2\Sms

CCM_SystemDevices třídy


- Řetezce Jméno

- Řetezce CompatibleIDs[]

- Řetezce DeviceID

- Řetezce HardwareIDs[]

- Datového IsPnP



## <a name="system-drivers"></a>Systémové ovladače

Obor názvů: root\cimv2

Win32_SystemDriver třídy


- Řetezce Jméno

- Datového AcceptPause

- Datového AcceptStop

- Řetezce Popisku

- Řetezce Název

- Datového DesktopInteract

- Řetezce DisplayName

- Řetezce ErrorControl

- UInt32 ExitCode

- Hodnotu InstallDate

- Řetezce Název

- UInt32 ServiceSpecificExitCode

- Řetezce ServiceType

- Datového Začínáme

- Řetezce StartMode

- Řetezce StartName

- Řetezce Státech

- Řetezce Stav

- Řetezce Systémový

- UInt32 TagId



## <a name="system-enclosure"></a>Skříň systému

Obor názvů: root\cimv2

Win32_SystemEnclosure třídy


- Řetezce Inteligentní

- Datového AudibleAlarm

- Řetezce BreachDescription

- Řetezce CableManagementStrategy

- Řetezce Popisku

- UInt16 ChassisTypes[]

- (SInt16) CurrentRequiredOrProduced

- Řetezce Název

- UInt16 HeatGeneration

- Datového HotSwappable

- Hodnotu InstallDate

- Datového LockPresent

- Řetezce Výrobců

- Řetezce Vzorový

- Řetezce Jméno

- UInt16 NumberOfPowerCords

- Řetezce OtherIdentifyingInfo

- Řetezce PartNumber

- Datového PoweredOn

- Datového Disket

- Datového Replaceable

- UInt16 SecurityBreach

- UInt16 SecurityStatus

- Řetezce Sériové

- Řetezce ServiceDescriptions []

- UInt16 ServicePhilosophy[]

- Řetezce SKLADOVÉ

- Řetezce SMBIOSAssetTag

- Řetezce Stav

- Řetezce TypeDescriptions[]

- Řetezce Znění

- Datového VisibleAlarm



## <a name="tape-drive"></a>Pásková jednotka

Obor názvů: root\cimv2

Win32_TapeDrive třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- UInt16 Možnosti []

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- UInt32 Komprese

- Řetezce CompressionMethod

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Řetezce Název

- UInt32 ECC

- UInt32 EOTWarningZoneSize

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- UInt32 FeaturesHigh

- UInt32 FeaturesLow

- Řetezce ÚČET

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- UInt32 MaxPartitionCount

- Řetezce Média

- UInt64 MinBlockSize

- Řetezce Jméno

- Datového NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Odsazení

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt32 ReportSetMarks

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový



## <a name="time-zone"></a>Časové pásmo

Obor názvů: root\cimv2

Win32_TimeZone třídy


- Řetezce Standardní

- (SInt32) Posun

- Řetezce Popisku

- (SInt32) DaylightBias

- UInt32 DaylightDay

- Uint8 DaylightDayOfWeek

- UInt32 DaylightHour

- UInt32 DaylightMillisecond

- UInt32 DaylightMinute

- UInt32 DaylightMonth

- Řetezce Letní čas

- UInt32 DaylightSecond

- UInt32 DaylightYear

- Řetezce Název

- Řetezce Vlastnost SettingId

- UInt32 StandardBias

- UInt32 StandardDay

- Uint8 StandardDayOfWeek

- UInt32 StandardHour

- UInt32 StandardMillisecond

- UInt32 StandardMinute

- UInt32 StandardMonth

- UInt32 StandardSecond

- UInt32 StandardYear



## <a name="tpm"></a>TPM

Obor názvů: root\CIMv2\Security\MicrosoftTpm

Win32_Tpm třídy


- Datového IsActivated_InitialValue

- Datového IsEnabled_InitialValue

- Datového IsOwned_InitialValue

- UInt32 ManufacturerId

- Řetezce ManufacturerVersion

- Řetezce ManufacturerVersionInfo

- Řetezce PhysicalPresenceVersionInfo

- Řetezce SpecVersion



## <a name="tpm-status"></a>Stav čipu TPM

Obor názvů: Root\Cimv2\Sms

SMS_TPM třídy


- Datového Jen pro čtení

- UInt32 Informace

- Datového Nedá se použít



## <a name="ts-issued-license"></a>Licence vydané TS

Obor názvů: root\cimv2

Win32_TSIssuedLicense třídy


- UInt32 LicenseId

- Hodnotu ExpirationDate

- Hodnotu IssueDate

- UInt32 KeyPackId

- UInt32 LicenseStatus

- (String) sHardwareId

- (String) sIssuedToComputer

- (String) sIssuedToUser



## <a name="ts-license-key-pack"></a>Balík klíčů TS License Key

Obor názvů: root\cimv2

Win32_TSLicenseKeyPack třídy


- UInt32 KeyPackId

- UInt32 AvailableLicenses

- Řetezce Název

- UInt32 IssuedLicenses

- UInt32 KeyPackType

- UInt32 ProductType

- Řetezce ProductVersion

- UInt32 TotalLicenses



## <a name="uninterruptible-power-supply"></a>Nepřerušitelný zdroj napájení

Obor názvů: root\cimv2

Win32_UninterruptiblePowerSupply třídy


- Řetezce DeviceID

- UInt16 ActiveInputVoltage

- UInt16 Dostupnosti

- Datového BatteryInstalled

- Datového CanTurnOffRemotely

- Řetezce Popisku

- Řetezce CommandFile

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime (

- UInt32 FirstMessageDelay

- Hodnotu InstallDate

- Datového IsSwitchingSupply

- UInt32 LastErrorCode

- Datového LowBatterySignal

- UInt32 MessageInterval

- Řetezce Jméno

- Řetezce PNPDeviceID

- Datového PowerFailSignal

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt32 Range1InputFrequencyHigh

- UInt32 Range1InputFrequencyLow

- UInt32 Range1InputVoltageHigh

- UInt32 Range1InputVoltageLow

- UInt32 Range2InputFrequencyHigh

- UInt32 Range2InputFrequencyLow

- UInt32 Range2InputVoltageHigh

- UInt32 Range2InputVoltageLow

- UInt16 RemainingCapacityStatus

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- UInt32 TimeOnBackup

- UInt32 TotalOutputPower

- UInt16 TypeOfRangeSwitching

- Řetezce Pro SPort



## <a name="usb-controller"></a>Řadič USB

Obor názvů: root\cimv2

Win32_USBController třídy


- Řetezce DeviceID

- UInt16 Dostupnosti

- Řetezce Popisku

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce Název

- Datového ErrorCleared

- Řetezce ErrorDescription

- Hodnotu InstallDate

- UInt32 LastErrorCode

- Řetezce Výrobců

- UInt32 MaxNumberControlled

- Řetezce Jméno

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- Hodnotu TimeOfLastReset



## <a name="usb-device"></a>Zařízení USB

Obor názvů: root\cimv2

Win32_USBDevice třídy


- Řetezce DeviceID

- Řetezce Popisku

- Řetezce ClassGuid

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce CreationClassName

- Řetezce Název

- Řetezce Výrobců

- Řetezce Jméno

- Řetezce PNPDeviceID

- Řetezce Službám

- Řetezce Stav

- Řetezce SystemCreationClassName

- Řetezce Systémový



## <a name="usm-user-profile"></a>Profil uživatele USM

Obor názvů: root\cimv2

Win32_UserProfile třídy


- Řetezce ID

- Uint8 Funkčnosti

- Řetezce LastAttemptedProfileDownloadTime

- Řetezce LastAttemptedProfileUploadTime

- Řetezce LastBackgroundRegistryUploadTime

- Hodnotu LastDownloadTime

- Hodnotu LastUploadTime

- Hodnotu LastUseTime

- Datového Nahrán

- Řetezce LocalPath

- UInt32 RefCount

- Datového RoamingConfigured

- Řetezce RoamingPath

- Datového RoamingPreference

- Datového Speciální

- UInt32 Stav



## <a name="video-controller"></a>Grafický adaptér

Obor názvů: root\cimv2

Win32_VideoController třídy


- Řetezce DeviceID

- UInt16 AcceleratorCapabilities[]

- Řetezce AdapterCompatibility

- Řetezce AdapterDACType

- UInt32 AdapterRAM

- UInt16 Dostupnosti

- Řetezce CapabilityDescriptions[]

- Řetezce Popisku

- UInt32 ColorTableEntries

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- UInt32 CurrentBitsPerPixel

- UInt32 CurrentHorizontalResolution

- UInt64 CurrentNumberOfColors

- UInt32 CurrentNumberOfColumns

- UInt32 CurrentNumberOfRows

- UInt32 CurrentRefreshRate

- UInt16 CurrentScanMode

- UInt32 CurrentVerticalResolution

- Řetezce Název

- UInt32 DeviceSpecificPens

- UInt32 DitherType

- Hodnotu DriverDate

- Řetezce DriverVersion

- Datového ErrorCleared

- Řetezce ErrorDescription

- UInt32 ICMIntent

- UInt32 ICMMethod

- Řetezce InfFilename

- Řetezce InfSection

- Hodnotu InstallDate

- Řetezce InstalledDisplayDrivers

- UInt32 LastErrorCode

- UInt32 MaxMemorySupported

- UInt32 MaxNumberControlled

- UInt32 MaxRefreshRate

- UInt32 MinRefreshRate

- Datového Jednobarevné

- Řetezce Jméno

- UInt16 NumberOfColorPlanes

- UInt32 NumberOfVideoPages

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- UInt16 ProtocolSupported

- UInt32 ReservedSystemPaletteEntries

- UInt32 SpecificationVersion

- Řetezce Stav

- UInt16 StatusInfo

- Řetezce Systémový

- UInt32 SystemPaletteEntries

- Hodnotu TimeOfLastReset

- UInt16 VideoArchitecture

- UInt16 VideoMemoryType

- UInt16 VideoMode

- Řetezce VideoModeDescription

- Řetezce VideoProcessor



## <a name="virtual-application-packages"></a>Balíčky virtuálních aplikací

Obor názvů: root\Microsoft\appvirt\client

Balíček třídy


- Řetezce PackageGUID

- UInt64 CachedLaunchSize

- UInt16 CachedPercentage

- UInt64 CachedSize

- UInt64 LaunchSize

- Řetezce Jméno

- Řetezce SftPath

- UInt64 TotalSize

- Řetezce Znění

- Řetezce VersionGUID



## <a name="virtual-applications"></a>Virtuální aplikace

Obor názvů: root\Microsoft\appvirt\client

Aplikace třídy


- Řetezce Jméno

- Řetezce Znění

- Řetezce CachedOsdPath

- UInt32 GlobalRunningCount

- Hodnotu LastLaunchOnSystem

- Datového Načítá

- Řetezce OriginalOsdPath

- Řetezce PackageGUID



## <a name="virtual-machine-64"></a>Virtuální počítač (64)

Obor názvů: root\cimv2

Win32Reg_SMSGuestVirtualMachine64 třídy


- Řetezce Klíč InstanceKey

- Řetezce PhysicalHostName

- Řetezce PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>Virtuální počítač

Obor názvů: root\cimv2

Win32Reg_SMSGuestVirtualMachine třídy


- Řetezce Klíč InstanceKey

- Řetezce PhysicalHostName

- Řetezce PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>Podrobnosti o virtuálním počítači

Obor názvů: root\vm\VirtualServer

VirtualMachine třídy


- Řetezce Jméno

- UInt32 CpuUtilization

- UInt64 DiskBytesRead

- UInt64 DiskBytesWritten

- UInt64 DiskSpaceUsed

- UInt64 HeartbeatCount

- UInt32 HeartbeatInterval

- UInt32 HeartbeatPercentage

- UInt32 HeartbeatRate

- UInt64 NetworkBytesReceived

- UInt64 NetworkBytesSent

- UInt64 PhysicalMemoryAllocated

- UInt32 Doba provozu



## <a name="volume"></a>Svazek

Obor názvů: root\cimv2

Win32_Volume třídy


- Řetezce DeviceID

- UInt16 Stoupit

- Datového Automaticky připojit

- UInt16 Dostupnosti

- UInt64 Velikostí bloku

- UInt64 Klíčivost

- Řetezce Popisku

- Datového Komprimován

- UInt32 ConfigManagerErrorCode

- Datového ConfigManagerUserConfig

- Řetezce CreationClassName

- Řetezce Název

- Datového DirtyBitSet

- Řetezce Písmeno_jednotky

- UInt32 DriveType

- Datového ErrorCleared

- Řetezce ErrorDescription

- Řetezce ErrorMethodology

- Řetezce Systému souborů

- UInt64 FreeSpace

- Datového IndexingEnabled

- Hodnotu InstallDate

- Řetezce Popisek

- UInt32 LastErrorCode

- UInt32 MaximumFileNameLength

- Řetezce Jméno

- UInt64 NumberOfBlocks

- Řetezce PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Datového PowerManagementSupported

- Řetezce Cílem

- Datového QuotasEnabled

- Datového QuotasIncomplete

- Datového QuotasRebuilding

- UInt32 Sériové

- Řetezce Stav

- UInt16 StatusInfo

- Datového SupportsDiskQuotas

- Datového SupportsFileBasedCompression

- Řetezce SystemCreationClassName

- Řetezce Systémový



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

Obor názvů: root\ccm\cimodels

CCM_WebAppInstallInfo třídy


- Řetezce AppDeliveryTypeId

- UInt32 AppDtRevision

- Řetezce TargetURL

- Řetezce Identifikátor UserSID

- Řetezce URLFileName

- Řetezce URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

Obor názvů: Root\Cimv2\Sms

SMS_Windows8Application třídy


- Řetezce FullName

- Řetezce ApplicationName

- Řetezce Architektura

- Datového ConfigMgrManaged

- Řetezce DependencyApplicationNames

- Řetezce FamilyName

- Řetezce InstalledLocation

- Datového Rozhraní

- Řetezce Microsoft

- Řetezce PublisherId

- Řetezce Znění



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

Obor názvů: Root\Cimv2\Sms

SMS_Windows8ApplicationUserInfo třídy


- Řetezce FullName

- Řetezce UserSecurityId

- Řetezce InstallState

- Řetezce UserAccountName



## <a name="windows-update"></a>Windows Update

Obor názvů: root\cimv2

Win32Reg_SMSWindowsUpdate třídy


- Řetezce Klíč InstanceKey

- UInt32 Možnosti automatických aktualizací

- UInt32 Žádné automatické aktualizace

- UInt32 UseWUServer



## <a name="windows-update-agent-version"></a>Verze agenta web Windows Update

Obor názvů: Root\Cimv2\Sms

Win32_WindowsUpdateAgentVersion třídy


- Řetezce Znění



## <a name="write-filter-state"></a>Stav filtru zápisu

Obor názvů: Root\Cimv2\Sms

CCM_WriteFilterState třídy


- Datového WriteFilterEnabled
