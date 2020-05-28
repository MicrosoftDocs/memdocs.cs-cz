---
title: Import profilů certifikátů PFX
titleSuffix: Configuration Manager
description: Naučte se používat soubory PFX v Configuration Manager ke generování certifikátů specifických pro uživatele, které podporují výměnu šifrovaných dat.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3304d480f0650191a784a9152ae464e81c2207a1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906400"
---
# <a name="import-pfx-certificate-profiles"></a>Import profilů certifikátů PFX

*Platí pro: Configuration Manager (Current Branch)*

Přečtěte si, jak vytvořit profil certifikátu importem přihlašovacích údajů z externích certifikátů. Tento článek popisuje konkrétní informace o profilech certifikátů PFX (Personal Information Exchange). Další informace o tom, jak vytvořit a nakonfigurovat tyto profily, najdete v tématu [profily certifikátů](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager podporuje různé druhy úložišť certifikátů pro různá zařízení a verze operačních systémů. Například Windows 10 a Windows 10 Mobile. Další informace najdete v tématu [požadavky na profil certifikátu](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Pomocí Configuration Manager importujte přihlašovací údaje certifikátu a pak na zařízení zřiďte soubory PFX. Tyto soubory můžete použít k vygenerování certifikátů specifických pro uživatele pro podporu výměny šifrovaných dat.

> [!TIP]  
> Podrobný návod k tomuto procesu najdete v blogovém příspěvku [jak vytvořit a nasadit profily certifikátů PFX v Configuration Manager](https://docs.microsoft.com/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager).  

## <a name="create-a-profile"></a>Vytvoření profilu

1. V konzole Configuration Manager přejděte do pracovního prostoru **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**, rozbalte položku **přístup k prostředkům společnosti**a pak vyberte **profily certifikátů**.

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit profil certifikátu**.

1. Na stránce **Obecné** v **Průvodci vytvořením profilu certifikátu**zadejte následující informace:  

    - **Název**: Zadejte jedinečný název profilu certifikátu. Opět můžete použít maximálně 256 znaků.  

    - **Popis**: zadejte popis, který poskytne přehled profilu certifikátu, který ho pomůže identifikovat v konzole Configuration Manager. Opět můžete použít maximálně 256 znaků.  

1. Vyberte **Nastavení osobní informace Exchange-PKCS (PFX) #12 (PFX) – importovat**. Tato možnost importuje informace z existujícího certifikátu pro vytvoření profilu certifikátu.

    > [!NOTE]
    > Možnost **Create** požaduje certifikát jménem uživatele z připojené místní certifikační autority (CA). Tento proces pak bezpečně doručuje certifikát klientům jako soubory PFX. Další informace najdete v tématu [Vytvoření profilů certifikátů PFX pomocí certifikační autority](create-pfx-certificate-profiles.md).

1. Na stránce **certifikát PFX** v **Průvodci vytvořením profilu certifikátu**zadejte poskytovatele úložiště klíčů zařízení (KSP):

    - **Instalovat do čipu Trusted Platform Module (TPM), pokud existuje**  
    - **Nainstalovat do čipu TPM (Trusted Platform Module), jinak selhání**
    - **Nainstalovat do Windows Hello pro firmy, jinak chyba**
    - **Instalovat do zprostředkovatele úložiště klíčů pro software**

1. Na stránce **podporované platformy** vyberte podporované platformy zařízení.

1. Dokončete průvodce.

## <a name="deploy-the-profile"></a>Nasaďte profil

Po vytvoření a zřízení profilu certifikátu je nyní k dispozici v uzlu **profily certifikátů** . Další informace o tom, jak ho nasadit, najdete v tématu [nasazení profilů přístupu k prostředkům](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Přiřazení primárních uživatelů

Přiřaďte cílové uživatele jako primární uživatele na zařízeních s Windows 10, kde potřebujete nainstalovat certifikáty PFX. Další informace najdete v tématu [spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Zřídit vytvoření skriptu PFX

Pokud chcete importovat certifikát PFX, použijte následující rutiny Configuration Manager PowerShellu ke zřízení skriptu PFX:

- [Get-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import – CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Ukázkový skript

Pokud chcete soubor PFX zřídit pro uživatele s profilem certifikátu, otevřete na počítači s konzolou Configuration Manager PowerShell. Změňte proměnné s hodnotami z vašeho prostředí.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Viz také

[Vytvoření nového profilu certifikátu](../../protect/deploy-use/create-certificate-profiles.md)

[Vytvoření profilů certifikátů PFX pomocí certifikační autority](create-pfx-certificate-profiles.md)

[Nasazení profilů sítí Wi-Fi a VPN, e-mailů a certifikátů](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
