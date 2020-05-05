---
title: Hledání nápovědy
titleSuffix: Configuration Manager
description: Další informace o Configuration Manager najdete v materiálech.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6610e86c12b6f7704b65dc11c476fa09e8f2ae63
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722904"
---
# <a name="find-help-for-using-configuration-manager"></a>Najít nápovědu k použití Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku najdete následující oddíly s více prostředky, které vám pomůžou najít nápovědu k používání Configuration Manager:  

- [Dokumentace k produktu](#bkmk_Info)  

- [Sdílení názoru na produkt](#product-feedback)  

- [Postupujte na blogu Configuration Manager týmu.](#BKMK_ProductGroupBlog)  

- [Možnosti podpory a komunitní zdroje](#BKMK_SupportOptions)  

Nápovědu k přístupnosti produktů najdete v tématu [funkce usnadnění](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a>Dokumentace k produktu  

Chcete-li získat přístup k nejaktuálnější dokumentaci k produktu, začněte v [indexu knihovny](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Tipy k hledání, poskytování zpětné vazby a další informace o používání dokumentace k produktu najdete v tématu [Jak používat dokumenty](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a>Váš názor na produkt od verze 1806

Od verze Configuration Manager 1806 můžete odeslat zpětnou vazbu produktu přímo z konzoly. Pokud potřebujete připojit protokoly, použijte [Centrum zpětné vazby](#BKMK_FeedbackHub). Můžete provést následující akce: <!--1357542-->

- **Poslat smajlíka**: pošlete nám svůj názor na to, co se vám líbilo.
- **Odeslání zamračení**: pošlete nám svůj názor na to, co jste nechtěli.
- **Odeslání návrhu**: přejdete na [Web UserVoice](https://configurationmanager.uservoice.com/) , abyste mohli svůj nápad sdílet.

  ![Odeslat názor v Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Poslat smajlíka nebo odeslat zamračení

Pokud chcete poslat svůj názor na něco, co se vám líbí, postupujte podle následujících pokynů:

1. V pravém horním rohu konzoly klikněte na Veselý obličej.
2. V rozevírací nabídce vyberte **odeslat smajlíka** nebo **Odeslat zamračení**.
3. Pomocí textového pole můžete vysvětlit, co se vám líbilo nebo co se vám nelíbilo. 
4. Vyberte, jestli chcete sdílet svou e-mailovou adresu a snímek obrazovky.
5. Klikněte na **Odeslat názor** .
     - Pokud nemáte připojení k Internetu, v dolní části klikněte na **Uložit** . Postupujte podle pokynů v části [odeslání zpětné vazby, kterou jste uložili pro pozdější odeslání](#BKMK_NoInternet) , a odešlete ji společnosti Microsoft. 

![Odeslat formulář zpětné vazby v Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Stavové zprávy pro odeslání smajlíka
<!--5891852-->
Počínaje Configuration Manager 2002 se při **odeslání smajlíka** nebo **odeslání zamračení**vytvoří stavová zpráva, která se vytvoří při odeslání zpětné vazby. Toto vylepšení poskytuje záznam o:
- Při odeslání zpětné vazby
- Kdo odeslal zpětnou vazbu
- ID zpětné vazby
- Pokud bylo odeslání zpětné vazby úspěšné nebo ne
   - ID zprávy 53900 pro úspěšné odeslání
   - ID zprávy 53901 pro odeslání, které selhalo.

Zobrazit stavové zprávy z **monitorování** > stavového**systému** > **dotazy stavových**zpráv. Začněte dotazem **všechny stavové zprávy** a vyberte svůj časový rámec. Po načtení zpráv klikněte na tlačítko **filtrovat zprávy** a filtr pro zprávu s ID 53900 nebo 53901.

Pokud [Odešlete zpětnou vazbu, kterou jste uložili pro pozdější odeslání,](find-help.md#BKMK_NoInternet)stavové zprávy se nevytvoří.

[![Stavová zpráva pro úspěšné odeslání zpětné vazby](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Poslat návrh

Když **pošlete návrh**, budete přesměrováni na web [UserVoice](https://configurationmanager.uservoice.com/), který bude mít na webu třetí strany, abyste mohli svůj nápad sdílet. Tým Configuration Manager produktů používá následující hodnoty stavu služby UserVoice:

- **Uvedeno** , porozuměli jsme žádosti a dává smysl. Přidali jsme ho do seznamu nevyřízených položek.
- **Plánováno** – pro tuto funkci jsme zahájili kódování a očekáváme, že se v průběhu několika následujících měsíců zobrazí v buildu pro verzi Preview.
- **Spuštěno** – Tato funkce je nyní ve verzi Preview. Podívejte se na ni a sdělte nám svůj názor. Dejte nám prosím jistotu, jestli je funkce na správné dráze. V části komentáře původní žádosti, aby ostatní viděli a komentovat, vložte další zpětnou vazbu. Přečteme to a použijeme zpětnou vazbu k pokusu o vylepšení funkce.
- **Dokončeno** – první verze funkce je v produkčním sestavení. Tento stav neznamená, že jsme v rámci této funkce provedli 100%, a už ji nebudete zlepšovat. Ale to znamená, že verze V1 funkcí je v produkčním sestavení, a můžete ji začít používat pro reálné účely. Označení bylo dokončeno z těchto důvodů:
  - Chceme, abyste věděli, že tato funkce je připravená pro produkční prostředí.
  - Chceme vaše hlasy ve službě UserVoice předat, abyste je mohli používat na dalších položkách.
  - Nové žádosti o změnu návrhu pro tuto funkci můžete zazálohovat, abychom nám pomohli zjistit další nejdůležitější vylepšení této funkce.

### <a name="information-sent-with-feedback"></a>Informace odesílané pomocí zpětné vazby

Když **odešlete smajlíka** nebo **odešlete zamračení**, odešlou se následující informace s názory:

- Informace o sestavení operačního systému
- ID Configuration Manager hierarchie
- Informace o sestavení produktu
- Informace o jazyku
- Identifikátor zařízení 
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SQMClient: MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a>Odeslat zpětnou vazbu, kterou jste uložili pro pozdější odeslání

1. V dolní části okna **poskytnout zpětnou vazbu** klikněte na **Uložit** . 
2. Uložte soubor. zip. Pokud místní počítač nemá přístup k Internetu, zkopírujte soubor na počítač připojený k Internetu. 
3. V případě potřeby zkopírujte složku UploadOfflineFeedback nacházející se v`cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Další informace o složce CD. poslední najdete [na disku CD. Poslední složka](../servers/manage/the-cd.latest-folder.md)

4. Na počítači připojeném k Internetu otevřete příkazový řádek. 
5. Spusťte následující příkaz:`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Volitelně můžete zadat následující parametry:
        -  `-t, --timeout`Časový limit pro odeslání dat v sekundách 0 je neomezený. Výchozí hodnota je 30.
        - `-s --silent`Žádné protokolování do konzoly (nelze kombinovat s--verbose)
        - `-v, --verbose`Výstup podrobného protokolování do konzoly (nemůže kombinovat s--Silent)
        - `--help`Zobrazí obrazovku help.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a>Potvrzení zpětné vazby z konzoly

<!--3556010-->
Od verze 1902 se při odesílání zpětné vazby prostřednictvím konzoly Configuration Manager nebo souboru UploadOfflineFeedback. exe zobrazí potvrzovací zpráva. Tato zpráva obsahuje **ID zpětné vazby**, které můžete společnosti Microsoft poskytnout jako identifikátor sledování.

- Chcete-li zkopírovat **ID zpětné vazby**, vyberte ikonu kopírování vedle ID nebo použijte klávesovou zkratku **CTRL** + **C** .
  - Tento identifikátor není uložený na vašem počítači, proto ho nezapomeňte před zavřením okna zkopírovat.
- Kliknutím na tlačítko **tuto zprávu už nezobrazovat** potlačíte dialog a zabráníte v jejich zobrazení v budoucnu.

   ![Potvrzení zpětné vazby z konzoly nástroje v Configuration Manager 1902](media/1902-feedback-id-example.png)
- Nástroj příkazového řádku **UploadOfflineFeedback** zapisuje **FeedbackID** do konzoly, pokud se nepoužívá-s nebo--Silent.

  ![Potvrzení zpětné vazby z UploadOfflineFeedback. exe v Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a>Názory na produkt pro verze 1802 a starší

Nahlaste potenciální vady produktu prostřednictvím integrované [aplikace centra pro názory](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) na Windows 10. Když **přidáte novou zpětnou vazbu**, nezapomeňte vybrat kategorii **Správa podniku** a pak vybrat jednu z následujících podkategorií:
- Klient nástroje Configuration Manager
- Konzola nástroje Configuration Manager
- Configuration Manager nasazení operačního systému
- Server Configuration Manager

Pokračujte na [stránku UserVoice](https://configurationmanager.uservoice.com/) a hlaste se s novými nápady k funkcím v Configuration Manager. Tým Configuration Manager produktů používá následující hodnoty stavu služby UserVoice:

- **Uvedeno** , porozuměli jsme žádosti a dává smysl. Přidali jsme ho do seznamu nevyřízených položek.
- **Plánováno** – pro tuto funkci jsme zahájili kódování a očekáváme, že se v průběhu několika následujících měsíců zobrazí v buildu pro verzi Preview.
- **Spuštěno** – Tato funkce je nyní ve verzi Preview. Podívejte se na ni a sdělte nám svůj názor. Dejte nám prosím jistotu, jestli je funkce na správné dráze. V části komentáře původní žádosti, aby ostatní viděli a komentovat, vložte další zpětnou vazbu. Přečteme to a použijeme zpětnou vazbu k pokusu o vylepšení funkce.
- **Dokončeno** – první verze funkce je v produkčním sestavení. Tento stav neznamená, že jsme v rámci této funkce provedli 100%, a už ji nebudete zlepšovat. Ale to znamená, že verze V1 funkcí je v produkčním sestavení, a můžete ji začít používat pro reálné účely. Označení bylo dokončeno z těchto důvodů:
  - Chceme, abyste věděli, že tato funkce je připravená pro produkční prostředí.
  - Chceme vaše hlasy ve službě UserVoice předat, abyste je mohli používat na dalších položkách.
  - Nové žádosti o změnu návrhu pro tuto funkci můžete zazálohovat, abychom nám pomohli zjistit další nejdůležitější vylepšení této funkce.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a>Blog týmu Configuration Manager  

Configuration Manager technické a partnerské týmy používají [blog Enterprise mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) k poskytování technických informací a dalších zpráv o Configuration Manager a souvisejících technologiích. Naše příspěvky blogu doplňují dokumentaci k produktu a informace o podpoře.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a>Možnosti podpory a komunitní zdroje  

Následující odkazy obsahují informace o možnostech podpory a komunitních zdrojích:  

-   [Podpora Microsoftu](https://aka.ms/cmcbsupport)  

-   [Configuration Manager komunita: Příručka pro přežití Configuration Manager (Current Branch)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Stránka Configuration Manager fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
