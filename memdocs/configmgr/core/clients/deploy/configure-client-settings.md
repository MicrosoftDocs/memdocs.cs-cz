---
title: Konfigurace nastavení klientů
titleSuffix: Configuration Manager
description: V Configuration Manager vyberte nastavení klienta.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713587"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Postup konfigurace nastavení klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Všechna nastavení klienta v Configuration Manager můžete spravovat z **Administration** > **nastavení klienta**Správa. Změnou výchozích nastavení můžete změnit nastavení pro všechny uživatele a zařízení v hierarchii, která nepoužívají vlastní nastavení. Pokud chcete použít různá nastavení jenom pro některé uživatele nebo zařízení, vytvořte vlastní nastavení a nasaďte je do kolekcí.  

Informace o jednotlivých nastaveních klienta najdete v tématu informace [o nastavení klienta](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Pomocí položek konfigurace můžete taky posuzovat, sledovat a opravovat kompatibilitu konfigurace klientských zařízení. Další informace najdete v tématu [zajištění dodržování předpisů zařízením pomocí Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Konfigurovat výchozí nastavení klienta    

1. V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

2. Na kartě **Domů** klikněte na položku **vlastnosti**.  

3. V navigačním podokně si můžete zobrazit a konfigurovat nastavení klientů podle skupin.  

   Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [spuštění načtení zásad pro klienta Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) v tématu [Správa klientů](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Vytvoření a nasazení vlastních nastavení klienta  
Pokud je nasazené vlastní nastavení, má přednost před výchozím nastavením klientů. Před zahájením tohoto postupu zkontrolujte, jestli máte kolekci obsahující uživatele a zařízení vyžadující tato vlastní nastavení.  

1. V konzole Configuration Manager vyberte možnost **Správa** > **nastavení klienta**.  

2. Na kartě **Domů** ve skupině **vytvořit** zvolte možnost **vytvořit vlastní nastavení klienta**a pak zvolte jednu z těchto akcí:  

   -   **Vytvořit vlastní nastavení klientského zařízení**  

   -   **Vytvořit vlastní uživatelská nastavení klienta**  

3. Zadejte jedinečný název a Popis možnosti.  

4. Zaškrtněte jedno nebo více políček, která zobrazují skupinu nastavení.  

5. V navigačním podokně zvolte každou skupinu nastavení a nakonfigurujte dostupná nastavení a pak klikněte na **OK**.   

6. Vyberte vlastní nastavení klienta, které jste vytvořili. Na kartě **Domů** ve skupině **nastavení klienta** vyberte možnost **nasadit**.  

7. V dialogovém okně **Vybrat kolekci** vyberte příslušnou kolekci a pak zvolte **OK**. Vybranou kolekci můžete ověřit kliknutím na kartu **Nasazení** v podokně podrobností.  

8. Podívejte se na pořadí vlastního nastavení klienta, které jste vytvořili. Pokud používáte víc vlastních nastavení klienta, aplikují se podle pořadového čísla. Pokud jsou nastavení v konfliktu, má přednost nastavení s nejnižším pořadovým číslem. Chcete-li změnit číslo objednávky, klikněte na kartě **Domů** ve skupině **nastavení klienta** na možnost **přesunout položku nahoru** nebo **přesunout položku dolů**.  

   Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [spuštění načtení zásad pro klienta Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) v tématu [Správa klientů](../../../core/clients/manage/manage-clients.md).  



##  <a name="view-client-settings"></a>Zobrazit nastavení klienta  
 Když nasadíte více nastavení klienta na stejné zařízení, uživatele nebo skupinu uživatelů, stanovení priorit a kombinace nastavení je složité. Zobrazení nastavení klienta:  

1.  V konzole Configuration Manager vyberte **prostředky a** > **zařízení** > dodržování předpisů**uživatele** nebo **kolekce uživatelů**.  

3.  Vyberte zařízení, uživatele nebo skupinu uživatelů a ve skupině **Nastavení klienta** zvolte **Výsledná nastavení klienta**.  

4.  V levém podokně vyberte nastavení klienta a zobrazí se nastavení. V tomto zobrazení jsou nastavení jen pro čtení. 

    > [!NOTE]  
    >  Chcete-li zobrazit nastavení klienta, je nutné mít oprávnění ke čtení pro nastavení klienta.  

    
