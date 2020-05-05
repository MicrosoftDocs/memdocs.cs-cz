---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1712 pro Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721273"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1712 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1712. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. 

Před instalací této verze Technical Preview si přečtěte [Technical Preview for Configuration Manager](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Známé problémy v této verzi Technical Preview:**
- **Aktualizace na novou verzi Preview se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné před aktualizací na tuto novou verzi Preview odinstalovat server lokality pasivního režimu. Server lokality v pasivním režimu můžete po dokončení aktualizace znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **Konfigurace** > **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms489412-->


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Neupgradovat automaticky nahrazené aplikace
<!-- 1351266 -->
Na základě [zpětné vazby vašeho uživatelského hlasu](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)v této verzi máte možnost nakonfigurovat nasazení aplikace tak, aby neautomaticky inovovali žádnou nahrazenou verzi. Nyní při vytváření nasazení na stránce **nastavení nasazení** v Průvodci nasazením **softwaru**pro **dostupný** nebo **požadovaný** účel instalace můžete povolit nebo zakázat možnost **automaticky upgradovat jakékoli nahrazené verze této aplikace**.


## <a name="install-multiple-applications-in-software-center"></a>Instalace více aplikací v centru softwaru
<!-- 1357126 -->
Pokud chce koncový uživatel nebo stolní počítač nainstalovat na zařízení více aplikací, Centrum softwaru teď podporuje instalaci více vybraných aplikací. To umožňuje, aby byl uživatel efektivnější, i když nečeká na dokončení jedné instalace před spuštěním dalšího.

Při použití režimu vícenásobného výběru na kartě **aplikace** určují následující kritéria, které aplikace Centrum softwaru umožňují vícenásobný výběr:
- Aplikace je viditelná pro uživatele.
- Aplikace už není nainstalovaná.
- Schválení správcem se nevyžaduje nebo už je udělené.
- Stav aplikace je k dispozici (například ještě nestahuje obsah).

### <a name="try-it-out"></a>Určitě to udělejte!
**V konzole Configuration Manager:** Nasaďte je pro uživatele nebo zařízení více aplikací pro instalaci, a to buď jako k dispozici, nebo požadováno (s konečným termínem v budoucnosti). Nevyžadují schválení správcem. Další informace najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).

**V centru softwaru:**
 1. Karta **aplikace** by měla být ve výchozím nastavení otevřená. 
 2. Pokud chcete v zobrazení seznamu zadat režim vícenásobného výběru, klikněte na ikonu Nový. ![Ikona vícenásobného výběru centra softwaru](media/software-center-multi-select-apps.png) v pravém horním rohu.
 3. Kliknutím na zaškrtávací políčko nalevo od aplikací v seznamu vyberte dvě nebo víc aplikací, které chcete nainstalovat.
 4. Klikněte na tlačítko **nainstalovat vybrané** .

Aplikace se instalují jako normální, jenom teď po úspěchu.


## <a name="client-based-pxe-responder-service"></a>Služba respondérů technologie PXE založená na klientovi
<!-- 1357148 -->
Běžnou výzvou pro zákazníky je poskytovat služby PXE na vzdálených nebo pobočkách s malou nebo žádnou infrastrukturou serveru. Role distribučního bodu podporuje klientské operační systémy, ale nemůže být povolená pomocí technologie PXE, protože je závislá na službě pro nasazení systému Windows.

Nová nastavení klienta jsou nyní k dispozici pro povolení služby respondéru PXE na Configuration Manager klienty. Spouštěcí image s povoleným PXE se musí nacházet v mezipaměti klienta respondérů PXE.

### <a name="try-it-out"></a>Určitě to udělejte!
Zajistěte, aby v testovacím prostředí neexistovaly žádné distribuční body s povoleným PXE nebo jiné servery PXE, které mohou být v konfliktu s tímto klientským respondérem PXE.

V konzole Configuration Manager:
1. V pracovním prostoru **softwarová knihovna** v části **operační systémy** **pořadí úloh**: Vytvořte pořadí úkolů pomocí vlastní šablony.
   1. Klikněte na tlačítko **Přidat**, vyberte možnost **Obecné**a potom krok **nastavit proměnnou pořadí úkolů** . Jako proměnnou pořadí úkolů zadejte **proměnné SMSTSPersistContent** a zadejte hodnotu **true**.
   1. Klikněte na tlačítko **Přidat**, vyberte možnost **software**a pak krok **Stáhnout obsah balíčku** . Klikněte na zlato hvězdičku a pak vyberte spouštěcí bitovou kopii s povoleným PXE. Zahrňte spouštěcí bitové kopie x86 i x64. Nakonfigurujte krok, který umístí do **mezipaměti klienta Configuration Manager**.
   1. Klikněte na tlačítko **Přidat**, vyberte možnost **Obecné**a potom krok **nastavit proměnnou pořadí úkolů** . Jako proměnnou pořadí úkolů zadejte **SMSTSPreserveContent** a zadejte hodnotu **true**.
