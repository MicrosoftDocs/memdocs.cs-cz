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
ms.openlocfilehash: 270560e289a7b2078bdb21b75cfe227992e84f29
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88616261"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Podpora partnerů dodržování předpisů zařízením třetích stran v Intune

Microsoft Intune může přidat data o stavu dodržování předpisů do služby Azure Active Directory (Azure AD) pro zařízení, která spravujete, s jedním nebo více partnery pro dodržování předpisů zařízeními třetích stran. V této konfiguraci je možné použít data o dodržování předpisů z těchto zařízení se zásadami podmíněného přístupu.

Ve výchozím nastavení je Intune nastavený jako autorita pro správu mobilních zařízení (MDM) pro vaše zařízení. Když přidáte partnera dodržování předpisů do Azure AD a Intune, konfigurujete tohoto partnera jako zdroj autority správy mobilních zařízení (MDM) pro zařízení, která přiřadíte k danému partnerovi prostřednictvím skupiny uživatelů Azure AD.

Pokud chcete povolit použití dat z partnerů dodržování předpisů zařízením, proveďte následující úlohy:

1. **Přidejte partnera pro dodržování předpisů zařízením do Azure AD** a navažte tohoto partnera jako autoritu pro správu mobilních zařízení (MDM) pro příslušná zařízení.

2. **Nakonfigurujte Intune tak, aby fungovala s partnerem dodržování předpisů zařízením**, a pak nakonfigurujte skupiny uživatelů, jejichž zařízení spravuje tento partner pro dodržování předpisů.

3. **Nakonfigurujte partnera dodržování předpisů, aby odesílal data do Intune**.

4. **Zaregistrujte zařízení s iOS nebo Androidem pro tohoto partnera pro dodržování předpisů zařízením**.

Po dokončení těchto úloh partner dodržování předpisů zařízením odešle podrobnosti o stavu zařízení do Intune. Intune pak přidá tyto informace do Azure AD. Například zařízení se stavem nedodržující předpisy mají tento stav přidané do záznamu zařízení ve službě Azure AD.

Stav dodržování předpisů se pak vyhodnotí podle zásad podmíněného přístupu, které jsou stejné jako data stavu dodržování předpisů pro zařízení spravovaná službou Intune.  Ve výchozím nastavení je Intune registrovaným partnerem dodržování předpisů pro iOS a Android. Když přidáte další partnery, můžete nastavit pořadí priority, abyste zajistili, že správný partner spravuje zařízení podle vašich obchodních potřeb.

## <a name="supported-device-compliance-partners"></a>Podporovaná partneři dodržování předpisů pro zařízení

Ve verzi Public Preview:

- Pracovní prostor VMWare ONE UEM (dříve provide)

## <a name="prerequisites"></a>Předpoklady

- Předplatné, které se má Microsoft Intune, a přístup k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

- Předplatné pro partnera dodržování předpisů zařízením.

- Přečtěte si dokumentaci k partnerovi dodržování předpisů pro podporované platformy zařízení a další požadavky.

## <a name="add-support-in-azure-ad-for-a-device-compliance-partner"></a>Přidání podpory ve službě Azure AD pro partnera dodržování předpisů pro zařízení

Pokud chcete povolit podporu pro zařízení, která spravuje partneři dodržování předpisů zařízením třetích stran, musíte tohoto partnera přidat do *mobility (MDM a mam)* ve službě Azure AD. Ve výchozím nastavení je Intune už zaregistrovaný pro *mobilitu (MDM a mam)*.

### <a name="add-a-device-compliance-partner-to-azure-ad"></a>Přidání partnera pro dodržování předpisů pro zařízení do Azure AD

