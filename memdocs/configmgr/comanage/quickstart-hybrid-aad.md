---
title: Použití Azure AD pro spolusprávu
titleSuffix: Configuration Manager
description: Pomocí Azure AD můžete využívat lepší produktivitu uživatelů a zabezpečení vašich prostředků v cloudových i Prem prostředích.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711522"
---
# <a name="use-azure-ad-for-co-management"></a>Použití Azure AD pro spolusprávu

V cloudu je identita novou rovinou ovládacího prvku. Azure Active Directory (Azure AD) umožňuje propojit uživatele, zařízení a aplikace v cloudových i místních prostředích. Registrace zařízení do Azure AD vám umožní zvýšit produktivitu vašich uživatelů a zabezpečení pro vaše prostředky. Zařízení ve službě Azure AD jsou základem pro spolusprávu i pro podmíněný přístup na základě zařízení.

Další informace o podmíněném přístupu na základě zařízení najdete v tématu [How to: vyžadovat spravovaná zařízení pro cloudovou aplikaci přístup s podmíněným přístupem.](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

V následujícím videu se vedoucí program Sandeep DEO a produkt marketingový manažer pro správu služby Active Directory, který je předmětem diskuze a ukázka Azure AD pro spolusprávu:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD nabízí dvě možnosti pro zařízení vlastněná společností, která vyhovují potřebám vaší organizace:  

- **Zařízení připojené k Azure AD**: Připojte zařízení s Windows 10 k Azure AD, aniž byste je museli připojit k místní službě Active Directory.  

  - Podporuje Windows 10

  - Nastavení bez nutnosti další konfigurace v místních prostředích  

  - Když ve službě Azure AD povolíte několik nastavení, můžete uživatelům povolit připojení zařízení k Azure AD prostřednictvím prostředí instalačního programu systému Windows (OOBE).  

  - Další informace najdete v tématu [Postup: plánování implementace služby Azure AD JOIN.](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Hybridní zařízení připojené k Azure AD**: Připojte stávající zařízení připojená k doméně k Azure AD  

  - Podporuje Windows 10, Windows 8.1 a Windows 7.

  - Nastavení pomocí deklarací identity AD FS nebo Azure AD Connect  

  - V případě Windows 10 se k připojení dojde v kontextu počítače, takže uživatelé nemusejí provádět další kroky.  

  - Další informace najdete v tématu [Plánování implementace služby hybrid Azure Active Directory JOIN](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) .  

Obě možnosti poskytují uživatelům podobné funkce. Je flexibilní, abyste si zvolili jednu z nich podle svých potřeb. Můžete například [získat přístup](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) k místním prostředkům z počítačů připojených k Azure AD i v případě, že nejsou připojené ke službě Active Directory.

Zařízení můžete připojit k Azure AD v různých prostředích bez ohledu na [metodu ověřování](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn). Například federované ověřování nebo cloudové ověřování.

Pokud už máte místní službu Active Directory, nastavení obou možností je jednoduché.

## <a name="benefits"></a>Výhody

Připojení zařízení k Azure AD poskytuje vaší organizaci tyto výhody:

### <a name="single-sign-on-to-cloud-resources"></a>Jednotné přihlašování ke cloudovým prostředkům

Na zařízeních připojených k Azure AD získáte integrované prostředí, které přistupuje k jakémukoli cloudu nebo místním prostředkům. Až se přihlásíte k počítači s Windows připojenému k Azure AD, získáte jednotné přihlašování ke všem aplikacím bez jakýchkoli dalších výzev k přihlášení.  

### <a name="windows-hello-for-business"></a>Windows Hello pro firmy

Windows Hello pro firmy přináší do Windows 10 silné ověřování bez hesla. Připojením zařízení ke službě Azure AD můžete povolit Windows Hello pro firmy napříč vaší uživatelskou základnou pro cloudové i místní prostředky. Windows Hello pro firmy eliminuje problémy se zapamatováním složitých hesel nebo neúmyslným zveřejněním. Proces přihlašování je jednoduchý a bezpečný.

Další informace najdete v tématu [Windows Hello pro firmy](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Podmíněný přístup podle zařízení

Povolte podmíněný přístup na základě stavu zařízení pro lepší ochranu dat vaší organizace. Podmíněný přístup na základě zařízení vyžaduje spravované zařízení. Toto zařízení musí být vyhovující zařízení nebo hybridní zařízení připojené k Azure AD. Pro zařízení připojená k Azure AD potřebujete Intune, aby zařízení označilo jako vyhovující. Ale pro zařízení připojená k hybridní službě Azure AD se k vyhodnocení podmíněného přístupu použije samotný stav zařízení. Spoluspráva poskytuje další výhody hodnocení dodržování předpisů prostřednictvím Intune pro hybridní zařízení připojená k Azure AD. Tato funkce zajišťuje, že konfigurace zařízení je nedotčená.

Další informace o podmíněném přístupu na základě zařízení najdete v tématu [How to: vyžadovat spravovaná zařízení pro cloudovou aplikaci přístup s podmíněným přístupem](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

### <a name="automatic-device-licensing"></a>Automatické licencování zařízení

Všechna zařízení s Windows 10 připojená k Azure AD procházejí prostřednictvím kontrol licencí. Tyto kontroly vám umožní automaticky upgradovat z verze pro na Enterprise prostřednictvím cloudu Microsoftu. Když odeberete příslušné předplatné z uživatele, zařízení automaticky sníží jeho licenci. Tato funkce poskytuje jediné podokno řízení pro správu licencí Windows bez složitých procesů nebo místních systémů.

### <a name="self-service-functionality"></a>Funkce samoobslužných služeb

Samoobslužná funkce zahrnuje Samoobslužné resetování hesla a obnovovací klíč BitLockeru. Azure AD taky poskytuje přímé možnosti pro resetování hesla nebo přístup k klíčům pro obnovení BitLockeru. Službu Azure AD můžete použít k resetování hesla přímo z zamykací obrazovky Windows místo z webového prohlížeče. Tyto funkce snižují tření uživatelů a pomůžou vám snížit náklady na helpdesk ve vaší organizaci.  

Další informace najdete v tématu [kurz: povolení odemknutí účtu nebo resetování hesla uživateli pomocí samoobslužného resetování hesla Azure Active Directory](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Roaming podnikového stavu

Všechna zařízení připojená k Azure AD můžou synchronizovat svá nastavení do cloudu. Jakékoli zařízení, ke kterému se uživatel přihlásí, synchronizuje všechna jeho nastavení s vyšší produktivitou.  

## <a name="value-proposition"></a>Pozice hodnoty

Připojení vašich zařízení ke službě Azure AD prostřednictvím obou metod zrychlí vaši digitální transformaci. Povoluje více funkcí poskytovaných Microsoft 365. Budete mít lepší prostředí a budete mít větší zabezpečení pro vaše data.

Azure AD nabízí několik možností, jak zjednodušit pracovní zatížení, například:

- Spravujte všechny identity zařízení ve vaší organizaci z jednoho místa.  

- Snižte náklady na helpdesk tím, že povolíte samoobslužné resetování hesla. Pak si uživatelé můžou kdykoli resetovat heslo z zamykací obrazovky Windows 10 na zařízení.  

## <a name="configure"></a>Konfigurace

Pokud už máte místní prostředí Active Directory a chcete připojit zařízení připojená k doméně ke službě Azure AD, nakonfigurujte hybridní zařízení připojená k Azure AD. Další informace najdete v tématu [Postup při plánování implementace služby hybrid Azure Active Directory JOIN](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager má nastavení klienta k [automatické registraci nových zařízení se systémem Windows 10 připojených k doméně pomocí Azure AD](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Další informace o konfiguraci nastavení klienta najdete v tématu [Konfigurace nastavení klienta](../core/clients/deploy/configure-client-settings.md).

Pokud chcete nakonfigurovat Azure AD – připojit se k vašim zařízením, aniž byste je museli připojit k místní doméně, přečtěte si téma požadavky na Azure AD – připojení ve vašem prostředí. Jakmile se rozhodnete, že se připojíte ke službě Azure AD JOIN, máte spoustu možností, jak ji nasadit na základě potřeb vaší organizace. Další informace najdete v těchto článcích:

- [Postupy: plánování implementace služby Azure AD JOIN](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Informace o možnostech zřizování](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  
