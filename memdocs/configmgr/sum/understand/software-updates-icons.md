---
title: Ikony používané pro aktualizace softwaru
titleSuffix: Configuration Manager
description: Konzola Configuration Manager obsahuje ikony, které označují stav pro synchronizovanou aktualizaci nebo skupinu aktualizací softwaru.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0ca0509893ecadc4c54d06ca98c18531959fb941
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608409"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Ikony používané pro aktualizace softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Synchronizované aktualizace softwaru se zobrazují v konzole Configuration Manager a první sloupec pro jednotlivé aktualizace softwaru obsahuje ikonu, která označuje určitý stav. Skupiny aktualizací softwaru jsou také reprezentované ikonou, která poskytuje informace o stavu aktualizací softwaru obsažených ve skupině. Tato část obsahuje informace o ikonách aktualizací softwaru a jejich významu.  

## <a name="icons-for-software-updates"></a>Ikony aktualizací softwaru  
 Synchronizované aktualizace softwaru jsou reprezentované pomocí jedné z následujících ikon.  

### <a name="normal-icon"></a>Ikona Normální  
 ![Ikona normální](../media/Normal.jpg) Ikona se zelenou šipkou představuje normální aktualizace softwaru.  

 **Popis:**  

 Normální aktualizace softwaru byly synchronizované a jsou k dispozici pro nasazení.  

 **Provozní otázky:**  

 Neexistují žádné provozní otázky.  

### <a name="expired-icon"></a>Ikona Konec platnosti  
 ![Ikona s vypršenou platnost ](../media/Expired.jpg) ikona s černou symbolem X představuje aktualizaci softwaru s vypršenou platností. Aktualizace softwaru s vypršenou platností můžete také zjistit zobrazením sloupce **vypršení platnosti** pro aktualizaci softwaru, když se zobrazí v konzole Configuration Manager.  

 **Popis:**  

 Aktualizace softwaru s vypršenou platností byly dřív dostupné pro nasazení do klientských počítačů, ale po vypršení platnosti už pro ně nejdou vytvářet nová nasazení. Aktualizace softwaru s vypršenou platností jsou odebrány z aktivních nasazení a již nebudou zpřístupněny klientům.  

 **Provozní otázky:**  

 Neexistují žádné provozní otázky.

### <a name="superseded-icon"></a>Ikona Nahrazeno  
 ![Nahrazená ikona ](../media/Superseded.jpg) ikona se žlutou hvězdičkou představuje nahrazenou aktualizaci softwaru. Nahrazené aktualizace softwaru můžete také identifikovat zobrazením **nahrazeného** sloupce aktualizace softwaru, když se zobrazí v konzole Configuration Manager.  

 **Popis:**  

 Nahrazené aktualizace softwaru se nahradily novější verzí aktualizace softwaru. Aktualizace softwaru, která nahrazuje jinou aktualizaci softwaru, má obvykle jednu nebo více následujících akcí:  

- Zdokonaluje, zlepšuje nebo doplňuje opravu, která byla vydaná v některé z předchozích aktualizací softwaru.  

- Zvyšuje účinnost balíčku aktualizace softwaru, který klientské počítače instalují, pokud je tato aktualizace schválená k instalaci. Nahrazená aktualizace softwaru může například obsahovat soubory, které již nejsou důležité pro opravu nebo operační systémy aktuálně podporované novou aktualizací softwaru, takže tyto soubory nejsou zahrnuty v nahrazujícím balíčku souborů aktualizace softwaru.  

