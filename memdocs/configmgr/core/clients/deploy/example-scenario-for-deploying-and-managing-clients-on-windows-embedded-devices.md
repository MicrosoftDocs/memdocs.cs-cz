---
title: Ukázkový scénář – nasazení klientů se systémem Windows Embedded
titleSuffix: Configuration Manager
description: Podívejte se na vzorový scénář pro nasazení a správu Configuration Manager klientů v zařízeních se systémem Windows Embedded.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713328"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Ukázkový scénář pro nasazení a správu Configuration Manager klientů v zařízeních se systémem Windows Embedded

*Platí pro: Configuration Manager (Current Branch)*

Tento scénář předvádí, jak můžete pomocí Configuration Manager spravovat zařízení se systémem Windows Embedded s povoleným filtrem zápisu. Pokud vaše integrovaná zařízení nepodporují filtry zápisu, chovají se jako standardní klienti Configuration Manager a tyto postupy se nevztahují.  

Společnost Coho vinic & Winery otevírá centrum návštěvníků a potřebují veřejné terminály, které používají Windows Embedded ke spouštění interaktivních prezentací. Budova pro nové centrum pro návštěvníky není blízko oddělení IT, takže veřejné terminály musí být spravované vzdáleně. Kromě softwaru, který spouští prezentace, musí tato zařízení používat aktuální software ochrany proti malwaru, aby splňovala zásady zabezpečení společnosti. Veřejné terminály musí běžet 7 dní v týdnu bez výpadku, než se otevře Centrum pro návštěvníky.  

 Společnost Coho už běží Configuration Manager ke správě zařízení v síti. Configuration Manager je nakonfigurované pro spouštění Endpoint Protection a instalaci aktualizací softwaru a aplikací. Protože však IT tým nespravoval zařízení se systémem Windows Embedded, správce Configuration Manager spustí pilotní nasazení, aby spravoval dvě veřejné terminály v rámci příjmu.   

 Chcete-li spravovat tato zařízení se systémem Windows Embedded s povolenými filtry zápisu, Configuration Manager správce provede následující kroky k instalaci klienta Configuration Manager, ochraně klienta pomocí Endpoint Protection a instalaci interaktivního prezentačního softwaru.  

