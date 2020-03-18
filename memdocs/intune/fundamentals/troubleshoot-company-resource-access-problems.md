---
title: Stavové a chybové kódy v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam chyb, stavový kód, popisy a rozlišení při použití zařízení spravovaných přes MDM, získání přístupu k prostředkům společnosti, chyb na zařízeních s iOS/iPadOS a chyby odezvy OMA v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 40622ced-6029-4abf-873e-b51d2b51934c
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91a0f717a8ed3d5574b731fe2f20a40c5494a160
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330459"
---
# <a name="common-error-codes-and-descriptions-in-microsoft-intune"></a>Běžné kódy chyb a popisy v Microsoft Intune

V tomto článku jsou uvedené běžné chyby, stavové kódy, popisy a možná řešení při přístupu k prostředkům organizace. Tyto informace vám pomůžou při řešení potíží s přístupem při použití Microsoft Intune.

Pokud potřebujete pomoc, přečtěte si téma [získání podpory pro Microsoft Intune](get-support.md).

## <a name="status-codes-for-mdm-managed-windows-devices"></a>Stavové kódy pro zařízení s Windows spravovaná systémem MDM

|Stavový kód|Chybová zpráva|Co dělat|
|---------------|-----------------|--------------|
|10 (APP_CI_ENFORCEMENT_IN_PROGRESS)|Probíhá instalace||
|20 (APP_CI_ENFORCEMENT_IN_PROGRESS_WAITING_CONTENT)|Čeká se na obsah||
|30 (APP_CI_ENFORCEMENT_ERROR_RETRIEVING_CONTENT)|Načítá se obsah|Pravděpodobná příčina: Stav úlohy 30 označuje, že se uživateli nepodařilo stáhnout aplikaci.<br /><br />Toto jsou pravděpodobné příčiny:<br /><br />V průběhu stahování zařízení ztratilo připojení k internetu.<br /><br />Mohlo dojít k vypršení platnosti certifikátu vydaného pro zařízení v době registrace.<br /><br />Snížení rizika:<br /><br />Spuštěním aplikace společnosti z ovládacích panelů na zařízení potvrďte, že platnost certifikátu zařízení nevypršela. Pokud má, bude nutné zařízení znovu zaregistrovat.<br /><br />Potvrďte, že zařízení je připojené k internetu , a zkuste znovu požádat o aplikaci.|
|40 (APP_CI_ENFORCEMENT_IN_PROGRESS_CONTENT_DOWNLOADED)|Stahování obsahu se dokončilo||
|50 (APP_CI_ENFORCEMENT_IN_PROGRESS_INSTALLING)|Probíhá instalace||
|60 (APP_CI_ENFORCEMENT_ERROR_INSTALLING)|Při instalaci došlo k chybě|Aplikaci se po stažení nepodařilo nainstalovat.<br /><br />Certifikát pro podpis kódu, kterým je aplikace podepsaná, se v zařízení nenachází.<br /><br />Závislost architektury, na které je aplikace závislá, není na zařízení nainstalovaná.<br /><br />Ujistěte se, že certifikát pro podpis kódu, se kterým je aplikace podepsaná, v zařízení existuje, a u správce ověřte, že tento certifikát je určený pro všechna zapsaná podniková zařízení s Windows RT.<br /><br />V případě, že je chyba instalace způsobená chybějící závislostí architektury, bude muset správce aplikaci znovu publikovat v balíčku společně s aplikací.<br /><br />Stažený balíček aplikace není platným balíčkem, je pravděpodobně poškozen nebo není kompatibilní s verzí operačního systému v zařízení.|
|70 (APP_CI_ENFORCEMENT_SUCCEEDED)|Instalace byla úspěšná||
|80 (APP_CI_ENFORCEMENT_IN_PROGRESS)|Probíhá odinstalace||
|90 (APP_CI_ENFORCEMENT_ERROR)|Došlo k chybě odinstalace||
|100 (APP_CI_ENFORCEMENT_SUCCEEDED)|Odinstalace byla úspěšná||
|110 (APP_CI_ENFORCEMENT_ERROR)|Neshoda algoritmu hash obsahu||
|120 (APP_CI_ENFORCEMENT_ERROR)|SLK / zkušební načítání se nepovoluje||
|130 (APP_CI_ENFORCEMENT_ERROR)|Instalace licence MSADP se nepodařila||
|Bez stavu (APP_CI_ENFORCEMENT_UNKNOWN)|není k dispozici|Stav je momentálně neznámý.|

## <a name="company-resource-access-common-errors"></a>Přístup k prostředkům společnosti (běžné chyby)

