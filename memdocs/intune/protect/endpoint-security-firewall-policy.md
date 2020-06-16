---
title: Správa nastavení brány firewall pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad brány firewall zabezpečení koncového bodu ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: aa518036aa99d5de003fbc56f99748267f3cc87b
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776867"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Zásady brány firewall pro zabezpečení koncových bodů v Intune

Pomocí zásad brány firewall zabezpečení koncového bodu v Intune můžete nakonfigurovat vestavěnou bránu firewall pro zařízení, která používají macOS a Windows 10.

I když můžete nakonfigurovat stejné nastavení brány firewall pomocí Endpoint Protection profilů pro konfiguraci zařízení, profily konfigurace zařízení obsahují další kategorie nastavení. Tato další nastavení se netýkají bran firewall a můžou zkomplikovat úlohy konfigurace pouze nastavení brány firewall pro vaše prostředí.

Zásady zabezpečení koncového bodu pro brány firewall najdete v části *Správa* v uzlu **zabezpečení koncového bodu** v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zobrazit [nastavení pro profily brány firewall](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Předpoklady pro profily brány firewall

- Windows 10 nebo novější
- Libovolná podporovaná verze macOS

## <a name="firewall-profiles"></a>Profily brány firewall

**MacOS profily**:

- **MacOS firewall** – povolí a nakonfiguruje nastavení pro vestavěnou bránu firewall na MacOS.

**Profily Windows 10**:

- **Firewall v programu Microsoft Defender** – konfigurace nastavení pro firewall v programu Windows Defender s pokročilým zabezpečením Firewall v programu Windows Defender poskytuje pro zařízení obousměrné filtrování síťového provozu a může blokovat neoprávněné síťové přenosy do nebo z místního zařízení.

- **Pravidla firewallu v programu Microsoft Defender** *(Preview)* – definují podrobná pravidla brány firewall, včetně konkrétních portů, protokolů, aplikací a sítí a povolují nebo blokují síťový provoz. Každá instance tohoto profilu podporuje až 150 vlastních pravidel.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Sloučení pravidel brány firewall a konflikty zásad

Naplánujte, aby se zásady brány firewall používaly na zařízení jenom v jedné zásadě. Použití jedné instance zásad a typu zásad pomáhá zabránit tomu, aby dvě samostatné zásady používaly různé konfigurace pro stejné nastavení, které vytváří konflikty. Pokud existuje konflikt mezi dvěma instancemi zásad nebo typy zásad, které spravují stejné nastavení s různými hodnotami, nastavení se do zařízení nepošle.

- Tato forma konfliktu zásad platí pro profil **firewallu v programu Microsoft Defender** , který může být v konfliktu s jinými profily firewallu v programu Microsoft Defender, nebo konfigurací brány firewall, která se doručuje jiným typem zásad, jako je konfigurace zařízení.

  *Profily firewallu* v programu Microsoft Defender nejsou v konfliktu s profily *pravidel firewallu v programu Microsoft Defender* .

Když použijete profily **pravidel firewallu v programu Microsoft Defender** , můžete na stejné zařízení použít několik profilů pravidel. Pokud však existují různá pravidla pro stejnou věc s různými konfiguracemi, obě jsou odesílány do zařízení a v tomto zařízení vytvoří konflikt.

- Pokud například jedno pravidlo blokuje *Teams.exe* přes bránu firewall a druhé pravidlo povoluje *Teams.exe*, budou se obě pravidla doručovat do klienta. Tento výsledek se liší od konfliktů vytvořených prostřednictvím jiných zásad pro nastavení brány firewall.

Když pravidla z různých pravidel nekolidují mezi sebou, zařízení sloučí pravidla z jednotlivých profilů a vytvoří na zařízení kombinovanou konfiguraci pravidel brány firewall. Toto chování umožňuje nasadit více než 150 pravidel, které jednotlivé profily podporují pro zařízení.

- Máte například dva profily pravidla firewallu v programu Microsoft Defender. První profil umožňuje *Teams.exe* přes bránu firewall. Druhý profil umožňuje *Outlook.exe* přes bránu firewall. Když zařízení obdrží oba profily, zařízení se nakonfiguruje tak, aby umožňovalo obě aplikace přes bránu firewall.

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
