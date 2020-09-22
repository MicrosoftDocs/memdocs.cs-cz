---
title: Použití standardních hodnot zabezpečení v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí doporučených nastavení zabezpečení systému Windows můžete chránit uživatele a data v zařízeních s Microsoft Intune pro správu mobilních zařízení. Povolení šifrování, konfigurace rozšířené ochrany před internetovými útoky v programu Microsoft Defender, řízení aplikací Internet Explorer, nastavení místních zásad zabezpečení, vyžadování hesla, blokování stahování na internetu a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom:
- intune-azure
- contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 570d848f624b5558d84177b66751f55c0a0ab4ae
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002728"
---
# <a name="use-security-baselines-to-configure-windows-10-devices-in-intune"></a>Konfigurace zařízení s Windows 10 v Intune pomocí směrných plánů zabezpečení

Pomocí standardních hodnot zabezpečení služby Intune můžete zajistit zabezpečení a ochranu vašich uživatelů a zařízení. Směrné plány zabezpečení jsou předem nakonfigurované skupiny nastavení systému Windows, které vám pomůžou použít známou skupinu nastavení a výchozí hodnoty, které jsou doporučeny pro příslušné týmy zabezpečení. Když v Intune vytvoříte profil standardních hodnot zabezpečení, vytváříte šablonu, která se skládá z několika profilů *Konfigurace zařízení* .

Tato funkce platí pro:

- Windows 10 verze 1809 a novější

Nasadíte standardní hodnoty zabezpečení do skupin uživatelů nebo zařízení v Intune a nastavení se použije na zařízení se systémem Windows 10 nebo novějším. Například *základní hodnota zabezpečení MDM* automaticky povoluje BitLocker pro vyměnitelné jednotky, automaticky vyžaduje heslo k odemknutí zařízení, automaticky zakáže základní ověřování a další. Pokud výchozí hodnota pro vaše prostředí nefunguje, upravte směrný plán tak, aby se projevila potřebná nastavení.

Samostatné typy standardních hodnot můžou zahrnovat stejná nastavení, ale pro tato nastavení použít jiné výchozí hodnoty. Je důležité porozumět výchozím hodnotám ve standardních hodnotách, které se rozhodnete použít, a pak změnit jednotlivé standardní hodnoty tak, aby vyhovovaly potřebám vaší organizace.

> [!NOTE]
> Microsoft nedoporučuje používat verze Preview standardních hodnot zabezpečení v produkčním prostředí. Nastavení v směrném plánu Preview se může v průběhu verze Preview změnit.

Směrné plány zabezpečení vám můžou při práci s Microsoft 365 mít komplexní zabezpečený pracovní postup. Některé výhody tohoto postupu:

- Základní hodnoty zabezpečení obsahují osvědčené postupy a doporučení týkající se nastavení, která mají vliv na zabezpečení. Partneři Intune se stejným týmem zabezpečení systému Windows, který vytváří standardní hodnoty zabezpečení zásad skupiny. Tato doporučení jsou založená na pokynech a rozsáhlém prostředí.
- Pokud s Intune začínáte a nejste si jistí, kde začít, pak vám standardní hodnoty zabezpečení poskytnou výhodu. Můžete rychle vytvořit a nasadit zabezpečený profil s vědomím, že pomáháte chránit prostředky a data vaší organizace.
- Pokud aktuálně používáte zásady skupiny, je migrace na Intune pro správu mnohem jednodušší u těchto směrných plánů. Tyto směrné plány jsou nativně integrované do Intune a zahrnují moderní prostředí pro správu.

Hlavní [směry zabezpečení Windows](/windows/security/threat-protection/windows-security-baselines) jsou skvělým prostředkem pro další informace o této funkci. [Správa mobilních zařízení](/windows/client-management/mdm/) (MDM) je skvělým prostředkem o MDM a o tom, co můžete dělat na zařízeních s Windows.

## <a name="available-security-baselines"></a>Dostupné standardní hodnoty zabezpečení

