---
title: Služba Endpoint Protection pro počítače s Windows
titleSuffix: Microsoft Intune
description: Chraňte své spravované počítače pomocí služby Endpoint Protection, která poskytuje ochranu proti malwarovým hrozbám v reálném čase.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/12/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 002241bf-6cd0-4c75-a4f0-891ac7e6721a
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c5a0a1405ceda93317dbefa6d80ec24cc0156bb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332479"
---
# <a name="help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune"></a>Pomoc se zabezpečením počítačů s Windows pomocí služby Endpoint Protection pro Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Microsoft Intune vám může pomoct zabezpečit spravované počítače pomocí služby Endpoint Protection, která zajišťuje ochranu v reálném čase proti malwarovým hrozbám, udržuje definice malwaru aktuální a automaticky kontroluje počítače. Endpoint Protection také poskytuje nástroje, které pomáhají se správou a monitorováním malwarových útoků.

Pokud jste ještě na svých počítačích nenainstalovali klienta Intune, přečtěte si téma [Instalace klienta na počítači s Windows pomocí Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Informace v následujících částech vám pomohou s konfigurací, nasazením a monitorováním služby Endpoint Protection.

## <a name="choose-when-to-use-endpoint-protection"></a>Rozhodnutí o tom, kdy používat službu Endpoint Protection
Jednou z vašich nejdůležitějších priorit jako správce IT je udržovat počítače, které spravujete, bez malwaru a virů. Před nasazením služby Intune do počítačů se systémem Windows ve vaší organizaci byste měli zvolením některé z následujících možností a nakonfigurováním příslušných nastavení zásad rozhodnout, jak tyto počítače chránit:


|                                                                                                                                                                       Chcete:                                                                                                                                                                        |                                                                                                       Nastavení zásad Endpoint Protection                                                                                                        |                                                                                                                                                  Další informace                                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                             Použít Microsoft Intune Endpoint Protection jenom v případě, že není nainstalovaná žádná aplikace koncové ochrany jiného výrobce.<br /><br />Microsoft Intune Endpoint Protection můžete použít na všech počítačích, kde není nainstalovaná aplikace koncové ochrany jiného výrobce.                                              | Nainstalovat službu Endpoint Protection = <strong>Ano</strong><br /><br />Povolit službu Endpoint Protection = <strong>Ano</strong><br /><br />Nainstalovat službu Endpoint Protection i v případě, že se nainstalovala aplikace koncové ochrany třetích stran = <strong>Ne</strong>  |                                                                      Pokud se detekuje aplikace koncové ochrany jiného výrobce, služba Microsoft Intune Endpoint Protection se nenainstaluje, a pokud byla dříve nainstalovaná, odinstaluje se.                                                                       |
| Použít službu Microsoft Intune Endpoint Protection i v případě, že je nainstalovaná aplikace koncové ochrany jiného výrobce.<br /><br />S tímto přístupem budete používat současně Microsoft Intune Endpoint Protection a aplikaci koncové ochrany jiného výrobce. Taková konfigurace se nedoporučuje kvůli možným problémům s výkonem. | Nainstalovat službu Endpoint Protection = <strong>Ano</strong><br /><br />Povolit službu Endpoint Protection = <strong>Ano</strong><br /><br />Nainstalovat službu Endpoint Protection i v případě, že se nainstalovala aplikace koncové ochrany třetích stran = <strong>Ano</strong> |                        Použijte, když:<br /><br />- Chcete přejít na používání Microsoft Intune Endpoint Protection.<br />- Nasazujete nového klienta, který bude používat Microsoft Intune Endpoint Protection.<br />- Upgradujete libovolného klienta, který bude používat Microsoft Intune Endpoint Protection.                         |
|                                                                                                             Použít Intune bez Microsoft Intune Endpoint Protection. Místo toho budete spoléhat na aplikaci koncové ochrany třetí strany.                                                                                                             |                                                                                                Nainstalovat službu Endpoint Protection = <strong>Ne</strong>                                                                                                 | Pokud nepoužíváte aplikaci koncové ochrany třetí strany, tato konfigurace se nedoporučuje, protože by počítače vaší organizace mohla vystavit malwaru nebo jiným útokům.<br /><br />Služba Microsoft Intune Endpoint Protection se nenainstaluje, a pokud byla dříve nainstalovaná, odinstaluje se. |

Pokud chcete přejít ze současné aplikace koncové ochrany na Microsoft Intune Endpoint Protection, postupujte podle následujících kroků:

1. Při nasazování klientského softwaru Intune do počítačů nechte stávající aplikaci koncové ochrany spuštěnou.

2. Ověřte, že je služba Microsoft Intune Endpoint Protection nainstalovaná a pomáhá zabezpečit klientské počítače.

3. Odeberte software koncové ochrany třetí strany:

    - Pomocí softwarové distribuce Intune nasaďte nástroj pro odebrání softwaru, který poskytuje výrobce aplikace koncové ochrany. Další informace najdete v tématu [Nasazení aplikací pomocí Microsoft Intune](../apps/apps-deploy.md).

    - Ručním odebráním aplikace koncové ochrany třetí strany.

> [!NOTE]
> Intune aplikace koncové ochrany třetích stran automaticky neodinstaluje.

## <a name="configure-microsoft-intune-endpoint-protection"></a>Konfigurace Microsoft Intune Endpoint Protection
Následující postup vám pomůže nakonfigurovat Endpoint Protection pro Microsoft Intune.

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) zvolte **Zásady** > **Přidat zásadu**.

