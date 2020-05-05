---
title: Plánování automatizace úloh
titleSuffix: Configuration Manager
description: Před vytvořením pořadí úloh pro automatizaci úloh pomocí Configuration Manager proveďte plánování.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723562"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Plánování automatizace úloh v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvořit pořadí úloh pro automatizaci úloh v prostředí Configuration Manager. Tyto úlohy jsou v rozsahu od zachycení operačního systému v referenčním počítači za účelem nasazení operačního systému do jednoho nebo více cílových počítačů. Akce vykonávané pořadím úloh definují jednotlivé kroky pořadí úloh. Po spuštění pořadí úkolů se spustí akce každého kroku na úrovni příkazového řádku v kontextu místního systému. Toto chování znamená, že pořadí úkolů běží plně automatizovaně bez zásahu uživatele.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a>Kroky a akce pořadí úkolů  

Kroky jsou základními součástmi pořadí úkolů. Můžou zahrnovat příkazy, jako je:

- Konfigurace a zachycení operačního systému referenčního počítače
- Instalace systému Windows, hardwarových ovladačů, Configuration Manager klienta a softwaru do cílového počítače

Akce kroku definují příkazy kroku pořadí úkolů. Existují dva typy akcí:  

- Akce, kterou definujete pomocí řetězce příkazového řádku, se nazývá *vlastní akce* .  
- Akce, která je předdefinovaná Configuration Manager, se označuje jako *Vestavěná akce*.  

Pořadí úkolů může dělat libovolnou kombinaci vlastních a vestavěných akcí.  

Kroky pořadí úkolů mohou obsahovat také podmínky, které určují, jak se krok chová. Toto chování zahrnuje zastavení pořadí úloh nebo pokračování v pořadí úkolů, pokud dojde k chybě. Jedním z typů podmínek je proměnná pořadí úloh. Například použijte proměnnou **SMSTSLastActionRetCode** k otestování podmínky předchozího kroku. Přidejte podmínky do jednoho kroku nebo do skupiny kroků.  

Pořadí úkolů zpracovává kroky postupně. Tato sekvence zahrnuje akci kroku a jakékoli podmínky v kroku. Když Configuration Manager začne zpracovávat krok pořadí úkolů, nespustí další krok, dokud nebude dokončena předchozí akce.

Pořadí úkolů je považováno za dokončené, když:

- Všechny jeho kroky jsou dokončené.  
- Neúspěšný krok způsobí, že Configuration Manager zastavit spuštění pořadí úkolů před dokončením všech kroků.  

Pokud například krok pořadí úloh nenalezne na distribučním bodu odkaz na bitovou kopii nebo balíček, obsahuje pořadí úloh poškozený odkaz. Configuration Manager zastaví pořadí úkolů v tomto okamžiku, pokud neúspěšný krok nemá podmínku pokračovat, když dojde k chybě.  

> [!IMPORTANT]  
> Není-li zadána jiná podmínka, pořadí úloh po selhání kroku nebo akci selže. Pokud chcete, aby pořadí úkolů pokračovalo i v případě neúspěchu kroku, upravte pořadí úloh, přepněte na kartu **Možnosti** a vyberte **pokračovat při chybě**.  

Další informace o krocích, které je možné přidat do pořadí úkolů, najdete v tématu [kroky pořadí úkolů](../understand/task-sequence-steps.md).  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a>Skupiny pořadí úkolů  

V rámci pořadí úkolů můžete seskupit více kroků. Skupina pořadí úkolů se skládá z názvu, volitelného popisu a všech volitelných podmínek. Pořadí úkolů vyhodnotí podmínky skupiny jako jednotku před tím, než pokračuje v dalším kroku. Vnoření skupin mezi sebou nebo zahrnutí různých kroků a podskupin. Skupiny jsou užitečné, pokud kombinujete několik kroků, které sdílejí stejnou podmínku.  

Přiřaďte název skupinám pořadí úloh. Nemusí být jedinečný. Ke skupině pořadí úloh můžete volitelně zadat také popis.  

