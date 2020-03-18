---
title: Nastavení sdíleného zařízení v Intune pro aplikaci pro iOS/iPadOS
titleSuffix: Microsoft Intune
description: Přečtěte si o nastaveních Intune, pomocí kterých můžete řídit nastavení pro aplikaci učeben na zařízeních s iOS/iPadOS.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/06/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 1381a5ce-c743-40e9-8a10-4c218085bb5f
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8612640ec71075194af680535a988f2228bb66fd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332647"
---
# <a name="configure-intune-education-settings-for-shared-ipad-devices"></a>Konfigurace nastavení vzdělávání Intune pro sdílená zařízení iPad

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

> [!NOTE]
> Intune v současné době nepodporuje konfiguraci aplikace učebny. Tento článek platí jenom pro uživatele, kteří mají stávající vzdělávací profily pro iOS/iPadOS v Intune.

Intune podporuje aplikaci pro iOS/iPadOS, která učitelům umožňuje seznámení s výukou a řízení zařízení studenta v učebně. Kromě aplikace Classroom podporuje Apple také možnost nakonfigurovat studentská zařízení iPad tak, aby mohlo jedno zařízení používat více studentů. Tento dokument vás provede využitím této možnosti pomocí Intune.

Informace o konfiguraci vyhrazených zařízení iPad (1:1) pro použití aplikace učebny najdete v tématu [jak nakonfigurovat nastavení Intune pro aplikaci pro iOS/iPadOS](education-settings-configure-ios.md).

## <a name="before-you-start"></a>Než začnete

Sdílení zařízení iPad vyžaduje, abyste nejprve provedli následující kroky:

- Nastavte [Apple School Manager](../enrollment/apple-school-manager-set-up-ios.md) a [School Data Sync (SDS)](https://support.office.com/article/Apple-School-Manager-integration-with-Intune-for-Education-and-School-Data-Sync-974bd1f9-2c7a-45cb-9447-b58166108617).
- V rámci nastavení Apple School Manageru nakonfigurujte pro studenty [spravovaná Apple ID](http://help.apple.com/schoolmanager/#/tes78b477c81). [Další informace o spravovaných Apple ID](https://support.apple.com/HT205918).
- Vytvořte registrační profil pro sériová čísla zařízení synchronizovaných prostřednictvím Apple School Manageru.

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

Dále potřebujete certifikáty k navázání vztahu důvěryhodnosti mezi iPady učitelů a studentů. Certifikáty se používají k bezproblémovému a bezobslužnému ověřování připojení mezi zařízeními bez nutnosti zadávání uživatelských jmen a hesel.

>[!Important]
>Použité certifikáty učitelů a studentů musí být vystavené odlišnými certifikačními autoritami (CA). Musíte vytvořit dvě nové podřízené certifikační autority propojené s vaší existující certifikační infrastrukturou; jednu pro učitele a druhou pro studenty.

Vzdělávací profily iOS podporují pouze certifikáty PFX. Certifikáty SCEP podporovány nejsou.

Certifikáty, které vytvoříte, musí kromě ověřování uživatelů podporovat také ověřování serverů.

### <a name="configure-teacher-certificates"></a>Konfigurace certifikátů učitelů

V podokně **Vzdělávání** zvolte **Certifikáty učitelů**.

#### <a name="configure-teacher-root-certificate"></a>Konfigurace kořenového certifikátu učitele

V části **Kořenový certifikát učitele** vyberte tlačítkem Procházet kořenový certifikát učitele s příponou .cer (DER nebo s kódováním Base64) nebo .P7B (s úplným řetězem nebo bez).

#### <a name="configure-teacher-pkcs12-certificate"></a>Konfigurace certifikátu PKCS#12 učitele

V části **Certifikát PKCS#12 učitele** nakonfigurujte následující hodnoty:

- **Formát názvu subjektu** – Intune automaticky přidá k běžnému názvu certifikátu předponu **leader** pro certifikát učitele a předponu **member** pro certifikát studenta.
- **Certifikační autorita** – Certifikační autorita organizace (CA), která běží na verzi Enterprise systému Windows Server 2008 R2 nebo novější. Samostatná certifikační autorita není podporovaná.
- **Název certifikační autority** – Zadejte název certifikační autority.
- **Název šablony certifikátu** – Zadejte název šablony certifikátu, která byla přidána k vystavující certifikační autoritě.
- **Prahová hodnota obnovení (%)** – Zadejte procento doby životnosti certifikátu zbývající v okamžiku, kdy zařízení požádá o obnovení certifikátu.
- **Období platnosti certifikátu** – Zadejte zbývající dobu do vypršení platnosti certifikátu. Zadat můžete hodnotu nižší, než je období platnosti zadané v šabloně certifikátu, ne však vyšší. Pokud je třeba období platnosti certifikátu v šabloně certifikátu dva roky, můžete zadat hodnotu jeden rok, ale ne pět let. Tato hodnota musí být zároveň nižší než zbývající doba platnosti certifikátu vystavující certifikační autority.

Po dokončení konfigurace certifikátů učitelů zvolte **OK**.

### <a name="configure-student-certificates"></a>Konfigurace certifikátů studentů

1. V podokně **Vzdělávání** zvolte **Certifikáty studentů**.
2. V podokně **Certifikáty studentů** zvolte v seznamu **Typ certifikátů studentských zařízení** možnost **Sdílené iPady**.

#### <a name="configure-student-root-certificate"></a>Konfigurace kořenového certifikátu studenta

V části **Kořenový certifikát zařízení** vyberte tlačítkem Procházet kořenový certifikát studenta s příponou .cer (DER nebo s kódováním Base64) nebo .P7B (s úplným řetězem nebo bez).

#### <a name="configure-device-pkcs12-certificate"></a>Konfigurace certifikátu PKCS#12 zařízení

V části **Certifikát PKCS#12 studenta** nakonfigurujte následující hodnoty:

- **Formát názvu subjektu** – Intune automaticky přidá k běžnému názvu certifikátu předponu leader pro certifikát učitele a předponu member pro certifikát zařízení.
- **Certifikační autorita** – Certifikační autorita organizace (CA), která běží na verzi Enterprise systému Windows Server 2008 R2 nebo novější. Samostatná certifikační autorita není podporovaná.
- **Název certifikační autority** – Zadejte název certifikační autority.
- **Název šablony certifikátu** – Zadejte název šablony certifikátu, která byla přidána k vystavující certifikační autoritě.
- **Prahová hodnota obnovení (%)** – Zadejte procento doby životnosti certifikátu zbývající v okamžiku, kdy zařízení požádá o obnovení certifikátu.
- **Období platnosti certifikátu** – Zadejte zbývající dobu do vypršení platnosti certifikátu. Zadat můžete hodnotu nižší, než je období platnosti zadané v šabloně certifikátu, ne však vyšší. Pokud je třeba období platnosti certifikátu v šabloně certifikátu dva roky, můžete zadat hodnotu jeden rok, ale ne pět let. Tato hodnota musí být zároveň nižší než zbývající doba platnosti certifikátu vystavující certifikační autority.

Až dokončíte konfiguraci certifikátů, zvolte **OK**.

### <a name="complete-certificate-setup"></a>Dokončení nastavení certifikátu

1. V podokně **Vzdělávání** zvolte **OK**.
2. V podokně **Vytvořit profil** zvolte **Vytvořit**.

Profil se vytvoří a zobrazí se v podokně se seznamem profilů.

## <a name="step-3---create-a-device-category"></a>Krok 3 – Vytvoření kategorie zařízení

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Registrace zařízení**.
4. V podokně **Registrace zařízení – Přehled** zvolte **Kategorie zařízení**.
5. V podokně **Registrace zařízení – Kategorie zařízení** zvolte **Vytvořit**.
6. V podokně **Vytvořit kategorii zařízení** zadejte **Název** a **Popis** kategorie.
7. V podokně **Vytvořit kategorii zařízení** zvolte **Vytvořit**.

Kategorie zařízení se vytváří v podokně **Registrace – Kategorie zařízení**.

## <a name="step-4--create-a-dynamic-group"></a>Krok 4 – Vytvoření dynamické skupiny

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Skupiny**.
4. V podokně **Uživatelé a skupiny – Všechny skupiny** zvolte **Nová skupina**.
5. V podokně **Skupina** vyberte **Typ skupiny** a pak zadejte **Název** a **Popis** skupiny.
6. Z rozevíracího seznamu **Typ členství** zvolte **Dynamické zařízení**.
7. Zvolte **Členové s dynamickými zařízeními** a vytvořte pravidla členství.
8. V podokně**Pravidla dynamického členství**:
1. Z rozevíracího seznamu **Přidat zařízení, kde** vyberte atribut **deviceCategory**.
2. Zvolte **Rovná se**.
3. Zadejte kategorii zařízení, kterou jste vytvořili v prázdném textovém poli.
9. V podokně**Pravidla dynamického členství** zvolte **Přidat dotaz**.
10. V podokně **Skupina** vyberte **Vytvořit**.

Dynamická skupina se vytvoří v podokně **Uživatelé a skupiny – Všechny skupiny**.

## <a name="step-5--assign-a-device-to-a-category-carts"></a>Krok 5 – Přiřazení zařízení do kategorie (Košíky)

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Zařízení**.
4. V podokně **Zařízení** zvolte **Všechna zařízení**.
5. V podokně **Zařízení – Všechna zařízení** zvolte zařízení.
6. V podokně zařízení zvolte **Vlastnosti**.
7. V podokně vlastností zařízení zadejte kategorii zařízení do textového pole **Kategorie zařízení**.
8. V podokně zařízení zvolte **Uložit**.

Zařízení je teď přidružené ke kategorii zařízení. Zopakujte tento postup u všech zařízení, která chcete k vytvořené kategorii zařízení přidružit.

## <a name="step-6--create-classroom-profiles"></a>Krok 6 – Vytvoření profilů učeben

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Konfigurace zařízení**.
4. V podokně **Konfigurace zařízení** zvolte **Spravovat** > **Profily košíků**.
5. V podokně profilů zvolte **Vytvořit profil**.
6. V podokně **Vytvořit přiřazení** zadejte **Název** a **Popis**.
7. Zvolte **Vyberte třídy** > **Konfigurovat** a přiřaďte skupiny k profilu košíku.
8. Zvolte třídy, které chcete do profilu košíku zahrnout, a potom zvolte **Vybrat**. 
9. Zvolte **Vyberte košíky** > **Konfigurovat** a přiřaďte skupiny k profilu košíku.
10. Zvolte skupiny, které chcete do profilu košíku zahrnout, a potom zvolte **Vybrat**.
11. V podokně **Vytvořit přiřazení** vyberte **Uložit**. Profil košíku se uloží.

Profil se vytvoří a zobrazí se v podokně se seznamem profilů.

## <a name="step-7---assign-the-cart-profile-to-classes"></a>Krok 7 – Přiřazení profilu košíku třídám

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. V podokně **Intune** zvolte **Konfigurace zařízení**.
4. V podokně **Konfigurace zařízení** zvolte **Monitorovat** > **Stav přiřazení**.
5. V podokně **Stav přiřazení** vyberte **Profil košíku**, který jste vytvořili.
6. V podokně **Profil košíku** zvolte **Přiřazení** a pak v nabídce **Zahnout** zvolte **Vybrat skupiny, které se zahrnou**.
7. Vyberte třídy, na které se má profil košíku uplatnit (nevybírejte skupinu), a potom zvolte **Vybrat**. 
8. Po dokončení zvolte **Uložit**.

Přiřazení se dokončí a Intune použije profil učebny na cílová zařízení podle přiřazení učebny.

## <a name="next-steps"></a>Další kroky

Studenti teď mohou zařízení navzájem sdílet. Každý student může vzít kterýkoli iPad v učebně a po přihlášení pomocí PIN kódu se mu zobrazí jeho vlastní obsah. Další informace o sdílených iPadech najdete na [webu společnosti Apple](https://www.apple.com/education/it/).
