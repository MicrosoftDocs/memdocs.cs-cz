---
title: Vytvoření profilů certifikátů v Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si, jak používat Simple Certificate Enrollment Protocol (SCEP) nebo certifikáty PKCS (Public Key Cryptography Standards) a profily certifikátů s Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22bfe44b95eedcdf87a41cfaaf959c72cfbe93e2
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423811"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Použití certifikátů pro ověřování v Microsoft Intune

Pomocí certifikátů s Intune můžete ověřovat uživatele s aplikacemi a podnikovými prostředky prostřednictvím sítě VPN, Wi-Fi nebo e-mailových profilů. Když k ověření těchto připojení použijete certifikáty, koncoví uživatelé nebudou muset zadávat uživatelská jména a hesla, což by mohlo mít bez potíží přístup. Certifikáty se taky používají k podepisování a šifrování e-mailů pomocí S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Podporované certifikáty a využití v Intune

| Typ              | Authentication | Podepisování S/MIME | Šifrování S/MIME  |
|--|--|--|--|
| Importovaný certifikát PKCS (Public Key Cryptography Standards) |  | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png)|
| PKCS#12 (nebo PFX)    | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) |  |
| Protokol SCEP (Simple Certificate Enrollment Protocol)  | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | |

K nasazení těchto certifikátů vytvoříte a přiřadíte profily certifikátů k zařízením.

Každý profil každého jednotlivého certifikátu, který vytvoříte, podporuje jednu platformu. Pokud například používáte certifikáty PKCS, vytvoříte profil certifikátu PKCS pro Android a samostatný profil certifikátu PKCS pro iOS/iPadOS. Pokud pro tyto dvě platformy používáte také certifikáty SCEP, vytvoříte profil certifikátu SCEP pro Android a druhý pro iOS/iPadOS.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Obecné pokyny při používání certifikační autority Microsoftu

Když použijete certifikační autoritu (CA) Microsoftu:

