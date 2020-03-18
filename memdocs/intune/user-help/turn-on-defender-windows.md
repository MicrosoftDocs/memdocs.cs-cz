---
title: Zapnutí programu Windows Defender | Microsoft Docs
description: Přečtěte si, jak zapnout program Windows Defender a umožnit mu tak přístup k prostředkům společnosti.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/08/2017
ms.topic: article
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
ms.openlocfilehash: 46ad7a5d34e6d006794b13cd5eae9c533e047ec3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79324255"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Zapnutí přístupu k prostředkům společnosti pro program Windows Defender

Vaše firma nebo škola potřebuje zajistit, aby zařízení přistupující k jejím prostředkům byla zabezpečená. Existuje několik způsobů, jak používat program [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx), integrovanou ochranu systému Windows proti škodlivému softwaru.

Některá nastavení programu Windows Defender bude možná potřeba při řešení problémů s přístupem změnit. Tyto postupy můžou vyžadovat, abyste na počítači přešli do několika různých umístění.

## <a name="turn-on-windows-defender"></a>Zapnutí programu Windows Defender

1. V nabídce **Start** otevřete **Ovládací panely**.
2. Otevřete **Nástroje pro správu** > **Upravit zásady skupiny**. V novém okně se otevře **Editor místních zásad skupiny**.
3. Otevřete **Konfigurace počítače** > **Šablony pro správu** > **Součásti systému Windows** > **Antivirová ochrana v programu Windows Defender**. Nastavení **Vypnout Antivirovou ochranu v programu Windows Defender** se nachází pod složkami dalších nastavení. 
4. Otevřete nastavení **Vypnout Antivirovou ochranu v programu Windows Defender** a ujistěte se, že je nastavené na **Zakázáno** nebo **Není nakonfigurováno**.

## <a name="turn-on-real-time-protection"></a>Zapnutí ochrany v reálném čase

Zkontrolujte, jestli je zapnutá ochrana v reálném čase. Uděláte to tak, že přejdete na **Start** a vyhledáte **Centrum zabezpečení v programu Windows Defender**. Vyberete **Nastavení ochrany před viry a hrozbami**  a ověříte, že možnosti **Ochrana v reálném čase** a **Cloudová ochrana** jsou přepnuté na **Zapnuto**. Pokud se tyto možnosti nezobrazují, zapněte je takto:

1. V nabídce **Start** otevřete **Ovládací panely**.
2. Otevřete **Nástroje pro správu** > **Upravit zásady skupiny**. V novém okně se otevře **Editor místních zásad skupiny**.
3. Otevřete **Konfigurace počítače** > **Šablony pro správu** > **Součásti systému Windows** > **Centrum zabezpečení v programu Windows Defender** > **Ochrana před viry a hrozbami**.
4. Otevřete nastavení **ochrany před viry a hrozbami** a nastavte je na **Zakázáno**.

## <a name="update-your-antivirus-definitions"></a>Aktualizace antivirových definic

Zkontrolujte, jestli jsou antivirové definice aktuální. Uděláte to tak, že přejdete na **Start** a vyhledáte **Centrum zabezpečení v programu Windows Defender**. Vyberete **Aktualizace ochrany** a **Vyhledat aktualizace** a zkontrolujete tak, jestli zařízení má aktuální ochranu před viry. Pokud se tato možnost nezobrazuje, proveďte postup uvedený v části [Zapnutí ochrany v reálném čase](turn-on-defender-windows.md#turn-on-real-time-protection).

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Jeho kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
