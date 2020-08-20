---
title: Partneři dodržování předpisů zařízením v Microsoft Intune – Azure | Microsoft Docs
description: Jako zdroj dat o dodržování předpisů pro zařízení, která spravujete pomocí Intune, použijte partnera dodržování předpisů zařízením třetí strany.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643699"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Podpora partnerů dodržování předpisů zařízením třetích stran v Intune

Microsoft Intune může přidat data o stavu dodržování předpisů do služby Azure Active Directory (Azure AD) pro zařízení, která spravujete, s jedním nebo více partnery pro dodržování předpisů zařízeními třetích stran. V této konfiguraci je možné použít data o dodržování předpisů z těchto zařízení se zásadami podmíněného přístupu.

Ve výchozím nastavení je Intune nastavený jako autorita pro správu mobilních zařízení (MDM) pro vaše zařízení. Když přidáte partnera dodržování předpisů do Azure AD a Intune, konfigurujete tohoto partnera jako zdroj autority správy mobilních zařízení (MDM) pro zařízení, která přiřadíte k danému partnerovi prostřednictvím skupiny uživatelů Azure AD.

Pokud chcete povolit použití dat z partnerů dodržování předpisů zařízením, proveďte následující úlohy:

1. **Nakonfigurujte Intune tak, aby fungovala s partnerem dodržování předpisů zařízením**, a pak nakonfigurujte skupiny uživatelů, jejichž zařízení spravuje tento partner pro dodržování předpisů.

2. **Nakonfigurujte partnera dodržování předpisů, aby odesílal data do Intune**.

3. **Zaregistrujte zařízení s iOS nebo Androidem pro tohoto partnera pro dodržování předpisů zařízením**.

Po dokončení těchto úloh partner dodržování předpisů zařízením odešle podrobnosti o stavu zařízení do Intune. Intune pak přidá tyto informace do Azure AD. Například zařízení se stavem nedodržující předpisy mají tento stav přidané do záznamu zařízení ve službě Azure AD.

Stav dodržování předpisů se pak vyhodnotí podle zásad podmíněného přístupu, které jsou stejné jako data stavu dodržování předpisů pro zařízení spravovaná službou Intune.  Ve výchozím nastavení je Intune registrovaným partnerem dodržování předpisů pro iOS a Android. Když přidáte další partnery, můžete nastavit pořadí priority, abyste zajistili, že správný partner spravuje zařízení podle vašich obchodních potřeb.

## <a name="supported-device-compliance-partners"></a>Podporovaná partneři dodržování předpisů pro zařízení

Ve verzi Public Preview:

- Pracovní prostor VMware ONE UEM (dříve provide)

## <a name="prerequisites"></a>Předpoklady

- Předplatné, které se má Microsoft Intune, a přístup k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

- Předplatné pro partnera dodržování předpisů zařízením.

- Přečtěte si dokumentaci k partnerovi dodržování předpisů pro podporované platformy zařízení a další požadavky.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Konfigurace Intune pro práci se partnerem dodržování předpisů pro zařízení

Povolit podporu pro partnera dodržování předpisů zařízením pro použití dat o stavu dodržování předpisů z tohoto partnera se zásadami podmíněného přístupu.

### <a name="add-a-compliance-partner-to-intune"></a>Přidání partnera dodržování předpisů do Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Přejít k konektorům **pro správu tenanta**  >  **a**ke  >  **správě dodržování předpisů partnerským**tokenům  >  **přidejte partnera dodržování předpisů**.

   > [!div class="mx-imgBorder"]
   > ![Přidat partnera pro dodržování předpisů zařízením](./media/device-compliance-partners/add-compliance-partner.png)

3. Na stránce **základy** rozbalte rozevírací seznam **partner dodržování předpisů** a vyberte partnera, který přidáváte.

   - Pokud chcete použít pracovní prostor VMware ONE jako partner dodržování předpisů pro platformy iOS nebo Android, vyberte možnost **pracovní prostor VMware jedno mobilní dodržování předpisů**.

   Pak vyberte rozevírací nabídku pro **platformu**a vyberte platformu. macOS se v této verzi Preview nepodporuje.

   Jenom jeden partner na platformu, a to i v případě, že jste do Azure AD přidali víc partnerů pro dodržování předpisů.

