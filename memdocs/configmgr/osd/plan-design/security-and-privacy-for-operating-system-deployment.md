---
title: Zabezpečení a ochrana osobních údajů pro nasazení operačního systému
titleSuffix: Configuration Manager
description: Seznamte se s osvědčenými postupy zabezpečení a ochrany osobních údajů pro nasazení operačního systému v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724423"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro nasazení operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje informace o zabezpečení a ochraně osobních údajů pro funkci nasazení operačního systému v Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a>Osvědčené postupy zabezpečení pro nasazení operačního systému  

Při nasazení operačních systémů pomocí Configuration Manager použijte následující osvědčené postupy zabezpečení:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementujte řízení přístupu, čímž ochráníte spouštěcí média.

Pokud vytvoříte spouštěcí média, vždy přiřaďte heslo, které vám pomůže média zabezpečit. I s heslem šifruje jenom soubory, které obsahují citlivé informace, a všechny soubory je možné přepsat.  

Řiďte fyzický přístup k médiím, čímž zabráníte útočníkovi v použití kryptografického útoku za účelem získání certifikátu ověřování klienta.  

Aby se zabránilo klientovi v instalaci obsahu nebo zásad klienta, se kterými se manipulovalo, použije se u obsahu hodnota hash a obsah se musí použít s původní zásadou. Pokud se hodnota hash obsahu nezdařila nebo je zkontrolováno, že obsah odpovídá zásadám, klient nebude používat spouštěcí médium. Pouze obsah se vyhodnotí jako hash. Tato zásada není vytvořená pomocí algoritmu hash, ale při zadání hesla je šifrovaná a zabezpečená. Díky tomuto chování může útočník obtížně zásadu úspěšně změnit.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Při vytváření médií pro image operačního systému použít zabezpečené umístění

Pokud mají k umístění přístup neoprávnění uživatelé, mohou manipulovat se soubory, které vytvoříte. Můžou také využívat veškeré dostupné místo na disku, aby se nepodařilo vytvořit médium.  


### <a name="protect-certificate-files"></a>Ochrana souborů certifikátů 

Chraňte soubory certifikátu (. pfx) pomocí silného hesla. Pokud je uložíte v síti, zabezpečte síťový kanál při jejich importu do Configuration Manager

Pokud pro import certifikátu ověřování klienta, který používáte pro spouštěcí médium, požadujete heslo, tato konfigurace pomáhá chránit certifikát před útočníkem.  

Pro komunikaci mezi umístěním v síti a serverem lokality použijte podepisování SMB nebo protokol IPsec. Zabráníte tak případnému útočníkovi v manipulaci se souborem certifikátu.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Blokování nebo odvolání jakýchkoli ohrožených certifikátů 

Pokud dojde k ohrožení bezpečnosti certifikátu klienta, zablokujte certifikát z Configuration Manager. Pokud se jedná o certifikát PKI, Odvolejte ho.  

Chcete-li nasadit operační systém pomocí spouštěcích médií a spouštění PXE, musíte mít certifikát ověřování klienta se soukromým klíčem. Pokud dojde k ohrožení bezpečnosti tohoto certifikátu, zablokujte certifikát v uzlu **Certifikáty** v pracovním prostoru **Správa**, uzel **Zabezpečení**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Zabezpečte komunikační kanál mezi serverem lokality a poskytovatelem služby SMS.

Když je poskytovatel serveru SMS vzdálený od serveru lokality, zabezpečte komunikační kanál pro ochranu spouštěcích imagí.

Když upravíte spouštěcí image a na serveru, který není serverem lokality, je spuštěný poskytovatel serveru SMS, jsou spouštěcí bitové kopie zranitelné vůči útokům. Pomocí podepisování SMS nebo protokolu IPsec ochraňte síťový kanál mezi těmito počítači.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Povolte komunikaci klientů pomocí PXE v distribučních bodech pouze v zabezpečených segmentech sítě.

Když klient odešle požadavek na spuštění pomocí technologie PXE, nemáte žádný způsob, jak zajistit, aby se požadavek aktivoval pomocí platného distribučního bodu s povoleným PXE. Tento scénář nese následující rizika zabezpečení:  

- Podvodný distribuční bod, který odpoví na požadavek PXE, by mohl klientům poskytnout zmanipulovanou bitovou kopii.  

- Útočník by mohl zahájit útok prostředníkem proti protokolu TFTP, který je používán technologií PXE. Tento útok by mohl odeslat škodlivý kód se soubory operačního systému. Útočník by taky mohl vytvořit podvodného klienta, který přímo do distribučního bodu provede požadavky TFTP.  

