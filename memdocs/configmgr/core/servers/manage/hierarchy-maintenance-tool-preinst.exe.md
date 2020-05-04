---
title: Nástroj Údržba hierarchie
titleSuffix: Configuration Manager
description: Zjistěte, co dělá Nástroj Hierarchy Maintenance a proč ho můžete použít. Obsahuje odkaz na možnosti příkazového řádku.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712439"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Nástroj Údržba hierarchie (Preinst. exe) pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nástroj Hierarchy Maintenance (Preinst. exe) předá příkazy do Správce hierarchie Configuration Manager, když je spuštěná služba Hierarchy Manager. Nástroj Hierarchy Maintenance se automaticky nainstaluje při instalaci lokality Configuration Manager. Preinst. exe najdete ve \\ &lt;složce *SiteServerName*> \ SMS_&lt;*SiteCode*\bin\X64\00000409 Shared na serveru lokality.  

 Nástroj Hierarchy Maintenance můžete použít v následujících scénářích:  

-   Pokud je požadována zabezpečená výměna klíčů, v některých případech je nutné ručně provést počáteční výměnu veřejných klíčů mezi lokalitami. Další informace najdete v části [Ruční výměna veřejných klíčů mezi lokalitami](#BKMK_ManuallyExchangeKeys) tohoto tématu.  

-   Odebrání aktivních úloh souvisejících s cílovou lokalitou, která již není dostupná.  

-   Odstranění serveru lokality z konzoly Configuration Manager, když nemůžete odinstalovat lokalitu pomocí instalačního programu. Pokud například fyzicky odeberete Configuration Manager lokalitu, aniž byste nejprve spustili instalační program pro odinstalaci lokality, informace o lokalitě stále existují v databázi nadřazené lokality a Nadřazená lokalita se bude dále pokoušet o komunikaci s podřízenou lokalitou. Chcete-li tento problém vyřešit, je nutné spustit Nástroj Hierarchy Maintenance a ručně odstranit podřízenou lokalitu z databáze nadřazené lokality.  

-   Zastavení všech služeb Configuration Manager Services v lokalitě, aniž by bylo nutné jednotlivé služby zastavit.  

-   Pokud obnovujete lokalitu, můžete pomocí možnosti CHILDKEYS distribuovat veřejné klíče z více podřízených lokalit do obnovované lokality.  

Chcete-li spustit nástroj Hierarchy Maintenance, musí mít aktuální uživatel oprávnění správce v místním počítači. Uživatel musí také výslovně mít bezpečnostní oprávnění ke správě lokality. Převzetí tohoto práva uživatelem na základě jeho členství ve skupině s oprávněním není dostačující.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Možnosti příkazového řádku nástroje Hierarchy Maintenance  
Pokud použijete nástroj Hierarchy Maintenance, je nutné jej spustit místně v lokalitě centrální správy, v primární lokalitě nebo na serveru sekundární lokality.  

Když spustíte Nástroj Hierarchy Maintenance, je nutné použít následující syntaxi: Preinst. exe/&lt;Option.\> Dál jsou uvedené možnosti příkazového řádku.  

 **> /DELJOB &lt; *SiteCode* ** – pomocí této možnosti v lokalitě odstraníte všechny úlohy nebo příkazy z aktuální lokality do určené cílové lokality.  

 **> /DELSITE &lt; *ChildSiteCodeToRemove* ** – pomocí této možnosti v nadřazené lokalitě odstraníte data podřízených lokalit z databáze nadřazené lokality. Tuto možnost obvykle použijete, pokud dojde k deaktivaci počítače serveru lokality před odinstalováním lokality z tohoto počítače.  

> [!NOTE]  
>  Možnost /DELSITE neodinstaluje lokalitu v počítači, která je určena parametrem KódPodřízenéLokalityKodstranění. Tato možnost pouze odebere informace o lokalitě z databáze lokality Configuration Manager.  

**> /Dump &lt; *SiteCode* ** – pomocí této možnosti na serveru místní lokality zapíšete řídicí image lokality do kořenové složky jednotky, na které je lokalita nainstalována. Můžete zapsat určitou řídicí bitovou kopii lokality do složky nebo můžete zapsat všechny řídicí soubory lokality v hierarchii.  

-   /DUMP &lt; *SiteCode*> zapisuje řídicí bitovou kopii lokality pouze pro určenou lokalitu.  

-   /DUMP zapíše řídicí soubory lokality pro všechny lokality.  

Obrázek je binární reprezentace řídicího souboru lokality, která je uložena v databázi lokality Configuration Manager. Vypsaná bitová kopie řidicího souboru lokality je souhrn základní bitové kopie a čekajících rozdílových bitových kopií.  

Po vypsání bitové kopie řídicího souboru lokality pomocí nástroje Hierarchy Maintenance je název souboru ve formátu sitectrl_&lt;*SiteCode*>. CT0.  

**/STOPSITE** – pomocí této možnosti na serveru místní lokality zahájíte cyklus vypnutí služby Configuration Manager správce součástí lokality, která částečně resetuje lokalitu. Po spuštění tohoto cyklu vypnutí se zastaví některé Configuration Manager služby na serveru lokality a ve svých vzdálených systémech lokality. Tyto služby jsou označeny k přeinstalování. Výsledkem tohoto cyklu vypnutí je automatická změna některých hesel během přeinstalování služeb.  

> [!NOTE]  
>  Pokud chcete zobrazit záznam vypnutí, přeinstalování a změn hesel ve službě Site Component Manager, před použitím této možnosti příkazového řádku povolte protokolování této součásti.  

Cyklus vypnutí pokračuje po spuštění automaticky a přeskočí jakékoli neodpovídající součásti nebo počítače. Pokud však služba Site Component Manager nemůže během cyklu vypnutí získat přístup ke vzdálenému systému lokality, v případě restartování služby Site Component Manager jsou přeinstalovány součásti nainstalované ve vzdáleném systému lokality. Pokud je služba Site Component Manager restartována, pokusí se opakovaně o přeinstalování všech služeb označených k přeinstalování, dokud akce neproběhne úspěšně.  

Službu Site Component Manager lze restartovat pomocí nástroje Service Manager. Po restartování služby se odinstalují, přeinstalují a restartují všechny ovlivněné služby. Po použití možnosti /STOPSITE k zahájení cyklu vypnutí se nelze vyhnout cyklům přeinstalování po restartování služby Site Component Manager.  

**/KEYFORPARENT** – Tato možnost v lokalitě slouží k distribuci veřejného klíče lokality do nadřazené lokality.  

Možnost/keyforparent umístí veřejný klíč lokality do souboru &lt; *SiteCode*>. CT4 v kořenové složce jednotky souborů programu. Po spuštění Preinst. exe s touto možností ručně zkopírujte &lt;> *SiteCode* . CT4 soubor do složky. ..\Inboxes\hman.Box nadřazené lokality (ne hman. box\pubkey).  

**/KEYFORCHILD** – Tato možnost v lokalitě slouží k distribuci veřejného klíče lokality do podřízené lokality.  

Možnost/keyforchild umístí veřejný klíč lokality do souboru &lt; *SiteCode*>. CT5 v kořenové složce jednotky souborů programu. Po spuštění Preinst. exe s touto možností ručně zkopírujte &lt;> *SiteCode* . CT5 soubor do složky. ..\Inboxes\hman.Box podřízené lokality (ne hman. box\pubkey).  

**/CHILDKEYS** – Tuto možnost je možné použít v podřízených lokalitách obnovované lokality. Tato možnost slouží k distribuci veřejných klíčů z více podřízených lokalit do obnovované lokality.  

Možnost/CHILDKEYS umístí klíč z lokality, ve které je spuštěna možnost, a všechny veřejné klíče podřízené lokality do souboru &lt; *SiteCode*>. CT6.  

Po spuštění Preinst. exe s touto možností ručně zkopírujte &lt;> *SiteCode* . CT6 soubor do složky. ..\Inboxes\hman.Box lokality pro obnovování (ne hman. box\pubkey).  

**/PARENTKEYS** – Tuto možnost můžete použít v nadřazené lokalitě obnovované lokality. Tato možnost slouží k distribuci veřejných klíčů ze všech nadřazených lokalit do obnovované lokality.  

Možnost/PARENTKEYS umístí klíč z lokality, ve které je spuštěná možnost, a klíče z každé nadřazené lokality nad touto lokalitou do souboru &lt;SiteCode.\> CT7.  

Po spuštění Preinst. exe s touto možností ručně zkopírujte &lt;> *SiteCode* . CT7 soubor do složky. ..\Inboxes\hman.Box lokality pro obnovování (ne hman. box\pubkey).  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a>Ruční výměna veřejných klíčů mezi lokalitami  
Ve výchozím nastavení je pro Configuration Manager weby povolena možnost **vyžadovat zabezpečenou výměnu klíčů** . Pokud je požadována zabezpečená výměna klíčů, ve dvou případech je nutné ručně provést počáteční výměnu klíčů mezi lokalitami:  

-   Pokud nebylo schéma služby Active Directory rozšířeno pro Configuration Manager  

-   Lokality Configuration Manager nepublikují data lokality ve službě Active Directory  

K exportování veřejných klíčů pro každou lokalitu lze použít nástroj Hierarchy Maintenance. Jakmile budou klíče exportovány, je nutné je ručně vyměnit mezi lokalitami.  

> [!NOTE]  
>  Po ruční výměně veřejných klíčů můžete na serveru nadřazené lokality zkontrolovat soubor protokolu **hman.log**, který obsahuje záznam změn konfigurace lokality a publikování informací o lokalitě ve službě Active Directory Domain Services, čímž se ujistíte, že primární lokalita zpracovala nový veřejný klíč.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Ruční přenos veřejného klíče podřízené lokality do nadřazené lokality  

1.  Během přihlášení k podřízené lokalitě otevřete příkazový řádek a přejděte do umístění souboru **Preinst.exe**.  

2.  Pro export veřejného klíče podřízené lokality zadejte následující text: **Preinst/keyforparent**  

3.  Možnost/keyforparent umístí veřejný klíč podřízené lokality do ** &lt;\>kódu lokality. CT4** soubor umístěný v kořenovém adresáři systémového disku.  

4.  Přesuňte ** &lt;\>kód lokality. CT4** soubor do složky ** &lt;\Inboxes\hman.Box instalačního adresáře\>** nadřazené lokality.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Ruční přenos veřejného klíče nadřazené lokality do podřízené lokality  

1.  Během přihlášení k nadřazené lokalitě otevřete příkazový řádek a přejděte do umístění souboru **Preinst.exe**.  

2.  Pro export veřejného klíče nadřazené lokality zadejte následující text: **Preinst/keyforchild**.  

3.  Možnost/keyforchild umístí veřejný klíč nadřazené lokality do ** &lt;\>kódu lokality. CT5** soubor umístěný v kořenovém adresáři systémového disku.  

4.  Přesuňte ** &lt;\>kód lokality. CT5** soubor do adresáře ** &lt;instalačního\>adresáře \Inboxes\hman.Box** v podřízené lokalitě.  
