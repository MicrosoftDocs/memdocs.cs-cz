---
title: Integrace řešení pro řízení přístupu k síti (NAC) do Microsoft Intune – Azure | Microsoft Docs
description: Řešení pro řízení přístupu k síti (NAC) kontrolují u zařízení s Intune stav registrace a dodržování předpisů. NAC zahrnuje určitá chování a pracuje s podmíněným přístupem. Prohlédněte si postup, který vám pomůže začít je využívat, a seznam partnerských řešení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: aa7ecff7-8579-4009-8fd6-e17074df67de
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bafd916ef31bea50dabb2de5012d693039ca741
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084825"
---
# <a name="network-access-control-nac-integration-with-intune"></a>Integrace řešení pro řízení přístupu k síti (NAC) do Intune

Intune spolupracuje s partnery, kteří řeší přístup k síti, aby organizacím pomohlo zabezpečit firemní data, když se zařízení pokoušejí o přístup k místním prostředkům.

>[!IMPORTANT]
> NAC se v tuto chvíli nepodporují pro zařízení s Androidem Enterprise (plně spravovaná) nebo zařízení s Androidem Enterprise.

## <a name="how-do-intune-and-nac-solutions-help-protect-your-organization-resources"></a>Jak Intune a řešení NAC pomáhají chránit prostředky organizace?

Řešení NAC kontrolují registrace zařízení a stav dodržování předpisů v Intune a podporují tak rozhodování o přístupu. Pokud zařízení není zaregistrované, nebo je zaregistrované, ale neodpovídá zásadám dodržování předpisů Intune, musí být přesměrováno do Intune, kde proběhne jeho registrace nebo kontrola z hlediska dodržování předpisů.

### <a name="example"></a>Příklad

Pokud je zařízení zaregistrované a kompatibilní s Intune, mělo by řešení NAC povolit zařízení přístup k prostředkům společnosti. Uživatelům může být třeba povolen nebo zakázán přístup k firemní síti Wi-Fi nebo VPN.

## <a name="feature-behaviors"></a>Chování funkce

Zařízení, která se aktivně synchronizují s Intune, se nemůžou **přesunout z** / nekompatibilního**nekompatibility** do **nesynchronizovaného** (nebo **neznámého**). Stav **Neznámé** je rezervovaný pro nově registrovaná zařízení, u kterých ještě neproběhla kontrola dodržování předpisů.

Pokud mají zařízení zablokovaný přístup k prostředkům, musí blokační služba přesměrovat všechny uživatele na [portál pro správu](https://portal.manage.microsoft.com), aby bylo možné zjistit důvod zablokování zařízení.  Když uživatelé tuto stránku navštíví, zároveň se znovu vyhodnotí, zda zařízení dodržuje předpisy.

## <a name="nac-and-conditional-access"></a>NAC a podmíněný přístup

NAC pracuje s podmíněným přístupem k poskytování rozhodnutí řízení přístupu. Další informace najdete v tématu [běžné způsoby použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md).

## <a name="how-the-nac-integration-works"></a>Jak funguje integrace NAC

Následující seznam obsahuje přehled fungování řešení pro řízení přístupu k síti (NAC) při integraci do Intune. První tři kroky (1–3) vysvětlují proces připojování. Kroky 4–9 popisují další provoz řešení NAC po jeho integraci do Intune.

![Koncepční obrázek toho, jak NAC funguje s Intune](./media/network-access-control-integrate/ca-intune-common-ways-2.png)

1. Partnerské řešení NAC zaregistrujte v Azure Active Directory (AAD) a přidělte rozhraní API řešení NAC integrovanému do Intune delegovaná oprávnění.
2. U partnerského řešení NAC nakonfigurujte příslušná nastavení, včetně adresy URL Intune pro zjišťování.
3. U partnerského řešení NAC nakonfigurujte ověřování certifikátů.
4. Uživatel se připojí k firemnímu přístupovému bodu Wi-Fi nebo požádá o připojení k síti VPN.
5. Partnerské řešení NAC předá informace o zařízení Intune a zeptá se na registraci zařízení a stav dodržování předpisů.
6. Pokud zařízení nedodržuje předpisy nebo není zaregistrované, dá partnerské řešení NAC uživateli pokyn, aby zařízení zaregistroval nebo opravil nedostatky v dodržování předpisů.
7. Ve vhodný okamžik se zařízení pokusí znovu ověřit dodržování předpisů a stav registrace.
8. Jakmile je zařízení zaregistrované a odpovídá předpisům, dostane partnerské řešení NAC z Intune informaci o stavu.
9. Připojení se úspěšně naváže, aby zařízení mělo přístup k firemním prostředkům.

## <a name="use-nac-for-vpn-on-your-iosipados-devices"></a>Použití NAC pro VPN na zařízeních s iOS/iPadOS

NAC je k dispozici na následujících sítích VPN bez povolení NAC v profilu sítě VPN:

- NAC pro Cisco Legacy AnyConnect
- Přístup k starší verzi F5
- Citrix VPN

NAC se podporuje taky pro přístup k Cisco AnyConnect, Citrix SSO a F5.

### <a name="to-enable-nac-for-cisco-anyconnect-for-ios"></a>Povolení NAC pro Cisco AnyConnect pro iOS

- Integrujte ISE do Intune pro NAC, jak je popsáno v následujícím odkazu.
- Nastavte možnost **Povolit síťové Access Control (NAC)** v profilu sítě VPN na **Ano**.

### <a name="to-enable-nac-for-citrix-sso"></a>Povolení NAC pro Citrix SSO

- Použijte Citrix Gateway 12.0.59 nebo vyšší.  
- Uživatelé musí mít nainstalované Citrix SSO 1.1.6 nebo novější.
- [Integrujte NetScaler do Intune pro NAC](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html) , jak je popsáno v dokumentaci k produktu Citrix.
- V profilu sítě VPN vyberte **základní nastavení** > **Povolit síťové Access Control (NAC)** **> vyberte Souhlasím**.

### <a name="to-enable-nac-for-f5-access"></a>Povolení přístupu k NAC pro F5

- Použijte F5 BIG-IP 13.1.1.5 nebo novější.
- Integrujte BIG-IP s Intune for NAC. [Přehled: Konfigurace funkce APM pro stav zařízení pomocí příručky pro správu koncových bodů v systému](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) F5 seznam kroků.
- V profilu sítě VPN vyberte **základní nastavení** > **Povolit síťové Access Control (NAC)** **> vyberte Souhlasím**.

Z bezpečnostních důvodů je připojení VPN odpojené každých 24 hodin. SÍŤ VPN se může okamžitě znovu připojit.

Spolupracujeme s našimi partnery pro vydání řešení NAC pro tyto novější klienty. Až budou řešení připravena, Tento článek se aktualizuje o další informace.

## <a name="next-steps"></a>Další kroky

- [Integrace Cisco ISE s Intune](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)
- [Integrace Citrix NetScaler s Intune](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html)
- [Integrace nástroje F5 BIG-IP Access Policy Manager s Intune](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-13-0-0/6.html)
- [Integrace řešení HP Aruba ClearPass do Intune](https://support.arubanetworks.com/Documentation/tabid/77/DMXModule/512/Command/Core_Download/Default.aspx?EntryId=31271)
- [Integrace řešení secRMM (Squadra security Removable Media Manager) do Intune](http://www.squadratechnologies.com/StaticContent/ProductDownload/secRMM/9.9.0.0/secRMMIntuneAccessControlSetupGuide.pdf)