1. Správce Configuration Manager (správce) přečte, jak zařízení se systémem Windows Embedded používají filtry zápisu a jak to může Configuration Manager zlepšit tím, že automaticky zakáže a znovu povolí filtry zapisovače k trvalé instalaci softwaru.  

    Další informace najdete v tématu [Plánování nasazení klientů na zařízení se systémem Windows Embedded](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Předtím, než správce nainstaluje klienta Configuration Manager, vytvoří správce novou kolekci zařízení založenou na dotazech pro zařízení se systémem Windows Embedded. Protože společnost k identifikaci svých počítačů používá standardní formáty názvů, může správce jednoznačně identifikovat zařízení se systémem Windows Embedded podle prvních šesti písmen názvu počítače: **WEMDVC**. Správce k vytvoření této kolekce používá následující dotaz WQL: **vyberte sms_r_system. NetBIOS z sms_r_system, kde sms_r_system. NetBIOS jako "WEMDVC%"**  

    Tato kolekce umožňuje správci spravovat zařízení se systémem Windows Embedded s různými možnostmi konfigurace z jiných zařízení. Správce použije tuto kolekci k řízení restartování, nasazení Endpoint Protection s nastaveními klienta a nasazení interaktivní prezentační aplikace.  

    Přečtěte si téma [Vytvoření kolekcí](../../../core/clients/manage/collections/create-collections.md).  

3. Správce nakonfiguruje kolekci pro časový interval pro správu a údržbu, aby se zajistilo, že restartování, které může být potřeba k instalaci aplikace pro prezentace a kdy upgrady, neproběhne během otevíracích hodin centra pro návštěvníky. Provozní doba bude od 09:00 do 18:00, pondělí až neděle. Správce nakonfiguruje časový interval pro správu a údržbu pro každý den, 18:30 až 06:00.  

4. Další informace najdete v tématu [použití časových období údržby](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. Správce pak nakonfiguruje vlastní nastavení klienta zařízení pro instalaci klienta Endpoint Protection, a to tak, že pro následující nastavení vyberete **Ano** a potom nasadí toto vlastní nastavení klienta do kolekce zařízení se systémem Windows Embedded:  

   - **Instalovat klienta Endpoint Protection na klientských počítačích**  

   - **U zařízení se systémem Windows Embedded s filtry zápisu povolit instalaci klienta aplikace Endpoint Protection (vyžaduje restart)**  

   - **Povolit provedení instalace a restartu klienta bodu Endpoint Protection mimo časové intervaly pro správu a údržbu**  

     Pokud je nainstalován klient Configuration Manager, tato nastavení nainstalují klienta Endpoint Protection a zajistěte, aby byla v operačním systému v rámci instalace zachována, místo zapsání pouze do překrytí. Zásady zabezpečení společnosti vyžadují, aby byl vždy nainstalován antimalwarový software, a správce nechce spustit riziko, že veřejné terminály nejsou chráněny po dobu jejich restartování ani po krátké době.  

   > [!NOTE]  
   >  Restartování, které je požadováno pro instalaci klienta bodu Endpoint Protection, probíhá pouze jednou v době instalace zařízení a před zprovoznění centra pro návštěvníky. Na rozdíl od pravidelného nasazování aplikací nebo aktualizací softwaru se při příštím instalaci klienta Endpoint Protection do stejného zařízení pravděpodobně bude v případě, že se společnost upgraduje na další verzi Configuration Manager.  

    Další informace najdete v tématu [konfigurace Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. S nastavením konfigurace pro klienta nyní správce připraví instalaci Configuration Managerch klientů. Předtím, než může správce nainstalovat klienty, musí ručně zakázat filtr zápisu na zařízeních se systémem Windows Embedded. Správce přečte dokumentaci výrobce OEM, která doprovází veřejné terminály, a postupuje podle pokynů pro zakázání filtrů zápisu.  

    Správce přejmenuje zařízení, aby používalo standardní firemní formát názvů, a potom ručně nainstaluje klienta spuštěním služby CCMSetup pomocí následujícího příkazu z mapované jednotky, která obsahuje zdrojové soubory klienta: **CCMSetup. exe/MP: mpserver. cohovineyardandwinery. com SMSSITECODE = CO1**  

    Tento příkaz nainstaluje klienta, přiřadí klienta k bodu správy s intranetovým názvem FQDN **mpserver.cohovineyardandwinery.com**a přiřadí klienta k primární lokalitě s názvem **CO1**.  

    Správce ví, že při instalaci a posílání jejich stavu na lokalitu vždycky trvá, když klienti přejdou. Proto správce počká, než potvrdí, že klienti se úspěšně nainstalovali, přiřadí k lokalitě a zobrazí se jako klienti v kolekci, kterou vytvořili pro zařízení se systémem Windows Embedded.  

    Jako další potvrzení správce zkontroluje vlastnosti Configuration Manager v Ovládacích panelech na zařízeních a porovná je se standardními počítači se systémem Windows, které jsou spravovány lokalitou. Například možnost **Agent inventáře hardwaru** na kartě **Součásti** zobrazuje hodnotu **Povoleno**a na kartě **Akce** se nachází 11 dostupných akcí, které zahrnují akce **Cyklus hodnocení nasazení aplikací** a **Cyklus sběru dat pro vyhledávání**.  

    Je možné, že klienti jsou úspěšně nainstalováni, přiřazeni a přijímáni klientské zásady z bodu správy, a poté ručně povolí filtry zápisu podle pokynů výrobce OEM.  

    Další informace naleznete v tématu:  

   -   [Postup nasazení klientů na počítače s Windows](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Přiřazení klientů k lokalitě](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Když je teď klient Configuration Manager nainstalovaný v zařízeních se systémem Windows Embedded, správce potvrdí, že je může spravovat stejným způsobem, jakým spravují standardní klienty se systémem Windows. Správce může například z konzoly Configuration Manager vzdáleně spravovat pomocí vzdáleného řízení, zahájit pro ně zásady klienta a zobrazit vlastnosti klienta a inventář hardwaru.  

    Vzhledem k tomu, že jsou tato zařízení připojená k doméně služby Active Directory, správce je nemusí ručně schvalovat jako důvěryhodné klienty a potvrzuje od konzoly Configuration Manager, kterou schvalují.  

    Další informace najdete v tématu [Správa klientů](../../../core/clients/manage/manage-clients.md).  

8. Aby mohl správce nainstalovat interaktivní prezentační software, spustí **Průvodce nasazením softwaru** a nakonfiguruje požadovanou aplikaci. Na stránce **činnost koncového uživatele** průvodce v části **zpracování filtru zápisu pro zařízení se systémem Windows Embedded** přijměte výchozí možnost, která vybere položku **Potvrdit změny v den konečného termínu nebo během údržby (vyžaduje restart)**.  

    Správce zachová tuto výchozí možnost pro filtry zápisu, aby bylo zajištěno, že aplikace bude po restartu stále dostupná, aby bylo vždy k dispozici návštěvníkům, kteří používají veřejné terminály. Denní interval pro správu a údržbu zajišťuje bezpečnou dobu, během které může dojít k restartování z důvodu instalace nebo aktualizací.  

    Správce nasadí aplikaci do kolekce zařízení se systémem Windows Embedded.  

    Další informace najdete v tématu [nasazení aplikací pomocí Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Pro konfiguraci aktualizací definic pro Endpoint Protection správce používá aktualizace softwaru a spustí Průvodce vytvořením pravidla automatického nasazení. Vyberou šablonu **aktualizace definic** , která má průvodce předem vyplnit nastavením vhodným pro Endpoint Protection.  

     Mezi tato nastavení patří následující možnosti na stránce **Činnost koncového uživatele** :  

   - **Chování konečného termínu**: Není zaškrtnuté políčko **Instalace softwaru** .  

   - **Zpracování filtru zápisu pro zařízení s platformou Windows Embedded**: Není zaškrtnuté políčko **Potvrdit změny v den konečného termínu nebo během údržby (vyžaduje restart)** .  

     Správce zachová tato výchozí nastavení. Tyto dvě možnosti s touto konfigurací společně umožňují instalovat jakékoli definice aktualizací softwaru pro bod Endpoint Protection do překrytí během dne, a definice tak nemusí čekat na instalaci a provedení během časového intervalu pro správu a údržbu. Tato konfigurace nejlépe splňuje zásady zabezpečení společnosti, aby mohly počítače používat aktuální antimalwarovou ochranu.  

     > [!NOTE]  
     >  Na rozdíl od instalací softwaru pro aplikace může k definicím aktualizací softwaru pro bod Endpoint Protection docházet velmi často, dokonce několikrát za den. Často jde o malé soubory. U těchto typů nasazení souvisejících se zabezpečením může být často užitečné místo čekání na časový interval pro správu a údržbu vždy instalovat do překrytí. Klient Configuration Manager v případě restartování zařízení rychle znovu nainstaluje aktualizace definic softwaru, protože tato akce zahájí kontrolu vyhodnocení a nečeká na další naplánované vyhodnocení.  

     Správce vybere kolekci zařízení se systémem Windows Embedded pro pravidlo automatického nasazení.  

     Další informace najdete v tématu  
               Krok 3: konfigurace Configuration Manager aktualizací softwaru pro doručení aktualizací definic do klientských počítačů při [konfiguraci Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. Správce rozhodne nakonfigurovat úlohu údržby, která pravidelně potvrdí všechny změny v překrytí. Účelem této úlohy je podpořit nasazení definic aktualizací softwaru a snížit počet aktualizací, které se nahromadí a které je nutné znovu nainstalovat, při každém restartování zařízení. V prostředí pro správu pomáhá aplikace antimalwaru běžet efektivněji.  

    > [!NOTE]  
    >  Pokud by integrovaná zařízení používala jinou úlohu údržby podporující provedení změn, byly by tyto definice aktualizací softwaru automaticky provedeny do bitové kopie. Instalace nové verze interaktivního prezentačního softwaru by například také provedla změny definic aktualizací softwaru. Případně by instalace standardních aktualizací softwaru, které se instalují každý měsíc a instalují se během časového intervalu pro správu a údržbu, také mohla provést změny definic aktualizací softwaru. V tomto scénáři, kdy se nespouštějí standardní aktualizace softwaru a interaktivní prezentační software pravděpodobně nebude příliš často aktualizován, však může automatické provedení aktualizací definic softwaru do bitové kopie trvat celé měsíce.  

     Správce nejprve vytvoří vlastní pořadí úloh, které nemá žádné jiné nastavení než název. Spustí Průvodce vytvořením pořadí úloh:  

    1. Na stránce **vytvořit novou sekvenci úloh** vybere správce možnost **vytvořit nové vlastní pořadí úloh**a poté klikne na tlačítko **Další**.  

    2. Na stránce **informace o pořadí úloh** správce zadá **úlohu údržby, která potvrdí změny v integrovaných zařízeních** pro název pořadí úloh a poté klikne na tlačítko **Další**.  

    3. Na stránce **Souhrn** vybere správce **Další**a dokončí průvodce.  

       Správce poté nasadí toto vlastní pořadí úloh do kolekce zařízení se systémem Windows Embedded a nakonfiguruje spuštění plánu každý měsíc. V rámci nastavení nasazení vyberou zaškrtávací políčko **Potvrdit změny v den konečného termínu nebo během údržby (vyžaduje restart)** , aby se změny zachovaly po restartování. Pro konfiguraci tohoto nasazení správce vybere vlastní pořadí úloh, které právě vytvořil, a potom na kartě **Domů** ve skupině **nasazení** kliknutím na **nasadit** spusťte Průvodce nasazením softwaru:  

    4. Na stránce **Obecné** správce vybere kolekci zařízení se systémem Windows Embedded a poté klikne na tlačítko **Další**.  

    5. Na stránce **nastavení nasazení** vybere správce **účel** **požadováno**a potom klikne na tlačítko **Další**.  

    6. Na stránce **plánování** klikne na možnost **Nový** a v časovém intervalu pro správu zadejte týdenní plán a potom klikněte na tlačítko **Další**.  

    7. Správce dokončí průvodce bez jakýchkoli dalších změn.  

       Další informace najdete v tématu  
                 [Správa pořadí úkolů pro automatizaci úloh](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Aby se veřejné terminály spouštěly automaticky, správce zapíše skript pro konfiguraci zařízení pro následující nastavení:  

    - Automaticky přihlásit pomocí účtu Guest bez hesla.  

    - Automaticky spouštět interaktivní prezentační software při spuštění.  

      Správce používá balíčky a programy k nasazení tohoto skriptu do kolekce zařízení se systémem Windows Embedded. Když správce spustí Průvodce nasazením softwaru, znovu zaškrtne políčko **Potvrdit změny v den konečného termínu nebo během okna údržby (vyžaduje restart)** a zachová tak změny po restartu.  

      Další informace najdete v tématu [balíčky a programy](../../../apps/deploy-use/packages-and-programs.md).  

12. Po ráno správce zkontroluje zařízení se systémem Windows Embedded. Potvrzují následující:  

    - Veřejný terminál je automaticky přihlášen pomocí účtu Guest.  

    - Interaktivní prezentační software je spuštěný.  

    - Klient Endpoint Protection je nainstalován a obsahuje nejnovější definice aktualizace softwaru.  

    - Zda se zařízení restartovalo během okna údržby.  

      Další informace naleznete v tématu:  

    - [Sledování služby Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Monitorování aplikací pomocí Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. Správce monitoruje veřejné terminály a nahlásí jejich úspěšnou správu správci. Výsledkem je, že pro centrum návštěvníků bude objednáno 20 veřejných terminálů.  

     Aby nedocházelo k ruční instalaci klienta Configuration Manager, která vyžaduje ruční zakázání a povolení filtrů zápisu, Správce zajistí, aby tato objednávka zahrnovala přizpůsobenou image, která už obsahuje instalaci a přiřazení lokality klienta Configuration Manager. Navíc jsou zařízení pojmenována v souladu s formátem přidělování názvů společnosti.  

     Veřejné terminály budou doručeny do centra pro návštěvníky týden před jeho otevřením. Během této doby se veřejné terminály připojují k síti, veškerá s nimi související správa zařízení probíhá automaticky a není nutný žádný místní správce. Správce potvrdí, že veřejné terminály fungují podle potřeby:  

    -   Klienti na veřejných terminálech dokončí přiřazení lokality a stáhnou důvěryhodný kořenový klíč ze služby Active Directory Domain Services.  

    -   Klienti na veřejných terminálech jsou automaticky přidáni do kolekce zařízení se systémem Windows a konfigurováni pomocí okna údržby.  

    -   Klient Endpoint Protection je nainstalován a obsahuje nejnovější definice aktualizace softwaru za účelem ochrany proti malwaru.  

    -   Interaktivní prezentační software je nainstalován a pracuje automaticky. Je připraven pro návštěvníky.  

14. Po tomto počátečním nastavení dojde k restartům, které mohou vyžadovat aktualizace pouze po uzavření centra pro návštěvníky.  
