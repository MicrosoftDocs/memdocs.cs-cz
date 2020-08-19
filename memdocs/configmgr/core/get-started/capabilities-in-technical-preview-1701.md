---
title: Možnosti ve verzi Technical Preview 1701
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 20c560925b2c1abec282b8c5f8dae3f6f42f4d64
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591201"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1701 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*



V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1701. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Vylepšení skupin hranic pro body aktualizace softwaru
Od této verze Preview teď k přidružení klientů k bodům aktualizace softwaru používáte skupiny hranic. Tato součást pokračuje v práci a rozbalí změny pro skupiny hranic za účelem správy dalších rolí systému lokality.  Změny skupin hranic byly nejprve představeny v Technical Preview 1609 a Current Branch ve verzi 1610.  

V této verzi Preview použijete nové chování hraniční skupiny pro správu, které body aktualizace softwaru může klient používat, podobně jako při správě, který distribučního bodu může klient použít:  

- Skupiny hranic konfigurujete k přidružení jednoho nebo více serverů, které jsou hostiteli bodu aktualizace softwaru.
- Klienti, kteří hledají nový bod aktualizace softwaru, se pokusí použít jeden, který je spojený s aktuální skupinou hranic.
- Pokud se klientovi nepodaří získat přístup k aktuálnímu bodu aktualizace softwaru a nemůže najít jeden z aktuálních hraničních skupin, klient použije záložní chování k rozšíření dostupného fondu bodů aktualizace softwaru, které může použít.    

Další informace o skupinách hranic najdete v tématu [skupiny hranic](../servers/deploy/configure/boundary-groups.md) v obsahu pro Current Branch.

V této verzi Preview však skupiny hranic pro body aktualizace softwaru jsou pouze částečně implementovány. Můžete přidat body aktualizace softwaru a nakonfigurovat sousední skupiny hranic, které obsahují body aktualizace softwaru, ale záložní čas pro body aktualizace softwaru ještě není podporován a klienti budou čekat dvě hodiny před zahájením zálohy.

Následující článek popisuje chování bodů aktualizace softwaru s touto verzí Technical Preview:  

- **Noví klienti používají skupiny hranic k výběru bodů aktualizace softwaru,** Klient, který nainstalujete po instalaci verze 1701, vybere bod aktualizace softwaru z těch, které jsou přidružené ke skupině hranic klienta.

  Tím se nahradí předchozí chování, kde klienti vyberou bod aktualizace softwaru náhodně ze seznamu těch, které sdílejí doménovou strukturu klientů.   

- **Dřív nainstalovaní klienti nadále používají svůj aktuální bod aktualizace softwaru, dokud nebudou moct najít nový.**
  Klienti, kteří byli dříve nainstalováni a již mají bod aktualizace softwaru, budou nadále používat tento bod aktualizace softwaru, dokud nebudou záložní. To zahrnuje body aktualizace softwaru, které nejsou přidružené k aktuální skupině hranic klienta. Nepokouší se hned najít a použít bod aktualizace softwaru z aktuální skupiny hranic.

  Klient, který už má bod aktualizace softwaru, začne používat tuto novou skupinu hranic jenom poté, co se klientovi nepovede přejít na svůj aktuální bod aktualizace softwaru a spustí se Fallback.
  Toto zpoždění při přepínání na nové chování je záměrné. Důvodem je to, že změna bodu aktualizace softwaru může vést k velkému využití šířky pásma sítě, protože klient synchronizuje data s novým bodem aktualizace softwaru. Zpoždění při přechodu může přispět k tomu, aby se zabránilo sytost vaší sítě, aby všichni klienti přešli na nové body aktualizace softwaru současně.

