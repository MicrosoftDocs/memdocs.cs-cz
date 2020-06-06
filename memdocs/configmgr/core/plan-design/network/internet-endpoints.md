---
title: Požadavky na přístup k internetu
titleSuffix: Configuration Manager
description: Přečtěte si o internetových koncových bodech, které umožní plnou funkčnost funkcí Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8423af8d4c743965f627a94a07f587fd97d45bdf
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454966"
---
# <a name="internet-access-requirements"></a>Požadavky na přístup k internetu

Některé funkce Configuration Manager spoléhají na možnosti připojení k Internetu, které mají plnou funkčnost. Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, nezapomeňte tyto koncové body povolit.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Bod připojení služby

Tyto konfigurace platí pro počítač, který je hostitelem spojovacího bodu služby a všech bran firewall mezi tímto počítačem a internetem. Oba musí umožňovat komunikaci prostřednictvím odchozího portu **tcp 443** pro https a odchozího portu **TCP 80** pro http do následujících internetových umístění.

Spojovací bod služby podporuje použití těchto umístění pomocí webového proxy serveru (s ověřováním nebo bez něj). Další informace najdete v tématu [Podpora proxy serveru](proxy-server-support.md).

Další informace o spojovacím bodu služby najdete v tématu [o spojovacím bodu služby](../../servers/deploy/configure/about-the-service-connection-point.md).

Další funkce Configuration Manager mohou vyžadovat další koncové body ze spojovacího bodu služby. Další informace najdete v dalších částech tohoto článku.