2. V pracovním prostoru **Správa** v části **nastavení klienta**: vytvořit vlastní zásadu nastavení klientského zařízení.
   1. Vyberte skupinu **nastavení mezipaměti klienta** .
   1. Nastavte nastavení **Povolit klientům Configuration Manager v úplném operačním systému na** **hodnotu Ano**.
   1. Nastavte možnost **Povolit službu respondér technologie PXE** na **Ano**.
   1. V části **vytvořit certifikát podepsaný svým držitelem nebo importovat nastavení klientského certifikátu PKI** klikněte na **zadat certifikát**. Vyberte možnost **importovat certifikát** , pokud vaše testovací prostředí má PKI, jinak kliknutím na tlačítko **OK** vytvořte certifikát podepsaný svým držitelem. 
   1. Nakonfigurujte zbývající nastavení podle potřeby pro vaše testovací prostředí. (Výchozí nastavení by měla fungovat, pokud neexistují konkrétní požadavky na síť nebo zabezpečení.)
3. Nasaďte pořadí úkolů a vlastní nastavení klienta do kolekce cílových klientů, kteří budou odpovídat na nástroje PXE. Počkejte, než se zásady použijí a spustí se pořadí úkolů.
4. Spusťte jiného klienta ve stejné podsíti, aby se spouštěla technologie PXE/síť jako normální.

### <a name="known-issues"></a>Známé problémy
- Editor pořadí úloh zobrazí červenou ikonu chyby pro krok **Stáhnout obsah balíčku** , když přidáte spouštěcí bitovou kopii, ale pořadí úkolů se úspěšně uloží. Po opětovném otevření tohoto pořadí úloh v editoru se zobrazí také upozornění na neškodné, že se odkazované objekty nenašly. <!-- sms427542 -->
- Spouštěcí bitová kopie z kroku stáhnout obsah balíčku se nezobrazuje v seznamu odkazů vlastního pořadí úkolů. I akce **distribuovat obsah** není k dispozici. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Změna v instalaci klienta Configuration Manager  
V důsledku zpětné vazby vašeho uživatelského hlasu [už nebude program Silverlight na klientech automaticky nainstalován.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Změnit na řídicí panel zařízení Surface
Řídicí panel Surface teď namísto verze operačního systému zobrazuje verze firmwaru pro zařízení Surface. V konzole nástroje přejdete na **monitorování** > **Surface zařízení**. Můžete zobrazit následující položky:
- Procento povrchů
- Procento modelů Surface
- Pět hlavních verzí firmwaru
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Vylepšení řídicího panelu pro správu klientů Office 365 
Řídicí panel pro správu klientů Office 365 teď po výběru oddílů grafů zobrazuje seznam relevantních zařízení. V konzole nástroje přejdete na >**Přehled** > **knihovny softwaru****Office 365 Správa klientů**. Řídicí panel se zobrazí na pravé straně. Výběrem kritérií z grafu se zobrazí seznam zařízení.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Vylepšení konzoly Configuration Manager 
Provedli jsme následující vylepšení Configuration Manager konzole, což bylo výsledkem zpětné vazby uživatele na hlas.

- [Seznam zařízení zobrazuje primárního uživatele](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): seznamy zařízení v části prostředky a kompatibilita, zařízení: ve výchozím nastavení se teď zobrazuje primární uživatel. Poslední přihlášený uživatel může být také přidán jako volitelný sloupec. <!-- 1357280 -->
- Počet [přejmenovaných zobrazení kolekcí v existujících pravidlech členství kolekce](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Pokud je kolekce členem jiné kolekce a je přejmenována, nový název se aktualizuje v souladu s pravidly členství.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Vylepšení nasazení operačního systému
Pro nasazení operačního systému jsme provedli následující vylepšení, z nichž některé byly výsledkem zpětné vazby uživatele na hlas.
- [Výchozí prohlížeč protokolů ve spouštěcí imagi](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): při spuštění CMTrace. exe se již nezobrazuje výzva k výběru, zda má být program nastaven jako výchozí prohlížeč pro soubory protokolu. <!-- SMS 500897 -->
- Krok stažení obsahu balíčku: do tohoto kroku pořadí úkolů teď můžete přidat spouštěcí bitové kopie.


## <a name="windows-10-feedback-hub-app-integration"></a>Integrace aplikace centra Feedback pro Windows 10

Máme nám zpětnou vazbu, takže teď umožňujeme zpětnou vazbu prostřednictvím integrované [aplikace centra pro názory](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) na Windows 10. Když **přidáte novou zpětnou vazbu**, nezapomeňte vybrat kategorii **Správa podniku** a pak vybrat jednu z následujících podkategorií:
- Klient nástroje Configuration Manager
- Konzola nástroje Configuration Manager
- Configuration Manager nasazení operačního systému
- Server Configuration Manager

Pokračujte v používání naší [uživatelské hlasové stránky](https://configurationmanager.uservoice.com/) a Hlasujte na nových nápadech funkcí v Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
