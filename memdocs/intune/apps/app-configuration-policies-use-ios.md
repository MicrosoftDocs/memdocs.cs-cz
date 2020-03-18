---
title: Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOS nebo iPadOS
titleSuffix: Microsoft Intune
description: Naučte se používat zásady konfigurace aplikací k poskytování konfiguračních dat do aplikace pro iOS/iPadOS při jejím spuštění.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a110b268c31f4e1ee5dada6554215b648449f01
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326351"
---
# <a name="add-app-configuration-policies-for-managed-iosipados-devices"></a>Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOS nebo iPadOS

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Zásady konfigurace aplikací v Microsoft Intune slouží k poskytování vlastních nastavení konfigurace pro aplikaci pro iOS/iPadOS. Tato nastavení konfigurace umožňují přizpůsobit aplikaci na základě směru dodavatele aplikace. Tato nastavení (klíče a hodnoty) vám poskytne dodavatel aplikace. Při konfiguraci aplikace je zadáváte jako klíče a hodnoty, nebo jako XML, které je obsahuje.

Jako správce Microsoft Intune můžete řídit, které uživatelské účty se přidají do aplikací Microsoft Office na spravovaných zařízeních. Můžete omezit přístup jenom na povolené uživatelské účty organizace a zablokovat osobní účty zaregistrovaných zařízení. Podpůrné aplikace zpracují konfiguraci aplikace a odeberou a zablokují neschválené účty. Nastavení zásad konfigurace se použije, když ho aplikace zjistí (obvykle při prvním spuštění aplikace).

Jakmile přidáte zásady konfigurace aplikace, můžete u těchto zásad konfigurace aplikací nastavit přiřazení. Když nastavíte přiřazení zásad, můžete zahrnout a vyloučit skupiny uživatelů, na které se zásady vztahují. Když zvolíte možnost zahrnout jednu nebo více skupin, můžete zahrnout konkrétní nebo integrované skupiny. Mezi integrované skupiny patří **Všichni uživatelé**, **Všechna zařízení** a **Všichni uživatelé a všechna zařízení**. 

> [!NOTE]
> V Intune máte v konzole pohodlně k dispozici předem vytvořené skupiny **Všichni uživatelé** a **Všechna zařízení** s integrovanými optimalizacemi. Důrazně doporučujeme použít tyto skupiny k zacílení na všechny uživatele a všechna zařízení místo na skupiny všichni uživatelé nebo všechna zařízení, které jste mohli sami vytvořit.

Když máte vybrané zahrnuté skupiny pro zásady konfigurace aplikace, můžete také konkrétní skupiny vyloučit. Podrobnosti najdete v tématu [Zahrnutí a vyloučení přiřazení aplikací v Microsoft Intune](apps-inc-exl-assignments.md).

