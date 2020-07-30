---
title: Nastavení sítě VPN pro jednotlivé aplikace pro zařízení s iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na požadavky, vytvořte skupinu pro uživatele virtuální privátní sítě (VPN), přidejte profil certifikátu SCEP, nakonfigurujte profil sítě VPN pro jednotlivé aplikace a přiřaďte některé aplikace k profilu sítě VPN v Microsoft Intune na zařízeních s iOS/iPadOS. Součástí článku je také postup pro ověření připojení VPN na zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1d52e968b5e35490027c7887b597608e25476e24
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365453"
---
# <a name="set-up-per-app-virtual-private-network-vpn-for-iosipados-devices-in-intune"></a>Nastavení virtuální privátní sítě (VPN) pro jednotlivé aplikace v Intune pro zařízení s iOS/iPadOS

V Microsoft Intune můžete vytvářet a používat virtuální privátní sítě (VPN) přiřazené k aplikaci. Tato funkce se nazývá VPN pro aplikaci. Zvolíte spravované aplikace, které můžou používat vaši síť VPN na zařízeních spravovaných přes Intune. Při použití sítí VPN pro jednotlivé aplikace se koncoví uživatelé automaticky připojují přes síť VPN a získají přístup k prostředkům organizace, jako jsou například dokumenty.

Tato funkce platí pro:

- iOS 9 a novější
- iPadOS 13,0 a novější

Zkontrolujte si dokumentaci poskytovatele sítě VPN a zjistěte, jestli vaše síť VPN podporuje síť VPN pro jednotlivé aplikace.

V tomto článku se dozvíte, jak vytvořit profil sítě VPN pro jednotlivé aplikace a přiřadit tento profil k vašim aplikacím. Pomocí těchto kroků můžete pro koncové uživatele vytvořit bezproblémové prostředí sítě VPN pro jednotlivé aplikace. U většiny sítí VPN, které podporují síť VPN pro jednotlivé aplikace, uživatel otevře aplikaci a automaticky se připojí k síti VPN.

Některé sítě VPN umožňují ověřování uživatelského jména a hesla u sítě VPN pro jednotlivé aplikace. To znamená, že uživatelé musí zadat uživatelské jméno a heslo pro připojení k síti VPN.

> [!IMPORTANT]
> Při použití ověřování založeného na certifikátech se v iOS 13 nebrání profily sítě VPN pro jednotlivé aplikace v připojení k prostředím pro zápis uživatelů. Apple plánuje tuto opravu v budoucí verzi iOS.

> [!IMPORTANT]
> SÍŤ VPN pro jednotlivé aplikace není pro profily IKEv2 VPN pro iOS/iPadOS podporovaná.

## <a name="per-app-vpn-with-zscaler"></a>SÍŤ VPN pro jednotlivé aplikace s Zscaler

