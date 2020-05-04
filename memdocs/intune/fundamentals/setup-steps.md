---
title: Nastavit Microsoft Intune
description: Požadavky a předpoklady k tomu, abyste se vaše předplatné Intune dalo začít používat
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d158503c-1276-422b-ab81-5f66c1cd7e7a
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 53a6d38212433b786719379c0916129ea5304c21
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330603"
---
# <a name="set-up-intune"></a>Nastavení Intune

Tento postup nastavení vám umožní povolit správu mobilních zařízení (MDM) pomocí Intune. Abyste mohli dát uživatelům přístup k firemním prostředkům nebo spravovat nastavení na jejich zařízeních, musí být jejich zařízení spravovaná.

Některé kroky, například nastavení předplatného Intune a nastavení autority pro správu mobilních zařízení, jsou ve většině situací povinné. Jiné kroky, například konfigurace vlastní domény nebo přidání aplikací, jsou nepovinné a závisejí na potřebách vaší firmy.

Pokud ke správě počítačů a serverů aktuálně používáte Microsoft Endpoint Configuration Manager, můžete [Configuration Manager pomocí spolusprávy připojit k cloudu](https://docs.microsoft.com/configmgr/comanage/overview).

>[!TIP]
>Pokud zakoupíte aspoň 150 licencí v rámci opravňujícího plánu Intune, můžete využít *zvýhodnění centra FastTrack*. Tato služba vám poskytne spolupráci se specialisty Microsoftu na připravení prostředí pro službu Intune. Přečtěte si téma [Zvýhodnění centra FastTrack pro Enterprise Mobility + Security (EMS)](https://docs.microsoft.com/enterprise-mobility-security/Solutions/enterprise-mobility-fasttrack-program).

| Kroky | Status  |
|---|---|
|   1   | [Podporované konfigurace](supported-devices-browsers.md) – všechno, co potřebujete vědět, než začnete. Sem patří podporované konfigurace a požadavky na síť.|
|   2   |  [Přihlášení do Intune](account-sign-up.md) – přihlaste se ke zkušebnímu předplatnému nebo si vytvořte nové předplatné Intune. |
|   3   | [Konfigurace názvu domény](custom-domain-name-configure.md) – nastaví registraci DNS pro připojení názvu domény vaší společnosti k Intune. Při připojování k Intune a využívání prostředků pak budou uživatelé používat známou doménu. |
|   4   | [Přidání uživatelů](users-add.md) a [skupin](groups-add.md) – přidání uživatelů a skupin nebo připojení služby Active Directory k synchronizaci s Intune. Vyžaduje se, pokud vaše zařízení nepatří mezi veřejné terminály bez uživatelů. Skupiny se používají k přiřazování aplikací, nastavení a jiných prostředků.|
|   5   | [Přiřazení licencí](licenses-assign.md) – Poskytněte uživatelům oprávnění k používání Intune. Každé zařízení (s uživateli nebo bez uživatelů) vyžaduje licenci Intune, aby mělo k této službě přístup. |
|   6   | [Nastavení autority MDM](mdm-authority-set.md) – pomocí skupin uživatelů a zařízení Zjednodušte úlohy správy. Skupiny se používají k přiřazování aplikací, nastavení a jiných prostředků. |
|   7   | [Přidání aplikací](../apps/apps-add.md) – aplikace je možné přiřadit ke skupinám a automaticky nebo volitelně nainstalovat. |
|   8   | [Konfigurace zařízení](../configuration/device-profiles.md) – nastavte profily, které slouží ke správě nastavení zařízení. Profily zařízení umožňují předem nakonfigurovat nastavení e-mailu, VPN, Wi-Fi a funkcí zařízení. Dokážou zařízení rovněž omezit, což pomůže chránit samotná zařízení i data. |
|   9   |  [Přizpůsobení Portálu společnosti](../apps/company-portal-app.md) – přizpůsobte Portál společnosti Intune, který uživatelé používají k registraci zařízení a instalaci aplikací. Tato nastavení se nacházejí jak v aplikaci Portál společnosti, tak na webu Portál společnosti Intune.       |
|  10   | [Povolení registrace zařízení](mdm-authority-set.md) – povolí správu Intune pro zařízení s iOS/IPadOS, Windows, Androidem a Mac nastavením autority MDM a povolením konkrétních platforem. |
|  11   |  [Konfigurace zásad aplikací](../apps/app-protection-policy.md) – zadejte konkrétní nastavení na základě zásad ochrany aplikací v Microsoft Intune. |
