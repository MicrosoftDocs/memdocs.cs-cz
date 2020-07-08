---
title: Připojte svůj účet Intune k vašemu spravovanému účtu Google Play.
titleSuffix: Microsoft Intune
description: Naučte se připojit svůj účet Intune ke spravovanému účtu Google Play.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6e57f062a3440ea922684d7ad746060ac7788f3
ms.sourcegitcommit: ba36a60b08bb85d592bfb8c4bbe6d02a47858b09
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052472"
---
# <a name="connect-your-intune-account-to-your-managed-google-play-account"></a>Připojte svůj účet Intune k vašemu spravovanému účtu Google Play

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Aby bylo možné podporovat [pracovní profil pro Android Enterprise](android-work-profile-enroll.md), [plně spravovanou platformu Android Enterprise](android-fully-managed-enroll.md)a [zařízení s Androidem Enterprise](android-kiosk-enroll.md), musíte svůj účet tenanta Intune připojit ke spravovanému účtu Google Play.  

Pokud chcete mít jistotu, že je Android Enterprise dostupný ve vaší zemi nebo oblasti, přečtěte si následující článek o podpoře od společnosti Google:https://support.google.com/work/android/answer/6270910

Aby bylo snazší konfigurovat a používat podnikovou správu Androidu, při připojení k Google Play Intune automaticky přidá čtyři běžné aplikace pro Android Enterprise v konzole pro správu Intune. Čtyři aplikace pro Android Enterprise jsou následující:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** – používá se pro plně spravované scénáře pro Android Enterprise.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** – vám pomůže se přihlašovat k vašim účtům, pokud použijete dvojúrovňové ověřování.
- **[Portál společnosti Intune](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** – používá se pro scénáře zásad ochrany aplikací (App) a Android Enterprise Work Profile.
- [Spravovaná Domovská obrazovka](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise) – používá se pro scénáře podnikových scénářů nebo veřejného terminálu pro Android.

> [!NOTE]
> Protože dochází k interakci mezi doménami Google a Microsoft, může tento krok vyžadovat úpravu nastavení prohlížeče.  Zkontrolujte, jestli jsou portal.azure.com a play.google.com ve vašem prohlížeči ve stejné zóně zabezpečení.

1. Pokud jste to ještě neudělali, připravte se na správu mobilních zařízení [nastavením autority pro správu mobilních zařízení na](../fundamentals/mdm-authority-set.md) **Microsoft Intune**.
2. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení**  >  **Android**Android  >  **registrace**  >  **spravovaná Google Play**.  Pokud používáte vlastní roli správce Intune, vyžaduje přístup k tomuto nastavení oprávnění ke čtení a aktualizaci na úrovni organizace.
   
   ![Obrazovka registrace Androidu Enterprise](./media/connect-intune-android-enterprise/android-work-bind.png)

3. Volbou možnosti **Souhlasím** udělte Microsoftu oprávnění k [odesílání informací o uživatelích a zařízeních do Googlu](../protect/data-intune-sends-to-google.md). 
   
4. Volbou možnosti **Pokud se chcete hned připojit, spusťte Google** otevřete web spravovaného obchodu Google Play. Web se otevře v prohlížeči na nové kartě.
  
5. Na přihlašovací stránce Google zadejte účet Google, který bude přidružený ke všem úlohám správy Android Enterprise pro tohoto tenanta. Jedná se o účet Google, který správci IT ve vaší společnosti sdílejí a používají ke správě a publikování aplikací v konzole Google Play. Můžete použít existující účet Google, nebo vytvořte nový. Zvolený účet nesmí být přidružený k doméně G-Suite.
    
    > [!Note]
    > Pokud používáte prohlížeč Microsoft Edge, kliknutím na **Přihlásit se** v pravém horním rohu se přihlaste ke svému účtu Google.

6. Do pole **Název organizace** zadejte název vaší společnosti. Jako **Poskytovatel EMM (Enterprise Mobility Management)** by se měl zobrazit **Microsoft Intune**.

7. Vyjádřete souhlas se smlouvou pro Android a zvolte **Potvrdit**. Vaše žádost bude zpracována.

## <a name="disconnect-your-android-enterprise-administrative-account"></a>Odpojení účtu správce Android Enterprise

Můžete vypnout registraci a správu Androidu Enterprise. Abyste to mohli udělat, musíte nejdřív vyřadit všechna zaregistrovaná podniková zařízení s Androidem, včetně zařízení s pracovním profilem, vyhrazených zařízení a plně spravovaných zařízení. Pak v konzole pro správu Intune zvolte **Odpojit** a odeberte všechna zaregistrovaná zařízení se systémem Android Enterprise Work Profiling, vyhrazená zařízení a plně spravovaná zařízení od registrace. Tím se taky odstraní vztah mezi spravovaným účtem Google Play a Intune.

1. Jako správce Intune se přihlaste k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Android**  >  **registrace**  >  **spravovaná Google Play**  >  **Odpojit**.
3. Volbou možnosti **Ano** odpojte a zrušte registraci všech zařízení s Androidem Enterprise z Intune.

## <a name="next-steps"></a>Další kroky

Po připojení ke spravovanému účtu Google Play můžete [nastavit zařízení s pracovním profilem Android Enterprise](android-work-profile-enroll.md), [nastavit vyhrazená zařízení](android-kiosk-enroll.md) s Androidem Enterprise a [nastavit zařízení s plnou správou pro Android Enterprise](android-fully-managed-enroll.md) .
