---
title: Nástroj pro odeslání plánu
titleSuffix: Configuration Manager
description: Pomocí nástroje Odeslat plán můžete aktivovat plán pro klienta Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723121"
---
# <a name="send-schedule-tool"></a>Nástroj pro odeslání plánu

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro odeslání plánu je jedním z [Configuration Manager nástrojů](tools.md). Použijte ji ke spuštění plánu na klientovi nebo aktivaci vyhodnocení zadaného směrného plánu konfigurace. Funguje pro místní počítač nebo se zaměřuje na vzdáleného klienta.  

Pomocí nástroje můžete například aktivovat plán inventarizace nebo vyhodnocení dodržování předpisů. Pokud počet klientů Configuration Manager neoznámil nedávno zprávu inventáře nebo stav dodržování předpisů, spusťte nástroj, který spustí potřebný plán pro každého klienta.



## <a name="usage"></a>Využití

Spusťte **SendSchedule. exe** jako správce. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Po aktivaci zprávy (GUID) si přečtěte téma **SMSClientMethodProvider. log**. Další informace o dostupných identifikátorech GUID zprávy najdete v tématu [ID zpráv](#bkmk_sendschedule-guids).

Po aktivaci vyhodnocení standardních hodnot konfigurace (identifikátor UID DCM) si přečtěte téma **DCMAgent. log**.



## <a name="command-line-options"></a>Možnosti příkazového řádku


### <a name="option-l"></a>Nastavení`/L` 
Zobrazí seznam všech identifikátorů GUID zprávy nebo identifikátoru DCM DCM k dispozici pro odeslání. Zobrazí smysluplné názvy zpráv v tabulce dat pro každou z nich. Pokud název počítače chybí, použije se místní počítač. Pokud zadáte zprávu bez názvu počítače, odešle se zpráva na místní počítač. 



## <a name="examples"></a>Příklady

#### <a name="list-the-available-messages-on-the-local-machine"></a>Zobrazit dostupné zprávy na místním počítači 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Vypíše dostupné zprávy na MyPC klienta: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Aktivovat inventář hardwaru v místním počítači
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Aktivovat inventář hardwaru v MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Aktivovat vyhodnocení konkrétního směrného plánu konfigurace na MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a>ID zpráv

|ID zprávy  |Zobrazovaný název  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventář hardwaru|
|{00000000-0000-0000-0000-000000000002}|Inventář softwaru|
|{00000000-0000-0000-0000-000000000003}|Inventář zjišťování|
|{00000000-0000-0000-0000-000000000010}|Kolekce souborů|
|{00000000-0000-0000-0000-000000000011}|Kolekce IDMIF|
|{00000000-0000-0000-0000-000000000021}|Žádost o přiřazení počítače|
|{00000000-0000-0000-0000-000000000022}|Zhodnotit zásady počítače|
|{00000000-0000-0000-0000-000000000023}|Aktualizovat výchozí úlohu MP|
|{00000000-0000-0000-0000-000000000024}|Úloha aktualizace umístění LS (služba umístění)|
|{00000000-0000-0000-0000-000000000025}|Úloha aktualizace časového limitu LS|
|{00000000-0000-0000-0000-000000000026}|Přiřazení žádosti agenta zásad (uživatel)|
|{00000000-0000-0000-0000-000000000027}|Přiřazení vyhodnocení agenta zásad (uživatel)|
|{00000000-0000-0000-0000-000000000031}|Sestava využití při generování měření softwaru|
|{00000000-0000-0000-0000-000000000032}|Zpráva o aktualizaci zdroje|
|{00000000-0000-0000-0000-000000000037}|Vymazání mezipaměti nastavení proxy serveru|
|{00000000-0000-0000-0000-000000000040}|Vyčištění agenta zásad počítače|
|{00000000-0000-0000-0000-000000000041}|Vyčištění agenta zásad uživatele|
|{00000000-0000-0000-0000-000000000042}|Agent zásad – ověření zásad počítače/přiřazení|
|{00000000-0000-0000-0000-000000000043}|Agent zásad ověřit zásady uživatele/přiřazení|
|{00000000-0000-0000-0000-000000000051}|Opakování/aktualizace certifikátů v AD v MP|
|{00000000-0000-0000-0000-000000000061}|Vytváření stavových zpráv partnerského DISTRIBUČNÍho bodu|
|{00000000-0000-0000-0000-000000000062}|Plán kontroly připraveného balíčku partnerského DISTRIBUČNÍho bodu|
|{00000000-0000-0000-0000-000000000063}|Plán instalace SUM Updates|
|{00000000-0000-0000-0000-000000000101}|Cyklus shromažďování inventáře hardwaru|
|{00000000-0000-0000-0000-000000000102}|Cyklus shromažďování inventáře softwaru|
|{00000000-0000-0000-0000-000000000103}|Cyklus shromažďování dat zjišťování|
|{00000000-0000-0000-0000-000000000104}|Cyklus sběru souborů|
|{00000000-0000-0000-0000-000000000105}|Cyklus shromažďování IDMIF|
|{00000000-0000-0000-0000-000000000106}|Cyklus sestav využití měření softwaru|
|{00000000-0000-0000-0000-000000000107}|Instalační služba systému Windows cyklus aktualizace zdrojového seznamu|
|{00000000-0000-0000-0000-000000000108}|Cyklus vyhodnocení přiřazení aktualizací softwaru akce v zásadách aktualizací softwaru|
|{00000000-0000-0000-0000-000000000109}|PDP úloha údržby distribučního bodu sítě PDP zásad údržby|
|{00000000-0000-0000-0000-000000000110}|Zásady DCM|
|{00000000-0000-0000-0000-000000000111}|Odeslat neodeslanou zprávu o stavu|
|{00000000-0000-0000-0000-000000000112}|Vyčištění mezipaměti zásad systému stavů|
|{00000000-0000-0000-0000-000000000113}|Aktualizovat zdrojové zásady|
|{00000000-0000-0000-0000-000000000114}|Aktualizovat zásady úložiště|
|{00000000-0000-0000-0000-000000000115}|Velké hromadné odesílání zásad systému stavu|
|{00000000-0000-0000-0000-000000000116}|Nízká úroveň odesílání zásad systému stavu|
|{00000000-0000-0000-0000-000000000121}|Akce zásad správce aplikací|
|{00000000-0000-0000-0000-000000000122}|Akce zásad uživatele Správce aplikací|
|{00000000-0000-0000-0000-000000000123}|Akce globálního vyhodnocení Správce aplikací|
|{00000000-0000-0000-0000-000000000131}|Úvodní Shrnutí řízení spotřeby|
|{00000000-0000-0000-0000-000000000221}|Opětovné vyhodnocení nasazení koncového bodu|
|{00000000-0000-0000-0000-000000000222}|Opětovné vyhodnocení zásad koncového bodu|
|{00000000-0000-0000-0000-000000000223}|Detekce externích událostí|



