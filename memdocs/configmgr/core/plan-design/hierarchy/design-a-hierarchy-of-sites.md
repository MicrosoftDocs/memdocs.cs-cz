---
title: Návrh hierarchie lokality
titleSuffix: Configuration Manager
description: Seznamte se s dostupnými topologiemi a možnostmi správy pro Configuration Manager pro plánování hierarchie lokality.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073343"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Návrh hierarchie lokalit pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Před instalací první lokality nové hierarchie Configuration Manager je vhodné pochopit tyto informace:  

- Dostupné topologie pro Configuration Manager  

- Typy dostupných lokalit a jejich vztahů mezi sebou  

- Rozsah správy, který poskytuje každý typ webu  

- Možnosti správy obsahu, které mohou snížit počet lokalit, které je třeba nainstalovat  

Pak Naplánujte topologii, která efektivně zachovává vaše aktuální obchodní potřeby a později ji můžete rozšířit pro správu budoucího růstu.  

Při plánování mějte na paměti omezení pro přidání dalších lokalit do hierarchie nebo samostatné lokality:  

- Nainstalujte novou primární lokalitu pod lokalitu centrální správy až do [podporovaného počtu primárních lokalit](../configs/size-and-scale-numbers.md) pro hierarchii.  

- [Rozšíření samostatné primární lokality pro instalaci nové lokality centrální správy](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)pro instalaci dalších primárních lokalit.  

- Nainstalujte nové sekundární lokality pod primární lokalitu až do [podporovaného limitu pro primární lokalitu](../configs/size-and-scale-numbers.md) a celkovou hierarchii.  

- Dříve nainstalovanou lokalitu nelze do existující hierarchie přidat, aby bylo možné sloučit dvě samostatné lokality. Configuration Manager podporuje jenom instalaci nových lokalit do existující hierarchie lokalit.  


> [!NOTE]  
> Při plánování nové instalace Configuration Manager mějte na paměti [poznámky k verzi](../../servers/deploy/install/release-notes.md), které podrobně popisují aktuální problémy v aktivních verzích. Poznámky k verzi platí pro všechny větve Configuration Manager. Pokud používáte [větev Technical Preview](../../get-started/technical-preview.md), najděte problémy specifické pro tuto větev v dokumentaci k jednotlivým verzím Technical Preview.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a>Topologie hierarchie  

Topologie hierarchie v rozsahu od:  

- Nejjednodušší: jedna samostatná primární lokalita  

- Nejvíc složitá: skupina propojených primárních a sekundárních lokalit s lokalitou centrální správy v lokalitě nejvyšší úrovně v hierarchii.  

Klíčovým ovladačem typu a počtu lokalit, které používáte v hierarchii, je obvykle počet a typ zařízení, která musíte podporovat.   

### <a name="standalone-primary-site"></a>Samostatná primární lokalita

Samostatnou primární lokalitu použijte, když může podporovat správu všech zařízení a uživatelů. Další informace najdete v tématu nastavení [velikosti a škálování](../configs/size-and-scale-numbers.md). Tato topologie je také úspěšná, když se geografické umístění vaší společnosti dá obsluhovat pomocí jedné primární lokality. Pro usnadnění správy síťového provozu použijte více bodů správy ve skupinách hranic a pečlivě plánovanou infrastrukturu obsahu. Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md) a [základní koncepty správy obsahu](fundamental-concepts-for-content-management.md).  

Tato topologie nabízí následující výhody:  

- Zjednodušení režie správy.  

- Zjednodušení přiřazování klientských lokalit a zjišťování dostupných prostředků a služeb.  

- Eliminace možných zpoždění zavedených replikací databáze mezi lokalitami  

- Možnost rozšířit samostatnou primární lokalitu do větší hierarchie s lokalitou centrální správy. Tato možnost umožňuje nainstalovat nové primární lokality a rozšířit tak škálování vašeho nasazení.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Lokalita centrální správy s jednou nebo více podřízenými primárními lokalitami 

Tuto topologii použijte, pokud požadujete víc než jednu primární lokalitu, která bude podporovat správu všech zařízení a uživatelů. Je vyžadován, pokud potřebujete použít více než jednu primární lokalitu. 

Tato topologie nabízí následující výhody:  