4. V části **přiřazení**vyberte skupiny uživatelů, které budou mít zařízení spravovaná tímto partnerem. S tímto přiřazením změníte autoritu MDM pro příslušné zařízení, aby používala tohoto partnera. Uživatelům, kteří mají zařízení spravovaná partnerem, musí být také přiřazena licence k Intune.

5. Na stránce **Revize + vytvořit** zkontrolujte výběry a pak výběrem možnosti **vytvořit** dokončete tuto konfiguraci.

Vaše konfigurace se teď zobrazí na stránce správy dodržování předpisů partnerů.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Úprava konfigurace pro partnera dodržování předpisů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Klikněte na možnost konektory **pro správu tenanta**  >  **a**  >  **správu dodržování předpisů partnerům**a pak vyberte konfiguraci partnerského serveru, kterou chcete upravit. Konfigurace jsou seřazené podle typu platformy.

3. Na stránce **Přehled** konfigurace partnerského serveru výběrem **Možnosti vlastnosti** otevřete stránku vlastnosti, kde můžete upravit přiřazení.

4. Na stránce **vlastnosti** výběrem možnosti **Upravit** otevřete zobrazení přiřazení, kde můžete změnit skupiny, které budou používat tuto konfiguraci.

5. Vyberte **zkontrolovat + Uložit** **a uložte změny** .

6. *Tento krok platí jenom v případě, že použijete pracovní prostor VMware One*:

   V pracovním prostoru jedna UEM konzola musíte ručně synchronizovat změny, které jste uložili v centru pro správu Microsoft Endpoint Manageru. Dokud neprovedete ruční synchronizaci změn, pracovní prostor ONE UEM neznáte změny konfigurace a uživatelé v nově přiřazených skupinách neúspěšně nahlásili dodržování předpisů.

   Postup ruční synchronizace ze služeb Azure:
   1. Přihlaste se k pracovnímu prostoru VMware jedna konzola UEM.
   2. Přejít na **Nastavení**  >  **systém**  >  **Podniková integrace**  >  **adresářové služby**.
   3. Pro *synchronizaci služeb Azure*klikněte na **synchronizovat**.

      Všechny změny, které jste udělali od počáteční konfigurace nebo poslední ruční synchronizace, se synchronizují ze služeb Azure až po UEM.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Konfigurace partnera dodržování předpisů pro práci s Intune

Pokud chcete, aby mohl partner dodržování předpisů zařízením spolupracovat s Intune, musíte dokončit konfigurace specifické pro tohoto partnera. Informace o této úloze najdete v dokumentaci k příslušnému partnerovi:

- [Pracovní prostor VMware ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Registrace zařízení se systémem iOS nebo Android tomuto partnerovi pro dodržování předpisů zařízením

Postup registrace zařízení s tímto partnerem najdete v dokumentaci k partnerům pro dodržování předpisů zařízením. Po registraci zařízení a odeslání dat o dodržování předpisů partnerovi budou tato data předána do Intune a přidána do Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Monitorování zařízení, která spravuje partneři dodržování předpisů zařízením třetích stran

Po nakonfigurování partnerů pro dodržování předpisů zařízeními třetích stran a registraci zařízení v nich partner přepošle podrobnosti o dodržování předpisů do Intune. Až Intune obdrží tato data, můžete zobrazit podrobnosti o zařízeních v Azure Portal.

Přihlaste se k Azure Portal a v části zařízení **Azure AD**klikněte na  >  **Devices**  >  [**všechna zařízení**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Další kroky

K vytváření zásad dodržování předpisů pro zařízení použijte dokumentaci od svého partnera třetí strany.

- [Pracovní prostor VMware ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
