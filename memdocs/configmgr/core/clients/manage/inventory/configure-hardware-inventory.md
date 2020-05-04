---
title: Konfigurace inventáře hardwaru
titleSuffix: Configuration Manager
description: Nastavte inventář hardwaru pro všechny klienty nebo pro kolekci v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714434"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Postup konfigurace inventáře hardwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento postup nakonfiguruje výchozí nastavení klienta pro inventář hardwaru a použije se pro všechny klienty ve vaší hierarchii. Pokud chcete toto nastavení použít jenom pro některé klienty, vytvořte vlastní nastavení klienta zařízení a přiřaďte ho kolekci obsahující zařízení, pro která chcete použít inventář hardwaru. Viz [Jak konfigurovat nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Pokud zařízení klienta obdrží nastavení inventáře hardwaru z více sad nastavení klienta, budou při hlášení inventáře hardwaru klientem třídy inventáře hardwaru ze všech sad nastavení sloučeny. Kromě toho není při kontrole třídy ve vlastním nastavení klienta s vyšší prioritou zakázán klientu v inventarizaci této třídy. 

Chcete-li zakázat konkrétní třídu inventáře hardwaru u většiny systémů s výjimkou několika málo, třída musí být ve výchozím nastavení klienta nezaškrtnuta. Pak vytvořte vlastní nastavení klienta, které povolí třídu, a nasaďte ji do cílových systémů.


### <a name="to-configure-hardware-inventory"></a>Konfigurace inventáře hardwaru  

1.  V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

4.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

5.  V dialogovém okně **výchozí nastavení** vyberte **inventář hardwaru**.  

6.  V seznamu **Nastavení zařízení** nakonfigurujte toto nastavení:  

    -   **Povolit inventář hardwaru na klientských počítačích** – vyberte **Ano**.  

    -   **Plán inventáře hardwaru** – klikněte na **plán** a zadejte interval, ve kterém Klienti shromažďují inventář hardwaru.  

7.  Nakonfigurujte další [nastavení klienta inventáře hardwaru](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) , která požadujete.  

Při příštím stažení zásad klienta budou klientská zařízení nakonfigurovaná pomocí tohoto nastavení. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../../../../core/clients/manage/manage-clients.md).  