- Používání profilů certifikátů SCEP:
  - [Nastavte server služby zápisu síťových zařízení (NDES)](certificates-scep-configure.md#set-up-ndes) pro použití s Intune.
  - [Nainstalujte Microsoft Certificate Connector](certificates-scep-configure.md#install-the-microsoft-intune-connector):

- Používání profilů certifikátů PKCS:
  - [Instalace Certificate Connectoru PFX pro Microsoft Intune] (Imported-Certificates-PFX-configure.
  
- Použití importovaných certifikátů PKCS:
  - [Nainstalujte Certificate Connector PFX pro Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Exportujte certifikáty od certifikační autority a pak je importujte do Microsoft Intune. Viz [projekt prostředí PowerShell pro PFXImport](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Nasaďte certifikáty pomocí následujících mechanismů:
  - [Profily důvěryhodných certifikátů](certificates-configure.md#create-trusted-certificate-profiles) pro nasazení certifikátu důvěryhodné kořenové certifikační autority z kořenové nebo zprostředkující certifikační autority do zařízení
  - Profily certifikátů SCEP
  - Profily certifikátů PKCS
  - Profily certifikátů PKCS importovány

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Obecné požadavky při použití certifikační autority třetí strany

Používáte-li certifikační autoritu (CA) třetí strany (od společnosti Microsoft):

- Používání profilů certifikátů SCEP:
  - Nastavte integraci s certifikační autoritou třetí strany z [některého z našich podporovaných partnerů](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). Nastavení zahrnuje následující pokyny od certifikační autority třetí strany, které dokončí integraci své certifikační autority s Intune.
  - [Vytvořte ve službě Azure AD aplikaci](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) , která deleguje práva k Intune, aby vystavoval ověření výzvy certifikátu SCEP.

- Importované certifikáty PKCS vyžadují, abyste [nainstalovali konektor PFX Certificate pro Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Nasaďte certifikáty pomocí následujících mechanismů:
  - [Profily důvěryhodných certifikátů](certificates-configure.md#create-trusted-certificate-profiles) pro nasazení certifikátu důvěryhodné kořenové certifikační autority z kořenové nebo zprostředkující certifikační autority do zařízení
  - Profily certifikátů SCEP
  - Profily certifikátů PKCS *(podporované jenom s [platformou PKI DigiCert](certificates-digicert-configure.md))*
  - Profily certifikátů PKCS importovány

## <a name="supported-platforms-and-certificate-profiles"></a>Podporované platformy a profily certifikátů

| Platforma              | Profil důvěryhodného certifikátu | Profil certifikátu PKCS | Profil certifikátu SCEP | Profil certifikátu importovaného PKCS  |
|--|--|--|--|---|
| Správce zařízení s Androidem | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png)|  ![Podporováno](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> – Plně spravované (vlastník zařízení)   | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png) |  ![Podporováno](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> -Vyhrazené (vlastník zařízení)   | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png)|
| Android Enterprise <br> – Pracovní profil ve vlastnictví firmy   | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png)  | ![Podporováno](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> – Pracovní profil    | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) |
| macOS                 | ![Podporováno](./media/certificates-configure/green-check.png) |  ![Podporováno](./media/certificates-configure/green-check.png) |![Podporováno](./media/certificates-configure/green-check.png)|![Podporováno](./media/certificates-configure/green-check.png)|
| Windows 8.1 a vyšší |![Podporováno](./media/certificates-configure/green-check.png)  |  |![Podporováno](./media/certificates-configure/green-check.png) |   |
| Windows 10 a novější  | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) | ![Podporováno](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Exportujte certifikát důvěryhodné kořenové certifikační autority.

Aby zařízení mohla používat importované certifikáty PKCS, SCEP a PKCS, musí důvěřovat vaší kořenové certifikační autoritě. Chcete-li vytvořit vztah důvěryhodnosti, exportujte certifikát důvěryhodné kořenové certifikační autority a všechny zprostředkující nebo vydávající certifikáty certifikační autority jako veřejný certifikát (. cer). Tyto certifikáty můžete získat z vydávající certifikační autority nebo z jakéhokoli zařízení, které důvěřuje vydávající certifikační autoritě.

Informace o exportu certifikátu najdete v dokumentaci k vaší certifikační autoritě. Veřejný certifikát budete muset exportovat jako soubor. cer.  Neexportujte privátní klíč, soubor. pfx.

Tento soubor. cer budete používat při [vytváření profilů důvěryhodných certifikátů](#create-trusted-certificate-profiles) k nasazení tohoto certifikátu do zařízení.

## <a name="create-trusted-certificate-profiles"></a>Vytvoření profilů důvěryhodných certifikátů

Vytvořte a nasaďte profil důvěryhodného certifikátu před vytvořením profilu certifikátu SCEP, PKCS nebo PKCS. Nasazení profilu důvěryhodného certifikátu do stejných skupin, které přijímají jiné typy profilů certifikátů, zajistí, že každé zařízení dokáže rozpoznat legitimitu vaší certifikační autority. To zahrnuje profily jako pro VPN, Wi-Fi a e-maily.

Profily certifikátů SCEP přímo odkazují na profil důvěryhodného certifikátu. Profily certifikátů PKCS přímo neodkazují na profil důvěryhodného certifikátu, ale přímo odkazují na server, který je hostitelem vaší certifikační autority. Profily certifikátů PKCS importované přímo neodkazují na profil důvěryhodného certifikátu, ale můžou ho použít na zařízení. Nasazení profilu důvěryhodného certifikátu na zařízení zajistí, že se tento vztah důvěryhodnosti naváže. Když zařízení nedůvěřuje kořenové certifikační autoritě, zásada profilu certifikátu SCEP nebo PKCS se nezdaří.

Vytvořte samostatný profil důvěryhodného certifikátu pro každou platformu zařízení, kterou chcete podporovat, stejně jako u profilů certifikátů SCEP, PKCS a PKCS.

> [!IMPORTANT]
> Důvěryhodné kořenové profily, které vytvoříte pro platformu *Windows 10 a novější*, se zobrazí v centru pro správu Microsoft Endpoint Manageru jako profily pro platformu *Windows 8.1 a novější*. 
>
> Jedná se o známý problém s prezentací platformy pro profily důvěryhodných certifikátů. I když profil zobrazuje platformu Windows 8.1 a novější, je funkční pro Windows 10 a novější.

> [!NOTE]
> Profil *důvěryhodného certifikátu* v Intune se dá použít jenom k doručování kořenových nebo zprostředkujících certifikátů. Účelem nasazení takových certifikátů je vytvořit řetěz důvěryhodnosti. Použití profilu důvěryhodného certifikátu k doručování certifikátů jiných než kořenových nebo zprostředkujících certifikátů není společností Microsoft podporováno. Při výběru profilu důvěryhodného certifikátu na portálu Intune může být zablokovaný import certifikátů, které se nepovažují za kořenové nebo zprostředkující certifikáty. I když můžete importovat a nasadit certifikát, který není ani kořenovým nebo zprostředkujícím certifikátem, který používá tento typ profilu, pravděpodobně dojde k neočekávaným výsledkům mezi různými platformami, jako je iOS nebo Android.

### <a name="to-create-a-trusted-certificate-profile"></a>Vytvoření profilu důvěryhodného certifikátu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte a přejdete na konfigurace **zařízení**  >  **profily**  >  **vytvořit profil**.

   ![Přejděte na Intune a vytvořte nový profil důvěryhodného certifikátu.](./media/certificates-configure/certificates-configure-profile-new.png)

3. Zadejte tyto vlastnosti:
   - **Platforma**: vyberte platformu zařízení, která obdrží tento profil.
   - **Profil**: vyberte **důvěryhodný certifikát** .
  
4. Vyberte **Vytvořit**.

5. V části **základy**zadejte následující vlastnosti:
   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například *profil důvěryhodného certifikátu pro celou firmu*.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**určete soubor. cer pro certifikát důvěryhodné kořenové certifikační autority, který jste předtím exportovali. 

   Jenom pro zařízení s Windows 8.1 a Windows 10 vyberte **cílové úložiště** pro důvěryhodný certifikát z těchto možností:

   - **Úložiště počítačových certifikátů – kořenové**
   - **Úložiště certifikátů počítače-zprostředkující**
   - **Úložiště uživatelských certifikátů – zprostředkující**

   ![Vytvoření profilu a nahrání důvěryhodného certifikátu](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

   Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

    Vyberte **Další**.

11. (*Platí jenom pro Windows 10*) V části **pravidla použitelnosti**zadejte pravidla použitelnosti pro upřesnění přiřazení tohoto profilu. Můžete vybrat, že chcete profil přiřadit nebo nepřiřadit, na základě edice nebo verze operačního systému zařízení.

  Další informace najdete v tématu [pravidla použitelnosti](../configuration/device-profile-create.md#applicability-rules) v tématu *Vytvoření profilu zařízení v Microsoft Intune*.

12. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete vytvořit, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="additional-resources"></a>Další zdroje

- [Přiřazení profilů zařízení](../configuration/device-profile-assign.md)  
- [Podepisování a šifrování e-mailů pomocí S/MIME](certificates-s-mime-encryption-sign.md)  
- [Použití certifikační autority třetích stran](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Další kroky

Pro každou platformu, kterou chcete použít, vytvořte profily certifikátů importované pomocí protokolu SCEP, PKCS nebo PKCS. Chcete-li pokračovat, přečtěte si následující články:

- [Konfigurace infrastruktury pro podporu certifikátů SCEP pomocí Intune](certificates-scep-configure.md)  
- [Konfigurace a správa certifikátů PKCS pomocí Intune](certficates-pfx-configure.md)  
- [Vytvoření importovaného profilu certifikátu PKCS](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

Další informace o [konektorech certifikátů](certificate-connectors.md)