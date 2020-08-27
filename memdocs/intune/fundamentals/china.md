---
title: Intune provozovaný společností 21Vianet v Číně
titleSuffix: ''
description: Intune provozovaný společností 21Vianet v Číně.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d652bea6e60417654ac06ebc1d0baa300f229a05
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915377"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune provozovaný společností 21Vianet v Číně  

Intune provozovaný společností 21Vianet je navržený tak, aby splňoval požadavky na bezpečné, spolehlivé a škálovatelné cloudové služby v Číně. Intune jako služba je postavená nad Microsoft Azure. Microsoft Azure provozovaný společností 21Vianet je fyzicky oddělená instance Cloud Services umístěná v Číně. Je nezávisle provozovaná a transakční společností 21Vianet. Tato služba využívá technologii, kterou společnost Microsoft uděluje společnosti 21Vianet.

Společnost Microsoft tuto službu nepracuje. 21Vianet funguje, poskytuje a spravuje doručování služby. 21Vianet je poskytovatel služeb pro Internet datového centra v Číně. Poskytuje hostování, spravované síťové služby a služby infrastruktury cloud computingu. Díky licencování technologií Microsoftu používá společnost 21Vianet místní datová centra, která vám poskytnou možnost používat službu Intune a přitom přitom uchovávat data v Číně. 21Vianet taky poskytuje vaše předplatné, fakturace a služby podpory.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Rozdíly ve funkcích Intune provozovaných společností 21Vianet

Vzhledem k tomu, že čínské služby provozuje partner z Číny v Číně, existují některé rozdíly ve funkcích Intune. 

- Intune provozovaný společností 21Vianet podporuje jenom samostatná nasazení. Podpora spolusprávy pomocí System Center Configuration Manager je aktuálně ve vývoji.
- Migrace z veřejných cloudů do svrchovaného cloudu není podporovaná. Zákazníci, kteří mají zájem o přechod na Intune provozovaný společností 21Vianet, se musí migrovat ručně.
- Funkce připojení tenanta (synchronizace zařízení s Intune bez registrace pro podporu scénářů cloudové konzoly) není v současné době podporovaná.
- Odvozené přihlašovací údaje se v Intune provozovaném společností 21Vianet nepodporují.
- Intune provozovaný společností 21Vianet nepodporuje agenta Intune, a proto nepodporuje správu starších počítačů.
- Správa Windows 10 je podporovaná pomocí moderního kanálu MDM.
- Intune provozovaný společností 21Vianet nepodporuje místní Exchange Connector.
- Funkce Windows autopilot a Business Store nejsou aktuálně k dispozici.
- Protože Google Mobile Services není k dispozici v Číně, zákazníci v Intune, které provozuje společnost 21Vianet, nemůžou používat funkce, které vyžadují Google Mobile Services. Patří k nim:
  - Google Play chránit možnosti, jako je například ověření zařízení SafetyNet.
  - Správa aplikací z Obchod Google Play.
  - Možnosti Androidu Enterprise. Další informace najdete v této [dokumentaci k Google](https://support.google.com/work/android/answer/6270910?hl=en).
- Aplikace Portál společnosti Intune pro Android používá ke komunikaci se službou Microsoft Intune Google Mobile Services. Vzhledem k tomu, že služba Google Play Services není k dispozici v Číně, můžou některé úlohy vyžadovat dokončení až 8 hodin. Další informace najdete v tomto [článku](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- Pro sledování místních předpisů a poskytování lepších funkcí se může klient Intune a prostředí klienta Intune (Portál společnosti aplikace) v Číně lišit.
- Oplocení není dostupné.
- Dostupnost správy mobilních aplikací (MAM) je podmíněná pro tyto aplikace, které jsou k dispozici v Číně v Čínské lidové republice.

## <a name="you-control-customer-data"></a>Můžete kontrolovat zákaznická data

V Microsoft Azure, Intune, Office 365 a Power BI provozovaných společností 21Vianet máte plnou kontrolu nad daty:
- Víte, kde se nacházejí zákaznická data.
- Můžete řídit přístup k zákaznickým datům.
- Pokud službu opustíte, budete mít kontrolu nad Zákaznickými daty.
- Máte možnost řídit zabezpečení zákaznických dat.

Pomocí Microsoft Azure, Intune, Office 365 a Power BI provozovaných společností 21Vianet jste vlastníkem vašich dat:
- 21Vianet nepoužívá zákaznická data pro reklamu.
- Vy řídíte, kdo má přístup k zákaznickým datům.
- K oddělení dat jednotlivých zákazníků používáme logickou izolaci.
- Poskytujeme jednoduché a transparentní zásady používání dat a obdržíme nezávislé audity.
- Naši subdodavatelé jsou předmětem smlouvy, aby splnily naše požadavky na ochranu osobních údajů.

## <a name="data-subject-requests"></a>Požadavky subjektu údajů

Role Správce klienta pro Intune, kterou provozuje 21Vianet, může vyžádat data pro předměty dat následujícími způsoby:

- Pomocí centra pro správu Azure Active Directory může Správce klienta trvale odstranit subjekt údajů z Azure Active Directory a souvisejících služeb. Další informace najdete v tématu [požadavky na subjekt dat Azure – odstranění](/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- Protokoly generované systémem pro služby Microsoftu provozované společností 21Vianet můžou exportovat Správci klientů pomocí exportu protokolů dat. Další informace najdete v tématu [požadavky na subjekt dat Azure – export](/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export).

## <a name="next-steps"></a>Další kroky

[Další informace o podporovaných konfiguracích služby Intune](supported-devices-browsers.md)