|Stavový kód|Šestnáctkový kód chyby|Chybová zpráva|
|---------------|--------------------------|-----------------|
|-2016281101|0x87D1FDF3|Nenašla se žádost MDM CRP.|
|-2016281102|0x87D1FDF2|Nenašla se adresa URL služby NDES.|
|-2016281103|0x87D1FDF1|Nenašly se informace o certifikátu MDM CRP.|
|-2016281104|0x87D1FDF0|Nenašly se informace o certifikátu MDM CI.|
|-2016281105|0x87D1FDEF|Pravidlo se nepodařilo vyhodnotit.|
|-2016281106|0x87D1FDEE|Nedá se použít kvůli ztrátě při řešení konfliktů.|
|-2016281107|0x87D1FDED|Nepodporovaný zdroj nastavení zjišťování|
|-2016281108|0x87D1FDEC|Odkazované nastavení se nepodařilo ve službě CI najít.|
|-2016281109|0x87D1FDEB|Převod datového typu se nepodařil.|
|-2016281110|0x87D1FDEA|Neplatný parametr pro nastavení služby CIM|
|-2016281111|0x87D1FDE9|Neplatí pro toto zařízení.|
|-2016281112|0x87D1FDE8|Náprava se nepodařila.|
|-2016330905|0x87D13B67|Stav aplikace je neznámý.|
|-2016330906|0x87D13B66|Aplikace je spravovaná, ale uživatel ji odebral.|
|-2016330907|0x87D13B65|Zařízení uplatňuje kód.|
|-2016330908|0x87D13B64|Aplikaci se nepovedlo nainstalovat.|
|-2016330909|0x87D13B63|Uživatel odmítl nabídku na aktualizaci aplikace.|
|-2016330910|0x87D13B62|Uživatel odmítl nabídku na instalaci aplikace.|
|-2016330911|0x87D13B61|Uživatel nainstaloval aplikaci dřív, než se mohla provést instalace spravované aplikace.|
|-2016330912|0x87D13B60|Instalace aplikace je naplánovaná, ale aby se dala dokončit transakce, potřebuje se kód, který by se dal uplatnit.|
|-2016341109|0x87D1138B|Zařízení s platformou iOS vrátilo chybu.|
|-2016341110|0x87D1138A|Zařízení s platformou iOS zamítlo příkaz kvůli nesprávnému formátu.|
|-2016341111|0x87D11389|Zařízení s platformou iOS vrátilo neočekávaný stav nečinnosti.|
|-2016341112|0x87D11388|Zařízení s platformou iOS je momentálně zaneprázdněné.|

## <a name="errors-returned-by-iosipados-devices"></a>Chyby vrácené zařízeními se systémem iOS/iPadOS

### <a name="company-portal-errors"></a>Chyby Portálu společnosti

|Text chyby na Portálu společnosti|Stavový kód HTTP|Další informace o chybě|
|---|---|---|
|__Vnitřní chyba serveru__ <br>Vypadá to, že nám se nám nepovedlo kontaktovat kvůli vnitřní chybě na našem serveru. Zkuste to znovu, a pokud s tím budou problémy dál, obraťte se na správce.|Chyba 500|Tato chyba je pravděpodobně způsobena problémem ve službě Intune. Problém by se měl řešit na straně služby Intune a není způsobený potížemi na straně zákazníka.|
|__Dočasně nedostupné__ <br>Vypadá to, že se nám nepovedlo kontaktovat, protože naše služba je dočasně nedostupná. Zkuste to znovu, a pokud s tím budou problémy dál, obraťte se na správce.|Chyba 503|Jedná se pravděpodobně o dočasný problém se službou Intune, může například probíhat údržba služby. Problém by se měl řešit na straně služby Intune a není způsobený potížemi na straně zákazníka.|
|__Nejde se připojit k serveru__ <br>Vypadá to, že se nám nepovedlo kontaktovat. Zkuste to znovu, a pokud s tím budou problémy dál, obraťte se na správce.|Není přidružen stavový kód HTTP|Nepovedlo se navázat zabezpečené připojení k serveru, pravděpodobně kvůli problému s certifikáty, které používá protokol SSL. K tomuto problému může dojít kvůli tomu, že konfigurace zákazníka nejsou v souladu s požadavky společnosti Apple na ATS (App Transport Security).|
|__Něco se nepovedlo__ <br>Klient Portál společnosti se nedal načíst. Zkuste to znovu, a pokud s tím budou problémy dál, obraťte se na správce.|Chyba 400|Všechny chyby se stavovým kódem HTTP obsahující 400, které nemají podrobnější chybovou zprávu, zobrazí toto. Toto je chyba na straně klienta, která se děje v aplikaci Portál společnosti pro iOS/iPadOS.|
|__Nejde kontaktovat server__ <br>Vypadá to, že se nám nepovedlo kontaktovat. Zkuste to znovu, a pokud s tím budou problémy dál, obraťte se na správce.|Chyba 500|Všechny chyby se stavovým kódem HTTP obsahující 500, které nemají podrobnější chybovou zprávu, zobrazí toto. Jedná se o chybu služby Intune, ke které dochází na straně služby.|

### <a name="service-errors"></a>Chyby služby

