---
title: Připojení k datovému skladu pomocí Power BI
titleSuffix: Microsoft Intune
description: Můžete si stáhnout soubor pro použití s Microsoft Power BI, který vám umožní načíst interaktivní, dynamicky generované sestavy vašeho tenanta Microsoft Intune.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5E5A35D3-88F8-441B-8A0B-C5D7A1E5137B
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e61e7e8bae436e567bceec5f098170cfb7b7c6a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907748"
---
# <a name="connect-to-the-data-warehouse-with-power-bi"></a>Připojení k datovému skladu pomocí Power BI

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Aplikaci Power BI dodržování předpisů můžete použít k načtení interaktivních a dynamicky generovaných sestav pro vašeho tenanta Intune. Kromě toho můžete načíst data tenanta v Power BI pomocí odkazu OData. Intune poskytuje vašemu tenantovi nastavení připojení, abyste mohli zobrazit následující ukázkové sestavy a grafy týkající se:  

- Zařízení
- Registrace
- zásady ochrany aplikací
- zásady dodržování předpisů
- Konfigurační profily zařízení
- Aktualizace softwaru
- Protokoly inventáře zařízení

Jsou tu také zvýrazněné trendy pro registraci, dodržování předpisů, konfigurační profil zařízení a aktualizace softwaru. Ukázkové grafy a sestavy používají uživatelsky přívětivé filtry plátna. Pokud chcete použít rozšířené filtry, podívejte se na podokno **Filtr** v aplikaci Power BI Desktop.

