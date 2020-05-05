---
title: Nová verze 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1710 Configuration Manager.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073615"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1710 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1710 pro Configuration Manager aktuální větev je k dispozici jako aktualizace konzoly pro dříve nainstalované lokality, na kterých běží verze 1610, 1702 nebo 1706.

Kromě nových funkcí obsahuje tato verze také další změny, jako jsou opravy chyb. Další informace najdete v tématu [Souhrn změn v Configuration Manager aktuální větvi, verze 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Nyní jsou k dispozici i následující další aktualizace této verze:
- [Kumulativní aktualizace pro Configuration Manager aktuální větev verze 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Kumulativní aktualizace 2 pro Configuration Manager aktuální větev verze 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, je nutné použít základní verzi Configuration Manager.  
>
> Další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1710 Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktura webu

### <a name="updates-for-peer-cache-----sms500850---"></a>Aktualizace pro sdílenou mezipaměť  <!-- sms500850 -->
Od této verze už není sdílená mezipaměť součástí předběžné verze.  V této verzi se nezavádí žádné další změny pro sdílenou mezipaměť. Další informace najdete v tématu sdílená [mezipaměť pro klienty Configuration Manager](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Podpora distribučního bodu cloudu pro Azure Government Cloud   <!-- sms491428 -->
Nyní můžete používat [cloudové distribuční body](../hierarchy/use-a-cloud-based-distribution-point.md) v cloudu Azure Government.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Výchozí revize jednotky inventáře <!-- sms503697 -->
Zařízení teď obsahují pevné disky s velikostmi v gigabajtech (GB), terabajtech (TB) a větší škálě. Tato verze mění výchozí jednotku (SMS_Units) použitou v mnoha zobrazeních z megabajtů (MB) až GB. Například hodnota v_gs_LogicalDisk. FreeSpace nyní hlásí GB jednotek.


<!-- ## Migration  -->


## <a name="client-management"></a>Správa klientů

### <a name="co-management-for-windows-10-devices"></a>Spoluspráva pro zařízení s Windows 10    
<!-- 1350871 -->
V předchozích aktualizacích Windows 10 už můžete připojit zařízení s Windows 10 k místní službě Active Directory (AD) a cloudovou službu Azure AD ve stejnou dobu (hybridní služba Azure AD). Configuration Manager počínaje verzí 1710 používá spoluspráva výhod tohoto vylepšení a umožňuje souběžně spravovat Windows 10, verze 1709 (označované také jako aktualizace pro povýšení tvůrci) pomocí Configuration Manager a Intune. Jedná se o řešení, které poskytuje přechod z tradičního na moderní správu a poskytuje cestu k převedení pomocí dvoufázového přístupu. Podrobnosti najdete v tématu [společná správa pro zařízení s Windows 10](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Restartování počítačů z konzoly Configuration Manager  <!-- 1356283 -->
Od této verze můžete použít konzolu Configuration Manager k identifikaci klientských zařízení, která vyžadují restart, a pak použít akci klientského oznámení k jejich restartování.

Viz [Správa klientů](../../clients/manage/manage-clients.md#restart-clients) .


<!-- ## Compliance settings -->


## <a name="application-management"></a>Správa aplikací
### <a name="improvements-for-run-scripts------1236459---"></a>Vylepšení skriptů pro spuštění   <!-- 1236459 -->
Tato verze přináší několik vylepšení funkce **spustit skripty** , která umožňuje nasazení skriptů PowerShellu pro spouštění na spravovaných zařízeních. Tato funkce byla poprvé představena ve verzi 1706.

Mezi vylepšení patří:
- Použijte obory zabezpečení, které vám pomůžou řídit, kdo může používat skripty pro spouštění.
- Sledování skriptů, které spouštíte v reálném čase
- Parametry pro zobrazení skriptu v Průvodci vytvořením skriptu, ověřování podpory a jsou označeny jako povinné nebo volitelné.

Další informace o používání skriptů pro spouštění najdete v tématu [vytváření a spouštění skriptů](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nová nastavení zásad správy mobilních aplikací
<!-- 1324760 -->
Do nastavení zásad správy mobilní aplikace byla přidána následující nastavení:
- **Zakázat synchronizaci kontaktů**: znemožní aplikaci ukládat data do nativní aplikace kontakty na zařízení.
- **Zakázat tisk**: aplikace brání v tisku pracovních nebo školních dat.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centrum softwaru už nedeformovaný ikony větší než 250x250  
<!-- 1356194 -->

V této verzi přestane Centrum softwaru derušit ikony, které jsou větší než 250x250. Centrum softwaru tyto ikony vypadá rozmazaně. Nyní můžete nastavit ikonu s rozměry v pixelech až na 512x512 a ta se zobrazí bez zkreslení.

Chcete-li přidat ikonu pro aplikaci v centru softwaru, přečtěte si téma [Vytvoření aplikací](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>Nasazení operačního systému
 > [!TIP]   
 > <!-- 1354281 -->
 > Od verze 1709 Windows 10 (označované také jako aktualizace pro povýšení tvůrci) obsahuje Windows Media několik edicí. Při konfiguraci pořadí úkolů pro použití balíčku s upgradem operačního systému nebo bitové kopie operačního systému nezapomeňte vybrat [edici, která je podporována pro použití v Configuration Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Přidání podřízených sekvencí úloh do pořadí úkolů
<!-- 1261338 -->

Můžete přidat nový krok pořadí úloh, který spustí jiné pořadí úkolů, které vytvoří vztah nadřazenosti/podřízenosti mezi pořadím úkolů. To vám umožní vytvořit další modulární pořadí úloh, která můžete znovu použít.  

Další informace o podřízeném pořadí úkolů najdete v tématu [Podřízená sekvence úloh](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Přizpůsobení centra softwaru
<!-- 1351224 -->
Můžete přidat prvky firemního brandingu a zadat viditelnost karet v centru softwaru. Můžete přidat název vaší společnosti v centru softwaru, nastavit motiv barvy konfigurace centra softwaru, nastavit logo společnosti a nastavit viditelné karty pro klientská zařízení.

Další informace najdete v tématu [plánování a konfigurace správy aplikací](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="surface-driver-updates-----1098490---"></a>Aktualizace ovladačů Surface  <!-- 1098490 -->
Od této verze už není k dispozici funkce pro správu aktualizací ovladačů Surface.  


## <a name="reporting"></a>Generování sestav

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Omezit rozšířená data Windows 10 tak, aby odesílala jenom data relevantní pro Windows Analytics Stav zařízení
<!-- 1356148 -->

Teď můžete nastavit úroveň shromažďování diagnostických dat Windows 10 na hodnotu **Rozšířené (s omezením)**. Toto nastavení umožňuje získat užitečné informace o zařízeních ve vašem prostředí bez toho, aby zařízení nahlásí všechna data v **Rozšířené** úrovni s Windows 10 verze 1709 nebo novější.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Správa mobilních zařízení

### <a name="actions-for-non-compliance"></a>Akce při nedodržení předpisů 
<!--1321366 -->    
Teď můžete nakonfigurovat časově řazenou posloupnost akcí, které se aplikují na zařízení, která nedodržují předpisy. Například můžete uživatelům zařízení, která nedodržují předpisy, upozorňovat pomocí e-mailu nebo označit zařízení jako nevyhovující předpisům.

### <a name="windows-10-arm64-device-support"></a>Podpora zařízení s Windows 10 ARM64
<!-- 1355000 -->

Hybridní scénáře správy mobilních zařízení (MDM) se budou podporovat na zařízeních ARM64 s Windows 10, když jsou tato zařízení k dispozici.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Vylepšené možnosti profilů VPN v konzole Configuration Manager 
<!-- 1318232 -->

V této verzi jsme aktualizovali Průvodce profilem sítě VPN a stránky vlastností, aby se zobrazila nastavení vhodná pro vybranou platformu:


- Každá platforma má svůj vlastní pracovní postup, což znamená, že nové profily sítě VPN obsahují pouze nastavení podporovaná platformou.
- Stránka **podporované platformy** se teď zobrazí po stránce **Obecné** .  Nyní si zvolíte platformu před nastavením hodnot vlastností.
- Když je platforma nastavená na **Android**, **Android for Work**nebo **Windows Phone 8,1**, stránka **podporované platformy** není potřeba a není zobrazená.
- Configuration Manager pracovní postup založený na klientech se spojil s pracovními postupy Windows 10 na základě klientů hybridního mobilního zařízení (MDM). podporují stejné nastavení.
- Každý pracovní postup platformy obsahuje jenom nastavení vhodná pro tento pracovní postup.  Například pracovní postup Androidu obsahuje nastavení vhodná pro Android. nastavení vhodná pro iOS nebo Windows 10 Mobile se už nezobrazí v pracovním postupu Android.
- Stránka automatické sítě VPN je zastaralá a byla odebrána.

Tyto změny platí pro nové profily sítě VPN.  

Kvůli minimalizaci rizika kompatibility se stávající profily sítě VPN nezměnily.  Když upravujete existující profil, nastavení se zobrazí stejně jako při vytvoření profilu.  

Další informace najdete v tématu [Profily sítě VPN na mobilních zařízeních](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Omezená podpora pro certifikáty Cryptography: Next Generation (CNG) <!-- 1356191 -->

Configuration Manager má omezené podpory pro certifikáty Cryptography: Next Generation (CNG). Klienti služby Configuration Manager můžou používat certifikát ověřování klientů PKI s privátním klíčem v CNG (klíč úložiště klíčů). S podporou KSP Configuration Manager klienti podporují privátní klíč založený na hardwaru, jako je například KSP čipu TPM pro certifikáty ověřování klientů PKI.

Další informace najdete v tématu [Přehled certifikátů CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Ochrana zařízení

### <a name="create-and-deploy-exploit-guard-policies"></a>Vytvoření a nasazení zásad ochrany před zneužitím
<!-- 1355468 -->

Můžete [vytvořit a nasadit zásady](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) , které spravují všechny čtyři součásti ochrany před zneužitím v programu Windows Defender, včetně omezení plochy pro útoky, řízeného přístupu ke složkám, ochrany před zneužitím a ochrany sítě.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Vytvoření a nasazení zásad ochrany Application Guard v programu Windows Defender
<!-- 1351960 -->

Zásady ochrany [Application Guard v programu Windows Defender můžete vytvořit a nasadit](../../../protect/deploy-use/create-deploy-application-guard-policy.md) pomocí Configuration Manager Endpoint Protection.

### <a name="device-guard-policy-changes"></a>Změny zásad Device Guard
<!-- 1355092 -->
Ve vztahu k zásadám ochrany zařízení byly provedeny následující tři změny:

- Zásady ochrany zařízení se přejmenovaly na zásady řízení aplikací v programu Windows Defender. Například **Průvodce vytvořením zásad pro ochranu zařízení** se teď jmenuje **Průvodce vytvořením zásad řízení aplikací v programu Windows Defender**.
- Zařízení, která používají aktualizaci Creators Update pro Windows verze 1709, nevyžadují restart, aby bylo možné použít zásady řízení aplikací v programu Windows Defender. Restart je stále výchozí, ale [můžete ho vypnout.](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
- Zařízení můžete [nastavit tak, aby automaticky spouštěla software, který](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) je důvěryhodný pro Intelligent Security Graph.





## <a name="next-steps"></a>Další kroky
Až budete připraveni k instalaci této verze, přečtěte si téma [aktualizace pro Configuration Manager](../../servers/manage/updates.md).
