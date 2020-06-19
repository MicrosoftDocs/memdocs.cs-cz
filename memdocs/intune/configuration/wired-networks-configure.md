---
title: Konfigurace nastavení drátové sítě 802.1 x pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte nebo přidejte konfigurační profil zařízení kabelové sítě pro zařízení macOS Desktop Computer. Podívejte se na různá nastavení, přidejte certifikáty, zvolte typ protokolu EAP a vyberte metodu ověřování v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095695"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Přidávání a používání nastavení drátových sítí na zařízeních macOS v Microsoft Intune

V mnoha organizacích využívají kabelové sítě k poskytnutí síťového přístupu počítačům v síti. Microsoft Intune zahrnuje vestavěná nastavení, která se dají nasadit tak, aby macOS uživatele a zařízení ve vaší organizaci. Tato skupina nastavení se nazývá profil. V profilu můžete zahrnout společná nastavení, jako je síťové rozhraní, akceptované typy protokolu EAP a nastavení důvěryhodnosti serveru.

Až bude profil připravený, dá se přiřadit k různým uživatelům a skupinám. Po přiřazení získají uživatelé přístup k pevné síti vaší organizace, aniž by ji nakonfigurovali sami.

V rámci řešení správy mobilních zařízení (MDM) pomocí této funkce můžete vytvořit profily 802.1 x pro správu drátových sítí. Potom tyto kabelové sítě nasaďte do zařízení macOS.

Tato funkce platí pro:

- macOS

Máte třeba pevnou síť s názvem **drátová síť contoso**. Chcete nastavit všechny macOS plochy pro připojení k této síti. Postup je následující:

1. Vytvořte profil drátové sítě, který obsahuje nastavení, která se připojují k **drátové síti Contoso**.
2. Přiřaďte profil ke skupině, která obsahuje všechny uživatele macOS stolní počítače. Doporučení k používání typů skupin najdete v tématu [skupiny uživatelů a skupiny zařízení](device-profile-assign.md#user-groups-vs-device-groups).
3. Na svých plochách uživatelé naleznou v seznamu sítí **drátovou síť contoso** . Potom se mohou k této síti připojit s využitím metody ověřování, kterou zvolíte.

Tento článek obsahuje seznam kroků pro vytvoření profilu drátové sítě. Obsahuje také odkaz, který popisuje různá nastavení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **MacOS**.
    - **Profil**: vyberte možnost **drátová síť**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil drátové sítě pro celou firmu na zařízeních MacOS**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**vyberte síťové rozhraní sítě a zvolte typ protokolu EAP (Extensible Authentication Protocol). Seznam všech nastavení a o tom, co dělají, najdete v těchto tématech:

    - [macOS](wired-network-settings-macos.md)

8. Vyberte **Další**.
9. V části **přiřazení**vyberte skupiny uživatelů nebo skupiny zařízení, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

10. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

> [!TIP]
> Použijete-li pro profil drátové sítě ověřování na základě certifikátů, pak nasaďte profil drátové sítě, profil certifikátu a důvěryhodný kořenový profil do stejných skupin. Toto nasazení zajistí, že každé zařízení dokáže rozpoznat legitimitu certifikační autority. Další informace najdete v tématu [Konfigurace certifikátů pomocí Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Další kroky

Profil je vytvořen, ale nemusí provádět žádné akce. Nezapomeňte [Tento profil přiřadit](device-profile-assign.md)a [monitorovat jeho stav](device-profile-monitor.md).
