---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Seznamte se s novými funkcemi dostupnými v Configuration Manager Technical Preview verze 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d8c1cd6610bd09b2714951d8a755770b6347b2f6
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905232"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1805 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1805. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Vytvoření postupného nasazení s ručně nakonfigurovanými fázemi pro pořadí úkolů
<!--1358148-->
Nyní můžete [vytvořit dvoufázové nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) s ručně nakonfigurovanými fázemi pro pořadí úkolů. Na kartě **fáze** v Průvodci vytvořením fáze nasazení můžete přidat až 10 dalších fází. 


### <a name="try-it-out"></a>Určitě to udělejte!
Postupujte podle pokynů a vytvořte dvoufázové nasazení, kde ručně nakonfigurujete všechny fáze. Pošlete nám [svůj názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali. 

1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.  

2. Klikněte pravým tlačítkem na existující pořadí úloh a vyberte **vytvořit dvoufázové nasazení**.  

3. Na kartě **Obecné** udělte postupné nasazení název, popis (volitelné) a vyberte možnost **ručně konfigurovat všechny fáze**.  

4. Na kartě **fáze** klikněte na **Přidat**.  

5. Zadejte **název** fáze a potom přejděte do cílové **kolekce fází**.  

6. Na kartě **nastavení fáze** zvolte jednu možnost pro každé nastavení plánování a po dokončení vyberte **Další** .  

    - Kritéria úspěchu předchozí fáze (Tato možnost je pro první fázi zakázaná.)
        - **Procento úspěšnosti nasazení**: zadejte procento zařízení, která úspěšně dokončí nasazení pro kritéria úspěšnosti předchozí fáze.  

    - Podmínky zahájení této fáze nasazení po úspěšném provedení předchozí fáze  
        - **Automaticky zahájit tuto fázi po odložení (ve dnech)**: Vyberte počet dní, po které se má čekat před začátkem další fáze po úspěchu předchozí fáze. 
        - **Ruční zahájení této fáze nasazení**: po úspěšném dokončení předchozí fáze tuto fázi nespustí automaticky.  

    - Po zacílení na zařízení nainstalovat software
        - **Co nejdříve**: nastaví konečný termín instalace na zařízení, jakmile bude zařízení cíleno.
        - **Čas konečného termínu (relativní vůči času cílení na zařízení)**: nastaví konečný termín pro instalaci určitého počtu dní od cílení na zařízení.  
     
7. Dokončete průvodce nastavením fáze.

8. Na kartě **fáze** v Průvodci vytvořením fáze nasazení teď můžete přidat, odebrat, změnit pořadí nebo upravit fáze tohoto nasazení.  

9. Dokončete Průvodce vytvořením postupného nasazení.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Podpora distribučního bodu cloudu pro Azure Resource Manager
<!--1322209-->
Při vytváření instance [distribučního bodu cloudu](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)nyní průvodce poskytuje možnost vytvoření **nasazení Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako [Skupina prostředků](/azure/azure-resource-manager/resource-group-overview#resource-groups). Při nasazování cloudového distribučního bodu s Azure Resource Manager lokalita používá Azure Active Directory (Azure AD) k ověření a vytvoření potřebných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure.  

Průvodce distribučním bodem cloudu stále nabízí možnost **nasazení klasické služby** pomocí certifikátu pro správu Azure. Pro zjednodušení nasazení a správy prostředků doporučujeme použít model nasazení Azure Resource Manager pro všechny nové distribuční body cloudu. Pokud je to možné, znovu nasaďte existující cloudové distribuční body prostřednictvím Správce prostředků.

Configuration Manager nemigruje stávající klasické cloudové distribuční body do modelu nasazení Azure Resource Manager. Pomocí Azure Resource Manager nasazení vytvořte nové distribuční body cloudu a pak odeberte klasické cloudové distribuční body. 

> [!IMPORTANT]  
> Tato funkce nepovoluje podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení distribučního bodu cloudu pomocí Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [dostupné služby Azure v CSP Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Požadavky  
- Integrace se službou [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Zjišťování uživatelů služby Azure AD není vyžadováno.  

- Stejné [požadavky pro cloudový distribuční bod](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), s výjimkou certifikátu pro správu Azure.  


### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager v pracovním prostoru **Správa** rozbalte položku **Cloud Services**a vyberte možnost **cloudové distribuční body**. Na pásu karet klikněte na **Vytvořit cloudový distribuční bod** .   

2. Na stránce **Obecné** vyberte **Azure Resource Manager nasazení**. Klikněte na **Přihlásit** se a proveďte ověření pomocí účtu správce předplatného Azure. Průvodce automaticky vyplní zbývající pole z informací o předplatném služby Azure AD uložených během integrace. Pokud vlastníte více předplatných, vyberte požadované předplatné, které chcete použít. Klikněte na **Další**.  

3. Na stránce **Nastavení** zadejte jako obvykle **soubor certifikátu** PKI serveru. Tento certifikát definuje **plně kvalifikovaný název domény služby** distribučního bodu cloudu, který Azure používá. Vyberte **oblast**a pak vyberte možnost skupiny prostředků pro **Vytvoření nové** nebo **použití existující**. Zadejte nový název skupiny prostředků nebo v rozevíracím seznamu vyberte existující skupinu prostředků.  

4. Dokončete průvodce.  

> [!NOTE]  
> U vybrané aplikace serveru Azure AD přiřadí Azure oprávnění **Přispěvatel** pro předplatné.  

Monitorujte průběh nasazení služby pomocí **CloudMgr. log** ve spojovacím bodu služby.



## <a name="take-actions-based-on-management-insights"></a>Provedení akcí na základě přehledů správy
<!--1357930-->
Některé [přehledy správy](../servers/manage/management-insights.md) teď mají možnost provést akci. V závislosti na pravidle se tato akce projeví v jednom z následujících chování:  

- Automaticky navigujte v konzole nástroje na uzel, kde můžete provádět další akce. Pokud například služba Management Insights doporučuje změnit nastavení klienta, převezme akce Přejít na uzel nastavení klienta. Úpravou výchozího nebo vlastního objektu nastavení klienta můžete provést další akce.  

- Přejděte do filtrovaného zobrazení na základě dotazu. Například provedení akce na základě pravidla prázdné kolekce zobrazí v seznamu kolekcí pouze tyto kolekce. Tady můžete provést další akce, jako je odstranění kolekce nebo změna pravidel členství.  

Následující pravidla přehledu správy mají v této verzi akce:
- Zabezpečení
    - Nepodporované verze antimalwarového klienta
- Centrum softwaru
    - Používat novou verzi centra softwaru
- Aplikace
    - Aplikace bez nasazení
- Zjednodušená správa
    - Verze klientů nepatřících k vyžádání
- Kolekce
    - Prázdné kolekce 
- Cloud Services
    - Aktualizace klientů na nejnovější verzi Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Přechod úlohy konfigurace zařízení do Intune pomocí spolusprávy
<!--1357903-->

Po povolení spolusprávy teď můžete převést úlohu konfigurace zařízení z Configuration Manager na Intune. Přechodem na tuto úlohu můžete pomocí Intune nasadit zásady MDM a přitom dál používat Configuration Manager pro nasazování aplikací. 

Chcete-li převést tuto úlohu, přejděte na stránku vlastností spolusprávy a přesuňte posuvník z Configuration Manager na **pilotní** nebo **všechny**. Další informace najdete v tématu [společná správa zařízení s Windows 10](../../comanage/overview.md).

> [!Note]  
> Přesunutím této úlohy také přesunete úlohy **přístupu k prostředkům** a **Endpoint Protection** , které jsou podmnožinou úlohy konfigurace zařízení.

Při přechodu na tuto úlohu můžete i nadále nasazovat nastavení z Configuration Manager do spoluspravovaných zařízení, i když Intune je autoritou pro konfiguraci zařízení. Tato výjimka se dá použít ke konfiguraci nastavení, která vaše organizace vyžaduje, ale ještě není v Intune dostupná. Zadejte tuto výjimku pro standardní hodnoty konfigurace Configuration Manager. Povolte možnost **vždy použít tuto standardní hodnotu i pro spoluspravované klienty** při vytváření standardních hodnot nebo na kartě **Obecné** ve vlastnostech existujícího směrného plánu. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Povolit distribučním bodům použití řízení zahlcení sítě
<!--1358112-->

Přenos na pozadí s nízkou prodlevou pro Windows (LEDBAT) je funkce systému Windows Server, která usnadňuje správu přenosů v síti na pozadí. U distribučních bodů běžících na podporovaných verzích Windows serveru můžete povolit možnost upravovat síťový provoz. Klienti používají šířku pásma sítě jenom v případě, že jsou k dispozici. 


### <a name="prerequisites"></a>Požadavky
- Distribuční bod v systému Windows Server verze 1709.  

- Není k dispozici žádný požadavek klienta.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Vyberte uzel **distribuční body** . Vyberte cílový distribuční bod a na pásu karet klikněte na tlačítko **vlastnosti** .  

2. Na kartě **Obecné** povolte možnost **upravit rychlost stahování, aby se používala nevyužitá šířka pásma sítě (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Řídicí panel pro správu cloudu
<!--1358461-->
Nový **řídicí panel pro správu cloudu** poskytuje centralizované zobrazení použití brány pro správu cloudu (CMG). Pokud je lokalita připojená pomocí Azure AD, zobrazuje také data o cloudových uživatelích a zařízeních.  

Následující snímek obrazovky je součástí řídicího panelu pro správu cloudu, který ukazuje dva z dostupných dlaždic:  
![Dlaždice řídicího panelu správy cloudu CMG provoz a aktuální online klienti](media/1358461-cmg-dashboard.png)

Tato funkce zahrnuje také **analyzátor připojení CMG** pro ověřování v reálném čase, který pomáhá řešit potíže. Nástroj v konzole kontroluje aktuální stav služby a komunikační kanál prostřednictvím spojovacího bodu CMG k jakýmkoli bodům správy, které povolují přenos CMG.


### <a name="prerequisites"></a>Požadavky
- Aktivní [Brána pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md) používaná internetovými klienty.  

- Lokalita připojená do [služeb Azure](../servers/deploy/configure/azure-services-wizard.md) pro správu cloudu.  


### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

#### <a name="cloud-management-dashboard"></a>Řídicí panel pro správu cloudu

V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Vyberte uzel **Správa cloudu** a zobrazte dlaždice řídicího panelu.  

#### <a name="cmg-connection-analyzer"></a>Analyzátor připojení CMG

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Cloud Services** a vyberte možnost **Brána pro správu cloudu**.  

2. Vyberte cílovou instanci CMG a pak na pásu karet vyberte **analyzátor připojení** .  

3. V okně analyzátor připojení CMG vyberte jednu z následujících možností, které se mají ověřit u služby:  

     1. **Uživatel Azure AD**: pomocí této možnosti můžete simulovat komunikaci stejně jako cloudovou identitu uživatelů přihlášenou k zařízení s Windows 10 připojenému k Azure AD. Klikněte na **Přihlásit** se a bezpečně zadejte přihlašovací údaje pro tento uživatelský účet Azure AD.  

     2. **Certifikát klienta**: pomocí této možnosti můžete simulovat komunikaci, která je stejná jako Configuration Manager klient s [certifikátem ověřování klienta](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Kliknutím na **Spustit** spusťte analýzu. Výsledky se zobrazí v okně analyzátoru. Výběrem položky zobrazíte další podrobnosti v poli Popis.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager vždy poskytoval velké centralizované úložiště dat zařízení, které zákazníci používají pro účely vytváření sestav. Tato data jsou ale stejně dobrá, jak byla naposledy shromážděna od klientů. 

CMPivot je nový nástroj v konzole, který poskytuje přístup ke stavu zařízení ve vašem prostředí v reálném čase. Okamžitě spustí dotaz na všech aktuálně připojených zařízeních v cílové kolekci a vrátí výsledky. Tato data pak můžete filtrovat a seskupovat v nástroji. Díky poskytování dat z online klientů v reálném čase můžete rychleji odpovídat na obchodní otázky, řešit problémy a reagovat na incidenty zabezpečení.

Například při [zmírnění ohrožení zabezpečení kanálu na straně spuštění](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)je jedním z požadavků aktualizace systému BIOS. Pomocí CMPivot můžete rychle zadat dotaz na informace o systému BIOS a vyhledat klienty, kteří nedodržují předpisy. 

Na tomto snímku obrazovky CMPivot zobrazí dvě samostatné verze systému BIOS s počtem zařízení, které má jednu z nich. Tento příklad dotazu můžete použít při vyzkoušení CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Okno CMPivot s příkladem dotazu BIOSVersion](media/1358456-cmpivot-biosversion.png)

Můžete kliknout na počet zařízení a přejít k podrobnostem a zobrazit konkrétní zařízení. Při zobrazování zařízení v CMPivot můžete kliknout pravým tlačítkem na zařízení a vybrat následující [Akce klientského oznámení](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode):
- Spustit skript
- Vzdálené řízení
- Průzkumník prostředků

Když kliknete pravým tlačítkem na konkrétní zařízení, můžete si také prohlédnout konkrétní zařízení na jeden z následujících atributů:
- Příkazy pro automatické spuštění
- Nainstalované produkty
- Procesy
- Služby
- Uživatelé
- Aktivní připojení
- Chybějící aktualizace

### <a name="prerequisites"></a>Požadavky
- Cílové klienty se musí aktualizovat na nejnovější verzi.  

- Správce Configuration Manager potřebuje oprávnění ke spouštění skriptů. Další informace najdete v tématu [role zabezpečení pro skripty](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte možnost **kolekce zařízení**. Vyberte cílovou kolekci a na pásu karet klikněte na tlačítko **Spustit CMPivot** a spusťte nástroj.  

2. Rozhraní poskytuje další informace o použití nástroje. 
     - Můžete ručně zadat řetězce dotazů v horní části nebo kliknout na odkazy v online dokumentaci.
     - Klikněte na jednu **entitu** a přidejte ji do řetězce dotazu. 
     - Odkazy pro **operátory tabulky**, **agregační funkce**a **skalární funkce** otevřou referenční dokumentaci jazyka ve webovém prohlížeči. CMPivot používá stejný dotazovací jazyk jako [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Vylepšená zabezpečená komunikace klientů
<!--1356889,1358228,1358460-->
Pro všechny Configuration Manager komunikačních cest se doporučuje používat komunikaci pomocí protokolu HTTPS, ale můžou být pro některé zákazníky náročné kvůli režii při správě certifikátů PKI. Zavedení integrace služby Azure Active Directory (Azure AD) omezuje některé, ale ne všechny požadavky na certifikáty. 

Tato verze obsahuje vylepšení způsobu, jakým klienti komunikují se systémy lokality. Existují dva primární cíle těchto vylepšení:  

- Komunikaci klienta můžete zabezpečit bez nutnosti ověřování certifikátů serverů PKI.  

- Klienti mohou bezpečně přistupovat k obsahu z distribučních bodů bez nutnosti účtu přístupu k síti.  

> [!Note]  
> Certifikáty PKI jsou stále platnou možností pro zákazníky, kteří je chtějí používat.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Řešení
Následující scénáře mají výhodu z těchto vylepšení:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a>Scénář 1: klient do bodu správy
<!--1356889-->
[Zařízení připojená k Azure AD](/azure/active-directory/devices/concept-azure-ad-join) můžou komunikovat přes bránu pro správu cloudu (CMG) s bodem správy nakonfigurovaným pro protokol HTTP. Webový server vygeneruje certifikát pro bod správy, který umožňuje komunikaci přes zabezpečený kanál.   

> [!Note]  
> Toto chování je změněno z Configuration Manager aktuální větev verze 1802, která vyžaduje bod správy s povoleným protokolem HTTPS pro tento scénář. Další informace najdete v tématu [Povolení bodu správy pro protokol HTTPS](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a>Scénář 2: klient s distribučním bodem
<!--1358228-->
V pracovní skupině nebo klientovi připojeném k Azure AD se dá obsah přes zabezpečený kanál stáhnout z distribučního bodu nakonfigurovaného pro protokol HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a>Scénář 3 identita zařízení Azure AD 
<!--1358460-->
Připojené zařízení Azure AD nebo [hybridní zařízení Azure AD](/azure/active-directory/devices/concept-azure-ad-join-hybrid) bez přihlášeného uživatele Azure AD může bezpečně komunikovat s přiřazenou lokalitou. Cloudová identita zařízení je nyní dostačující k ověřování pomocí CMG a bodu správy.  


### <a name="prerequisites"></a>Požadavky  

- Bod správy nakonfigurovaný pro připojení klienta pomocí protokolu HTTP. Tuto možnost nastavte na kartě **Obecné** ve vlastnostech role systému lokality.  

- Distribuční bod konfigurovaný pro připojení klienta pomocí protokolu HTTP. Tuto možnost nastavte na kartě **Obecné** ve vlastnostech role systému lokality. Nepovolujte možnost **Povolit anonymní připojení klientů**.  

- Brána pro správu cloudu.  

- Připojte lokalitu k Azure AD pro správu cloudu.  

    - Pokud jste už tento požadavek splnili pro vaši lokalitu, musíte aktualizovat aplikaci Azure AD. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte možnost **Azure Active Directory klienti**. Vyberte tenanta Azure AD, vyberte webovou aplikaci v podokně **aplikace** a pak na pásu karet klikněte na **aktualizovat nastavení aplikace** .  

- Klient se systémem Windows 10 verze 1803 a připojený ke službě Azure AD. (Tento požadavek je technicky jenom pro [scénář 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte možnost **lokality**. Vyberte lokalitu a na pásu karet klikněte na tlačítko **vlastnosti** .  

2. Přepněte na kartu **komunikace s klientským počítačem** . Vyberte možnost **protokolu HTTPS nebo http** a pak povolte možnost Nová pro **použití Configuration Manager generovaných certifikátů pro systémy lokality http**.  

Podívejte se na předchozí [seznam scénářů](#bkmk_token) , které chcete ověřit.

> [!Tip]
> V této verzi počkejte až 30 minut, než bod správy přijme a nakonfiguruje nový certifikát z lokality.

Tyto certifikáty můžete zobrazit v konzole Configuration Manager. Otevřete pracovní prostor **Správa** , rozbalte položku **zabezpečení**a vyberte uzel **certifikáty** . Vyhledejte kořenový certifikát **vydávající zprávu SMS** a certifikáty rolí serveru lokality vydané kořenem vydávající zprávy SMS.


### <a name="known-issues"></a>Známé problémy
- Uživatel nemůže zobrazit v centru softwaru žádné aplikace, které jsou mu cílené, jako dostupné.  

- Scénáře nasazení operačního systému stále vyžadují účet pro přístup k síti.  

- Rychlé a opakované povolení a zakázání možnosti **použití Configuration Manager generovaných certifikátů pro systémy lokality http** může způsobit, že se certifikát nebude správně navazovat na role systému lokality. Žádné certifikáty vydané certifikátem vydávající SMS nejsou vázány na web ve Windows Server Internetová informační služba (IIS). Pokud chcete tento problém obejít, odstraňte z úložiště certifikátů **SMS** v systému Windows všechny certifikáty vydané vydáním SMS a pak restartujte službu Smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Vylepšení pro povolení podpory aktualizací softwaru třetích stran
<!--1357605-->
V důsledku vaší zpětné vazby služby UserVoice na [podporu aktualizací softwaru třetích stran](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)se tato verze dále opakuje na integraci s System Center Updates Publisher (SCUP). Verze Configuration Manager Technical Preview [1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) přidala možnost číst certifikát ze služby WSUS pro aktualizace třetích stran a potom tento certifikát nasadit do klientů. Ale pořád potřebujete použít nástroj SCUP k vytvoření a správě certifikátu pro podepisování aktualizací softwaru třetích stran.

V této verzi můžete povolit, aby lokalita Configuration Manager automaticky nakonfigurovala certifikát. Lokalita komunikuje se službou WSUS, aby vygenerovala certifikát pro tento účel. Configuration Manager pak tento certifikát dál nasadí na klienty. Tato iterace eliminuje nutnost použití nástroje SCUP k vytvoření a správě certifikátu. 

Další informace o obecném použití nástroje SCUP naleznete v tématu [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Požadavky
- Povolte a nasaďte nastavení klienta **Povolit aktualizace softwaru třetích stran** ve skupině **aktualizace softwaru** .
- Pokud je služba WSUS na samostatném serveru z bodu aktualizace softwaru, musíte na vzdáleném serveru služby WSUS udělat jednu z následujících možností:
    - Povolení služby Remote Registry v systému Windows  
    nebo
    - V klíči registru `HKLM\Software\Microsoft\Update Services\Server\Setup` vytvořte novou hodnotu DWORD s názvem **EnableSelfSignedCertificates** s hodnotou `1` . 

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality** a vyberte možnost **lokality**. Vyberte lokalitu nejvyšší úrovně, klikněte na pásu karet na možnost **Konfigurovat součásti lokality** a vyberte možnost **bod aktualizace softwaru**.  

2. Přepněte na kartu **aktualizace třetích stran** . Vyberte možnost **Povolení aktualizací softwaru třetích stran**a potom vyberte možnost **Configuration Manager automaticky spravuje certifikát**.

3. Pokračujte ve zbytku typického SCUP pracovního postupu pro import katalogu aktualizací softwaru třetí strany a potom tyto aktualizace nasaďte do klientů.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Vylepšení pořadí úkolů místního upgradu Windows 10
<!--1358500-->

Výchozí šablona pořadí úkolů pro místní upgrade systému Windows 10 nyní zahrnuje další novou skupinu s doporučenými akcemi, které je třeba přidat pro případ, že proces upgradu nebude úspěšný. Tyto akce usnadňují řešení potíží.

### <a name="new-groups-under-run-actions-on-failure"></a>Nové skupiny v části **Akce spuštění při selhání**
- **Shromažďovat protokoly**: Pokud chcete shromáždit protokoly z klienta, přidejte do této skupiny další kroky. 
    - Běžný postup je zkopírovat soubory protokolu do sdílené síťové složky. Chcete-li vytvořit toto připojení, použijte krok [připojit k síťové složce](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) . 
    - K provedení operace kopírování použijte vlastní skript nebo nástroj buď pomocí [příkazového řádku spustit](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) , nebo kroku [Spustit skript prostředí PowerShell](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .
    - Soubory, které se mají shromažďovat, můžou zahrnovat tyto protokoly:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Další informace o setupaccích. log a dalších protokolech instalační program systému Windows najdete v tématu [instalační program systému Windows soubory protokolu](/windows/deployment/upgrade/log-files).
    - Další informace o Configuration Manager klientských protokolech najdete v tématu [Configuration Manager protokolech klienta](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs) .
    - Další informace o _SMSTSLogPath a dalších užitečných proměnných najdete v tématu [předdefinované proměnné pořadí úkolů](../../osd/understand/task-sequence-variables.md) .

- **Spustit diagnostické nástroje**: Pokud chcete spustit další diagnostické nástroje, přidejte do této skupiny kroky. Tyto nástroje by měly být automatizované pro shromažďování dalších informací ze systému hned po případném selhání.
    - Jedním z těchto nástrojů je Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Jedná se o samostatný diagnostický nástroj, který můžete použít k získání podrobných informací o tom, proč upgrade Windows 10 neproběhl úspěšně.
         - V Configuration Manager [vytvořte balíček](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) pro nástroj.
         - Přidejte krok [Spustit příkazový řádek](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) do této skupiny pořadí úkolů. K odkazování na nástroj použijte možnost **balíček** . Následující řetězec je příkladem **příkazového řádku**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace nainstalované s klientem
<!--1357971-->

Nástroj pro zobrazení protokolu CMTrace se teď automaticky nainstaluje společně s klientem Configuration Manager. Přidá se do instalačního adresáře klienta, který je ve výchozím nastavení `%WinDir%\ccm\cmtrace.exe` .

> [!Note]  
> CMTrace není *automaticky registrován* v systému Windows pro otevření přípony souboru. log.



## <a name="improvement-to-the-configuration-manager-console"></a>Zlepšení konzoly Configuration Manager
<!--1358202-->
Provedli jsme následující vylepšení Configuration Manager konzole:

- Seznam zařízení v části prostředky a kompatibilita, zařízení, teď ve výchozím nastavení zobrazuje aktuálně přihlášeného uživatele. Tato hodnota je jako [stav klienta](../clients/manage/monitor-clients.md#bkmk_indStatus)jako aktuální. Hodnota se vymaže při odhlášení uživatele. Pokud není přihlášen žádný uživatel, hodnota je prázdná. 

### <a name="known-issues"></a>Známé problémy
Hodnota aktuálně přihlášeného uživatele je prázdná v uzlu zařízení nebo při zobrazení seznamu zařízení v uzlu kolekce zařízení. Pokud chcete tento problém obejít, Stáhněte si tento [skript SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Na serveru databáze lokality spusťte sp_BgbUpdateLiveData. SQL a restartujte služby Smsexec a sms_notification_server v bodu správy.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Vylepšení zpětné vazby z konzoly
<!--1357542-->
Tato verze zahrnuje následující vylepšení nového mechanismu [zpětné vazby](capabilities-in-technical-preview-1804.md#bkmk_feedback) v konzole Configuration Manager:  

- Dialog zpětná vazba teď pamatuje předchozí nastavení, například vybrané možnosti a vaši e-mailovou adresu.  

- Teď podporuje offline zpětnou vazbu. Uložte svůj názor z konzoly a pak ho nahrajte do Microsoftu z internetového systému připojeného k Internetu. Použijte nový nástroj pro odeslání zpětné vazby z offline umístění v části `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` . Chcete-li zobrazit dostupné a požadované možnosti příkazového řádku, spusťte nástroj s `--help` možností. Připojený systém potřebuje přístup k **Petrol.Office.Microsoft.com**.

### <a name="known-issues"></a>Známé problémy
Když použijete možnost **odeslat smajlíka** nebo **Odeslat zamračení** z konzoly na počítači s připojením k Internetu, může se vám vrátit následující zpráva: "Chyba při odesílání názoru." Pokud kliknete na **Další podrobnosti**, zobrazí se následující text: `{"Message":""}` . Příčinou této chyby je známý problém s odpovědí ze systému zpětné vazby back-endu. Chybu můžete zavřít. Společnost Microsoft si pořád obdržela váš názor. (Pokud se v podrobnostech zobrazují jiné zprávy, použijte možnost zpětné vazby offline, abyste mohli znovu poslat svůj názor později.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Vylepšení distribučních bodů s povoleným PXE
<!--1357580-->

Tato verze zahrnuje následující vylepšení, pokud použijete možnost [**Povolit respondér technologie PXE bez služby pro nasazení systému Windows**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) v distribučním bodě:  

- Pokud tuto možnost povolíte, automaticky se v distribučním bodě vytvoří pravidla brány Windows Firewall.  
- Vylepšení protokolování součástí



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Zlepšení inventáře hardwaru pro velké celočíselné hodnoty
<!--1357880-->
Inventář hardwaru má v současné době omezení pro celá čísla větší než 4 294 967 296 (2 ^ 32). Tento limit se dá dosáhnout u atributů, jako jsou například velikosti pevného disku v bajtech. Bod správy nezpracovává celočíselné hodnoty nad tímto limitem, takže v databázi není uložena žádná hodnota. V této verzi se tento limit zvýšil na 18446744073709551616 (2 ^ 64). 

U vlastnosti s hodnotou, která se nemění, jako je celková velikost disku, se po upgradu lokality nemusí okamžitě zobrazit hodnota. Většina inventáře hardwaru je rozdílová sestava. Klient odesílá pouze hodnoty, které se mění. Chcete-li toto chování obejít, přidejte do stejné třídy další vlastnost. Tato akce způsobí, že klient aktualizuje všechny vlastnosti ve třídě, která se změnila. 



## <a name="improvement-to-wsus-maintenance"></a>Zlepšení údržby služby WSUS
<!--1357898-->

Průvodce vyčištěním služby WSUS nyní odmítá aktualizace, jejichž platnost vypršela nebo byla nahrazena podle pravidel nahrazení. Tato pravidla jsou definovaná ve vlastnostech komponenty bodu aktualizace softwaru.

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality** a vyberte možnost **lokality**. Vyberte lokalitu nejvyšší úrovně, klikněte na pásu karet na možnost **Konfigurovat součásti lokality** a vyberte možnost **bod aktualizace softwaru**.  

2. Přepněte na kartu **pravidla nahrazení** . Povolte možnost **Spustit Průvodce vyčištěním služby WSUS**. Zadejte požadované chování nahrazování.  

3. Zkontrolujte soubor souboru wsyncmgr. log.



## <a name="improvement-to-support-for-cng-certificates"></a>Vylepšení podpory pro certifikáty CNG
<!--1357314-->
V této verzi použijte [certifikáty CNG](../plan-design/network/cng-certificates-overview.md) pro následující další role serveru s podporou protokolu https:  
- Bod registrace certifikátu, včetně serveru NDES, s modulem zásad Configuration Manager



## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
