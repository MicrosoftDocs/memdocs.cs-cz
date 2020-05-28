---
title: funkce Asset Intelligence předpoklady
titleSuffix: Configuration Manager
description: Získejte předpoklady pro funkce Asset Intelligence v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7f87336c35c236a9e07d531469d65958d5d14e0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906586"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Předpoklady pro funkce Asset Intelligence v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Funkce Asset Intelligence v Configuration Manager má vnější závislosti a závislosti v rámci produktu.  

## <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager  
 Následující tabulka uvádí závislosti pro funkce Asset Intelligence, které jsou pro Configuration Manager externí.  

|Závislost|Další informace|  
|----------------|----------------------|  
|Požadavky na auditování událostí úspěšného přihlášení|Čtyři sestavy Asset Intelligence zobrazují informace získané z protokolů událostí Zabezpečení systému Windows v klientských počítačích. Když nastavení protokolu událostí zabezpečení není nakonfigurované tak, aby se protokolovaly všechny události úspěšného přihlášení, tyto sestavy neobsahují žádná data, a to ani v případě, že příslušná třída generování sestav inventáře hardwaru je povolená.<br /><br /> Na informacích  shromážděných v protokolu událostí zabezpečení systému Windows jsou závislé následující sestavy funkce Asset Intelligence:<br /><br /> -Hardware 03A – primární uživatelé počítačů<br />-03B hardwaru – počítače pro určitého primárního uživatele konzoly<br />-Hardware 04A – sdílené počítače (více uživatelů)<br />-Hardware 05A – uživatelé konzoly v určitém počítači<br /><br /> Pokud chcete Klientskému agentu pro inventáře hardwaru povolit inventarizaci informací potřebných k podpoře těchto sestav, musíte nejdřív na klientech změnit nastavení protokolu událostí zabezpečení systému Windows Security, aby se protokolovaly všechny události úspěšného přihlášení, a povolit třídu generování sestav inventáře hardwaru **SMS_SystemConsoleUser** . Další informace o změnách nastavení protokolu událostí zabezpečení, aby se protokolovaly všechny události úspěšného přihlášení, najdete v části [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  Třída vytváření sestav inventáře hardwaru **SMS_SystemConsoleUser** uchovává data událostí úspěšného přihlášení v protokolu událostí zabezpečení jenom za předchozích 90 dnů bez ohledu na délku protokolu. Když protokol událostí obsahuje méně než 90 dnů dat, čte se celý protokol.  

## <a name="dependencies-internal-to-configuration-manager"></a>Vnitřní závislosti nástroje Configuration Manager  
 Následující tabulka uvádí závislosti pro funkce Asset Intelligence, které jsou interní pro Configuration Manager.  

|Závislost|Další informace|  
|----------------|----------------------|  
|Požadavky agenta klienta|Sestavy Asset Intelligence závisí na informacích z klienta získaných ze sestav klientských agentů inventáře hardwaru a softwaru. Pokud chcete získat informace potřebné pro všechny sestavy funkce Asset Intelligence, musí se povolit následující agenti klientů:<br /><br /> – Klientský Agent pro inventáře hardwaru<br />– Klientský Agent softwarového měření|  
|Závislosti pro klientský agent pro inventáře hardwaru|Aby se daly shromažďovat inventarizační údaje požadované pro některé sestavy Asset Intelligence, musí být povolený Klientský agent pro inventáře hardwaru. Kromě toho musí být na serverových počítačích primární lokality povolené některé třídy inventáře hardwaru, na kterých sestavy funkce Asset Intelligence závisí.<br /><br /> Informace o povolení klientského agenta inventáře hardwaru najdete v tématu [postup rozšiřování inventáře hardwaru](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Závislosti pro klientský agent softwarového měření|Na datech klientského agentu měření softwaru závisí celá řada sestav o softwaru funkce Asset Intelligence. Informace o povolení klientského agenta softwarového měření najdete v tématu [monitorování využití aplikací pomocí monitorování míry využívání softwaru](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Na datech klientského agentu měření softwaru závisí následující sestavy funkce Asset Intelligence.<br /><br /> -Software 07A – nedávno použité spustitelné soubory podle počtu počítačů<br />-Software 07B – počítače, které nedávno používaly zadaný spustitelný soubor<br />-Software 07C – nedávno použité spustitelné soubory na určitém počítači<br />-Software 08A – nedávno použité spustitelné soubory podle počtu uživatelů<br />-Software 08B – uživatelé, kteří naposledy použili zadaný spustitelný soubor<br />-Software 08C – nedávno použité spustitelné soubory zadaným uživatelem|  
|Požadavky na třídy generování sestav inventáře hardwaru funkce Asset Intelligence|Sestavy funkce Asset Intelligence v Configuration Manager závisí na konkrétních třídách generování sestav inventáře hardwaru. Dokud nebudou povolené třídy generování sestav inventáře hardwaru a dokud klienty nenahlásí inventář hardwaru založený na těchto třídách, příslušné sestavy funkce Asset Intelligence nebudou obsahovat žádná data. Pro podporu vytváření sestav funkce Asset Intelligence můžete povolit následující třídy generování sestav inventáře hardwaru:<br /><br /> -SMS_SystemConsoleUsage<sup>1</sup><br />-SMS_SystemConsoleUser<sup>1</sup><br />-SMS_InstalledSoftware<br />-SMS_AutoStartSoftware<br />-SMS_BrowserHelperObject<br />-Win32_USBDevice<br />-SMS_InstalledExecutable<br />-SMS_SoftwareShortcut<br />– SoftwareLicensingService<br />– SoftwareLicensingProduct<br />-SMS_SoftwareTag<br /><br /> <sup>1</sup> ve výchozím nastavení jsou povolené třídy **SMS_SystemConsoleUsage** a **SMS_SystemConsoleUser** .<br /><br /> Třídy generování sestav inventáře hardwaru funkce Asset Intelligence můžete upravit v konzole Configuration Manager v pracovním prostoru **prostředky a kompatibilita** , když kliknete na uzel **funkce Asset Intelligence** . Další informace najdete v části [povolení funkce Asset Intelligence třídy generování sestav inventáře hardwaru](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) v tématu [Konfigurace funkce Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) .|  
|Bod služby Reporting services|Než bude možné zobrazit sestavy o aktualizaci softwaru, musí být nainstalovaná role systému lokality bodu služby Reporting Services. Další informace o vytvoření bodu služby Reporting Services najdete v tématu [Konfigurace generování sestav](../../../servers/manage/configuring-reporting.md).|  
