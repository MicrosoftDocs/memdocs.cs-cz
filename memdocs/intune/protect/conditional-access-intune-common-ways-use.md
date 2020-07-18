---
title: Scénáře podmíněného přístupu
titleSuffix: Microsoft Intune
description: Přečtěte si, jak se podmíněný přístup Intune běžně používá pro podmíněný přístup na základě zařízení a aplikací.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1d4dacf29aa0c87a8356306d10bf05acbf3afb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462163"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Jaké jsou běžné způsoby použití podmíněného přístupu s Intune?

Existují dva typy podmíněného přístupu s Intune: podmíněný přístup podle zařízení a podle aplikace. K zavedení dodržování předpisů podmíněného přístupu ve vaší organizaci musíte nakonfigurovat související zásady dodržování předpisů. Podmíněný přístup se často používá k provádění akcí, jako je povolení nebo blokování přístupu k Exchangi, řízení přístupu k síti nebo integrace s řešením ochrany před mobilními hrozbami.
 
Informace v tomto článku vám pomohou pochopit, jak používat možnosti dodržování předpisů mobilního *zařízení* Intune a možnosti správy mobilních *aplikací* (MAM) Intune. 

> [!NOTE]
> Podmíněný přístup je Azure Active Directory funkce, která je součástí licence Azure Active Directory Premium. Intune tuto funkci vylepšuje tím, že do řešení přidává dodržování předpisů pro mobilní zařízení a správu mobilních aplikací. Uzel podmíněného přístupu, ke kterému se přistupuje z *Intune*, je stejný uzel, ke kterému se přistupuje z *Azure AD*.  

## <a name="device-based-conditional-access"></a>Podmíněný přístup podle zařízení

Intune a Azure Active Directory spolupracují, aby se zajistilo, že přístup k e-mailu, službám Office 365, aplikacím softwaru jako služby (SaaS) a místním [aplikacím](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)mají jenom spravovaná a vyhovující zařízení. Kromě toho můžete nastavit zásadu v Azure Active Directory tak, aby povolovala přístup ke službám Office 365 jenom počítačům připojeným k doméně nebo mobilním zařízením, která jsou zaregistrovaná v Intune.

Intune poskytuje schopnosti zásad dodržování předpisů pro zařízení, které vyhodnocují stav dodržování předpisů ze strany zařízení. Stav dodržování předpisů se oznamuje Azure Active Directory, který ho používá k vymáhání zásad podmíněného přístupu vytvořených v Azure Active Directory, když se uživatel pokusí získat přístup k prostředkům společnosti.

Zásady podmíněného přístupu na základě zařízení pro Exchange Online a další produkty Office 365 se konfigurují prostřednictvím [Azure Portal](../fundamentals/what-is-intune.md).

- Přečtěte si další informace o [vyžadování spravovaných zařízení s podmíněným přístupem v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).

- Přečtěte si další informace o [dodržování předpisů zařízením v Intune](device-compliance-get-started.md).

