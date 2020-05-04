---
title: nastavení zásad macOS antivirové ochrany pro Intune v programu Microsoft Defender | Microsoft Docs
description: Podívejte se na seznam nastavení v profilu antivirového programu Microsoft Defender pro macOS. Tento profil je součástí zásad ochrany koncových bodů zabezpečení Endpoint pro macOS v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 9a0687b9e3938c93cfaebe0e064fd994077a92af
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086278"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Nastavení pro Microsoft Defender ATP pro Mac v Microsoft Intune

Prohlédněte si nastavení *antivirového* profilu, které můžete nakonfigurovat pro Microsoft Defender ATP pro Mac v Microsoft Intune. Další informace o těchto nastaveních najdete v dokumentaci k Windows v článku [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender pro Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) .

**Microsoft Defender ATP**

- **Ochrana v reálném čase**  
  Vyžaduje Defender na zařízeních macOS, aby se používaly funkce monitorování v reálném čase. Sledování v reálném čase vyhledává a brání v instalaci nebo spuštění malwaru v zařízení. Toto nastavení můžete po krátkou dobu vypnout, než se znovu zapne automaticky.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího nastavení systému.
  - **Povoleno** – vynutilo použití monitorování v reálném čase. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Zakázáno** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Ochrana Doručená v cloudu**  
  Ve výchozím nastavení Defender odesílá společnosti Microsoft informace o případných problémech, které najde. Microsoft analyzuje tyto informace, aby se dozvěděly Další informace o problémech, které se týkají vás a dalších zákazníků, a nabízí Vylepšená řešení. Ochrana funguje nejlépe při nastavení *automatického odesílání vzorků* .

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Povoleno** – ochrana s doručováním do cloudu je zapnutá. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Zakázáno** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Automatické odesílání vzorků**  
  Pošle ukázkové soubory Microsoftu, aby lépe chránily uživatele zařízení a vaši organizaci před potenciálními hrozbami.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Povoleno** – ochrana s doručováním do cloudu je zapnutá.  Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Zakázáno** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Shromažďování diagnostických dat**

  Nakonfigurujte, jak budou data o využití a diagnostika sdílena s Microsoftem.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Požadováno**
  - **Nepovinné**

- **Složky vyloučené ze skenování**  
  Vyberte **Přidat** a pak zadejte složky, které se při kontrole mají ignorovat.

- **Soubory vyloučené ze skenování**  
  Vyberte **Přidat** a zadejte soubory, které se při kontrole mají ignorovat.

- **Typy souborů vyloučené ze skenování**  
  Vyberte **Přidat** a zadejte přípony souborů, které se během kontroly mají ignorovat.

- **Procesy vyloučené ze skenování**  
  Vyberte **Přidat** a pak určete procesy, které se během kontroly mají ignorovat.