- Podporuje až 25 primárních lokalit, které umožňují rozšířit škálování vaší hierarchie.    

- Lokalitu centrální správy vždy používáte, pokud nepřeinstalujete své lokality. Tato možnost je trvalá. Podřízenou primární lokalitu nelze odpojit, aby mohla být samostatnou primární lokalitou.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a>Určení, kdy použít lokalitu centrální správy  

Pomocí lokality centrální správy můžete nakonfigurovat nastavení pro celou hierarchii a monitorovat všechny lokality a objekty v hierarchii. Tento typ lokality nespravuje klienty přímo. Koordinuje replikaci dat mezi lokalitami, což zahrnuje konfiguraci lokalit a klientů v celé hierarchii.  

Při rozhodování, kdy nainstalovat lokalitu centrální správy, vám můžou pomoct následující informace:  

- Lokalita centrální správy je lokalita nejvyšší úrovně v hierarchii.  

- Když nakonfigurujete hierarchii, která má více než jednu primární lokalitu, nainstalujete lokalitu centrální správy.  

     - Pokud okamžitě potřebujete dvě nebo víc primárních lokalit, nainstalujte nejdřív lokalitu centrální správy.  

     - Pokud již máte primární lokalitu a chcete nainstalovat lokalitu centrální správy, [pomocí rozšíření samostatné primární lokality](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) nainstalujte lokalitu centrální správy.  

- Lokalita centrální správy podporuje pouze primární lokality jako podřízené lokality.  

- Lokalita centrální správy nemůže mít přiřazené klienty.  

- Lokalita centrální správy nepodporuje role systému lokality, které přímo podporují klienty, jako jsou body správy a distribuční body.  

- Spravujte všechny klienty v hierarchii a proveďte všechny úlohy správy lokality z konzoly Configuration Manager, která je připojená k lokalitě centrální správy. Tyto úlohy zahrnují instalaci bodů správy nebo jiných rolí systému lokality v podřízených primárních nebo sekundárních lokalitách.  

- Pokud používáte lokalitu centrální správy, je to jediné místo, kde vidíte data lokality ze všech lokalit ve vaší hierarchii. Tato data obsahují informace, jako jsou data inventáře a stavové zprávy.  

- Nakonfigurujte operace zjišťování v celé hierarchii z lokality centrální správy. Z lokality centrální správy přiřaďte metody zjišťování, které se mají spouštět v jednotlivých primárních lokalitách.  

- Spravujte zabezpečení v celé hierarchii přiřazením různých rolí zabezpečení, oborů zabezpečení a kolekcí různým administrativním uživatelům. Tyto konfigurace platí v každé lokalitě v hierarchii.  

- Nakonfigurujte replikaci pro řízení komunikace mezi lokalitami v hierarchii. Plánování replikace databáze pro data lokality a Správa šířky pásma pro přenos dat založených na souborech mezi lokalitami.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a>Určení, kdy použít primární lokalitu  

Primární lokality slouží ke správě klientů. Nainstalujte primární lokalitu jako podřízenou lokalitu pod lokalitou centrální správy nebo jako první lokalitu nové hierarchie. Primární lokalita, která je první lokalitou hierarchie, vytvoří samostatnou primární lokalitu. Podřízené primární lokality i samostatné primární lokality podporují sekundární lokality.  

Zvažte přidání dalších primárních lokalit z následujících důvodů:  

- Pokud chcete zvýšit počet zařízení, spravujte s jedinou hierarchií.  

- Splnění organizačních požadavků správy. Například můžete nainstalovat primární lokalitu ve vzdáleném umístění pro správu přenosu obsahu nasazení v síti s malou šířkou pásma.  

     - Zvažte místo toho použití možností k omezení šířky pásma sítě při přenosu dat do distribučního bodu. Tato funkce správy obsahu může nahradit nutnost instalace dalších lokalit.  


Následující informace vám pomohou při rozhodování, kdy nainstalovat primární lokalitu:  

