---
title: Nastavení Windows Hello pro firmy
titleSuffix: Configuration Manager
description: Přečtěte si, jak integrovat Windows Hello pro firmy s Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722232"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Nastavení Windows Hello pro firmy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1245704-->
Configuration Manager se integruje s Windows Hello pro firmy. (Tato funkce se dřív jmenovala jako Microsoft Passport for Work.) Windows Hello pro firmy je alternativní metoda přihlašování pro zařízení s Windows 10. Pomocí účtu služby Active Directory nebo Azure Active Directory (Azure AD) můžete nahradit heslo, čipovou kartu nebo virtuální čipovou kartu. Hello pro firmy umožňuje používat k přihlášení *gesto uživatele* místo hesla. Gesto uživatele může být PIN, biometrické ověřování nebo externí zařízení, jako je třeba čtečka otisků prstů.

> [!Important]  
> Počínaje verzí 1910 se ověřování na základě certifikátů s nastavením Windows Hello pro firmy v Configuration Manager nepodporuje. Další informace najdete v tématu [zastaralé funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Ověřování založené na klíčích je stále platné.
>
> Nasazení Active Directory Federation Services (AD FS) registrační autority (AD FS) je jednodušší, nabízí lepší uživatelské prostředí a má více deterministické možnosti Registrace certifikátů. Pro ověřování na základě certifikátů pomocí Windows Hello pro firmy použijte AD FS.
>
> Pro spoluspravovaná zařízení zvažte přesunutí [úlohy **zásad přístupu k prostředkům** ](../../comanage/workloads.md#resource-access-policies) do Intune. Pak tyto certifikáty spravujte pomocí zásad Intune. Další informace najdete v tématu [Jak přepínat úlohy](../../comanage/how-to-switch-workloads.md).

Další informace najdete v tématu [Windows Hello pro firmy](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager se integruje s Windows Hello pro firmy následujícími způsoby:  

- Určuje, která gesta uživatel může nebo nemůže používat k přihlášení.  

- Uložte ověřovací certifikáty ve zprostředkovateli úložiště klíčů (KSP) ve Windows Hello pro firmy. Další informace najdete v tématu [profily certifikátů](introduction-to-certificate-profiles.md).  

- Vytvořte a nasaďte profil Windows Hello pro firmy, abyste mohli řídit jeho nastavení na zařízeních s Windows 10 připojenými k doméně, na kterých běží klient Configuration Manager. Od verze 1910 nemůžete použít ověřování pomocí certifikátů. Při použití ověřování založeného na klíčích nemusíte nasazovat profil certifikátu.

## <a name="configure-a-profile"></a>Konfigurace profilu  

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů**, rozbalte **přístup k prostředkům společnosti**a vyberte uzel **profily Windows Hello pro firmy** .

1. Na pásu karet vyberte **vytvořit profil Windows Hello pro firmy** a spusťte Průvodce profilem.

1. Na stránce **Obecné** zadejte název a volitelný popis pro tento profil.

1. Na stránce **podporované platformy** vyberte verze operačního systému, na které se má tento profil vztahovat.

1. Na stránce **Nastavení** nakonfigurujte následující nastavení:

    - **Konfigurace Windows Hello pro firmy**: Určete, jestli tento profil povoluje, zakáže nebo nekonfiguruje Hello pro firmy.

    - **Použít čip TPM (Trusted Platform Module)**: čip TPM poskytuje další úroveň zabezpečení dat. Vyberte jednu z těchto hodnot:  

      - **Požadováno**: Windows Hello pro firmy může zřídit jenom zařízení s PŘÍSTUPNÝM čipem TPM.  

      - **Preferované**: zařízení se nejdřív pokusí použít čip TPM. Pokud není k dispozici, můžou použít softwarové šifrování.

    - **Metoda ověřování**: tuto možnost nastavte na **nenakonfigurované** nebo **na základě klíče**.

        > [!NOTE]
        > Počínaje verzí 1910 se ověřování na základě certifikátů s nastavením Windows Hello pro firmy v Configuration Manager nepodporuje.

    - **Nakonfigurujte minimální délku PIN kódu**: Pokud chcete pro PIN kód vyžadovat minimální délku, povolte tuto možnost a zadejte hodnotu. Je-li tato možnost povolena, `4`je použita výchozí hodnota.

    - **Nakonfigurujte maximální délku PIN kódu**: Pokud chcete pro PIN kód pro uživatele vyžadovat maximální délku, povolte tuto možnost a zadejte hodnotu. Pokud je povolená výchozí hodnota `127`, je.

    - **Vyžadovat vypršení platnosti kódu PIN (dny)**: Určuje počet dní, než uživatel musí změnit kód PIN zařízení.

    - **Zakázat opakované použití předchozích PIN kódů**: nepovolujte uživatelům používat PIN kódy, které používali dřív.

    - **Vyžadovat v PIN kódu velká písmena**: Určuje, jestli uživatelé musí v PIN kódu Windows Hello pro firmy obsahovat velká písmena. Vybírejte z těchto možností:  

      - **Povoleno**: uživatelé můžou ve svém PIN kódu používat velká písmena, ale nemusí být.

      - **Požadováno**: uživatelé musí ve svém PIN kódu použít aspoň jedno velké písmeno.  

      - **Nepovoleno**: uživatelé nemůžou ve svém PIN kódu používat velká písmena.  

    - **Vyžadovat v PIN kódu malá písmena**: Určuje, jestli uživatelé musí v PIN kódu Windows Hello pro firmy obsahovat malá písmena. Vybírejte z těchto možností:  

      - **Povoleno**: uživatelé můžou ve svém PIN kódu používat malá písmena, ale nemusí být.

      - **Požadováno**: uživatelé musí ve svém PIN kódu použít aspoň jedno malé písmeno.  

      - **Nepovoleno**: uživatelé nemůžou ve svém PIN kódu používat malá písmena.  

    - **Konfigurovat speciální znaky**: Určuje použití speciálních znaků v PIN kódu. Vybírejte z těchto možností:  

        > [!NOTE]
        > Mezi speciální znaky patří následující sada:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Povoleno**: uživatelé mohou ve svém PIN kódu používat speciální znaky, ale nemusí být.  

      - **Požadováno**: uživatelé musí ve svém PIN kódu použít aspoň jeden speciální znak.  

      - **Nepovoleno**: uživatelé nemůžou ve svém PIN kódu používat speciální znaky. Toto chování je také v případě, že nastavení není **nakonfigurováno**.  

    - **Konfigurovat použití číslic v PIN kódu**: Určuje použití čísel v PIN kódu. Vybírejte z těchto možností:

      - **Povoleno**: uživatelé můžou ve svém PIN kódu používat čísla, ale nemusí být.  

      - **Požadováno**: uživatelé musí ve svém PIN kódu zahrnovat aspoň jedno číslo.  

      - **Nepovoleno**: uživatelé nemůžou ve svém PIN kódu používat čísla.

    - **Povolit biometrická gesta**: Používejte biometrické ověřování, jako je rozpoznávání obličeje nebo otisk prstu. Tyto režimy jsou alternativou k PIN kódu pro Windows Hello pro firmy. Uživatelé pořád konfigurují PIN kód pro případ, že se biometrické ověřování nezdařilo.  

      Pokud je nastaveno na **Ano**, Windows Hello pro firmy umožňuje biometrické ověřování. Pokud je nastaveno na **ne**, Windows Hello pro firmy znemožní biometrické ověřování pro všechny typy účtů.  

    - **Použít rozšířené ochrany proti falšování identity**: konfiguruje rozšířené ochrany proti falšování identity na zařízeních, která je podporují. Pokud je tato hodnota nastavená na **Ano**, Windows vyžaduje, aby všichni uživatelé používali pro funkce obličeje ochranu proti falšování.  

    - **Používat přihlášení telefonem**: konfiguruje dvojúrovňové ověřování pomocí mobilního telefonu.

1. Dokončete průvodce.

Následující snímek obrazovky je příkladem nastavení profilu Windows Hello pro firmy:  

![Průvodce zásadami Windows Hello pro firmy zobrazující seznam dostupných nastavení](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Konfigurace oprávnění

1. Jako správce domény nebo ekvivalentní přihlašovací údaje se přihlaste ke zabezpečené pracovní stanici pro správu, která má nainstalovanou následující volitelnou funkci: RSAT: Active Directory Domain Services a Lightweight Directory Services Tools.

1. Otevřete konzolu **Uživatelé a počítače služby Active Directory** .

1. Vyberte doménu, přejděte do nabídky **Akce** a vyberte **vlastnosti**.

1. Přepněte na kartu **zabezpečení** a vyberte **Upřesnit**.

    > [!TIP]
    > Pokud nevidíte kartu **zabezpečení** , zavřete okno Vlastnosti. Přejděte do nabídky **zobrazení** a vyberte možnost **Pokročilé funkce**.

1. Vyberte **Přidat**.

1. Zvolte **Vyberte objekt zabezpečení** a zadejte `Key Admins`.

1. V seznamu **platí pro** vyberte **podřízené objekty uživatele**.

1. V dolní části stránky vyberte **Zrušit vše**.

1. V části **vlastnosti** vyberte **číst msDS-KeyCredentialLink**.

1. Výběrem **OK** uložte změny a zavřete všechna okna.

## <a name="next-steps"></a>Další kroky

[Profily certifikátů](introduction-to-certificate-profiles.md)
