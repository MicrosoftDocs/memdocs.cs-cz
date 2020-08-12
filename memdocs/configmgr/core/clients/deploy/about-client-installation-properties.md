---
title: Parametry a vlastnosti instalace klienta
titleSuffix: Configuration Manager
description: Přečtěte si o parametrech a vlastnostech příkazového řádku služby CCMSetup pro instalaci klienta Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d26be4d3e3381a80fcbaa547cfcc7a3b8db42f5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127014"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Informace o parametrech instalace a vlastnostech klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí příkazu CCMSetup.exe nainstalujte klienta Configuration Manager. Pokud zadáte *parametry* instalace klienta na příkazovém řádku, upraví se chování při instalaci. Pokud do příkazového řádku zadáte *vlastnosti* instalace klienta, upraví počáteční konfiguraci nainstalovaného agenta klienta.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a>O CCMSetup.exe

Příkaz CCMSetup.exe stáhne potřebné soubory pro instalaci klienta z bodu správy nebo ze zdrojového umístění. Tyto soubory mohou zahrnovat:  

- Balíček Instalační služba systému Windows client.msi, který nainstaluje klientský software.

- Požadavky klienta

- Aktualizace a opravy pro klienta Configuration Manager

> [!NOTE]
> Nemůžete přímo nainstalovat client.msi.  