- **Konfigurace pro záložní čas:** V této verzi Technical Preview se nepodporují konfigurace, kdy klienti spouštějí v režimu Fallback pro hledání nového bodu aktualizace softwaru. To zahrnuje konfigurace pro **záložní časy (v minutách)** a **nikdy**nezálohované, které můžete nakonfigurovat pro různé vztahy skupin hranic.

  Místo toho klienti uchovávají své aktuální chování, když se klient pokusí připojit ke svému aktuálnímu bodu aktualizace softwaru po dobu dvou hodin před jeho zahájením, aby našel nový bod aktualizace softwaru, který může použít.

  Když klient použije zálohu, použije konfigurace hraničních skupin pro záložní sadu k vytvoření fondu dostupných bodů aktualizace softwaru. Tento fond zahrnuje všechny body aktualizace softwaru z *aktuální skupiny hranic*klientů, *hraničních skupin hranic*a *výchozí skupiny hranic lokality*klientů.

- **Nakonfigurujte výchozí skupinu hranic lokality:**  
  Zvažte přidání bodu aktualizace softwaru do *lokality default-site-hranice-Group &lt;>*. Tím je zajištěno, že klienti, kteří nejsou členy jiné skupiny hranic, mohou být pro vyhledání bodu aktualizace softwaru zárukou.


Chcete-li spravovat body aktualizace softwaru pro skupiny hranic, použijte [postupy z dokumentace Current Branch](../servers/deploy/configure/boundary-group-procedures.md), ale mějte na paměti, že pro body aktualizace softwaru se zatím nepoužívají záložní časy, které byste mohli nakonfigurovat.