2. Rozbalte položku **Správa počítače** a vyberte **Nastavení agenta Microsoft Intune**. Vyberte **Vytvoření a nasazení vlastních zásad**, abyste zadali zásady pro nastavení služby Endpoint Protection. Potom klikněte na tlačítko **Vytvořit zásadu**.

Můžete použít doporučená nastavení, nebo nastavení upravit. Pokud potřebujete více informací o vytvoření a nasazení zásad, přejděte k tématu [Běžné úlohy správy počítačů s Windows pomocí počítačového klienta Microsoft Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md).

  ![Nastavení služby Endpoint Protection](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-pc-endpoint-policy.png)

Nasazené zásady Endpoint Protection můžete zobrazit na stránce **Všechny zásady** pracovního prostoru **Zásady**.

## <a name="specify-endpoint-protection-service-settings"></a>Zadání nastavení služby Endpoint Protection

|                                                 Nastavení zásad                                                  |                                                                                                                                                                                                                                                                                                                                                                                                             Podrobnosti                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                  <strong>Nainstalovat službu Endpoint Protection</strong>                                   | Nastavte na <strong>Ano</strong>, pokud chcete nainstalovat Endpoint Protection na spravované počítače. Pokud se v průběhu instalace detekuje aplikace koncové ochrany jiného výrobce, Endpoint Protection se nainstaluje jenom v případě, že je zásada <strong>Nainstalovat službu Endpoint Protection i v případě, že byla nainstalována aplikace koncové ochrany třetích stran</strong> nastavená na <strong>Ano</strong>. <strong>Poznámka:</strong> Ve výchozím nastavení se Intune Endpoint Protection instaluje na spravované počítače. Pokud nechcete službu Endpoint Protection instalovat na spravované počítače, musíte tuto zásadu explicitně nastavit na <strong>Ne</strong>. Pokud už je služba Endpoint Protection nainstalovaná z dřívějška a zásada se aktualizuje na <strong>Ne</strong>, pak se klient Endpoint Protection odinstaluje.<br />Doporučená hodnota: <strong>Ano</strong> |
| <strong>Nainstalovat službu Endpoint Protection i v případě, že byla nainstalována aplikace koncové ochrany třetích stran</strong> |                                                                                                                                                                                                                                                                                                                Nastavte <strong>Ano</strong>, pokud chcete Microsoft Intune Endpoint Protection instalovat i v případě, že se detekuje aplikace koncové ochrany jiného výrobce.<br /><br />Doporučená hodnota: <strong>Ano</strong>                                                                                                                                                                                                                                                                                                                |
|                                   <strong>Povolit službu Endpoint Protection</strong>                                   |                                                                                                                                                                                                            Nastavte na <strong>Ano</strong>, pokud chcete povolit Microsoft Intune Endpoint Protection na počítačích, které mají klienta Endpoint Protection.<br /><br />Pokud je zásada nastavená na <strong>Ne</strong> a služba Microsoft Intune Endpoint Protection je nainstalovaná, uživatelské rozhraní klienta Endpoint Protection se uživatelům nezobrazí a všechny funkce ochrany jsou neaktivní.<br /><br />Doporučená hodnota: <strong>Ano</strong>                                                                                                                                                                                                             |
|                                       <strong>Zakázat uživatelské rozhraní klienta</strong>                                        |                                                                                                                                                                                                                                                                                                      Nastavte na <strong>Ano</strong>, pokud chcete uživatelům skrýt uživatelské rozhraní klienta Microsoft Intune Endpoint Protection (vyžaduje restartování počítače klienta).<br /><br />Doporučená hodnota: <strong>Ne</strong>                                                                                                                                                                                                                                                                                                       |
| <strong>Nainstalovat službu Endpoint Protection i v případě, že byla nainstalována aplikace koncové ochrany třetích stran</strong> |                                                                                                                                                                                                                                                                                                       Nastavte <strong>Ano</strong>, pokud chcete vynutit instalaci Microsoft Intune Endpoint Protection i v případě, že se detekuje aplikace koncové ochrany byla nainstalována aplikace koncové ochrany třetích stran.<br /><br />Doporučená hodnota: <strong>Ne</strong>                                                                                                                                                                                                                                                                                                       |
|                    <strong>Vytvořit bod obnovení systému před nápravou škod způsobených nebezpečným softwarem</strong>                    |                                                                                                                                                                                                                                                                                                                                 Nastavte na <strong>Ano</strong> , pokud chcete vytvořit bod obnovení systému Windows před zahájením nápravy škod způsobených malwarem.<br /><br />Doporučená hodnota: <strong>Ano</strong>                                                                                                                                                                                                                                                                                                                                  |
|                                 <strong>Sledovat vyřešené problémy s malwarem (dny)</strong>                                  |                                                                                                                                                                                                                                                                                      Umožňuje službě Endpoint Protection po určitou dobu sledovat vyřešené problémy s malwarem, abyste mohli ručně zkontrolovat dříve infikované počítače.<br /><br />Můžete určit hodnotu od 0 do 30 dnů.<br /><br />Doporučená hodnota: <strong>7 dnů</strong>                                                                                                                                                                                                                                                                                       |

