---
title: Nastavení registrace pro zařízení s Windows pomocí Microsoft Intune
titleSuffix: ''
description: Nastavte registraci pro zařízení s Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55d7be5d54d194ccd3a1f982f70f26ee8c829d4f
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824145"
---
# <a name="set-up-enrollment-for-windows-devices"></a>Nastavení registrace pro zařízení s Windows

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Tento článek pomáhá správcům IT zjednodušit svým uživatelům registraci zařízení s Windows. Jakmile [nastavíte Intune](../fundamentals/setup-steps.md), mohou uživatelé registrovat svá zařízení s Windows tím, že se [přihlásí](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal) pomocí pracovního nebo školního účtu.  

Jako správce Intune můžete registraci zjednodušit. Máte tyto možnosti:

- [Povolit automatický zápis](#enable-windows-10-automatic-enrollment) (Azure AD Premium vyžaduje)
- [Registrace CNAME](#simplify-windows-enrollment-without-azure-ad-premium)
- [Povolit hromadnou registraci](windows-bulk-enroll.md) (vyžaduje se Azure AD Premium a Windows Configuration Designer)

Způsob zjednodušení registrace zařízení s Windows určují dva faktory:

- **Používáte Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) je součástí Enterprise Mobility + Security a dalších plánů licencování.
- **Jaké verze klientů Windows si uživatelé budou registrovat?** <br>Zařízení s Windows 10 se můžou zaregistrovat automaticky přidáním pracovního nebo školního účtu. Starší verze se musí zaregistrovat pomocí aplikace Portál společnosti.

||**Azure AD Premium**|**Jiné AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Automatická registrace](#enable-windows-10-automatic-enrollment) |Registrace uživatele|
|**Starší verze Windows**|Registrace uživatele|Registrace uživatele|

Organizace, které mohou používat automatickou registraci, také mohou nakonfigurovat [hromadnou registraci zařízení](windows-bulk-enroll.md) v aplikaci Windows Configuration Designer.

## <a name="device-enrollment-prerequisites"></a>Požadavky registrace zařízení

Předtím, než může správce zaregistrovat zařízení do Intune za účelem správy, by licence již měly být přiřazeny k účtu správce. [Přečtěte si informace o přiřazování licencí pro registraci zařízení.](../fundamentals/licenses-assign.md)

## <a name="multi-user-support"></a>Podpora více uživatelů

Intune podporuje více uživatelů na zařízeních, která obě:

- Spustit aktualizaci Windows 10 Creator 's Update
- jsou Azure Active Directory připojeny k doméně.

Když standardní uživatelé použijí k přihlášení přihlašovací údaje služby Azure AD, dostanou aplikace a zásady přiřazené ke svému uživatelskému jménu. Pouze [primární uživatel](../remote-actions/find-primary-user.md) zařízení může použít portál společnosti pro samoobslužné scénáře, jako je instalace aplikací a provádění akcí zařízení (odebrat, obnovit). Pro sdílená zařízení s Windows 10, která nemají přiřazeného primárního uživatele, se Portál společnosti dá dál použít k instalaci dostupných aplikací.

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="simplify-windows-enrollment-without-azure-ad-premium"></a>Zjednodušení registrace zařízení s Windows bez služby Azure AD Premium
Pokud chcete uživatelům registraci zjednodušit, vytvořte alias serveru DNS (typu záznamu CNAME), který přesměruje žádosti o registraci na servery Intune. V opačném případě musí uživatelé, kteří se pokoušejí připojit k Intune, zadat během registrace název serveru Intune.

**Krok 1: Vytvořte záznamy CNAME** (volitelné)<br>
Vytvořte záznamy o prostředcích DNS CNAME pro doménu vaší společnosti. Pokud je například web vaší společnosti contoso.com, vytvořili jste ve službě DNS záznam CNAME, který přesměruje EnterpriseEnrollment.contoso.com na enterpriseenrollment-s.manage.microsoft.com.

Vytváření položek CNAME DNS není povinné, ale záznamy CNAME usnadňují uživatelům registraci. Pokud se nenajde žádný záznam CNAME pro registraci, zobrazí se uživatelům výzva, aby ručně zadali název serveru MDM: enrollment.manage.microsoft.com.

|Typ|Název hostitele|Odkazuje na|Hodnota TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.doména_společnosti.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hodina|
|CNAME|EnterpriseRegistration.doména_společnosti.com|EnterpriseRegistration.windows.net|1 hodina|

Pokud podnik používá více než jednu příponu UPN, musíte vytvořit jeden CNAME pro každý název domény a každý z nich odkazovat na EnterpriseEnrollment-s.manage.microsoft.com. Uživatelé v Contosu například používají následující formáty jako svůj e-mail/UPN:

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

Správce DNS Contosa by měl vytvořit následující záznamy CNAME:

|Typ|Název hostitele|Odkazuje na|Hodnota TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hodina|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hodina|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hodina|

`EnterpriseEnrollment-s.manage.microsoft.com`– Podporuje přesměrování na službu Intune s rozpoznáním domény z doménového názvu e-mailu.

Změny záznamů DNS se mohou projevit až po 72 hodinách. Před rozšířením záznamu DNS nemůžete v Intune ověřit změnu DNS.

## <a name="additional-endpoints-are-used-but-no-longer-supported"></a>Používají se další koncové body, ale už se nepodporují.
EnterpriseEnrollment-s.manage.microsoft.com je upřednostňovaný plně kvalifikovaný název domény pro registraci. Existují dva ostatní koncové body, které zákazníci používali v minulosti a stále pracují, ale již nejsou podporováni. EnterpriseEnrollment.manage.microsoft.com (bez a-s) a manage.microsoft.com fungují jako cíl pro Server automatického zjišťování, ale uživatel bude muset na potvrzovací zprávě se dotknout OK. Pokud odkazujete na EnterpriseEnrollment-s.manage.microsoft.com, uživatel nebude muset provést další potvrzovací krok, takže se jedná o doporučenou konfiguraci.

## <a name="alternate-methods-of-redirection-are-not-supported"></a>Alternativní metody přesměrování se nepodporují.
Použití jiné metody než konfigurace CNAME není podporováno. Například použití proxy server k přesměrování enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc na enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc nebo manage.microsoft.com/EnrollmentServer/Discovery.svc není podporováno.

**Krok 2: Ověřte záznamy CNAME** (volitelné)<br>
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace**  >  **CNAME ověřování**.
2. Do pole **Doména** zadejte web společnosti a zvolte **Test**.

## <a name="tell-users-how-to-enroll-windows-devices"></a>Informování uživatelů, jak zařízení s Windows zaregistrovat
Informujte uživatele, jak si mají svá zařízení s Windows zaregistrovat a co můžou očekávat od zařazení do systému správy.

> [!NOTE]
> Koncoví uživatelé musí k webu Portál společnosti přistupovat přes Microsoft Edge, aby si mohli zobrazit aplikace Windows, které jste přiřadili ke konkrétním verzím Windows. Jiné prohlížeče, včetně Google Chrome, Mozilla Firefoxu a Internet Exploreru, tento typ filtrování nepodporují.

Postup registrace koncových uživatelů najdete v tématu [Registrace zařízení s Windows v Intune](../user-help/windows-enrollment-company-portal.md). Uživatelům také můžete poradit, aby si přečetli článek o tom, [jaké informace vidí správce IT na zařízení](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

>[!IMPORTANT]
> Pokud není povolená automatická registrace MDM, ale máte zařízení s Windows 10 připojená ke službě Azure AD, zobrazí se v konzole Intune po registraci dva záznamy. To můžete zastavit tím, že zajistíte, že uživatelé se zařízeními připojenými k Azure AD přejdou na **účty**  >  **přístup do práce nebo do školy** a **připojíte** se pomocí stejného účtu. 

Další informace o úlohách pro koncové uživatele najdete v tématu [Materiály o prostředí Microsoft Intune pro koncové uživatele](../fundamentals/end-user-educate.md).

## <a name="registration-and-enrollment-cnames"></a>Registrace a zápisy CNAME
Azure Active Directory má jiný záznam CNAME, který používá k registraci zařízení pro zařízení s iOS/iPadOS, Androidem a Windows. Podmíněný přístup Intune vyžaduje, aby se zařízení zaregistrovala, taky se označuje jako připojená k pracovišti. Pokud máte v úmyslu používat podmíněný přístup, měli byste také nakonfigurovat EnterpriseRegistration CNAME pro každý název společnosti, který máte.

| Typ | Název hostitele | Odkazuje na | Hodnota TTL |
| --- | --- | --- | --- |
| NÁZEV | EnterpriseRegistration. company_domain. com | EnterpriseRegistration.windows.net | 1 hodina|

Další informace o registraci zařízení najdete v tématu [Správa identit zařízení pomocí Azure Portal](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal) .

## <a name="windows-10-auto-enrollment-and-device-registration"></a>Automatický zápis a registrace zařízení s Windows 10

Tato část se vztahuje na zákazníky v cloudu pro státní správu USA.

Vytváření položek CNAME DNS není povinné, ale záznamy CNAME usnadňují uživatelům registraci. Pokud nebude nalezen žádný záznam CNAME pro registraci, zobrazí se uživatelům výzva k zadání názvu serveru MDM, enrollment.manage.microsoft.us.

| Typ | Název hostitele | Odkazuje na | Hodnota TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.doména_společnosti.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 hodina|
|CNAME | EnterpriseRegistration.doména_společnosti.com | EnterpriseRegistration.windows.net | 1 hodina |


## <a name="next-steps"></a>Další kroky

- [Co je třeba zvážit při správě zařízení Windows pomocí Intune v Azure](../fundamentals/intune-legacy-pc-client.md)