|Stavový kód|Šestnáctkový kód chyby|Chybová zpráva|
|---------------|--------------------------|-----------------|
|-2016299111|0x87D1B799|Vnitřní chyba|
|-2016299112|0x87D1B798|Vnitřní chyba|
|-2016300111|0x87D1B3B1|36001:(vnitřní chyba)|
|-2016300112|0x87D1B3B0|36000:Mobilní připojení už je nakonfigurované.|
|-2016301110|0x87D1AFCA|35002:V jedné datové části je víc písem.|
|-2016301111|0x87D1AFC9|35001:Instalace písma selhala.|
|-2016301112|0x87D1AFC8|35000:Neplatná data písma|
|-2016302109|0x87D1ABE3|34003:Neplatný hlavní název protokolu Kerberos|
|-2016302110|0x87D1ABE2|34003:Chybí hlavní název protokolu Kerberos.|
|-2016302111|0x87D1ABE1|34001:Neplatný vzor pro shodu adresy URL|
|-2016302112|0x87D1ABE0|34000:Neplatný vzor pro shodu identifikátoru aplikace server|
|-2016304112|0x87D1A410|32000:Moc aplikací|
|-2016305111|0x87D1A029|31001:Nastavení nejde použít.|
|-2016305112|0x87D1A028|31000:Přihlašovací údaje nejde použít.|
|-2016306111|0x87D19C41|30001:Vypršel časový limit.|
|-2016306112|0x87D19C40|30000:Ověření se nepovedlo.|
|-2016307109|0x87D1985B|29003:Chybná data certifikátu|
|-2016307110|0x87D1985A|29002:|
|-2016307111|0x87D19859|29001:|
|-2016307112|0x87D19858|29000:Zařízení není pod dohledem.|
|-2016308110|0x87D19472|28002:Nejde nastavit tapetu.|
|-2016308111|0x87D19471|28001:Chybný obrázek tapety|
|-2016308112|0x87D19470|28000:Neznámá položka|
|-2016310111|0x87D18CA1|26001:Nepodporované šifrování na úrovni souborů|
|-2016310112|0x87D18CA0|26000:Nepodporované šifrování na úrovni bloků|
|-2016311110|0x87D188BA|25002:Nejde odebrat.|
|-2016311111|0x87D188B9|25001:Nejde nainstalovat.|
|-2016311112|0x87D188B8|25000:Chybný profil|
|-2016312109|0x87D184D3|24003:Chybný finální profil|
|-2016312110|0x87D184D2|24002:Chybná datová část identity|
|-2016312111|0x87D184D1|24001:Nejde podepsat slovník atributů.|
|-2016312112|0x87D184D0|24000:Nejde vytvořit slovník atributů.|
|-2016313110|0x87D180EA|23002:Neplatný certifikát serveru|
|-2016313111|0x87D180E9|23001:Chybná odpověď serveru|
|-2016313112|0x87D180E8|23000:Chybná identita|
|-2016314099|0x87D17D0D|22013:Neplatná odpověď PKIOperation|
|-2016314100|0x87D17D0C|22012:Nejde uložit CACertificate.|
|-2016314101|0x87D17D0B|22011:Nejde vygenerovat CSR.|
|-2016314102|0x87D17D0A|22010:Nejde uložit dočasnou identitu.|
|-2016314103|0x87D17D09|22009:Nejde vytvořit dočasnou identitu.|
|-2016314104|0x87D17D08|22008:Nejde vytvořit identitu.|
|-2016314105|0x87D17D07|22007:Neplatný podepsaný certifikát|
|-2016314106|0x87D17D06|22006:Nedostatečné CACaps|
|-2016314107|0x87D17D05|22005:Chyba sítě|
|-2016314108|0x87D17D04|22004:Nepodporovaná konfigurace certifikátu|
|-2016314109|0x87D17D03|22003:Neplatná odpověď RAResponse|
|-2016314110|0x87D17D02|22002:Neplatná odpověď CAResponse|
|-2016314111|0x87D17D01|22001:Nejde vygenerovat pár klíčů.|
|-2016314112|0x87D17D00|22000:Neplatné použití klíče|
|-2016315105|0x87D1791F|21007:Nejde ověřit účet.|
|-2016315106|0x87D1791E|21006:Nejde dešifrovat certifikát.|
|-2016315107|0x87D1791D|21005:Účet není jedinečný (e-mailový profil už na zařízení existuje)|
|-2016315108|0x87D1791C|21004:Nejde vytvořit účet.|
|-2016315109|0x87D1791B|21003:Žádný název hostitele|
|-2016315110|0x87D1791A|21002:Nejde dodržet zásadu šifrování ze serveru.|
|-2016315111|0x87D17919|21001:Nejde dodržet zásadu ze serveru.|
|-2016315112|0x87D17918|21000:Nejde získat zásadu ze serveru.|
|-2016316110|0x87D17532|20002:Účet není jedinečný.|
|-2016316111|0x87D17531|20001:Žádný název hostitele|
|-2016316112|0x87D17530|20000:Nejde vytvořit účet.|
|-2016317110|0x87D1714A|19002:Účet není jedinečný.|
|-2016317111|0x87D17149|19001:Žádný název hostitele|
|-2016317112|0x87D17148|19000:Nejde vytvořit účet.|
|-2016318110|0x87D16D62|18002:Neplatné přihlašovací údaje|
|-2016318111|0x87D16D61|18001:Nedosažitelný hostitel|
|-2016318112|0x87D16D60|18000:Neznámá chyba|
|-2016319110|0x87D1697A|17002:Účet není jedinečný.|
|-2016319111|0x87D16979|17001:Žádný název hostitele|
|-2016319112|0x87D16978|17000:Nejde vytvořit účet.|
|-2016320110|0x87D16592|16002:Účet není jedinečný.|
|-2016320111|0x87D16591|16001:Žádný název hostitele|
|-2016320112|0x87D16590|16000:Nejde vytvořit předplatné.|
|-2016321109|0x87D161AB|15003:Neplatný certifikát|
|-2016321110|0x87D161AA|15002:Nejde zamknout konfiguraci sítě.|
|-2016321111|0x87D161A9|15001:Nejde odebrat VPN.|
|-2016321112|0x87D161A8|15000:Nejde nainstalovat VPN.|
|-2016322110|0x87D15DC2|14002:Konfigurace cloudu už existuje.|
|-2016322111|0x87D15DC1|14001:Zařízení je zamčené.|
|-2016322112|0x87D15DC0|14000:Neplatné pole|
|-2016323107|0x87D159DD|13005:Nejde nastavit proxy server.|
|-2016323108|0x87D159DC|13004:Nejde nastavit protokol EAP.|
|-2016323109|0x87D159DB|13003:Nejde vytvořit konfiguraci připojení WiFi.|
|-2016323110|0x87D159DA|13002:Heslo je povinné.|
|-2016323111|0x87D159D9|13001:Uživatelské jméno je povinné.|
|-2016323112|0x87D159D8|13000:Nejde nainstalovat.|
|-2016324070|0x87D1561A|12042:Neznámý kód národního prostředí|
|-2016324071|0x87D15619|12041:Neznámý kód jazyka|
|-2016324072|0x87D15618|12040:Vyžadují se přihlašovací údaje pro přihlášení do obchodu iTunes.|
|-2016324073|0x87D15617|12039:(nepoužívá se)|
|-2016324074|0x87D15616|12038:Aplikace není spravovaná.|
|-2016324075|0x87D15615|12037:Neplatný kód pro uplatnění|
|-2016324076|0x87D15614|12036:Aplikaci nejde odebrat v aktuálním stavu.|
|-2016324077|0x87D15613|12035:Aplikaci nejde koupit.|
|-2016324078|0x87D15612|12034:Adresa URL není adresa HTTPS.|
|-2016324079|0x87D15611|12033:Neplatný manifest|
|-2016324080|0x87D15610|12032:V manifestu je moc velký počet aplikací.|
|-2016324081|0x87D1560F|12031:Instalace aplikace je zakázaná.|
|-2016324082|0x87D1560E|12030:Neplatná adresa URL|
|-2016324083|0x87D1560D|12029:Aplikace není spravovaná.|
|-2016324084|0x87D1560C|12028:Nečeká se na uplatnění kódu.|
|-2016324085|0x87D1560B|12027:Nejde o aplikaci.|
|-2016324086|0x87D1560A|12026:Aplikace už je ve frontě.|
|-2016324087|0x87D15609|12025:Aplikace už je nainstalovaná.|
|-2016324088|0x87D15608|12024:Nepovedlo se ověřit manifest aplikace.|
|-2016324089|0x87D15607|12023:Nepovedlo se ověřit ID aplikace.|
|-2016324090|0x87D15606|12022:Neplatné téma|
|-2016324091|0x87D15605|12021:Neplatný typ požadavku|
|-2016324092|0x87D15604|12020:Neautorizované serverem|
|-2016324093|0x87D15603|12019:Nejde zkopírovat tajný klíč v úschově.|
|-2016324094|0x87D15602|12018:Nejde zkopírovat data úložiště šifrovacích klíčů v úschově.|
|-2016324095|0x87D15601|12017:Nejde vytvořit úložiště šifrovacích klíčů v úschově.|
|-2016324096|0x87D15600|12016:Chybí identita.|
|-2016324097|0x87D155FF|12015:Nejde získat token push.|
|-2016324098|0x87D155FE|12014:Profil zřizování není spravovaný.|
|-2016324099|0x87D155FD|12013:Profil není spravovaný.|
|-2016324100|0x87D155FC|12012:Neshoda pro nahrazení MDM|
|-2016324101|0x87D155FB|12011: Neplatná konfigurace MDM|
|-2016324102|0x87D155FA|12010:Vnitřní chyba kvůli nekonzistenci|
|-2016324103|0x87D155F9|12009:Neplatný profil nahrazení|
|-2016324104|0x87D155F8|12008: Chybně vytvořený požadavek|
|-2016324105|0x87D155F7|12007:Neautorizované|
|-2016324106|0x87D155F6|12006:Odmítnuté přesměrování|
|-2016324107|0x87D155F5|12005:Nejde najít certifikát.|
|-2016324108|0x87D155F4|12004:Neplatný certifikát push|
|-2016324109|0x87D155F3|12003:Neplatná výzva/odezva pro ověřování|
|-2016324110|0x87D155F2|12002:Nejde provést vrácení se změnami.|
|-2016324111|0x87D155F1|12001:Několik instancí MDM|
|-2016324112|0x87D155F0|12000:Neplatná přístupová práva|
|-2016325111|0x87D15209|11001:Vlastní APN už je nainstalovaný.|
|-2016325112|0x87D15208|11000:Nejde nainstalovat APN.|
|-2016326111|0x87D14E21|10001:Neplatná podepisující osoba|
|-2016326112|0x87D14E20|10000:Nejde nainstalovat výchozí.|
|-2016327106|0x87D14A3E|9006:Certifikát není identita.|
|-2016327107|0x87D14A3D|9005:Certifikát je chybně vytvořený.|
|-2016327108|0x87D14A3C|9004:Nejde uložit kořenový certifikát.|
|-2016327109|0x87D14A3B|9003:Nejde uložit data WAPI.|
|-2016327110|0x87D14A3A|9002:Nejde uložit certifikát.|
|-2016327111|0x87D14A39|9001:V datové části je moc velký počet certifikátů.|
|-2016327112|0x87D14A38|9000:Neplatné heslo|
|-2016328112|0x87D14650|8000:Nejde nainstalovat funkci Web Clip.|
|-2016329105|0x87D1426F|7007:Účet SMTP je špatně nakonfigurovaný.|
|-2016329106|0x87D1426E|7006:Účet POP je špatně nakonfigurovaný.|
|-2016329107|0x87D1426D|7005:Účet IMAP je špatně nakonfigurovaný.|
|-2016329108|0x87D1426C|7004:Certifikát SMIME je chybný.|
|-2016329109|0x87D1426B|7003:Certifikát SMIME se nenašel.|
|-2016329110|0x87D1426A|7002:Během ověřování došlo k neznámé chybě.|
|-2016329111|0x87D14269|7001:Neplatné přihlašovací údaje|
|-2016329112|0x87D14268|7000:Nedosažitelný hostitel|
|-2016330110|0x87D13E82|6002:Nejde vytvořit dotaz.|
|-2016330111|0x87D13E81|6001:Prázdný řetězec|
|-2016330112|0x87D13E80|6000:Systémová chyba řetězce klíčů|
|-2016331097|0x87D13AA7|5015:Nejde nastavit období odkladu.|
|-2016331098|0x87D13AA6|5014:Nejde nastavit heslo.|
|-2016331099|0x87D13AA5|5013:Nejde vymazat heslo.|
|-2016331100|0x87D13AA4|5012:(nepoužívá se)|
|-2016331101||5011:Nesprávné heslo|
|-2016331102||5010:Zařízení je zamčené.|
|-2016331103|0x87D13AA4|5009:(nepoužívá se)|
|-2016331104|0x87D13AA0|5008:Stejné heslo se použilo v nedávné době.|
|-2016331105|0x87D13A9F|5007:Skončila platnost hesla.|
|-2016331106|0x87D13AA3|5006:V hesle musí být alfanumerické znaky.|
|-2016331107|0x87D13A9D|5005:V hesle musí být číslo.|
|-2016331108|0x87D13A9C|5004:V hesle jsou znaky, které jdou po sobě (vzestupně nebo sestupně).|
|-2016331109|0x87D13A9B|5003:V hesle jsou znaky, které se opakují.|
|-2016331110|0x87D13A9A|5002:Moc málo složitých znaků|
|-2016331111|0x87D13A99|5001:Moc málo jedinečných znaků|
|-2016331112|0x87D13A98|5000:Heslo je moc krátké.|
|-2016332093|0x87D136C3|4019:Několik datových částí App Lock|
|-2016332094|0x87D136C2|4018:Několik datových částí pro APN / mobilní připojení|
|-2016332095|0x87D136C1|4017:Několik globálních datových částí HTTPProxy|
|-2016332096|0x87D136C0|4016:(vnitřní chyba)|
|-2016332097|0x87D136BF|4015:Profil nahrazení neobsahuje datovou část MDM.|
|-2016332098|0x87D136BE|4014:Není dostupná žádná identita zařízení.|
|-2016332099|0x87D136BD|4013:Aktualizace selhala.|
|-2016332100|0x87D136BC|4012:Profil nejde aktualizovat.|
|-2016332101|0x87D136BB|4011:Finální profil není konfigurační profil.|
|-2016332102|0x87D136BA|4010:Aktualizovaný profil nemá stejný identifikátor.|
|-2016332103|0x87D136B9|4009:Zařízení je zamčené.|
|-2016332104|0x87D136B8|4008:Neshoda certifikátů|
|-2016332105|0x87D136B7|4007:Nerozpoznaný formát souboru|
|-2016332106|0x87D136B6|4006:Datum odebrání profilu je v minulosti.|
|-2016332107|0x87D136B5|4005:Heslo nevyhovuje zásadám.|
|-2016332108|0x87D136B4|4004: uživatel zrušil instalaci.|
|-2016332109|0x87D136B3|4003:Profil není ve frontě pro instalaci.|
|-2016332110|0x87D136B2|4002:Duplicitní UUID|
|-2016332111|0x87D136B1|4001:Selhání instalace|
|-2016332112|0x87D136B0|4000:Nejde analyzovat profil.|
|-2016333111|0x87D132C9|3001:Nekonzistení rozpoznávání porovnání hodnot (vnitřní chyba)|
|-2016333112|0x87D132C8|3000:Nekonzistení rozpoznávání omezení (vnitřní chyba)|
|-2016334108|0x87D12EE4|2004:Nepodporovaná hodnota pole|
|-2016334109|0x87D12EE3|2003:Chybný datový typ v poli|
|-2016334110|0x87D12EE2|2002:Chybí hodnota v povinném poli.|
|-2016334111|0x87D12EE1|2001:Nepodporovaná verze datové části|
|-2016334112|0x87D12EE0|2000:Chybně vytvořená datová část|
|-2016335102|0x87D12B02|1010:Nepodporovaná hodnota pole|
|-2016335103|0x87D12B01|1009:Selhání instalace profilu|
|-2016335104|0x87D12B00|1008:Nejedinečné identifikátory datové části|
|-2016335105|0x87D12AFF|1007:Nejedinečné identifikátory UUID|
|-2016335106|0x87D12AFE|1006:Nejde dešifrovat.|
|-2016335107|0x87D12AFD|1005:Prázdný profil|
|-2016335108|0x87D12AFC|1004:Chybný podpis|
|-2016335109|0x87D12AFB|1003:Chybný datový typ v poli|
|-2016335110|0x87D12AFA|1002:Chybí hodnota v povinném poli.|
|-2016335111|0x87D12AF9|1001:Nepodporovaná verze profilu|
|-2016335112|0x87D12AF8|1000:Chybně vytvořený profil|