- Útočník by mohl použít škodlivého klienta ke spuštění útoku proti distribučnímu bodu s cílem odepření služeb.  

K ochraně síťových segmentů, ve kterých klienti přistupují k distribučním bodům s povoleným PXE, použijte důkladnou obranu.  

> [!WARNING]  
>  Z důvodu těchto rizik zabezpečení nepovolujte komunikaci pomocí technologie PXE distribuční bod, pokud je v nedůvěryhodné síti, jako je hraniční síť.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Nakonfigurujte distribuční body s povoleným PXE, aby odpovídaly na požadavky PXE pouze v určených síťových rozhraních.  

Pokud ve všech síťových rozhraních povolíte distribučnímu bodu, aby odpovídal na požadavky PXE, může tato konfigurace odhalit službu PXE nedůvěryhodným sítím.  


### <a name="require-a-password-to-pxe-boot"></a>Požadujte heslo při spouštění PXE.

Když pro spuštění pomocí technologie PXE požadujete heslo, přidá tato konfigurace další úroveň zabezpečení procesu spouštění PXE. Tato konfigurace pomáhá chránit před neautorizovanými klienty, kteří se připojují k Configuration Manager hierarchii.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Omezení obsahu v bitových kopiích operačního systému používaných pro spouštění pomocí technologie PXE nebo vícesměrové vysílání

Nezahrnovat obchodní aplikace nebo software obsahující citlivá data v imagi, kterou používáte pro spouštění pomocí technologie PXE nebo vícesměrové vysílání.  

Z důvodu základních rizik zabezpečení při spouštění pomocí technologie PXE a vícesměrového vysílání snížíte riziko, pokud počítač stáhne bitovou kopii operačního systému z neautorizovaných počítačů.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Omezení obsahu nainstalovaného pomocí proměnných pořadí úkolů

Do balíčků aplikací, které nainstalujete pomocí proměnných pořadí úloh, nezahrnujte obchodní aplikace nebo software obsahující citlivá data.  

Když nasadíte software pomocí proměnných pořadí úloh, může být nainstalován do počítačů a uživatelům, kteří nemají oprávnění k přijetí tohoto softwaru.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Zabezpečte síťový kanál při migraci stavu uživatele

Při migraci stavu uživatele Zabezpečte síťový kanál mezi klientem a bodem migrace stavu pomocí podepisování SMB nebo protokolu IPsec.  

Po úvodním připojení prostřednictvím protokolu HTTP se migrovaná data o stavu uživatele přenesou pomocí protokolu SMB. Pokud nezabezpečte síťový kanál, může útočník tato data přečíst a změnit.  


### <a name="use-the-latest-version-of-usmt"></a>Použijte nejnovější verzi nástroje USMT.

Použijte nejnovější verzi Nástroj pro migraci uživatelských souborů a nastavení (USMT), kterou Configuration Manager podporuje.  

Nejnovější verze nástroje USMT zajistí vylepšení zabezpečení a větší kontrolu v případě migrování dat o stavu uživatele.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Ručně odstranit složky v místech migrace stavu, když je vyřadíte z provozu  

Když odeberete složku bodu migrace stavu v konzole Configuration Manager ve vlastnostech bodu migrace stavu, lokalita neodstraní fyzickou složku. Chcete-li chránit data migrace stavu uživatele před zpřístupněním informací, odstraňte ručně sdílenou síťovou složku a odstraňte ji.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Nekonfigurujte zásadu odstraňování tak, aby okamžitě odstranila stav uživatele.  

Pokud nakonfigurujete zásadu odstraňování v bodu migrace stavu tak, aby okamžitě odstranila data, která jsou označená k odstranění, a pokud útočník načetl data o stavu uživatele před platným počítačem, lokalita okamžitě odstraní data o stavu uživatele. Nastavte dostatečnou délku intervalu **Odstranit po**, čímž ověříte úspěšné obnovení dat o stavu uživatele.  


### <a name="manually-delete-computer-associations"></a>Ruční odstranění přidružení počítačů 

Ručně odstranit přidružení počítačů, když je obnovení dat migrace stavu uživatele dokončeno a ověřeno.

Configuration Manager neodstraní automaticky přidružení počítačů. Chraňte identitu dat o stavu uživatele ručním odstraněním přidružení počítačů, která již nejsou vyžadována.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Zálohujte ručně migrovaná data o stavu uživatele v bodě migrace stavu.  

Configuration Manager Backup nezahrnuje data migrace stavu uživatele v záloze lokality.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementujte řízení přístupu, čímž ochráníte předzpracovaná média.  

