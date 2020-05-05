---
title: Základy správy zařízení
titleSuffix: Configuration Manager
description: Naučte se používat Configuration Manager ke správě zařízení.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722841"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Základy správy zařízení pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager může spravovat dvě rozsáhlé kategorie zařízení:

- *Klienti* jsou zařízení, jako jsou pracovní stanice, přenosné počítače, servery a mobilní zařízení, do kterých nainstalujete Configuration Manager klientský software. Některé funkce správy, jako je inventář hardwaru, vyžadují tento klientský software.  

- *Spravovaná zařízení* můžou zahrnovat *klienty*, ale obvykle se jedná o mobilní zařízení, ve kterém není nainstalovaný Configuration Manager klientský software. V tomto typu zařízení můžete spravovat pomocí integrované místní správy mobilních zařízení v Configuration Manager.

Můžete také seskupit a identifikovat zařízení založená na uživateli, nikoli pouze typ klienta.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Správa zařízení s klientem nástroje Configuration Manager

Existují dva způsoby, jak použít Configuration Manager klientský software ke správě zařízení. Prvním způsobem je zjistit zařízení v síti a poté na toto zařízení nasadit klientský software. Dalším způsobem je ruční instalace klientského softwaru do nového počítače a jeho následné připojení k vaší lokalitě, když se připojí k síti. Pokud chcete zjistit zařízení, ve kterých není nainstalovaný klientský software, spusťte jednu nebo více předdefinovaných metod zjišťování. Po zjištění zařízení použijte k instalaci klientského softwaru jednu z několika metod. Informace o použití zjišťování najdete v tématu [spuštění zjišťování pro Configuration Manager](../servers/deploy/configure/run-discovery.md).  

Po zjištění zařízení, která jsou podporována pro spuštění klientského softwaru Configuration Manager, můžete použít některou z několika metod k instalaci softwaru. Po nainstalování softwaru a přiřazení klienta k primární lokalitě můžete začít zařízení spravovat. Mezi běžné metody instalace patří:

- Klientská nabízená instalace

- Instalace na základě aktualizace softwaru

- Zásady skupiny

- Ruční instalace na počítač

- Zahrnutí klienta v rámci bitové kopie operačního systému, kterou nasazujete  

Po instalaci klienta můžete zjednodušit úlohy správy zařízení pomocí kolekcí. Kolekce jsou skupiny zařízení nebo uživatelů, které vytvoříte, abyste je mohli spravovat jako skupinu. Můžete například chtít nainstalovat aplikaci pro mobilní zařízení do všech mobilních zařízení, která Configuration Manager registrovat. V takovém případě můžete použít kolekci všechna mobilní zařízení.  

Další informace najdete v těchto článcích:  

- [Výběr řešení správy zařízení](../plan-design/choose-a-device-management-solution.md)  

- [Metody instalace klienta](../clients/deploy/plan/client-installation-methods.md)  

- [Úvod do kolekcí](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Nastavení klienta

Při první instalaci Configuration Manager jsou všichni klienti v hierarchii nakonfigurováni pomocí výchozího nastavení klienta, které můžete změnit. Mezi nastavení klienta patří tyto možnosti konfigurace:

- Jak často zařízení komunikují s lokalitou.

- Určuje, zda je klient nastaven pro aktualizace softwaru a jiné operace správy.

- Jestli si uživatelé můžou zaregistrovat svoje mobilní zařízení, aby je spravovala Configuration Manager.  

Můžete vytvořit vlastní nastavení klienta a pak je přiřadit ke kolekcím. Členové kolekce jsou nakonfigurováni tak, aby měli vlastní nastavení, a můžete vytvořit více vlastních nastavení klienta, která jsou použita v pořadí, které zadáte (podle číselného pořadí). Pokud jsou nastavení v konfliktu, má přednost nastavení s nejnižším pořadovým číslem.  

Následující diagram znázorňuje příklad vytváření a používání vlastních nastavení klienta.  

![Nastavení klienta](media/ClientSettings.gif)  

Další informace o nastavení klienta najdete v následujících článcích:

- [Postup konfigurace nastavení klienta](../clients/deploy/configure-client-settings.md)
- [O nastavení klientů](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Správa zařízení bez klienta nástroje Configuration Manager

Configuration Manager podporuje správu některých zařízení, která nemají nainstalovaný klientský software a nejsou spravována službou Intune. Další informace najdete v tématech [Správa mobilních zařízení pomocí místní infrastruktury v nástroji Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) a [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Správa na základě uživatelů

Configuration Manager podporuje kolekce uživatelů Azure Active Directory a Active Directory Domain Services. Když použijete kolekci uživatelů, můžete nainstalovat software do všech počítačů, které používají členové kolekce. Aby se zajistilo, že se software, který nasazujete, nainstaluje jenom na zařízení, která jsou určená jako primární zařízení uživatele, nastavte spřažení uživatelských zařízení. Uživatel může mít jedno či více primárních zařízení.  

Jedním ze způsobů, jak mohou uživatelé řídit nasazování softwaru, je použití klientského rozhraní **centra softwaru** . **Centrum softwaru** se automaticky nainstaluje na klientské počítače a spustí se z nabídky **Start** v systému Windows. **Centrum softwaru** umožňuje uživatelům spravovat vlastní software a provádět následující úlohy:  

- Instalovat software  

- Plánovat automatickou instalaci softwaru mimo pracovní dobu  

- Nakonfigurovat, kdy Configuration Manager může instalovat software na zařízení  

- Konfigurace nastavení přístupu pro vzdálené řízení, pokud je vzdálené řízení nastaveno v Configuration Manager  

- Konfigurace možností pro řízení spotřeby, pokud správce nastaví tuto možnost  

- Vyhledat, nainstalovat a požádat o software

- Konfigurovat nastavení předvoleb

- Po nastavení zadejte primární zařízení pro spřažení uživatelských zařízení.

Další informace najdete v těchto článcích:

- [Plánování Centra softwaru](../../apps/plan-design/plan-for-software-center.md)
- [Propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Uživatelská příručka Centra softwaru](software-center.md)
