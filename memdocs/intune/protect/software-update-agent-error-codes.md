---
title: Chyby a popisy aktualizace softwaru v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam kódu chyby agenta aktualizace softwaru v Microsoft Intune, včetně kódu chyby, symbolického názvu a popisu chyby.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ROBOTS: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e762106a13bb42be11771276f38a37e46ae24662
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325267"
---
# <a name="software-update-agent-error-codes-and-descriptions-in-microsoft-intune"></a>Kódy a popisy chyb agenta aktualizace softwaru v Microsoft Intune

Kódy chyb agenta Intune **Update Agent** jsou uvedené v následující tabulce. Pokud v této tabulce nemůžete najít konkrétní kód chyby, přečtěte si téma [web Windows Update seznam kódů chyb](https://support.microsoft.com/help/938205/windows-update-error-code-list).

|Kód chyby|Symbolický název|Další informace|
|--------------|-----------------|--------------------|
|**0x00cf0001**|OM_S_SERVICE_STOP|Agenta se povedlo zastavit.|
|**0x00cf0003**|OM_S_UPDATE_ERROR|Opraci se povedlo dokončit, ale nastaly chyby během použití aktualizací.|
|**0x00cf0004**|OM_S_MARKED_FOR_DISCONNECT|Zpětné volání bylo označeno pro pozdější odpojení, protože žádost o odpojení operace přišla v průběhu provádění zpětného volání.|
|**0x00cf0005**|OM_S_REBOOT_REQUIRED|Aby bylo možné instalaci aktualizace dokončit, musí se restartovat systém.|
|**0x00cf0006**|OM_S_ALREADY_INSTALLED|Aktualizace, která se má nainstalovat, je v systému už nainstalovaná.|
|**0x00cf0007**|OM_S_ALREADY_UNINSTALLED|Aktualizace, která se má odebrat, není v systému nainstalovaná.|
|**0x00cf2015**|OM_S_UH_INSTALLSTILLPENDING|Instalace aktualizace zrovna probíhá.|
|**0x80cf0001**|OM_E_NO_SERVICE|Agentovi se nepovedlo službu zajistit.|
|**0x80cf0002**|OM_E_MAX_CAPACITY_REACHED|Překročila se maximální kapacita služby.|
|**0x80cf0003**|OM_E_UNKNOWN_ID|ID nejde najít.|
|**0x80cf0004**|OM_E_NOT_INITIALIZED|Objekt nešlo inicializovat.|
|**0x80cf0007**|OM_E_INVALIDINDEX|Index pro kolekci není platný.|
|**0x80cf0008**|OM_E_ITEMNOTFOUND|Nenašel se klíč pro položku, která je předmětem dotazu.|
|**0x80cf0009**|OM_E_OPERATIONINPROGRESS|Probíhala nějaká konfliktní operace. Některé operace, třeba vícenásobné instalace, nejde dělat současně.|
|**0x80cf000B**|OM_E_CALL_CANCELLED|Operace byla zrušena.|
|**0x80cf000C**|OM_E_NOOP|Nebyla nutná žádná operace.|
|**0x80cf000D**|OM_E_XML_MISSINGDATA|Agent nemohl najít v datech XML aktualizace požadované informace.|
|**0x80cf000E**|OM_E_XML_INVALID|Agent našel v datech XML aktualizace informace, které nejsou platné.|
|**0x80cf000F**|OM_E_CYCLE_DETECTED|V metadatech se zjistily cyklické vztahy aktualizace.|
|**0x80cf0010**|OM_E_TOO_DEEP_RELATION|Vztahy aktualizace byly na vyhodnocení moc vnořené.|
|**0x80cf0011**|OM_E_INVALID_RELATIONSHIP|Našel se vztah aktualizace, který není platný.|
|**0x80cf0012**|OM_E_REG_VALUE_INVALID|Přečtená hodnota registru není platná.|
|**0x80cf0013**|OM_E_DUPLICATE_ITEM|Operace se snažila přidat do seznamu duplicitní položku.|
|**0x80cf0014**|OM_E_INVALID_INSTALL_REQUESTED|Volající funkce nemůže nainstalovat aktualizace, které se pro instalaci požadovaly.|
|**0x80cf0016**|OM_E_INSTALL_NOT_ALLOWED|Operace se pokusila o instalaci, když probíhala jiná instalace nebo když systém čekal na povinné restartování.|
|**0x80cf0017**|OM_E_NOT_APPLICABLE|Operace neproběhla, protože nejsou dostupné žádné použitelné aktualizace.|
|**0x80cf0018**|OM_E_NO_USERTOKEN|Operace se nepovedla, protože chybí požadovaný token uživatele.|
|**0x80cf0019**|OM_E_EXCLUSIVE_INSTALL_CONFLICT|Výhradní aktualizaci nejde instalovat současně s jinými aktualizacemi.|
|**0x80cf001A**|OM_E_POLICY_NOT_SET|Nebyla nastavena hodnota zásad.|
|**0x80cf001D**|OM_E_INVALID_UPDATE|Aktualizace obsahuje metadata, která nejsou platná.|
|**0x80cf001E**|OM_E_SERVICE_STOP|Operaci nešlo dokončit, protože probíhalo vypínání služby nebo systému.|
|**0x80cf001F**|OM_E_NO_CONNECTION|Operaci nešlo dokončit, protože nebylo dostupné síťové připojení.|
|**0x80cf0020**|OM_E_NO_INTERACTIVE_USER|Operaci nešlo dokončit, protože není přihlášený žádný interaktivní uživatel.|
|**0x80cf0021**|OM_E_TIME_OUT|Operaci nešlo dokončit, protože vypršel její časový limit.|
|**0x80cf0022**|OM_E_ALL_UPDATES_FAILED|Operace se pro žádnou aktualizaci nepovedla.|
|**0x80cf0024**|OM_E_NO_UPDATE|Nejsou dostupné žádné aktualizace.|
|**0x80cf0025**|OM_E_USER_ACCESS_DISABLED|Nastavení zásad skupiny zabránilo přístupu ke službě Windows Update.|
|**0x80cf0026**|OM_E_INVALID_UPDATE_TYPE|Daný typ aktualizace není platný.|
|**0x80cf0028**|OM_E_UNINSTALL_NOT_ALLOWED|Aktualizaci nešlo odinstalovat, protože žádost nepřišla ze serveru WSUS.|
|**0x80cf0029**|OM_E_INVALID_PRODUCT_LICENSE|Při hledání se asi některé aktualizace nenašly, nebo je možné, že je v systému nějaká nelicencovaná aplikace.|
|**0x80cf002C**|OM_E_BIN_SOURCE_ABSENT|Aktualizaci s rozdílovou kompresí nešlo nainstalovat, protože vyžadovala zdrojové soubory.|
|**0x80cf002D**|OM_E_SOURCE_ABSENT|Aktualizaci s kompletními soubory nešlo nainstalovat, protože vyžadovala zdrojové soubory.|
|**0x80cf002E**|OM_E_WU_DISABLED|Přístup k nespravovanému serveru není povolený.|
|**0x80cf002F**|OM_E_CALL_CANCELLED_BY_POLICY|Operaci nešlo dokončit, protože byla nastavená zásada **DisableWindowsUpdateAccess**.|
|**0x80cf0030**|OM_E_INVALID_PROXY_SERVER|Formát seznamu proxy serverů není platný.|
|**0x80cf0031**|OM_E_INVALID_FILE|Soubor je ve špatném formátu.|
|**0x80cf0032**|OM_E_INVALID_CRITERIA|Řetězec kritérií hledání není platný.|
|**0x80cf0034**|OM_E_DOWNLOAD_FAILED|Aktualizaci se nepovedlo stáhnout.|
|**0x80cf0035**|OM_E_UPDATE_NOT_PROCESSED|Aktualizace nebyla zpracována.|
|**0x80cf0036**|OM_E_INVALID_OPERATION|Aktuální stav objektu takovou operaci neumožnil.|
|**0x80cf0037**|OM_E_NOT_SUPPORTED|Operace není podporovaná.|
|**0x80cf0038**|OM_E_WINHTTP_INVALID_FILE|Stažený soubor má neočekávaný typ obsahu.|
|**0x80cf0039**|OM_E_TOO_MANY_RESYNC|Počet, kolikrát server požádal agenta o novou synchronizaci, je moc velký.|
|**0x80cf0043**|OM_E_NO_UI_SUPPORT|Uživatelské rozhraní agenta WUA není podporované.|
|**0x80cf0044**|OM_E_PER_MACHINE_UPDATE_ACCESS_DENIED|Tuto operaci můžou u aktualizací pro jednotlivé počítače dělat jenom správci.|
|**0x80cf0045**|OM_E_UNSUPPORTED_SEARCHSCOPE|Zkoušelo se hledat s nepodporovaným oborem.|
|**0x80cf0046**|OM_E_BAD_FILE_URL|Adresa URL neukazuje na soubor.|
|**0x80cf0047**|OM_E_NOTSUPPORTED|Požadovaná operace není podporovaná.|
|**0x80cf0049**|OM_E_OUTOFRANGE|Data jsou mimo rozsah.|
|**0x80cf004A**|OM_E_INVALIDWUAVERSION|Data obsahují verzi, která není platná.|
|**0x80cf004B**|OM_E_SEARCH_COMPLETED_WITH_SOME_FAILURES|Volání hledání se dokončilo, ale některé aktualizace nešlo rozpoznat.|
|**0x80cf004C**|OM_E_DOWNLOAD_COMPLETED_WITH_SOME_FAILURES|Volání stažení se dokončilo, ale některé aktualizace nešlo stáhnout.|
|**0x80cf004D**|OM_E_INSTALL_COMPLETED_WITH_SOME_FAILURES|Volání instalace se dokončilo, ale některé aktualizace nešlo nainstalovat.|
|**0x80cf004E**|OM_E_WINUPDATE_CACHE_UNINITIALIZED|Mezipaměť služby Windows Update je prázdná, protože se neinicializovala.|
|**0x80cf0436**|OM_E_PT_CATALOG_SYNC_REQUIRED|Server nepodporuje hledání podle kategorií. Místo toho je potřeba provést kompletní hledání v katalogu.|
|**0x80cf0437**|OM_E_PT_SECURITY_VERIFICATION_FAILURE|Došlo k problému s autorizací u příslušné služby.|
|**0x80cf0438**|OM_E_PT_ENDPOINT_UNREACHABLE|Neexistuje žádná trasa ani síťové připojení ke koncovému bodu.|
|**0x80cf0439**|OM_E_PT_INVALID_FORMAT|Přijatá data nesplňují očekávání kontraktu dat.|
|**0x80cf043A**|OM_E_PT_INVALID_URL|Adresa URL není platná.|
|**0x80cf043B**|OM_E_PT_NWS_NOT_LOADED|Modul NWS runtime nejde načíst.|
|**0x80cf043C**|OM_E_PT_PROXY_AUTH_SCHEME_NOT_SUPPORTED|Schéma ověřování proxy serverem není podporované.|
|**0x80cf043D**|OM_E_SERVICEPROP_NOTAVAIL|Požadovaná vlastnost služby není dostupná.|
|**0x80cf043E**|OM_E_PT_ENDPOINT_REFRESH_REQUIRED|Modul plug-in zprostředkovatele koncových bodů vyžaduje on-line aktualizaci.|
|**0x80cf043F**|OM_E_PT_ENDPOINTURL_NOTAVAIL|Adresa URL pro požadovaný koncový bod služby není dostupná.|
|**0x80cf0440**|OM_E_PT_ENDPOINT_DISCONNECTED|Připojení ke koncovému bodu služby bylo ukončeno.|
|**0x80cf0441**|OM_E_PT_INVALID_OPERATION|Operace není platná, protože mluvčí protokolu je v nevhodném stavu.|
|**0x80cf0FFF**|OM_E_UNEXPECTED|Operace se nepovedla kvůli důvodům, které nevysvětluje jiný kód chyby.|
|**0x80cf1001**|OM_E_MSI_WRONG_VERSION|Při hledání se asi nenašly některé aktualizace, protože verze Instalační služby Windows je starší než 3.1.|
|**0x80cf1002**|OM_E_MSI_NOT_CONFIGURED|Při hledání se asi nenašly některé aktualizace, protože Instalační služba Windows není nakonfigurovaná.|
|**0x80cf1003**|OM_E_MSP_DISABLED|Při hledání se asi nenašly některé aktualizace, protože zásady zakázaly použití dílčích oprav Instalační služby Windows.|
|**0x80cf1004**|OM_E_MSI_WRONG_APP_CONTEXT|Aktualizaci nešlo použít, protože aplikace je nainstalovaná pro jednotlivé uživatele.|
|**0x80cf2000**|OM_E_UH_REMOTEUNAVAILABLE|Žádost o obslužnou rutinu vzdálené aktualizace nešlo dokončit, protože není dostupný žádný vzdálený proces.|
|**0x80cf2001**|OM_E_UH_LOCALONLY|Žádost o obslužnou rutinu vzdálené aktualizace nešlo dokončit, protože obslužná rutina je jenom místní.|
|**0x80cf2003**|OM_E_UH_REMOTEALREADYACTIVE|Obslužnou rutinu vzdálené aktualizace nešlo vytvořit, protože už existuje.|
|**0x80cf2004**|OM_E_UH_DOESNOTSUPPORTACTION|Žádost o to, aby obslužná rutina nainstalovala (odinstalovala) aktualizaci, nešlo dokončit, protože aktualizace instalaci (odinstalaci) nepodporuje.|
|**0x80cf2005**|OM_E_UH_WRONGHANDLER|Operaci nešlo dokončit, protože byla zadána špatná obslužná rutina.|
|**0x80cf2006**|OM_E_UH_INVALIDMETADATA|Operaci obslužné rutiny nešlo dokončit, protože aktualizace obsahuje metadata, která nejsou platná.|
|**0x80cf2007**|OM_E_UH_INSTALLERHUNG|Operaci nešlo dokončit, protože instalační program překročil časový limit. Zkontrolujte, jestli nebylo schváleno nasazení aktualizace, která vyžaduje interakci s uživatelem. Pokud ano, musíte parametry instalace aktualizace změnit tak, by šlo aktualizaci nainstalovat bezobslužně.|
|**0x80cf2008**|OM_E_UH_OPERATIONCANCELLED|Operace prováděná obslužnou rutinou aktualizace byla zrušena.|
|**0x80cf2009**|OM_E_UH_BADHANDLERXML|Operaci nešlo dokončit, protože metadata specifická pro obslužnou rutinu nejsou platná.|
|**0x80cf200B**|OM_E_UH_INSTALLERFAILURE|Instalačnímu programu se nepovedlo nainstalovat (odinstalovat) nejmíň jednu aktualizaci.|
|**0x80cf200D**|OM_E_UH_NEEDANOTHERDOWNLOAD|Obslužná rutina aktualizace aktualizaci nenainstalovala, protože se musí znova stáhnout.|
|**0x80cf200E**|OM_E_UH_NOTIFYFAILURE|Obslužné rutině aktualizace se nepovedlo odeslat oznámení o stavu operace instalace (odinstalace).|
|**0x80cf2014**|OM_E_UH_POSTREBOOTSTILLPENDING|Operace po restartování pro danou aktualizaci pořád probíhá.|
|**0x80cf2015**|OM_E_UH_POSTREBOOTRESULTUNKNOWN|Výsledek operace po restartování pro danou aktualizaci nešlo zjistit.|
|**0x80cf2016**|OM_E_UH_POSTREBOOTUNEXPECTEDSTATE|Po dokončení operace po restartování je aktualizace v neočekávaném stavu.|
|**0x80cf2017**|OM_E_UH_NEW_SERVICING_STACK_REQUIRED|Před stažením nebo instalací této aktualizace se musí aktualizovat sada služeb operačního systému.|
|**0x80cf2018**|OM_E_UH_CALLED_BACK_FAILURE|Při zpětném volání instalačního programu se zpětným voláním došlo k chybě.|
|**0x80cf2019**|OM_E_UH_CUSTOMINSTALLER_INVALID_SIGNATURE|Vlastní podpis instalačního programu neodpovídá podpisu, který vyžaduje aktualizace.|
|**0x80cf201A**|OM_E_UH_UNSUPPORTED_INSTALLCONTEXT|Instalační program nepodporuje příslušnou konfiguraci instalace.|
|**0x80cf201B**|OM_E_UH_INVALID_TARGETSESSION|Cílená relace pro instalaci není platná.|
|**0x80cf2FFF**|OM_E_UH_UNEXPECTED|Chyba obslužné rutiny aktualizace není předmětem jiného kódu OM_E_UH_&#42;.|
|**0x80cf3FFD**|OM_E_NON_UI_MODE|V režimu bez uživatelského rozhraní nejde zobrazit uživatelské rozhraní. Nejspíš nejsou nainstalované moduly uživatelského rozhraní klienta služby Windows Update.|
|**0x80cf3FFE**|OM_E_WUCLTUI_UNSUPPORTED_VERSION|Tato verze exportovaných funkcí uživatelského rozhraní klienta služby WU není podporovaná.|
|**0x80cf3FFF**|OM_E_AUCLIENT_UNEXPECTED|Došlo k chybě uživatelského rozhraní, která není předmětem jiného kódu chyby OM_E_AUCLIENT_&#42;.|
|**0x80cf4007**|OM_E_PT_SOAPCLIENT_SOAPFAULT|Stejné jako **SOAPCLIENT_SOAPFAULT**. V klientovi SOAP došlo k chybě, protože nastala chyba protokolu SOAP s kódem chyby typu **OM_E_PT_SOAP_&#42;** .|
|**0x80cf4008**|OM_E_PT_SOAPCLIENT_PARSEFAULT|Stejné jako **SOAPCLIENT_PARSEFAULT_ERROR**.  Klientovi SOAP se nepovedlo analyzovat chybu protokolu SOAP.|
|**0x80cf400A**|OM_E_PT_SOAPCLIENT_PARSE|Stejné jako **SOAPCLIENT_PARSE_ERROR**.  Klientovi SOAP se nepovedlo analyzovat odpověď ze serveru.|
|**0x80cf400B**|OM_E_PT_SOAP_VERSION|Stejné jako **SOAP_E_VERSION_MISMATCH**. Klient SOAP zjistil nerozpoznatelný obor názvů pro obálku protokolu SOAP.|
|**0x80cf400C**|OM_E_PT_SOAP_MUST_UNDERSTAND|Stejné jako **SOAP_E_MUST_UNDERSTAND**. Klient SOAP nedokázal přeložit hlavičku.|
|**0x80cf400D**|OM_E_PT_SOAP_CLIENT|Stejné jako **SOAP_E_CLIENT**. Klient SOAP zjistil, že je zpráva poškozená. Než ji odešlete znova, opravte ji.|
|**0x80cf400E**|OM_E_PT_SOAP_SERVER|Stejné jako **SOAP_E_SERVER**. Zprávu SOAP nešlo kvůli chybě serveru zpracovat. Odešlete ji znova později.|
|**0x80cf4010**|OM_E_PT_EXCEEDED_MAX_SERVER_TRIPS|Počet zpátečních cest k serveru překročil maximální limit.|
|**0x80cf4012**|OM_E_PT_DOUBLE_INITIALIZATION|Inicializace se nepovedla, protože daný objekt je už inicializovaný.|
|**0x80cf4013**|OM_E_PT_INVALID_COMPUTER_NAME|Název počítače nešlo zjistit.|
|**0x80cf4015**|OM_E_PT_REFRESH_CACHE_REQUIRED|Z odpovědi serveru to vypadá, že se server změnil nebo byl soubor cookie neplatný. Aktualizujte interní mezipaměť a akci opakujte.|
|**0x80cf4016**|OM_E_PT_HTTP_STATUS_BAD_REQUEST|Stejné jako **stav HTTP 400**. Server nemohl žádost kvůli neplatné syntaxi zpracovat.|
|**0x80cf4017**|OM_E_PT_HTTP_STATUS_DENIED|Stejné jako **stav HTTP 401**. Požadovaný prostředek vyžaduje ověření uživatele.|
|**0x80cf4018**|OM_E_PT_HTTP_STATUS_FORBIDDEN|Stejné jako **stav HTTP 403**. Server žádosti rozumí, ale odmítl ji splnit.|
|**0x80cf4019**|OM_E_PT_HTTP_STATUS_NOT_FOUND|Stejné jako **stav HTTP 404**. Server nemůže najít požadovaný identifikátor URI (Uniform Resource Identifier).|
|**0x80cf401A**|OM_E_PT_HTTP_STATUS_BAD_METHOD|Stejné jako **stav HTTP 405**. Příslušná metoda HTTP není povolená.|
|**0x80cf401B**|OM_E_PT_HTTP_STATUS_PROXY_AUTH_REQ|Stejné jako **stav HTTP 407**. Požaduje se ověření proxy serverem.|
|**0x80cf401C**|OM_E_PT_HTTP_STATUS_REQUEST_TIMEOUT|Stejné jako **stav HTTP 408**. Časový limit čekání serveru na žádost vypršel.|
|**0x80cf401D**|OM_E_PT_HTTP_STATUS_CONFLICT|Stejné jako **stav HTTP 409**. Žádost se kvůli konfliktu s aktuálním stavem prostředku nedokončila.|
|**0x80cf401E**|OM_E_PT_HTTP_STATUS_GONE|Stejné jako **stav HTTP 410**. Požadovaný prostředek už není na serveru dostupný.|
|**0x80cf401F**|OM_E_PT_HTTP_STATUS_SERVER_ERROR|Stejné jako **stav HTTP 500**. Splnění žádosti zabránila vnitřní chyba serveru.|
|**0x80cf4020**|OM_E_PT_HTTP_STATUS_NOT_SUPPORTED|Stejné jako **stav HTTP 500**. Server nepodporuje funkci, která je nutná ke splnění žádosti.|
|**0x80cf4021**|OM_E_PT_HTTP_STATUS_BAD_GATEWAY|Stejné jako **stav HTTP 502**. V době, kdy server fungoval jako brána nebo proxy server, dostal neplatnou odpověď od nadřazeného serveru, ke kterému získával přístup, když se snažil splnit žádost.|
|**0x80cf4022**|OM_E_PT_HTTP_STATUS_SERVICE_UNAVAIL|Stejné jako **stav HTTP 503**. Služba je dočasně přetížená.|
|**0x80cf4023**|OM_E_PT_HTTP_STATUS_GATEWAY_TIMEOUT|Stejné jako **stav HTTP 503**. Při čekání na bránu vypršel časový limit žádosti.|
|**0x80cf4024**|OM_E_PT_HTTP_STATUS_VERSION_NOT_SUP|Stejné jako **stav HTTP 505**. Server nepodporuje verzi protokolu HTTP použitou v žádosti.|
|**0x80cf4025**|OM_E_PT_FILE_LOCATIONS_CHANGED|Operace se kvůli změně umístění souboru nepovedla. Aktualizujte vnitřní mezipaměť a opakujte odeslání.|
|**0x80cf4027**|OM_E_PT_NO_AUTH_PLUGINS_REQUESTED|Server vrátil prázdný seznam ověřovacích informací.|
|**0x80cf4028**|OM_E_PT_NO_AUTH_COOKIES_CREATED|Agentovi se nepovedlo vytvořit žádné platné ověřovací soubory cookie.|
|**0x80cf4029**|OM_E_PT_INVALID_CONFIG_PROP|Hodnota vlastnosti konfigurace byla špatná.|
|**0x80cf402A**|OM_E_PT_CONFIG_PROP_MISSING|Hodnota vlastnosti konfigurace chyběla.|
|**0x80cf402B**|OM_E_PT_HTTP_STATUS_NOT_MAPPED|Požadavek HTTP se nemohl být dokončit a důvod neodpovídá žádnému kódu chyby **OM_E_PT_HTTP_&#42;** .|
|**0x80cf402C**|OM_E_PT_WINHTTP_NAME_NOT_RESOLVED|Stejné jako **ERROR_WINHTTP_NAME_NOT_RESOLVED**. Název proxy serveru nebo cílového serveru nejde přeložit.|
|**0x80cf402F**|OM_E_PT_ECP_SUCCEEDED_WITH_ERRORS|Zpracování externích souborů .cab bylo dokončeno s několika chybami.|
|**0x80cf4030**|OM_E_PT_ECP_INIT_FAILED|Inicializace procesoru externích souborů .cab nebyla dokončena.|
|**0x80cf4031**|OM_E_PT_ECP_INVALID_FILE_FORMAT|Formát souboru metadat není platný.|
|**0x80cf4032**|OM_E_PT_ECP_INVALID_METADATA|Procesor externích souborů .cab našel metadata, která nejsou platná.|
|**0x80cf4033**|OM_E_PT_ECP_FAILURE_TO_EXTRACT_DIGEST|Z externího souboru .cab nešlo extrahovat hodnotu hash souboru.|
|**0x80cf4034**|OM_E_PT_ECP_FAILURE_TO_DECOMPRESS_CAB_FILE|Externí soubor .cab nešlo dekomprimovat.|
|**0x80cf4035**|OM_E_PT_ECP_FILE_LOCATION_ERROR|Procesoru externích souborů .cab se nepovedlo načíst umístění souborů.|
|**0x80cf4FFF**|OM_E_PT_UNEXPECTED|Došlo k chybě komunikace, která není předmětem jiného kódu chyby **OM_E_PT_&#42;** .|
|**0x80cf6001**|OM_E_DM_URLNOTAVAILABLE|Operaci správce stahování nešlo dokončit, protože požadovaný soubor nemá adresu URL.|
|**0x80cf6002**|OM_E_DM_INCORRECTFILEHASH|Operaci správce stahování nešlo dokončit, protože nebyla rozpoznána hodnota hash souboru.|
|**0x80cf6003**|OM_E_DM_UNKNOWNALGORITHM|Operaci správce stahování nešlo dokončit, protože metadata souboru požadovala nerozpoznaný hashovací algoritmus.|
|**0x80cf6005**|OM_E_DM_NONETWORK|Operaci správce stahování nešlo dokončit, protože nebylo dostupné síťové připojení.|
|**0x80cf6007**|OM_E_DM_NOTDOWNLOADED|Aktualizace se nestáhla.|
|**0x80cf6008**|OM_E_DM_FAILTOCONNECTTOBITS|Operace správce stahování se nepovedla, protože správce stahování nemohl připojit službu BITS (Background Intelligent Transfer Service).|
|**0x80cf6009**|OM_E_DM_BITSTRANSFERERROR|Operace správce stahování se nepovedla, protože došlo k nespecifikované chybě přenosu služby BITS (Background Intelligent Transfer Service).|
|**0x80cf600a**|OM_E_DM_DOWNLOADLOCATIONCHANGED|Stahování se musí restartovat, protože se změnilo umístění zdroje tohoto stahování.|
|**0x80cf600B**|OM_E_DM_CONTENTCHANGED|Stahování se musí restartovat, protože se v nové revizi změnil obsah aktualizace.|
|**0x80cf6FFF**|OM_E_DM_UNEXPECTED|Došlo k chybě správce stahování, která není předmětem jiného kódu chyby **OM_E_DM_&#42;** .|
|**0x80cf7003**|OM_E_INVALID_EVENT_PAYLOAD|Byla zadána neplatná datová část události.|
|**0x80cf7004**|OM_E_INVALID_EVENT_PAYLOADSIZE|Velikost odeslané datové části události není platná.|
|**0x80cf7005**|OM_E_SERVICE_NOT_REGISTERED|Služba není zaregistrovaná.|
|**0x80cf8000**|OM_E_DS_SHUTDOWN|Operace ne nepovedla, protože se vypíná agent.|
|**0x80cf8001**|OM_E_DS_INUSE|Operace se nepovedla, protože se používalo úložiště dat.|
|**0x80cf8002**|OM_E_DS_INVALID|Aktuální a očekávaný stav úložiště dat se neshodují.|
|**0x80cf8003**|OM_E_DS_TABLEMISSING|V úložišti dat chybí tabulka.|
|**0x80cf8004**|OM_E_DS_TABLEINCORRECT|Úložiště dat obsahuje tabulku s neočekávanými sloupci.|
|**0x80cf8005**|OM_E_DS_INVALIDTABLENAME|Tabulku nešlo otevřít, protože není v úložišti dat.|
|**0x80cf8006**|OM_E_DS_BADVERSION|Aktuální a očekávaná verze úložiště dat se neshodují.|
|**0x80cf8007**|OM_E_DS_NODATA|V úložišti dat nejsou požadované informace.|
|**0x80cf8008**|OM_E_DS_MISSINGDATA|V úložišti dat chybí požadované informace, nebo má ve sloupci tabulky, který vyžaduje jinou hodnotu než null, hodnotu null.|
|**0x80cf8009**|OM_E_DS_MISSINGREF|V úložišti dat chybí požadované informace, nebo obsahuje odkaz na chybějící licenční podmínky, soubor, lokalizovanou vlastnost nebo propojený řádek.|
|**0x80cf800A**|OM_E_DS_UNKNOWNHANDLER|Aktualizace nebyla zpracována, protože nebyla rozpoznána její obslužná rutina.|
|**0x80cf800B**|OM_E_DS_CANTDELETE|Aktualizace nebyla odstraněna, protože na ni pořád odkazuje nejmíň jedna služba.|
|**0x80cf800C**|OM_E_DS_LOCKTIMEOUTEXPIRED|Oddíl úložiště dat nešlo v přiděleném čase zamknout.|
|**0x80cf800E**|OM_E_DS_ROWEXISTS|Řádek se nepřidal, protože stávající řádek má stejný primární klíč.|
|**0x80cf800F**|OM_E_DS_STOREFILELOCKED|Úložiště dat nešlo inicializovat, protože ho zamknul jiný proces.|
|**0x80cf8010**|OM_E_DS_CANNOTREGISTER|Úložiště dat není povoleno zaregistrovat u modelu COM v aktuálním procesu.|
|**0x80cf8011**|OM_E_DS_UNABLETOSTART|Operaci se nepovedlo vytvořit objekt úložiště dat v jiném procesu.|
|**0x80cf8013**|OM_E_DS_DUPLICATEUPDATEID|Server poslal klientovi stejnou aktualizaci se dvěma různými identifikátory revize.|
|**0x80cf8014**|OM_E_DS_UNKNOWNSERVICE|Operaci nešlo dokončit, protože služba není v úložišti dat.|
|**0x80cf8015**|OM_E_DS_SERVICEEXPIRED|Operaci nešlo dokončit, protože platnost registrace služby vypršela.|
|**0x80cf8016**|OM_E_DS_DECLINENOTALLOWED|Žádost o skrytí aktualizace byla odmítnuta, protože jde o povinnou aktualizaci nebo proto, že byla nasazena s konečným termínem.|
|**0x80cf8017**|OM_E_DS_TABLESESSIONMISMATCH|Tabulka se nezavřela, protože není přidružená k relaci.|
|**0x80cf8018**|OM_E_DS_SESSIONLOCKMISMATCH|Tabulka se nezavřela, protože není přidružená k relaci.|
|**0x80cf8019**|OM_E_DS_NEEDWINDOWSSERVICE|Žádost o odebrání nebo zrušení registrace služby byla odmítnuta, protože se jedná o integrovanou službu nebo proto, že se funkce Automatické aktualizace nemůže vrátit k jiné službě.|
|**0x80cf801A**|OM_E_DS_INVALIDOPERATION|Žádost byla odmítnuta, protože operace není povolená.|
|**0x80cf801B**|OM_E_DS_SCHEMAMISMATCH|Schéma aktuálního úložiště dat a schéma tabulky v záložním dokumentu XML se neshodují.|
|**0x80cf801C**|OM_E_DS_RESETREQUIRED|Úložiště dat vyžaduje resetování relace. Uvolněte relaci a zkuste to znova s novou relací.|
|**0x80cf801D**|OM_E_DS_IMPERSONATED|Operaci úložiště dat nešlo dokončit, protože byla vyžádána se zosobněnou identitou.|
|**0x80cf8FFF**|OM_E_DS_UNEXPECTED|Došlo k chybě úložiště dat, která není předmětem jiného kódu **OM_E_DS_&#42;** .|
|**0x80cfA000**|OM_E_AU_NOSERVICE|Funkce Automatické aktualizace nemohla zpracovat příchozí žádosti.|
|**0x80cfA004**|OM_E_AU_PAUSED|Funkce Automatické aktualizace nemohla zpracovat příchozí žádosti, protože byla pozastavena.|
|**0x80cfA005**|OM_E_AU_NO_REGISTERED_SERVICE|Ve funkci Automatické aktualizace není zaregistrovaná žádná nespravovaná služba.|
|**0x80cfA006**|OM_E_AU_DETECT_SVCID_MISMATCH|Výchozí služba zaregistrovaná ve funkci Automatické aktualizace se během hledání změnila.|
|**0x80cfA007**|OM_E_AU_ALREADY_PROMPTING_FOR_REBOOT|Funkce Automatické aktualizace už uživateli zobrazuje výzvu k restarování.|
|**0x80cfAFFF**|OM_E_AU_UNEXPECTED|Došlo k chybě funkce Automatické aktualizace, která není předmětem jiného kódu **OM_E_AU &#42;** .|
|**0x80cfE001**|OM_E_EE_UNKNOWN_EXPRESSION|Operaci vyhodnocovacího filtru výrazů nešlo kvůli nerozpoznanému výrazu dokončit.|
|**0x80cfE002**|OM_E_EE_INVALID_EXPRESSION|Operaci vyhodnocovacího filtru výrazů nešlo kvůli neplatnému výrazu dokončit.|
|**0x80cfE003**|OM_E_EE_MISSING_METADATA|Operaci vyhodnocovacího filtru výrazů nešlo dokončit, protože výraz obsahuje nesprávný počet uzlů metadat.|
|**0x80cfE004**|OM_E_EE_INVALID_VERSION|Operaci vyhodnocovacího filtru výrazů nešlo dokončit, protože verze serializovaných dat výrazu není platná.|
|**0x80cfE005**|OM_E_EE_NOT_INITIALIZED|Vyhodnocovací filtr výrazů nešlo inicializovat.|
|**0x80cfE006**|OM_E_EE_INVALID_ATTRIBUTEDATA|Operaci vyhodnocovacího filtru výrazů nešlo kvůli neplatnému atributu dokončit.|
|**0x80cfE007**|OM_E_EE_CLUSTER_ERROR|Operaci vyhodnocovacího filtru výrazů nešlo dokončit, protože se nedal zjistit stav clusteru počítače.|
|**0x80cfEFFF**|OM_E_EE_UNEXPECTED|Došlo k chybě vyhodnocovacího filtru výrazů, která není předmětem jiného kódu chyby **OM_E_EE_&#42;** .|
|**0x80cfF001**|OM_E_REPORTER_EVENTCACHECORRUPT|Soubor mezipaměti událostí byl poškozený.|
|**0x80cfF002**|OM_E_REPORTER_EVENTNAMESPACEPARSEFAILED|Kód XML v popisovači oboru názvů událostí nešlo analyzovat.|
|**0x80cfF003**|OM_E_INVALID_EVENT|Kód XML v popisovači oboru názvů událostí není platný.|
|**0x80cfF004**|OM_E_SERVER_BUSY|Server odmítl událost, protože byl moc zaneprázdněný.|
|**0x80cfFFFF**|OM_E_REPORTER_UNEXPECTED|Došlo k chybě ohlašování, která není předmětem jiného kódu chyby.|
|**0x80af0005**|OMC_E_INSTALL_NOT_ALLOWED_REBOOT_REQUIRED|Instalace se nepovedla, protože se čeká na povinné restartování.|
|**0x80af0006**|OMC_E_DOWNLOAD_CANCELLED|Stahování bylo zrušeno.|