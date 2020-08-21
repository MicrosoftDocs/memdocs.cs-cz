---
title: Vytvoření položek konfigurace pro Windows 10
titleSuffix: Configuration Manager
description: Použijte položku Konfigurace Windows 10 ke správě nastavení pro počítače se systémem Windows 10, které jsou spravované klientem Configuration Manager.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9589b9e542c9d323ab7a23af169725c1a54bfb70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694759"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Vytváření položek konfigurace pro zařízení s Windows 10

Pomocí položky konfigurace Configuration Manager **Windows 10** můžete spravovat nastavení pro počítače s Windows 10, které jsou spravované klientem Configuration Manager.  
  
> [!IMPORTANT]  
>  Pokud jste v této verzi vytvořili nastavení **hesla** jako součást položky konfigurace typu **Windows 10** (pro zařízení spravované pomocí klienta Configuration Manager), uvědomte si následující problém. Pokud nastavení ještě neexistuje nebo není nakonfigurované na zařízení s Windows 10, vyhodnotí se jako vyhovující předpisům.  
>   
>  Tento problém můžete vyřešit tím, že se při vytvoření nastavení pro tato zařízení ujistíte, že je vybraná volba **Napravit neshodná nastavení** na stránkách nastavení průvodce vytvořením položky konfigurace. Pokud navíc nasadíte standardní hodnoty konfigurace obsahující položku Konfigurace Windows 10 s nastavením hesla, vyberte možnost **napravit pravidla nesplňující požadavky, pokud jsou podporovaná**. Tento výběr provedete v dialogovém okně nasadit standardní hodnoty konfigurace. Když použijete toto alternativní řešení, nastavení se monitoruje a napravuje se, pokud se zjistí, že nedodržuje předpisy. Po nápravě je nastavení správně hlášené jako **vyhovující** (Pokud se nevyskytne problém, v takovém případě se zpráva zobrazí **Chyba**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Vytvoření položky konfigurace Windows 10  
  
1. V konzole Configuration Manager vyberte **prostředky a kompatibilita**.  
  
2. V pracovním prostoru **prostředky a kompatibilita** rozbalte **Nastavení dodržování předpisů**a pak vyberte **položky konfigurace**.  
  
3. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit položku konfigurace**.  
  
4. Na stránce **Obecné** v průvodci **vytvořením položky konfigurace** zadejte název a volitelný popis položky konfigurace.  
  
5. V části **Zadejte typ položky konfigurace, který chcete vytvořit**vyberte **Windows 10**.  
  
6. Pokud vytvoříte a přiřadíte kategorie, které vám pomůžou při hledání a filtrování položek konfigurace v konzole Configuration Manager, vyberte **kategorie**.  
  
7. Na stránce průvodce **Podporované platformy** vyberte specifické platformy Windows 10, které vyhodnotí položku konfigurace.  
  
8. Na stránce průvodce **Nastavení zařízení** vyberte skupinu nastavení, kterou chcete konfigurovat. (Podrobnosti najdete v části [referenční informace k nastavení položky konfigurace Windows 10](#BKMK_Ref) v tomto článku.) Pak vyberte **Další**.  
  
   > [!TIP]  
   >  Pokud není uvedené požadované nastavení, zaškrtněte políčko **Konfigurovat další nastavení, která nejsou ve skupinách výchozích nastavení**.  
  
9. Na každé stránce nastavení nakonfigurujte požadovaná nastavení a zda je chcete opravit, když nedodržují předpisy na zařízeních (Pokud je tato podpora podporovaná).  
  
10. U každé skupiny nastavení můžete také nakonfigurovat závažnost oznámenou, když se zjistí, že je položka konfigurace nekompatibilní:  
  
    -   **Žádné**: zařízení, které nesplní toto pravidlo dodržování předpisů, nehlásí pro sestavy Configuration Manager žádné závažnost selhání.  
  
    -   **Informace**: zařízení, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager nástroje závažnost selhání typu **informace** .  
  
    -   **Upozornění**: zařízení, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **Upozornění** .  
  
    -   **Kritické**: zařízení, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** .  
  
    -   **Kritické s událostí**: zařízení, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** . Tato úroveň závažnosti je rovněž zaznamenána jako událost systému Windows v protokolu událostí aplikací.  
  
11. Na stránce průvodce **použitelnost platformy** zkontrolujte nastavení, která nejsou kompatibilní s dříve vybranými podporovanými platformami. Můžete se vrátit zpět a tato nastavení odebrat, nebo můžete pokračovat.  
  
    > [!TIP]  
    >  Nepodporovaná nastavení se nevyhodnocují pro kompatibilitu.  
  
12. Dokončete průvodce.  
  
    Novou položku konfigurace můžete zobrazit v uzlu **Položky konfigurace** pracovního prostoru **Prostředky a kompatibilita** .  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Heslo  
  
|Nastavení|Podrobnosti|  
|-------------|-------------|  
|**Vyžadované nastavení hesla na zařízeních**|Vyžaduje heslo na podporovaných zařízeních.|  
|**Minimální délka hesla (ve znacích)**|Vyžadovaná minimální délka hesla ve znacích.|  
|**Heslo vyprší za následující počet dnů**|Počet dní, než bude heslo nutné změnit.|  
|**Počet zapamatovaných hesel**|Znemožní znovu používat předchozí hesla.|  
|**Počet neúspěšných pokusů o přihlášení před vymazáním zařízení**|Vymaže zařízení, pokud se nejedná o počet neúspěšných přihlášení.|  
|**Doba nečinnosti, po které bude zařízení uzamčeno**|Určuje, kolik minut musí být zařízení neaktivní, než se automaticky uzamkne.|  
|**Složitost hesla**|Zvolte, jestli můžete zadat kód PIN, například ' 1234 ', nebo jestli musíte zadat silné heslo.|
|**Počet složitých znakových sad vyžadovaných v hesle**|Pokud jste vybrali **silné** heslo, použijte toto nastavení ke konfiguraci požadovaného počtu složitých znakových sad. Pro silné heslo by mělo být toto nastavení nastaveno aspoň na **3**, což znamená, že se vyžadují písmena i číslice. Vyberte **4** , pokud chcete vynutíte heslo, které navíc vyžaduje speciální znaky, například **(% $**).<br>(Pouze Windows 10)  |
  
###  <a name="device"></a>Zařízení  
  
|Název nastavení|Podrobnosti|  
|------------------|-------------|  
|**Bluetooth**|Umožňuje používat v zařízení funkci Bluetooth.|  
  
### <a name="cloud"></a>Cloud  
  
|Název nastavení|Podrobnosti|  
|------------------|-------------|  
|**Synchronizace nastavení**|Umožňuje synchronizaci nastavení mezi zařízeními.|  
|**Synchronizace přihlašovacích údajů**|Umožňuje synchronizaci přihlašovacích údajů mezi zařízeními.|  
|**Synchronizace nastavení přes připojení účtovaná podle objemu dat**|Umožňuje synchronizaci nastavení v případě měření připojení k Internetu.|  
  
### <a name="roaming"></a>Roaming  
  
|Název nastavení|Podrobnosti|  
|------------------|-------------|  
|**Datový roaming**|Umožňuje roaming mezi sítěmi při přístupu k datům.|  
  
### <a name="encryption"></a>Šifrování  
  
|Název nastavení|Podrobnosti|  
|------------------|-------------|  
|**Šifrování souborů v zařízení**|Vyžaduje, aby soubory v zařízení byly šifrované.|  
  
### <a name="system-security"></a>Zabezpečení systému  
  
|Název nastavení|Podrobnosti|  
|------------------|-------------|  
|**řízení uživatelských účtů**|Konfiguruje fungování řízení uživatelských účtů v systému Windows v zařízení.<br />Můžete ho například zakázat nebo nastavit úroveň, při které budete upozorněni.|  
|**Síťová brána firewall**|Povolí nebo zakáže bránu Windows Firewall.|  
|**SmartScreen**|Povolí nebo zakáže filtr Windows SmartScreen.|  
|**Ochrana proti virům**|Vyžaduje instalaci a konfiguraci antivirového softwaru.|  
|**Signatury antivirové ochrany jsou aktuální**|Vyžaduje, aby se soubory signatury antivirového softwaru na zařízení nastavily v aktuálním stavu.|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Díky nárůstu počtu zařízení vlastněných zaměstnanci v podniku se také zvyšuje riziko náhodných úniků dat prostřednictvím aplikací a služeb, jako jsou e-mail, sociální média a veřejný cloud. Tyto prvky jsou mimo řízení organizace. Příklady zahrnují případy, kdy zaměstnanec:

- Odesílá nejnovější technické obrázky ze svého osobního e-mailového účtu.
- Zkopíruje informace o produktu a vloží je do souboru.
- Uloží probíhající zprávu o prodeji do veřejného cloudového úložiště.

Windows Information Protection (dříve nedokončená podniková ochrana dat) pomáhá chránit před touto potenciálním únikem dat, aniž by bylo v konfliktu s prostředím zaměstnanců. Nedokončená práce také pomáhá chránit podnikové aplikace a data před náhodnými úniky dat na zařízeních ve vlastnictví podniku a na osobních zařízeních, která zaměstnanci přinášejí. Nedokončená výroba nevyžaduje změny v prostředí nebo jiných aplikacích.

Položky konfigurace Configuration Manager Information Protection Windows spravují tyto položky:

- Seznam aplikací chráněných nedokončenou výrobou
- Firemní umístění v síti
- Úroveň ochrany
- Nastavení šifrování
  
Informace o konfiguraci nedokončené výroby pomocí Configuration Manager najdete v tématech:

- [Ochrana podnikových dat pomocí Information Protection Windows (NV)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Vytvoření a nasazení zásady Information Protection Windows (nedokončené výroby) pomocí Configuration Manager](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Omezení při použití Information Protection Windows (NV)](/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Viz také:  
[Položky konfigurace pro zařízení spravovaná pomocí klienta Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)