> [!IMPORTANT]  
> Není-li zadána jiná podmínka, skupina pořadí úloh po selhání kroku nebo začleněné skupiny v rámci dané skupiny selže. Pokud chcete, aby pořadí úkolů pokračovalo i v případě, že dojde k chybě kroku nebo vložené skupiny, nastavte v kroku nebo skupině možnost **pokračovat při chybě** .  

Následující tabulka ukazuje, jak při seskupování kroků funguje možnost **pokračovat při chybě** .  

V tomto příkladu jsou k dispozici dvě skupiny pořadí úkolů, které obsahují tři kroky pořadí úkolů.  

|Skupina nebo krok pořadí úloh|Nastavení Pokračovat při chybě|  
|---------------------------------|-------------------------------|  
|**Skupina pořadí úloh 1**|**Pokračovat při chybě** vybráno.|  
|Krok 1 pořadí úkolů|**Pokračovat při chybě** vybráno.|  
|2. krok pořadí úkolů|Nenastaveno|  
|3. krok pořadí úkolů|Nenastaveno|  
|**Skupina pořadí úloh 2**|Nenastaveno|  
|4. krok pořadí úkolů|Nenastaveno|  
|5. krok pořadí úkolů|Nenastaveno|  
|Krok 6 pořadí úkolů|Nenastaveno|  

- Pokud pořadí úkolů krok 1 neproběhne úspěšně, pořadí úkolů pokračuje v kroku 2 pořadí úkolů.  

- Pokud pořadí úkolů krok 2 selhává, pořadí úkolů nespustí pořadí úkolů krok 3. Vzhledem k tomu, že je skupina pořadí úloh 1 nakonfigurovaná tak, aby **při chybě pokračovala**, pořadí úkolů pokračuje ve skupině pořadí úloh 2. Spustí pořadí úkolů další krok 4.  

- Pokud se 4. krok pořadí úkolů nezdařil, nejsou spuštěny žádné další kroky. Pořadí úkolů se nepovede, protože nastavení **pokračovat při chybě** není nakonfigurované pro skupinu pořadí úloh 2.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Přidání podřízených sekvencí úloh do pořadí úkolů

<!--1261338-->

Přidejte nový krok pořadí úloh, který spustí jiné pořadí úkolů. Tento krok vytvoří vztah nadřazený-podřízený mezi pořadím úkolů. Pomocí tohoto kroku můžete vytvořit více modulárních pořadí úkolů, které můžete znovu použít.  

