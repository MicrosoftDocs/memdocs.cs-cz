---
title: Přizpůsobení samoobslužného portálu
titleSuffix: Configuration Manager
description: Přidání vlastních informací specifických pro organizaci na Samoobslužný portál pro správu BitLockeru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713069"
---
# <a name="customize-the-self-service-portal"></a>Přizpůsobení samoobslužného portálu

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Po [instalaci samoobslužného portálu BitLocker](setup-websites.md)ho můžete přizpůsobit pro vaši organizaci. Přidejte vlastní oznámení, název vaší organizace a další informace specifické pro danou organizaci.

## <a name="branding"></a>Branding

Brandingujte Samoobslužný portál s názvem vaší organizace, adresou URL helpdesku a textem oznámení.

1. Na webovém serveru, který je hostitelem samoobslužného portálu, se přihlaste jako správce.

1. Spusťte **správce Internetová informační služba (IIS)** (spusťte příkaz **inetmgr. exe**).

1. Rozbalte **lokality**, rozbalte **výchozí web**a vyberte uzel **samoobslužný** . V podokně podrobností, ve skupině **ASP.NET** otevřete **nastavení aplikace**.

    [![Příklad obrazovky nastavení aplikace samoobslužný ve Správci služby IIS](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Vyberte položku, kterou chcete změnit, a v podokně **Akce** vyberte **Upravit**. Změňte **hodnotu** na nový název, který chcete použít.

    > [!CAUTION]
    > Neměňte hodnoty **názvu** . Například neměňte `CompanyName`, změňte `Contoso IT`. Pokud změníte hodnoty **názvu** , Samoobslužný portál přestane fungovat.

Změny se projeví okamžitě.

### <a name="supported-branding-values"></a>Podporované hodnoty brandingu

Hodnoty, které lze nastavit, naleznete v následující tabulce:

|Název|Popis|Výchozí&nbsp;hodnota|
|--- |--- |--- |
|CompanyName|Název organizace, který Samoobslužný portál zobrazuje jako záhlaví v horní části každé stránky.|`Contoso IT`|
|DisplayNotice|Zobrazí úvodní oznámení, které musí uživatel potvrdit.|`true`|
|HelpdeskText|Řetězec v pravém podokně "pro všechny ostatní související problémy"|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Odkaz na řetězec HelpdeskText|obsahovat|
|NoticeTextPath|Text počátečního oznámení, které musí uživatel potvrdit. Ve výchozím nastavení je `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`úplná cesta k souboru na webovém serveru. Upravte a uložte soubor v editoru prostého textu. Tato hodnota cesty je relativní vzhledem k aplikaci samoobslužný.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Snímek obrazovky s výchozím samoobslužným portálem najdete v tématu [Samoobslužný portál BitLocker](self-service-portal.md).

> [!TIP]
> V případě potřeby můžete některé z těchto řetězců lokalizovat k zobrazení v různých jazycích. Další informace najdete v tématu [lokalizace](#bkmk_localize).

## <a name="session-time-out"></a>Časový limit relace

Pokud chcete, aby platnost relace uživatele po zadaném období nečinnosti vyprší, můžete změnit nastavení časového limitu relace pro samoobslužný portál.

1. Na webovém serveru, který je hostitelem samoobslužného portálu, se přihlaste jako správce.

1. Spusťte **správce Internetová informační služba (IIS)** (spusťte příkaz **inetmgr. exe**).

1. Rozbalte **lokality**, rozbalte **výchozí web**a vyberte uzel **samoobslužný** . V podokně podrobností, ve skupině **ASP.NET** otevřete **stav relace**.

1. Ve skupině **nastavení souborů cookie** změňte hodnotu **časového limitu (v minutách)** . Je to počet minut, po jejichž uplynutí vyprší relace uživatele. Výchozí hodnota je `5`. Pokud chcete nastavení zakázat, aby nedošlo k vypršení časového limitu, nastavte hodnotu na `0`.

1. V podokně **Akce** vyberte **použít**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a>Text a adresa URL pro lokalizaci

Můžete nakonfigurovat lokalizované verze příkazu samoobslužného portálu `HelpdeskText` a `HelpdeskUrl` propojit. Tento řetězec informuje uživatele o tom, jak získat další nápovědu při používání portálu. Pokud konfigurujete lokalizovaný text, portál zobrazí lokalizovanou verzi webových prohlížečů v daném jazyce. Pokud se nenalezne lokalizovaná verze, zobrazí se výchozí hodnota v `HelpdeskText` nastaveních `HelpdeskUrl` a.

1. Na webovém serveru, který je hostitelem samoobslužného portálu, se přihlaste jako správce.

1. Spusťte **správce Internetová informační služba (IIS)** (spusťte příkaz **inetmgr. exe**).

1. Rozbalte **lokality**, rozbalte **výchozí web**a vyberte uzel **samoobslužný** . V podokně podrobností, ve skupině **ASP.NET** otevřete **nastavení aplikace**.

1. V podokně **Akce** vyberte **Přidat**.

1. V okně **Přidat nastavení aplikace** nakonfigurujte následující hodnoty:

    - **Název**: zadejte `HelpdeskText_<language>`, kde `<language>` je kód jazyka pro text.

      Chcete-li například vytvořit lokalizovaný `HelpdeskText` příkaz v španělštině (Španělsku), název je. `HelpdeskText_es-es`

    - **Hodnota**: lokalizovaný řetězec, který se má zobrazit v pravém podokně samoobslužného portálu, pro všechny ostatní související problémy

1. Výběrem **OK** uložte nové nastavení.

1. Tento postup opakujte, pokud chcete přidat nové nastavení aplikace `HelpdeskUrl_<language>` , které odpovídá přidruženému `HelpdeskText_<language>` nastavení.

Tento postup opakujte, pokud chcete přidat dvojici nastavení pro všechny jazyky, které ve vaší organizaci podporujete.

## <a name="localize-the-notice-file"></a>Lokalizovat soubor oznámení

Můžete nakonfigurovat lokalizované verze počátečního oznámení, které musí uživatel potvrdit na samoobslužném portálu. Ve výchozím nastavení je `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`úplná cesta k souboru na webovém serveru.

Chcete-li zobrazit lokalizovaný text poznámky, vytvořte lokalizovaný soubor s oznámením. txt. Pak ho uložte pod konkrétní jazykovou složku. Například: `Self Service Website\es-es\Notice.txt` for španělština (Španělsko).

Samoobslužný portál zobrazuje text oznámení na základě následujících pravidel:

- Pokud chybí výchozí soubor oznámení, portál zobrazí zprávu, že chybí výchozí soubor.

- Pokud vytvoříte lokalizovaný soubor oznámení v příslušné složce jazyka, zobrazí se text s lokalizovaným oznámením.

- Pokud webový server nenajde lokalizovanou verzi souboru oznámení, zobrazí se výchozí oznámení.

- Pokud uživatel nastaví prohlížeč na jazyk, který nemá lokalizované oznámení, zobrazí se na portálu výchozí oznámení.

### <a name="create-a-localized-notice-file"></a>Vytvoření lokalizovaného souboru oznámení

1. Na webovém serveru, který je hostitelem samoobslužného portálu, se přihlaste jako správce.

1. Vytvořte `<language>` složku pro každý podporovaný jazyk v cestě k `Self Service Website` aplikaci. Například `es-es` pro španělštinu (Španělsko). Ve výchozím nastavení je `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`úplná cesta.

    Seznam platných kódů jazyků, které můžete použít, najdete v [referenčních informacích k rozhraní API pro národní jazykovou podporu (NLS)](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > Název složky jazyka může být také jazykově neutrální název. Například **ES** pro španělštinu, nikoli **ES-ES** pro španělštinu (Španělsko) a **ES-ar** pro španělštinu (Argentina). Pokud uživatel nastaví svůj prohlížeč na **ES-ES**a tato složka jazyků neexistuje, webový server rekurzivně kontroluje nadřazené složky národního prostředí (**y**). (Nadřazená národní prostředí jsou definovaná v .NET.) Například`Self Service Website\es\Notice.txt`. Tento rekurzivní záložní prostředek napodobuje pravidla načítání prostředků .NET.

1. Vytvořte kopii výchozího souboru oznámení s lokalizovaným textem. Uložte ho do složky pro kód jazyka. Například pro španělštinu (Španělsko) je `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`ve výchozím nastavení úplná cesta.

Tento postup opakujte s lokalizovaným souborem oznámení pro všechny jazyky, které ve vaší organizaci podporujete.

## <a name="next-steps"></a>Další kroky

Teď, když jste nainstalovali a přizpůsobili Samoobslužný portál, zkuste to! Další informace najdete v tématu [Samoobslužný portál BitLocker](self-service-portal.md).
