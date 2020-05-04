---
title: Vytváření profilů certifikátů PFX
titleSuffix: Configuration Manager
description: Naučte se používat soubory PFX v Configuration Manager ke generování certifikátů specifických pro uživatele, které podporují výměnu šifrovaných dat.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711172"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Vytvoření profilů certifikátů PFX pomocí certifikační autority

*Platí pro: Configuration Manager (Current Branch)*

Naučte se vytvořit profil certifikátu, který používá certifikační autoritu pro přihlašovací údaje. Tento článek popisuje konkrétní informace o profilech certifikátů PFX (Personal Information Exchange). Další informace o tom, jak vytvořit a nakonfigurovat tyto profily, najdete v tématu [profily certifikátů](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager umožňuje vytvořit profil certifikátu PFX pomocí přihlašovacích údajů vydaných certifikační autoritou. Můžete zvolit Microsoft nebo pověřit jako certifikační autoritu. Při nasazení do zařízení uživatelů soubory PFX generují uživatelem specifické certifikáty pro podporu výměny šifrovaných dat.

Pokud chcete importovat přihlašovací údaje certifikátu z existujících souborů certifikátů, přečtěte si téma [import profilů certifikátů PFX](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Požadavky

Než začnete s vytvářením profilu certifikátu, ujistěte se, že jsou připravené nezbytné požadavky. Další informace najdete v tématu [předpoklady pro profily certifikátů](../../protect/plan-design/prerequisites-for-certificate-profiles.md). Například pro profily certifikátů PFX potřebujete roli systému lokality [bod registrace certifikátu](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) .

## <a name="create-a-profile"></a>Vytvoření profilu  

1. V konzole Configuration Manager přejděte do pracovního prostoru **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**, rozbalte položku **přístup k prostředkům společnosti**a pak vyberte **profily certifikátů**.

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit profil certifikátu**.

1. Na stránce **Obecné** v **Průvodci vytvořením profilu certifikátu**zadejte následující informace:  

    - **Název**: Zadejte jedinečný název profilu certifikátu. Opět můžete použít maximálně 256 znaků.  

    - **Popis**: zadejte popis, který poskytne přehled profilu certifikátu, který ho pomůže identifikovat v konzole Configuration Manager. Opět můžete použít maximálně 256 znaků.  

1. Vybrat **Nastavení Personal Information Exchange – PKCS #12 (PFX) – vytvořit**. Tato možnost vyžádá certifikát jménem uživatele z připojené místní certifikační autority (CA). Vyberte certifikační autoritu: **Microsoft** nebo **Entrust Datacard**.

    > [!NOTE]
    > Možnost **importu** načte z existujícího certifikátu informace o vytvoření profilu certifikátu. Další informace najdete v tématu [import profilů certifikátů PFX](import-pfx-certificate-profiles.md).

1. Na stránce **podporované platformy** vyberte verze operačních systémů, které tento profil certifikátu podporuje. Další informace o podporovaných verzích operačních systémů pro vaši verzi Configuration Manager najdete v tématu [podporované verze operačních systémů pro klienty a zařízení](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. Na stránce **certifikační autority** vyberte bod registrace certifikátu (CRP) pro zpracování certifikátů PFX:

    1. **Primární lokalita**: vyberte server, který obsahuje roli CRP pro certifikační autoritu.
    1. **Certifikační autority**: vyberte příslušnou certifikační autoritu.

    Další informace najdete v tématu [infrastruktura certifikátů](../../protect/deploy-use/certificate-infrastructure.md).

Nastavení na stránce **certifikátu PFX** se liší v závislosti na vybrané certifikační autoritě na stránce **Obecné** :

- [CA Microsoftu](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Konfigurace nastavení **certifikátu PFX** pro certifikační autoritu Microsoftu

1. V poli **název šablony certifikátu**vyberte šablonu certifikátu.

1. Pokud chcete použít profil certifikátu pro podpis nebo šifrování S/MIME, povolte **použití certifikátu**.

    Když tuto možnost povolíte, budou všechny certifikáty PFX přidružené k cílovému uživateli na všech svých zařízeních. Pokud tuto možnost nepovolíte, každé zařízení obdrží jedinečný certifikát.  

1. Jako **Formát názvu subjektu** nastavte buď **běžný název** , nebo **plně rozlišující název**. Pokud si nejste jistí, která z nich se má použít, obraťte se na správce certifikační autority.

1. V poli **alternativní název subjektu**povolte **e-mailovou adresu** a **hlavní název uživatele (UPN)** podle potřeby vaší certifikační autority.

1. **Prahová hodnota obnovení**: Určuje, kdy se certifikáty automaticky Obnovují na základě procenta zbývající doby před vypršením platnosti.

1. Nastavte **dobu platnosti certifikátu** na životnost certifikátu.

1. Pokud bod registrace certifikátu Určuje pověření služby Active Directory, povolte **publikování služby Active Directory**.

1. Pokud jste vybrali jednu nebo více podporovaných platforem Windows 10:

    1. Nastavte **úložiště certifikátů systému Windows** na hodnotu **uživatel**. (Možnost **místní počítač** nepoužívá nasazení certifikátů, nevybírejte ho.)

    1. Vyberte jednoho z následujících **zprostředkovatelů úložiště klíčů (KSP)**:

        - **Instalovat do čipu Trusted Platform Module (TPM), pokud existuje**  
        - **Nainstalovat do čipu TPM (Trusted Platform Module), jinak selhání**
        - **Nainstalovat do Windows Hello pro firmy, jinak chyba**
        - **Instalovat do zprostředkovatele úložiště klíčů pro software**

1. Dokončete průvodce.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Konfigurace nastavení **certifikátu PFX** pro Entrust Datacard CA

1. V části **konfigurace digitálního ID**vyberte konfigurační profil. Správce pověření vytvoří možnosti konfigurace digitálního ID.

1. Pokud chcete použít profil certifikátu pro podpis nebo šifrování S/MIME, povolte **použití certifikátu**.

    Když tuto možnost povolíte, budou všechny certifikáty PFX přidružené k cílovému uživateli na všech svých zařízeních. Pokud tuto možnost nepovolíte, každé zařízení obdrží jedinečný certifikát.  

1. Pokud chcete mapovat svěřené tokeny pro **Formát názvu subjektu** na Configuration Manager pole, vyberte **Formát**.

    Dialogové okno **formátování názvu certifikátu** obsahuje seznam pověření pro proměnné konfigurace digitálního ID. Pro každou proměnnou pověřit vyberte odpovídající pole Configuration Manager.

1. Pro mapování **pojmenovaných alternativních názvů subjektů** do podporovaných proměnných LDAP zvolte **Formát**.

    Dialogové okno **formátování názvu certifikátu** obsahuje seznam pověření pro proměnné konfigurace digitálního ID. Pro každou proměnnou pověřit vyberte příslušnou proměnnou LDAP.

1. **Prahová hodnota obnovení**: Určuje, kdy se certifikáty automaticky Obnovují na základě procenta zbývající doby před vypršením platnosti.

1. Nastavte **dobu platnosti certifikátu** na životnost certifikátu.

1. Pokud bod registrace certifikátu Určuje pověření služby Active Directory, povolte **publikování služby Active Directory**.

1. Pokud jste vybrali jednu nebo více podporovaných platforem Windows 10:

    1. Nastavte **úložiště certifikátů systému Windows** na hodnotu **uživatel**. (Možnost **místní počítač** nepoužívá nasazení certifikátů, nevybírejte ho.)

    1. Vyberte jednoho z následujících **zprostředkovatelů úložiště klíčů (KSP)**:

        - **Instalovat do čipu Trusted Platform Module (TPM), pokud existuje**  
        - **Nainstalovat do čipu TPM (Trusted Platform Module), jinak selhání**
        - **Nainstalovat do Windows Hello pro firmy, jinak chyba**
        - **Instalovat do zprostředkovatele úložiště klíčů pro software**

1. Dokončete průvodce.

## <a name="deploy-the-profile"></a>Nasaďte profil

Po vytvoření profilu certifikátu je teď dostupný v uzlu **profily certifikátů** . Další informace o tom, jak ho nasadit, najdete v tématu [nasazení profilů přístupu k prostředkům](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Viz také

[Vytvoření nového profilu certifikátu](../../protect/deploy-use/create-certificate-profiles.md)

[Import profilů certifikátů PFX](import-pfx-certificate-profiles.md)

[Nasazení profilů sítí Wi-Fi a VPN, e-mailů a certifikátů](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
