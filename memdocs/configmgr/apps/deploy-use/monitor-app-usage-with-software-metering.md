---
title: Sledování využití aplikací pomocí monitorování míry využívání softwaru
titleSuffix: Configuration Manager
description: Přečtěte si o operacích, které jsou k dispozici v Configuration Manager měření softwaru.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710080"
---
# <a name="software-metering-in-configuration-manager"></a>Monitorování míry využívání softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje referenční informace pro všechny operace, které můžete provést při použití Configuration Manager měření softwaru.

> [!IMPORTANT]
>  Monitorování míry využívání softwaru se používá ke sledování desktopových aplikací pro osobní počítače s Windows, jejichž název souboru končí na **.exe**. Monitorování míry využívání softwaru nesleduje moderní aplikace pro Windows (třeba aplikace využívané systémem Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Požadavky pro monitorování míry využívání softwaru
Monitorování míry využívání softwaru nemá žádné externí závislosti, jenom závislosti v rámci produktu.

|Závislost|Další informace|
|----------------|----------------------|
|Nastavení klienta pro monitorování míry využívání softwaru|Aby se dalo použít monitorování míry využívání softwaru, musí být klientské nastavení **Povolit měření softwaru na klientských počítačích** povolené a nasazené do počítačů. Nastavení monitorování míry využívání softwaru můžete nasadit do všech počítačů v hierarchii, nebo můžete nasadit vlastní nastavení do skupiny počítačů. Viz **Konfigurace monitorování míry využívání softwaru** v tomto tématu.|
|Bod služby Reporting services|Bod služby Reporting Services musíte nakonfigurovat, abyste mohli zobrazit sestavy monitorování míry využívání softwaru. Další informace najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Configure software metering
 Tento postup nakonfiguruje výchozí nastavení klienta pro monitorování míry využívání softwaru a použije se pro všechny počítače ve vaší hierarchii. Pokud toto nastavení chcete použít jenom pro některé počítače, vytvořte vlastní nastavení klienta zařízení a nasaďte ho do kolekci obsahující počítače, na kterých chcete používat monitorování míry využívání softwaru. Další informace o tom, jak vytvořit vlastní nastavení zařízení, najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).

1. V konzole Configuration Manager klikněte na **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.

2. Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.

3. V dialogovém okně **Výchozí nastavení** klikněte na **Monitorování míry využívání softwaru**.

4. V seznamu **Nastavení zařízení** nakonfigurujte toto nastavení:

   -   **Povolit měření softwaru na klientských počítačích**: Pokud chcete monitorování míry využívání softwaru povolit, vyberte **True** .

   -   **Shromáždění dat plánu**: Nakonfigurujte, jak často se mají shromažďovat data monitorování míry využívání softwaru z klientských počítačů. Použijte výchozí hodnotu každých **7 dnů** nebo klikněte na **Plán** a zadejte vlastní plán.

5. Kliknutím na **OK** zavřete dialogové okno **Výchozí nastavení** .

   Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a> Vytvoření pravidel monitorování míry využívání softwaru
 Pomocí Průvodce vytvořením pravidla pro měření softwaru vytvořte nové pravidlo monitorování míry využívání softwaru pro váš Configuration Manager Web.

1.  V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů** > **monitorování míry využívání softwaru**.

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit pravidlo pro měření softwaru**.