- Primární lokalitou může být samostatná primární lokalita nebo podřízená primární lokalita v rozsáhlejší hierarchii. Když je primární lokalita členem hierarchie s lokalitou centrální správy, lokality používají k replikování dat mezi sebou replikaci databáze. Pokud nepotřebujete podporovat více klientů a zařízení, než podporuje jedna primární lokalita, zvažte instalaci samostatné primární lokality. Když nainstalujete samostatnou primární lokalitu, rozbalte ji v případě potřeby v budoucnu, abyste nahlásili novou lokalitu centrální správy pro horizontální navýšení kapacity nasazení.  

- Primární lokalita podporuje pouze lokalitu centrální správy jako nadřazenou lokalitu.  

- Primární lokalita podporuje jenom sekundární lokality jako podřízené lokality a podporuje víc sekundárních lokalit.  

- Primární lokality jsou zodpovědné za zpracování všech klientských dat z klientů, kteří jsou jim přiřazeni.  

- Primární lokality používají replikaci databáze k přímé komunikaci s příslušnou lokalitou centrální správy. Toto chování se konfiguruje automaticky při instalaci nové lokality.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a>Určení, kdy použít sekundární lokalitu  

Pomocí sekundárních lokalit můžete spravovat přenos obsahu nasazení a dat klientů napříč sítěmi s malou šířkou pásma.  

Sekundární lokalitu lze spravovat z lokality centrální správy nebo z primární lokality přímé nadřazené lokality. Sekundární lokality jsou připojeny k primární lokalitě. Nemůžete je přesunout do jiné nadřazené lokality, aniž byste je odinstalovali a znovu nainstalovali jako podřízenou lokalitu pod novou primární lokalitou.

Můžete ale směrovat obsah mezi dvěma partnerskými sekundárními lokalitami, aby se usnadnila Správa replikace obsahu nasazení na základě souborů. Chcete-li přenést data klienta do primární lokality, sekundární lokalita používá replikaci na základě souborů. Sekundární lokalita používá replikaci databáze taky pro komunikaci se svou nadřazenou primární lokalitou.  

Pokud platí kterákoli z následujících podmínek, zvažte instalaci sekundární lokality:  

- Pro administrativního uživatele nepožadujete místní bod připojení.  

- Je nutné spravovat přenos obsahu nasazení do lokalit, které jsou v hierarchii nižší.  

- Musíte spravovat informace o klientech, které se odesílají do lokalit vyšších v hierarchii.  

Pokud nechcete instalovat sekundární lokalitu a máte klienty ve vzdálených umístěních, zvažte následující možnosti:  

- Použití technologií peer-to-peer, jako je Windows BranchCache  

- Povolení distribučních bodů pro řízení a plánování šířky pásma   