> [!NOTE]
> Power BI šablonových aplikací umožňují Power BI partnerům vytvářet Power BI aplikace s malým nebo žádným kódováním a nasazovat je na jakéhokoli Power BIho zákazníka. Můžete například použít šablonu sestavy dodržování předpisů Power BI v 2.0. Verze 2.0 zahrnuje vylepšený návrh a také změny výpočtů a dat, která jsou v rámci šablony Surface. Další informace najdete v tématu [aktualizace aplikace šablony](/power-bi/service-template-apps-install-distribute#update-a-template-app), [aplikace pro dodržování předpisů v Intune (datový sklad)](https://appsource.microsoft.com/product/power-bi/pbi_intune.intune_compliance_dw_app-preview?flightCodes=65ede247-5273-43b8-8a25-b89c7d211fbd)a [co jsou Power BIch aplikací šablon](/power-bi/service-template-apps-overview) .

Následující kroky vám ukážou, jak stáhnout soubor Power BI a jak používat odkaz OData s Power BI.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## <a name="install-power-bi"></a>Instalace Power BI

Nainstalujte nejnovější verzi [Power BI Desktop](https://aka.ms/intune/datawarehouseapi/installpowerbi). Další informace najdete v tématu [Power BI Desktop](https://powerbi.microsoft.com/desktop).

## <a name="load-the-data-and-reports-using-the-power-bi-intune-compliance-data-warehouse-app"></a>Načtěte data a sestavy pomocí Power BI aplikace datového skladu dodržování předpisů Intune.

Aplikace Power BI [Intune pro dodržování předpisů (datový sklad)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) obsahuje informace pro vašeho tenanta a sadu předem připravených sestav založených na datovém modelu datového skladu.

> [!NOTE]
> Aplikace datového skladu dodržování předpisů v Intune Power BI není pro cloudová prostředí Azure Government podporovaná.

1. Přejděte na stránku **AppSource** aplikace pro [dodržování předpisů v Intune (datový sklad)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) , abyste zahájili proces instalace.
2. Klikněte na tlačítko **získat nyní** a potom klikněte na tlačítko **pokračovat**.
3. Po zobrazení výzvy k instalaci aplikace Power BI klikněte na **nainstalovat**.
4. Po dokončení instalace klikněte na dlaždici aplikace **Intune pro dodržování předpisů (datový sklad)** .
5. Klikněte na tlačítko **připojit** . Zobrazí se dialogové okno **připojit k Intune dodržování předpisů (datový sklad)** .
6. Klikněte na tlačítko **Přihlásit** se.
7. Přihlaste se pomocí uživatelského účtu, který má přístup k datovému skladu Intune pro tenanta se sestavami, které chcete zobrazit.
8. Pokud chcete zobrazit zahrnutý řídicí panel, klikněte na kartu **řídicí panely** a potom klikněte na řídicí panel **Přehled dodržování předpisů** .
9. Chcete-li zobrazit všechny dostupné sestavy, klikněte na kartu **sestavy** a potom klikněte na sestavu **dodržování předpisů v 1.0** . Procházejte stránkami sestavy kliknutím na karty v dolní části.
10. Chcete-li se později snadno vrátit k těmto sestavám, klikněte na hvězdičku vedle sestavy **dodržování předpisů v 1.0** . Tím se sestava přidá do oblíbených Power BI.

Alternativně můžete aplikaci nainstalovat z centra pro správu Microsoft Endpoint Manageru:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy**  >  datový sklad**datového skladu Intune**  >  **Data warehouse**.
3. Vyberte **získat Power BI aplikaci** pro přístup k předem vytvořeným Power BIm sestavám pro vašeho tenanta v prohlížeči a jejich sdílení.
4. Postupujte podle kroků 2-10 výše.

## <a name="load-the-data-in-power-bi-using-the-odata-link"></a>Načtení dat v Power BI pomocí odkazu OData

S klientem ověřeným v Azure AD se adresa URL pro OData připojí ke koncovému bodu RESTful v rozhraní API datového skladu, který zveřejní datový model do klienta sestav. Pokud chcete použít aplikaci Power BI Desktop pro připojení a vytvoření vlastních sestav, postupujte podle těchto pokynů. Nejste omezeni aplikací Power BI Desktop. Můžete použít oblíbený analytický nástroj s adresou URL pro OData, za předpokladu, že klient podporuje ověřování OAUTH2.0 a standard OData v4.0.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **sestavy**  >  datový sklad**datového skladu Intune**  >  **Data warehouse**.
3. V okně vytváření sestav načtěte adresu URL vlastního kanálu, například:<br>
    `https://fef.{yourtenant}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Otevřete **Power BI Desktop**.
5. Vyberte **soubor**  >  **získat data**. Vyberte **Datový kanál OData**.
6. Zvolte **Základní**.
7. Do pole adresy URL zadejte nebo vložte **adresu URL pro OData**.
8. Vyberte **OK**.
9. Pokud jste se službě Azure AD pro vašeho tenanta neověřili z klienta aplikace Power BI Desktop, zadejte své přihlašovací údaje. Abyste získali přístup k datům, musíte se vůči službě Azure Active Directory (Azure AD) autorizovat protokolem OAuth 2.0.  
    1. Vyberte **Účet organizace**.  
    2. Zadejte své uživatelské jméno a heslo.  
    3. Vyberte **Přihlásit se.**  
    4. Vyberte **Připojit**.  
10. Vyberte **Načíst**.

## <a name="next-steps"></a>Další kroky

Můžete získat odpovědi na otázky týkající se vašeho prostředí, například týkající se počtu zařízení zaregistrovaných podle dne za poslední týden. Můžete získat přehled o naplnění tenanta a klientů Intune pomocí datových skladů Intune Power BI sestav načtených z okna v centru pro správu Microsoft Endpoint Management. Intune ale poskytuje množství dalších způsobů, jak data rozšířit a znovu použít. Power BI a rozhraní API datového skladu Intune poskytují další funkce, například:

<!-- - You can use Power BI Desktop to create additional report types with your data. For example, you could create a custom chart representing the ratio of device manufactures in your enterprise. For more information about creating custom reports with Power BI and the Intune Data Warehouse, see `BLOG POST ON POWER BI`. -->
- Data tenanta budou uspořádána tak, aby vám pomohla získat lepší přehled. Další informace o způsobu uspořádání dat najdete v tématu [Datový model datového skladu](reports-ref-data-model.md).
- K datům můžete získat přístup také z rozhraní RESTful a začlenit je do své vlastní aplikace. Další informace najdete v článku [Získání dat z rozhraní API datového skladu pomocí klienta REST](reports-proc-data-rest.md).