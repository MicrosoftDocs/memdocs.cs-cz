---
title: Nastavení portálu Desktop Analytics
titleSuffix: Configuration Manager
description: Průvodce nastavením a zprovozněním pro desktopovou analýzu
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91a65f240a20e30af1610670c79182dee744e77b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714903"
---
# <a name="how-to-set-up-desktop-analytics"></a>Jak nastavit analýzu plochy

Pomocí tohoto postupu se můžete přihlásit k portálu Analytics a nakonfigurovat ho v předplatném. Tento postup představuje jednorázový proces pro nastavení analýzy plochy pro vaši organizaci.  

> [!Important]  
> Informace o obecných požadavcích na desktopovou analýzu pomocí Configuration Manager najdete v tématu [požadavky](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Počáteční připojování

1. Otevřete [portál Desktop Analytics](https://aka.ms/desktopanalytics) v Microsoft 365 Správa zařízení jako uživatel s rolí **globálního správce** . Vyberte **Spustit**. Případně můžete v konzole Configuration Manager přejít do pracovního prostoru **softwarová knihovna** , vybrat uzel **údržby Desktop Analytics** a vybrat **naplánovat nasazení**.

2. Na stránce **přijmout licenční smlouvu** si přečtěte smlouvu o poskytování služeb a vyberte **přijmout**.  

3. Na stránce **Potvrdit předplatné** si přečtěte seznam požadovaných opravňujících licencí. Přepněte nastavení na **Ano** . vedle **toho máte jeden z podporovaných nebo vyšších předplatných**a pak vyberte **Další**.  

4. Na stránce **udělení přístupu uživatelům** :

    - **Umožněte službě Desktop Analytics spravovat role adresáře vaším jménem**: Desktop Analytics automaticky přiřadí **vlastníky pracovního prostoru** role **správce pro Desktop Analytics** . Pokud jsou tyto skupiny již **globálním správcem**, nedojde ke změně.

        Pokud tuto možnost nevyberete, bude aplikace Desktop Analytics stále přidávat uživatele jako členy skupiny zabezpečení. **Globální správce** musí ručně přiřadit roli **správce Desktop Analytics** pro uživatele.

        Další informace o přiřazení oprávnění role správce v Azure Active Directory a oprávnění přiřazená **správcům Desktop Analytics**najdete v tématu [oprávnění role správce v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Pro vytváření a správu pracovních prostorů a plánů nasazení v nástroji Desktop Analytics předkonfiguruje skupinu zabezpečení **vlastníci pracovního prostoru** v Azure Active Directory.

        Pokud chcete do skupiny přidat uživatele, zadejte jejich jméno nebo e-mailovou adresu do části **Zadejte jméno nebo e-mailovou adresu** . Po dokončení vyberte **Další**.

5. Na stránce **nastavte svůj pracovní prostor**:  

    > [!NOTE]  
    > K dokončení tohoto kroku potřebuje uživatel oprávnění **vlastníka pracovního prostoru** a další přístup k předplatnému Azure a skupině prostředků. Další informace najdete v tématu [předpoklady](overview.md#prerequisites).  

    - Pokud chcete použít existující pracovní prostor pro Desktop Analytics, vyberte ho a pokračujte dalším krokem.  

        > [!TIP]  
        > Můžete mít jenom jeden pracovní prostor pro Desktop Analytics na tenanta Azure AD. Zařízení mohou odesílat diagnostická data pouze do jednoho pracovního prostoru.  

    - Pokud chcete vytvořit pracovní prostor pro Desktop Analytics, vyberte **Přidat pracovní prostor**.  

        1. Zadejte globálně jedinečný **název pracovního prostoru**.

        2. V rozevíracím seznamu vyberte **název předplatného Azure pro tento pracovní prostor**a zvolte předplatné Azure pro tento pracovní prostor.  

        3. **Vytvořit nový** Skupinu prostředků nebo **použijte existující**.

        4. Vyberte **oblast** ze seznamu a pak vyberte **Přidat**.  

6. Vyberte nový nebo existující pracovní prostor a pak vyberte **nastavit jako pracovní prostor Analytics pro stolní počítače**.  Pak v dialogovém okně **potvrzení a udělení přístupu** vyberte **pokračovat** .  

7. Na kartě nový prohlížeč vyberte účet, který se má použít k přihlášení. Vyberte možnost **souhlasu jménem vaší organizace** a vyberte **přijmout**.  

    > [!Note]  
    > Tímto souhlasem je přiřazení aplikace MALogAnalyticsReader k pracovnímu prostoru role čtecího modulu Log Analytics. Tato role aplikace je vyžadována analýzou plochy. Další informace najdete v tématu [aplikační role MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Zpátky na stránce **nastavte svůj pracovní prostor**tak, že vyberete **Další**.  

9. Na stránce **Poslední kroky** vyberte **Přejít na Desktop Analytics**.

Azure Portal zobrazuje **domovskou** stránku nástroje Desktop Analytics.

## <a name="next-steps"></a>Další kroky

Přejděte k dalšímu článku a připojte se Configuration Manager k Desktop Analytics.
> [!div class="nextstepaction"]  
> [Připojení správce konfigurací](connect-configmgr.md)  