Následující instance standardních hodnot zabezpečení jsou k dispozici pro použití s Intune. Pomocí odkazů můžete zobrazit nastavení nejaktuálnější instance každého směrného plánu.

- **Základní hodnoty zabezpečení MDM**
  - [Směrný plán zabezpečení MDM za září 2019](security-baseline-settings-mdm-all.md?pivots=mdm-sept-2020)
  - [Základní hodnota zabezpečení MDM pro květen 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Preview: směrný plán zabezpečení MDM pro říjen 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)

- **Základní hodnoty** 
   ATP v programu Microsoft Defender *(K použití tohoto směrného plánu musí vaše prostředí splňovat požadavky na použití [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](advanced-threat-protection.md#prerequisites))*.
  - [Směrné plány ATP v programu Microsoft Defender pro srpna 2020 – verze 5](security-baseline-settings-defender-atp.md?pivots=atp-sept-2020)
  - [Směrné plány ATP v programu Microsoft Defender pro 2020. dubna verze 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Směrné plány ATP v programu Microsoft Defender pro březen 2020 – verze 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > Základní hodnoty zabezpečení služby Microsoft Defender ATP byly optimalizované pro fyzická zařízení a v tuto chvíli se nedoporučují pro použití na virtuálních počítačích (VM) nebo koncových bodech VDI. Určitá nastavení standardních hodnot můžou mít vliv na vzdálené interaktivní relace ve virtualizovaných prostředích.  Další informace najdete v dokumentaci k Windows v tématu [zvýšení dodržování předpisů pro základní hodnoty zabezpečení služby Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) .

- **Základní hodnoty Microsoft Edge**
  - [Směrný plán Microsoft Edge pro duben 2020 (hrana verze 80 a novější)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Preview: směrný plán Microsoft Edge pro říjen 2019 (verze Edge 77 a novější)](security-baseline-settings-edge.md?pivots=edge-october-2019)

Můžete dál používat a upravovat profily, které jste předtím vytvořili na základě šablony verze Preview, a to i v případě, že tato šablona Preview už není dostupná pro vytváření nových profilů.

Až budete připraveni přejít na novější verzi používaného směrného plánu, přečtěte si téma [Změna základní verze profilu](#change-the-baseline-version-for-a-profile) v tomto článku. 

## <a name="about-baseline-versions-and-instances"></a>Základní verze a instance

Každá nová instance verze směrného plánu může přidat nebo odebrat nastavení nebo zavést další změny. Například protože nové nastavení Windows 10 bude k dispozici v nových verzích Windows 10, základní hodnota zabezpečení MDM může obdržet novou instanci verze, která bude obsahovat nejnovější nastavení.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)v části základní hodnoty zabezpečení **Endpoint Security**se  >  **Security baselines** zobrazí seznam dostupných směrných plánů. Seznam obsahuje:
- Název šablony směrného plánu.
- Kolik profilů používá daný typ standardních hodnot.
- Kolik různých instancí typu základní (verze) je k dispozici.
- Datum *posledního publikování* , které určuje, kdy byla k dispozici nejnovější verze šablony standardních hodnot.

Chcete-li zobrazit další informace o základních verzích, které používáte, vyberte typ standardních hodnot, jako je například *směrný plán zabezpečení MDM* , a otevřete jeho podokno *profily* a pak vyberte možnost **verze**. Intune zobrazí podrobnosti o verzích tohoto směrného plánu, které používají vaše profily. Podrobnosti zahrnují nejnovější a aktuální základní verzi. Pro zobrazení podrobných podrobností o profilech, které používají tuto verzi, můžete vybrat jednu verzi.

Můžete zvolit [změnu verze](#change-the-baseline-version-for-a-profile) směrného plánu, který se používá s daným profilem. Když změníte verzi, nemusíte vytvářet nový základní profil, abyste mohli využívat aktualizované verze. Místo toho můžete vybrat profil standardních hodnot a použít vestavěnou možnost ke změně verze instance pro tento profil na nový.

### <a name="compare-baseline-versions"></a>Porovnat základní verze

V podokně **verze** pro směrný plán zabezpečení je seznam každé verze tohoto směrného plánu, který jste nasadili. Tento seznam obsahuje také nejnovější a aktivní verzi směrného plánu. Při vytváření nového *profilu*standardních hodnot zabezpečení profil používá tuto nejnovější verzi směrného plánu zabezpečení.  Můžete pokračovat v používání a úpravách dříve vytvořených profilů, které používají dřívější základní verzi, včetně standardních hodnot vytvořených pomocí verze Preview.

Chcete-li zjistit, co se změnilo mezi verzemi, zaškrtněte políčka pro dvě různé verze a pak vyberte **Porovnat směrné plány**. Pak se zobrazí výzva ke stažení souboru CSV s podrobnostmi o těchto rozdílech.

Stažení identifikuje všechna nastavení ve dvou standardních verzích a poznámky, pokud se toto nastavení změnilo (*notEqual*) nebo má stejné (*stejné*). Podrobnosti zahrnují také výchozí hodnotu nastavení podle verze, a pokud bylo nastavení *přidáno* do novější verze nebo *odebrané* z novější verze.

![Porovnat směrné plány](./media/security-baselines/compare-baselines.png)

## <a name="avoid-conflicts"></a>Vyhnout se konfliktům

V prostředí Intune můžete současně použít jeden nebo více dostupných směrných plánů. Můžete také použít více instancí stejných standardních hodnot zabezpečení, které mají různá přizpůsobení.

Pokud používáte více směrných plánů zabezpečení, Projděte si nastavení v každém z nich, abyste identifikovali, kdy různé základní konfigurace zavádějí do stejného nastavení konfliktní hodnoty. Vzhledem k tomu, že můžete nasadit standardní hodnoty zabezpečení, které jsou navrženy pro různé záměry, a nasadit více instancí stejného směrného plánu, který obsahuje vlastní nastavení, můžete vytvořit konflikty konfigurace pro zařízení, která musí být prověřená a vyřešená.

Standardní hodnoty zabezpečení často spravují stejná nastavení, která můžete nastavit pomocí [profilů konfigurace zařízení](../configuration/device-profiles.md) nebo jiných typů zásad. Proto si zamyslete na dalších zásadách a profilech pro nastavení při hledání, abyste se vyhnuli nebo vyřešili konflikty.

Pomocí informací na následujících odkazech můžete identifikovat a vyřešit konflikty:

- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorování standardních hodnot zabezpečení](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="manage-baselines"></a>Spravovat směrné plány

Mezi běžné úlohy při práci se standardními hodnotami zabezpečení patří:

- [Vytvořit profil](#create-the-profile) – nakonfigurujte nastavení, která chcete použít, a přiřaďte směrný plán skupinám.
- [Změna verze](#change-the-baseline-version-for-a-profile) – změňte základní verzi, kterou používá profil.
- [Odebrání přiřazení standardních hodnot](#remove-a-security-baseline-assignment) – Zjistěte, co se stane, když zastavíte správu nastavení se směrným plánem zabezpečení.


### <a name="prerequisites"></a>Požadavky

- Aby bylo možné spravovat směrné plány v Intune, musí mít váš účet předdefinovanou roli [správce zásad a profilů](../fundamentals/role-based-access-control.md#built-in-roles) .

- Použití některých směrných plánů může vyžadovat, abyste měli aktivní předplatné dalších služeb, jako je ATP Microsoft Defender.

### <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint security**možnost  >  **základní hodnoty zabezpečení** Endpoint Security a zobrazte seznam dostupných směrných plánů.

   ![Vyberte standardní hodnoty zabezpečení, které se mají nakonfigurovat.](./media/security-baselines/available-baselines.png)

3. Vyberte standardní hodnoty, které chcete použít, a pak vyberte **vytvořit profil**.

4. Na kartě **základy** zadejte následující vlastnosti:

   - **Název**: zadejte název profilu standardních hodnot zabezpečení. Zadejte například *standardní profil pro ATP v programu Defender*.

   - **Popis**: Zadejte nějaký text, který popisuje, co tento směrný plán dělá. Popis je, abyste zadali libovolný text, který chcete. Je volitelný, ale doporučený.

   Kliknutím na tlačítko **Další** přejdete na další kartu. Po upřesnění na novou kartu můžete vybrat název karty, který se vrátí na dříve zobrazenou kartu.

5. Na kartě nastavení konfigurace si prohlédněte skupiny **Nastavení** , která jsou k dispozici ve vybraných standardních hodnotách. Skupinu můžete rozbalit a zobrazit tak nastavení v dané skupině a výchozí hodnoty pro tato nastavení ve standardních hodnotách. Chcete-li najít konkrétní nastavení:
   - Vyberte skupinu, kterou chcete rozbalit, a zkontrolujte dostupná nastavení.
   - Použijte panel *hledání* a zadejte klíčová slova, která filtrují zobrazení, aby se zobrazily pouze ty skupiny, které obsahují vaše kritéria hledání.

   Každé nastavení ve směrném plánu má výchozí konfiguraci pro tuto základní verzi. Překonfigurujte výchozí nastavení tak, aby vyhovovalo vašim obchodním potřebám. Různé směrné plány můžou obsahovat stejné nastavení a pro nastavení použít jiné výchozí hodnoty, v závislosti na záměru směrného plánu.

   ![Rozbalením skupiny zobrazíte nastavení pro tuto skupinu.](./media/security-baselines/sample-list-of-settings.png)

6. Na kartě **značky oboru** vyberte **Vybrat značky oboru** a otevřete tak podokno *Vybrat značky* , abyste přiřadili značky oboru k profilu.

7. Na kartě **přiřazení** vyberte **Vybrat skupiny, které se mají zahrnout** , a pak přiřaďte směrný plán k jedné nebo více skupinám. K vyřazení tohoto přiřazení použijte **možnost vybrat skupiny, které chcete vyloučit** .

   ![Přiřazení profilu](./media/security-baselines/assignments.png)

8. Až budete připraveni k nasazení standardních hodnot, přejděte na kartu **Revize + vytvořit** a Prohlédněte si podrobnosti pro směrný plán. Výběrem **vytvořit** uložte a nasaďte profil.

   Jakmile profil vytvoříte, bude přesunut do přiřazené skupiny a může se okamžitě uplatnit.

   > [!TIP]
   > Pokud uložíte profil, aniž byste ho nejdřív přiřadíte do skupin, můžete ho později upravit.

   ![Kontrola standardních hodnot](./media/security-baselines/review.png)

9. Po vytvoření profilu ho upravte tak, že kliknete na **Endpoint security**  >  možnost**základní hodnoty zabezpečení**Endpoint Security, vyberte typ standardních hodnot, který jste nakonfigurovali, a pak vyberte **profily**. V seznamu dostupných profilů vyberte profil a pak vyberte **vlastnosti**. Můžete upravit nastavení ze všech dostupných karet konfigurace a kliknutím na tlačítko **zkontrolovat + Uložit** změny potvrďte.

### <a name="change-the-baseline-version-for-a-profile"></a>Změna základní verze profilu

Můžete změnit verzi základní instance, která se používá s profilem.  Když změníte verzi, vyberete dostupnou instanci stejného směrného plánu. Nemůžete měnit mezi dvěma různými typy standardních hodnot, jako je například změna profilu z použití směrného plánu pro ATP v programu Defender na používání standardních hodnot zabezpečení MDM.

Když nakonfigurujete změnu základní verze, můžete si stáhnout soubor CSV, který obsahuje seznam změn mezi dvěma zahrnutými základními verzemi. Můžete také zvolit, že chcete zachovat všechna vlastní nastavení z původní základní verze, nebo implementovat novou verzi pomocí všech výchozích hodnot. Při změně verze směrného plánu pro profil nemáte možnost provádět změny v individuálním nastavení.

Po uložení se po dokončení převodu směrný plán okamžitě znovu nasadí na přiřazené skupiny.

**Během převodu**:

- Nová nastavení, která neexistovala v původní verzi, kterou jste použili, se přidají a nastaví tak, aby používala výchozí hodnoty.

- Nastavení, která nejsou ve vybrané verzi nového směrného plánu, se odeberou a už se tímto profilem standardních hodnot zabezpečení neuplatní.

  Pokud se nastavení už nespravuje pomocí směrného plánu, toto nastavení se na zařízení neresetuje. Místo toho zůstane nastavení v zařízení nastavené na poslední konfiguraci, dokud jiný proces nespravuje nastavení, aby ho změnil. Příklady procesů, které mohou změnit nastavení po zastavení správy, zahrnují jiný základní profil, nastavení zásad skupiny nebo ruční konfiguraci provedenou na zařízení.

#### <a name="to-change-the-baseline-version-for-a-profile"></a>Změna základní verze profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 

2. Vyberte **Endpoint security**možnost  >  **základní hodnoty zabezpečení**Endpoint Security a potom vyberte dlaždici pro typ základního typu, který má profil, který chcete změnit.

3. V dalším kroku vyberte **profily**a potom zaškrtněte políčko u profilu, který chcete upravit, a pak vyberte **změnit verzi**.

   ![výběr standardních hodnot](./media/security-baselines/select-baseline.png)

4. V podokně **změnit verzi** použijte **možnost vybrat standardní hodnotu zabezpečení pro aktualizaci na** rozevírací seznam a vyberte instanci verze, kterou chcete použít.

   ![vybrat verzi](./media/security-baselines/select-instance.png)

5. Pokud chcete stáhnout soubor CSV, který zobrazuje rozdíl mezi verzí aktuální instance a novou verzí, kterou jste vybrali, vyberte **zkontrolovat aktualizaci** . Zkontrolujte tento soubor, abyste pochopili, která nastavení jsou nová nebo odebraná, a jaké jsou výchozí hodnoty těchto nastavení v aktualizovaném profilu.

   Až budete připraveni, pokračujte k dalšímu kroku.

6. Zvolte jednu ze dvou možností pro **možnost vybrat metodu pro aktualizaci profilu**:
   - **Přijmout změny směrného plánu, ale zachovat existující přizpůsobení nastavení** – Tato možnost zachovává vlastní nastavení, které jste provedli v profilu standardních hodnot, a aplikuje je na novou verzi, kterou jste vybrali k použití.
   - **Přijmout změny směrného plánu a zahodit existující přizpůsobení nastavení** – Tato možnost přepíše původní profil úplně. Aktualizovaný profil bude používat výchozí hodnoty pro všechna nastavení.

7. Vyberte **Odeslat**. Profil se aktualizuje na vybranou základní verzi a po dokončení převodu se směrný plán hned znovu nasadí do přiřazených skupin.

### <a name="remove-a-security-baseline-assignment"></a>Odebrání přiřazení standardních hodnot zabezpečení

Pokud se nastavení standardních hodnot zabezpečení už netýká zařízení, nebo se nastavení ve standardních hodnotách nastaví na *není nakonfigurované*, nastavení se v zařízení nevrátí do předem spravované konfigurace. Místo toho předchozí spravovaná nastavení v zařízení ponechá poslední konfigurace přijatá od standardních hodnot, dokud některý jiný proces tyto nastavení v zařízení neaktualizuje.

Jiné procesy, které můžou později měnit nastavení zařízení, zahrnují různé nebo nové základní hodnoty zabezpečení, konfigurační profil zařízení, konfigurace Zásady skupiny nebo ruční úpravu nastavení na zařízení.

### <a name="duplicate-a-security-baseline"></a>Duplikovat směrný plán zabezpečení

Můžete vytvořit duplicity svých standardních hodnot zabezpečení. Scénář při duplikaci standardních hodnot je užitečný, pokud chcete přiřadit podobný, ale odlišný směrný plán k podmnožině zařízení. Vytvořením duplicitních dat nebudete muset ručně znovu vytvořit celý směrný plán. Místo toho můžete duplikovat všechny aktuální směrné plány a potom zavádět pouze změny, které nová instance vyžaduje. Můžete změnit pouze konkrétní nastavení a skupinu, ke které je směrný plán přiřazen.

Při vytváření duplicitního názvu přiřadíte kopii nový název. Kopie se vytvoří se stejnou konfigurací nastavení a značkami oboru jako původní, ale nebude mít žádné přiřazení. Chcete-li přidat přiřazení, bude nutné upravit nový směrný plán.

Všechny standardní hodnoty zabezpečení podporují vytváření duplicitních hodnot.

Po duplikaci směrného plánu zkontrolujte a upravte novou instanci, aby se změnila její konfigurace.

#### <a name="to-duplicate-a-baseline"></a>Duplikace standardních hodnot

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V části **Endpoint security**  >  **základní hodnoty zabezpečení**Endpoint Security vyberte typ směrného plánu, který chcete duplikovat, a pak vyberte **profily**.
3. Klikněte pravým tlačítkem na profil, který chcete duplikovat, a vyberte **Duplikovat**, nebo vyberte tři tečky (**...**) napravo od směrného plánu a vyberte **Duplikovat**.
4. Zadejte **nový název** pro směrný plán a potom vyberte **Uložit**.

Po *aktualizaci*se nový základní profil zobrazí v centru pro správu.

#### <a name="to-edit-a-baseline"></a>Úprava směrného plánu

1. Vyberte standardní hodnoty a pak vyberte **vlastnosti**.
2. Vyberte **Nastavení** a rozbalte seznam kategorií nastavení ve standardních hodnotách. Nastavení z tohoto zobrazení nemůžete změnit, ale můžete zkontrolovat, jak jsou nakonfigurované.
3. Chcete-li upravit nastavení, vyberte možnost **Upravit** pro každou kategorii, u které chcete provést změnu:
   - Základy
   - Přiřazení
   - Značky oboru
   - Nastavení konfigurace
4. Až změny provedete, vyberte **Uložit** a uložte provedené úpravy.  Než začnete s úpravou dalších kategorií, je nutné změny v jedné kategorii Uložit.

### <a name="older-baseline-versions"></a>Starší základní verze

Microsoft Endpoint Manager aktualizuje verze předdefinovaných standardních hodnot zabezpečení v závislosti na měnícím se potřebách typické organizace. Každá nová verze má za následek aktualizaci verze na konkrétní směrný plán. Očekává se, že zákazníci budou používat nejnovější základní verzi jako výchozí bod pro své konfigurační profily zařízení.

Pokud už neexistují žádné profily, které používají starší standardní hodnoty uvedené ve vašem tenantovi, Microsoft Endpoint Manager zobrazí jenom nejnovější dostupnou verzi základní verze.

Pokud máte profil přidružený ke staršímu směrnému plánu, bude tento starší směrný plán dál uveden.

## <a name="co-managed-devices"></a>Společně spravovaná zařízení

Standardní hodnoty zabezpečení na zařízeních spravovaných přes Intune se podobají spoluspravovaným zařízením s Configuration Manager. Společně spravovaná zařízení používají Configuration Manager a Microsoft Intune ke správě zařízení s Windows 10 současně. Umožňuje cloudu připojit stávající Configuration Manager investic k výhodám služby Intune. [Přehled spolusprávy](/configmgr/comanage/overview) je skvělý prostředek, pokud používáte Configuration Manager a chcete mít i výhody cloudu.

Pokud používáte spoluspravovaná zařízení, musíte přepnout zatížení **Konfigurace zařízení** (jeho nastavení) do Intune. Další informace najdete v [úlohách konfigurace zařízení](/configmgr/comanage/workloads#device-configuration) .

## <a name="q--a"></a>Otázky a odpovědi

### <a name="why-these-settings"></a>Proč tato nastavení?

Tým Microsoftu pro zabezpečení má za několik let práce přímo s vývojáři systému Windows a komunitou zabezpečení k vytváření těchto doporučení. Nastavení v těchto standardních hodnotách se považují za relevantní možnosti konfigurace související se zabezpečením. V každém novém sestavení systému Windows tým upraví doporučení na základě nově vydaných funkcí.

### <a name="is-there-a-difference-in-the-recommendations-for-windows-security-baselines-for-group-policy-vs-intune"></a>Existuje rozdíl v doporučeních pro základní hodnoty zabezpečení Windows pro zásady skupiny vs. Intune?

Stejný tým zabezpečení Microsoftu zvolil a organizoval nastavení pro jednotlivé standardní hodnoty. Intune zahrnuje všechna relevantní nastavení v základní úrovni zabezpečení Intune. Existují některá nastavení v standardních hodnotách zásad skupiny, která jsou specifická pro místní řadič domény. Tato nastavení jsou vyloučená z doporučení služby Intune. Všechna ostatní nastavení jsou stejná.

### <a name="are-the-intune-security-baselines-cis-or-nsit-compliant"></a>Jsou služby Intune Security standarded nebo institutu NSIT kompatibilní?

Striktně řečeno, ne. Tým Microsoft Security konzultuje organizace, jako je například SNS, ke kompilaci doporučení. Nejedná se ale o mapování 1:1 mezi "kompatibilní s službami CIS" a směrnými plány společnosti Microsoft.

### <a name="what-certifications-does-microsofts-security-baselines-have"></a>Jaké certifikace má standardní hodnoty zabezpečení od Microsoftu? 

- Společnost Microsoft nadále zveřejňuje standardní hodnoty zabezpečení pro zásady skupiny (GPO) a [sadu nástrojů dodržování předpisů zabezpečení](/windows/security/threat-protection/security-compliance-toolkit-10), protože to trvá mnoho let. Tyto směrné plány používá mnoho organizací. Doporučení v těchto směrných plánech vycházejí ze závazku týmu zabezpečení společnosti Microsoft s podnikovými zákazníky a externími úřady, včetně ministerstva obrany, National Institute of Standards and Technology (NIST) a dalších. Naše doporučení a směrné plány sdílíme s těmito organizacemi. Tyto organizace mají také svá vlastní doporučení, která pečlivě zrcadlí doporučení Microsoftu. Protože správa mobilních zařízení (MDM) se stále rozrůstá do cloudu, společnost Microsoft vytvořila ekvivalentní doporučení MDM těchto směrných plánů zásad skupiny. Tyto další směrné plány jsou integrované pro Microsoft Intune a zahrnují zprávy o dodržování předpisů pro uživatele, skupiny a zařízení, která následují (nebo nesleduje) na základě směrného plánu.

- Spousta zákazníků používá jako výchozí bod doporučení základní úrovně Intune a pak je přizpůsobuje tak, aby splňovala požadavky na IT a zabezpečení. **Směrný plán zabezpečení MDM** pro Windows 10 RS5 je první základ pro vydání. Tato standardní hodnota je sestavená jako obecná infrastruktura, která zákazníkům umožňuje nakonec importovat další standardní hodnoty zabezpečení založené na CIS, NIST a dalších standardech. V současné době je k dispozici pro Windows a nakonec bude zahrnovat iOS/iPadOS a Android.

- Migrace z místních zásad skupiny služby Active Directory do čistě cloudového řešení pomocí Azure Active Directory (AD) s Microsoft Intune je cesta. V sadě [nástrojů pro zabezpečení dodržování předpisů](/windows/security/threat-protection/security-compliance-toolkit-10) , které vám pomůžou při správě hybridních AD a zařízení připojených k Azure AD, je potřeba, aby byly k dispozici šablony zásad skupiny. Tato zařízení můžou podle potřeby získat nastavení MDM z cloudu (Intune) a nastavení zásad skupiny z místních řadičů domény.

## <a name="next-steps"></a>Další kroky

- Zobrazit nastavení v nejnovějších verzích dostupných standardních hodnot:
  - [Základní hodnoty zabezpečení MDM](security-baseline-settings-mdm-all.md)
  - [Základní hodnoty ATP v programu Microsoft Defender](security-baseline-settings-defender-atp.md)

- Zkontroluje stav a monitoruje [základní a profil](security-baselines-monitor.md) .