## <a name="hardware-inventory-collects-uefi-information"></a>Inventář hardwaru shromažďuje informace o rozhraní UEFI.
K dispozici je nová třída inventáře hardwaru (**SMS_Firmware**) a vlastnost (**UEFI**), která vám pomůže určit, jestli se počítač spustí v režimu UEFI. Pokud je počítač spuštěn v režimu UEFI, vlastnost **UEFI** je nastavena na **hodnotu true**. Tato možnost je ve výchozím nastavení povolená v inventáři hardwaru. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="improvements-to-operating-system-deployment"></a>Vylepšení nasazení operačního systému
Provedli jsme následující vylepšení nasazení operačního systému, mnohé z nich byly výsledkem vašich názorů na hlas uživatele.
- [**Podpora dalších aplikací pro krok pořadí úkolů instalovat aplikace**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): zvýšili jsme maximální počet aplikací, které můžete nainstalovat do 99 v kroku pořadí úkolů **instalovat aplikace** . Předchozí maximální počet aplikací byl 9.
- [**V kroku pořadí úkolů instalovat aplikaci vyberte více aplikací**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Když přidáte aplikace do kroku pořadí úkolů instalovat aplikaci v editoru pořadí úkolů, můžete teď v podokně **Vybrat aplikaci pro instalaci** vybrat více aplikací.
- [**Konec platnosti samostatného**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media)média: při vytváření samostatných médií jsou k dispozici nové možnosti pro nastavení volitelných dat začátku a konce platnosti média. Tato nastavení jsou ve výchozím nastavení zakázaná. Data jsou porovnána se systémovým časem v počítači před spuštěním samostatného média. Pokud je systémový čas dřívější než čas spuštění nebo pozdější než čas vypršení platnosti, nebude samostatné médium spuštěno. Tyto možnosti jsou dostupné taky pomocí rutiny New-CMStandaloneMedia prostředí PowerShell.
- [**Podpora dalšího obsahu v samostatném médiu**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): na samostatném médiu se teď podporuje další obsah. Můžete vybrat další balíčky, balíčky ovladačů a aplikace, které mají být připravené na médiu, spolu s dalším obsahem, na který je odkazováno v pořadí úkolů. Dříve byl na samostatném médiu připraven pouze obsah odkazovaný v pořadí úkolů.
- [**Konfigurovatelný časový limit pro krok pořadí úkolů pro automatické použití ovladače**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): nové proměnné pořadí úkolů jsou nyní k dispozici ke konfiguraci hodnoty Timeout v kroku pořadí úkolů automaticky použít ovladač při vytváření požadavků katalogu http. K dispozici jsou následující proměnné a výchozí hodnoty (v sekundách):
   - SMSTSDriverRequestResolveTimeOut výchozí: 60
   - SMSTSDriverRequestConnectTimeOut výchozí: 60
   - SMSTSDriverRequestSendTimeOut výchozí: 60
   - SMSTSDriverRequestReceiveTimeOut výchozí: 480
- [**ID balíčku se teď zobrazuje v krocích pořadí úloh: v**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste)kroku pořadí úkolů, který odkazuje na balíček, balíček ovladačů, image operačního systému, spouštěcí image nebo balíček s upgradem operačního systému, se teď zobrazí ID odkazovaného objektu. Když krok pořadí úkolů odkazuje na aplikaci, zobrazí se ID objektu.
- **Windows 10 ADK sledovaných verzí buildu**: Windows 10 ADK je teď sledován verzí buildu, aby se zajistilo více podporované prostředí při přizpůsobení spouštěcích imagí s Windows 10. Pokud například lokalita používá Windows ADK pro Windows 10 verze 1607, můžete v konzole přizpůsobit jenom spouštěcí image s verzí 10.0.14393. Podrobnosti o přizpůsobení verzí prostředí WinPE najdete v tématu [Přizpůsobení spouštěcích bitových kopií](../../osd/get-started/customize-boot-images.md).
- **Výchozí cestu ke zdroji spouštěcí bitové kopie již nelze změnit**: výchozí spouštěcí bitové kopie jsou spravovány Configuration Manager a výchozí cestu ke zdroji spouštěcí bitové kopie již nelze změnit v konzole Configuration Manager nebo pomocí sady Configuration Manager SDK. Můžete pokračovat v konfiguraci vlastní zdrojové cesty pro vlastní spouštěcí image.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Hostování aktualizací softwaru v cloudových distribučních bodech
Od této verze Preview můžete k hostování balíčku aktualizace softwaru použít cloudový distribuční bod. Vzhledem k tomu, že je možné nakonfigurovat klienty ke stahování aktualizací softwaru přímo z Microsoft Update, zvažte další náklady, které mohou nasazovat balíček aktualizace softwaru do cloudového distribučního bodu.

Informace o použití cloudových distribučních bodů najdete v tématu [Použití cloudového distribučního bodu](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) v obsahu pro Current Branch Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Ověřit data ověření stavu zařízení přes body správy

Od této verze Preview můžete nakonfigurovat body správy pro ověření dat vytváření sestav ověření stavu pro cloudové nebo místní služby ověření stavu. Nová karta **Pokročilá nastavení** v dialogovém okně **Vlastnosti komponenty bodu správy** umožňuje **Přidat**, **Upravit**nebo **Odebrat** **adresu URL místní služby ověření stavu zařízení**. Můžete také zadat **vlastní nastavení zařízení** pro klientského agenta, aby bylo možné **použít místní službu ověření stavu**.  Nastavením **Ano** pro toto nastavení povolíte vytváření sestav pro místní bod správy místo cloudové služby.

### <a name="try-it-out"></a>Vyzkoušet

- **Povolit ověřování stavu místních zařízení v bodu správy**<br>  V konzole Configuration Manager přejděte do části bod správy a otevřete **Vlastnosti komponenty bodu správy** a potom klikněte na kartu **Upřesnit možnosti** . klikněte na **Přidat** a zadejte místní adresu URL (například https://10.10.10.10) pro **místní adresy URL služby ověření stavu zařízení**.
- **Povolit vytváření sestav ověření stavu místních bodů správy pro agenta klienta**<br>V konzole Configuration Manager vyberte možnost **Správa**  >  **nastavení klienta** a dvakrát klikněte nebo vytvořte nové **vlastní nastavení zařízení**. Vyberte **Počítačový agent** a nastavte **použít místní službu ověření stavu** na **Ano**. Pokud je **možnost povolit komunikaci se službou ověření stavu zařízení** nastavená na **hodnotu Ano** a **použít místní ověření stavu** je nastavené na **ne**, bod správy bude používat cloudovou službu ověření stavu zařízení.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Použití konektoru OMS pro Microsoft Azure Government Cloud
V této verzi Technical Preview se teď můžete pomocí konektoru Microsoft Operations Management Suite (OMS) připojit k pracovnímu prostoru OMS, který se nachází v Microsoft Azure Government cloudu.  

Provedete to tak, že upravíte konfigurační soubor tak, aby odkazoval na Cloud státní správy, a pak nainstalujete konektor OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Nastavení konektoru OMS pro Microsoft Azure Government Cloud
1. V jakémkoli počítači s nainstalovanou konzolou Configuration Manager upravte následující konfigurační soubor tak, aby odkazoval na Cloud pro státní správu: *** &lt; Instalační cesta CM # C0\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Úpravě**

   Změňte hodnotu parametru name *FairFaxArmResourceID* tak, aby se rovnala "<https://management.usgovcloudapi.net/">

   - **Původní:** &lt; nastavení Name = "FairFaxArmResourceId" serializeAs = "String" >   
     &lt;hodnota>&lt; /value>   
     &lt;/Setting>

   - **Změněna**     
     &lt;nastavení Name = "FairFaxArmResourceId" serializeAs = "String" > &lt; Value &gt; https://management.usgovcloudapi.net/&lt ;/Value&gt;  
     &lt;/Setting>

   Změňte hodnotu vlastnosti Name *FairFaxAuthorityResource* tak, aby byla rovna hodnotě " <https://login.microsoftonline.com/> ".

   - **Původní:** &lt; nastavení Name = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;hodnota>&lt; /value>

   - **Upraveno:** &lt; nastavení Name = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;hodnota &gt; [https://login.microsoftonline.com](https://login.microsoftonline.com) &lt; /Value&gt;

2. Po uložení souboru se dvěma změnami restartujte konzolu Configuration Manager na stejném počítači a pomocí této konzoly nainstalujte konektor OMS. Chcete-li nainstalovat konektor, použijte informace v části [synchronizovat data z Configuration Manager do Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)a vyberte **pracovní prostor Operations Management Suite** , který je v cloudu Microsoft Azure Government.

3. Po instalaci konektoru OMS je připojení ke cloudu pro státní správu dostupné, když použijete jakoukoli konzolu, která se připojuje k lokalitě nástroje.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Verze Androidu a iOS už nejsou cílené v průvodcích vytváření pro hybridní správu mobilních zařízení (MDM).

Počínaje v této verzi Technical Preview pro hybridní správu mobilních zařízení (MDM) už nemusíte při vytváření nových zásad a profilů pro zařízení spravovaná přes Intune cílit na konkrétní verze Androidu a iOS. Místo toho vyberte jeden z následujících typů zařízení:

- Android
- Samsung KNOX Standard 4,0 a vyšší
- iPhone
- iPad

Tato změna má vliv na průvodce vytvářením následujících položek:

- Položky konfigurace
- Compliance zásady
- Profily certifikátů
- E-mailové profily.
- Profily sítě VPN
- Profily sítě Wi-Fi

Díky této změně můžou hybridní nasazení poskytovat rychlejší podporu pro nové verze Androidu a iOS, aniž by bylo potřeba nové vydání Configuration Manager nebo rozšíření. Jakmile je nová verze v Intune samostatně podporovaná, uživatelé budou moct mobilní zařízení upgradovat na tuto verzi.

Aby se zabránilo problémům při upgradu z předchozích verzí Configuration Manager, jsou verze mobilního operačního systému stále k dispozici na stránkách vlastností pro tyto položky. Pokud stále potřebujete cílit na konkrétní verzi, můžete vytvořit novou položku a pak na stránce vlastností nově vytvořené položky zadat cílovou verzi.
