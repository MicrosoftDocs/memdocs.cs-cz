---
title: Nasazení a aktualizace Microsoft Edge verze 77 a novější
titleSuffix: Configuration Manager
description: Jak nasadit a aktualizovat Microsoft Edge verze 77 a novější pomocí Configuration Manager
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 423864c2c954cc67da4ef54d55d7263ae346e786
ms.sourcegitcommit: 24ce7df7dadf2385afe364b817ec58feeb04c700
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86212296"
---
# <a name="microsoft-edge-management"></a>Správa Microsoft Edge

*Platí pro: Configuration Manager (Current Branch)*

Microsoft Edge pro všechny nové je připravený pro firmy. Od verze Configuration Manager 1910 teď můžete k vašim uživatelům nasadit [Microsoft Edge, verze 77 a novější](https://docs.microsoft.com/deployedge/) . Skript PowerShellu se používá k instalaci hraničního sestavení vybraného. Skript také vypne automatické aktualizace pro Edge, aby bylo možné je spravovat pomocí Configuration Manager.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>Nasazení Microsoft Edge
<!--4561024-->
Správci si můžou vybrat beta verzi, vývoj nebo stabilní kanál spolu s verzí klienta Microsoft Edge, která se má nasadit. Každé vydání zahrnuje učení a vylepšení od našich zákazníků a komunity.

### <a name="prerequisites-for-deploying"></a>Předpoklady pro nasazení

Pro klienty cílené na nasazení Microsoft Edge:

- [Zásady spouštění](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) prostředí PowerShell nemůžou být nastavené na omezené.
  - K provedení instalace se provede PowerShell.

- Instalační program Microsoft Edge a [CMPivot](../../core/servers/manage/cmpivot.md) se podepisují pomocí certifikátu **Microsoft Code Signing** Certificate. Pokud tento certifikát není uvedený v úložišti **důvěryhodných vydavatelů** , budete ho muset přidat. V opačném případě se instalační program Microsoft Edge a CMPivot nespustí, pokud jsou zásady spouštění prostředí PowerShell nastavené na **AllSigned**. <!--7585106-->

Zařízení, na kterém běží Konzola Configuration Manager, potřebuje přístup k následujícím koncovým bodům:

|Umístění|Použití|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Informace o vydaných verzích Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Obsah pro Microsoft Edge releases|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a>Ověření zásad aktualizace Microsoft Edge

#### <a name="configuration-manager-version-1910"></a>Configuration Manager verze 1910

Při nasazení Microsoft Edge ve verzi 1910 instalační skript vypne automatické aktualizace pro Microsoft Edge, aby bylo možné je spravovat pomocí Configuration Manager. Toto chování můžete změnit pomocí Zásady skupiny. Další informace najdete v tématu [Plánování nasazení Microsoft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) a [zásad aktualizace Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies).

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager verze 2002 a novější
<!--4561024-->
Počínaje verzí 2002 můžete vytvořit aplikaci Microsoft Edge, která je nastavená tak, aby přijímala automatické aktualizace, a nemusíte mít zakázané automatické aktualizace. Tato změna vám umožní spravovat aktualizace pro Microsoft Edge pomocí Configuration Manager nebo povolit automatické aktualizace Microsoft Edge. Když vytváříte aplikaci, vyberte možnost **dovolit, aby Microsoft Edge automaticky aktualizoval verzi klienta na zařízení koncového uživatele** na stránce **nastavení Microsoft Edge** . Pokud jste dříve použili Zásady skupiny ke změně tohoto chování, Zásady skupiny přepsat nastavení provedené Configuration Manager během instalace Microsoft Edge.

[![Nastavení automatických aktualizací Microsoft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Vytvoření nasazení

Vytvořte aplikaci Microsoft Edge pomocí integrovaného prostředí aplikací, které usnadňuje správu Microsoft Edge:

1. V konzole nástroje je v části **softwarová knihovna**k dispozici nový uzel s názvem **Správa Microsoft Edge**.
1. Vyberte možnost **vytvořit aplikaci Microsoft Edge** z pásu karet nebo kliknutím pravým tlačítkem myši na uzel **Microsoft Edge Management** .

   ![Akce kliknutí pravým tlačítkem myši na uzel správy Microsoft Edge](./media/4561024-create-microsoft-edge-application.png)

1. Na stránce **nastavení aplikace** v průvodci zadejte název, popis a umístění obsahu aplikace. Zajistěte, aby složka umístění obsahu, kterou zadáte, byla prázdná.
1. Na stránce **nastavení Microsoft Edge** vyberte:
   - Kanál k nasazení
   - Verze, která se má nasadit
   - Pokud chcete, aby **Microsoft Edge mohl automaticky aktualizovat verzi klienta na zařízení koncového uživatele** (přidáno ve verzi 2002)
1. Na stránce **nasazení** se rozhodněte, jestli chcete aplikaci nasadit. Pokud vyberete **Ano**, můžete zadat nastavení nasazení pro aplikaci. Další informace o nastavení nasazení najdete v tématu [nasazení aplikací](deploy-applications.md#bkmk_deploy-general).
1. V nástroji **Software Center** na klientském zařízení může uživatel zobrazit a nainstalovat aplikaci.

   ![Stránka nastavení Microsoft Edge v Průvodci nasazením](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Soubory protokolu pro nasazení

|Umístění|Protokol|Použití|
|---|---|---|
| Server lokality|SMSProv.log|Zobrazí podrobnosti o neúspěšném vytvoření aplikace nebo nasazení.|
| [Různé](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Zobrazí podrobnosti o neúspěšném stažení obsahu.|
| Klient|  AppEnforce.log|Zobrazuje informace o instalaci.|

## <a name="update-microsoft-edge"></a>Aktualizovat Microsoft Edge
<!--4831871-->

Configuration Manager počínaje verzí 1910 se na **webu Microsoft Edge Management**zobrazí uzel s názvem **všechny aktualizace Microsoft Edge** . Tento uzel vám pomůže spravovat aktualizace pro všechny kanály Microsoft Edge.<!--initial edge updates released Jan 15,2020-->

1. Pokud chcete získat aktualizace pro Microsoft Edge, ujistěte se, že máte klasifikaci **aktualizací** a produkt **Microsoft Edge** [vybraný pro synchronizaci](../../sum/get-started/configure-classifications-and-products.md).

   [![Vybrat Microsoft Edge jako produkt ve vlastnostech bodu aktualizace softwaru](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. V pracovním prostoru **softwarová knihovna** rozbalte položku **Microsoft Edge Management** a klikněte na uzel **všechny aktualizace Microsoft Edge** .

1. V případě potřeby klikněte na pásu karet na **synchronizovat aktualizace softwaru** a spusťte synchronizaci. Další informace najdete v tématu [synchronizace aktualizací softwaru](../../sum/get-started/synchronize-software-updates.md).

   ![Všechny uzly aktualizací Microsoft Edge](./media/4831871-all-microsoft-edge-updates.png)

1. Spravujte a nasaďte aktualizace Microsoft Edge jako jakoukoli jinou aktualizaci, například jejich přidání do [pravidla automatického nasazení](../../sum/deploy-use/automatically-deploy-software-updates.md). Některé běžné úlohy aktualizace, které můžete provádět v uzlu **všechny aktualizace Microsoft Edge** , zahrnují:

   - [Vytvoření postupného nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Ruční nasazení aktualizací softwaru](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Stažení aktualizací softwaru](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a>Řídicí panel pro správu Microsoft Edge
<!--3871913-->
*(Představené ve verzi 2002)*

Od Configuration Manager 2002 se řídicí panel pro správu Microsoft Edge poskytuje přehledy o využití Microsoft Edge a dalších prohlížečů. V tomto řídicím panelu můžete:

- Podívejte se, kolik vašich zařízení má nainstalované Microsoft Edge.
- Podívejte se, kolik klientů má nainstalované různé verze Microsoft Edge.
   - Tento graf nezahrnuje Kanárské kanál.
- Zobrazení nainstalovaných prohlížečů v různých zařízeních
- Zobrazit preferovaný prohlížeč podle zařízení <!--5907383-->
   - V současnosti pro vydání 2002 bude tento graf prázdný.

### <a name="prerequisites-for-the-dashboard"></a>Předpoklady pro řídicí panel

V níže uvedených třídách [inventáře hardwaru](../../core/clients/manage/inventory/extend-hardware-inventory.md) pro řídicí panel Microsoft Edge Management Povolte následující vlastnosti:

- **Nainstalovaný software-funkce Asset Intelligence (SMS_InstalledSoftware)**
   - Softwarový kód
   - Název produktu
   - Verze produktu

- **Výchozí prohlížeč (SMS_DefaultBrowser)**
   - ID programu prohlížeče

- **Použití prohlížeče (SMS_BrowserUsage)**
   - Browser
   - UsagePercentage

### <a name="view-the-dashboard"></a>Zobrazení řídicího panelu

V pracovním prostoru **softwarová knihovna** klikněte na **Správa Microsoft Edge** a zobrazte řídicí panel. Změňte kolekci dat grafu kliknutím na **Procházet** a výběrem jiné kolekce. Ve výchozím nastavení se v rozevíracím seznamu nacházejí pět největších kolekcí. Když vyberete kolekci, která není v seznamu, nově vybraná kolekce vezme v rozevíracím seznamu na spodní místo.

[![Řídicí panel pro správu Microsoft Edge](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>Známé problémy

### <a name="hardware-inventory-may-fail-to-process"></a>Zpracování inventáře hardwaru se nemusí zdařit.
<!--7535675-->
Zpracování inventáře hardwaru pro zařízení se nemusí zdařit. V souboru Dataldr. log se mohou zobrazit chyby podobné následujícímu:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Omezení rizik:** Pokud chcete tento problém obejít, zakažte shromažďování třídy inventáře hardwaru využití prohlížeče (SMS_BrowerUsage).

## <a name="next-steps"></a>Další kroky

[Monitorování aplikací](monitor-applications-from-the-console.md)

[Monitorování aktualizací softwaru](../../sum/deploy-use/monitor-software-updates.md)

[Správa a sledování postupných nasazení](../../osd/deploy-use/manage-monitor-phased-deployments.md)
