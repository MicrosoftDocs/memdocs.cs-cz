---
title: Klientské oznámení
titleSuffix: Configuration Manager
description: Spravujte klienty tím, že převezmete okamžitou akci z konzoly centrálního Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714091"
---
# <a name="client-notification-in-configuration-manager"></a>Klientské oznámení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud chcete provést okamžitou akci na vzdálených klientech, odešlete akci oznámení klienta z konzoly Configuration Manager. Tyto akce spusťte na individuálním zařízení nebo v kolekci zařízení.

## <a name="actions"></a>Akce

Následující akce jsou na pásu karet na kartě Domů ve skupině zařízení nebo kolekce.

### <a name="install-client"></a>Nainstalovat klienta

Otevře **Průvodce instalací klienta**. Tento průvodce používá nabízenou instalaci klienta k instalaci klienta Configuration Manager. Další informace najdete v tématu [klientská nabízená instalace](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>Oprávnění – klient instalace

Tato akce vyžaduje oprávnění **Upravit prostředek** a **číst** pro objekt **kolekce** .

Ve výchozím nastavení mají tato oprávnění následující předdefinované role:

- Správce aplikace  
- Správce s úplnými oprávněními  
- Správce infrastruktury  
- Správce provozu  
- Deployment Manager operačního systému  

Přidejte tato oprávnění k libovolným vlastním rolím, které vyžadují nabízení klienta.

### <a name="run-script"></a>Spuštění skriptu

Otevře průvodce **spuštěním skriptu** pro spuštění skriptu PowerShellu na všech klientech v kolekci. Další informace najdete v tématu [vytváření a spouštění skriptů PowerShellu](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>Oprávnění – spustit skript

Tato akce vyžaduje pro objekt **kolekce** oprávnění **Run Script** .

Následující předdefinované role mají toto oprávnění ve výchozím nastavení:

- Správce s úplnými oprávněními  
- Správce infrastruktury  
- Správce provozu  

Toto oprávnění přidejte do všech vlastních rolí, které potřebují spouštět skripty.

### <a name="start-cmpivot"></a>Spustit CMPivot

Spustí **CMPivot**, které spouští dotazy v reálném čase na cílových zařízeních. Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>Oprávnění – Start CMPivot

Tato akce vyžaduje stejná oprávnění jako akce [Spustit skript](#run-script) .

Počínaje verzí 1906 můžete použít oprávnění **Run CMPivot** pro objekt **kolekce** .

## <a name="client-notification"></a>Klientské oznámení

Tyto akce jsou v nabídce **oznámení klienta** na pásu karet ve skupině zařízení nebo kolekce na kartě Domů.

Ve verzi 1806 nebo starší je možnost **oznámení klienta** dostupná jenom z uzlu kolekce zařízení nebo když jste zobrazili členství v kolekci zařízení. Počínaje verzí 1810 můžete spustit **klientské oznámení** přímo z uzlu **zařízení** . Už nemusíte mít v zobrazení členství v kolekci žádné požadavky. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Oprávnění – klientské oznámení

<!--SCCMDocs-pr issue #2972-->
Počínaje verzí 1810 budou akce oznámení klienta nyní vyžadovat oprávnění **oznámit prostředek** u objektu Collection. Toto oprávnění platí pro všechny akce v nabídce **oznámení klienta** .

Následující předdefinované role mají toto oprávnění ve výchozím nastavení:

- Správce s úplnými oprávněními  
- Správce provozu  

Toto oprávnění přidejte do všech vlastních rolí, které potřebují používat akce klientských oznámení.

### <a name="download-computer-policy"></a>Stáhnout zásady počítače

Aktualizujte zásady zařízení. Další informace najdete v tématu [spuštění načtení zásad pro klienta Configuration Manager](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Stáhnout zásady uživatele

Aktualizujte zásady uživatele.  

### <a name="collect-discovery-data"></a>Shromáždit data zjišťování

Spustí klienty pro odeslání záznamu dat zjišťování (DDR). Další informace najdete v tématu [zjišťování prezenčního signálu](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

### <a name="collect-software-inventory"></a>Shromáždit inventář softwaru

Spustí klienty pro spuštění cyklu inventáře softwaru. Další informace najdete v tématu [Úvod do inventáře softwaru](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Shromáždění inventáře hardwaru

Spustí klienty pro spuštění cyklu inventáře hardwaru. Další informace najdete v tématu [Úvod do inventáře hardwaru](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Vyhodnotit nasazení aplikací

Spustí klienty pro spuštění cyklu vyhodnocení nasazení aplikace. Další informace najdete v tématu [Plánování opětovného vyhodnocení nasazení](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Vyhodnotit nasazení aktualizací softwaru

Spustí klienty, aby spouštěli cyklus vyhodnocení nasazení aktualizací softwaru. Další informace najdete v tématu [Úvod do aktualizací softwaru](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Přepnout na další bod aktualizace softwaru

Spustí klienty pro přepnutí do dalšího dostupného bodu aktualizace softwaru. Další informace najdete v tématu [Přepínání bodů aktualizace softwaru](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Vyhodnotit ověření stavu zařízení

Aktivujte klientům Windows 10 kontrolu a odeslání nejnovějšího stavu zařízení. Další informace najdete v tématu [ověření stavu](../../servers/manage/health-attestation.md).  

### <a name="wake-up"></a>Probuď se

Počínaje verzí 1810 můžete aktivovat zařízení nakonfigurovaná tak, aby podporovala funkci Wake-on-LAN k probuzení pomocí dalších zařízení ve stejné podsíti k odeslání balíčku Wake-on-LAN. Další informace najdete v tématu [Postup konfigurace funkce Wake on LAN](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Restartování

Aktivovat vybraná zařízení k restartování Další informace najdete v tématu [restart klientů](manage-clients.md#restart-clients).

## <a name="client-diagnostics"></a>Diagnostika klienta
<!--4433455-->

Počínaje verzí 1910 existují nové akce zařízení pro **diagnostiku klienta** v konzole Configuration Manager. Byly přidány následující akce:

- **Zapnout podrobné protokolování**: změňte úroveň globálního protokolu pro komponentu ccm na Verbose a povolte protokolování ladění.
- **Zakázat podrobné protokolování**: změňte úroveň globálního protokolu na výchozí a zakažte protokolování ladění.
- **Shromažďovat protokoly klientů** (počínaje 2002): pro shromáždění protokolů ccm se vybraným klientům pošle zpráva s klientským oznámením. Protokoly se vrátí pomocí kolekce souborů inventáře softwaru. <!--4226618-->
   - Omezení velikosti pro komprimované protokoly klienta je 100 MB. <!--6366098-->
   - Pomocí [Průzkumník prostředků](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) spravovat a zobrazovat tyto soubory.

   [![Shromažďovat protokoly klientů z konzoly](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Tyto akce mění pouze podrobnosti protokolu, nikoli velikost nebo historii. Podrobnější protokolování může vygenerovat další obsah protokolu.
> - Role bodu správy používá také komponentu CCM. Pokud cílové zařízení je také bodem správy, tato akce se vztahuje také na tuto roli.

Další informace o těchto nastaveních najdete v tématu [informace o souborech protokolu](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client).

Sledujte stav úlohy v **diagnostice. log** v klientovi. Po shromáždění protokolů klienta jsou další informace přihlášeny **MP_SinvCollFile. log** v bodu správy a **protokolu Sinvproc. log** na serveru lokality.

### <a name="prerequisites---client-diagnostics"></a>Předpoklady – Diagnostika klientů

- Aktualizujte cílového klienta na nejnovější verzi.

- Váš Configuration Manager administrativní uživatel potřebuje oprávnění pro **oznamování prostředků** .

  Následující předdefinované role mají toto oprávnění ve výchozím nastavení:

  - Správce s úplnými oprávněními  
  - Správce infrastruktury  

  Toto oprávnění přidejte do všech vlastních rolí, které potřebují používat akce klientských oznámení.


## <a name="endpoint-protection"></a>Funkce Endpoint Protection

Následující akce jsou v rámci nabídky **Endpoint Protection** . Tato nabídka se nachází na pásu karet ve skupině kolekce na kartě Domů. Když vyberete jedno nebo několik zařízení, tyto akce se nachází na kartě **vybraný objekt** na pásu karet.

Další informace najdete v tématu [Endpoint Protection v Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).

### <a name="permissions---endpoint-protection"></a>Oprávnění – Endpoint Protection

Tato akce vyžaduje oprávnění **vynutí zabezpečení** pro objekt **kolekce** .

Následující předdefinované role mají toto oprávnění ve výchozím nastavení:

- Správce s úplnými oprávněními  
- Endpoint Protection Manager  
- Správce provozu  

Toto oprávnění přidejte do všech vlastních rolí, které potřebují aktivovat Endpoint Protection akce.

### <a name="full-scan"></a>Úplná kontrola

Spustí Endpoint Protection nebo Windows Defender pro spuštění *úplné* kontroly malwaru.  

### <a name="quick-scan"></a>Rychlá kontrola

Spustí Endpoint Protection nebo Windows Defender pro spuštění *rychlé* kontroly malwaru.  

### <a name="download-definition"></a>Definice stažení

Aktivujte Endpoint Protection nebo Windows Defender a Stáhněte si nejnovější antimalwarové definice.  

## <a name="see-also"></a>Viz také

- [Správa klientů](manage-clients.md)
- [Správa kolekcí](collections/manage-collections.md)
