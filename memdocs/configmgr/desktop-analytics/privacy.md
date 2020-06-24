---
title: Ochrana osobních údajů v datech Desktop Analytics
titleSuffix: Configuration Manager
description: Desktop Analytics se zaznamená do ochrany osobních údajů zákaznických dat
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 34005a63b372198bbc2e3079f8ab560ef6b2b791
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795631"
---
# <a name="desktop-analytics-data-privacy"></a>Ochrana osobních údajů v datech Desktop Analytics

Plocha Analytics je plně potvrzená pro ochranu osobních údajů zákaznických dat, centrování na těchto principy:

- **Transparentnost:** Události diagnostiky systému Windows jsme kompletně zdokumentují. Projděte si je s týmy zabezpečení a dodržování předpisů vaší společnosti. Prohlížeč diagnostických dat systému Windows umožňuje zobrazit diagnostická data odesílaná z daného zařízení. Další informace najdete v tématu [Přehled prohlížeče diagnostických dat](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Ovládací prvek:** Můžete řídit úroveň diagnostických dat, která se mají sdílet se společností Microsoft. Windows 10 verze 1709 přidává novou zásadu pro omezení rozšířených diagnostických dat na minimum vyžadovaného Desktop Analytics.  

- **Zabezpečení:** Společnost Microsoft chrání vaše data pomocí silného zabezpečení a šifrování.  

- **Vztah důvěryhodnosti:** Desktop Analytics podporuje [prohlášení o zásadách ochrany osobních údajů](https://privacy.microsoft.com/privacystatement) společnosti Microsoft a [online smlouvy o poskytování služeb](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

Další informace najdete v tématu [služby systému Windows, kde Microsoft je procesor v rámci GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Tok dat

Následující obrázek ukazuje, jak diagnostická data přecházejí z jednotlivých zařízení prostřednictvím služby diagnostiky dat, přechodného úložiště a do vašeho pracovního prostoru Log Analytics:

![Diagram znázorňující tok diagnostických dat ze zařízení](media/da-data-flow.png)

1. Přihlašujete se k Azure Portal a připojíte se k Desktop Analytics. Vytvoříte aplikaci Azure AD pro připojení k Configuration Manager. Když nastavíte desktopovou analýzu, vytvoříte pracovní prostor Azure Log Analytics v umístění dle vašeho výběru.  

2. Připojíte Configuration Manager a zaregistrujete zařízení.  

    1. Cloudovou službu Desktop Analytics můžete nakonfigurovat v Configuration Manager s podrobnostmi o aplikaci Azure AD.  

    2. Během 15 minut Configuration Manager synchronizuje následující data s desktopovou analýzou pomocí vašeho ID tenanta. Tento proces se opakuje každou hodinu.

      - Informace o kolekcích zařízení nezbytných pro [vytváření plánů nasazení](create-deployment-plans.md). Tyto informace zahrnují ID kolekce, ID hierarchie, název kolekce a počet zařízení. 
      - Informace vyžadované k [registraci zařízení](enroll-devices.md) Tyto informace zahrnují ID kolekce, jedinečný identifikátor SMS, verzi buildu operačního systému, název zařízení a sériové číslo.
      - Informace z řídicího panelu pro [monitorování stavu připojení](monitor-connection-health.md) Tyto informace zahrnují počet zařízení podle stavu a vlastnosti zařízení.
      - Informace o plánech nasazení, které zahrnují ID kolekce, ID nasazení, pilotní nebo produkční typ nasazení a počet zařízení na rozhodnutí o upgradu.

    3. Configuration Manager nastaví komerční ID, úroveň diagnostických dat a další nastavení pro zařízení v cílové kolekci. Tato konfigurace určuje zařízení, která se mají zobrazit v pracovním prostoru Analytics pro stolní počítače.  

    4. Nasadíte aktualizace kompatibility na všechna cílová zařízení.  

3. Zařízení odesílají diagnostická data službě Microsoft Diagnostic Správa dat Service pro Windows. Všechna diagnostická data jsou šifrována přes protokol HTTPS a při přenosu ze zařízení do této služby používají připnutí certifikátů. Služba Microsoft Správa dat je hostována v USA.

      - Chyby aplikací, chyby jádra, nereagující aplikace a další problémy specifické pro aplikace používají rozhraní Zasílání zpráv o chybách systému Windows API k posílání sestav problémů specifických pro aplikace do Microsoftu. Konkrétní podrobnosti o tomto toku dat najdete v tématu [použití služby wer](https://docs.microsoft.com/windows/win32/wer/using-wer) .
      
4. Každý den Microsoft vytvoří snímek přehledů zaměřených na IT. Tento snímek kombinuje diagnostická data z Windows se vstupem pro zaregistrovaná zařízení. K tomuto procesu dochází v přechodném úložišti, které se používá jenom pro Desktop Analytics. Přechodné úložiště je hostované v datových centrech Microsoftu v USA. Všechna data se odesílají přes zašifrovaný kanál SSL (HTTPS). Snímky jsou oddělené pomocí komerčního ID.  

5. Snímky se pak zkopírují do vašeho pracovního prostoru Azure Log Analytics. K přenosu dat dojde přes protokol HTTPS prostřednictvím protokolu ingestování Webhooku, což je funkce Log Analytics. Desktop Analytics nemá žádná oprávnění ke čtení nebo zápisu do úložiště Log Analytics. Desktop Analytics volá rozhraní API Webhooku s identifikátorem URI sdíleného přístupového podpisu (SAS). Pak Log Analytics získá data z tabulek úložiště přes protokol HTTPS.

6. Desktop Analytics ukládá vaše vstupy do Log Analyticsho úložiště. Mezi tyto konfigurace patří plány nasazení a rozhodnutí o prostředcích pro upgrade a důležitost.  

## <a name="other-resources"></a>Další prostředky

Nejčastější dotazy týkající se ochrany osobních údajů pro Desktop Analytics najdete v tématu [Nejčastější dotazy](faq.md#privacy)týkající se ochrany osobních údajů.

Další informace o souvisejících aspektech ochrany osobních údajů najdete v následujících článcích:

- [Windows 10 a GDPR pro tvůrce rozhodnutí IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8 a Windows 8.1 události a pole diagnostiky dat posouzení](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, verze 1809 úrovně Basic diagnostické události a pole Windows](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, verze 1709 rozšířené události diagnostických dat a pole používaná analýzou pro stolní počítače](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [instalační program systému Windows zasílání zpráv o chybách](https://docs.microsoft.com/windows/deployment/upgrade/windows-error-reporting)

- [Přehled prohlížeče diagnostických dat](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Licenční podmínky a dokumentace](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Zabezpečení dat Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Zabezpečení a ochrana osobních údajů v Microsoft Azure datových Centre](https://azure.microsoft.com/global-infrastructure/)  

- [Jistota v důvěryhodném cloudu](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centrum zabezpečení](https://www.microsoft.com/trustcenter)  

- [Privacy Shield](https://www.privacyshield.gov/)  

Z Desktop Analytics Configuration Manager odesílá data o využití a diagnostiku do Microsoftu. Společnost Microsoft používá tato data ke zlepšení prostředí pro instalaci, kvality a zabezpečení budoucích verzí Configuration Manager. Další informace najdete v tématu [Diagnostika a data o využití pro Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
