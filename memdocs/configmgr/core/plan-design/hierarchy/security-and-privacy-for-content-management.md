---
title: Zabezpečení a ochrana osobních údajů ve správě obsahu
titleSuffix: Configuration Manager
description: Optimalizujte zabezpečení a ochranu osobních údajů pro správu obsahu v Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720853"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů při správě obsahu v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje informace o zabezpečení a ochraně osobních údajů při správě obsahu v nástroji Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Osvědčené postupy zabezpečení pro správu obsahu  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Výhody a nevýhody protokolu HTTPS nebo HTTP pro distribuční body intranetu
V případě distribučních bodů v intranetu zvažte výhody a nevýhody používání protokolu HTTPS a protokolu HTTP. Ve většině scénářů používá protokol HTTP a účty pro přístup k balíčkům pro autorizaci lepší zabezpečení než používání protokolu HTTPS s šifrováním, ale bez autorizace. Jsou-li však součástí obsahu citlivá data, která chcete při přenosu šifrovat, použijte protokol HTTPS.  

-   **Pokud používáte protokol HTTPS pro distribuční bod**, Configuration Manager nepoužívá k autorizaci přístupu k obsahu účty pro přístup k balíčkům, ale obsah je při přenosu v síti zašifrovaný.  

-   **Pokud pro distribuční bod použijete protokol HTTP**, můžete pro autorizaci použít účty pro přístup k balíčkům, ale obsah není při přenosu v síti zašifrovaný.  

