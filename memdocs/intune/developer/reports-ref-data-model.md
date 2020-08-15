---
title: Datový model datového skladu
titleSuffix: Microsoft Intune
description: Datový sklad Microsoft Intune denně vzorkuje data, aby mohl poskytovat historický přehled průběžně se měnícího mobilního prostředí.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4D04D3D9-4B6C-41CD-AAF8-466AF8FA6032
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fb6ec17ce058247529ab1e51d50d876e4c97408
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252669"
---
# <a name="microsoft-intune-data-warehouse-data-model"></a>Microsoft Intune datový model datového skladu

Datový sklad Intune denně vzorkuje data, aby mohl poskytovat historický přehled průběžně se měnícího prostředí mobilních zařízení. Zobrazení se skládá z časově souvisejících entit.

## <a name="entities-entity-sets"></a>Entity: sady entit

Sklad zveřejňuje data v následujících oblastech vyšší úrovně:

- Aplikace se zapnutou ochranou aplikací a využití
- Zaregistrovaná zařízení, vlastnosti a inventář
- Inventář aplikací a softwaru
- Konfigurace zařízení a zásady dodržování předpisů

Tyto oblasti obsahují entity, které mají smysl v daném prostředí Intune. V následujících tématech se můžete podívat na podrobnosti o sadách entit:

- [Aplikace](reports-ref-application.md)
- [Date](reports-ref-date.md) (Datum)
- [Zařízení](reports-ref-devices.md)
- [Intune Management Extension](reports-ref-intunemanagementextension.md)
- [Zásady](reports-ref-policy.md)
- [Správa mobilních aplikací (MAM)](../apps/app-management.md)
- [Uživatel](reports-ref-user.md)
- [Přidružení zařízení uživatelů](reports-ref-user-device.md)

## <a name="relationships-star-schema-model"></a>Relace: Model hvězdicového schématu

Sklad uspořádává entity do relací využitelných v rámci typů otázek, které chcete položit. Můžete například zkontrolovat počet instalací interně vyvinuté aplikace pro Android. Struktura datového skladu umožňuje získat přehled o mobilním prostředí. Analytické nástroje, jako je Microsoft Power BI, můžou používat datový model datového skladu k vytvoření vizualizací a dynamických řídicích panelů.

Entity a relace používají model hvězdicového schématu. Hvězdicové schéma vytváří korelaci faktů v časové dimenzi. *Faktem* je v kontextu modelu kvantitativní míra, jako například počet zařízení, počet aplikací nebo čas registrace. V tabulkách faktů se ukládá velké množství dat. Protože mohou být velmi rozsáhlé, omezují obvykle množství informací na 30 dnů. *Dimenze* poskytuje kontext pro fakty. Zatímco fakt udává, co se stalo, dimenze určují, komu se to stalo. Tabulky dimenzí, jako je například tabulka **Uživatelé**, jsou menší a mohou uchovávat data za delší časové období než tabulky faktů.

Model hvězdicového schématu je optimalizovaný pro flexibilitu a analýzu dat, abyste mohli vytvářet sestavy potřebné k pochopení vyvíjejícího se mobilního prostředí.

## <a name="time-daily-snapshots"></a>Čas: Denní snímky

Sklad je podřízený datům Intune. Intune pořizuje denní snímek o půlnoci v čase standardu UTC a ukládá ho do skladu. Doba uchování snímků může být u každé tabulky faktů jiná. Některé se udržují sedm dní, jiné 30 dní a některé i déle.

> [!NOTE]
> Datový sklad nesynchronizuje zařízení Jamf. Další informace o Jamf najdete v článku [řešení potíží s integrací Jamf pro s Microsoft Intune](..\protect\troubleshoot-jamf.md) a [data Jamf pro odesílá do Intune](..\protect\data-jamf-sends-to-intune.md).

## <a name="next-steps"></a>Další kroky

- Další informace o tom, jak datový sklad sleduje dobu života uživatele v Intune, získáte v článku [Znázornění životnosti uživatele v datovém skladu Microsoft Intune](reports-ref-user-timeline.md).
- Další informace o práci s datovými sklady získáte v článku, který se zabývá [vytvořením prvního datového skladu](https://www.codeproject.com/Articles/652108/Create-First-Data-WareHouse).
- Další informace o práci s Power BI a datovým skladem získáte v článku [Vytvoření nové sestavy Power BI importem sady dat](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/). 
