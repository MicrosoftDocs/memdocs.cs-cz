---
title: Nastavení Intune pro aplikaci učebny pro iOS/iPadOS
titleSuffix: Microsoft Intune
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení pro aplikaci učeben na zařízeních s iOS/iPadOS.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 1381a5ce-c743-40e9-8a10-4c218085bb5f
ms.reviewer: derriw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 104996e87c830701b1725129727c76d8c7a09ee3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326875"
---
# <a name="how-to-configure-intune-settings-for-the-iosipados-classroom-app"></a>Jak nakonfigurovat nastavení Intune pro aplikaci pro iOS/iPadOS

> [!NOTE]
> Intune v současné době nepodporuje konfiguraci aplikace učebny. Tento článek platí jenom pro uživatele, kteří mají stávající vzdělávací profily pro iOS/iPadOS v Intune.  

## <a name="introduction"></a>Úvod
[Classroom](https://itunes.apple.com/app/id1085319084) je aplikace, která učitelům umožňuje vést výuku a ovládat zařízení studentů v učebně. Učitelé například můžou:

- Otevírat aplikace na zařízeních studentů
- Zamykat a odemykat obrazovku iPadu
- Prohlížet obrazovku iPadu studenta
- Přejít v iPadech studentů na záložku nebo kapitolu v knize
- Ukázat obrazovku iPadu studenta na Apple TV

K nastavení učebny na zařízení budete muset vytvořit a nakonfigurovat profil vzdělávacího zařízení pro iOS nebo iPadOS v Intune.

## <a name="before-you-start"></a>Než začnete

Než tato nastavení začnete konfigurovat, zvažte následující skutečnosti:

- Učitelé i studenti musí být zaregistrovaní v Intune.
- Zajistěte, aby na zařízení učitele byla nainstalovaná aplikace [Apple Classroom](https://itunes.apple.com/us/app/classroom/id1085319084?mt=8). Můžete aplikaci nainstalovat buď ručně, nebo přes [správu aplikací Intune](../apps/app-management.md).
- Musíte nakonfigurovat certifikáty pro ověřování připojení mezi zařízeními učitelů a studentů (viz krok 2, vytvoření a přiřazení vzdělávacího profilu pro iOS/iPadOS v Intune).
- iPady učitelů a studentů musí být ve stejné síti Wi-Fi a musí mít povolené Bluetooth.
- Aplikace učebny se spouští na iPady pod dohledem, na kterém běží iOS/iPadOS 9,3 nebo novější.
- V této verzi podporuje Intune správu scénáře 1:1, kdy má každý student svůj vlastní vyhrazený iPad.


## <a name="step-1---import-your-school-data-into-azure-active-directory"></a>Krok 1 – Import školních dat do služby Azure Active Directory

Pomocí služby Microsoft SDS (School Data Sync) naimportujte školní záznamy z existujícího studentského informačního systému (SIS) do služby Azure Active Directory (Azure AD).
Služba SDS synchronizuje informace z vašeho systému SIS a uloží je do služby Azure AD. Azure AD je systém správy od Microsoftu, který pomáhá s organizací uživatelů a zařízení. Tato data vám pak pomohou se správou vašich studentů a zařízení. [Přečtěte si další informace o nasazení SDS](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91).

### <a name="how-to-import-data-using-sds"></a>Jak naimportovat data pomocí SDS

Informace můžete do SDS naimportovat jednou z následujících metod:

- [Soubory CSV](https://support.office.com/article/Follow-these-steps-71d5fe4a-aa51-4f35-9b53-348898a390a1) – ruční export a sestavení textových souborů s oddělovačem (.csv)
- [PowerSchool API](https://support.office.com/article/Follow-these-steps-851b5edc-558f-43a9-9122-b2d63458cb8f) – poskytovatel SIS, který zjednodušuje synchronizaci se službou Azure AD
- [OneRoster](https://support.office.com/article/Follow-these-steps-f43cbb2a-b502-497d-a8b1-783dc05a57ab) – formát CSV, který můžete exportovat a konvertovat pro synchronizaci se službou Azure AD

### <a name="find-out-more"></a>Další informace

- [Další informace o úplné synchronizaci místních školních dat se službou Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)
- [Další informace o službě Microsoft SDS (School Data Sync](https://sds.microsoft.com/)
- [Další informace o licencování ve službě Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-whatis-azure-portal)

## <a name="step-2---create-and-assign-an-iosipados-education-profile-in-intune"></a>Krok 2 – Vytvoření a přiřazení vzdělávacího profilu pro iOS/iPadOS v Intune

### <a name="configure-general-settings"></a>Konfigurace obecných nastavení

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Konfigurace zařízení**.
2. V podokně **Konfigurace zařízení** v části **Spravovat** zvolte **Profily**.
5. V podokně profilů zvolte **Vytvořit profil**.
6. V podokně **vytvořit profil** zadejte **název** a **Popis** vzdělávacího profilu pro iOS/iPadOS.
7. Z rozevíracího seznamu **Platforma** zvolte **iOS**.
8. Z rozevíracího seznamu **Typ profilu** zvolte **Vzdělávání**.
9. Zvolte **Nastavení** > **Konfigurovat**.


Teď si vytvoříte certifikáty k navázání vztahu důvěryhodnosti mezi iPady učitelů a studentů. Certifikáty se používají k bezproblémovému a bezobslužnému ověřování připojení mezi zařízeními bez nutnosti zadávání uživatelských jmen a hesel.

>[!IMPORTANT]
>Použité certifikáty učitelů a studentů musí být vystavené odlišnými certifikačními autoritami (CA). Musíte vytvořit dvě nové podřízené certifikační autority propojené s vaší existující certifikační infrastrukturou; jednu pro učitele a druhou pro studenty.

Vzdělávací profily iOS podporují pouze certifikáty PFX. Certifikáty SCEP podporovány nejsou.

Vytvořené certifikáty musí podporovat ověřování serverů i ověřování uživatelů.

### <a name="configure-teacher-certificates"></a>Konfigurace certifikátů učitelů

V podokně **Vzdělávání** zvolte **Certifikáty učitelů**.

#### <a name="configure-teacher-root-certificate"></a>Konfigurace kořenového certifikátu učitele

V části **Kořenový certifikát učitele** vyberte tlačítko Procházet. Vyberte kořenový certifikát s jednou z těchto přípon:
- .cer (DER nebo s kódováním Base64) 
- .P7B (s úplným řetězem nebo bez něj)

#### <a name="configure-teacher-pkcs12-certificate"></a>Konfigurace certifikátu PKCS#12 učitele

V části **Certifikát PKCS#12 učitele** nakonfigurujte následující hodnoty:

- **Formát názvu subjektu** – Intune automaticky přidá k běžnému názvu certifikátu učitele předponu **leader**. K certifikátu studenta přidává předponu **member**.
- **Certifikační autorita** – Certifikační autorita organizace (CA), která běží na verzi Enterprise systému Windows Server 2008 R2 nebo novější. Samostatná certifikační autorita není podporovaná. 
- **Název certifikační autority** – Zadejte název certifikační autority.
- **Název šablony certifikátu** – Zadejte název šablony certifikátu, která byla přidána k vystavující certifikační autoritě. 
- **Prahová hodnota obnovení (%)** – Zadejte procento doby životnosti certifikátu zbývající v okamžiku, kdy zařízení požádá o obnovení certifikátu.
- **Období platnosti certifikátu** – Zadejte zbývající dobu do vypršení platnosti certifikátu.
Zadat můžete hodnotu nižší, než je období platnosti zadané v šabloně certifikátu, ne však vyšší. Pokud je třeba období platnosti certifikátu v šabloně certifikátu dva roky, můžete zadat hodnotu jeden rok, ale ne pět let. Tato hodnota musí být zároveň nižší než zbývající doba platnosti certifikátu vystavující certifikační autority.

Jakmile dokončíte konfiguraci certifikátů, zvolte **OK**.

### <a name="configure-student-certificates"></a>Konfigurace certifikátů studentů

1. V podokně **Vzdělávání** zvolte **Certifikáty studentů**.
2. V podokně **Certifikáty studentů** zvolte v seznamu **Typ certifikátů studentských zařízení** možnost **1:1**.

#### <a name="configure-student-root-certificate"></a>Konfigurace kořenového certifikátu studenta

V části **Kořenový certifikát studenta** vyberte tlačítko Procházet. Vyberte kořenový certifikát s jednou z těchto přípon:
- .cer (DER nebo s kódováním Base64) 
- .P7B (s úplným řetězem nebo bez něj)

#### <a name="configure-student-pkcs12-certificate"></a>Konfigurace certifikátu PKCS#12 studenta

V části **Certifikát PKCS#12 studenta** nakonfigurujte následující hodnoty:

- **Formát názvu subjektu** – Intune automaticky přidá k běžnému názvu certifikátu učitele předponu **leader**. K certifikátu studenta přidává předponu **member**.
- **Certifikační autorita** – Certifikační autorita organizace (CA), která běží na verzi Enterprise systému Windows Server 2008 R2 nebo novější. Samostatná certifikační autorita není podporovaná. 
- **Název certifikační autority** – Zadejte název certifikační autority.
- **Název šablony certifikátu** – Zadejte název šablony certifikátu, která byla přidána k vystavující certifikační autoritě. 
- **Prahová hodnota obnovení (%)** – Zadejte procento doby životnosti certifikátu zbývající v okamžiku, kdy zařízení požádá o obnovení certifikátu.
- **Období platnosti certifikátu** – Zadejte zbývající dobu do vypršení platnosti certifikátu.
Zadat můžete hodnotu nižší, než je období platnosti zadané v šabloně certifikátu, ne však vyšší. Pokud je třeba období platnosti certifikátu v šabloně certifikátu dva roky, můžete zadat hodnotu jeden rok, ale ne pět let. Tato hodnota musí být zároveň nižší než zbývající doba platnosti certifikátu vystavující certifikační autority.

Jakmile dokončíte konfiguraci certifikátů, zvolte **OK**.

## <a name="finish-up"></a>Dokončení

1. V podokně **Vzdělávání** zvolte OK.
2. V podokně **Vytvořit profil** zvolte **Vytvořit**.

Profil se vytvoří a zobrazí se v podokně se seznamem profilů.

Přiřaďte profil ke studentským zařízením ve skupinách učebny, které se vytvořily při synchronizaci školních dat se službou Azure AD (viz [Přiřazení profilů zařízení](../configuration/device-profile-assign.md)).

## <a name="next-steps"></a>Další kroky

Když teď učitel použije aplikaci Classroom, bude mít plnou kontrolu nad zařízeními studentů.

Další informace o aplikaci Classroom najdete v [nápovědě pro Classroom](https://help.apple.com/classroom/ipad/2.0/) na webu Applu.

Pokud chcete konfigurovat sdílená zařízení iPad pro studenty, podívejte se na článek o [konfiguraci nastavení vzdělávání Intune pro sdílená zařízení s iOSem](education-settings-configure-ios-shared.md).