Zscaler Private Access (ZPA) se integruje s Azure Active Directory (Azure AD) pro ověřování. Pokud používáte ZPA, nepotřebujete profily [trusted certificate](#create-a-trusted-certificate-profile) [certifikátů SCEP nebo PKCS](#create-a-scep-or-pkcs-certificate-profile) (popsané v tomto článku). Pokud máte nastaven profil sítě VPN pro jednotlivé aplikace pro Zscaler, otevření jedné z přidružených aplikací se automaticky nepřipojí k ZPA. Místo toho se uživatel musí nejdřív přihlašovat do aplikace Zscaler. Vzdálený přístup je pak omezen na přidružené aplikace.

## <a name="prerequisites-for-per-app-vpn"></a>Předpoklady pro síť VPN pro jednotlivé aplikace

> [!IMPORTANT]
> Dodavatel VPN může mít další požadavky na síť VPN pro jednotlivé aplikace, jako je třeba konkrétní hardware nebo licencování. Nezapomeňte zkontrolovat jeho dokumentaci a splnit tyto požadavky dříve, než VPN pro aplikaci v Intune nastavíte.

Server VPN prokáže svoji identitu tak, že předloží certifikát, který musí zařízení bez vyzvání přijmout. Chcete-li potvrdit automatické schválení certifikátu, vytvořte profil důvěryhodného certifikátu, který obsahuje kořenový certifikát serveru VPN vystavený certifikační autoritou (CA).

### <a name="export-the-certificate-and-add-the-ca"></a>Exportujte certifikát a přidejte certifikační autoritu.

1. Na serveru VPN otevřete konzolu pro správu.
2. Ověřte, že server VPN používá ověřování pomocí certifikátů. 
3. Vyexportujte soubor s důvěryhodným kořenovým certifikátem. Soubor má příponu .cer a přidáte ho při vytváření profilu důvěryhodného certifikátu.
4. Přidejte název certifikační autority, která vystavila certifikát pro ověřování vůči serveru VPN.

    Pokud certifikační autorita, kterou zařízení prezentuje, odpovídá certifikační autoritě v seznamu důvěryhodných certifikačních autorit na serveru VPN, pak server VPN úspěšně ověří zařízení.

## <a name="create-a-group-for-your-vpn-users"></a>Vytvoření skupiny pro uživatele sítě VPN

Vytvořte nebo vyberte existující skupinu v Azure Active Directory (Azure AD) pro uživatele nebo zařízení, která používají síť VPN pro jednotlivé aplikace. Pokud chcete vytvořit novou skupinu, přečtěte si téma [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).

## <a name="create-a-trusted-certificate-profile"></a>Vytvoření profilu důvěryhodného certifikátu

Kořenový certifikát serveru VPN vystavený certifikační autoritou naimportujte do profilu vytvořeného v Intune. Profil důvěryhodného certifikátu instruuje zařízení iOS/iPadOS, aby automaticky důvěřovalo certifikační autoritě, kterou server VPN prezentuje.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **iOS/iPadOS**.
    - **Profil**: vyberte **důvěryhodný certifikát**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil sítě VPN pro iOS/iPadOS pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**vyberte ikonu složky a vyhledejte certifikát VPN (soubor. cer), který jste exportovali z konzoly pro správu sítě VPN.
8. Vyberte **Další**a pokračujte v vytváření profilu. Další informace najdete v tématu [Vytvoření profilu sítě VPN](vpn-settings-configure.md#create-the-profile).

    > [!div class="mx-imgBorder"]
    > ![Vytvoření profilu důvěryhodného certifikátu pro zařízení s iOS/iPadOS v Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-or-pkcs-certificate-profile"></a>Vytvoření profilu certifikátu SCEP nebo PKCS

Profil důvěryhodného kořenového certifikátu umožňuje zařízení automaticky důvěřovat serveru VPN. Certifikát SCEP nebo PKCS poskytuje přihlašovací údaje od klienta VPN iOS/iPadOS k serveru VPN. Certifikát umožňuje, aby se zařízení tiše ověřovalo bez výzvy k zadání uživatelského jména a hesla. 

Pokud chcete nakonfigurovat a přiřadit certifikát pro ověřování klientů, přečtěte si jeden z následujících článků:

- [Konfigurace infrastruktury pro podporu SCEP s Intune](../protect/certificates-scep-configure.md)
- [Konfigurace a správa certifikátů PKCS pomocí Intune](../protect/certficates-pfx-configure.md)

Nezapomeňte nakonfigurovat certifikát pro ověřování klientů. Ověřování klienta můžete nastavit přímo v profilech certifikátů SCEP (seznam**použití rozšířeného klíče** > **ověřování klientů**). V případě PKCS nastavte ověřování klientů v šabloně certifikátu v certifikační autoritě (CA).

> [!div class="mx-imgBorder"]
> ![Vytvoření profilu certifikátu SCEP v Microsoft Intune, včetně formátu názvu subjektu, použití klíče, rozšířeného použití klíče a dalších](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>Vytvoření profilu sítě VPN pro jednotlivé aplikace

Profil VPN obsahuje certifikát SCEP nebo PKCS s přihlašovacími údaji klienta, informace o připojení VPN a příznak sítě VPN pro jednotlivé aplikace, který umožňuje použití sítě VPN pro jednotlivé aplikace, kterou používá aplikace pro iOS/iPadOS.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Konfigurace profily**  >  **vytvořit profil**.
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **iOS/iPadOS**.
    - **Profil**: vyberte **VPN**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název vlastního profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil sítě VPN pro iOS/iPadOS pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. V **nastavení konfigurace**nakonfigurujte následující nastavení:

    - **Typ připojení**: vyberte aplikaci klienta VPN.
    - **Základní síť VPN**: Konfigurace nastavení. [nastavení sítě VPN pro iOS/iPadOS](vpn-settings-ios.md) obsahuje a popisuje všechna nastavení. Při použití sítě VPN pro jednotlivé aplikace se ujistěte, že jste nastavili následující vlastnosti, jak je uvedeno níže:

      - **Metoda ověřování**: vyberte **certifikáty**. 
      - **Certifikát ověřování**: Vyberte existující certifikát SCEP nebo PKCS > **OK**.
      - **Dělené tunelové propojení**: Pokud vyberete **Zakázat** , vynutí se použití tunelu VPN v případě, že je připojení VPN aktivní. 

      > [!div class="mx-imgBorder"]
      > ![V profilu sítě VPN pro jednotlivé aplikace zadejte připojení, IP adresu nebo plně kvalifikovaný název domény, metodu ověřování a dělené tunelové propojení v Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    Informace o dalších nastaveních najdete v tématu [nastavení sítě VPN pro iOS/iPadOS](vpn-settings-ios.md).

    - **Automatické připojení VPN**  >  **Typ automatické sítě VPN**  >  **Síť VPN pro jednotlivé aplikace**

      > [!div class="mx-imgBorder"]
      > ![V Intune nastavte pro zařízení s iOS/iPadOS automatickou síť VPN na síť VPN pro jednotlivé aplikace.](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. Vyberte **Další**a pokračujte v vytváření profilu. Další informace najdete v tématu [Vytvoření profilu sítě VPN](vpn-settings-configure.md#create-the-profile).

## <a name="associate-an-app-with-the-vpn-profile"></a>Přidružení aplikace k profilu sítě VPN

Po přidání profilu sítě VPN přidružte aplikaci a skupinu služby Azure AD k profilu.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **všechny aplikace**.
2. Vyberte aplikaci ze seznamu > **vlastnosti**  >  **přiřazení**  >  **Přidat skupinu**.
3. V **typu přiřazení**vyberte možnost **požadováno** nebo **k dispozici pro zaregistrovaná zařízení**.
4. Vyberte **zahrnuté skupiny**  >  **Vybrat skupiny, které se mají zahrnout** > vyberte skupinu [, kterou jste vytvořili](#create-a-group-for-your-vpn-users) (v tomto článku) > **Vybrat**.
5. V části **sítě VPN**vyberte profil sítě VPN pro jednotlivé aplikace [, který jste vytvořili](#create-a-per-app-vpn-profile) (v tomto článku).

    > [!div class="mx-imgBorder"]
    > ![Přiřaďte aplikaci k profilu sítě VPN pro jednotlivé aplikace v Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. Vyberte **OK**  >  **Uložit**.

Přidružení mezi aplikací a profilem se při dalším vrácení se změnami zařízení odebere, pokud existují všechny následující podmínky:

- Aplikace byla cílem záměru požadované instalace.
- Profil a aplikace cílí na stejnou skupinu.
- Odeberete konfiguraci sítě VPN pro jednotlivé aplikace z přiřazení aplikace.

Přidružení mezi aplikací a profilem přetrvá, dokud uživatel nepožaduje přeinstalaci z Portál společnosti, pokud existují všechny následující podmínky:

- Aplikace byla cílem záměru dostupné instalace.
- Profil a aplikace cílí na stejnou skupinu.
- Koncový uživatel požádal o instalaci aplikace z Portál společnosti, což vede k tomu, že se na zařízení nainstalují aplikace a profil.
- Z přiřazené aplikace jste odebrali konfiguraci sítě VPN pro aplikaci nebo jste ji změnili.

## <a name="verify-the-connection-on-the-iosipados-device"></a>Ověření připojení na zařízení se systémem iOS/iPadOS

Po nastavení sítě VPN pro jednotlivé aplikace a jejím přidružení k aplikaci ověřte, že připojení ze zařízení funguje.

### <a name="before-you-attempt-to-connect"></a>Než se pokusíte připojit

- Ujistěte se, že jste nasadili všechny výše uvedené zásady do stejné skupiny. V opačném případě prostředí VPN pro jednotlivé aplikace nebude fungovat.
- Pokud používáte aplikaci VPN Pulse Secure nebo vlastní klientská aplikace VPN, můžete použít tunelování vrstvy aplikace nebo paketů. U tunelování v aplikační vrstvě nastavte hodnotu **ProviderType** na **app-proxy**, u tunelování na úrovni paketů na **packet-tunnel**. Zkontrolujte dokumentaci poskytovatele sítě VPN a ujistěte se, že používáte správnou hodnotu.

### <a name="connect-using-the-per-app-vpn"></a>Připojení pomocí sítě VPN pro jednotlivé aplikace

Ověřte funkčnost bezdotykového prostředí – připojte se bez výběru sítě VPN nebo zadání svých přihlašovacích údajů. Bezdotykové prostředí znamená toto:

- Zařízení vás nevyzve k důvěřování serveru VPN. To znamená, že uživatel se nezobrazí v dialogovém okně **dynamického vztahu důvěryhodnosti** .
- Uživatel není muset zadávat přihlašovací údaje.
- Zařízení uživatele je připojené k síti VPN, když uživatel otevře jednu z přidružených aplikací.

## <a name="next-steps"></a>Další kroky

- Pokud chcete zkontrolovat nastavení pro iOS/iPadOS, přečtěte si téma [nastavení sítě VPN pro zařízení se systémem iOS/iPadOS v Microsoft Intune](vpn-settings-ios.md).
- Další informace o nastavení sítě VPN a Intune najdete v tématu [Konfigurace nastavení sítě VPN v Microsoft Intune](vpn-settings-configure.md).
