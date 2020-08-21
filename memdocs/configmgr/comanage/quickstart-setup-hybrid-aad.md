---
title: Nastavení hybridní služby Azure AD
titleSuffix: Configuration Manager
description: Pokud má vaše prostředí v současné době zařízení s Windows 10 připojená k doméně, nastavte hybridní službu Azure AD ještě předtím, než povolíte spolusprávu.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 405303b3988e8c853ba30e8fb6d620d782b0474e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694895"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Nastavení hybridní služby Azure AD pro spolusprávu

Pokud máte zařízení s Windows 10 připojená k místní službě Active Directory, před povolením spolusprávy v Configuration Manager nejdřív připojte tato zařízení k Azure Active Directory (Azure AD). Tento proces se nazývá hybridní připojení ke službě Azure AD. 

V následujícím videu se vedoucí program Sandeep DEO a produkt marketingový manažer pro správu a přípravek a ukázka konfigurace zařízení v Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Proces připojení Hybrid Azure AD automaticky registruje vaše místní zařízení připojená k doméně pomocí Azure AD. Další informace o tomto procesu najdete v následujících článcích:
- [Úvod do správy zařízení v Azure Active Directory](/azure/active-directory/device-management-introduction) 
- [Jak naplánovat připojení k hybridní službě Azure AD](/azure/active-directory/devices/hybrid-azuread-join-plan)

Hybridní připojení k Azure AD je jednou z klíčových základů pro spolusprávu. Tento proces může být pro některé zákazníky náročný, například:
- Vaše organizace používá řešení identity od jiného výrobce. 
- Složitosti nastavení Active Directory Federation Services (AD FS) (ADFS)

Řešení těchto problémů může vzít v úvahu některé doprovodné materiály. Tento článek vám pomůže zmírnit veškerá zpoždění.


## <a name="how-to-do-it"></a>Jak to provést

Zařízení se podobají uživatelům při vytváření identity, kterou chcete chránit. Chcete-li chránit identitu zařízení kdykoli a v jakémkoli umístění, musíte uvést identitu tohoto zařízení do služby Azure AD.

Na základě typu domény, kterou používáte, existují dva hlavní způsoby, jak to provést. Nakonfigurujte hybridní připojení ke službě Azure AD pro jeden z následujících typů domén:  
- [Federované domény](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Spravované domény](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Tyto dvě předchozí metody poskytují nejlepší prostředí. Podrobnější informace, včetně úplného ručního procesu, najdete v následujících článcích:
- [Ruční konfigurace zařízení připojených k hybridní službě Azure AD](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Předávací ověřování ADFS pro hybridní službu Azure AD](/windows-server/identity/ad-fs/ad-fs-overview), která zahrnuje zjišťování Azure AD  

Pokyny k odstraňování potíží najdete v tématu [Průvodce řešením potíží se službou Azure AD Hybrid pro připojení k Windows 10](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Případová studie

Velká Evropská softwarová společnost s více než 100 000 uživateli ve své síti má podrobnější a dvoufázové přístup k povolení hybridního připojení k Azure AD.

Vzhledem k tomu, že služba Azure AD JOIN ve fázi plánování je klíčovým prvkem, který podporuje spolusprávu, Configuration Manager správci pracovali s týmem identity. Tato softwarová společnost má mnoho pravidel ADFS a některé z nich jsou komplexní. Pro vyřešení této výzvy tým identity zkontroloval stávající pravidla ADFS ještě předtím, než povolí hybridní připojení ke službě Azure AD. Tým IT také rozhodl upgradovat Azure AD Connect na nejnovější verzi. Azure AD Connect teď poskytuje automatizovaný tok procesu pro povolení připojení k hybridní službě Azure AD.

Po úspěšném nasazení a testování v předprodukčním prostředí je tento zákazník povolený pro celou produkční službu Azure AD. Během jednoho týdne mají každé spoluspravované zařízení s Windows 10.



## <a name="contact-fasttrack"></a>Kontaktujte FastTrack

Pokud potřebujete pomoc s nastavením Azure AD kdykoli během procesu, přejděte na [Microsoft FastTrack](https://Microsoft.com/FastTrack/), přihlaste se a požádejte o pomoc. 

Další informace najdete v tématu [získání Nápověda z FastTrack](quickstart-fasttrack.md).