---
title: Test upgradu klienta v předprodukční kolekci
titleSuffix: Configuration Manager
description: Testování upgradu klienta v předprodukční kolekci v Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715407"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Postup testování upgradu klienta v předprodukční kolekci v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Novou verzi klienta Configuration Manager můžete otestovat v předprodukční kolekci ještě před upgradem zbytku lokality.  Když to uděláte, upgradují se jenom zařízení, která jsou součástí testovací kolekce. Jakmile budete mít možnost otestovat klienta, můžete zvýšit úroveň klienta, což zpřístupňuje novou verzi klientského softwaru pro zbytek lokality.

> [!NOTE]
> Chcete-li zvýšit úroveň testovacího klienta na produkční, musíte být přihlášeni jako uživatel s rolí zabezpečení **správce s úplnými oprávněními** a **s oborem zabezpečení.** Další informace najdete v tématu [základy správy na základě rolí](../../../understand/fundamentals-of-role-based-administration.md). Musíte být také přihlášení k serveru připojenému k lokalitě centrální správy nebo samostatné primární lokalitě nejvyšší úrovně.

 Existují 3 základní kroky pro testování klientů v předprodukčním prostředí.  

1.  Konfigurace automatických upgradů klientů pro použití předprodukční kolekce.  

2.  Nainstalujte aktualizaci Configuration Manager, která obsahuje novou verzi klienta.  

3.  Zvyšte úroveň nového klienta na produkční.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Konfigurace automatických upgradů klienta, aby používaly předprodukční kolekci  
> [!IMPORTANT]
> Nasazení předprodukčního klienta není podporováno pro počítače pracovní skupiny. Nemůžou použít ověřování vyžadované pro distribuční bod pro přístup k předprodukčnímu klientskému balíčku.  Budou dostávat nejnovějšího klienta, pokud bude povýšen na produkčního klienta.

1. [Nastavte kolekci](../collections/create-collections.md) , která obsahuje počítače, do kterých chcete nasadit předprodukčního klienta.   

2. V konzole Configuration Manager otevřete **Správa** > **Konfigurace** > lokality**lokality**a pak vyberte **Nastavení hierarchie**.  

    Na kartě **Upgrade klienta** v okně **Vlastnosti nastavení hierarchie**:  

   -   Vyberte **Upgradovat všechny klienty v předprodukční kolekci automaticky pomocí předprodukčního klienta**.  

   -   Zadejte název kolekce, která se použije jako předprodukční.  

![Testovat upgrady klientů](media/test-client-upgrades.png)

>[!NOTE]
>Chcete-li změnit tato nastavení, váš účet musí být členem role zabezpečení **správce s úplnými oprávněními** a oborem zabezpečení **vše** .


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Instalace aktualizace Configuration Manageru, která obsahuje novou verzi klienta  

1.  V konzole Configuration Manager otevřete okno**aktualizace a údržba** **pro správu** > , vyberte **dostupnou** aktualizaci a pak zvolte **instalovat balíček aktualizací**. (Před verzí 1702 se aktualizace a údržba **Administration** > **Cloud Services**.)

     Další informace o instalaci aktualizací najdete v tématu [aktualizace pro Configuration Manager](../../../../core/servers/manage/updates.md) .  

2.  Během instalace aktualizace na stránce **Možnosti klienta** v průvodci vyberte možnost **testovat v předprodukční kolekci**.  

3.  Dokončete průvodce a nainstalujte aktualizační balíček.  

     Po dokončení průvodce začnou klienti v předprodukční kolekci nasazovat aktualizovaného klienta. Nasazení upgradovaných klientů můžete monitorovat na stránce **monitorování** > **stav** > klienta**nasazení předprodukčního klienta**. Další informace najdete v tématu [monitorování stavu nasazení klienta](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Stav nasazení v počítačích hostujících role systému lokality v předprodukční kolekci může být hlášen jako **nedodržující předpisy** i v případě, že byl klient úspěšně nasazen. Když zvýšíte úroveň klienta do produkčního prostředí, stav nasazení bude uveden správně.

##  <a name="to-promote-the-new-client-to-production"></a>Zvýšení úrovně nového klienta do produkčního prostředí  

1.  V konzole Configuration Manager otevřete **Správa** > **aktualizace a údržba**a vyberte možnost **zvýšit úroveň předprodukčního klienta**. (Před verzí 1702 se aktualizace a údržba **Administration** > **Cloud Services**.)

    > [!TIP]
    > Tlačítko **Zvýšit úroveň předprodukčního klienta** je k dispozici také v případě, že monitorujete nasazení klientů v konzole v okně **Monitorování** > **Stav klienta** > **Nasazení předprodukčního klienta**.

2.  Zkontrolujte verze klientů v produkčním a předprodukčním prostředí, ujistěte se, že je zadána správná předprodukční kolekce, a potom klikněte na tlačítko **zvýšit úroveň**a pak na **Ano**.  

3.  Po zavření dialogového okna bude aktualizovaná verze klienta nahrazena verzí klienta použitou ve vaší hierarchii. Pak můžete upgradovat klienty v celé lokalitě. Další informace najdete v tématu [Postup upgradu klientů pro počítače s Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) .  

>[!NOTE]
>Pokud chcete povolit předprodukčního klienta nebo zvýšit úroveň předprodukčního klienta na produkčního klienta, musí být váš účet členem role zabezpečení, která má oprávnění **ke čtení** a **změnám** pro objekt **aktualizace balíčků** .
>Upgrady klientů dodržují všechna Configuration Manager okna údržby, která jste nakonfigurovali.
