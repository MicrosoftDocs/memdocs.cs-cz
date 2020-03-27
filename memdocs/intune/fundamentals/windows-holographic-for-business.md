---
title: Použití zařízení s Windows Holographic v Microsoft Intune – Azure | Microsoft Docs
description: V Microsoft Intune můžete spravovat a plnit různé úkoly spojené se zařízeními se systémem Windows Holographic pro firmy a HoloLens, jako je konfigurace Portálu společnosti, vytvoření zásady dodržování předpisů, přizpůsobení nastavení OMA-URI, nasazení aplikací, zařazení zařízení do skupin, vytváření profilů, omezení zařízení, povolení aktualizací softwaru, nastavení podmínek a ujednání, konfigurace nastavení VPN a Wi-Fi a použití funkce Hello pro firmy.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 585a2f17-106b-4f02-adf7-05f08a92dbc1
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 44cae6e1e7fdd310a6053cbcb6f19371263d0161
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326621"
---
# <a name="manage-and-use-different-device-management-features-on-windows-holographic-and-hololens-devices-with-intune"></a>Spravovat a využívat funkce správy různých zařízení na Windows Holographic a zařízení HoloLens s Intune

Microsoft Intune zahrnuje mnoho funkcí pro usnadnění správy zařízení s Windows Holographic pro firmy, jako [Microsoft HoloLens](https://docs.microsoft.com/hololens/). Pomocí Intune můžete potvrdit, že jsou zařízení v souladu s pravidly vaší organizace, a můžete zařízení přizpůsobit tak, že přidáte profil sítě VPN nebo Wi-Fi. Další klíčovou funkcí je použití zařízení jako veřejného terminálu a spuštění konkrétní aplikace nebo konkrétní sady aplikací.

Úlohy v tomto článku vám pomůžou při správě, přizpůsobování a zabezpečování zařízení s Windows Holographic pro firmy, včetně aktualizací softwaru a použití Windows Hello pro firmy.

Pokud chcete používat zařízení s Windows Holographic v Intune, vytvořte profil Upgrade edice. Tento aktualizační profil upgraduje zařízení z Windows Holographic na Windows Holographic for Business. V případě zařízení Microsoft HoloLens můžete požadovanou licenci pro upgrade získat zakoupením edice Commercial Suite. Další informace najdete v tématu [Upgrade zařízení s Windows Holographic na Windows Holographic for Business](../configuration/holographic-upgrade.md).

## <a name="azure-active-directory"></a>Azure Active Directory

Azure Active Directory (AD) představuje skvělý prostředek, který vám pomůže se správou a řízením zařízení, na nichž běží Windows Holographic for Business. Pomocí Intune a Azure AD můžete: 

- **[Připojit zařízení k Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)** : v Azure Active Directory (AD) můžete přidat vlastní zařízení s Windows 10, včetně zařízení s Windows holografickým pro firmy. Tato funkce umožňuje službě Azure AD řídit zařízení. Pomůže vám zajistit, že uživatelé používají prostředky společnosti ze zařízení, která jsou v souladu s vámi stanovenými standardy zabezpečení a dodržování předpisů.

  Další podrobnosti najdete [v správě zařízení ve službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/overview) .

- **[Hromadně registrovat zařízení s Windows](../enrollment/windows-bulk-enroll.md)** : K Azure Active Directory (AD) a Intune můžete připojit větší počet nových zařízení s Windows. Tato funkce se označuje jako hromadná registrace a využívá zřizovací balíčky. Tyto balíčky připojí zařízení s Windows Holographic for Business k tenantovi Azure AD a zaregistrují je v Intune.

## <a name="company-portal"></a>Portál společnosti

**[Konfigurace aplikace Portál společnosti](../apps/company-portal-app.md)**

Intune poskytuje aplikaci Portál společnosti pro přístup uživatelů k firemním datům, registraci zařízení, instalaci aplikací, možnost kontaktovat oddělení IT apod. Aplikaci Portál společnosti můžete přizpůsobit pro zařízení s Windows Holographic for Business.

Pomocí aplikace Portál společnosti můžete také provádět následující akce:

- [Odebrání zařízení z Intune](../user-help/unenroll-your-device-from-intune-windows.md) pomocí aplikace Nastavení nebo Portál společnosti
- [Přejmenování zařízení](../user-help/rename-your-device-cpapp.md)
- [Instalace aplikací](../user-help/install-apps-cpapp-windows.md) na zařízení
- [Ruční synchronizace zařízení](../user-help/sync-your-device-manually-windows.md) v aplikaci Nastavení nebo Portál společnosti

## <a name="compliance-policy"></a>zásady dodržování předpisů

**[Vytvoření zásady dodržování předpisů pro zařízení](../protect/compliance-policy-create-windows.md)**

Zásady dodržování předpisů jsou pravidla a nastavení, která musí zařízení dodržovat, aby vyhovovala. Pomocí těchto zásad s podmíněným přístupem Zablokujte přístup k prostředkům společnosti pro zařízení, která nedodržují předpisy. V Intune můžete vytvářet zásady dodržování předpisů, které povolí nebo zablokují přístup zařízením s Windows Holographic for Business. Můžete například vytvořit zásadu, která vyžaduje, aby byl povolen nástroj BitLocker.

Další informace najdete v tématu **[Začínáme se zásadami dodržování předpisů](../protect/device-compliance-get-started.md)** .

## <a name="deploy-and-manage-apps"></a>Nasazení a správa aplikací

**[Přidání aplikací do Intune](../apps/apps-add.md)**

V Intune můžete do zařízení s Windows Holographic for Business přidat aplikace. Existují různé způsoby nasazování aplikací:

- [Přidání aplikací z Microsoft Storu](../apps/store-apps-windows.md)
- [Přidání vytvořených aplikací](../apps/lob-apps-windows.md)
- [Přiřazení aplikací skupinám](../apps/apps-deploy.md)

Microsoft Intune může nasadit univerzální aplikace pro Windows na zařízení Microsoft HoloLens s Windows Holographic for Business. Balíčky aplikací můžete přímo nahrát na portálu Intune Azure nebo je můžete nasadit z Microsoft Storu pro firmy. Další informace o souvisejících oblastech najdete v těchto tématech:
- Pokud chcete nasadit obchodní aplikace pomocí portálu Intune Azure, přečtěte si téma [Přidání obchodních aplikací pro Windows do Microsoft Intune](../apps/lob-apps-windows.md).

    > [!NOTE]
    > Maximální velikost balíčku v Intune může být 8 GB. Tato velikost balíčku je dostupná jen pro obchodní aplikace nahrané do Intune.

- Pokud chcete nasadit aplikace pomocí Microsoft Storu pro firmy, přečtěte si téma [Správa aplikací zakoupených v Microsoft Storu pro firmy v Microsoft Intune](../apps/windows-store-for-business.md). 
- Pokud se chcete dozvědět informace o správě aplikací v Microsoft Intune, přečtěte si téma [Co je Správa aplikací v Microsoft Intune](../apps/app-management.md).
- Pokud se chcete dozvědět další informace o vývoji aplikací pro Microsoft HoloLens, přečtěte si téma [Aplikace hybridní reality pro Microsoft HoloLens](https://www.microsoft.com/hololens/apps). 

> [!NOTE]
> Zařízení HoloLens se systémem Windows 10 Holographic for Business 1607 nepodporují online licencované aplikace z Microsoft Storu pro firmy. Další informace najdete v tématu [Instalace aplikací na HoloLens](/hololens/holographic-store-apps).

## <a name="device-actions"></a>Akce zařízení

Intune obsahuje několik integrovaných akcí, které správcům IT umožňují provádět různé úlohy, a to buď místně na zařízení, nebo vzdáleně prostřednictvím Intune na portálu Azure Portal. Uživatelé můžou také z Portálu společnosti Intune vydat vzdálený příkaz zařízením v osobním vlastnictví, která jsou registrovaná v Intune.

Když používáte zařízení s Windows Holographic for Business, můžete používat tyto akce: 

- **[Vymazání](../remote-actions/devices-wipe.md#wipe)** : Akce **Vymazání** odebere zařízení z Intune a obnoví ho zpět do výchozího továrního nastavení. Tuto akci použijte v případě, že zařízení dáváte novému uživateli nebo dojde ke ztrátě či odcizení zařízení.

- **[Vyřazení](../remote-actions/devices-wipe.md#retire)** : Akce **Vyřazení** odebere zařízení z Intune. Zároveň se odeberou i data spravovaných aplikací, nastavení a e-mailové profily přiřazené přes Intune. Osobní data uživatele zůstanou na zařízení.

- **[Synchronizace zařízení za účelem získání nejnovějších zásad a akcí](../remote-actions/device-sync.md)** : Akce **Synchronizovat** vynutí okamžité připojení zařízení k Intune. Jakmile se zařízení připojí, začne okamžitě přijímat veškeré čekající akce nebo zásady, které mu byly přiřazeny. Tato funkce vám pomůže ověřit a vyřešit potíže se zásadami, které jste přiřadili, bez čekání na další plánované vrácení se změnami.

**Pokud se chcete dozvědět něco o správě zařízení pomocí portálu Azure Portal, najdete užitečné informace v článku [Co je správa zařízení v Microsoft Intune](../remote-actions/device-management.md)** . 

## <a name="device-categories-and-groups"></a>Kategorie a skupiny zařízení

**[Zařazení zařízení do skupin](../enrollment/device-group-mapping.md)**

V Intune můžete vytvářet kategorie zařízení, abyste podle nich mohli zařízení automaticky přidávat do skupin. Příklad: Prodej, Účetnictví, Lidské zdroje apod. Cílem je usnadnit správu zařízení s Windows Holographic for Business.

## <a name="device-configuration-profiles"></a>Konfigurační profily zařízení

**[Začínáme s konfiguračními profily](../configuration/device-profiles.md)a [Přehled profilů](../configuration/device-profile-create.md)**

Intune obsahuje nastavení a funkce, které můžete různým zařízením v organizaci povolit nebo zakázat. Tato nastavení a funkce se spravují pomocí profilů. Můžete například vytvořit profil, který umožňuje Cortana nebo na zařízeních s Windows holografickým pro firmy používat inteligentní obrazovku Microsoft Defenderu.

V profilech můžete k přizpůsobení některých nastavení, vytvoření omezení pro zařízení a konfiguraci sítí VPN a Wi-Fi použít OMA-URI.

### <a name="custom-device-settings"></a>[Vlastní nastavení zařízení](../configuration/custom-settings-windows-holographic.md)

Pokud chcete nakonfigurovat nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier), můžete v Intune vytvořit vlastní profil. Nastavení OMA-URI se používá k ovládání různých funkcí zařízení s Windows Holographic for Business, jako je povolení VPN nebo kontrola aktualizací ve službě Microsoft Update.

### <a name="configure-kiosk-mode"></a>[Konfigurace beznabídkového režimu](../configuration/kiosk-settings-holographic.md)

Pomocí funkcí sdíleného nebo hostovaného počítače dostupných v Intune můžete na zařízeních s Windows Holographic for Business nakonfigurovat beznabídkový režim. Na těchto zařízení může běžet jen jedna aplikace (beznabídkový režim s jednou aplikací), nebo několik aplikací (beznabídkový režim s více aplikacemi).

### <a name="device-restrictions"></a>[Omezení zařízení](../configuration/device-restrictions-windows-holographic.md)

Omezení zařízení umožňují ovládat různá nastavení a funkce zařízení, jako je povinné heslo, instalace aplikací z [Microsoft Storu](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps), zapnutí technologie Bluetooth atd. Tato omezení se vytvářejí v profilu Intune. Profil můžete použít u více zařízení, na kterých běží Windows Holographic for Business.

### <a name="configure-vpn"></a>[Konfigurace VPN](../configuration/vpn-settings-configure.md)

Virtuální privátní sítě (VPN) umožňují uživatelům zabezpečený vzdálený přístup k firemní síti. V Intune můžete vytvořit profil VPN, ve kterém budou mít zařízení s Windows Holographic for Business určité nastavení. Můžete třeba vytvořit profil VPN, kde budou mít všechna zařízení s Windows Holographic for Business typ připojení Citrix VPN.

### <a name="configure-wi-fi"></a>[Konfigurace Wi-Fi](../configuration/wi-fi-settings-configure.md)

V Intune můžete také vytvořit profil Wi-Fi, kterým zařízením s Windows Holographic for Business přiřadíte nastavení bezdrátové sítě. Když zařízení přiřadíte profil Wi-Fi, získají koncoví uživatelé přístup k firemní síti bez konfigurace. Můžete třeba vytvořit síť Wi-Fi určenou jenom zařízením s Windows Holographic for Business.

## <a name="shared-multi-user-devices"></a>Sdílená zařízení s více uživateli

[Sdílená zařízení](../configuration/shared-user-device-settings-windows-holographic.md)

Zařízení s Windows holografickým pro firmy, jako je například Microsoft HoloLens, můžou mít více uživatelů. Intune zahrnuje nastavení pro řízení různých funkcí na těchto sdílených zařízeních, jako je řízení spotřeby, použití místního úložiště a správy účtů. Konfigurační profily lze také použít u zařízení s různými operačními systémy. Například skupina zařízení může mít zařízení, která spouštějí RS2 a RS3 ve stejné skupině.

## <a name="software-updates"></a>Aktualizace softwaru

**[Správa softwarových aktualizací](../protect/windows-update-for-business-configure.md)**

V Intune je funkce Aktualizační kanály zařízení s Windows 10. Tyto aktualizační kanály zahrnují skupinu nastavení, která určují, jak se budou aktualizace instalovat. Pro instalaci aktualizací můžete třeba vytvořit časové období údržby nebo můžete zvolit, že po instalaci aktualizací chcete zařízení restartovat. Aktualizační kanál můžete použít pro více zařízení s Windows Holographic for Business.

## <a name="terms-and-conditions"></a>Podmínky a ujednání

**[Nastavení podmínek a ujednání společnosti pro přístup uživatelů](../enrollment/terms-and-conditions-create.md)**

Před registrací zařízení a získáním přístupu k firemním aplikacím (včetně e-mailu) můžete vyžadovat, aby uživatelé přijali podmínky a ujednání společnosti. V Intune definujete, jak se podmínky a ujednání zobrazí v aplikaci Portál společnosti, a také tyto podmínky a ujednání přiřadíte zařízením s Windows Holographic for Business.

## <a name="windows-hello-for-business"></a>Windows Hello pro firmy

**[Použití Windows Hello pro firmy](../protect/windows-hello.md)**

Hello pro firmy je alternativní přihlašovací metoda, která k nahrazení hesla, čipové karty nebo virtuální čipové karty používá účet Azure Active Directory. Hello pro firmy umožňuje zařízením s Windows Holographic for Business používat k přihlášení PIN o minimální délce, kterou sami určíte.

## <a name="next-steps"></a>Další kroky

[Nastavte Intune](setup-steps.md).
