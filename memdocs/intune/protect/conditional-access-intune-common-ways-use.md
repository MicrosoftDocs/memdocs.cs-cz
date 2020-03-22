---
title: Scénáře podmíněného přístupu
titleSuffix: Microsoft Intune
description: Přečtěte si, jak se podmíněný přístup Intune běžně používá pro podmíněný přístup na základě zařízení a aplikací.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2019
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
ms.openlocfilehash: 9c8c78106125b45f52b45cb5fc6494b8e13b7a15
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084952"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Jaké jsou běžné způsoby použití podmíněného přístupu s Intune?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]


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
> 3. Stiskne tlačítko **Povolit přístup z prohlížeče** . 
> 4. V prohlížeči Chrome se odhlaste z Office 365 a znovu spusťte Chrome.

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

#### <a name="how-conditional-access-for-exchange-on-premises-works"></a>Jak podmíněný přístup pro místní Exchange funguje

Podmíněný přístup pro místní Exchange funguje jinak než zásady založené na podmíněném přístupu Azure. Intune Exchange On-Premises Connector nainstalujete k přímé interakci se systémem Exchange Server. Konektor Intune Exchange si vyžádá všechny záznamy Exchange Active Sync (EAS), které existují na serveru Exchange, aby Intune mohl tyto záznamy EAS namapovat na záznamy zařízení Intune. Tyto záznamy jsou zařízení zaregistrovaná a rozpoznaná službou Intune. Tento proces povolí nebo zablokuje přístup k e-mailu.

Pokud je záznam EAS nový a Intune o něm není vědět, Intune vydá rutinu (příkaz-let), která přesměruje Exchange Server, aby blokoval přístup k e-mailu. Níže najdete další podrobnosti o tom, jak tento proces funguje:

![Vývojový diagram místního Exchange s podmíněným přístupem](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. Uživatel se pokusí o přístup k podnikovému e-mailu, který je hostovaný na místním Exchangi 2010 SP1 nebo novějším.

2. Pokud zařízení nespravuje Intune, bude přístup k e-mailu blokovaný. Intune pošle klientovi EAS oznámení o blokování.

3. EAS obdrží oznámení o zablokování, přesune zařízení do karantény a odešle e-mail o karanténě s kroky k nápravě, které obsahují odkazy, aby uživatelé mohli svá zařízení zaregistrovat.

4. Provede se proces připojení k pracovišti, který je prvním krokem k tomu, aby se zařízení spravovalo pomocí Intune.

5. Zařízení se zaregistruje v Intune.

6. Intune namapuje záznam EAS na záznam zařízení a uloží stav dodržování předpisů zařízením.

7. ID klienta EAS se zaregistruje prostřednictvím procesu registrace zařízení Azure AD. Tím se vytvoří vztah mezi záznamem zařízení v Intune a ID klienta EAS.

8. Registrace zařízení Azure AD uloží informace o stavu zařízení.

9. Pokud uživatel splňuje zásady podmíněného přístupu, Intune vydá rutinu prostřednictvím Intune Exchange Connectoru, která umožňuje synchronizaci poštovní schránky.

10. Server Exchange odešle oznámení klientovi EAS, aby uživatel získal přístup k e-mailu.


#### <a name="whats-the-intune-role"></a>Jaká je role Intune?

Intune vyhodnocuje a spravuje stav zařízení.

#### <a name="whats-the-exchange-server-role"></a>Co je role Exchange serveru?

Exchange Server poskytuje rozhraní API a infrastrukturu pro přesunutí zařízení do karantény.

> [!IMPORTANT]
> Mějte na paměti, že uživatel, který zařízení používá, musí mít profil dodržování předpisů a přiřazenou licenci Intune, aby bylo možné zařízení vyhodnotit pro dodržování předpisů. Pokud uživatel nemá nasazené žádné zásady dodržování předpisů, považuje se zařízení za dodržující předpisy a žádná omezení přístupu se neuplatní.

## <a name="next-steps"></a>Další kroky

[Postup konfigurace podmíněného přístupu v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

[Nastavení zásad podmíněného přístupu na základě aplikace](app-based-conditional-access-intune-create.md)

[Jak nainstalovat místní konektor Exchange v Intune](exchange-connector-install.md)

[Vytvoření zásady podmíněného přístupu pro místní Exchange](conditional-access-exchange-create.md)
