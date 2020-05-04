---
title: Použití diagnostických dat
titleSuffix: Configuration Manager
description: Přečtěte si, jak Microsoft používá diagnostická data a data o využití, která Configuration Manager shromažďuje.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715610"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Jak Microsoft používá Configuration Manager Diagnostika a data o využití

*Platí pro: Configuration Manager (Current Branch)*

Diagnostická data a údaje o využití, které Configuration Manager shromažďuje, poskytují Microsoftu skoro okamžitou zpětnou vazbu o tom, jak produkt pracuje a který slouží k úpravě budoucích aktualizací. Microsoft také uvidí konfigurační data, která je pomohou analyzovat a testovat konfigurace používané v produkčním prostředí. Příklad:

- Verze Windows serveru používané na serverech lokality

- Nainstalované jazykové sady

- Rozdíly mezi schématem SQL a výchozím nastavením produktu

Tato data pomáhají technickému týmu plánovat budoucí testy, abyste měli jistotu, že máte nejlepší zkušenosti s nejběžnějšími konfiguracemi. Tato data jsou zásadní pro rychlé přizpůsobení a přizpůsobení s častým cyklem vydávání verzí.

Stejně důležité je, jak se data o využití a diagnostika nepoužívají. Microsoft nepoužívá tato data pro:

- Audity licencování, jako například porovnávání používání zákazníky oproti licenčním smlouvám

- Auditování produktů, pro které už skončila podpora

- Reklama na základě dostupných dat, jako je například využití funkcí nebo zeměpisná poloha (časové pásmo)

Společnost Microsoft používá dostupná data k vylepšení produktu. Příklad:

- Počáteční podpora nabízená aktuální větví Configuration Manager omezila časovou osu podpory pro Windows Server 2008 R2. Společnost Microsoft zkoumala data o využití od zákazníků, kteří upgradovali na Configuration Manager aktuální větev. Pak identifikovali nutnost revidovat a roztáhnout tuto časovou osu pro podporu zákazníků, kteří ještě používají tento operační systém.

- Společnost Microsoft vylepšila kontroly požadovaných součástí pro instalaci aktualizace. Odebrali jsme zastaralá pravidla, která se týkají dalších případů a automaticky opravila nějaké problémy.  

> [!div class="nextstepaction"]
> [Jak Configuration Manager shromažďuje data](how-diagnostics-and-usage-data-is-collected.md)