- Přečtěte si další informace o [podporovaných prohlížečích s podmíněným přístupem v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> Když v zařízeních s Androidem povolíte přístup na základě zařízení pro SharePoint Online nebo přístup k Exchangi Online, uživatelé musí na zaregistrovaném zařízení povolit možnost **Povolit přístup z prohlížeče** následujícím způsobem:
> 1. Spusťte **aplikaci Portál společnosti**.
> 2. Přejděte na stránku **Nastavení** prostřednictvím tlačítka se třemi tečkami (...) nebo hardwarového tlačítka nabídky.
> 3. Stiskněte tlačítko **Povolit přístup z prohlížeče**. 
> 4. V prohlížeči Chrome se odhlásí z Office 365 a restartuje Chrome.

### <a name="conditional-access-based-on-network-access-control"></a>Podmíněný přístup na základě řízení přístupu k síti

Intune se integruje s partnery, jako jsou Cisco ISE, Aruba Clear Pass a Citrix NetScaler, a poskytuje přístup k řízení přístupu na základě registrace v Intune a stavu dodržování předpisů zařízením.

Uživatelé můžou povolit nebo odepřít přístup k podnikovým prostředkům Wi-Fi nebo VPN na základě toho, jestli zařízení, které používáte, je spravované a dodržuje zásady dodržování předpisů zařízením Intune.

- Další informace o[integraci NAC s Intune](network-access-control-integrate.md).

### <a name="conditional-access-based-on-device-risk"></a>Podmíněný přístup na základě rizika zařízení

Intune ve spolupráci s dodavateli služeb Mobile Threat Defense poskytuje řešení zabezpečení pro zjišťování malwaru, trojských koňů a dalších hrozeb na mobilních zařízeních.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Jak funguje integrace Intune s ochranou před mobilními hrozbami

Pokud mají mobilní zařízení nainstalovaného agenta ochrany před mobilními hrozbami, odešle agent zprávy o stavu dodržování předpisů zpět do Intune, když se na mobilním zařízení zjistí hrozba.

Integrace Intune a ochrany před mobilními hrozbami hraje faktor v rozhodnutích podmíněného přístupu na základě rizika zařízení.

- Přečtěte si další informace o [Intune Mobile Threat Defense](mobile-threat-defense.md).

### <a name="conditional-access-for-windows-pcs"></a>Podmíněný přístup pro počítače s Windows

Podmíněný přístup pro počítače poskytuje podobné možnosti jako pro mobilní zařízení. Pojďme se seznámit s možnostmi použití podmíněného přístupu při správě počítačů s Intune.

#### <a name="corporate-owned"></a>Ve vlastnictví firmy

- **Připojeno k hybridní službě Azure AD:** Tato možnost se běžně používá v organizacích, které jsou dostatečně pohodlné, jak už spravují své počítače prostřednictvím zásad skupiny služby AD nebo Configuration Manager.

- **Připojené k doméně Azure AD a Správa Intune:** Tento scénář je určen pro organizace, které mají být nejprve cloudové služby (tedy primárně využívají cloudové služby, s cílem snížit využití místní infrastruktury) nebo pouze Cloud (bez místní infrastruktury). Funkce připojení k Azure AD funguje dobře v hybridním prostředí a umožňuje přístup ke cloudovým i místním aplikacím a prostředkům. Zařízení se připojí k Azure AD a zaregistruje se do Intune, které se dá použít jako kritéria podmíněného přístupu při přístupu k podnikovým prostředkům.

#### <a name="bring-your-own-device-byod"></a>Přineste si vlastní zařízení (BYOD)

- **Připojení k pracovišti a správa prostřednictvím Intune:** V tomto případě může uživatel připojit svoje osobní zařízení pro přístup k podnikovým prostředkům a službám. K získání zásad na úrovni zařízení, což je další možnost pro vyhodnocení kritérií podmíněného přístupu, můžete použít připojení k síti na pracovišti a registrovat zařízení do Intune MDM.

Další informace o [správě zařízení najdete v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview).

## <a name="app-based-conditional-access"></a>Podmíněný přístup založený na aplikacích

Intune a Azure Active Directory společně zajišťují, aby přístup k podnikovému e-mailu nebo jiným službám Office 365 měly jenom spravované aplikace.

- Přečtěte si další informace o [podmíněném přístupu založeném na aplikacích s Intune](app-based-conditional-access-intune.md).

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Podmíněný přístup Intune pro místní Exchange

Pomocí podmíněného přístupu můžete na základě zásad dodržování předpisů a stavu registrace zařízení povolit nebo zablokovat přístup k **místnímu Exchangi**. Když zásady podmíněného přístupu použijete v kombinaci se zásadami dodržování předpisů zařízením, povolí se přístup k místnímu Exchangi jen zařízením dodržujícím předpisy.

V podmíněném přístupu můžete nakonfigurovat upřesňující nastavení pro podrobnější řízení, třeba:

- Povolit nebo zakázat určité platformy

- Okamžitě zablokovat zařízení, která nespravuje Intune.

Při použití zásad dodržování předpisů zařízením a podmíněného přístupu se u všech zařízení používaných pro přístup k místnímu Exchangi kontroluje dodržování předpisů.

Pokud zařízení nesplňuje podmínky nastavené, koncový uživatel se provede procesem registrace zařízení za účelem vyřešení problému, který zařízení nedodržuje.

> [!NOTE]
> Od 1. července 2020 se podpora pro Exchange Connector zastaralá a nahrazuje ji pomocí [hybridního moderního ověřování](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) Exchange (HMA). Použití paměti HMA nevyžaduje instalaci Intune a použití konektoru Exchange. Díky této změně se uživatelské rozhraní pro konfiguraci a správu Exchange Connectoru pro Intune odebralo z centra pro správu Microsoft Endpoint Manageru, pokud už nepoužíváte Exchange Connector s vaším předplatným.
>
> Pokud máte ve svém prostředí nastavený Exchange Connector, zůstane klient Intune pro jeho použití podporovaný a vy budete mít přístup k uživatelskému rozhraní, které podporuje jeho konfiguraci. Další informace najdete v tématu věnovaném [instalaci konektoru Exchange On-Premises Connector](../protect/exchange-connector-install.md) . Můžete dál používat konektor nebo nakonfigurovat HMA a pak konektor odinstalovat.
>
> Hybridní moderní ověřování nabízí funkce, které dříve poskytoval Exchange Connector pro Intune: mapování identity zařízení na záznam Exchange.  Toto mapování se teď stane mimo konfiguraci, kterou provedete v Intune, nebo požadavek konektoru Intune, aby se zajistilo přemostění Intune a Exchange. S HMA je nutné odebrat požadavek na použití konfigurace specifické pro Intune (konektor).


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Jaká je role Intune?

Intune vyhodnocuje a spravuje stav zařízení.

#### <a name="whats-the-exchange-server-role"></a>Co je role Exchange serveru?

Exchange Server poskytuje rozhraní API a infrastrukturu pro přesunutí zařízení do karantény.

> [!IMPORTANT]
> Mějte na paměti, že uživatel, který zařízení používá, musí mít profil dodržování předpisů a přiřazenou licenci Intune, aby bylo možné zařízení vyhodnotit pro dodržování předpisů. Pokud uživatel nemá nasazené žádné zásady dodržování předpisů, považuje se zařízení za dodržující předpisy a žádná omezení přístupu se neuplatní.

## <a name="next-steps"></a>Další kroky

[Postup konfigurace podmíněného přístupu v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

[Nastavení zásad podmíněného přístupu k aplikacím](app-based-conditional-access-intune-create.md)

[Vytvoření zásady podmíněného přístupu pro místní Exchange](conditional-access-exchange-create.md)
