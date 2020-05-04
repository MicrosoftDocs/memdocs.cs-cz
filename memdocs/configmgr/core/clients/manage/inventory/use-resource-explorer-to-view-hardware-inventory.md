---
title: Jak používat Průzkumník prostředků
titleSuffix: Configuration Manager
description: Pomocí Průzkumník prostředků můžete zobrazit inventář hardwaru v Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710675"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Použití Průzkumník prostředků k zobrazení inventáře hardwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Průzkumník prostředků v Configuration Manager můžete zobrazit informace o inventáři hardwaru. Lokalita shromažďuje tyto informace od klientů ve vaší hierarchii.  

> [!Tip]  
>  Průzkumník prostředků nezobrazí žádná data, dokud cyklus inventáře hardwaru neběží na klientovi, ke kterému se připojujete.  



## <a name="overview"></a>Přehled

Průzkumník prostředků má následující části týkající se inventáře hardwaru:  

- **Hardware**: zobrazuje nejnovější inventář hardwaru shromážděný ze zadaného klientského zařízení.  

    - Uzel **stav pracovní stanice** zobrazuje čas a datum posledního inventáře hardwaru ze zařízení.  

- **Historie hardwaru**: Historie položek v inventáři, které se změnily od posledního cyklu inventáře hardwaru.  

    - Rozbalením položky zobrazíte **aktuální** uzel a jeden nebo více uzlů s historickým datem. Porovnat informace v aktuálním uzlu s jedním z historických uzlů, aby bylo možné zobrazit položky, které se změnily.  

> [!NOTE]  
> Ve výchozím nastavení Configuration Manager odstraní data inventáře hardwaru, která jsou neaktivní po dobu 90 dnů. Upravte tento počet dní v úloze údržby lokality **Odstranit zastaralou historii inventáře** . Další informace najdete v tématu [úlohy údržby](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a>Postup otevření Průzkumník prostředků   

1.  V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také vybrat libovolnou kolekci v uzlu **kolekce zařízení** .  

2.  Vyberte zařízení. Na pásu karet na kartě **Domů** a ve skupině **zařízení** klikněte na **Start**a vyberte **Průzkumník prostředků**.   

> [!Tip]  
> V Průzkumník prostředků klikněte pravým tlačítkem myši na položku v pravém podokně výsledků pro další akce. Kliknutím na **vlastnosti** zobrazíte tuto položku v jiném formátu.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a>Použití velkých celočíselných hodnot
<!--1357880-->
V Configuration Manager verzích 1802 a předchozí má inventář hardwaru omezení pro celá čísla větší než 4 294 967 296 (2 ^ 32). Tento limit se dá dosáhnout u atributů, jako jsou například velikosti pevného disku v bajtech. Bod správy nezpracovává celočíselné hodnoty nad rámec tohoto limitu, takže v databázi není uložena žádná hodnota. 

Počínaje verzí 1806 se limit zvyšuje na 18446744073709551616 (2 ^ 64). 

U vlastnosti s hodnotou, která se nemění, jako je celková velikost disku, se po upgradu lokality nemusí okamžitě zobrazit hodnota. Většina inventáře hardwaru je rozdílová sestava. Klient odesílá pouze hodnoty, které se mění. Chcete-li toto chování obejít, přidejte do stejné třídy další vlastnost. Tato akce způsobí, že klient aktualizuje všechny vlastnosti ve třídě, která se změnila. 



## <a name="see-also"></a>Viz také

Informace o tom, jak zobrazit inventář hardwaru z klientů se systémem Linux a UNIX, najdete v tématu [Postup monitorování klientů pro servery se systémy Linux a UNIX](../monitor-clients-for-linux-and-unix-servers.md).  

Průzkumník prostředků taky zobrazuje inventář softwaru. Další informace najdete v tématu [použití Průzkumník prostředků k zobrazení inventáře softwaru](use-resource-explorer-to-view-software-inventory.md).
