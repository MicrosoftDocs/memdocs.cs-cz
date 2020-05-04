---
title: aplikace pro iOS/iPadOS se zásadami ochrany aplikací
description: Toto téma popisuje, co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b57e6525-b57c-4cb4-a84c-9f70ba1e8e19
ms.reviewer: andcerat
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc804efad2cf8ef45bd046fb1234eef9895cbd97
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332603"
---
# <a name="what-to-expect-when-your-iosipados-app-is-managed-by-app-protection-policies"></a>Co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací

Zásady ochrany aplikací Intune se vztahují na aplikace, které se používaly pro práci nebo školu. To znamená, že když vaši zaměstnanci a studenti používají své aplikace v osobním kontextu, můžou si všimnout žádného rozdílu ve svém prostředí. V pracovním nebo školním kontextu se ale můžou zobrazovat výzvy k rozhodování o rozhodnutích, aktualizovat jejich nastavení nebo se obrátit na nápovědu. V tomto článku se dozvíte, co se uživatelům snaží při pokusu o přístup a používání aplikací chráněných v Intune.  

## <a name="access-apps"></a>Přístup k aplikacím

Pokud zařízení **není zaregistrované v Intune**, zobrazí se uživateli při prvním použití aplikace výzva k jejímu restartování. Aby bylo možné v aplikaci použít zásady ochrany aplikací, je nutné restartovat počítač.

<!--- The following screenshot from the Skype app illustrates this restart request: --->

<!---  ![Screenshot of the iOS/iPadOS device showing PIN prompt](./media/end-user-mam-apps-ios/iOS_AppPINPrompt.png) --->

Na zařízeních, která jsou **zaregistrovaná pro správu přes Intune**, se uživateli zobrazí zpráva, že jeho aplikace je teď spravovaná.

## <a name="use-apps-with-multi-identity-support"></a>Použití aplikací s podporou více identit

Aplikace, které podporují více identit, umožňují pro přístup ke stejným aplikacím používat různé pracovní a osobní účty. Zásady ochrany aplikací, jako je zadání PIN kódu zařízení, se aktivují, když uživatelé přistupují k těmto aplikacím v pracovním nebo školním kontextu.   

V závislosti na tom, jak nakonfigurujete zásady, se uživatelé můžou setkat s výzvou k zadání kódu PIN v různých aplikacích.  Můžete například nakonfigurovat zásady tak, aby:       
* Aplikace Microsoft Outlook vyzve uživatele k zadání kódu PIN při spuštění aplikace. 
* OneDrive vyzve uživatele k zadání kódu PIN, když se přihlásí ke svému pracovnímu účtu.  
* Microsoft Word, PowerPoint a Excel vyzve uživatele k zadání kódu PIN, když přistupuje k dokumentům uloženým v umístění OneDrive pro firmy.  

- Přečtěte si další informace o aplikacích, které podporují [ochranu aplikací a více identit](https://www.microsoft.com/cloud-platform/microsoft-intune-apps) s Intune.  

## <a name="manage-user-accounts-on-the-device"></a>Správa uživatelských účtů v zařízení  

Zásady ochrany aplikací Intune omezují uživatele na jeden spravovaný pracovní nebo školní účet na aplikaci. Zásady ochrany aplikací neomezují počet nespravovaných účtů, které uživatel může přidat.   

- Pokud se uživatel pokusí přidat druhý spravovaný účet, zobrazí se mu výzva k výběru spravovaného účtu, který se má použít. Pokud uživatel přidá druhý účet, první účet se odebere.
- Pokud přidáte zásady ochrany na jiný účet uživatele, zobrazí se uživateli výzva k výběru spravovaného účtu, který se má použít. Druhý účet se odebere. 

Někteří uživatelé nezískají možnost přepínat a vybírat mezi spravovanými účty. Tato možnost není k dispozici na zařízeních, která jsou:
* Spravované přes Intune  
* Spravuje řešení pro správu firemní mobility třetích stran a konfigurují se s nastavením IntuneMAMUPN. 

Následující vzorový scénář popisuje, jak se zachází s několika uživatelskými účty:  

Uživatel A funguje pro dvě společnosti –**společnosti X** a **firmu Y**. Uživatel A má pro každou společnost pracovní účet a obě služby používají Intune k nasazení zásad ochrany aplikací. **Společnost X** nasadí zásady ochrany aplikací **před** **firmou Y**. Účet, který je přidružený ke **společnosti X** , získá nejdřív zásady ochrany aplikací. Pokud chcete, aby uživatelský účet přidružený ke společnosti Y spravovaly zásady ochrany aplikací, musíte odebrat uživatelský účet přidružený ke společnosti X a přidat uživatelský účet přidružený ke společnosti Y.  

## <a name="next-steps"></a>Další kroky

[Co očekávat, když ke správě svojí aplikace pro Android používáte zásady ochrany aplikací](end-user-mam-apps-android.md)
