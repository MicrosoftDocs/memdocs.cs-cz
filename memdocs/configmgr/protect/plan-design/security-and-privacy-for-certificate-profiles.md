---
title: Zabezpečení a ochrana osobních údajů u profilů certifikátů
titleSuffix: Configuration Manager
description: Seznamte se s osvědčenými postupy zabezpečení pro správu profilů certifikátů pro uživatele a zařízení v Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f73a556f28f8ebe4abf6e762104776b40b0cd0e8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697020"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro profily certifikátů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Nejlepší postupy zabezpečení pro profily certifikátů  
 Když spravujete profily certifikátů pro uživatele a zařízení, používejte následující nejlepší postupy.  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Určete a dodržujte veškeré nejlepší postupy zabezpečení pro službu zápisu síťových zařízení Network Device Enrollment Service, která zahrnuje webovou stránku služby Network Device Enrollment Service ve službě Internetová informační služba (IIS), k vyžádání protokolu SSL a ignorování klientských certifikátů.|Další informace najdete v tématu [pokyny pro službu zápisu síťových zařízení](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).|  
|Když konfigurujete profily certifikátů SCEP, vyberte nejbezpečnější možnosti, které mohou zařízení a vaše infrastruktura podporovat.|Určete, implementujte a dodržujte veškeré nejlepší postupy zabezpečení, které byly doporučeny pro vaše zařízení a infrastrukturu.|  
|Místo toho, abyste uživatelům povolili identifikaci jejich primárního zařízení, ručně zadejte spřažení uživatelských zařízení. Nepovolujte ani konfiguraci na základě využití.|Pokud kliknete na možnost **Povolit zápis certifikátů pouze na primárním zařízení uživatelů** v profilu certifikátů SCEP, neberte v úvahu informace, které jsou shromážděny od uživatelů nebo ze zařízení, které bude autoritativní. Pokud nasadíte profily certifikátů SCEP s touto konfigurací a důvěryhodný správce neurčí spřažení uživatelských zařízení, mohou neoprávnění uživatelé obdržet oprávnění vyšší úrovně a mohou jim být uděleny certifikáty pro ověřování.<br /><br /> **Poznámka:** Pokud povolíte konfiguraci na základě využití, tyto informace se shromažďují pomocí stavových zpráv, které nejsou zabezpečené pomocí Configuration Manager. K zmírnění této hrozby použijte podepisování protokolu SMB nebo protokol IPsec mezi klientskými počítači a bodem správy.|  
|Nepřidávejte oprávnění k čtení a zápisu pro uživatele do šablon certifikátů nebo nakonfigurujte bod registrace certifikátu tak, aby přeskočil kontrolu šablon certifikátů.|I když Configuration Manager podporuje další kontrolu, pokud přidáte oprávnění zabezpečení pro čtení a zápis pro uživatele a můžete nakonfigurovat bod registrace certifikátu, který tuto kontrolu přeskočí, pokud není možné ověřování, ani konfigurace není osvědčeným postupem zabezpečení. Další informace najdete v tématu [Plánování oprávnění šablon certifikátů pro profily certifikátů](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informace o ochraně dat pro profily certifikátů  
 Profily certifikátů můžete použít k nasazení kořenových certifikátů certifikačního úřadu (CA) a klientských certifikátů a pak vyhodnotit, zda po použití profilů jsou tato zařízení kompatibilní. Bod správy odesílá informace o kompatibilitě do serveru lokality a Configuration Manager ukládá tyto informace do databáze lokality. Informace o kompatibilitě zahrnují vlastnosti certifikátů, například název předmětu a kryptografický otisk. Data jsou zašifrována, když je zařízení zasílají do místa správy, ale v databázi lokality nejsou uložena v zašifrovaném formátu. Databáze zachovává informace, dokud úloha správy lokality **Odstranit starší data správy konfigurací** tyto informace neodstraní po výchozím intervalu 90 dní. Můžete provést konfiguraci intervalu odstranění. Informace o shodě nejsou zaslány do společnosti Microsoft.  

 Profily certifikátů používají informace, které Configuration Manager shromažďuje pomocí funkce zjišťování. Další informace o ochraně osobních údajů pro zjišťování naleznete v části **informace o ochraně** osobních údajů pro zjišťování v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Certifikáty, které jsou vydány uživatelům nebo zařízením, mohou povolovat přístup k důvěrným informacím.  

 Ve výchozím nastavení zařízení nevyhodnocují profily certifikátů. Kromě toho musíte nakonfigurovat profily certifikátů a pak je nasadit na uživatele nebo zařízení.  

 Před nakonfigurováním profilů certifikátů vezměte v úvahu vaše požadavky na ochranu dat.