CCMSetup.exe poskytuje *parametry* příkazového řádku pro přizpůsobení instalace. Parametry mají předponu lomítka ( `/` ) a jsou všeobecně malá. V případě potřeby určíte hodnotu parametru pomocí dvojtečky (), `:` a to hned za následováním hodnoty. Další informace najdete v tématu [CCMSetup.exe parametry příkazového řádku](#ccmsetupexe-command-line-parameters).

*Vlastnosti* můžete také uvést na příkazovém řádku CCMSetup.exe a upravit tak chování client.msi. Vlastnosti podle konvence jsou velkými písmeny. Zadejte hodnotu pro vlastnost pomocí znaku rovná se ( `=` ) ihned následovaný hodnotou. Další informace najdete v tématu [Client.msi Properties](#clientMsiProps).

> [!IMPORTANT]  
> Před zadáním vlastností pro client.msi zadejte parametry CCMSetup.  

CCMSetup.exe a podpůrné soubory jsou na serveru lokality ve složce **klienta** Configuration Manager instalační složky. Configuration Manager sdílí tuto složku do sítě ve sdílené složce lokality. Například, `\\SiteServer\SMS_ABC\Client`.

Příkaz CCMSetup.exe používá v příkazovém řádku tento formát:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Například:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Tento příklad provádí následující akce:  

- Určuje bod správy s názvem SMSMP01, který vyžádá seznam distribučních bodů pro stažení instalačních souborů klienta.  

- Určuje, že pokud na počítači už existuje verze klienta nástroje, instalace se zastaví.  

- Dá souboru client.msi pokyn, aby klienta přiřadil ke kódu lokality S01.  

- Dá souboru client.msi pokyn, aby použil záložní stavový bod s názvem SMSFP01.  

> [!TIP]  
> Pokud hodnota parametru obsahuje mezery, uzavřete ji do uvozovek.  

Pokud rozšíříte schéma služby Active Directory pro Configuration Manager, lokalita publikuje mnoho vlastností instalace klienta v Active Directory Domain Services. Configuration Manager klient tyto vlastnosti automaticky přečte. Další informace najdete v tématu [o vlastnostech instalace klienta publikovaných ve službě Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>Parametry příkazového řádku CCMSetup.exe

### <a name=""></a><a name="bkmk_help"></a> /?

Zobrazuje dostupné parametry příkazového řádku pro ccmsetup.exe.  

Příklad: `ccmsetup.exe /?`

### <a name="allowmetered"></a>/AllowMetered

<!--6976145-->

Počínaje verzí 2006 použijte tento parametr k řízení chování klienta v měřené síti. Tento parametr nepřijímá žádné hodnoty. Když povolíte komunikaci klienta v monitorovaných sítích pro CCMSetup, stáhne se obsah, zaregistruje se v lokalitě a stáhne počáteční zásady. Veškerá další komunikace klienta se řídí konfigurací nastavení klienta z těchto zásad. Další informace najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections).

Pokud klienta přeinstalujete na existující zařízení, použije se k určení jeho konfigurace tato priorita:

1. Existující zásady místních klientů
1. Poslední příkazový řádek uložený v registru Windows
1. Parametry na příkazovém řádku služby CCMSetup

### <a name="alwaysexcludeupgrade"></a>/AlwaysExcludeUpgrade

Tento parametr určuje, zda se má klient automaticky upgradovat, když povolíte [**Automatický upgrade klienta**](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Podporované hodnoty:

- `TRUE`: Klient nebude automaticky upgradován.
- `FALSE`: Klient se automaticky upgraduje (výchozí).

Například:  

`CCMSetup.exe /AlwaysExcludeUpgrade:TRUE`

Další informace najdete v tématu [Rozšířený klient interoperability](../../understand/interoperability-client.md).

> [!NOTE]  
> Při použití parametru **/AlwaysExcludeUpgrade** stále běží automatický upgrade. Pokud se ale pro provedení upgradu spustí program CCMSetup, Upozorňujeme, že se nastavil parametr **/AlwaysExcludeUpgrade** a v souboru **CCMSetup. log**se zaprotokoluje následující řádek:
>
> `Client is stamped with /alwaysexcludeupgrade. Stop proceeding.`
>
> Program CCMSetup pak okamžitě ukončí a neprovede upgrade.

### <a name="bitspriority"></a>/BITSPriority

Když zařízení stáhne instalační soubory klienta přes připojení HTTP, použijte tento parametr k určení priority stahování. Zadejte jednu z následujících možných hodnot:

- `FOREGROUND`

- `HIGH`

- `NORMAL`výchozí

- `LOW`

Příklad: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="config"></a>/config

Tento parametr určuje textový soubor se seznamem vlastností instalace klienta.

- Pokud je program CCMSetup spuštěn jako služba, umístěte tento soubor do systémové složky CCMSetup: `%Windir%\Ccmsetup` .

- Pokud zadáte parametr [**/noservice**](#noservice) , umístěte tento soubor do stejné složky jako CCMSetup.exe.

Příklad: `CCMSetup.exe /config:"configuration file name.txt"`

Chcete-li zadat správný formát souboru, použijte soubor **mobileclienttemplate. TCF** ve `\bin\<platform>` složce v instalačním adresáři Configuration Manager na serveru lokality. Tento soubor obsahuje komentáře k oddílům a jejich použití. Vlastnosti instalace klienta zadejte v `[Client Install]` části za následujícím textem: `Install=INSTALL=ALL` .

Příklad `[Client Install]` položky oddílu:`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="downloadtimeout"></a>/downloadtimeout

Pokud služba CCMSetup nedokáže stáhnout instalační soubory klienta, tento parametr určuje maximální časový limit v minutách. Po uplynutí tohoto časového limitu se program CCMSetup zastaví pokus o stažení instalačních souborů. Výchozí hodnota je **1440** minut (jeden den).

K určení intervalu mezi opakovanými pokusy použijte parametr [**/Retry**](#retry) .

Příklad: `ccmsetup.exe /downloadtimeout:100`

### <a name="excludefeatures"></a>/ExcludeFeatures

Tento parametr určuje, že CCMSetup.exe nenainstaluje zadanou funkci.

Příklad: `CCMSetup.exe /ExcludeFeatures:ClientUI` nenainstaluje na klienta Centrum softwaru.  

> [!NOTE]  
> `ClientUI`je jediná hodnota, kterou podporuje parametr **/ExcludeFeatures** .

### <a name="forceinstall"></a>/forceinstall

Určete, že CCMSetup.exe odinstaluje všechny existující klienty a nainstaluje nového klienta.  

### <a name="forcereboot"></a>/forcereboot

Tento parametr použijte k vynucení restartování počítače, pokud je to nutné pro dokončení instalace. Pokud tento parametr nezadáte, program CCMSetup ukončí, jakmile bude nutné restartovat počítač. Pak pokračuje po dalším ručním restartování.

Příklad: `CCMSetup.exe /forcereboot`

### <a name="logon"></a>/logon

Pokud je již nainstalována nějaká verze klienta, tento parametr určuje, zda má být instalace klienta zastavena.  

Příklad: `ccmsetup.exe /logon`  

### <a name="mp"></a>/MP

Určuje zdrojový bod správy, ke kterému se mají počítače připojit. Počítače používají tento bod správy k vyhledání nejbližšího distribučního bodu pro instalační soubory. Pokud nejsou k dispozici žádné distribuční body nebo počítač nemůže stáhnout soubory z distribučních bodů po čtyřech hodinách, stáhne soubory ze zadaného bodu správy.  

Další informace o tom, jak služba CCMSetup stahuje obsah, najdete v tématu [skupiny hranic – instalace klienta](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Tento článek obsahuje také podrobnosti o chování programu CCMSetup, pokud použijete parametry **/MP** a **/source** .

> [!IMPORTANT]  
> Tento parametr určuje počáteční bod správy pro počítače, které mají najít zdroj stahování, a může to být libovolný bod správy v libovolné lokalitě. Nepřiřazuje *assign* klienta k určenému bodu správy.

Počítače stahují soubory pomocí připojení HTTP nebo HTTPS podle konfigurace role systému lokality pro připojení klientů. Pokud ho nakonfigurujete, může stahování také používat omezení služby BITS. Pokud nakonfigurujete všechny distribuční body a body správy pouze pro připojení klientů pomocí protokolu HTTPS, ověřte, zda má klientský počítač platný klientský certifikát.  

K určení více než jednoho bodu správy můžete použít parametr příkazového řádku **/MP** . Pokud se počítač nepřipojí k prvnímu, pokusí se o další seznam v zadaném seznamu. Pokud zadáte více bodů správy, oddělte hodnoty středníky.

Pokud se klient připojuje k bodu správy pomocí protokolu HTTPS, zadejte plně kvalifikovaný název domény (FQDN) název počítače. Hodnota se musí shodovat s názvem **předmětu** nebo **alternativního názvu subjektu**certifikátu PKI bodu správy. I když Configuration Manager podporuje použití názvu počítače v certifikátu pro připojení na intranetu, doporučuje se použít plně kvalifikovaný název domény.

Příklad s názvem počítače:`ccmsetup.exe /mp:SMSMP01`  

Příklad s plně kvalifikovaným názvem domény:`ccmsetup.exe /mp:smsmp01.contoso.com`  

Tento parametr také umožňuje zadat adresu URL brány pro správu cloudu (CMG). Pomocí této adresy URL můžete nainstalovat klienta nástroje na internetové zařízení. Chcete-li získat hodnotu pro tento parametr, použijte následující postup:

- Vytvořte CMG. Další informace najdete v tématu [Nastavení CMG](../manage/cmg/setup-cloud-management-gateway.md).
- V aktivním klientovi otevřete příkazový řádek Windows PowerShellu jako správce.
- Spusťte následující příkaz:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Připojí `https://` předponu, která se použije s parametrem **/MP** .

Příklad, kdy použijete adresu URL brány pro správu cloudu:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Při zadání adresy URL brány pro správu cloudu pro parametr **/MP** musí začínat na `https://` .

### <a name="nocrlcheck"></a>/NoCRLCheck

Určuje, že klient by neměl kontrolovat seznam odvolaných certifikátů (CRL), když komunikuje přes protokol HTTPS s certifikátem PKI. Pokud tento parametr nezadáte, klient zkontroluje seznam CRL předtím, než vytvoří připojení HTTPS. Další informace o kontrole seznamu CRL klienta najdete v tématu [Plánování odvolání certifikátu PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Příklad: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="noservice"></a>/noservice

Tento parametr brání spuštění programu CCMSetup jako služby, což je ve výchozím nastavení. Když je program CCMSetup spuštěn jako služba, běží v kontextu účtu místního systému počítače. Tento účet nemusí mít dostatečná oprávnění pro přístup k požadovaným síťovým prostředkům pro instalaci. V **/noservice**se CCMSetup.exe spouští v kontextu uživatelského účtu, který používáte ke spuštění instalace.

Příklad: `ccmsetup.exe /noservice`  

### <a name="regtoken"></a>/regtoken

<!--5686290-->

Počínaje verzí 2002 použijte tento parametr k poskytnutí velkokapacitní registračního tokenu. Internetové zařízení používá tento token v procesu registrace prostřednictvím brány pro správu cloudu (CMG). Další informace najdete v tématu [ověřování založené na tokenech pro CMG](deploy-clients-cmg-token.md).

Pokud použijete tento parametr, zahrňte také následující parametry a vlastnosti:

- [**/MP**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

Následující příklad příkazového řádku obsahuje další požadované parametry a vlastnosti instalace:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Pokud se CCMSetup.exe nepovede stáhnout instalační soubory, použijte tento parametr k zadání intervalu opakování v minutách. Program CCMSetup se bude pokoušet opakovat, dokud nedosáhne limitu zadaného v parametru [**/downloadtimeout**](#downloadtimeout) .

Příklad: `ccmsetup.exe /retry:20`  

### <a name="service"></a>/service

Určuje, že má být program CCMSetup spuštěn jako služba, která používá účet místního systému.  

> [!TIP]
> Pokud používáte skript ke spuštění CCMSetup.exe s parametrem **/Service** , CCMSetup.exe po spuštění služby ukončen. Nemusí správně nahlásit podrobnosti o instalaci skriptu.

Příklad: `ccmsetup.exe /service`  

### <a name="skipprereq"></a>/skipprereq

Tento parametr určuje, že CCMSetup.exe neinstaluje určenou součást. Můžete zadat více než jednu hodnotu. `;`Jednotlivé hodnoty oddělte pomocí středníku ().

Příklady:

- `CCMSetup.exe /skipprereq:filename.exe`

- `CCMSetup.exe /skipprereq:filename1.exe;filename2.exe`

Další informace o požadavcích klienta najdete v tématu [požadavky klienta Windows](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="source"></a>/Source

Určuje umístění souboru ke stažení. Použijte místní cestu nebo cestu UNC. Zařízení stahuje soubory pomocí protokolu SMB (Server Message Block). Aby bylo možné používat **/source**, uživatelský účet systému Windows pro instalaci klienta potřebuje oprávnění **ke čtení** pro dané umístění.

Další informace o tom, jak služba CCMSetup stahuje obsah, najdete v tématu [skupiny hranic – instalace klienta](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Tento článek obsahuje také podrobnosti o chování programu CCMSetup, pokud použijete parametry **/MP** a **/source** .

> [!TIP]  
> Parametr **/source** lze použít více než jednou na příkazovém řádku pro určení alternativních umístění pro stahování.  

Příklad: `ccmsetup.exe /source:"\\server\share"`

### <a name="uninstall"></a>/uninstall

Tento parametr použijte k odinstalaci klienta Configuration Manager. Další informace najdete v tématu [odinstalace klienta](../manage/manage-clients.md#BKMK_UninstalClient).

Příklad: `ccmsetup.exe /uninstall`  

### <a name="usepkicert"></a>/UsePKICert

Zadejte tento parametr pro klienta, aby používal certifikát pro ověřování klientů PKI. Pokud tento parametr nezadáte, nebo pokud klient nenalezne platný certifikát, použije připojení HTTP s certifikátem podepsaným svým držitelem.

Příklad: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> V některých scénářích nemusíte tento parametr zadávat, ale stále používat klientský certifikát. Například nabízená instalace klienta a instalace klienta na základě aktualizace softwaru. Tento parametr použijte, když instalujete klienta ručně a použijete parametr **/MP** s bodem správy s POVOLENým protokolem HTTPS.
>
> Tento parametr zadejte také při instalaci klienta pro internetovou komunikaci. Použijte vlastnost **CCMALWAYSINF = 1** spolu s vlastnostmi pro internetový bod správy (**CCMHOSTNAME**) a kód lokality (**SMSSITECODE**). Další informace o internetové správě klientů najdete v tématu [požadavky na komunikaci klienta z Internetu nebo nedůvěryhodné doménové struktury](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a>Návratové kódy CCMSetup.exe

Příkaz CCMSetup.exe poskytuje následující návratové kódy. Chcete-li vyřešit potíže, přečtěte si `%WinDir%\ccmsetup\ccmsetup.log` v klientovi kontext a další podrobnosti o návratových kódech.

|Návratový kód|Význam|  
|-----------|-------|  
|0|Success|  
|6|Chyba|  
|7|Je vyžadován restart|  
|8|Instalace již byla spuštěna|  
|9|Selhání vyhodnocení požadavků|  
|10|Selhání ověření hodnoty hash manifestu instalačního programu|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a>Vlastnosti Ccmsetup.msi

Následující vlastnosti mohou změnit chování při instalaci ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Použijte tento program CCMSetup. vlastnost *MSI* k předání dalších parametrů a vlastností příkazového řádku do programu CCMSetup. *exe*. Zahrnutí dalších parametrů a vlastností uvnitř uvozovek ( `"` ). Tuto vlastnost použijte při spuštění klienta Configuration Manager s [metodou instalace Intune MDM](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Příklad: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune omezuje příkazový řádek na 1024 znaků.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a>Vlastnosti Client.msi

Následující vlastnosti mohou změnit chování při instalaci client.msi, které ccmsetup.exe nainstalovat. Pokud používáte [metodu nabízené instalace klienta](plan/client-installation-methods.md#client-push-installation), určete tyto vlastnosti na kartě **klient** **vlastností klientské nabízené instalace** v konzole Configuration Manager.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Určuje identifikátor aplikace klienta Azure Active Directory (Azure AD). Klientskou aplikaci můžete vytvořit nebo importovat při [konfiguraci služeb Azure](../../servers/deploy/configure/azure-services-wizard.md) pro správu cloudu. Správce Azure může získat hodnotu této vlastnosti z Azure Portal. Další informace najdete v tématu [získání ID aplikace](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Pro vlastnost **AADCLIENTAPPID** je toto ID aplikace pro typ **nativní** aplikace.

Příklad: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Určuje identifikátor aplikace serveru Azure AD. Serverovou aplikaci můžete vytvořit nebo importovat při [konfiguraci služeb Azure](../../servers/deploy/configure/azure-services-wizard.md) pro správu cloudu. Když vytváříte aplikaci serveru, v okně vytvořit serverová aplikace je tato vlastnost **identifikátor URI ID aplikace**.

Správce Azure může získat hodnotu této vlastnosti z Azure Portal. V **Azure Active Directory**Najděte serverovou aplikaci v části **Registrace aplikací**. Vyhledejte typ aplikace **Webová aplikace/rozhraní API**. Otevřete aplikaci, vyberte **Nastavení**a pak vyberte **vlastnosti**. Pro tuto vlastnost instalace klienta **AADRESOURCEURI** použijte hodnotu **identifikátoru URI ID aplikace** .

Příklad: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Určuje identifikátor tenanta Azure AD. Při [konfiguraci služeb Azure](../../servers/deploy/configure/azure-services-wizard.md) pro správu cloudu Configuration Manager odkazy na tohoto tenanta. Pro získání hodnoty pro tuto vlastnost použijte následující postup:

- Na zařízení s Windows 10, které je připojené ke stejnému tenantovi služby Azure AD, otevřete příkazový řádek.
- Spusťte následující příkaz:`dsregcmd.exe /status`
- V části stav zařízení vyhledejte hodnotu **TenantId** . Například `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`.

  > [!Note]
  > Správce Azure může tuto hodnotu také získat v Azure Portal. Další informace najdete v tématu [získání ID tenanta](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Příklad: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Určuje jeden nebo více uživatelských účtů nebo skupin systému Windows, kterým bude poskytnut přístup k nastavení klienta a zásadám. Tato vlastnost je užitečná, pokud nemáte pověření místního správce v klientském počítači. Zadejte seznam účtů, které jsou odděleny středníky ( `;` ).

Příklad: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

V případě potřeby nechte počítač po instalaci klienta tiše restartovat.

> [!IMPORTANT]  
> Při použití této vlastnosti se počítač bez upozornění restartuje. K tomuto chování dochází i v případě, že je uživatel přihlášený k Windows.

Příklad: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Chcete-li určit, že je klient vždy na internetu a nikdy se nepřipojuje k intranetu, nastavte tuto vlastnost na hodnotu `1` . U typu připojení klienta se zobrazí hodnota **Vždy v síti Internet**.  

Tato vlastnost s [**CCMHOSTNAME**](#ccmhostname) slouží k určení plně kvalifikovaného názvu domény internetového bodu správy. Použijte ji také s parametrem CCMSetup [**/UsePKICert**](#usepkicert) a kódem lokality ([**SMSSITECODE**](#smssitecode)).

Další informace o internetové správě klientů najdete v tématu [požadavky na komunikaci klienta z Internetu nebo nedůvěryhodné doménové struktury](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Příklad: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Pomocí této vlastnosti lze zadat seznam vystavitelů certifikátů. Tento seznam obsahuje informace o certifikátech důvěryhodných kořenových certifikačních autorit (CA), které jsou vztahem k Configuration Manager lokalitě.  

Tato hodnota rozlišuje malá a velká písmena pro atributy subjektu, které jsou v kořenovém certifikátu certifikační autority. Jednotlivé atributy oddělujte čárkou ( `,` ) nebo středníkem ( `;` ). Zadejte více než jeden kořenový certifikát certifikační autority pomocí oddělovacího panelu ( `|` ).

Příklad: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Použijte hodnotu atributu **Nastavení CertificateIssuers** v souboru **MobileClient. TCF** pro daný web. Tento soubor je v `\bin\<platform>` podsložce instalačního adresáře Configuration Manager na serveru lokality.

Další informace o seznamu vydavatelů certifikátů a jeho použití klienty během procesu výběru certifikátu najdete v tématu [plánování výběru klientského certifikátu PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Pokud má klient více než jeden certifikát pro komunikaci pomocí protokolu HTTPS, tato vlastnost určuje kritéria pro výběr platného certifikátu ověřování klienta.

K vyhledání názvu subjektu certifikátu nebo alternativního názvu předmětu použijte následující klíčová slova:

- **Subject**: najít přesnou shodu
- **SubjectStr**: najít částečnou shodu

Příklady:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: Vyhledejte certifikát s přesnou shodou názvu počítače `computer1.contoso.com` v názvu subjektu nebo v alternativním názvu subjektu.

- `CCMCERTSEL="SubjectStr:contoso.com"`: Vyhledejte certifikát, který se nachází `contoso.com` v názvu subjektu nebo v alternativním názvu subjektu.

Pomocí klíčového slova **SubjectAttr** vyhledejte atributy identifikátoru objektu (OID) nebo rozlišující název v poli název subjektu nebo alternativní název předmětu.

Příklady:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Vyhledejte atribut organizační jednotky vyjádřený jako identifikátor objektu a pojmenovaný `Computers` .

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Vyhledejte atribut organizační jednotky vyjádřený jako rozlišující název a pojmenujte `Computers` .

> [!IMPORTANT]
> Pokud použijete název subjektu, klíčové slovo **Subject** rozlišuje velká a malá písmena a klíčové slovo **SubjectStr** nerozlišuje malá a velká písmena.
>
> Pokud použijete alternativní název subjektu, rozlišují se malá a velká písmena v obou **předmětech** a klíčovém slově **SubjectStr** .

Úplný seznam atributů, které můžete použít pro výběr certifikátu, najdete v tématu [podporované hodnoty atributů pro kritéria výběru certifikátu PKI](#BKMK_attributevalues).

Pokud hledání odpovídá více než jeden certifikát a nastavili jste [**CCMFIRSTCERT**](#ccmfirstcert) na `1` , pak instalační program klienta vybere certifikát s nejdelší dobou platnosti.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Pokud instalační program klienta nemůže najít platný certifikát ve výchozím **osobním** úložišti certifikátů pro daný počítač, použijte tuto vlastnost k určení alternativního názvu úložiště certifikátů.

Příklad: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Tato vlastnost povoluje protokolování ladění při instalaci klienta. Tato vlastnost způsobí, že klient bude protokolovat informace nízké úrovně pro řešení potíží. Nepoužívejte tuto vlastnost v produkčních lokalitách. Může dojít k nadměrnému protokolování, které by mohlo ztížit nalezení relevantních informací v souborech protokolu. Povolit také [**CCMENABLELOGGING**](#ccmenablelogging).

Podporované hodnoty:

- `0`: Vypnout protokolování ladění (výchozí)
- `1`: Zapnout protokolování ladění

Příklad: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Další informace najdete v tématu [informace o souborech protokolu](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager umožňuje protokolování ve výchozím nastavení.

Podporované hodnoty:

- `TRUE`: Zapnout protokolování (výchozí)
- `FALSE`: Vypnout protokolování

Příklad: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Další informace najdete v tématu [informace o souborech protokolu](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

Frekvence v minutách, kdy se spustí nástroj pro vyhodnocení stavu klienta (ccmeval.exe). Zadejte celočíselnou hodnotu z hodnoty `1` do `1440` . Ve výchozím nastavení se ccmeval spustí jednou denně (1440 minut).

Příklad: `CCMSetup.exe CCMEVALINTERVAL=1440`

Další informace o vyhodnocení stavu klienta najdete v tématu [monitorování klientů](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

Hodina během dne, kdy se nástroj pro vyhodnocení stavu klienta (ccmeval.exe) spouští. Zadejte celočíselnou hodnotu od `0` (půlnoc) do `23` (11:00 odp). Ve výchozím nastavení se ccmeval spouští na půlnoci.

Další informace o vyhodnocení stavu klienta najdete v tématu [monitorování klientů](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Pokud tuto vlastnost nastavíte na `1` , klient vybere certifikát PKI s nejdelší dobou platnosti.

Příklad: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Pokud je klient spravován přes Internet, tato vlastnost určuje plně kvalifikovaný název domény internetového bodu správy.  

Nezadávejte tuto možnost společně s vlastností instalace **SMSSITECODE = auto**. Přímé přiřazení internetových klientů k internetovému webu.

Příklad: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Tato vlastnost může určovat adresu brány pro správu cloudu (CMG). Pro získání hodnoty pro tuto vlastnost použijte následující postup:

- Vytvořte CMG. Další informace najdete v tématu [Nastavení CMG](../manage/cmg/setup-cloud-management-gateway.md).
- V aktivním klientovi otevřete příkazový řádek Windows PowerShellu jako správce.
- Spusťte následující příkaz:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Použijte vrácenou hodnotu jako-je s vlastností **CCMHOSTNAME** .

Příklad: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Pokud zadáte adresu CMG pro vlastnost **CCMHOSTNAME** , nepřipojujte předponu, například `https://` . Tuto předponu použijte pouze s adresou URL **/MP** CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Určuje port, který má klient použít při komunikaci přes protokol HTTP se servery systému lokality. Ve výchozím nastavení je tato hodnota `80` .

Příklad: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Určuje port, který má klient použít při komunikaci přes protokol HTTPS se servery systému lokality. Ve výchozím nastavení je tato hodnota `443` .

Příklad: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Tato vlastnost slouží k nastavení složky pro instalaci Configuration Manager klientských souborů. Ve výchozím nastavení používá `%WinDir%\CCM` .

> [!TIP]
> Bez ohledu na to, kam nainstalujete soubory klienta, vždy nainstaluje soubor **ccmcore.dll** do `%WinDir%\System32` složky. V 64 operačním systému nainstaluje kopii ccmcore.dll do `%WinDir%\SysWOW64` složky. Tento soubor podporuje 32 aplikací, které používají 32 verzi klientských rozhraní API ze sady Configuration Manager SDK.

Příklad: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Tato vlastnost slouží k určení úrovně podrobností pro zápis do souborů protokolu Configuration Manager.

Podporované hodnoty:

- `0`: Verbose
- `1`: Výchozí
- `2`: Upozornění a chyby
- `3`: Pouze chyby

Příklad: `CCMSetup.exe CCMLOGLEVEL=0`

Další informace najdete v tématu [informace o souborech protokolu](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Když soubor protokolu Configuration Manager dosáhne maximální velikosti, klient ho přejmenuje jako zálohu a vytvoří nový soubor protokolu. Tato vlastnost určuje, kolik předchozích verzí souboru protokolu bude zachováno. Výchozí hodnota je `1`. Pokud nastavíte hodnotu na `0` , klient nebude uchovávat žádnou historii souborů protokolu.

Příklad: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Další informace najdete v tématu [informace o souborech protokolu](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Tato vlastnost určuje maximální velikost souboru protokolu v bajtech. Když protokol naroste do zadané velikosti, klient ho přejmenuje do souboru historie a vytvoří nový. Výchozí velikost je 250 000 bajtů a minimální velikost je 10 000 bajtů.

Příklad: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300 000 bajtů)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Nastavte tuto vlastnost na `TRUE` , chcete-li zablokovat správcům změnu přiřazené lokality v ovládacím panelu Configuration Manager.

Příklad: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Pokud je tato vlastnost nastavená na TRUE, zakáže správcům měnit nastavení složky mezipaměti klienta v Ovládacích panelech **Configuration Manager** .  

Příklad: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Zadejte doménu DNS pro klienty pro vyhledání bodů správy, které publikujete v DNS. Když klient vyhledá bod správy, informuje klienta o dalších bodech správy v hierarchii. Toto chování znamená, že bod správy, který klient najde z DNS, může být libovolný v hierarchii.

> [!NOTE]
> Tuto vlastnost nemusíte určovat, pokud je klient ve stejné doméně jako publikovaný bod správy. V takovém případě se doména klienta automaticky používá k hledání DNS pro body správy.

Další informace o publikování DNS jako metody umístění služby pro klienty Configuration Manager najdete v části [umístění služby a jak klienti zjišťují přiřazený bod správy](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> Ve výchozím nastavení Configuration Manager nepovoluje publikování DNS.

Příklad: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Zadejte záložní stavový bod, který obdrží a zpracuje zprávy o stavu odeslané Configuration Manager klienty.

Další informace najdete v tématu [určení, zda potřebujete bod stavu pro použití náhradní lokality](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).

Příklad: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Pokud nastavíte tuto vlastnost na `TRUE` , instalační služba klienta nekontroluje minimální požadovanou verzi Microsoft Application Virtualization (App-V).

> [!IMPORTANT]  
> Pokud instalujete klienta Configuration Manager bez instalace sady App-V, nebudete moci [nasadit virtuální aplikace](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Příklad: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Když tuto vlastnost povolíte, klient hlásí stav, ale neopraví problémy, které najde.

Příklad: `CCMSetup.exe NOTIFYONLY=TRUE`

Další informace najdete v tématu [Postup konfigurace stavu klienta](configure-client-status.md).

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

Počínaje verzí 2002 můžete pomocí této vlastnosti spustit pořadí úkolů na klientovi po úspěšné registraci v lokalitě.

> [!NOTE]
> Pokud pořadí úkolů nainstaluje aktualizace softwaru nebo aplikace, klienti potřebují platný certifikát pro ověřování klientů. Samotný ověřovací token nefunguje. Další informace najdete v tématu [poznámky k verzi – nasazení operačního systému](../../servers/deploy/install/release-notes.md#os-deployment).<!--7527072-->
      
Můžete třeba zřídit nové zařízení s Windows 10 pomocí automatického pilotního projektu Windows, automaticky ho zapsat do Microsoft Intune a pak nainstalovat klienta Configuration Manager pro spolusprávu. Pokud zadáte tuto novou možnost, nově zřízený klient pak spustí pořadí úkolů. Tento proces poskytuje větší flexibilitu při instalaci aplikací a aktualizací softwaru nebo konfiguraci nastavení.


Použijte následující postup:

1. [Vytvořte pořadí úkolů nasazení mimo operační systém](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) , které nainstaluje aplikace, nainstaluje aktualizace softwaru a nakonfiguruje nastavení.

1. [Nasaďte toto pořadí úloh](../../../osd/deploy-use/deploy-a-task-sequence.md) do nové předdefinované kolekce, **všechna zřizovací zařízení**. Poznamenejte si ID nasazení pořadí úloh, například `PRI20001` .

1. Do zařízení [nainstalujte klienta Configuration Manager](deploy-clients-to-windows-computers.md#BKMK_Manual) a zahrňte následující vlastnost: `PROVISIONTS=PRI20001` . Nastavte hodnotu této vlastnosti jako ID nasazení pořadí úloh.

    - Pokud instalujete klienta nástroje z Intune během registrace spolusprávy, přečtěte si téma [Příprava internetových zařízení pro spolusprávu](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Tato metoda může mít další požadavky. Například zápis lokality do Azure Active Directory nebo vytvoření brány pro správu cloudu s povoleným obsahem.

Po instalaci a správné registraci klienta s lokalitou se spustí odkazované pořadí úkolů. Pokud se registrace klienta nezdařila, pořadí úkolů se nespustí.



### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Pokud má klient chybný Configuration Manager důvěryhodný kořenový klíč, nemůže kontaktovat důvěryhodný bod správy, aby získal nový důvěryhodný kořenový klíč. Tuto vlastnost použijte k odebrání starého důvěryhodného kořenového klíče. K této situaci může dojít, když přesunete klienta z jedné hierarchie lokality do jiné. Tato vlastnost se vztahuje na klienty, kteří používají komunikaci na základě protokolu HTTP nebo HTTPS. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Příklad: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Povoluje automatické opětovné přiřazení lokality pro upgrady klientů při použití s [SMSSITECODE = auto](#smssitecode).

Příklad: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Určuje umístění složky mezipaměti klienta v klientském počítači. Ve výchozím nastavení je umístění mezipaměti `%WinDir%\ccmcache` .

Příklad: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Tuto vlastnost s vlastností [**SMSCACHEFLAGS**](#smscacheflags) použijte k řízení umístění složky mezipaměti klienta. Například pro instalaci složky mezipaměti klienta na největší dostupnou diskovou jednotku klienta:`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Tato vlastnost slouží k určení dalších podrobností instalace složky mezipaměti klienta. Vlastnosti **SMSCACHEFLAGS** můžete použít samostatně nebo v kombinaci oddělené středníky ( `;` ).

Pokud tuto vlastnost nezadáte:

- Klient nainstaluje složku mezipaměti podle vlastnosti [**SMSCACHEDIR**](#smscachedir) .
- Složka není komprimovaná.
- Klient používá vlastnost [**SMSCACHESIZE**](#smscachesize) jako omezení velikosti v MB mezipaměti.

Když upgradujete stávajícího klienta, instalační služba klienta tuto vlastnost ignoruje.

#### <a name="values-for-the-smscacheflags-property"></a>Hodnoty pro vlastnost SMSCACHEFLAGS

- **Vlastností PERCENTDISKSPACE**: nastavte velikost mezipaměti jako procentuální hodnotu *celkového* místa na disku. Pokud zadáte tuto vlastnost, nastavte také [**SMSCACHESIZE**](#smscachesize) na hodnotu procent.

- **PERCENTFREEDISKSPACE**: nastavte velikost mezipaměti jako procento *volného* místa na disku. Pokud zadáte tuto vlastnost, nastavte také [**SMSCACHESIZE**](#smscachesize) jako procentuální hodnotu. Například disk má 10 MB volného místa a zadáte `SMSCACHESIZE=50` . Instalační program klienta nastaví velikost mezipaměti na 5 MB. Tuto vlastnost nelze použít s vlastností **vlastností PERCENTDISKSPACE** .

- **MAXDRIVE**: Nainstalujte mezipaměť na největší dostupný disk. Pokud zadáte cestu s vlastností [**SMSCACHEDIR**](#smscachedir) , instalační služba klienta tuto hodnotu ignoruje.

- **MAXDRIVESPACE**: Nainstalujte mezipaměť na diskovou jednotku s největším množstvím volného místa. Pokud zadáte cestu s vlastností [**SMSCACHEDIR**](#smscachedir) , instalační služba klienta tuto hodnotu ignoruje.

- **NTFSONLY**: Nainstalujte mezipaměť jenom na diskovou jednotku formátovanou systémem souborů NTFS. Pokud zadáte cestu s vlastností [**SMSCACHEDIR**](#smscachedir) , instalační služba klienta tuto hodnotu ignoruje.

- **Komprimace**: uložte mezipaměť do komprimovaného formátu.

- **FAILIFNOSPACE**: Pokud není k dispozici dostatek místa pro instalaci mezipaměti, odeberte klienta Configuration Manager.

Příklad: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Nastavení klienta jsou k dispozici pro zadání velikosti složky mezipaměti klienta. Díky přidání tohoto nastavení klienta už není potřeba k určení velikosti mezipaměti klienta používat vlastnost programu client.msi SMSCACHESIZE. Další informace o najdete v tématu o [nastavení velikosti mezipaměti v klientovi](about-client-settings.md#client-cache-settings).  

Když upgradujete stávajícího klienta, instalační program klienta toto nastavení ignoruje. Klient také ignoruje velikost mezipaměti při stahování aktualizací softwaru.

Příklad: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Pokud přeinstalujete klienta, nemůžete použít **SMSCACHESIZE** nebo **SMSCACHEFLAGS** k nastavení velikosti mezipaměti, aby byla menší než dříve. Předchozí velikost je minimální hodnota.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Tato vlastnost slouží k určení umístění a pořadí, ve kterém Instalační program klienta kontroluje nastavení konfigurace. Jedná se o řetězec jednoho nebo více znaků, z nichž každý definuje konkrétní zdroj konfigurace:

- `R`: Projděte si konfigurační nastavení v registru.

  Další informace najdete v tématu [zřízení vlastností klientské instalace](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: Ověřte nastavení konfigurace ve vlastnostech instalace z příkazového řádku.

- `M`: Projděte si existující nastavení při upgradu staršího klienta.

- `U`: Upgradujte nainstalovaného klienta na novější verzi a použijte přiřazený kód lokality.

Ve výchozím nastavení používá instalační program klienta `PU` . Nejprve zkontroluje vlastnosti instalace ( `P` ) a pak existující nastavení ( `U` ).  

Příklad: `CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

Určuje, zda klient může používat službu Windows Internet Name Service (WINS) k hledání bodu správy, který přijímá připojení protokolu HTTP. Klienti používají tuto metodu, když nemohou najít bod správy v Active Directory Domain Services nebo v DNS.

Tato vlastnost nemá vliv na to, zda klient používá službu WINS pro rozlišení názvu.

U této vlastnosti můžete provést konfiguraci dvou odlišných režimů:

- **Služba WINS**: Tato hodnota je nejbezpečnější nastavení pro tuto vlastnost. Zabrání klientům najít bod správy ve službě WINS. Pokud použijete toto nastavení, musí mít klienti alternativní metodu pro vyhledání bodu správy v intranetu. Například Active Directory Domain Services nebo publikování DNS.

- **WINSSECURE** (výchozí): v tomto režimu může klient, který používá komunikaci pomocí protokolu HTTP, použít službu WINS k nalezení bodu správy. Klient však musí obsahovat kopii důvěryhodného kořenového klíče, než ho bude možné úspěšně připojit do bodu správy. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Příklad: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Určuje počáteční bod správy, který má klient Configuration Manager použít.  

> [!IMPORTANT]  
> Pokud bod správy akceptuje pouze připojení klientů přes protokol HTTPS, použijte předponu názvu bodu správy pomocí `https://` .

Příklady:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Pokud klient nemůže získat Configuration Manager důvěryhodný kořenový klíč od Active Directory Domain Services, použijte k zadání klíče tuto vlastnost. Tato vlastnost se vztahuje na klienty, kteří používají komunikaci pomocí protokolu HTTP a HTTPS. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Příklad: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Získá hodnotu důvěryhodného kořenového klíče webu ze souboru mobileclient. TCF na serveru lokality. Další informace najdete v tématu [předběžné poskytnutí důvěryhodného kořenového klíče klientovi pomocí souboru](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Tuto vlastnost použijte k přeinstalování Configuration Manager důvěryhodného kořenového klíče. Určuje úplnou cestu a název souboru, který obsahuje důvěryhodný kořenový klíč. Tato vlastnost se vztahuje na klienty, kteří používají komunikaci na základě protokolu HTTP nebo HTTPS. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Příklad: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Určuje úplnou cestu a název exportovaného certifikátu podepsaného svým držitelem na serveru lokality. Server lokality uloží tento certifikát do úložiště certifikátů **SMS** . Má název subjektu **Server lokality** a popisný název **podpisový certifikát serveru lokality**.

Příklad: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Tato vlastnost určuje lokalitu Configuration Manager, ke které přiřadíte klienta. Tato hodnota může být buď kód lokality o třech znacích, nebo slovo `AUTO` . Pokud zadáte `AUTO` nebo nezadáte tuto vlastnost, klient se pokusí určit přiřazení lokality z Active Directory Domain Services nebo ze zadaného bodu správy. Pokud chcete povolit `AUTO` upgrady klientů, nastavte také [SITEREASSIGN = true](#sitereassign).

> [!NOTE]  
> Pokud zadáte také internetový bod správy s vlastností [**CCMHOSTNAME**](#ccmhostname) , nepoužívejte `AUTO` s **SMSSITECODE**. Přímo přiřaďte klienta ke svému webu zadáním kódu lokality.

Příklad: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a>Hodnoty atributů pro kritéria výběru certifikátu

Configuration Manager podporuje následující hodnoty atributu pro kritéria výběru certifikátu PKI:

|Atribut OID|Atribut s rozlišujícím názvem|Definice atributu|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Součást domény|  
|1.2.840.113549.1.9.1|E nebo e-mail|E-mailová adresa|  
|2.5.4.3|CN|Běžný název|  
|2.5.4.4|SN|Název předmětu|  
|2.5.4.5|SERIALNUMBER|Sériové číslo|  
|2.5.4.6|C|Kód země|  
|2.5.4.7|L|Lokalita|  
|2.5.4.8|S nebo ST|Název státu nebo oblasti|  
|2.5.4.9|STREET|Ulice a číslo|  
|2.5.4.10|O|Název organizace|  
|2.5.4.11|OU|Organizační jednotka|  
|2.5.4.12|T nebo Title|Nadpis|  
|2.5.4.42|G nebo GN nebo GivenName|Křestní jméno|  
|2.5.4.43|I nebo Initials|Iniciály|  
|2.5.29.17|(žádná hodnota)|Alternativní název subjektu|  