- Aktualizuje novější verze produktu, jinými slovy už není použitelná pro starší verze nebo konfigurace produktu. Aktualizace softwaru můžou také nahrazovat jiné aktualizace, pokud se provedly úpravy rozšiřující jazykovou podporu. Například pozdější revize aktualizace produktu pro Microsoft 365 aplikace může odebrat podporu pro starší operační systém, ale přidat další podporu nových jazyků v úvodním vydání aktualizace softwaru.  

  Na kartě Pravidla nahrazení ve vlastnostech komponenty bodu aktualizace softwaru můžete určit způsob správy nahrazených aktualizací softwaru. Další informace najdete v části [Pravidla nahrazení](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Provozní otázky:**  

  Pokud je to možné, nasaďte nahrazující aktualizaci softwaru do klientských počítačů namísto nahrazené softwarové aktualizace. Seznam aktualizací softwaru, které nahrazují aktualizace softwaru můžete zobrazit na kartě **Informace o nahrazení** ve vlastnostech aktualizací softwaru.  

### <a name="invalid-icon"></a>Ikona Neplatné  
 ![Neplatná ikona](../media/Invalid.jpg) Ikona s černým symbolem X představuje neplatnou aktualizaci softwaru.  

 **Popis:**  

 Neplatné aktualizace softwaru jsou v aktivním nasazení, ale z nějakého důvodu není k dispozici obsah (soubory aktualizace softwaru). Tento stav může nastat v následujících situacích:  

- Úspěšně jste nasadili aktualizaci softwaru, ale soubor aktualizace softwaru byl z balíčku pro nasazení odebraný a již není k dispozici.  

- Vytvoříte nasazení aktualizace softwaru v lokalitě a objekt nasazení se úspěšně replikuje do podřízené lokality, ale balíček pro nasazení se úspěšně nereplikoval do podřízené lokality.  

  **Provozní otázky:**  

  Pokud pro aktualizaci softwaru chybí obsah, klienti ji nebudou moct nainstalovat, dokud nebude obsah v distribučním bodě opět k dispozici. Obsah můžete znovu distribuovat do distribučních bodů pomocí akce **Znovu distribuovat** . Pokud chybí obsah pro aktualizaci softwaru v nasazení vytvořeném v nadřazené lokalitě, je třeba aktualizaci softwaru replikovat nebo distribuovat do podřízené lokality. Další informace o redistribuci obsahu najdete v tématu [Správa obsahu, který jste distribuujei](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Ikona Pouze metadata
 ![Ikona jenom s metadaty](../media/MetadataOnly.png) Ikona s modrou šipkou představuje aktualizace softwaru obsahující jenom metadata.

 **Popis:**  

 V konzole Configuration Manager jsou k dispozici pouze aktualizace softwaru s metadaty pro vytváření sestav. Aktualizace softwaru obsahující pouze metadata nelze nasadit ani stáhnout, protože soubor aktualizace softwaru není přidružen k metadatům aktualizace softwaru.  

 **Provozní otázky:**  

 Pro účely vytváření sestav jsou k dispozici pouze aktualizace softwaru, které nejsou určeny pro nasazení aktualizací softwaru.  

## <a name="icons-for-software-update-groups"></a>Ikony pro skupiny aktualizací softwaru  
 Skupiny aktualizací softwaru jsou reprezentované pomocí jedné z následujících ikon.  

### <a name="normal-icon"></a>Ikona Normální  
 ![Skupiny aktualizací softwaru – ikona normální](../media/Normal.jpg) Ikona s zelenou šipku představuje skupinu, která obsahuje jenom normální softwarové aktualizace.  

 **Provozní otázky:**  

 Neexistují žádné provozní otázky.  

### <a name="expired-icon"></a>Ikona Konec platnosti  
 ![Ikona neplatných skupin aktualizací softwaru](../media/Expired.jpg) Ikona s černým symbolem X představuje skupinu, která obsahuje jednu nebo několik softwarových aktualizací s ukončenou platností.  

 **Provozní otázky:**  

 Nahraďte aktualizace softwaru s vypršenou platností, pokud je to možné.  

### <a name="superseded-icon"></a>Ikona Nahrazeno  
 ![Skupiny aktualizací softwaru-ikona nahrazeno](../media/Superseded.jpg) Ikona s černým symbolem X představuje skupinu, která obsahuje jednu nebo několik softwarových aktualizací s ukončenou platností.  

 **Provozní otázky:**  

 Pokud je to možné, nahraďte nahrazené softwarové aktualizace ve skupině nahrazující aktualizací.  

### <a name="invalid-icon"></a>Ikona Neplatné  
 ![Skupiny aktualizací softwaru-neplatná ikona](../media/Invalid.jpg) Ikona s červeným symbolem X představuje skupinu, která obsahuje jednu nebo několik neplatných softwarových aktualizací.  

 **Provozní otázky:**  

 Pokud pro aktualizaci softwaru chybí obsah, klienti ji nebudou moct nainstalovat, dokud nebude obsah v distribučním bodě opět k dispozici. Obsah můžete znovu distribuovat do distribučních bodů pomocí akce **Znovu distribuovat** . Pokud chybí obsah pro aktualizaci softwaru v nasazení vytvořeném v nadřazené lokalitě, je třeba aktualizaci softwaru replikovat nebo distribuovat do podřízené lokality. Další informace o redistribuci obsahu najdete v tématu [Správa obsahu, který jste distribuujei](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Další kroky 

[Plánování aktualizací softwaru](../plan-design/plan-for-software-updates.md)