---
title: Příprava nasazení operačního systému
titleSuffix: Configuration Manager
description: Přečtěte si, jak připravit nasazení operačního systému v Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724080"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Příprava na nasazení operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete moct nasadit operační systém, musíte v Configuration Manager udělat několik věcí. Příprava nasazení operačního systému pomocí následujících článků:  

-   [Správa spouštěcích imagí](manage-boot-images.md)  

-   [Správa imagí operačního systému](manage-operating-system-images.md)  

-   [Správa balíčků s upgradem operačního systému](manage-operating-system-upgrade-packages.md)  

-   [Správa ovladačů](manage-drivers.md)  

-   [Správa stavu uživatele](manage-user-state.md)  

-   [Příprava pro nasazení do neznámých počítačů](prepare-for-unknown-computer-deployments.md)  

-   [Spojení uživatelů s cílovým počítačem](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Velikost bitové kopie operačního systému  

Velikosti imagí operačního systému jsou velké. Například velikost obrázku pro systém Windows 7 je 3 GB nebo více. Velikost bitové kopie a počet počítačů, do kterých současně nasazujete operační systém, ovlivňuje výkon sítě a dostupnou šířku pásma. Ujistěte se, že otestujete výkon sítě. Testování dopadu lépe vybere efekt, který může mít nasazení bitové kopie, a čas potřebný k dokončení nasazení. Configuration Manager aktivity, které ovlivňují výkon sítě, zahrnují distribuci image do distribučního bodu, distribuci image z jedné lokality do druhé a stažení Image do klienta.  

Také se ujistěte, že v distribučních bodech, které hostují bitové kopie operačního systému, plánujete dostatek místa na disku.  

Další informace najdete v tématu [Další aspekty plánování pro distribuční body](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Velikost mezipaměti klientů  

Když Configuration Manager klienti stahují obsah, automaticky používají Background Intelligent Transfer Service (BITS), pokud je k dispozici. Když nasadíte pořadí úloh, které nainstaluje operační systém, můžete nastavit možnost nasazení tak, aby Configuration Manager klienti před spuštěním pořadí úloh stáhli do místní mezipaměti úplnou bitovou kopii.  

Pokud klient Configuration Manager musí stáhnout bitovou kopii operačního systému, ale v mezipaměti není dostatek místa, může klient vymazat místo v mezipaměti. Zkontroluje ostatní balíčky v mezipaměti, aby zjistil, jestli se odstraněním některého z nejstarších balíčků uvolní dostatek místa na disku pro umístění Image. Pokud se odstraněním balíčků neuvolní dostatek místa, klient nestáhne image a nasazení se nepodaří. K tomuto chování může dojít v případě, že mezipaměť obsahuje velký balíček, který nakonfigurujete tak, aby zůstal v mezipaměti. Pokud se odstraněním balíčků uvolní dostatek místa v mezipaměti, klient je odstraní a potom stáhne image do mezipaměti.  

Výchozí velikost mezipaměti u Configuration Manager klientů nemusí být dostatečně velká pro většinu nasazení bitových kopií operačního systému. Pokud plánujete stáhnout úplnou bitovou kopii do mezipaměti klienta, upravte velikost mezipaměti klienta v cílových počítačích tak, aby vyhovovala velikosti bitové kopie, kterou nasazujete.  

Další informace najdete v tématu [Konfigurace mezipaměti klienta](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


