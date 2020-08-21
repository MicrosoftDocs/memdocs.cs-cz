---
title: Upgrade Windows 10
titleSuffix: Configuration Manager
description: Upgrade zařízení na Windows 10 verze 1709 nebo novější, který je nutný pro spolusprávu
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d41a0806a33ac627eceaafab54c73c31ea013365
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694827"
---
# <a name="upgrade-windows-10-for-co-management"></a>Upgrade Windows 10 pro spolusprávu

Když pracujete na registraci vaší organizace pro spolusprávu, je získání aktuální důležitou prahovou hodnotu pro některé zákazníky. Spoluspráva vyžaduje [Windows 10 verze 1709](/windows/whats-new/whats-new-windows-10-version-1709) nebo novější. Po aktualizaci Windows a konfiguraci automatického zápisu se klienti automaticky zaregistrují do spolusprávy.

V následujícím videu, vedoucí program v programu Rob York a marketingový manažer pro produkty, Ainley diskutovat a ukázka upgradu na Windows 10 pro spolusprávu:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Proč upgradovat?

Kromě dalších možností využití platformy Windows 10 verze 1709 a novější podporuje automatickou registraci. Díky tomuto chování se zařízení automaticky zaregistruje do Intune, když se připojí Azure Active Directory (Azure AD). 

Další informace najdete v tématu [Povolení automatické registrace Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Jak to provést

Tady je několik tipů, které jsme se dozvěděli od pomoci tisícům zákazníků, jak rychle získat aktuální:

- Postupné nasazení použijte k zavedení tohoto upgradu na správné lidi ve správných časech. Další informace najdete v tématu [Vytvoření dvoufázové nasazení](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Pomocí předukládání do mezipaměti můžete zkrátit dobu čekání uživatelů. Další informace najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../osd/deploy-use/configure-precache-content.md).  

- Použijte výchozí šablonu pořadí úkolů místní upgrade. Pak proveďte konfiguraci kroků pro předem a po upgradu a případné akce při selhání. Další informace najdete v tématu [Doporučené kroky pořadí úloh pro následné zpracování](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Pokud má vaše prostředí vysoce mobilní pracovní síly, Configuration Manager podporuje místní upgrade přes bránu pro správu cloudu (CMG). Tato funkce umožňuje upgradovat klienty s Windows 10, pokud jsou na něm připojení. Další informace o CMG najdete v tématu [nasazení místního upgradu Windows 10 prostřednictvím CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Nabídnout výslovný souhlas se spolusprávou pro uživatele, kteří chtějí být předčasného přijetí. Tento přístup zrychlí prvotní přijetí. Díky identifikaci těchto osob předem můžete zajistit dobré pokrytí v počátečních dnech zavedení. Obdržíte také ověření a zpětnou vazbu od uživatelů, kteří jsou spokojení ke změně a mají zájem o častější vydání. Programy předčasného přihlašování generují zájem o nové technologie a zvětšují velikost v průběhu času.  


## <a name="case-studies"></a>Případové studie

Společnost Microsoft vyvinula Windows 10 na 96 000 distribuovaných uživatelů v Microsoftu. Nasazení zahrnuje vzdálené uživatele i uživatele v podnikové síti. Nasazení bylo dokončeno za devět týdnů. Další informace o jejich prostředí najdete v tématu [nasazení Windows 10 v Microsoftu jako místní upgrade](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Velký evropský výrobce softwaru úspěšně používá skupinu prvotních schválení. Po počátečním testování a pilotních skupinách, přibližně 2 000 zaměstnanců obdrží první aktualizaci, upgrady a software. Tato skupina zahrnuje pracovníky IT a výslovný souhlas s dobrovolníky. Tato úroveň zapojení se svými uživateli poskytuje při testování větší úroveň spolehlivosti a při zahájení uváděníosti větší věrohodnosti.



## <a name="contact-fasttrack"></a>Kontaktujte FastTrack

Pokud potřebujete pomoc s upgradem Windows 10 kdykoli v průběhu procesu, přejděte na [Microsoft FastTrack](https://Microsoft.com/FastTrack/), přihlaste se a požádejte o pomoc. 

Další informace najdete v tématu [získání Nápověda z FastTrack](quickstart-fasttrack.md).