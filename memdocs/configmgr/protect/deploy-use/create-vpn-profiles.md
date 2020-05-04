---
title: Postup vytvoření profilů sítě VPN
titleSuffix: Configuration Manager
description: Naučte se vytvářet profily sítě VPN v Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713594"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Postup vytvoření profilů sítě VPN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje více typů připojení VPN. Další informace o typech připojení, které jsou k dispozici pro různé platformy zařízení, najdete v tématu [Profily sítě VPN](vpn-profiles.md).

Pro připojení k síti VPN třetích stran před nasazením profilu sítě VPN distribuujte aplikaci VPN. Pokud neprovedete nasazení aplikace, uživatelé se k tomu budou vyzváni při pokusu o připojení k síti VPN. Další informace najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Vytvoření profilu sítě VPN

1. V konzole Configuration Manager přejděte do pracovního prostoru **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**, rozbalte položku **přístup k prostředkům společnosti**a vyberte uzel **Profily sítě VPN** .

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** klikněte na možnost **vytvořit profil sítě VPN**.

1. Na stránce **Obecné** v Průvodci vytvořením profilu sítě VPN zadejte následující informace:

    - **Název**: Zadejte jedinečný název pro identifikaci profilu sítě VPN v konzole nástroje.

        > [!NOTE]
        > V názvu profilu sítě VPN nepoužívejte následující znaky: `\/:*?<>|; `. Profil sítě VPN systému Windows nepodporuje tyto speciální znaky.

    - **Popis**: Volitelně zadejte popis, který poskytne další informace o profilu sítě VPN.

    - **Typ profilu VPN**: vyberte příslušnou platformu.

        Pokud vyberete platformu **Windows 8.1** , můžete také **Importovat ze souboru**. Tato akce importuje informace o profilu sítě VPN ze souboru XML. Pokud vyberete tuto možnost, zbytek Průvodce se zjednoduší na následujících stránkách: **podporované platformy** a **Importovat profil sítě VPN**.

1. Na stránce **podporované platformy** vyberte verze operačních systémů, které tento profil sítě VPN podporuje.

1. Na stránce **připojení** zadejte následující informace:

    - **Typ připojení**: Vyberte typ připojení VPN. Další informace o podporovaných typech najdete v tématu [Profily sítě VPN](vpn-profiles.md).

    - **Seznam serverů**: přidejte nový server, který se použije pro připojení k síti VPN. V závislosti na typu připojení můžete přidat jeden nebo více serverů VPN a určit, který server je výchozí.

    - **Obcházet VPN při připojení k podnikové síti**: nakonfigurujte klienty tak, aby nepoužívali VPN, pokud jsou ve vaší interní síti. V případě potřeby zadejte název DNS specifický pro připojení.

