---
title: Aplikace pro prostředí RSZ s vysokým a DoD
titleSuffix: Microsoft Intune
description: Přečtěte si o aplikacích zahrnujících prostředí RSZ s vysokým a DoD pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 29329f86-1aa5-434f-9925-8dc28bf35348
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d37bf060f11be9e295a9ef2743fa0ba33844df7
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79325887"
---
# <a name="deploying-apps-using-intune-on-the-gcc-high-and-dod-environments"></a>Nasazení aplikací pomocí Intune pro prostředí RSZ s vysokým a DoD 

Microsoft Intune je můžou používat Správci klienta k distribuci aplikací do jejich zaměstnanců. Pracovní síly jsou zaměstnanci společnosti, uživatelé aplikací. V prostředích služby Intune s vysokým nebo DoD. je možné nasadit spoustu typů aplikací. Pokud správce potřebuje nahrát a distribuovat aplikaci pro Windows, která je určená pro skupinu s vysokou nebo oslavou na základě vlastního vlastnictví, kterou vytvořili dodavatelé třetích stran, nebo jako offline aplikaci staženou z [Microsoft Store pro firmy](https://businessstore.microsoft.com/store), může ji správce rozhodnout distribuovat jako [obchodní aplikaci](apps-add.md#app-types-in-microsoft-intune).  

> [!NOTE]
> V případě komerčních prostředí může správce tenanta synchronizovat své úložiště pro firmy s Intune, ale pro prostředí RSZ High a DoD není tato služba k dispozici. Správci v této situaci musí aplikaci nasadit nahrajte přímo do Intune.  

## <a name="add-line-of-business-apps-using-intune"></a>Přidání obchodních aplikací pomocí Intune 

Pokud chcete přidat obchodní aplikaci, která je určená pro prostředí RSZ s vysokým nebo DoD pomocí Intune, můžete postupovat podle pokynů pro [aplikace pro Windows LOB](lob-apps-windows.md) . Můžete se rozhodnout nasadit Portál společnosti nejprve z Microsoft Store pro firmy. Pokud se rozhodnete použít Portál společnosti, můžete Portál společnosti nainstalovat a nasadit ručně. Další informace najdete v tématu [Jak konfigurovat aplikaci Microsoft Intune portál společnosti](company-portal-app.md). 

## <a name="distribute-offline-apps-from-the-store-for-business-using-intune"></a>Distribuce offline aplikací z obchodu pro firmy pomocí Intune  

Pokud potřebujete [stáhnout offline aplikaci licencovanou](https://docs.microsoft.com/microsoft-store/distribute-offline-apps#download-an-offline-licensed-app) z Microsoft Store pro firmy, postupujte podle těchto kroků a stáhněte aplikaci: 

1. Přihlaste se ke [Storu pro firmy](https://businessstore.microsoft.com/).
2. Vyberte **Spravovat** > **Nastavení**.
3. V části **možnosti nákupu**nastavte **Zobrazit offline aplikace** na **zapnuto**.

Pokud je v případě, že je k dispozici offline verze, při nákupu pro aplikace, můžete zvolit možnost změnit typ licence na offline. Po získání aplikace ji můžete spravovat tak, že vyberete **Spravovat** > **produkty & služby** ve [Storu pro firmy](https://businessstore.microsoft.com/). Navíc můžete stáhnout aplikaci a její závislosti. Pak můžete tuto staženou aplikaci (a její závislosti) nasadit uživatelům pomocí Intune.  

## <a name="syncing-intune-to-the-store-for-business"></a>Synchronizuje se Intune s Storem pro firmy. 

V komerčním prostředí (bez státní správy) může správce synchronizovat Intune s Microsoft Store pro firmy. Nejedná se o funkci dostupnou v prostředích státní správy. Podrobnosti o rozdílech mezi Intune v komerčních prostředích a Intune pro státní správu najdete v tématu [Enterprise mobility + Security pro popis služby pro státní správu USA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ems-govt-service-description).  

Pokud chcete synchronizovat Intune s účtem Storu pro firmy, přečtěte si téma [Správa aplikací zakoupených v Microsoft Store pro firmy pomocí Microsoft Intune](windows-store-for-business.md).  

## <a name="compliance"></a>Dodržování předpisů 

Přečtěte si prohlášení o ochraně osobních údajů a dodržování předpisů v aplikacích a porovnejte je s požadavky vaší organizace na dodržování předpisů, zabezpečení a ochrany osobních údajů, a to při vyhodnocování vhodného používání těchto služeb.   

## <a name="next-steps"></a>Další kroky

Další informace o nasazování a přiřazování aplikací najdete v článku [přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).

 