> [!TIP]  
> Bod připojení služby používá službu Microsoft Intune při připojení ke službě `go.microsoft.com` nebo `manage.microsoft.com` . Došlo k známému problému, při kterém konektor Intune funguje, pokud není nainstalovaný kořenový certifikát Baltimore CyberTrust, vypršela jeho platnost nebo je v spojovacím bodě služby poškozený. Další informace najdete v tématu [KB 3187516: bod připojení služby nestahuje aktualizace](https://support.microsoft.com/help/3187516).  

Od verze 2002, pokud se lokalita Configuration Manager nepovede připojit k požadovaným koncovým bodům pro cloudovou službu, vyvolá kritickou stavovou zprávu ID 11488. Když se nemůže připojit ke službě, stav součásti SMS_SERVICE_CONNECTOR se změní na kritický. Zobrazit podrobný stav v uzlu [Stav součásti](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) konzoly Configuration Manager.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a>Aktualizace a údržba

Další informace o této funkci najdete v tématu [aktualizace a údržba pro Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Povolte tyto koncové body pro pravidlo [přehledu správy](../../servers/manage/management-insights.md) a **Připojte lokalitu k Microsoft cloudu pro Configuration Manager aktualizace**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Údržba Windows 10

Další informace o této funkci najdete v tématu [Správa systému Windows jako služby](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Služby Azure

Další informace o této funkci najdete v tématu [Konfigurace služeb Azure pro použití s Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com`  

## <a name="co-management"></a>Spoluspráva

Pokud zařízení s Windows 10 zaregistrujete Microsoft Intune pro spolusprávu, ujistěte se, že tato zařízení mají přístup k koncovým bodům požadovaným službou Intune. Další informace najdete v tématu [koncové body sítě pro Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store pro firmy

Pokud integrujete Configuration Manager s [Microsoft Store pro firmy](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), ujistěte se, že spojovací bod služby a cílová zařízení mají přístup ke cloudové službě. Další informace najdete v tématu [konfigurace proxy serveru Microsoft Store pro firmy](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Optimalizace doručení

Pokud používáte optimalizaci doručování, klienti musí komunikovat se svou cloudovou službou:`*.do.dsp.mp.microsoft.com`

Distribuční body, které podporují mezipaměť připojené Microsoftem, vyžadují také tyto koncové body.

Další informace najdete v následujících článcích:

- [Nejčastější dotazy k optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Základní koncepty správy obsahu v nástroji Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Mezipaměť propojená Microsoftem v Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Cloudové služby

<!-- SCCMDocs-pr #3402 -->

Tato část obsahuje následující funkce:

- Brána pro správu cloudu (CMG)
- Distribuční bod cloudu (CDP)
- Integrace Azure Active Directory (Azure AD)
- Zjišťování založené na službě Azure AD

Pro nasazení služby CMG/CDP potřebuje **spojovací bod služby** přístup k těmto akcím:

- Konkrétní koncové body Azure se v závislosti na konfiguraci liší v jednotlivých prostředích. Configuration Manager ukládá tyto koncové body do databáze lokality. Dotaz na tabulku **AzureEnvironments** v SQL Server pro seznam koncových bodů Azure.  

**Bod připojení CMG** potřebuje přístup k následujícím koncovým bodům služby:

- Koncový bod služby Service Management:`https://management.core.windows.net/`  

- Koncový bod úložiště: `<name>.blob.core.windows.net` a`<name>.table.core.windows.net`

    Kde `<name>` je název cloudové služby vašeho CMG nebo CDP. Například pokud je vaše CMG `GraniteFalls.CloudApp.Net` , pak první koncový bod úložiště, který se má použít, je `GraniteFalls.blob.core.windows.net` .<!-- SCCMDocs#2288 -->

Pro získání tokenu Azure AD pomocí **konzoly Configuration Manager** a **klienta**:

- ActiveDirectoryEndpoint`https://login.microsoftonline.com/`  

Pro zjišťování uživatelů Azure AD potřebuje **spojovací bod služby** přístup k:

- Verze 1810 a starší: koncový bod Azure AD graphu`https://graph.windows.net/`  

- Verze 1902 a novější: Microsoft Graph koncový bod`https://graph.microsoft.com/`

Systém lokality bodu správy v cloudu (CMG) podporuje používání webového proxy serveru. Další informace o konfiguraci této role proxy serveru najdete v tématu [Podpora proxy serveru](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Bod připojení CMG se musí připojit pouze k koncovým bodům služby CMG. Nepotřebuje přístup k jiným koncovým bodům Azure.

Další informace o CMG najdete v tématu [Plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

## <a name="software-updates"></a><a name="bkmk_sum"></a>Aktualizace softwaru

Povolí aktivnímu bodu aktualizace softwaru přístup k následujícím koncovým bodům, aby služba WSUS a automatické aktualizace mohly komunikovat s Microsoft Update cloudovou službou:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Další informace o aktualizacích softwaru najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Intranetová brána firewall

Je možné, že budete muset přidat koncové body do brány firewall, která je mezi dvěma systémy lokality, v následujících případech:

- Pokud mají podřízené lokality bod aktualizace softwaru
- Pokud je v lokalitě vzdálený aktivní internetový bod aktualizace softwaru

#### <a name="software-update-point-on-the-child-site"></a>Bod aktualizace softwaru v podřízené lokalitě

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Správa Office 365

> [!NOTE]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

Pokud používáte Configuration Manager k nasazení a aktualizaci Microsoft 365 aplikací pro podniky, povolte následující koncové body:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`synchronizace bodu aktualizace softwaru pro aplikace Microsoft 365 pro aktualizace podnikových klientů

- `config.office.com`Vytvoření vlastních konfigurací pro aplikace Microsoft 365 pro podniková nasazení

## <a name="configuration-manager-console"></a>Konzola nástroje Configuration Manager

Počítače s konzolou Configuration Manager vyžadují přístup k následujícím koncovým bodům Internetu pro konkrétní funkce:

### <a name="in-console-feedback"></a>Zpětná vazba v konzole

- `http://petrol.office.microsoft.com`

Další informace o této funkci najdete v tématu o [zpětné vazbě produktu](../../understand/find-help.md#product-feedback).

### <a name="community-workspace-documentation-node"></a>Pracovní prostor komunity, uzel dokumentace

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Další informace o tomto uzlu konzoly najdete v tématu [použití konzoly Configuration Manager](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Pracovní prostor monitorování, uzel hierarchie lokality

Pokud používáte **zeměpisné zobrazení**, povolte přístup k následujícímu koncovému bodu:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Další informace o požadovaných koncových bodech pro cloudovou službu Desktop Analytics najdete v tématu [Povolení sdílení dat](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Veřejné IP adresy Microsoftu

Další informace o rozsahu IP adres společnosti Microsoft najdete v tématu věnovaném [veřejné IP adrese Microsoftu](https://www.microsoft.com/download/details.aspx?id=53602). Tyto adresy se pravidelně aktualizují. Služba nenabízí žádnou členitost, proto by mohla být použita jakákoli IP adresa v těchto rozsahech.

## <a name="see-also"></a>Viz také

- [Porty používané v Configuration Manager](../hierarchy/ports.md)

- [Podpora proxy serveru v Configuration Manager](proxy-server-support.md)
