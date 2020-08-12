---
title: Profily OneDrivu pro firmy
titleSuffix: Configuration Manager
description: Přesměrovat známé složky Windows na OneDrive pro firmy pomocí profilu OneDrivu pro firmy v Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d13d9dfd75abb656a765ce8c91ce6f177636cd3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127167"
---
# <a name="onedrive-for-business-profiles"></a>Profily OneDrivu pro firmy

Od verze Configuration Manager 1902 můžete vytvořit profily OneDrivu pro firmy pro přesun známých složek Windows na OneDrive pro firmy. Mezi tyto složky patří plocha, dokumenty a obrázky. V každém profilu můžete zadat nastavení pro přesunutí známých složek Windows. Další informace o OneDrivu pro firmy najdete v tématu [přesměrování a přesunutí známých složek Windows na OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Požadavky

- [Najít ID tenanta Microsoft 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Nasazení synchronizačního klienta OneDrive verze 18.111.0603.0004 nebo novější. Další informace najdete v tématu [nasazení aplikací OneDrive pomocí Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a>Přesunout známé složky Windows na OneDrive
<!--3556021-->
Pomocí Configuration Manager můžete přesunout známé složky Windows na OneDrive pro firmy. Mezi tyto složky patří plocha, dokumenty a obrázky. Chcete-li zjednodušit upgrady Windows 10, nasaďte tato nastavení do klientů se systémem Windows 7 před nasazením pořadí úkolů. 

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte **Nastavení dodržování předpisů**a vyberte uzel **profily OneDrivu pro firmy** .  

   ![Uzel profilů OneDrivu pro firmy](media/onedrive-for-business-profiles-node.png)
2. Na pásu karet vyberte **vytvořit profil OneDrivu pro firmy**.  

3. Zadejte název pro identifikaci této zásady a vyberte **Další**.  

4. Vyberte platformy, které se zřídí s profilem OneDrivu pro firmy. Po dokončení výběru platforem klikněte na **Další**.

    ![Výběr platforem pro profil OneDrivu pro firmy](media/onedrive-for-business-profile-select-platforms.png) 

5. Na stránce **Nastavení** :

    1. Zadejte ID tenanta Microsoft 365.  

    2. Vyberte jednu z následujících možností pro přesunutí známých složek na OneDrive:  

        - **Vyzvat uživatele k přesunutí známých složek Windows na OneDrive**: s touto možností se uživateli zobrazí průvodce pro přesunutí svých souborů. Pokud se rozhodne odložit nebo odmítnout přesun svých složek, OneDrive je bude v pravidelných intervalech připomenout.  

        - **Bezobslužné přesunutí známých složek Windows na OneDrive**: Pokud se tato zásada vztahuje na zařízení, klient OneDrive automaticky přesměruje známé složky na OneDrive pro firmy.  

            - **Zobrazit oznámení uživatelům po přesměrování složek**: Pokud povolíte tuto možnost, klient OneDrivu uživatele po přesunutí svých složek upozorní.  

    3. **Zabránit uživatelům v přesměrování svých známých složek Windows zpátky na jejich počítače**: zakáže možnost na OneDrivu pro firmy na klientovi, aby uživatelé přesunuli tyto složky zpátky do zařízení.  

       ![Nastavení přesunutí známé složky OneDrivu pro firmy](media/onedrive-for-business-profile-move-folder-settings.png)

6. Dokončete průvodce a potom zásadu nasaďte.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Nasazení profilu OneDrivu pro firmy

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte **Nastavení dodržování předpisů**a vyberte uzel **profily OneDrivu pro firmy** .  


2. Vyberte profil a pak na pásu karet vyberte **nasadit** .

3. Pro nasazení zadejte následující nastavení:

   1. **Kolekce**: klikněte na **Procházet...** a vyberte kolekci, pro kterou chcete profil nasadit.  
   1. **Vygenerovat výstrahu**:

      - **Pokud je uvedeno dodržování předpisů níže**: minimální procento dodržování předpisů klientů pro zachování v opačném případě se vygeneruje výstraha.
      -  **Datum a čas**: upozornění na datum prvního spuštění se generuje na základě dodržování předpisů pro profily.
      - **Generovat výstrahu System Center Operations Manager**: odešlete výstrahu o dodržování předpisů, která se má System Center Operations Manager.
   1. **Plán**:

      - **Jednoduchý plán**: Toto nastavení ve výchozím nastavení používá jednoduchý plán ke spuštění vyhodnocení dodržování předpisů každých 7 dní.
      - **Vlastní plán**: Určete, kdy se má spustit vyhodnocení dodržování předpisů. Čas spuštění vychází z místního času počítače, na kterém je spuštěna konzola Configuration Manager, v době, kdy jste plán vytvořili, nebo můžete použít UTC.
 
      ![Nasadit profil OneDrivu pro firmy](media/onedrive-for-business-deploy-profile.png)

4. Kliknutím na **OK** nasaďte profil OneDrivu pro firmy.


## <a name="next-steps"></a>Další kroky

[Vytváření profilů vzdáleného připojení](create-remote-connection-profiles.md)