Řiďte fyzický přístup k médiím, čímž zabráníte útočníkovi v použití kryptografického útoku za účelem získání certifikátu ověřování klienta a citlivých dat.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementujte řízení přístupu, čímž ochráníte proces vytváření bitové kopie v referenčním počítači.  

Ujistěte se, že referenční počítač, který používáte k zachycení imagí operačního systému, je v zabezpečeném prostředí. Použijte odpovídající ovládací prvky přístupu, aby nedošlo k neočekávanému nebo škodlivému softwaru, a nechtěně zahrnuté do zaznamenané bitové kopie. Když zachytíte image, ujistěte se, že je umístění cílové sítě zabezpečené. Tento proces pomáhá zajistit, aby image po jejím zachycení nemohla být úmyslně poškozená.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Do referenčního počítače vždy nainstalujte nejnovější aktualizace zabezpečení.  

Pokud jsou v referenčním počítači nové aktualizace zabezpečení, je omezeno okno zranitelnosti nových počítačů při jejich prvním spuštění.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementovat řízení přístupu při nasazení operačního systému do neznámého počítače

Pokud je nutné nasadit operační systém do neznámého počítače, implementujte řízení přístupu, čímž zabráníte neoprávněným počítačům v připojení k síti.  

Zřizování neznámých počítačů představuje pohodlný způsob nasazení nových počítačů na vyžádání. Ale může také umožnit útočníkovi, aby se efektivně stal důvěryhodným klientem v síti. Omezte fyzický přístup k síti a monitorujte klienty, čímž zjistíte neoprávněné počítače. 

Počítače, které reagují na nasazení operačního systému inicializované technologií PXE, můžou mít během procesu zničená všechna data. Toto chování může způsobit ztrátu dostupnosti systémů, které jsou neúmyslně přeformátovány.  


### <a name="enable-encryption-for-multicast-packages"></a>Povolte šifrování balíčků pro vícesměrové vysílání.  

U každého balíčku pro nasazení operačního systému můžete povolit šifrování, když Configuration Manager přenos balíčku pomocí vícesměrového vysílání. Tato konfigurace pomáhá zabránit neautorizovaným počítačům v připojení k relaci vícesměrového vysílání. Pomáhá také zabránit útočníkům v manipulaci s přenosem.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Monitorujte neoprávněné distribuční body s povoleným vícesměrovým vysíláním.  

Pokud útočníci získají přístup k síti, můžou nakonfigurovat neautorizovaný server vícesměrového vysílání pro nasazení operačního systému s falešnou identitou.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Pokud exportujete pořadí úloh do umístění v síti, zabezpečte umístění a síťový kanál.

Omezte přístup k síťové složce neoprávněným uživatelům.  

Pro komunikaci mezi umístěním v síti a serverem lokality použijte podepisování SMB nebo protokol IPsec. Zabráníte tak případnému útočníkovi v manipulaci s pořadím exportovaných úloh.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Pokud používáte účet Spustit jako pořadí úloh, proveďte další bezpečnostní opatření.

Pokud použijete [účet Spustit jako pořadí úloh](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account), proveďte následující kroky:  

- Použijte účet s nejmenšími možnými oprávněními.  

- Pro tento účet nepoužívejte účet pro přístup k síti.  

- Nikdy neudělujte účtu správcovství domény.  

- Nikdy nekonfigurujte profily roamingu pro tento účet. Když je pořadí úloh spuštěno, stáhne profil roamingu pro účet, což ponechá profil pro přístup k místnímu počítači.  

- Omezte rozsah účtu. Vytvořte například různé účty spuštění pořadí úloh jako pro každé pořadí úloh. Pokud dojde k ohrožení bezpečnosti jednoho účtu, budou ohroženy pouze klientské počítače, ke kterým má tento účet přístup. Pokud příkazový řádek vyžaduje k počítači oprávnění správce, zvažte vytvoření místního účtu správce výhradně pro účet Spustit jako pořadí úloh. Vytvořte tento místní účet na všech počítačích, které spouští pořadí úkolů, a pak účet odstraňte, jakmile už není potřeba.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Omezit a monitorovat administrativní uživatele, kterým je udělena role zabezpečení Správce nasazení operačního systému

Administrativní uživatelé, kterým je udělena role zabezpečení **Správce nasazení operačního systému** , mohou vytvořit certifikáty podepsané svým držitelem. Tyto certifikáty pak můžete použít k zosobnění klienta a získání zásad klienta z Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Použití rozšířeného protokolu HTTP k omezení nutnosti účtu přístupu k síti

