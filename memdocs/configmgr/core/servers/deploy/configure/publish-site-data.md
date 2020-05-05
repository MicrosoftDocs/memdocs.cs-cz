---
title: Publikování dat lokalit
titleSuffix: Configuration Manager
description: Naučte se publikovat Configuration Manager weby do Active Directory Domain Services.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718361"
---
# <a name="publish-site-data-for-configuration-manager"></a>Publikování dat webu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po rozšíříte schéma služby Active Directory pro Configuration Manager můžete publikovat Configuration Manager lokality do Active Directory Domain Services (služba AD DS). Díky tomu mohou počítače služby Active Directory bezpečně načítat informace o lokalitě z důvěryhodného zdroje. I když publikování informací o lokalitě služba AD DS není vyžadováno pro základní funkce Configuration Manager, může to snížit administrativní režii.  

-   **Pokud je lokalita nakonfigurována pro publikování na služba AD DS**, klienti Configuration Manager mohou automaticky vyhledat body správy prostřednictvím publikování služby Active Directory. Používají dotaz LDAP na server globálního katalogu.  

-   **Pokud se lokalita nepublikuje ve službě AD DS**, klienti musí mít alternativní mechanismus vyhledání svého výchozího bodu správy.  

Informace o tom, jak klienti hledají bod správy, najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality pro Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Konfigurace lokalit pro publikování ve službě AD DS  
 Postup vysoké úrovně je následující:  

-   Je nutné [, abyste rozšíříte schéma služby Active Directory pro Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) v každé doménové struktuře, ve které budete publikovat data lokality. Ujistěte se také, že je kontejner **System Management** přítomný.  

-   Účtu počítače každé primární lokality, která bude publikovat data, je nutné udělit **Úplné řízení** kontejneru **System Management** a všech jeho podřízených objektů.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Povolení publikování informací o lokalitě Configuration Manager v doménové struktuře služby Active Directory

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**a klikněte na možnost **lokality**. Vyberte lokalitu, pro kterou chcete publikovat data lokality. Pak na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

3.  Na kartě **publikování** vlastností lokality vyberte doménové struktury, do kterých bude tato lokalita publikovat data lokality.  

4.  Konfiguraci uložíte kliknutím na **OK** .  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Nastavení doménové struktury služby Active Directory pro publikování  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** rozbalte položku **Konfigurace hierarchie**a klikněte na možnost **doménové struktury služby Active Directory**. Jestliže bylo předtím spuštěno zjišťování doménové struktury služby Active Directory, v podokně výsledků uvidíte všechny zjištěné doménové struktury. Při spuštění doménové struktury služby Active Directory je zjištěna místní doménová struktura a všechny důvěryhodné doménové struktury. Ručně je nutno přidat pouze nedůvěryhodné doménové struktury.  

    -   Pokud chcete nastavit dříve zjištěnou doménovou strukturu, vyberte doménovou strukturu v podokně výsledků. Pak na kartě **Domů** ve skupině **vlastnosti** kliknutím na **vlastnosti** otevřete vlastnosti doménové struktury. Pokračujte krokem 3.  

    -   Pokud chcete nastavit novou doménovou strukturu, která není uvedená, na kartě **Domů** ve skupině **vytvořit** kliknutím na **Přidat doménovou strukturu** otevřete dialogové okno **Přidat** doménové struktury. Pokračujte krokem 3.  

3.  Na kartě **Obecné** dokončete konfigurace pro doménovou strukturu, které chcete zjišťovat, a zadejte **účet doménové struktury služby Active Directory**.  

    > [!NOTE]  
    >  Zjišťování doménové struktury služby Active Directory vyžaduje pro zjišťování a publikování na nedůvěryhodných doménových strukturách globální účet. Pokud nepoužíváte účet počítače serveru lokality, můžete zvolit pouze globální účet.  

4.  Pokud plánujete povolit, aby lokality publikovaly data lokality na doménových strukturách, na kartě **Publikování** dokončete konfigurace pro publikování na těchto doménových strukturách.  

    > [!NOTE]  
    >  Pokud povolíte, aby lokality publikovaly do doménové struktury, musíte pro Configuration Manager zvětšit schéma služby Active Directory této doménové struktury. Účet doménové struktury služby Active Directory musí mít oprávnění k úplnému řízení kontejneru systému v této doménové struktuře.  

5.  Po dokončení konfigurace této doménové struktury pro použití se zjišťováním doménových struktur služby Active Directory klikněte na tlačítko **OK** , čímž konfiguraci uložíte.  
