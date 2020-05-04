---
title: Role systému lokality pro klienty
titleSuffix: Configuration Manager
description: Určete role systému lokality pro klienty v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713244"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Určení rolí systému lokality pro klienty Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek vám může přispět k určení rolí systému lokality, které potřebujete k nasazení Configuration Manager klientů.

Další informace o tom, kam tyto role nainstalovat v hierarchii, najdete v tématu [Návrh hierarchie lokalit](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Další informace o instalaci a konfiguraci těchto rolí najdete v tématu [Instalace rolí systému lokality](../../../servers/deploy/configure/install-site-system-roles.md).  

## <a name="management-point"></a>Bod správy

Ve výchozím nastavení všechny klientské počítače se systémem Windows používají k instalaci klienta Configuration Manager distribuční bod. Můžou přejít zpátky do bodu správy, pokud není dostupný distribuční bod. Když ale použijete vlastnost `/source:<Path>`příkazového řádku CCMSetup, můžete na počítače nainstalovat klienty systému Windows z alternativního zdroje. Tuto akci můžete třeba provést, pokud instalujete klienty na Internet. Dalším scénářem je situace, kdy chcete zabránit posílání síťových paketů mezi počítačem a bodem správy během instalace klienta. Tato situace je způsobená tím, že brána firewall blokuje požadované porty nebo máte připojení s malou šířkou pásma. Všichni klienti však musí komunikovat s bodem správy, aby je bylo možné přiřadit k lokalitě a spravovat je pomocí Configuration Manager.  

Další informace o vlastnostech příkazového řádku klienta najdete v tématu [informace o vlastnostech instalace klienta](../about-client-installation-properties.md).  

Když v hierarchii nainstalujete více než jeden bod správy, klienti se automaticky připojí k jednomu bodu na základě jejich členství v doménové struktuře a umístění v síti. V sekundární lokalitě nemůžete nainstalovat více než jeden bod správy.  

Klienti počítačů Mac a klienti mobilních zařízení, které zaregistrujete v Configuration Manager vždy vyžadují bod správy pro instalaci klienta. Tento bod správy musí být v primární lokalitě, musí být nakonfigurován na podporu mobilních zařízení a musí přijmout připojení klienta z Internetu. Tito klienti nemůžou používat body správy v sekundárních lokalitách ani se nemohou připojit k bodům správy v jiných primárních lokalitách.  

## <a name="distribution-point"></a>Distribuční bod

K instalaci Configuration Manager klientů do počítačů se systémem Windows není nutný žádný distribuční bod. Ve výchozím nastavení používá Configuration Manager k instalaci zdrojových souborů klienta do počítačů se systémem Windows distribuční bod. Může se vrátit ke stažení těchto souborů z bodu správy. Distribuční body se nepoužívají k instalaci klientů mobilních zařízení, které jsou zapsány pomocí Configuration Manager, ale jsou používány při instalaci starší verze klienta pro mobilní zařízení. Nainstalujete-li klienta Configuration Manager jako součást nasazení operačního systému, bitová kopie operačního systému bude uložena a načtena z distribučního bodu.

I když možná nepotřebujete distribuční body pro instalaci většiny Configuration Managerch klientů, budete je potřebovat k instalaci softwaru, jako jsou aplikace a aktualizace softwaru na klienty.  

## <a name="fallback-status-point"></a>Bod záložního stavu

Bod záložního stavu můžete použít k monitorování nasazení klientů pro počítače se systémem Windows. Můžete také identifikovat klienty počítačů se systémem Windows, které nejsou spravované, protože nemohou komunikovat s bodem správy.

Následující typy klientů nepoužívají bod stavu pro použití náhradní lokality:

- Počítače Mac
- Mobilní zařízení zaregistrovaná službou Configuration Manager
- Mobilní zařízení spravovaná pomocí konektoru systému Exchange Server

Bod záložního stavu není nutný k monitorování činnosti klienta a stavu klienta.  

Bod záložního stavu vždy komunikuje s klienty přes protokol HTTP, který používá neověřená připojení a odesílá data ve formě prostého textu. Toto chování způsobí, že záložní stavový bod je zranitelný vůči útokům, zejména v případě, že se používá pro internetovou správu klientů. Chcete-li snížit plochu pro útok, vždy vyhradí Server pro spuštění záložního stavového bodu. Na stejný server v produkčním prostředí neinstalujte jiné role systému lokality.  

Nainstalujte záložní stavový bod, pokud platí všechny následující podmínky:  

- Chcete, aby byly chyby komunikace klienta z počítačů s Windows odesílány do lokality, i když tyto klientské počítače nemohou komunikovat s bodem správy.  

- Chcete použít sestavy nasazení klienta Configuration Manager, které zobrazují data odesílaná bodem záložního stavu.  

- Máte vyhrazený server pro tuto roli systému lokality a máte další bezpečnostní opatření, která vám pomůžou chránit server před útoky.  

- Výhody použití náhradního stavového bodu převažují všechna rizika zabezpečení spojená s neověřenými připojeními a Nešifrovaný přenos textu přes HTTP provoz.  

Neinstalujte záložní stavový bod, pokud se bezpečnostní rizika při spouštění webu s neověřenými připojeními a při čistém přenosu textu převažují nad výhodami identifikace problémů s komunikací klientů.  

## <a name="reporting-services-point"></a>Bod služby Reporting services

Configuration Manager poskytuje mnoho sestav, které vám pomůžou monitorovat instalaci, přiřazení a správu klientů v konzole Configuration Manager. Některé sestavy nasazení klientů vyžadují, aby klienti byli přiřazeni k bodu stavu pro použití náhradní lokality.  

Sestavy nejsou nutné k nasazení klientů. Některé informace o nasazení si můžete prohlédnout v konzole Configuration Manager nebo použít soubory protokolu klienta pro podrobné informace. Nicméně sestavy klienta poskytují cenné informace, které vám pomůžou monitorovat a řešit potíže s nasazením klientů.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Bod registrace a zprostředkující bod registrace

Configuration Manager vyžaduje bod registrace a zprostředkující bod registrace k registraci mobilních zařízení a k registraci certifikátů pro počítače se systémem Mac. Tyto role systému lokality nepotřebujete v následujících situacích:

- Máte v plánu spravovat mobilní zařízení pomocí konektoru systému Exchange Server
- Nainstalujete starší verzi klienta pro mobilní zařízení, například pro systém Windows CE
- Certifikát klienta si vyžádáte a nainstalujete na počítače Mac nezávisle na Configuration Manager

## <a name="application-catalog"></a>Katalog aplikací

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Bod konektoru brány pro správu cloudu

Pokud nastavujete [bránu pro správu cloudu](../../manage/cmg/plan-cloud-management-gateway.md) pro [správu klientů na internetu](../../manage/manage-clients-internet.md), budete potřebovat bod konektoru brány pro správu cloudu.