Od verze 1806 když povolíte [Rozšířené protokol HTTP](../../core/plan-design/hierarchy/enhanced-http.md), několik scénářů nasazení operačního systému nevyžaduje účet pro přístup k síti ke stažení obsahu z distribučního bodu. Další informace najdete v tématu [sekvence úloh a účet přístupu k síti](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problémy se zabezpečením při nasazení operačního systému  

I když nasazení operačního systému může být pohodlný způsob, jak nasadit nejbezpečnější operační systémy a konfigurace pro počítače ve vaší síti, má následující bezpečnostní rizika:  


### <a name="information-disclosure-and-denial-of-service"></a>Zpřístupnění informací a odepření služby  

Pokud může útočník získat kontrolu nad Configuration Manager infrastruktuře, mohl by spustit jakékoli pořadí úloh. Tento proces může zahrnovat formátování pevných disků všech klientských počítačů. Pořadí úloh lze nakonfigurovat, aby obsahovala citlivé informace, například účty s oprávněním pro připojení k doméně a multilicenční klíče.  


### <a name="impersonation-and-elevation-of-privileges"></a>Zosobnění a zvýšení oprávnění  

Pořadí úloh mohou připojit počítač k doméně, což může zajistit podvodnému počítači ověřený přístup k síti. 

Chraňte certifikát ověřování klienta, který se používá pro spouštěcí médium pořadí úkolů a pro nasazení spuštění pomocí technologie PXE. Když zachytíte certifikát ověřování klienta, tento proces poskytne útočníkovi možnost získat privátní klíč v certifikátu. Tento certifikát umožňuje zosobnit platného klienta v síti. V takovém případě může podvodný počítač stáhnout zásadu, která obsahuje citlivá data.  

Pokud klienti používají účet přístupu k síti pro přístup k datům uloženým v bodu migrace stavu, tito klienti efektivně sdílejí stejnou identitu. Mohou přistupovat k datům migrace stavu z jiného klienta, který používá účet pro přístup k síti. Data jsou šifrovaná, takže je může číst pouze původní klient, avšak lze je úmyslně poškodit nebo je odstranit.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Ověřování klientů do bodu migrace stavu se dosahuje pomocí Configuration Manager tokenu, který je vydaný bodem správy.  

Configuration Manager neomezuje ani nespravuje množství dat, která jsou uložená v bodu migrace stavu. Útočník by mohl zaplnit dostupné místo na disku a způsobit odepření služby.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Používáte-li proměnné kolekce, mohou místní správci číst potenciálně citlivé informace.  

I když proměnné kolekce nabízejí flexibilní metodu pro nasazení operačních systémů, může tato funkce způsobit zpřístupnění informací.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a>Informace o ochraně osobních údajů pro nasazení operačního systému  

Kromě nasazení operačního systému do počítačů bez jednoho Configuration Manager lze použít k migraci souborů a nastavení uživatelů z jednoho počítače do druhého. Správce nakonfiguruje, které informace se mají přenášet, včetně souborů osobních dat, nastavení konfigurace a souborů cookie prohlížeče.  

Configuration Manager ukládá informace do bodu migrace stavu a zašifruje je během přenosu a úložiště. Uložené informace mohou získat pouze nový počítač přidružený k informacím o stavu. Pokud nový počítač ztratí klíč pro načtení informací, správce Configuration Manager s oprávněním **Zobrazit informace o obnovení** v objektech instance přidružení počítače může získat přístup k informacím a přidružit je k novému počítači. Jakmile nový počítač obnoví informace o stavu, po jednom dni ve výchozím nastavení data odstraní. Můžete nakonfigurovat, kdy bod migrace stavu odebere data označená k odstranění. Configuration Manager neukládá informace o stavu migrace do databáze lokality a neodesílá je do společnosti Microsoft.  

Použijete-li spouštěcí médium k nasazení bitových kopií operačního systému, používejte vždy výchozí možnost k ochraně spouštěcího média heslem. Heslo zašifruje všechny proměnné uložené v pořadí úkolů, ale všechny informace neuložené v této proměnné mohou být zranitelné v důsledku zpřístupnění.  

Nasazení operačního systému může používat pořadí úkolů k provedení mnoha různých úkolů během procesu nasazení, který zahrnuje instalaci aplikací a aktualizací softwaru. Když nakonfigurujete pořadí úkolů, měli byste si být vědomi také dopadů instalace softwaru na ochranu osobních údajů.  

Configuration Manager neimplementuje nasazení operačního systému ve výchozím nastavení. Před shromažďováním informací o stavu uživatele nebo vytváření pořadí úkolů nebo spouštěcích imagí vyžaduje několik kroků konfigurace.  

Před konfigurací nasazení operačního systému zvažte své požadavky na ochranu osobních údajů.  



## <a name="see-also"></a>Viz také

[Data o využití a diagnostika](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Zabezpečení a ochrana osobních údajů v nástroji Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