Tyto možnosti správy obsahu můžete používat s sekundárními lokalitami nebo bez nich. Můžou snížit velikost vaší infrastruktury Configuration Manager. Další informace o možnostech správy obsahu v Configuration Manager najdete v tématu [určení, kdy použít možnosti správy obsahu](#BKMK_ChooseSecondaryorDP).  


Při rozhodování, kdy nainstalovat sekundární lokalitu, vám můžou pomoct následující informace:  

- Pokud není k dispozici místní instance SQL Server, servery sekundární lokality se při instalaci lokality automaticky nainstalují SQL Server Express.  

- Instalace sekundárního webového serveru je inicializovaná z konzoly Configuration Manager místo spuštění instalačního programu přímo v počítači.  

- Sekundární lokality používají podmnožinu informací v databázi lokality. Toto chování snižuje množství dat, která SQL replikuje mezi nadřazenou primární lokalitou a sekundární lokalitou.  

- Sekundární lokality podporují směrování obsahu založeného na souborech do jiných sekundárních lokalit, které mají společnou nadřazenou primární lokalitu.  

- Instalace sekundární lokality automaticky instalují role systému lokality bodu správy a distribučního bodu na serveru sekundární lokality.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a>Určení, kdy použít možnosti správy obsahu  

Pokud se někteří vaši klienti nacházejí ve vzdálených síťových umístěních, zvažte namísto primární nebo sekundární lokality použití jedné nebo více možností správy obsahu. Následující možnosti často odstraňují nutnost instalace lokality:  

- Optimalizace doručení pro Windows 10  

- Configuration Manager sdílené mezipaměti  

- Služba BranchCache systému Windows  

- Konfigurace distribučních bodů pro řízení šířky pásma  

- Ručně kopírovat obsah do distribučních bodů (připravený obsah)  


Pokud platí kterákoli z následujících podmínek, zvažte nasazení distribučního bodu namísto instalace další lokality:  

- Šířka pásma sítě je dostatečná pro klientské počítače ve vzdáleném umístění ke komunikaci s bodem správy v primární lokalitě. Klienti komunikují s bodem správy, aby stáhli zásady klienta, odesílali inventář, odesílali stav generování sestav a odesílali informace o zjišťování.  

- Background Intelligent Transfer Service (BITS) neposkytuje dostatečnou kontrolu šířky pásma pro vaše požadavky na síť.  

Další informace o možnostech správy obsahu v Configuration Manager najdete v tématu [základní koncepty správy obsahu](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a>Rámec topologie hierarchie  

Společně s vaší počáteční topologií hierarchie Zvažte také následující otázky:  

- Které role systému lokality poskytují služby nebo možnosti z různých lokalit v hierarchii?  

- Jak ve vaší infrastruktuře spravujete konfigurace a možnosti v rámci hierarchie?  


V samostatných článcích jsou uvedeny následující běžné požadavky. Tyto informace jsou důležité pro ovlivnění nebo ovlivnění návrhem hierarchie:  

- Když připravujete [správu počítačů a zařízení](../../clients/manage/manage-clients.md), zvažte, jestli jsou zařízení v místním prostředí, v cloudu nebo zahrnuje zařízení vlastněná uživateli (BYOD). Zvažte také, jak budete spravovat zařízení, která podporují více možností správy. Můžete například spravovat zařízení s Windows 10 pomocí Configuration Manager nebo i když Integrujte s Microsoft Intune. Další informace najdete v tématu [Volba řešení pro správu zařízení](../choose-a-device-management-solution.md).  

- Pochopte, jak může vaše dostupná síťová infrastruktura ovlivnit tok dat mezi vzdálenými umístěními. Další informace najdete v tématu [Příprava síťového prostředí](../network/configure-firewalls-ports-domains.md). Zvažte také zeměpisnou polohu vašich uživatelů a zařízení a to, jestli mají přístup k vaší infrastruktuře prostřednictvím místní sítě nebo Internetu.  

- Plánování infrastruktury obsahu pro efektivní distribuci obsahu, který nasazujete, do zařízení, která spravujete. Tento obsah může být aplikace, aktualizace softwaru nebo operační systémy. Další informace najdete v tématu [Správa obsahu a infrastruktury obsahu](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

- Určete, jaké [funkce a možnosti Configuration Manager](../changes/features-and-capabilities.md) plánujete použít. Různé funkce vyžadují různé role systému lokality nebo infrastrukturu Windows. V hierarchii více lokalit se rozhodněte, kam je nasadíte pro nejúčinnější používání prostředků sítě a serveru.  

- Zvažte zabezpečení dat a zařízení, včetně použití infrastruktury veřejných klíčů (PKI). Další informace najdete v tématu [požadavky na certifikát PKI](../network/pki-certificate-requirements.md).  


Projděte si následující články pro konfigurace specifické pro lokalitu:  

- [Plánování poskytovatele serveru SMS](plan-for-the-sms-provider.md)  

- [Plánování databáze lokality](plan-for-the-site-database.md)  

- [Plánování systémových serverů lokality a rolí systémů lokality](plan-for-site-system-servers-and-site-system-roles.md)  

- [Plánování zabezpečení](../security/plan-for-security.md)  

- [Správa šířky pásma sítě](manage-network-bandwidth.md) při nasazování obsahu v rámci lokality.  


Zvažte konfigurace, které zahrnují lokality a hierarchie.  

- [Možnosti vysoké dostupnosti](../../servers/deploy/configure/high-availability-options.md) pro lokality a hierarchie

- [Rozšíříte schéma služby Active Directory](../network/extend-the-active-directory-schema.md) a nakonfigurujete lokality pro [publikování dat lokality](../../servers/deploy/configure/publish-site-data.md) .  

- [Přenos dat mezi lokalitami](data-transfers-between-sites.md)  

- [Základy správy na základě rolí](../../understand/fundamentals-of-role-based-administration.md)  

- [Správa klientů na internetu](../../clients/manage/manage-clients-internet.md)  