1. Přihlaste se k [Azure Portal](https://aad.portal.azure.com/) a do **Azure Active Directory**  >  **mobility (MDM a mam)**  >  **přidejte aplikaci**. ([Otevřete okno *mobilita (MDM a mam)* přímo](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility).)

2. V okně **Přidat aplikaci** vyberte dlaždici pro partnera dodržování předpisů zařízením a pak vyberte **Přidat**.

   - Pro *pracovní prostor jeden UEM*vyberte možnost **sledování videa podle VMware** .

3. V okně *mobilita (MDM a mam)* vyberte svého partnera dodržování předpisů a otevřete okno **Konfigurovat** a nakonfigurujte dostupné možnosti.  Mezi možnosti patří **obor uživatele MDM**, **Adresa URL podmínek použití MDM**a **Adresa URL zjišťování MDM**. Když je obor uživatele nastavený na **nějaké**, vybíráte skupiny uživatelů Azure AD, které můžou registrovat zařízení s tímto partnerem dodržování předpisů.

   Zařízení, která cílí na vybrané skupiny, budou používat partnera jako svoji autoritu MDM.

4. Výběrem **Uložit** dokončete konfiguraci partnera ve službě Azure AD. V dalším kroku přidáte partnera dodržování předpisů do Intune.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Konfigurace Intune pro práci se partnerem dodržování předpisů pro zařízení

Když je služba Azure AD nakonfigurovaná tak, aby podporovala partnera dodržování předpisů zařízením pro *mobilitu (MDM a mam)*, můžete nakonfigurovat Intune tak, aby spolupracovali s tímto partnerem. Tato konfigurace je nutná, pokud chcete použít data o stavu dodržování předpisů z tohoto partnera se zásadami podmíněného přístupu.

### <a name="add-a-compliance-partner-to-intune"></a>Přidání partnera dodržování předpisů do Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Přejít k konektorům **pro správu tenanta**  >  **a**ke  >  **správě dodržování předpisů partnerským**tokenům  >  **přidejte partnera dodržování předpisů**.

   > [!div class="mx-imgBorder"]
   > ![Přidat partnera pro dodržování předpisů zařízením](./media/device-compliance-partners/add-compliance-partner.png)

3. Na stránce **základy** rozbalte rozevírací seznam **partner dodržování předpisů** a vyberte partnera, který přidáváte. Pak vyberte rozevírací nabídku pro **platformu**a vyberte platformu.

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
   1. Přihlaste se k pracovnímu prostoru VMWare jedna konzola UEM.
   2. Přejít na **Nastavení**  >  **systém**  >  **Podniková integrace**  >  **adresářové služby**.
   3. Pro *synchronizaci služeb Azure*klikněte na **synchronizovat**.

      Všechny změny, které jste udělali od počáteční konfigurace nebo poslední ruční synchronizace, se synchronizují ze služeb Azure až po UEM.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Konfigurace partnera dodržování předpisů pro práci s Intune

Pokud chcete, aby mohl partner dodržování předpisů zařízením spolupracovat s Intune, musíte dokončit konfigurace specifické pro tohoto partnera. Informace o této úloze najdete v dokumentaci k příslušnému partnerovi:

- [Pracovní prostor VMware ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Registrace zařízení se systémem iOS nebo Android tomuto partnerovi pro dodržování předpisů zařízením

Postup registrace zařízení s tímto partnerem najdete v dokumentaci k partnerům pro dodržování předpisů zařízením. Po registraci zařízení a odeslání dat o dodržování předpisů partnerovi budou tato data předána do Intune a přidána do Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Monitorování zařízení, která spravuje partneři dodržování předpisů zařízením třetích stran

Po nakonfigurování partnerů pro dodržování předpisů zařízeními třetích stran a registraci zařízení v nich partner přepošle podrobnosti o dodržování předpisů do Intune. Až Intune obdrží tato data, můžete si Zobrazit podrobnosti o zařízeních v centru pro správu Microsoft Endpoint Manageru.  

Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a pak na **Endpoint Security**  >  **všechna zařízení**.  Zařízení, která spravuje Partnerská Autorita MDM jiného výrobce, zobrazí jména tohoto partnera ve sloupci **spravováno** .

> [!NOTE]
> V centru pro správu nejsou identifikováni všichni partneři dodržování předpisů třetí strany. Pokud vaše zařízení nejsou uvedena, můžete se přihlásit k [Azure Portal](https://portal.azure.com) , abyste měli přístup k předplatnému Intune a mohli je zobrazit.

Další informace o tomto zobrazení najdete v tématu [Správa zařízení](../protect/endpoint-security-manage-devices.md).

## <a name="next-steps"></a>Další kroky

- [Začínáme se zásadami dodržování předpisů pro zařízení](../protect/device-compliance-get-started.md)