Další informace najdete v tématu [spuštění pořadí úkolů](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a>Proměnné pořadí úkolů  

Proměnné pořadí úkolů jsou množinou párů název-hodnota. Poskytují konfiguraci a nastavení nasazení operačního systému pro úlohy pro počítač, operační systém a konfiguraci stavu uživatele u klienta Configuration Manager. Proměnné pořadí úloh poskytují mechanismus konfigurace a vlastního nastavení kroků v pořadí úloh.  

Když spustíte pořadí úloh, uloží se spousta nastavení pořadí úkolů jako proměnné prostředí. Můžete přistupovat k hodnotám vestavěných proměnných pořadí úloh nebo je změnit. Můžete také vytvořit nové proměnné pořadí úkolů a přizpůsobit tak způsob, jakým je pořadí úkolů spuštěno v cílovém počítači.  

Pomocí proměnných pořadí úkolů můžete provádět následující akce:  

- Konfigurace nastavení pro akci pořadí úkolů  

- Zadání argumentů příkazového řádku pro krok pořadí úkolů  

- Vyhodnocení podmínky, která určuje, zda je krok pořadí úloh nebo skupina spuštěna  

- Zadejte hodnoty pro vlastní skripty používané v pořadí úkolů.  

Například máte pořadí úkolů, které zahrnuje krok pořadí úkolů **připojit k doméně nebo pracovní skupině** . Nasaďte pořadí úkolů do různých kolekcí, kde je členství v kolekci určeno členstvím v doméně. Pro název domény každé kolekce zadejte proměnnou pořadí úkolů pro kolekci. Pak tuto proměnnou pořadí úkolů použijte k zadání příslušného názvu domény do pořadí úkolů.  

Další informace najdete v tématu [Použití proměnných pořadí úkolů](../understand/using-task-sequence-variables.md).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a>Vytvoření pořadí úkolů  

Pořadí úloh lze vytvořit pomocí průvodce vytvořením pořadí úloh. Průvodce může vytvořit Vestavěná pořadí úloh, která dělají konkrétní úkoly nebo vlastní pořadí úkolů, které může provádět mnoho různých úloh. Průvodce vám umožní vytvořit následující typy pořadí úloh:

- Instalace existující image operačního systému do cílového počítače  

- Sestavení a zachycení bitové kopie operačního systému v referenčním počítači  

- Upgrade na Windows 10 z balíčku pro upgrade operačního systému na cílovém počítači

- Vytvoření vlastního pořadí úloh, které provádí přizpůsobený úkol nebo specializované nasazení operačního systému  

Další informace najdete v tématu [Vytvoření pořadí úkolů](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a>Úprava pořadí úloh  

Upravte pořadí úloh pomocí **editoru pořadí úloh**. Editor může v pořadí úkolů provádět následující změny:  

- Přidat nebo odebrat kroky z pořadí úloh  

- Změna pořadí kroků pořadí úloh  

- Přidat nebo odebrat skupiny kroků  

- Určete, jestli pořadí úkolů pokračuje v situaci, kdy dojde k chybě.  

- Přidání podmínek do kroků a skupin pořadí úkolů  

> [!IMPORTANT]  
> Pokud pořadí úkolů obsahuje v důsledku úpravy nějaké nepřidružené odkazy na objekt, Editor vyžaduje, abyste před zavřením odstranili odkaz. Mezi možné akce patří:  
>
> - Opravte odkaz.
> - Odstraní neodkazovaný objekt z pořadí úloh.  
> - Dočasně zakažte krok neúspěšného pořadí úkolů, dokud nebude poškozený odkaz opraven nebo odebrán.  

Další informace o úpravách pořadí úkolů najdete v tématu [použití editoru pořadí úloh](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a>Nasazení pořadí úloh  

Nasaďte pořadí úkolů do cílových počítačů, které jsou v libovolné kolekci Configuration Manager. K nasazení operačních systémů do neznámých počítačů použijte vestavěnou kolekci **všechny neznámé počítače** . Pořadí úkolů nemůžete nasadit do kolekcí uživatelů.  

> [!IMPORTANT]  
> Nesaďte pořadí úloh, která instalují operační systémy, do nevhodných kolekcí. Ujistěte se, že kolekce, do které nasazujete pořadí úloh, obsahuje pouze počítače, do nichž chcete operační systém nainstalovat. Chcete-li zabránit nechtěnému nasazení operačního systému, nakonfigurujte nastavení pro vysoce rizikové nasazení. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Každý cílový počítač, který přijímá pořadí úkolů, spustí pořadí úkolů podle nastavení určeného v nasazení. Samotná pořadí úloh neobsahují přidružené soubory nebo programy. Všechny soubory, které odkazují na pořadí úkolů, již musí být v cílovém počítači nebo uloženy v distribučním bodě, ke kterému mají klienti přístup.

> [!NOTE]  
> Pořadí úkolů nainstaluje balíčky, na které odkazují programy, i v případě, že je už v cílovém počítači nainstalovaný program nebo balíček.
>
> Pokud pořadí úkolů nainstaluje aplikaci, aplikace se nainstaluje pouze v případě, že jsou splněna pravidla požadavků pro danou aplikaci a aplikace ještě není nainstalovaná, a to na základě metody detekce zadané pro aplikaci.  

Klient Configuration Manager spouští nasazení pořadí úloh při stahování zásad klienta. Pokud chcete tuto akci aktivovat místo čekání na další cyklus cyklického dotazování, přečtěte si téma [spuštění načtení zásad pro klienta Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

Když nasadíte pořadí úloh do zařízení se systémem Windows Embedded, která jsou povolená pomocí filtru zápisu, můžete určit, jestli se má v zařízení během nasazení zakázat filtr zápisu, a po nasazení restartovat zařízení. Pokud není filtr zápisu zakázán, pořadí úkolů je nasazeno do dočasného překrytí a po restartu zařízení nebude k dispozici.  

> [!NOTE]  
> Když nasadíte pořadí úloh do zařízení se systémem Windows Embedded, ujistěte se, že je zařízení členem kolekce, která má nakonfigurované časové období údržby. To vám umožní spravovat, kdy je filtr zápisu zakázán a povolen a kdy se zařízení restartuje.  
>
> Pokud klienti stahují pořadí úloh mimo časové období údržby, pořadí úkolů se stáhne dvakrát. V tomto scénáři klient stáhne pořadí úloh, zakáže filtr zápisu, restartuje počítač a znovu stáhne pořadí úloh. Důvodem je to, že se pořadí úkolů původně stáhlo do dočasného překrytí, které se po restartu zařízení vymaže.  

Další informace o nasazení pořadí úkolů najdete v tématu [nasazení pořadí úkolů](../deploy-use/deploy-a-task-sequence.md).  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a>Export a import

Configuration Manager umožňuje exportovat a importovat pořadí úloh. Pokud exportujete pořadí úloh, můžete do něj začlenit objekty, na něž pořadí úloh odkazuje.

Další informace najdete v tématu [Export a import pořadí úkolů](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a>Spuštění pořadí úkolů  

Pořadí úkolů se vždy spouští pomocí účtu místního systému. Když je spuštěno pořadí úloh, klient Configuration Manager nejprve zkontroluje všechny odkazované balíčky, než spustí kroky pořadí úloh. Pokud nemůže ověřit nebo stáhnout odkazovaný balíček, pořadí úkolů vrátí chybu pro přidružený krok pořadí úkolů.  

> [!Note]  
> Krok pořadí úkolů **Spustit příkazový řádek** poskytuje možnost spustit příkaz jako jiný účet.  

Pokud nakonfigurujete nasazení pořadí úkolů, které se stáhne a spustí, klient Configuration Manager stáhne veškerý závislý obsah do mezipaměti. Pokud je velikost mezipaměti klienta příliš malá nebo nelze najít obsah, pořadí úloh se nezdařilo. Klient vygeneruje stavovou zprávu.

Můžete také určit, že klient stáhne obsah pouze v případě, že je požadován. Tuto akci provedete tak, že v případě potřeby v nasazení pořadí úkolů vyberete možnost **Stáhnout obsah místně** . Další možností je **Spustit program z distribučního bodu**. Pomocí této možnosti klient nainstaluje soubory přímo z distribučního bodu, aniž by je nejdřív stáhl do mezipaměti.

Když nakonfigurujete nasazení pořadí úloh jako **dostupné**, pokud klient nemůže najít závislý obsah pro pořadí úkolů, okamžitě pošle chybu. V případě **požadovaného** nasazení klient Configuration Manager čeká v této situaci. Pokusí se o stažení obsahu až do konečného termínu, pro případ, že se obsah ještě nereplikoval do umístění obsahu, ke kterému má klient přístup.  

Když se pořadí úkolů úspěšně dokončí nebo dojde k chybě, Configuration Manager tento stav zaznamená do historie klienta.

Jakmile se pořadí úkolů spustí v počítači, nemůžete ho zrušit ani zastavit.  

> [!IMPORTANT]  
> Pokud krok pořadí úkolů vyžaduje restartování počítače, musí být klient schopný spustit systém do formátovaného diskového oddílu. V opačném případě se pořadí úkolů nezdařilo bez ohledu na zpracování chyb, které zadáte v pořadí úkolů.  

Pokud je závislý objekt pořadí úloh aktualizován na novější verzi, jakékoliv pořadí úkolů, které se na tento balíček odkazuje, se automaticky aktualizuje. Odkazuje na nejnovější verzi bez ohledu na to, kolik aktualizací jste nasadili.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a>Použití časových období údržby

Můžete určit, kdy se může pořadí úkolů Spustit, definováním časového období údržby pro kolekci zařízení. Časové intervaly pro správu a údržbu konfigurujete pomocí počátečního data, času zahájení a dokončení a způsobu opakování. Když nastavíte plán pro časové období údržby, můžete určit, že okno údržby platí pouze pro pořadí úkolů. Další informace najdete v tématu [použití časových období údržby](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
> Když nakonfigurujete spuštění pořadí úkolů v časovém intervalu pro správu a údržbu, jakmile se pořadí úkolů spustí, pokračuje v činnosti i v případě, že se okno údržby uzavře.  

Pokud má zařízení více než jedno časové období údržby, může klient ignorovat okno údržby **všechna nasazení** . Od verze 1810 použijte následující nastavení klienta k řízení tohoto chování: **Povolit instalaci aktualizací softwaru v okně údržby "všechna nasazení", když je k dispozici okno Údržba aktualizace softwaru**. Další informace najdete v tématu [o nastavení klienta](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint) .<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a>Pořadí úloh a účet přístupu k síti  

> [!Important]  
> Některé scénáře nasazení operačního systému nevyžadují použití účtu přístupu k síti. Další informace najdete v tématu [Rozšířená http](#enhanced-http).

I když se pořadí úkolů spouští jenom v kontextu účtu místního systému, může být potřeba nakonfigurovat [účet přístupu k síti](../../core/plan-design/hierarchy/accounts.md#network-access-account) v následujících případech:  

- Pokud se pořadí úkolů pokusí o přístup k Configuration Manager obsahu v distribučních bodech. Správně nakonfigurujte účet přístupu k síti, jinak se pořadí úkolů nezdaří.

- Když použijete spouštěcí image k zahájení nasazení operačního systému. V takovém případě Configuration Manager používá prostředí Windows PE, což není úplný operační systém. Prostředí Windows PE používá automaticky generovaný náhodný název, který není členem žádné domény. Pokud účet pro přístup k síti nenakonfigurujete správně, nemůže počítač získat přístup k požadovanému obsahu pro pořadí úkolů.  

> [!NOTE]  
> Účet přístupu k síti se nikdy nepoužívá jako kontext zabezpečení pro spouštění programů, instalaci aplikací, instalaci aktualizací nebo spouštění pořadí úloh. Účet přístupu k síti se používá jenom pro přístup k přidruženým prostředkům v síti.  

Další informace o účtu přístupu k síti najdete v tématu [účet pro přístup k síti](../../core/plan-design/hierarchy/accounts.md#network-access-account).  

### <a name="enhanced-http"></a>Vylepšený protokol HTTP
<!--1358278-->

Pokud povolíte **Rozšířené protokol HTTP**, následující scénáře nevyžadují účet pro přístup k síti ke stažení obsahu z distribučního bodu:

- Pořadí úloh spuštěná ze spouštěcího média nebo technologie PXE  
- Pořadí úkolů spuštěné z centra softwaru  

Tato pořadí úloh mohou být pro nasazení operačního systému nebo vlastní. Podporuje se taky pro počítače pracovní skupiny.

Další informace najdete v tématu [Rozšířená http](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> Následující scénáře nasazení operačního systému stále vyžadují použití účtu přístupu k síti:
>  
> - [Možnost nasazení](../deploy-use/deploy-a-task-sequence.md)pořadí úloh, **přístup k obsahu přímo z distribučního bodu, pokud to vyžaduje běžící pořadí úloh**
> - Možnost kroku [úložiště stavu požadavku](../understand/task-sequence-steps.md#BKMK_RequestStateStore) , **Pokud se účet počítače nedokáže připojit k úložišti stavů, použijte účet přístupu k síti** .
> - Při připojování k nedůvěryhodné doméně nebo napříč doménovými strukturami služby Active Directory
> - Možnost kroku [použít bitovou kopii operačního systému](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) , **přístup k obsahu přímo z distribučního bodu**
> - [Rozšířené nastavení](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) pořadí úkolů pro **první spuštění jiného programu**
> - [Odesílání](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a>Vytvoření média

Pořadí úloh a jejich související soubory a závislosti můžete zapsat na několik typů médií. Configuration Manager podporuje vyměnitelná média, jako je například DVD nebo USB flash disk pro zachycení, samostatné a spouštěcí média. Předzpracované médium používá soubor bitové kopie systému Windows (WIM).  

Když vytváříte médium, zadejte heslo pro řízení přístupu. Uživatel pak musí zadat heslo v cílovém počítači, aby bylo možné pořadí úkolů Spustit.  

Když spouštíte pořadí úkolů z média, zadaná architektura procesoru média není rozpoznána. Pokud zadaná architektura neodpovídá cílovému počítači, pořadí úkolů se stále pokusí spustit. Pokud se architektura média neshoduje s architekturou cílového počítače, pořadí úkolů se nezdařilo.  

Další informace najdete v tématu [Vytvoření média pořadí úkolů](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Typy médií

Configuration Manager podporuje následující typy médií:  

#### <a name="capture-media"></a>Záznamová média

Toto médium zachytí bitovou kopii operačního systému, kterou nakonfigurujete a vytvoříte mimo Configuration Manager infrastrukturu. Záznamová média mohou obsahovat vlastní programy, které se mohou spouštět před spuštěním pořadí úkolů. Vlastní program může spolupracovat s plochou, vyzvat uživatele k zadáním vstupních hodnot nebo vytvořit proměnné používané pořadím úkolů.  

Další informace najdete v tématu [Vytvoření záznamového média](../deploy-use/create-capture-media.md).  

#### <a name="stand-alone-media"></a>Samostatné médium

Samostatná média obsahují pořadí úkolů a všechny související objekty, které jsou potřebné ro spuštění pořadí úkolů. Pořadí úkolů samostatného média lze spustit, když Configuration Manager má omezené nebo žádné připojení k síti. Samostatné médium spouštějte následujícími způsoby:  

- Pokud cílový počítač není spuštěný, použije se image prostředí Windows PE přidružená k tomuto pořadí úkolů ze samostatného média a zahájí se pořadí úkolů.  

- Ruční spuštění samostatného média. Pokud je uživatel přihlášený k počítači, může spustit pořadí úkolů z média.  

> [!IMPORTANT]  
> Kroky pořadí úkolů v samostatném médiu musí být možné spustit bez načtení dat ze sítě. V opačném případě se krok pořadí úkolů, který se pokusí načíst data, nezdařil. Například krok pořadí úloh, který vyžaduje, aby distribuční bod získal balíček, se nezdařil. Pokud samostatné médium obsahuje nezbytný balíček, krok pořadí úkolů se úspěšně dokončí.  

Další informace najdete v tématu [vytvoření samostatného média](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Spouštěcí médium

Spouštěcí médium obsahuje požadované soubory ke spuštění cílového počítače, aby se mohl připojit k infrastruktuře Configuration Manager. Pak určí, která pořadí úkolů se mají spustit na základě jejich členství v kolekci. Toto médium neobsahuje pořadí úkolů ani závislé objekty. Místo toho klient stáhne obsah přes síť. Tato metoda je užitečná pro nové počítače nebo holé nasazení, pokud v cílovém počítači není žádný operační systém.  

Další informace najdete v tématu [Vytvoření spouštěcího média](../deploy-use/create-bootable-media.md).  

#### <a name="prestaged-media"></a>Předzpracované médium

Předzpracované médium nasadí bitovou kopii operačního systému do cílového počítače, který není zřízený. Předzpracované médium je uloženo jako soubor bitové kopie systému Windows (WIM). Tento soubor může výrobce nebo v přípravném centru podniku nainstalovat na holé počítač. Výhodou předzpracovaného média je to, že tato umístění nevyžadují připojení k vašemu Configuration Manager prostředí.  

Další informace najdete v tématu [Vytvoření předzpracovaného média](../deploy-use/create-prestaged-media.md).  

## <a name="next-steps"></a>Další kroky

- [Zabezpečení a ochrana osobních údajů pro nasazení operačního systému](security-and-privacy-for-operating-system-deployment.md)

- [Příprava rolí systému webového serveru pro nasazení operačního systému](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