Od verze 1806 zvažte povolení **Rozšířené protokolu HTTP** pro danou lokalitu. Tato funkce umožňuje klientům pomocí Azure Active Directory ověřování zabezpečeně komunikovat s distribučním bodem protokolu HTTP. Další informace najdete v tématu [Rozšířená http](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Ochrana souboru s certifikátem pro ověřování klientů
Používáte-li u distribučního bodu certifikát ověřování klienta PKI místo certifikátu podepsaného svým držitelem, chraňte soubor certifikátu (.pfx) silným heslem. Pokud soubor uložíte v síti, zabezpečte síťový kanál při importu souboru do Configuration Manager.

Pokud vyžadujete heslo k importu certifikátu ověřování klienta, který distribuční bod používá ke komunikaci s body správy, tato konfigurace pomáhá chránit certifikát před útočníkem. Použijte podepisování SMB (Server Message Block) nebo protokol IPsec mezi umístěním v síti a serverem lokality, abyste zabránili útočníkovi v manipulaci se souborem certifikátu.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Odebrání role distribučního bodu ze serveru lokality
Ve výchozím nastavení Configuration Manager instalační program nainstaluje distribuční bod na server lokality. Klienti nemusí komunikovat přímo se serverem lokality. Chcete-li omezit plochu pro útok, přiřaďte roli distribučního bodu jiným systémům lokality a odeberte ji ze serveru lokality.  

#### <a name="secure-content-at-the-package-access-level"></a>Zabezpečte obsah na úrovni přístupu k balíčku
Sdílená složka distribučního bodu umožňuje všem uživatelům přístup ke čtení. Chcete-li omezit přístup k obsahu jen na některé uživatele a je-li distribuční bod konfigurován pro protokol HTTP, můžete použít účty pro přístup k balíčkům. Tato konfigurace se nevztahuje na distribuční body cloudu, které nepodporují účty pro přístup k balíčkům. Další informace najdete v tématu [účty pro přístup k balíčkům](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Konfigurace služby IIS v roli distribučního bodu
Pokud Configuration Manager nainstaluje službu IIS při přidání role systému lokality distribučního bodu, odeberte po dokončení instalace distribučního bodu přesměrování protokolu HTTP nebo skripty a nástroje správy služby IIS. Distribuční bod nevyžaduje přesměrování protokolu HTTP nebo skripty a nástroje správy služby IIS. Chcete-li omezit plochu pro útok, odeberte tyto služby rolí pro roli webového serveru.  Další informace o službách rolí pro roli webového serveru u distribučních bodů najdete v tématu [požadavky na lokalitu a systém lokality](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Nastavení oprávnění k přístupu k balíčku při vytváření balíčku
Vzhledem k tomu, že změny účtů pro přístup k souborům balíčku budou platné pouze při opětovné distribuci balíčku, při prvním vytvoření balíčku Nastavte přístupová oprávnění k balíčku pečlivě. Tato konfigurace je důležitá, pokud je balíček rozsáhlý nebo distribuovaný do mnoha distribučních bodů a pokud je kapacita šířky pásma pro distribuci obsahu omezená.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementace ovládacích prvků přístupu pro ochranu médií obsahujících připravený obsah
Připravený obsah je komprimován, ale není šifrovaný. Útočník by mohl přečíst a změnit soubory stažené do zařízení. Configuration Manager klienti odmítnou obsah, který je porušen, ale pořád si ho stáhnou.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Import předem připraveného obsahu pomocí ExtractContent
Naimportujte předem připravený obsah pomocí nástroje příkazového řádku ExtractContent. exe. Chcete-li zabránit manipulaci a zvýšení oprávnění, používejte pouze autorizovaný nástroj příkazového řádku, který je součástí nástroje Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Zabezpečte komunikační kanál mezi serverem lokality a zdrojovým umístěním balíčku.
Při vytváření aplikací a balíčků použijte podepisování protokolu IPsec nebo SMB mezi serverem lokality a zdrojovým umístěním balíčku. Tato konfigurace pomáhá zabránit útočníkovi v manipulaci se zdrojovými soubory.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Odebrat výchozí virtuální adresáře pro vlastní web s rolí distribučního bodu
Pokud změníte možnost Konfigurace lokality tak, aby po instalaci role distribučního bodu používala vlastní web, a ne výchozí web, odeberte výchozí virtuální adresáře. Když přepnete z výchozího webu na vlastní web, Configuration Manager neodebere staré virtuální adresáře. Odeberte následující virtuální adresáře, které Configuration Manager původně vytvořené na výchozím webu:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>V případě distribučních bodů cloudu Chraňte svoje podrobnosti a certifikáty předplatného Azure.
Při použití distribučních bodů cloudu můžete chránit následující položky s vysokou hodnotou:
- Uživatelské jméno a heslo pro vaše předplatné Azure
- Certifikát pro správu Azure 
- Certifikát služby distribučního bodu cloudu

Certifikáty bezpečně uložte. Pokud k nim při konfiguraci distribučního bodu cloudu přejdete přes síť, použijte podepisování protokolu IPsec nebo SMB mezi serverem systému lokality a zdrojovým umístěním.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>V případě kontinuity služeb Sledujte datum vypršení platnosti certifikátů distribučního bodu cloudu.
Configuration Manager vás neupozorní, pokud se brzy vyprší platnost importovaných certifikátů pro distribuční bod cloudu. Monitorujte data vypršení platnosti nezávisle na Configuration Manager. Ujistěte se, že jste obnovili a pak importovali nové certifikáty před datem vypršení platnosti. Tato akce je důležitá, pokud získáváte certifikát ověřování serveru od externího poskytovatele veřejné, protože k získání obnoveného certifikátu může být potřeba další čas.  

 Pokud platnost certifikátu vyprší, nástroj Cloud Services Manager vygeneruje ID stavové zprávy **9425**. Soubor CloudMgr. log obsahuje položku, která označuje, že certifikát **je ve stavu vypršela**, datum vypršení platnosti se také zaznamenalo jako UTC.  



## <a name="security-considerations-for-content-management"></a>Aspekty zabezpečení pro správu obsahu  

Při plánování správy obsahu Vezměte v úvahu následující body:  

-   Klienti neověřují obsah do až po jeho stažení.  

     Configuration Manager klienti Ověřují hodnotu hash obsahu až po jeho stažení do mezipaměti klienta. Pokud útočník provede manipulaci se seznamem souborů ke stažení nebo obsahu samotného, proces stahování může zabrat značnou šířku pásma sítě, a to pouze v případě, že klient zahodí obsah, pokud nalezne neplatnou hodnotu hash.  

-   Pokud používáte distribuční body cloudu, přístup k obsahu je automaticky omezen na váš podnik. Nemůžete ho dál omezit na vybrané uživatele nebo skupiny.  

-   Při použití distribučních bodů cloudu jsou klienti ověřováni bodem správy a pak používají Configuration Manager token pro přístup k distribučním bodům cloudu. Token je platný po dobu osmi hodin. Toto chování znamená, že pokud klienta zablokujete, protože už není důvěryhodný, může pokračovat v stahování obsahu z distribučního bodu cloudu, dokud nevyprší doba platnosti tohoto tokenu. V tomto okamžiku bod správy nevydá pro klienta jiný token, protože klient je zablokován.  

     Pokud chcete blokovanému klientovi zabránit ve stahování obsahu v rámci tohoto osmi hodinového okna, zastavte cloudovou službu. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **distribuční body cloudu** .  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Ochrana osobních údajů při správě obsahu  

 Configuration Manager nezahrnuje žádná uživatelská data v souborech obsahu, i když se uživatel může rozhodnout pro tuto akci.  



## <a name="see-also"></a>Viz také

- [Základní koncepty správy obsahu](fundamental-concepts-for-content-management.md)  

- [Zabezpečení a ochrana osobních údajů pro správu aplikací](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Zabezpečení a ochrana osobních údajů pro aktualizace softwaru](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Zabezpečení a ochrana osobních údajů pro nasazení operačního systému](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