4.  Na stránce **Obecné** v Průvodci vytvořením pravidla pro měření softwaru zadejte následující informace:

    -   **Název** – název pravidla monitorování míry využívání softwaru. Měl by být jedinečný a popisný.

        > [!NOTE]
        >  Pravidla monitorování míry využívání softwaru se můžou jmenovat stejně, pokud se liší název souboru, který je v nich uvedený.

    -   **Název souboru** – název programového souboru, u kterého chcete monitorovat využití. Kliknutím na tlačítko **Procházet** můžete zobrazit dialogové okno **Otevřít** , ve kterém můžete vybrat požadovaný programový soubor.

        > [!NOTE]
        >  Pokud do pole **Název souboru** zadáte název spustitelného souboru, neprovedou se žádné kontroly, jestli tento soubor existuje nebo jestli v hlavičce obsahuje nezbytné informace. Pokud to jde, klikněte na **Procházet** a vyberte spustitelný soubor, který se má monitorovat.
        >
        >  Zástupné znaky nejsou v názvu souboru povolené.
        >
        >  Pokud je zadaná hodnota **Původní název souboru** , není použití tohoto pole povinné.

    -   **Původní název souboru** – název spustitelného souboru, u kterého chcete monitorovat využití. Tento název odpovídá informacím v hlavičce souboru, a ne vlastnímu názvu souboru. Může proto být užitečný případech, kdy se spustitelný soubor přejmenoval, ale chcete monitorovat na základě jeho původního názvu.

        > [!NOTE]
        >  Zástupné znaky nejsou v původním názvu souboru povolené.
        >
        >  Pokud je zadaná hodnota **Název souboru** , není použití tohoto pole povinné.

    -   **Verze** – verze spustitelného souboru, který chcete monitorovat. Můžete použít zástupný znak (&#42;) k vyjádření libovolného řetězce znaků nebo zástupného znaku (? ), který představuje libovolný jeden znak. Pokud chcete měřič pro všechny verze spustitelného souboru, použijte výchozí hodnotu (&#42;).

    -   **Jazyk** – jazyk spustitelného souboru, který se má monitorovat. Výchozí hodnotou je aktuální národní prostředí operačního systému, který používáte. Pokud jste spustitelný soubor, který chcete monitorovat, vybrali kliknutím na **Procházet** a v hlavičce tohoto souboru jsou uvedené jazykové informace, vyplní se toto pole automaticky. Pokud chcete monitorovat všechny jazykové verze, v rozevíracím seznamu vyberte **Libovolný** .

    -   **Popis** –volitelný popis pravidla monitorování míry využívání softwaru.

    -   **Použijte toto pravidlo měření softwaru na následující klienty** – vyberte, jestli se toto pravidlo monitorování míry využívání softwaru má použít pro všechny klienty v hierarchii nebo jenom pro klienty, kteří jsou přiřazení lokalitě uvedené v seznamu **Lokalita** .

5.  Pokračujte kliknutím na tlačítko **Další**.

6.  Zkontrolujte nastavení, potvrďte ho a potom dokončete průvodce. Vytvoří se pravidlo monitorování míry využívání softwaru. Toto nové pravidlo monitorování míry využívání softwaru se zobrazí v pracovním prostoru **Prostředky a kompatibilita** v uzlu **Monitorování míry využívání softwaru** .

##  <a name="configure-automatic-software-metering-rules"></a> Konfigurace automatických pravidel monitorování míry využívání softwaru
 Monitorování míry využívání softwaru v Configuration Manager můžete nakonfigurovat tak, aby automaticky generovala zakázaná pravidla monitorování míry využívání softwaru z nedávných dat inventáře využití uchovávaných v databázi lokality. Tato inventární data můžete nakonfigurovat tak, aby se pravidla monitorování vytvořila jenom pro aplikace, které se využívají na zadaném procentu počítačů. Můžete také určit maximální počet automaticky generovaných pravidel monitorování míry využívání softwaru, který je v lokalitě povolený.

> [!NOTE]
>  Ve výchozím nastavení jsou všechna automaticky vytvořená pravidla monitorování míry využívání softwaru zakázaná. Než začnete pomocí těchto pravidel shromažďovat údaje o využití, musíte je povolit.

1.  V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů** > **monitorování míry využívání softwaru**a potom na kartě **Domů** ve skupině **Nastavení** klikněte na **Vlastnosti měření softwaru**.

3.  V dialogovém okně **Vlastnosti měření softwaru** nakonfigurujte toto nastavení:

    -   **Uchovávání dat (ve dnech)** – určuje dobu, kterou s data generovaná pravidly monitorování míry využívání softwaru uchovávají v databázi lokality. Výchozí hodnota je **90** dní.

    -   Povolte možnost **Automaticky vytvářet zakázaná pravidla pro měření z posledních dat inventáře využití**.

    -   **Zadejte procentuální podíl počítačů v hierarchii, které musí použít program, než je automaticky vytvořeno pravidlo pro měření softwaru** – výchozí hodnota je **10** procent.

    -   **Zadejte počet pravidel pro měření softwaru, který musí být překročen v hierarchii, než bude zakázáno automatické vytváření pravidel** – výchozí hodnota je **100** pravidel.

4.  Kliknutím na **OK** zavřete dialogové okno **Vlastnosti měření softwaru** .

##  <a name="manage-software-metering-rules"></a> Správa pravidel monitorování míry využívání softwaru
 V pracovním prostoru **Prostředky a kompatibilita** vyberte **Monitorování míry využívání softwaru**, vyberte pravidlo monitorování míry využívání softwaru, které chcete spravovat, a potom vyberte úlohu správy.

 Následující tabulka obsahuje podrobnosti o úlohách správy, které mohou před výběrem vyžadovat určité informace.

|Úloha správy|Podrobnosti|
|---------------------|-------------|
|**Povolení**<br /><br /> **Zakázat**|Povolí nebo zakáže pravidlo monitorování míry využívání softwaru. Toto nastavení se stáhne do klientských počítačů podle nastavení **Interval dotazování zásad klienta** v oddílu **Zásady klienta** (ve výchozím nastavení je to každých 60 minut).<br /><br /> Viz [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md) .|

##  <a name="monitor-software-metering"></a>Monitorování monitorování míry využívání softwaru
 Monitorování míry využívání softwaru v Configuration Manager zahrnuje řadu předdefinovaných sestav, které umožňují sledovat informace o operacích monitorování míry využívání softwaru. Tyto sestavy spadají do kategorie **Monitorování míry využívání softwaru**.

 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).

 Kromě toho můžete vytvářet dotazy a kolekce založené na datech uložených v Configuration Manager databázi podle monitorování míry využívání softwaru.

 Další informace o kolekcích v Configuration Manager najdete v tématu [Úvod do kolekcí](../../core/clients/manage/collections/introduction-to-collections.md).

 Další informace o dotazech v Configuration Manager najdete v tématu [Úvod do dotazů](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Zabezpečení a ochrana osobních údajů pro monitorování míry využívání softwaru

### <a name="security-issues-for-software-metering"></a>Problémy se zabezpečením monitorování míry využívání softwaru
 Útočník by mohl do Configuration Manager odeslat neplatné informace o monitorování míry využívání softwaru, které bod správy přijme, i když je nastavení klienta monitorování míry využívání softwaru zakázáno. Výsledkem může být velký počet pravidel monitorování, které se replikují v celé hierarchii, což by způsobilo odepření služby v síti a Configuration Manager serverů lokality.

 Protože útočník může vytvořit neplatná data monitorování míry využívání softwaru, neměli byste data monitorování míry využívání softwaru považovat za směrodatná.

 Ve výchozím klientském nastavení je monitorování míry využívání softwaru povolené.

###  <a name="privacy-information-for-software-metering"></a> Ochrana osobních údajů při monitorování míry využívání softwaru
 Při monitorování míry využívání softwaru se sleduje využití aplikací v klientských počítačích. Ve výchozím nastavení je monitorování míry využívání softwaru povolené. Musíte nakonfigurovat, které aplikace se mají monitorovat. Informace o měření jsou uloženy v databázi Configuration Manager. Informace jsou při přenosu do bodu správy zašifrované, ale v databázi Configuration Manager se neukládají v zašifrovaném tvaru.

 Tyto informace jsou v databázi uložené, dokud je neodstraní úlohy správy lokality **Odstranit stará data softwarového měření** (každých pět dní) a **Odstranit stará data shrnutí softwarového měření** (každých 270 dní). Můžete provést konfiguraci intervalu odstranění. Informace o monitorování se neposílají společnosti Microsoft.

 Před konfigurací monitorování míry využívání softwaru zvažte své požadavky na ochranu osobních údajů.

## <a name="example-scenario-for-using-software-metering"></a>Ukázkový scénář použití monitorování míry využívání softwaru
 V této části vytvoříte ukázkové pravidlo monitorování míry využívání softwaru, které vám může pomoct vyřešit následující požadavky:

- Určit, kolik kopií konkrétní aplikace se ve vaší firmě používá

- Vyhledat všechny nepoužívané kopie aplikace

- Určit, kteří uživatelé konkrétní aplikaci pravidelně používají

  Společnost Woodgrove Bank nasadila Microsoft Office 2010 jako svou standardní sadu kancelářského softwaru. Kvůli podpoře starší verze aplikace se v některých počítačích musí i dál spouštět Microsoft Office Word 2003. Oddělení IT chce snížit náklady na podporu a licencování tím, že tyto kopie Wordu 2003 odebere, pokud se starší verze aplikace už nepoužívá. Helpdesk chce taky určit, kteří uživatelé starší verzi aplikace používají.

  Správce systému IT v Woodgrove Bank používá měření softwaru v Configuration Manager k dosažení těchto obchodních cílů. Správce provede následující akce:

- Kontroluje požadavky na monitorování míry využívání softwaru a potvrdí, že bod služby Reporting Services je nainstalovaný a funkční.
- Nakonfiguruje výchozí nastavení klienta pro monitorování míry využívání softwaru:<br>Správce povolí monitorování míry využívání softwaru a použije výchozí plán shromažďování dat každých 7 dní.<br>Správce nakonfiguruje inventář softwaru na soubory inventáře, které mají příponu. exe, nakonfigurováním nastavení klienta inventáře softwaru **inventář těchto typů souborů**.<br>Správce přidá nové pravidlo monitorování míry využívání softwaru s názvem **Woodgrove. exe**pro monitorování starší verze aplikace.
- Počká po dobu sedmi dnů, po jejímž uplynutí klientské počítače začnou nahlásit data o využití pro spustitelný soubor **Woodgrove. exe** .
- Správce používá ke **všem monitorovaným softwarovým programům instalaci sestav Configuration Manager pro všechny monitorované softwarové programy** , aby bylo možné zjistit, které počítače mají načtenou aplikaci **Woodgrove. exe** .
- Po šesti měsících správce spustí sestavu **počítače s nainstalovaným monitorovaným programem, ale nespouštěl program od zadaného data, zadá**pravidlo monitorování míry využívání softwaru a datum v minulosti šest měsíců. Tato sestava identifikuje 120 počítačů, ve kterých se program za  posledních šest měsíců nespustil.
- Správce provede další kontroly a potvrdí, že starší verze aplikace není na identifikovaných počítačích vyžadována. Správce pak z těchto počítačů odinstaluje starší verzi aplikace a kopii Wordu 2003.<br>Správce spustí sestavu **Uživatelé spouštějící určitý monitorovaný softwarový program** a poskytne helpdesku seznam uživatelů, kteří nadále používají starší verzi aplikace.
- Správce bude v případě potřeby nadále kontrolovat sestavy monitorování míry využívání softwaru a v případě potřeby provede nápravné akce.

  Výsledkem celé akce je snížení nákladů na licencování a podporu IT díky odebrání aplikací, které se už nevyžadují. Helpdesk navíc má seznam uživatelů, kteří využívají starší verzi aplikace.