1. Na stránce **metoda ověření** v průvodci vyberte metodu podporovanou typem připojení. Nastavení a dostupné možnosti na této stránce se liší v závislosti na vybraném typu připojení. Další informace najdete v tématu [referenční informace o metodách ověřování](#bkmk_auth).

1. Pokud vaše síť VPN používá proxy server, na stránce **nastavení proxy** vyberte jednu z možností, jak je to vhodné pro vaše prostředí. Pak zadejte informace o konfiguraci proxy serveru.

1. Stránka **aplikace** se vztahuje pouze na profily Windows 10. Přidejte desktopové a univerzální aplikace, které se automaticky připojovat k této síti VPN. Typ aplikace určuje identifikátor aplikace:

    - V případě *desktopové aplikace*zadejte cestu k souboru aplikace.

    - V případě *univerzální aplikace*zadejte název řady balíčků (PFN). Informace o tom, jak najít PFN pro aplikaci, najdete v tématu [vyhledání názvu rodiny balíčků pro síť VPN pro jednotlivé aplikace](find-a-pfn-for-per-app-vpn.md).

    Můžete taky nakonfigurovat možnost, aby **Tato síť VPN mohla používat jenom uvedené aplikace**.

    > [!IMPORTANT]
    > Zabezpečte všechny seznamy přidružených aplikací, které kompilujete pro konfiguraci sítě VPN pro jednotlivé aplikace. Pokud váš seznam změní neoprávněný uživatel a Vy ho naimportujete do seznamu aplikací sítě VPN pro jednotlivé aplikace, můžete jim povolit přístup k síti VPN pro aplikace, které nemají přístup.

1. Stránka **hranice** se vztahuje pouze na profily Windows 10, aby bylo možné konfigurovat hranice sítě VPN. Můžete přidat následující možnosti:

    - **Pravidla síťového provozu**: nastavte protokoly, místní port, vzdálený port a rozsah adres, které chcete povolit pro připojení k síti VPN.  

        > [!Note]
        > Pokud nevytvoříte pravidlo pro provoz sítě, budou povolené všechny protokoly, porty a rozsahy adres. Po vytvoření pravidla se pro připojení VPN použijí jenom protokoly, porty a rozsahy adres, které určíte v tomto pravidle nebo v dalších pravidlech.

    - **Názvy a servery DNS**: servery DNS, které připojení VPN používá poté, co zařízení naváže připojení.

    - **Trasy**: síťové trasy, které používají připojení VPN. Vytvoření více než 60 tras může způsobit selhání zásad.

1. Dokončete průvodce.

Nový profil sítě VPN se zobrazí v uzlu **Profily sítě VPN** v pracovním prostoru **Prostředky a kompatibilita**.

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Odkaz na metodu ověřování

Dostupné metody ověřování sítě VPN závisí na typu připojení:

### <a name="certificates"></a>Certifikáty

Pokud se klientský certifikát ověřuje na serveru RADIUS, jako je server NPS (Network Policy Server), nastavte alternativní název subjektu v certifikátu na hlavní název uživatele.

Podporované typy připojení:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Kontrolní bod – mobilní síť VPN

### <a name="username-and-password"></a>Uživatelské jméno a heslo

Podporované typy připojení:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Kontrolní bod – mobilní síť VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Podporované typy připojení:

- Protokol SSL společnosti Microsoft (SSTP)
- Automaticky pomocí technologie Microsoft
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Protokol PEAP (Protected EAP) společnosti Microsoft

Podporované typy připojení:

- Protokol SSL společnosti Microsoft (SSTP)
- Automaticky pomocí technologie Microsoft
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Heslo zabezpečené technologií Microsoft (EAP-MSCHAP v2)

Podporované typy připojení:

- Protokol SSL společnosti Microsoft (SSTP)
- Automaticky pomocí technologie Microsoft
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Čipová karta nebo jiný certifikát

Podporované typy připojení:

- Protokol SSL společnosti Microsoft (SSTP)
- Automaticky pomocí technologie Microsoft
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Podporované typy připojení:

- Protokol SSL společnosti Microsoft (SSTP)
- Automaticky pomocí technologie Microsoft
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Použít certifikáty počítače

Podporované typy připojení:

- IKEv2

### <a name="additional-authentication-options"></a>Další možnosti ověřování

Pokud je verze klienta Windows podporuje, je k dispozici možnost **Konfigurace** metody ověřování. Tato možnost otevře okno Vlastnosti systému Windows, ve kterém můžete nakonfigurovat metodu ověřování.

V závislosti na vybraných možnostech se může zobrazit výzva k zadání dalších informací, například:

- **Pamatovat přihlašovací údaje uživatele při každém přihlašování**: přihlašovací údaje uživatele se pamatují, aby je uživatelé nemuseli zadávat při každém připojení.  

- **Vyberte klientský certifikát pro ověřování klientů**: vyberte dříve vytvořený profil certifikátu SCEP klienta k ověření připojení VPN. Další informace najdete v tématu [Vytvoření profilů certifikátů PFX](create-certificate-profiles.md).

## <a name="next-steps"></a>Další kroky

- Pro připojení k síti VPN třetích stran před nasazením profilu sítě VPN distribuujte aplikaci VPN. Pokud neprovedete nasazení aplikace, uživatelé se k tomu budou vyzváni při pokusu o připojení k síti VPN. Další informace najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).

- Nasaďte profil sítě VPN. Další informace najdete v tématu [nasazení profilů](deploy-wifi-vpn-email-cert-profiles.md).
