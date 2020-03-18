---
title: Identifikace scénářů pro případy použití
titleSuffix: Microsoft Intune
description: Tento článek vám pomůže určit scénáře použití a dílčí scénáře použití při cloudové implementaci Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4b3c9af9-78da-44d2-8bd2-3f0f8885952d
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d277b47b2d753b5068e871fe33ce0cab48cfb1e4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330947"
---
# <a name="identify-mobile-device-management-use-case-scenarios"></a>Identifikace scénářů použití při správě mobilních zařízení

Identifikace scénářů použití je důležitou součástí plánování úspěšného nasazení Intune. Scénáře použití jsou praktické, protože s nimi můžete uživatele rozdělit do lépe zvládnutelných skupin podle typu uživatele nebo role a vlastnictví uživatelského zařízení (například firemní nebo osobní vlastnictví).

Podíváme se na několik příkladů, které vaší organizaci pomůžou identifikovat scénáře použití Intune a také organizační skupiny a platformy mobilních zařízení přidružené ke každému případu použití.

## <a name="device-ownership"></a>Vlastnictví zařízení
Můžete začít rekapitulací cílů a úkolů organizace při nasazení Intune, které vám pomohou identifikovat hlavní scénáře použití nasazeného řešení. Při sestavování plánu nasazení Intune si odpovězte na následující otázky:

- Plánujete podporu zařízení patřících společnosti?

- Plánujete podporu vlastních zařízení uživatelů (BYOD)?

Tyto možnosti se vzájemně nevylučují. Možná zjistíte, že ke splnění cílů organizace potřebujete podporovat obě formy vlastnictví zařízení. Dílčí případy použití vám pomohou vyjasnit, kde použít různé zásady správy zařízení.

### <a name="user-type-or-device-role"></a>Typ uživatele nebo role zařízení

Zjistěte, jestli každý scénář použití také obsahuje dílčí scénáře. Organizace například identifikuje požadavky na podporu scénáře firemního použití, který zahrnuje další, dílčí případy použití založené na typu uživatele nebo roli zařízení. Příklad:

- Informatik

- Vedení

- Veřejný terminál

Tady je několik příkladů scénářů použití a dílčích scénářů použití:

| **Případy použití** | **Dílčí případy použití** |
|:---:|:---:|
| Firemní | Informatik |              
| Firemní | Vedení |           
| Firemní | Veřejný terminál |
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Informatik |           
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Vedení |

Můžete [si stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a zadat scénáře použití a dílčí scénáře použití ve vaší organizaci.

## <a name="organizational-groups-for-your-scenarios"></a>Organizační skupiny pro scénáře

Teď potřebujete určit organizační skupiny přidružené ke každému hlavnímu a dílčímu scénáři použití. Příklad:

| **Případy použití** | **Dílčí případy použití** | **Organizační skupiny** |
|:---:|:---:|:---:|
| Firemní | Informatik | Personální, finanční oddělení |               
| Firemní | Vedení | Personální, finanční oddělení |            
| Firemní | Veřejný terminál | Maloobchod |
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Informatik | Marketing, prodej |            
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Vedení | Marketing, prodej |


## <a name="mobile-device-platforms-for-your-scenarios"></a>Platformy mobilních zařízení pro vaše scénáře

V dalším kroku budete identifikovat platformy mobilních zařízení přidružené ke každému scénáři použití. Může jich být více.

Scénář firemního použití může například podporovat platformy zařízení iOS/iPadOS a Android Samsung KNOX. Zásady pro uživatele s vlastním zařízením (BYOD) ale mohou zahrnovat podporu dalších platforem pro mobilní zařízení, jako je Android (bez zabezpečení Samsung KNOX) a Windows 10 Mobile. Pokud budeme vycházet z předchozích příkladů, přidružíme každému scénáři použití následující platformy mobilních zařízení.

| **Případy použití** | **Dílčí případy použití** | **Skupiny** | **Platformy zařízení** |   
|:---:|:---:|:---:|:---:|
| Firemní | Informatik | Personální, finanční oddělení | iOS/iPadOS |                                                           
| Firemní | Vedení | Personální, finanční oddělení | iOS/iPadOS |                                                           
| Firemní | Veřejný terminál | Maloobchod | Android |
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Informatik | Marketing, prodej | iOS/iPadOS |                                                           
| UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Vedení | Marketing, prodej | iOS/iPadOS |

## <a name="next-steps"></a>Další kroky

V další části najdete pokyny, [jak identifikovat požadavky na Intune pro jednotlivé scénáře použití](planning-guide-requirements.md).
