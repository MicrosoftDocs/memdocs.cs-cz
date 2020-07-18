---
title: Zapnutí programu Windows Defender | Microsoft Docs
description: Přečtěte si, jak zapnout program Windows Defender a umožnit mu tak přístup k prostředkům společnosti.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2169abf9955446d6299a64c7ce2ae03723faa792
ms.sourcegitcommit: 5c15b59cde085787b85f032f88add70a11d8e9a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2020
ms.locfileid: "86447972"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Zapnutí přístupu k prostředkům společnosti pro program Windows Defender

Vaše firma nebo škola potřebuje zajistit, aby zařízení přistupující k jejím prostředkům byla zabezpečená. Existuje několik způsobů, jak používat program [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx), integrovanou ochranu systému Windows proti škodlivému softwaru.

Některá nastavení programu Windows Defender bude možná potřeba při řešení problémů s přístupem změnit. Tyto postupy můžou vyžadovat, abyste na počítači přešli do několika různých umístění.

## <a name="turn-on-windows-defender"></a>Zapnutí programu Windows Defender

1. V nabídce **Start** otevřete **Ovládací panely**.
2. Otevřete **Nástroje pro správu**  >  **upravit zásady skupiny**. V novém okně se otevře **Editor místních zásad skupiny**.
3. Otevřete okno **Konfigurace počítače**  >  **šablony pro správu**  >  **součásti systému Windows**  >  **antivirová ochrana v programu Windows Defender**. Nastavení **Vypnout Antivirovou ochranu v programu Windows Defender** se nachází pod složkami dalších nastavení. 
4. Otevřete nastavení **Vypnout Antivirovou ochranu v programu Windows Defender** a ujistěte se, že je nastavené na **Zakázáno** nebo **Není nakonfigurováno**.

## <a name="turn-on-real-time-protection"></a>Zapnutí ochrany v reálném čase

Zkontrolujte, jestli je zapnutá ochrana v reálném čase, a to tak, že **spustíte** a vyhledáte **zabezpečení systému Windows**. Vyberete **Nastavení ochrany před viry a hrozbami ** a ověříte, že možnosti **Ochrana v reálném čase** a **Cloudová ochrana** jsou přepnuté na **Zapnuto**. Pokud se tyto možnosti nezobrazují, zapněte je takto:

1. V nabídce **Start** otevřete **Ovládací panely**.
2. Otevřete **Nástroje pro správu**  >  **upravit zásady skupiny**. V novém okně se otevře **Editor místních zásad skupiny**.
3. Otevřete okno **Konfigurace počítače**  >  **šablony pro správu**  >  **součásti systému Windows**  >  Ochrana proti**Windows Security**  >  **virům a hrozbám**zabezpečení systému Windows.
4. Otevřete nastavení **Skrýt oblast ochrana před viry a hrozbami** a nastavte ji na **zakázané**.

## <a name="update-your-antivirus-definitions"></a>Aktualizace antivirových definic

Zkontrolujte, jestli jsou antivirové definice aktuální. Uděláte to tak, že přejdete na **Start** a vyhledáte **Centrum zabezpečení v programu Windows Defender**. Vyberete **Aktualizace ochrany** a **Vyhledat aktualizace** a zkontrolujete tak, jestli zařízení má aktuální ochranu před viry. Pokud se tato možnost nezobrazuje, proveďte postup uvedený v části [Zapnutí ochrany v reálném čase](turn-on-defender-windows.md#turn-on-real-time-protection).

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Jeho kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