Pokud jste nastavili hodnoty zásad **Nainstalovat službu Endpoint Protection** a **Povolit službu Endpoint Protection** na **Ano**a hodnotu zásady **Nainstalovat službu Endpoint Protection i v případě, že byla nainstalována aplikace koncové ochrany třetích stran** na **Ne**, služba Microsoft Intune Endpoint Protection zjistí, že je nainstalovaná jiná aplikace koncové ochrany. To znamená, že se služba Endpoint Protection nenainstaluje, a pokud už byla dříve nainstalovaná, odinstaluje se. Microsoft Intune Endpoint Protection však ve službě Intune podá hlášení o stavu jiné aplikace koncové ochrany.

  Ochrana v reálném čase Microsoft Security Essentials vás upozorní, když se bude chtít do počítače nainstalovat nežádoucí software představující potenciální hrozbu (viry, spyware a další) nebo se bude zkoušet spustit. V okamžiku, kdy k tomu dojde, se vám v oznamovací oblasti napravo od hlavního panelu zobrazí zpráva.

### <a name="specify-real-time-protection-settings"></a>Zadání nastavení ochrany v reálném čase

|Nastavení zásad|Podrobnosti|
|------------------|--------------------|
|**Povolit ochranu v reálném čase**|Umožňuje sledování a kontrolu všech souborů a aplikací, ke kterým se přistupuje. Blokuje taky všechny škodlivé soubory a aplikace ještě před jejich spuštěním na počítačích.<br /><br />Doporučená hodnota: **Ano**|
|**Kontrolovat všechny stahované soubory**|Umožňuje kontrolu všech souborů a příloh, které se stahují z internetu do počítačů.<br /><br />Doporučená hodnota: **Ano**|
|**Sledovat činnost souborů a programů v počítačích**|Umožňuje sledování příchozích a odchozích souborů a aktivitu programů na počítačích. S tímto nastavením může Endpoint Protection sledovat, když se soubory a programy spouštějí, a upozornit vás na všechny akce, které samy provádějí, nebo akce, které se s nimi provádějí.<br /><br />Doporučená hodnota: **Ano**|
|**Sledované soubory**|Umožňuje zvolit, jestli se budou sledovat jenom příchozí, odchozí nebo všechny soubory.<br /><br />Doporučená hodnota: **Monitorovat všechny soubory**|
|**Povolit monitorování chování**|Umožňuje, aby služba Microsoft Intune Endpoint Protection kontrolovala určité vzorce podezřelých aktivit na klientských počítačích.<br /><br />Doporučená hodnota: **Ano**|
|**Povolit systém kontroly sítě**|Povolí systém kontroly sítě (NIS) na klientských počítačích. Systém NIS používá signatury známých slabých míst z [Centra společnosti Microsoft pro ochranu před škodlivým softwarem](https://go.microsoft.com/fwlink/?LinkId=234249) ke zjištění a blokování škodlivého síťového provozu.<br /><br />Doporučená hodnota: **Ano**|

  ![Nastavení ochrany v reálném čase pro Endpoint Protection](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-pc-policy-realtime.png)

### <a name="specify-scan-schedule-settings"></a>Zadání nastavení plánu kontrol

|Nastavení zásad|Další informace|
|------------------|--------------------|
|**Naplánovat každodenní rychlou kontrolu**|Naplánuje denní rychlou kontrolu často používaných souborů a důležitých systémových souborů na počítačích. Tato rychlá kontrola má minimální vliv na výkon.<br /><br />Doporučená hodnota: **Ano**|
|**Spustit rychlou kontrolu, pokud se neuskutečnily dvě po sobě následující rychlé kontroly**|Nakonfiguruje službu Endpoint Protection, aby na počítačích automaticky spustila rychlou kontrolu, pokud na nich neproběhly dvě po sobě následující rychlé kontroly.<br /><br />Doporučená hodnota: **Ano**|
|**Naplánovat úplnou kontrolu**|Nakonfiguruje úplnou kontrolu všech souborů a prostředků na místních pevných discích počítačů. Tato kontrola může nějakou dobu trvat a může ovlivnit výkon počítače (doba závisí na počtu kontrolovaných souborů a prostředků).<br /><br />Doporučená hodnota: **Ne**|
|**Spustit úplnou kontrolu, pokud se neuskutečnily dvě po sobě následující úplné kontroly**|Nakonfiguruje službu Endpoint Protection, aby na počítačích automaticky spustila úplnou kontrolu, pokud na nich neproběhly dvě po sobě následující úplné kontroly.<br /><br />Doporučená hodnota: Nenakonfigurováno|

### <a name="specify-scan-options-settings"></a>Zadat nastavení možností kontroly

|Nastavení zásad|Podrobnosti|
|------------------|--------------------|
|**Po instalaci služby Endpoint Protection spustit úplnou kontrolu**|Nastavení na hodnotu **Ano** nakonfiguruje službu Endpoint Protection, aby po instalaci na počítačích automaticky spustila úplnou kontrolu systému. Tato kontrola běží jenom v případě, že jsou počítače v nečinnosti, aby se minimalizoval vliv na produktivitu uživatelů.<br /><br />Doporučená hodnota: **Ano**|
|**Automaticky spouštět úplnou kontrolu v případě potřeby po odebrání malwaru**|Nastavte na **Ano**, pokud chcete, aby služba Endpoint Protection automaticky spustila úplnou kontrolu systému na počítačích po odstranění malwaru kvůli ověření, že to neovlivnilo ostatní soubory.<br /><br />Doporučená hodnota: **Ano**|
|**Spustit naplánovanou kontrolu pouze v případě, že je počítač v nečinnosti**|Nastavte na **Ano** , pokud chcete zabránit spouštění naplánovaných kontrol, když se počítače používají, aby nedocházelo ke snížení produktivity uživatelů.<br /><br />Doporučená hodnota: **Ano**|
|**Před zahájením kontroly zkontrolovat nejnovější definice malwaru**|Nastavte na **Ano**, pokud chcete, aby služba Endpoint Protection před spuštěním kontroly na počítačích automaticky vyhledala nejnovější definice malwaru.<br /><br />Doporučená hodnota: **Ano**|
|**Prohledat archivní soubory**|Nastavte na **Ano**, pokud chcete nakonfigurovat, aby služba Endpoint Protection na počítačích kontrolovala malware v souborech archivu (jako jsou soubory ZIP nebo CAB).<br /><br />Doporučená hodnota: **Ne**|
|**Kontrolovat e-mailové zprávy**|Nastavte na **Ano**, pokud chcete konfigurovat, aby služba Endpoint Protection kontrolovala příchozí e-mailové zprávy, když dorazí do počítačů.<br /><br />Doporučená hodnota: **Ano**|
|**Kontrolovat soubory otevřené ze síťových sdílených složek**|Nastavte na **Ano**, pokud chcete nakonfigurovat, aby služba Endpoint Protection kontrolovala soubory otvírané ze sdílených složek v síti. Obvykle jsou to soubory, ke kterým se přistupuje pomocí cesty Universal Naming Convention (UNC). Povolení této funkce může způsobit problémy uživatelům, kteří mají přístup jenom pro čtení, protože nemůžou malware odebrat.<br /><br />Doporučená hodnota: **Ne**|
|**Kontrolovat namapované síťové jednotky**|Nastavte na **Ano**, pokud chcete nakonfigurovat, aby služba Endpoint Protection kontrolovala soubory na namapovaných síťových jednotkách. Povolení této funkce může způsobit problémy uživatelům, kteří mají přístup jenom pro čtení, protože nemůžou malware odebrat.<br /><br />Doporučená hodnota: **Ne**|
|**Kontrolovat vyměnitelné jednotky**|Nastavte na **Ano**, pokud chcete nakonfigurovat, aby služba Endpoint Protection kontrolovala malware nebo nežádoucí software na vyměnitelných jednotkách, jako jsou jednotky USB flash, když na počítačích spustíte úplnou kontrolu.<br /><br />Doporučená hodnota: **Ano**|
|**Omezit využití procesoru při prověřování**|Nastaví maximální procento využití procesoru, které se smí využít při naplánovaných kontrolách na počítačích. Tuto hodnotu můžete nastavit od 1 do 100 procent.<br /><br />Doporučená hodnota: **50 %**|

### <a name="choose-default-actions-settings"></a>Výběr nastavení výchozích akcí

Nastavení **Zvolte, jak má služba Endpoint Protection postupovat v případě následujících stupňů výstrahy před malwarem** určuje výchozí akci, kterou služba Endpoint Protection provede, když zjistí malware s různými stupni výstrahy. Při každém stupni výstrahy můžete malware odebrat, dát ho do karantény nebo provést akci doporučenou společností Microsoft.

Doporučená hodnota: **Doporučená akce**, což umožňuje službě Endpoint Protection doporučit akci.   

### <a name="decide-whether-to-choose-the-excluded-files-and-folders-settings"></a>Rozhodněte, jestli vybrat nastavení vyloučených souborů a složek

Nastavení **Soubory a složky, které mají být vyloučeny z kontroly a ochrany v reálném čase** vyloučí určité soubory nebo složky, když se na počítačích spustí kontrola nebo když se použije ochrana v reálném čase.

### <a name="decide-whether-to-choose-the-excluded-processes-settings"></a>Rozhodněte, jestli vybrat nastavení vyloučených procesů

Nastavení **Procesy, které se mají vynechat při kontrole a ochraně v reálném čase** umožňuje vyloučit konkrétní procesy, když se na počítačích spustí kontrola nebo když se použije ochrana v reálném čase. Můžete vyloučit jenom soubory s těmito příponami: **.exe**, **.com** nebo **.scr**.

### <a name="decide-whether-to-choose-the-excluded-file-types-settings"></a>Rozhodněte, jestli vybrat nastavení vyloučených typů souborů

Nastavení **Přípony souborů, které se mají vynechat při kontrole a ochraně v reálném čase** umožňuje vyloučit konkrétní přípony názvů souborů, když se na počítačích spustí kontrola nebo když se použije ochrana v reálném čase.

### <a name="specify-microsoft-active-protection-service-settings"></a>Zadejte nastavení služby Microsoft Active Protection Service
Služba Microsoft Active Protection Service je online komunita poskytující pomoc při rozhodování, jak reagovat na případné hrozby. Tato komunita taky pomáhá zastavit šíření nových napadení malwarem. **Ke službě Microsoft Active Protection Service se můžete připojit** tak, že vyberete možnost **Ano** a potom zadáte svou **úroveň členství**:
- **Základní** – odesílá společnosti Microsoft základní informace o zjištěném malwaru. Jsou to například informace o tom, odkud software pochází, jaké používáte akce nebo jaké akce automaticky používá Endpoint Protection a jestli byly tyto akce úspěšné.
- **Rozšířené** – odesílá společnosti Microsoft informace o malwaru, spywaru nebo potenciálně nežádoucím softwaru. Jsou to například informace o umístění softwaru, názvech souborů, jak software funguje a jaký měl na počítač dopad.

Můžete také **přijímat dynamické definice založené na zprávách služby Microsoft Active Protection Service**.

## <a name="choose-management-tasks-for-endpoint-protection"></a>Výběr úloh správy pro službu Endpoint Protection
Následující úlohy umožňují provádět různé úlohy správy na spravovaných počítačích, na kterých běží Endpoint Protection.
- Aktualizovat definice malwaru
  - V konzole Intune: V pracovním prostoru **Skupiny** vyberte počítače, které chcete aktualizovat. Vyberte **vzdálené úlohy** &gt; **aktualizovat definice malwaru**.
  - Spravovaný počítač: Z oznamovací oblasti systému Windows spusťte klientský software Endpoint Protection. Vyberte kartu **Aktualizace** a pak **Aktualizovat**.
- Spusťte kontrolu malwaru:
  - V konzole Intune: V pracovním prostoru **Skupiny** vyberte počítače, které chcete zkontrolovat. Zvolte **Spustit úplné prověřování zaměřené na malware** nebo **Spustit rychlé prověřování zaměřené na malware**.
  - Spravovaný počítač: Z oznamovací oblasti systému Windows spusťte klientský software Endpoint Protection. Vyberte **Rychlé**, **Úplné**nebo **Vlastní** a pak **Zkontrolovat**.

Stav vzdálené úlohy můžete zobrazit výběrem odkazu **Vzdálené úlohy** v pravém dolním rohu konzoly Intune. V dialogovém okně **Stav vzdálené úlohy** najdete seznam aktuálních vzdálených úlohy, stav úloh, název zařízení a všechny hlášené chyby. V případě potřeby také obsahuje odkaz na informace o odstraňování potíží.

## <a name="monitor-endpoint-protection"></a>Sledování služby Endpoint Protection
Stav malwaru na počítačích se sleduje pomocí pracovního prostoru **Ochrana** v [konzole pro správu Microsoft Intune](https://manage.microsoft.com/). Tento pracovní prostor obsahuje dvě stránky:
- **Přehled služby Endpoint Protection** – zobrazuje důležité problémy jako odkazy, které kliknutí výběru zobrazí další informace. Mezi zobrazované problémy patří:
  - **Instance malwaru vyžadující následné akce** – kliknutím na odkaz zobrazíte seznam problémů s malwarem včetně následné akce, kterou je potřeba provést k vyřešení problému. V tomto seznamu můžete zobrazit další podrobnosti a zobrazit tak počítače, které jsou ovlivněné.
  - **Počítače s malwarem vyžadující následnou akci** – kliknutím na odkaz zobrazíte všechny počítače s nevyřešenými problémy s malwarem včetně následné akce, kterou je potřeba provést k vyřešení problému.
  - **Zařízení, které nejsou chráněna** – kliknutím na odkaz zobrazíte počítače, které nejsou chráněné žádným softwarem koncové ochrany, protože žádný takový software není nainstalovaný nebo protože došlo k chybě. Vybráním počítače zobrazíte další podrobnosti.
  - **Zařízení, na kterých je spuštěna jiná aplikace ochrany koncových bodů** – kliknutím na odkaz zobrazíte počítače, na kterých je spuštěná aplikace koncové ochrany třetí strany.
- **Veškerý malware** – zobrazí seznam veškerého aktivního malwaru, který se nachází na vašich počítačích. V tomto seznamu můžete zobrazit další podrobnosti a zobrazit tak všechny počítače, které jsou postižené konkrétním malwarem, nebo můžete vybrat některou z následujících úloh:
  - **Zobrazit vlastnosti** – otevře stránku s dalšími informacemi o vybraném malwaru.
  - **Další informace o tomto malwaru** – otevře téma z Centra společnosti Microsoft pro ochranu před škodlivým softwarem s dalšími informacemi o malwaru.

> [!IMPORTANT]
> Pracovní prostor **Ochrana** se v konzole pro správu nezobrazí, dokud nenainstalujete klienta a nebudete spravovat aspoň na jeden počítač.

  ![Sledování služby Endpoint Protection](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/pol-sa-ep-monitor.png)

### <a name="how-to-view-recent-detection-paths-for-malware-on-computers"></a>Jak zobrazit nedávné cesty zjišťování malwaru na počítačích
Intune může v zařízení zobrazit cesty až 10 naposledy zjištěných instancí malwaru. Možnost **Nedávno kontrolované cesty** je ve výchozím nastavení vypnutá. Postup pro zapnutí tohoto zobrazení:

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) zvolte **Skupiny** > **Všechna zařízení** > **Všechny počítače**.
2. Klikněte pravým tlačítkem na počítač, jehož nedávno kontrolované cesty chcete zobrazit, a vyberte **Vlastnosti**.
3. Na kartách podél horního okraje zvolte **Malware**.

   ![Vyberte kartu Malware a zaškrtněte políčko Nedávno kontrolované cesty.](./media/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune/malware-path-column.png)
4. Klikněte pravým tlačítkem na záhlaví sloupce. Zobrazí se seznam dostupných sloupců. V seznamu zaškrtněte políčko **Nedávno kontrolované cesty**. Zobrazí se sloupec **Nedávno kontrolované cesty** , ve kterém bude uvedeno až 10 posledních instancí malwaru zjištěných na zařízení.

## <a name="run-a-malware-scan-or-update-malware-definitions-on-a-computer"></a>Spuštění kontroly malwaru nebo aktualizace definic malwaru na počítači
Intune může spustit úplnou nebo rychlou kontrolu malwaru pomocí Endpoint Protection nebo Microsoft Defenderu na vzdáleně spravovaném počítači s nainstalovaným klientem Intune.

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) přejděte na **Skupiny** > **Přehled** > **Všechna zařízení** > **Všechny počítače** a vyberte počítač, na který chcete cílit.

2. Klikněte na rozevírací seznam **Vzdálené úlohy** a vyberte úlohu, která se má spustit ve vzdáleném počítači.

## <a name="need-more-help"></a>Potřebujete další pomoc?
Další pomoc a podporu najdete v tématu [Řešení potíží se službou Endpoint Protection v Microsoft Intune](troubleshoot-endpoint-protection-in-microsoft-intune.md).

## <a name="see-also"></a>Viz také
[Zásady ochrany počítačů se systémem Windows](policies-to-protect-windows-pcs-in-microsoft-intune.md)