> [!TIP]
> Tento typ zásad je nyní k dispozici pouze pro zařízení se systémem iOS/iPadOS 8,0 a novějším. Podporuje následující typy instalací aplikací:
>
> - **Spravovaná aplikace pro iOS/iPadOS z App Storu**
> - **Balíček aplikace pro iOS**
>
> Další informace o typech instalace aplikací najdete v tématu [Přidání aplikace do Microsoft Intune](apps-add.md). Další informace o zahrnutí konfigurace aplikace do balíčku aplikace. IPA pro spravovaná zařízení najdete v tématu Konfigurace spravované aplikace v [dokumentaci pro vývojáře pro iOS](https://developer.apple.com/library/archive/samplecode/sc2279/Introduction/Intro.html).

## <a name="create-an-app-configuration-policy"></a>Vytvoření zásad konfigurace aplikací

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat** > **spravovaná zařízení**. Všimněte si, že si můžete vybrat mezi **spravovanými zařízeními** a **spravovanými aplikacemi**. Další informace najdete v tématu [aplikace, které podporují konfiguraci aplikací](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. Na stránce **základy** nastavte následující podrobnosti:
    - **Název**: Název profilu, který se zobrazí na portálu Azure Portal
    - **Popis**: Popis profilu, který se zobrazí na portálu Azure Portal
    - **Typ registrace zařízení** – toto nastavení je nastavené na **spravovaná zařízení**.
4. Jako **platformu**vyberte **iOS/iPadOS** .
5. Klikněte na **Vybrat aplikaci** vedle **cílové aplikace**. Zobrazí se podokno **přidružená aplikace** . 
6. V podokně **cílová aplikace** vyberte spravovanou aplikaci, kterou chcete přidružit k zásadám konfigurace, a klikněte na **OK**.
7. Kliknutím na **Další** zobrazte stránku **Nastavení** .
8. V rozevíracím seznamu vyberte **formát nastavení konfigurace**. Chcete-li přidat informace o konfiguraci, vyberte jednu z následujících metod:
    - **Použití návrháře konfigurace**
    - **Zadání XML dat**<br><br>
    Podrobnosti o používání návrháře konfigurace najdete v části [Použití návrháře konfigurace](#use-configuration-designer). Podrobnosti o zadávání XML dat najdete v části [Zadání XML dat](#enter-xml-data). 
9. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
10. V rozevíracím seznamu vedle pole **přiřadit k**vyberte možnost **vybrané skupiny**, **Všichni uživatelé**, **všechna zařízení**nebo **Všichni uživatelé a všechny** oddálení, aby bylo možné zásadu konfigurace aplikace přiřadit k.

    ![Snímek obrazovky s přiřazením zásad – karta Zahrnout](./media/app-configuration-policies-use-ios/app-config-policy01.png)

11. Vyberte možnost **Všichni uživatelé** v rozevíracím seznamu.

    ![Snímek obrazovky s přiřazením zásad – možnost rozevírací nabídky Všichni uživatelé](./media/app-configuration-policies-use-ios/app-config-policy02.png)

12. Klikněte na možnost **Vybrat skupiny, které se vyloučí** a zobrazte tak související podokno.

    ![Snímek obrazovky s přiřazením zásad – vyberte skupiny, které chcete vyloučit.](./media/app-configuration-policies-use-ios/app-config-policy03.png)

13. Vyberte skupiny, které chcete vyloučit, a potom klikněte na **Vybrat**.

    >[!NOTE]
    >Pokud přidáváte skupinu a pro daný typ přiřazení už byla zahrnuta jakákoliv jiná skupina, je pro ostatní typy zahrnutí přiřazení předem vybraná a není ji možné změnit. Tato použitá skupina se tedy nedá použít jako vyloučená skupina.

14. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** .
15. Kliknutím na **vytvořit** přidejte zásady konfigurace aplikací do Intune.

## <a name="use-configuration-designer"></a>Použití návrháře konfigurace

Microsoft Intune poskytuje konfigurační nastavení jedinečná pro aplikaci. Návrháře konfigurace můžete použít u aplikací jak v zařízeních, která jsou zaregistrovaná v Microsoft Intune, tak i v zařízeních, která zaregistrovaná nejsou. Návrhář umožňuje nakonfigurovat konkrétní klíče a hodnoty konfigurace, které vám pomohou při vytváření základního XML. Pro každou hodnotu musíte také zadat datový typ. Nastavení se aplikacím poskytují automaticky při instalaci.

### <a name="add-a-setting"></a>Přidání nastavení

1. Pro každý klíč a hodnotu v konfiguraci nastavte:
   - **Konfigurační klíč**: Klíč, který jedinečně identifikuje konkrétní konfiguraci nastavení
   - **Typ hodnoty**: Datový typ konfigurační hodnoty Mezi typy patří integer, real, string a boolean.
   - **Hodnota konfigurace**: Hodnota konfigurace
2. Zvolte **OK** a nastavte tak nastavení konfigurace.

### <a name="delete-a-setting"></a>Odstranění nastavení

1. Zvolte tři tečky ( **...** ) vedle příslušného nastavení.
2. Vyberte **Odstranit**.

Znaky \{\{ a \}\} se používají jenom pro typy tokenů a nesmí se používat pro jiné účely.

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Povolte jenom nakonfigurované účty organizace v aplikacích s více identitami 

Pro zařízení s iOS/iPadOS použijte následující páry klíč/hodnota:

| **Klíč** | **Hodnoty** |
|----|----|
| IntuneMAMAllowedAccountsOnly | <ul><li>**Povolené**: Jediný povolený účet je spravovaný uživatelský účet definovaný klíčem [IntuneMAMUPN](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).</li><li>**Zakázané** (nebo libovolná hodnota, která se neshoduje malými a velkými písmeny s **Povolené**): Je povolený libovolný účet.</li></ul> |
| IntuneMAMUPN | <ul><li>Hlavní název uživatele (UPN) účtu, kterému se povoluje přihlašovat k aplikaci</li><li> Pro zařízení zaregistrovaná v Intune se může použít token <code>{{userprincipalname}}</code>, aby představoval účet zaregistrovaného uživatele.</li></ul>  |

   > [!NOTE]
   > Je nutné použít OneDrive pro iOS 10,34 nebo novější, Outlook pro iOS 2.99.0 nebo novější nebo Edge pro iOS 44.8.7 nebo novější a aplikace musí být cílem [zásad ochrany aplikací Intune](app-protection-policy.md) , když se povolují jenom nakonfigurované účty organizace s více identitami.

## <a name="enter-xml-data"></a>Zadání XML dat

Můžete zadat nebo vložit seznam vlastností XML, který obsahuje nastavení konfigurace aplikace pro zařízení zaregistrovaná v Intune. Formát seznamu vlastností XML se liší v závislosti na aplikaci, kterou konfigurujete. Podrobnosti o přesném formátu, který se má použít, získáte od dodavatele aplikace.

Intune ověří formát XML. Intune ale nekontroluje, jestli seznam vlastností XML funguje s cílovou aplikací.

Další informace o seznamech vlastností XML:

- Projděte si informace uvedené v článku [Vysvětlení seznamů vlastností XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) v knihovně pro vývojáře aplikací pro iOS.

### <a name="example-format-for-an-app-configuration-xml-file"></a>Příklad formátu pro soubor XML konfigurace aplikací

Když vytvoříte soubor konfigurace aplikací, můžete pomocí tohoto formátu zadat jednu nebo několik následujících hodnot:

```xml
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
  <key>aaddeviceid</key>
  <string>{{aaddeviceid}}</string>
</dict>
```

### <a name="supported-xml-plist-data-types"></a>Podporované datové typy v seznamu vlastností XML

Intune podporuje v seznamu vlastností následující typy dat:

- &lt;integer&gt;
- &lt;real&gt;
- &lt;string&gt;
- &lt;array&gt;
- &lt;dict&gt;
- &lt;true /&gt; nebo &lt;false /&gt;

### <a name="tokens-used-in-the-property-list"></a>Tokeny použité v seznamu vlastností

Intune dál v seznamu vlastností podporuje následující typy tokenů:
- \{\{userPrincipalName\}\}– například **jan\@contoso.com**
- \{\{mail\}\}– například **jan\@contoso.com**
- \{\{partialupn\}\} – například **John**
- \{\{accountid\}\} – například **fc0dc142-71d8-4b12-bbea-bae2a8514c81**
- \{\{deviceid\}\} – například **b9841cd9-9843-405f-be28-b2265c59ef97**
- \{\{userid\}\} – například **3ec2c00f-b125-4519-acf0-302ac3761822**
- \{\{username\}\} – například **John Doe**
- \{\{sériové\}\}– například **F4KN99ZUG5V2** (pro zařízení s iOS/iPadOS)
- \{\{serialnumberlast4digits\}\}– například **G5V2** (pro zařízení se systémem iOS/iPadOS)
- \{\{aaddeviceid\}\} – například **ab0dc123-45d6-7e89-aabb-cde0a1234b56**

## <a name="configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices"></a>Konfigurace aplikace Portál společnosti pro podporu zařízení s iOS a iPadOS DEP

Registrace programu DEP (Apple Program registrace zařízení) nejsou kompatibilní s verzí Portál společnosti aplikace App Storu. Aplikaci Portál společnosti můžete ale nakonfigurovat tak, aby podporovala zařízení se systémem iOS/iPadOS DEP pomocí následujících kroků.

1. V Intune v případě potřeby přidejte aplikaci Portál společnosti Intune, a to tak, že na > **aplikace** **Intune** > **všechny aplikace** > **Přidat**.
2. Pokud chcete vytvořit zásady konfigurace aplikace pro Portál společnosti aplikaci, můžete přejít na **aplikace** > **zásady konfigurace aplikací**.
3. V níže uvedeném XML vytvořte zásadu konfigurace aplikace. Další informace o tom, jak vytvořit zásadu konfigurace aplikace a zadat data XML, najdete v tématu [Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOS/iPadOS](app-configuration-policies-use-ios.md).

    ``` xml
    <dict>
        <key>IntuneCompanyPortalEnrollmentAfterUDA</key>
        <dict>
            <key>IntuneDeviceId</key>
            <string>{{deviceid}}</string>
            <key>UserId</key>
            <string>{{userid}}</string>
        </dict>
    </dict>
    ```

3. Nasaďte Portál společnosti do zařízení se zásadami konfigurace aplikace, které cílí na požadované skupiny. Nezapomeňte zásadu nasadit jenom do skupin zařízení, která jsou už zaregistrovaná v DEP.
4. Sdělte koncovým uživatelům, aby se k aplikaci Portál společnosti přihlásili při automatické instalaci.

## <a name="monitor-iosipados--app-configuration-status-per-device"></a>Monitorování stavu konfigurace aplikace pro iOS/iPadOS na zařízení 
Po přiřazení zásady konfigurace můžete monitorovat stav konfigurace aplikace pro iOS/iPadOS pro každé spravované zařízení. V části **Microsoft Intune** na portálu Azure Portal vyberte **Zařízení** > **Všechna zařízení**. V seznamu spravovaných zařízení vyberte konkrétní zařízení, ve kterém se má zobrazit podokno pro zařízení. V podokně zařízení vyberte **Konfigurace aplikace**.  

## <a name="additional-information"></a>Další informace

- [Nasazení Outlooku pro iOS/iPadOS a nastavení konfigurace aplikací pro Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Další kroky

Pokračujte s [přiřazením](apps-deploy.md) a [sledováním](apps-monitor.md) aplikace.