## <a name="oma-response-codes"></a>Kódy odpovědí OMA

|Stavový kód|Šestnáctkový kód chyby|Chybová zpráva|
|---------------|--------------------------|-----------------|
|-2016344008|0x87D10838|(1404): Přístup k certifikátu zamítnut|
|-2016344009|0x87D10837|(1403): Certifikát nebyl nalezen|
|-2016344010|0x87D10836|DCMO(1402): Operace se nezdařila|
|-2016344011|0x87D10835|DCMO(1401): Uživatel reagoval na výzvu nepřijetím operace|
|-2016344012|0x87D10834|DCMO(1400): Chyba klienta|
|-2016344108|0x87D107D4|DCMO(1204): Funkce zařízení je vypnutá. Uživatel ji může znovu zapnout.|
|-2016344109|0x87D107D3|DCMO(1203): Funkce zařízení je vypnutá. Uživatel ji nemůže znovu zapnout.|
|-2016344110|0x87D107D2|DCMO(1202): Zapnutí proběhlo úspěšně, ale funkce zařízení je momentálně odpojená.|
|-2016344111|0xF3FB4D95|DCMO(1201): Zapnutí proběhlo úspěšně. Funkce zařízení je v současnosti připojená.|
|-2016344112|0x87D107D0|DCMO(1200): Operace probíhá úspěšně|
|-2016345595|0x87D10205|Syncml(517): Odpověď na atomický příkaz byla tak velká, že se nevešla do jedné zprávy.|
|-2016345596|0x87D10204|Syncml(516): Příkaz byl uvnitř elementu Atomic, a ten selhal. Příkaz se nepovedlo úspěšně vrátit zpátky.|
|-2016345598|0x87D10202|SyncML (514): příkaz SyncML se nedokončil úspěšně, protože operace byla zrušená před zpracováním příkazu.|
|-2016345599|0x87D10201|Syncml(513): Příjemce nepodporuje nebo odmítá podporovat určenou verzi synchronizačního protokolu SyncML použitou ve zprávě SyncML žádosti.|
|-2016345600|0x87D10200|Syncml(512): Při synchronizační relaci došlo k chybě aplikace.|
|-2016345601|0x87D101FF|Syncml(511): Při zpracování požadavku došlo na serveru k vážné chybě.|
|-2016345602|0x87D101FE|Syncml(510): Při zpracování žádosti došlo k chybě. Chyba se týká výpadku úložiště dat příjemce.|
|-2016345603|0x87D101FD|Syncml(509): Vyhrazené pro budoucí použití.|
|-2016345604|0x87D101FC|Syncml (508): Došlo k chybě, která vyžaduje obnovení aktuálního stavu synchronizace klienta se serverem.|
|-2016345605|0x87D101FB|Syncml(507): Chyba způsobila selhání všech příkazů protokolu SyncML v typu elementu Atomic.|
|-2016345606|0x87D101FA|Syncml(506): Při zpracování žádosti došlo k chybě aplikace.|
|-2016345607|0x87D101F9|Syncml(505): Příjemce nepodporuje nebo odmítá podporovat určenou verzi souboru DTD protokolu SyncML použitou ve zprávě SyncML žádosti.|
|-2016345608|=0x87D101F8|Syncml(504): Příjemce, který funguje jako brána nebo proxy, nedostal včas odpověď od nadřazeného příjemce určeného identifikátorem URI (např. HTTP, FTP, LDAP) nebo od jiného pomocného příjemce (třeba DNS). Odpověď potřeboval pro přístup, když se pokoušel dokončit žádost.|
|-2016345609|0x87D101F7|Syncml(503): Příjemce v současnosti nemůže žádost zpracovat. Příčinou je dočasné přetížení nebo údržba na straně příjemce.|
|-2016345610|0x87D101F6|Syncml(502): Příjemce, který funguje jako brána nebo proxy, nedostal platnou odpověď od nadřazeného příjemce, na kterého se obrátil při pokusu o splnění žádosti.|
|-2016345611|0x87D101F5|Syncml(501): Příjemce nepodporuje příkaz potřebný ke splnění žádosti.|
|-2016345612|0x87D101F4|Syncml(500): U příjemce vznikl nečekaně stav, který brání splnění žádosti.|
|-2016345684|0x87D101AC|Syncml(428): Přesun se nepodařil.|
|-2016345685|0x87D101AB|Syncml(427): Nadřazený objekt nejde odstranit, protože obsahuje podřízené položky.|
|-2016345686|0x87D101AA|Syncml(426): Dílčí položka není přijatá.|
|-2016345687|0x87D101A9|Syncml(425): Požadovaný příkaz nejde provést, protože odesílatel nemá u příjemce odpovídající oprávnění pro řízení přístupu (ACL).|
|-2016345688|0x87D101A8|Syncml(424): Objekt v bloku byl přijatý, ale velikost přijatého objektu neodpovídá velikosti deklarované v prvním bloku.|
|-2016345689|0x87D101A7|Syncml(423): Požadovaný příkaz nejde provést, protože „logicky odstraněná“ položka už byla předtím na serveru trvale odstraněná.|
|-2016345690|0x87D101A6|Syncml(422): Požadovaný příkaz nejde na serveru provést kvůli nesprávně vytvořenému skriptování CGI v LocURI.|
|-2016345691|0x87D101A5|Syncml(421): Požadovaný příkaz nejde na serveru provést, protože byla zadaná neznámá gramatika vyhledávání.|
|-2016345692|0x87D101A4|Syncml(420): Pro zbývající synchronizovaná data příjemce nemá další úložný prostor.|
|-2016345693|0x87D101A3|Syncml(419): Žádost klienta způsobila konflikt, který se vyřešil předností pro serverový příkaz.|
|-2016345694|0x87D101A2|Syncml(418): Požadovaný příkaz Put nebo Add nejde provést, protože cíl už existuje.|
|-2016345695|0x87D101A1|Syncml(417): Žádost v této chvíli nejde provést, ale původce ji může zopakovat později.|
|-2016345696|0x87D101A0|Syncml(416): Žádost nejde provést, protože je v ní uvedená nadměrná velikost v bajtech.|
|-2016345697|0x87D1019F|Syncml(415): Nepodporovaný typ nebo formát média|
|-2016345698|0x87D1019E|Syncml(414): Požadovaný příkaz nejde provést, protože cílový identifikátor URI je moc dlouhý na to, aby ho příjemce mohl nebo chtěl zpracovat.|
|-2016345699|0x87D1019D|Syncml(413): Příjemce odmítá provést požadovaný příkaz, protože požadovaná položka je větší, než příjemce může nebo chce zpracovat.|
|-2016345700|0x87D1019C|Syncml(412): Požadovaný příkaz se na straně příjemce nepodařilo provést, protože je neúplný nebo nesprávně vytvořený.|
|-2016345701|0x87D1019B|Syncml(411): Požadovaný příkaz musí doprovázet velikost v bajtech nebo informace o délce v typu elementu Meta.|
|-2016345702|0x87D1019A|Syncml(410): Požadovaný cíl už není u příjemce a není známý ani předávací identifikátor URI.|
|-2016345703|0x87D10199|Syncml(409): Žádost nebyla úspěšná, protože došlo ke konfliktu aktualizací mezi klientskou a serverovou verzí dat.|
|-2016345704|0x87D10198|Syncml(408): Očekávaná zpráva nebyla v požadované době přijatá.|
|-2016345705|0x87D10197|Syncml(407): Požadovaný příkaz nejde provést, protože původce nezajistil správné ověření.|
|-2016345706|0x87D10196|Syncml(406): Požadovaný příkaz nejde provést, protože volitelná funkce v žádosti nebyla podporovaná.|
|-2016345707|0x87D10195|Syncml(405): Požadovaný příkaz není v cíli dovolený.|
|-2016345708|0x87D10194|Syncml(404): Požadovaný cíl se nepovedlo najít.|
|-2016345709|0x87D10193|Syncml(403): Požadovaný příkaz nejde provést, i když mu příjemce rozumí.|
|-2016345710|0x87D10192|Syncml(402): Požadovaný příkaz nejde provést, protože je potřeba řádná platba.|
|-2016345711|0x87D10191|Syncml(401): Požadovaný příkaz nejde provést, protože žadatel nezajistil správné ověření.|
|-2016345712|0x87D10190|Syncml(400): Požadovaný příkaz nejde provést kvůli chybné syntaxi příkazu.|
|-2016345807|0x87D10131|Syncml(305): Přístup k požadovanému cíli je možný přes zadaný identifikátor URI proxy serveru.|
|-2016345808|0x87D10130|Syncml(304): Požadovaný příkaz SyncML se v cíli neprovedl.|
|-2016345809|0x87D1012F|Syncml(303): Požadovaný cíl byl nalezený na jiném identifikátoru URI.|
|-2016345810|0x87D1012E|Syncml(302): Požadovaný cíl se dočasně přesunul na jiný identifikátor URI.|
|-2016345811|0x87D1012D|Syncml(301): Požadovaný cíl má nový identifikátor URI.|
|-2016345812|0x87D1012C|Syncml(300): Požadovaný cíl je jedním z několika alternativních požadovaných cílů.|
|-2016345896|0x87D100D8|Syncml(216):Příkaz byl uvnitř elementu Atomic, a ten selhal. Příkaz je úspěšně vrácený zpět.|
|-2016345897|0x87D100D7|Syncml(215): Příkaz se neprovedl kvůli zásahu uživatele, který nepotvrdil volbu.|
|-2016345898|0x87D100D6|SyncML (214): operace se zrušila. Příkaz SyncML se úspěšně dokončil, ale v této relaci se další příkazy nezpracují.|
|-2016345899|0x87D100D5|Syncml(213): Položka v bloku je přijatá a uložená do vyrovnávací paměti.|
|-2016345900|0x87D100D4|Syncml(212): Ověření je přijaté. Zbytek synchronizační relace nevyžaduje další ověřování. Kód odpovědi jde použít jenom v odpovědi na žádost, ve které byly přihlašovací údaje poskytnuté.|
|-2016345901|0x87D100D3|Syncml(211): Položka není odstraněná. Požadovaná položka se nenašla. Možná se odstranila dřív.|
|-2016345902|0x87D100D2|Syncml(210): Odstranění bez archivace. Z odpovědi vyplývá, že požadovaná data se úspěšně odstranila, ale nearchivovala se předtím, protože implementace tuto VOLITELNOU funkci nepodporuje.|
|-2016345903|0x87D100D1|Konflikt se vyřešil vytvořením duplicitních dat. Z odpovědi vyplývá, že žádost způsobila aktualizační konflikt, který se vyřešil vytvořením duplicitních klientských dat v serverové databázi. Odpověď obsahuje cílový identifikátor URI duplicitních dat v položce stavu. V případě obousměrné synchronizace je navíc vrácený příkaz Add s definicí duplicitních dat.|
|-2016345904|0x87D100D0|Konflikt se vyřešil tím, že „vyhrál“ příkaz klienta. Z odpovědi vyplývá, že při aktualizaci došlo ke konfliktu, který se vyřešil vítězstvím příkazu klienta.|
|-2016345905|0x87D100CF|Konflikt se vyřešil sloučením. Z odpovědi vyplývá, že žádost vytvořila konflikt, který se vyřešil sloučením klientských a serverových instancí dat. Odpověď obsahuje v položce stavu zdrojové i cílové adresy URL. Se sloučenými daty je dál vrácený příkaz Replace.|
|-2016345906|0x87D100CE|Z odpovědi vyplývá, že je dokončená jenom část příkazu. Jestli může být zbytek příkazu dokončený později, tak při dokončení by se MĚL vytvořit další odpovídající stavový kód žádosti o dokončení.|
|-2016345907|0x87D100CD|Zdroj by MĚL aktualizovat obsah. Odesílatel požadavku dostane informaci o tom, ŽE BY MĚL synchronizovat obsah, aby získal aktuální verzi.|
|-2016345908|0x87D100CC|Žádost se úspěšně dokončila, ale nevrátila se žádná data. Když v cíli není obsah, vrátí se v reakci na příkaz Get kód odpovědi.|
|-2016345909|0x87D100CB|Nespolehlivá odpověď. Na žádost odpověděla jiná entita, než jaké byla určená. Odpověď se vrátí jenom tehdy, když důvěryhodný cíl vrátí na žádost kód odpovědi 200.|
|-2016345910|0x87D100CA|Přijaté ke zpracování. Žádost o vzdálené spuštění aplikace nebo o upozornění uživatele nebo aplikace se úspěšně provedla.|
|-2016345911|0x87D100C9|Požadovaná položka se přidala.|
|-2016345912|0x87D100C8|Příkaz SyncML se úspěšně dokončil.|
|-2016346011|0x87D10065|Zadaný příkaz SyncML se provádí, ale zatím není dokončený.|

## <a name="next-steps"></a>Další kroky

Obraťte se na podpora Microsoftu, abyste [získali podporu pro Microsoft Intune](get-support.md).
