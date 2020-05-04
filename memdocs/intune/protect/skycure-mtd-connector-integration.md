---
title: Nastavení integrace služby Symantec s Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak nastavit řešení Symantec Endpoint Protection Mobile s Microsoft Intune, abyste mohli regulovat přístup mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 359448d9-2384-42ac-a21c-a25148c20a7b
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0810205e1b1e8b349d074560ec589b10e85443f1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80525225"
---
# <a name="set-up-symantec-endpoint-protection-mobile-integration-with-intune"></a>Nastavení integrace Symantec Endpoint Protection Mobile s Intune

Pomocí následujících kroků integrujete řešení Symantec Endpoint Protection Mobile (SEP Mobile) s Intune. Pokud chcete mít možnosti jednotného přihlašování, musíte aplikace SEP Mobile přidat do služby Azure AD.

> [!NOTE]
> Tento dodavatel ochrany před mobilními hrozbami není u neregistrovaných zařízení podporován.

## <a name="before-you-begin"></a>Před zahájením

### <a name="azure-ad-account-used-to-integrate-intune-and-sep-mobile"></a>Účet Azure AD použitý k integraci Intune a SEP Mobile

- Než začnete se základním nastavením SEP Mobile, ujistěte se, že máte správně nastavený účet Azure AD v [konzole pro správu Symantec Endpoint Protection Mobile](https://aad.skycure.com).
- K provedení integrace musí být účet Azure AD účtem globálního správce.
### <a name="network-setup"></a>Nastavení sítě

Můžete zajistit, aby byla síť správně nakonfigurovaná pro integraci s nastavením nástroje SEP Mobile, a to odkazem na článek od Symantecu s [konfigurací Správce SEP po instalaci](http://techdocs.broadcom.com/content/broadcom/techdocs/us/en/symantec-security-software/endpoint-security-and-management/endpoint-protection/all/Managing_a_Custom_Installation_3/Planning_the_Installation_0/network-architecture-considerations-v19543152-d23e65.html).

### <a name="full-integration-vs-read-only"></a>Úplná integrace vs. jen pro čtení

SEP Mobile podporuje dva způsoby integrace s Intune:

- **Integrace jen pro čtení (základní nastavení):** Vytvoří jenom inventář zařízení z adresáře Azure Active Directory a importuje je do konzoly pro správu Symantec Endpoint Protection Mobile.
<br>
  - Pokud nejsou políčka **Report the health and risk of devices to Intune** (Hlásit stav a riziko zařízení službě Intune) a **Also report security incidents to Intune** (Hlásit službě Intune také bezpečnostní incidenty) v konzole pro správu Symantec Endpoint Protection Mobile zaškrtnutá, znamená to, že integrace je jen pro čtení, a proto se ve službě Intune nikdy nezmění stav zařízení (vyhovující nebo nevyhovující).
<br></br>
- **Úplná integrace:** Umožňuje službě SEP Mobile odesílat podrobnosti o rizikových a bezpečnostních incidentech do služby Intune, která vytváří obousměrnou komunikaci mezi oběma cloudovými službami.

### <a name="how-are-the-sep-mobile-apps-used-with-azure-ad-and-intune"></a>Jak se používají aplikace SEP Mobile s Azure AD a Intune?

- **aplikace pro iOS:** Umožňuje koncovým uživatelům přihlásit se k Azure AD pomocí aplikace pro iOS/iPadOS.

- **Aplikace pro Android:** Umožňuje koncovým uživatelům přihlásit se do služby Azure AD pomocí aplikace pro Android.

- **Aplikace pro správu:** Toto je aplikace SEP Mobile pro více klientů Azure AD, která umožňuje komunikaci typu služba-služba s Intune.

## <a name="to-set-up-the-read-only-integration-between-intune-and-sep-mobile"></a>Nastavení integrace jen pro čtení mezi Intune a SEP Mobile

> [!IMPORTANT]
> Přihlašovací údaje správce SEP Mobile se musí skládat z e-mailového účtu, který patří platnému uživateli Azure Active Directory, jinak se přihlášení nezdaří. SEP Mobile k ověření správce používá jednotné přihlašování (SSO) služby Azure Active Directory.

1. Přejděte do [konzoly pro správu Symantec Endpoint Protection](https://aad.skycure.com).

2. Zadejte **přihlašovací údaje správce SEP Mobile** a pak zvolte **Continue** (Pokračovat).

3. Přejděte na **Settings** (Nastavení) a v části **Intune Integration** (Integrace Intune) vyberte **Basic Setup** (Základní nastavení).

4. Vedle **iOS App** (Aplikace pro iOS) zvolte **Add to Active Directory** (Přidat do AD).

    ![Obrázek konzoly pro správu Symantec Endpoint Protection Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

5. Když se otevře přihlašovací stránka, zadejte své přihlašovací údaje Intune a pak vyberte **Accept** (Přijmout).

    ![Obrázek výzvy pro přihlášení k Intune aplikace pro iOS/iPadOS](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

6. Po přidání aplikace do Azure AD se zobrazí indikace, že byla aplikace úspěšně přidána.

    ![Obrázek obrazovky pro dokončení aplikace pro iOS/iPadOS](./media/skycure-mtd-connector-integration/symantec-portal-basic-added.png)

7. Tyto kroky opakujte pro aplikaci **SEP Mobile pro Android** a aplikaci **správy**.

### <a name="add-an-azure-ad-security-group-into-sep-mobile"></a>Přidání skupiny zabezpečení Azure AD do SEP Mobile

Je potřeba přidat skupinu zabezpečení služby Azure AD, která obsahuje všechna zařízení s SEP Mobile.

- Zadejte a vyberte všechny skupiny zabezpečení se zařízeními, na kterých běží SEP Mobile, a pak uložte změny.

    ![Obrázek znázorňující skupiny uživatelů pro SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

Služba SEP Mobile sesynchronizuje zařízení, na kterých běží její služba ochrany před mobilními hrozbami, se skupinami zabezpečení Azure AD.

![Obrázek konfigurace skupiny zabezpečení v konzole pro správu mobilních zařízení SEP](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.png)

## <a name="to-set-up-the-full-integration-between-intune-and-sep-mobile"></a>Nastavení úplné integrace mezi Intune a SEP Mobile

### <a name="retrieve-the-directory-id-in-azure-ad"></a>Načtení ID adresáře v Azure AD

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com).

2. Do vyhledávacího pole zadejte „Active Directory“ a pak vyberte **Azure Active Directory**.

3. Zvolte **Properties** (Vlastnosti).

4. Vedle **ID adresáře** zvolte ikonu kopírování a pak identifikátor vložte do bezpečného umístění. Tento identifikátor budete potřebovat v pozdějším kroku.

    ![Obrázek znázorňující ID adresáře na portálu Azure Portal](./media/skycure-mtd-connector-integration/symantec-azure-portal-directory-ID.png)

### <a name="optional-create-a-dedicated-security-group-for-devices-that-need-to-run-the-sep-mobile-apps"></a>(Volitelné) Vytvoření vyhrazených skupin zabezpečení pro zařízení, která potřebují používat aplikace SEP Mobile
1. Na [portálu Azure Portal](https://portal.azure.com) v části **Spravovat** zvolte **Uživatelé a skupiny** a pak zvolte **Všechny skupiny**.

2. Vyberte tlačítko **Přidat**. Zadejte **Název** skupiny. V části **Typ členství** zvolte **Přiřazené**.

3. V okně **Členové** vyberte členy skupiny a pak zvolte tlačítko **Vybrat**.

4. V okně **Skupina** vyberte **Vytvořit**.

### <a name="set-up-the-integration-between-symantec-endpoint-protection-mobile-and-intune"></a>Nastavení integrace mezi Symantec Endpoint Protection Mobile a Intune

1. Přejděte do [konzoly pro správu Symantec Endpoint Protection](https://aad.skycure.com).

2. Zadejte **přihlašovací údaje správce SEP Mobile** a pak zvolte **Continue** (Pokračovat).

3. Přejít do části **integrace nastavení** > **integrace** > modulu EMM**Intune** > pro**Výběr** .

4. Do pole **Directory ID** (ID adresáře) vložte identifikátor adresáře, který jste zkopírovali z Azure Active Directory v předchozí části, a uložte nastavení.

    ![Obrázek znázorňující ID adresáře na portálu SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-directory-ID.png)

5. Přejít do části **Nastavení** > **integrace** > s nastavením**základní instalace** **Intune** > .

6. Vedle **iOS App** (Aplikace pro iOS) zvolte tlačítko **Add to Active Directory** (Přidat do AD).

    ![Obrázek znázorňující přidání aplikace pro iOS/iPadOS do služby Active Directory](./media/skycure-mtd-connector-integration/symantec-portal-basic-add.png)

7. Přihlaste se pomocí přihlašovacích údajů Azure Active Directory pro účet Office 365, který spravuje adresář.

8. Kliknutím na tlačítko **přijmout** přidejte aplikaci SEP Mobile iOS/iPadOS do Azure Active Directory.

    ![Obrázek znázorňující tlačítko Přijmout](./media/skycure-mtd-connector-integration/symantec-portal-basic-accept.png)

9. Stejný postup zopakujte pro **aplikaci pro Android** a **aplikaci pro správu**.

10. Vyberte všechny skupiny uživatelů, kteří potřebují používat aplikace SEP Mobile, například skupinu zabezpečení, kterou jste vytvořili.

    ![Obrázek znázorňující skupiny uživatelů pro SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-groups.png)

11. SEP Mobile sesynchronizuje zařízení ve vybraných skupinách a začne hlásit informace do Intune. Tato data můžete zobrazit v části Úplná integrace. Přejít do části **Settings** > **integrace** > nastavení s**úplnými integrací** **Intune** > .

     ![Obrázek znázorňující dokončenou úplnou integraci SEP Mobile](./media/skycure-mtd-connector-integration/symantec-portal-basic-status.PNG)
## <a name="next-steps"></a>Další kroky

[Nastavení aplikací SEP Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)
