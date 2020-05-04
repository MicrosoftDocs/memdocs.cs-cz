---
title: Nasazení klientů do systému Windows
titleSuffix: Configuration Manager
description: Naučte se nasadit klienta Configuration Manager do počítačů se systémem Windows.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07c5488b0ea28f37f7f8a07b532c67fb64aad810
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713426"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Postup nasazení klientů na počítače se systémem Windows v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek poskytuje podrobné informace o tom, jak nasadit klienta Configuration Manager do počítačů se systémem Windows. Další informace o plánování a přípravě nasazení klientů najdete v těchto článcích:

- [Metody instalace klienta](plan/client-installation-methods.md)  
- [Požadavky pro nasazení klientů do počítačů s Windows](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](plan/security-and-privacy-for-clients.md)  
- [Osvědčené postupy nasazení klientů](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a>Klientská nabízená instalace

Existují tři hlavní způsoby použití nabízených oznámení klienta:  

- Když nakonfigurujete nabízenou instalaci klienta pro lokalitu, instalace klienta se automaticky spustí na počítačích, které lokalita zjistí. Tato metoda je vymezená na hranice nakonfigurovaných lokalitou, když jsou tato hranice nakonfigurovaná jako skupina hranic.  

- Spusťte nabízenou instalaci klienta spuštěním Průvodce nabízenou instalací klienta pro konkrétní kolekci nebo prostředek v rámci kolekce.  

- Pomocí Průvodce nabízenou instalací klienta nainstalujte klienta Configuration Manager, který můžete použít k [dotazování](../../servers/manage/introduction-to-queries.md) výsledku. Instalace bude úspěšná pouze v případě, že jedna z položek vrácených dotazem je atribut **ResourceID** třídy **systémového prostředku** .

Pokud se server lokality nemůže připojit ke klientskému počítači nebo spustit proces instalace, automaticky zopakuje instalaci každou hodinu. Server se i nadále opakuje po dobu až sedmi dnů.  

Chcete-li sledovat proces instalace klientů, nainstalujte záložní stavový bod před instalací klientů. Při instalaci záložního stavového bodu je automaticky přiřazen klientům, pokud jsou nainstalovány metodou nabízené instalace klienta. Chcete-li sledovat průběh instalace klienta, Prohlédněte si sestavy nasazení a přiřazení klientů.

Soubory protokolů klienta poskytují podrobnější informace pro řešení potíží. Soubory protokolu nevyžadují bod záložního stavu. Například soubor CCM. log na serveru lokality zaznamenává všechny problémy, ke kterým dojde, když se server lokality připojí k počítači. Soubor CCMSetup. log v klientovi zaznamenává proces instalace.  

> [!IMPORTANT]  
> Klientská nabízená oznámení se zdaří jenom v případě, že jsou splněné všechny požadavky. Další informace najdete v tématu [závislosti metod instalace](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Nakonfigurovat lokalitu tak, aby automaticky používala pro zjištěné počítače klientskou nabízenou instalací

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte lokalitu, pro kterou chcete nastavit automatickou klientskou nabízenou instalaci pro všechny lokality.  

3. Na kartě **Domů** na pásu karet ve skupině **Nastavení** vyberte **nastavení instalace klienta**a potom vyberte **klientská nabízená instalace**.  

4. Na kartě **obecné** okno Vlastnosti klientské nabízené instalaci vyberte možnost **Povolit automatickou nabízenou instalaci klienta v rámci lokality**.

5. Pokud při aktualizaci lokality začíná verze 1806, je povolena kontrolu protokolu Kerberos pro nabízenou registraci klienta. Ve výchozím nastavení je povolená možnost **Povolit pro použití sekundárního připojení protokolem NTLM** , což odpovídá předchozímu chování. Pokud lokalita nemůže ověřit klienta pomocí protokolu Kerberos, pokusí se znovu připojit pomocí protokolu NTLM. Doporučená konfigurace pro zlepšení zabezpečení je zakázat toto nastavení, které vyžaduje protokol Kerberos bez použití protokolu NTLM Fallback.<!--1358204-->  

    > [!NOTE]  
    > Pokud nástroj používá nabízenou instalaci klienta k instalaci klienta Configuration Manager, server lokality vytvoří vzdálené připojení ke klientovi. Počínaje verzí 1806 může lokalita vyžadovat vzájemné ověřování protokolem Kerberos tím, že před vytvořením připojení nepovolí použití protokolu NTLM pro ověřování. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem.  
    >
    > V závislosti na zásadách zabezpečení může vaše prostředí už vyžadovat nebo vyžadovat protokol Kerberos přes starší ověřování NTLM. Další informace o bezpečnostních faktorech těchto ověřovacích protokolů najdete v tématu o [nastavení zásad zabezpečení systému Windows k omezení protokolu NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Aby bylo možné tuto funkci používat, musí být klienti v důvěryhodné doménové struktuře služby Active Directory. Protokol Kerberos v systému Windows spoléhá na vzájemné ověřování ve službě Active Directory.  

6. Vyberte typy systému, do kterých má Configuration Manager nabízet klientský software. Vyberte, zda chcete klienta nainstalovat na řadiče domény.  

7. Na kartě **účty** zadejte alespoň jeden účet, který má Configuration Manager použít při připojení k cílovému počítači. Vyberte ikonu **vytvořit** , zadejte **uživatelské jméno** a **heslo** (maximálně 38 znaků), potvrďte heslo a pak vyberte **OK**. Zadejte alespoň jeden účet klientské nabízené instalace. Tento účet musí mít oprávnění místního správce pro cílový počítač pro instalaci klienta. Pokud nezadáte účet klientské nabízené instalace, Configuration Manager se pokusí použít účet počítače systému lokality. Při použití účtu počítače systému lokality dojde k chybě při nabízení klienta mezi doménami.  

    > [!NOTE]  
    > Chcete-li použít klientskou nabízenou kopii ze sekundární lokality, zadejte účet v sekundární lokalitě, která iniciuje nabízenou kopii klienta.  
    >
    > Další informace o účtu klientské nabízené instalace najdete v dalším postupu [pomocí Průvodce nabízenou instalací klienta](#use-the-client-push-installation-wizard).  

8. Na kartě **vlastnosti instalace** zadejte všechny požadované vlastnosti instalace.

    Pokud jste rozšířili schéma služby Active Directory pro Configuration Manager, lokalita publikuje zadané [vlastnosti instalace klienta](about-client-installation-properties.md) na Active Directory Domain Services. Pokud je program CCMSetup spuštěn bez vlastností instalace, přečte tyto vlastnosti ze služby Active Directory.  

    > [!NOTE]  
    > Pokud povolíte klientskou nabízenou instalaci v sekundární lokalitě, nastavte vlastnost **SMSSITECODE** na kód lokality jeho nadřazené primární lokality na Configuration Manager. Pokud jste rozšířili schéma služby Active Directory pro Configuration Manager, aby bylo automaticky Nalezeno správné přiřazení lokality, nastavte tuto vlastnost na hodnotu **automaticky**.

### <a name="use-the-client-push-installation-wizard"></a>Použití Průvodce nabízenou instalací klienta

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte lokalitu, pro kterou chcete nastavit automatickou klientskou nabízenou instalaci pro všechny lokality.  

3. Na kartě **Domů** na pásu karet ve skupině **Nastavení** vyberte **nastavení instalace klienta**a potom vyberte **klientská nabízená instalace**.  

4. Na kartě **vlastnosti instalace** zadejte všechny požadované vlastnosti instalace.  

    Pokud jste rozšířili schéma služby Active Directory pro Configuration Manager, lokalita publikuje zadané [vlastnosti instalace klienta](about-client-installation-properties.md) na Active Directory Domain Services. Pokud je program CCMSetup spuštěn bez vlastností instalace, přečte tyto vlastnosti ze služby Active Directory.

5. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** .  

6. V uzlu **zařízení** vyberte jeden nebo více počítačů. Nebo vyberte kolekci počítačů v uzlu **kolekce zařízení** .  

7. Na kartě **Domů** na pásu karet vyberte jednu z následujících možností:  

    - Chcete-li klienta odeslat do jednoho nebo více zařízení, ve skupině **zařízení** vyberte možnost **instalovat klienta**.  

    - Pokud chcete klienta nabídnout do kolekce zařízení, ve skupině **kolekce** vyberte **instalovat klienta**.  

8. Na stránce **než začnete** v průvodci instalací Configuration Manager klienta zkontrolujte informace a pak vyberte **Další**.  

9. Na stránce **Možnosti instalace** vyberte příslušné možnosti.  

10. Zkontrolujte nastavení instalace a pak dokončete průvodce.  

> [!NOTE]  
> Tento průvodce použijte k instalaci klientů i v případě, že lokalita není nakonfigurovaná na nabízenou instalaci klienta.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a>Instalace na základě aktualizace softwaru  

Instalace klienta na základě aktualizace softwaru publikuje klienta nástroje v bodu aktualizace softwaru jako aktualizaci softwaru. Tuto metodu použijte při první instalaci nebo upgradu.  

Pokud je klient Configuration Manager nainstalován v počítači, počítač obdrží z lokality zásady klienta. Tato zásada zahrnuje název serveru a port aktualizace softwaru, ze kterého se mají získat aktualizace softwaru.

> [!IMPORTANT]  
> Pro instalaci na základě aktualizace softwaru použijte stejný server Windows Server Update Services (WSUS) pro instalaci klienta a aktualizace softwaru. Tento server musí být aktivním bodem aktualizace softwaru v primární lokalitě. Další informace najdete v tématu [instalace bodu aktualizace softwaru](../../../sum/get-started/install-a-software-update-point.md).

Pokud klient Configuration Manager není nainstalován v počítači, nakonfigurujte a přiřaďte objekt Zásady skupiny. Zásady skupiny určuje název serveru bodu aktualizace softwaru.  

Do instalace klienta na základě aktualizace softwaru nelze přidat vlastnosti příkazového řádku. Pokud jste rozšířili schéma služby Active Directory pro Configuration Manager, instalace klienta se automaticky dotazuje Active Directory Domain Services vlastností instalace.  

Pokud jste schéma služby Active Directory nerozšířili, použijte Zásady skupiny ke zřízení nastavení instalace klienta. Tato nastavení se automaticky aplikují na jakoukoli instalaci klienta na základě aktualizace softwaru. Další informace najdete v části o tom, [jak zřídit vlastnosti instalace klienta](#BKMK_Provision) a článek o tom, [jak přiřadit klienty k lokalitě](assign-clients-to-a-site.md)nástroje.  

Následující postupy použijte ke konfiguraci počítačů bez klienta Configuration Manager pro použití bodu aktualizace softwaru. K dispozici je také postup publikování klientského softwaru do bodu aktualizace softwaru.  

> [!TIP]  
> Pokud jsou počítače ve stavu čeká na restartování po předchozí instalaci softwaru, může instalace klienta na základě aktualizace softwaru způsobit, že se počítač restartuje.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Konfigurace objektu Zásady skupiny k určení bodu aktualizace softwaru  

1. Pomocí **Konzola pro správu zásad skupiny** otevřete nový nebo existující objekt Zásady skupiny.  

2. Rozbalte položku **Konfigurace počítače**, **šablony pro správu**a **součásti systému Windows**a poté vyberte možnost **web Windows Update**.  

3. Otevřete vlastnosti nastavení **určit umístění intranetového služby Microsoft Update**a pak vyberte **povoleno**.  

4. **Nastavte intranetovou aktualizační službu pro zjišťování aktualizací**: zadejte název a port serveru bodu aktualizace softwaru.  

    - Pokud jste nakonfigurovali Configuration Manager systém lokality tak, aby používal plně kvalifikovaný název domény (FQDN), použijte tento formát.  

    - Pokud není systém lokality Configuration Manager nakonfigurovaný tak, aby používal plně kvalifikovaný název domény, použijte formát krátkého názvu.

    > [!TIP]  
    > Číslo portu zjistíte v tématu [Určení nastavení portu používaného službou WSUS](../../../sum/plan-design/plan-for-software-updates.md).

    Příklad ve formátu plně kvalifikovaného názvu domény:`http://server1.contoso.com:8530`  

5. **Nastavte intranetový server pro statistiku**: Toto nastavení se obvykle nakonfiguruje se stejným názvem serveru.

6. Přiřaďte objekt Zásady skupiny počítačům, na kterých chcete nainstalovat klienta a získávat aktualizace softwaru.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publikování klienta Configuration Manager do bodu aktualizace softwaru  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte lokalitu, pro kterou chcete nakonfigurovat instalaci klienta na základě aktualizace softwaru.  

3. Na kartě **Domů** na pásu karet ve skupině **Nastavení** vyberte **nastavení instalace klienta**a potom vyberte možnost **instalace klienta na základě aktualizace softwaru**.  

4. Vyberte **Povolit instalaci klienta na základě aktualizace softwaru**.  

5. Pokud je verze klienta webu novější než verze v bodě aktualizace softwaru, otevře se dialogové okno **novější verze klientského balíčku** , které se zjistilo. Pokud chcete publikovat nejnovější verzi, vyberte **Ano** .  

    > [!NOTE]  
    > Pokud jste ještě nepublikovali klientský software do bodu aktualizace softwaru, toto dialogové okno je prázdné.

Aktualizace softwaru pro klienta Configuration Manager není aktualizována automaticky, pokud je k dispozici nová verze. Když aktualizujete lokalitu, opakujte tento postup pro aktualizaci klienta.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a>Instalace Zásady skupiny

K publikování nebo přiřazení Configuration Manager klienta použijte Zásady skupiny v Active Directory Domain Services. Klient se nainstaluje při spuštění počítače. Když použijete Zásady skupiny, klient se zobrazí v okně **Přidat nebo odebrat programy** v Ovládacích panelech. Uživatel ho může nainstalovat odsud.  

Pro instalace na základě Zásady skupiny použijte balíček Instalační služba systému Windows CCMSetup. msi. Tento soubor se nachází ve `<ConfigMgr installation directory>\bin\i386` složce na serveru lokality. Do tohoto souboru nemůžete přidat vlastnosti, abyste mohli změnit chování při instalaci.  

> [!IMPORTANT]  
> Pro přístup k instalačním souborům klienta musíte mít oprávnění správce.  

- Pokud jste rozšířili schéma služby Active Directory pro Configuration Manager a vybrali jste doménu na kartě **publikování** v dialogovém okně **vlastnosti lokality** , klientské počítače automaticky vyhledají vlastnosti instalace Active Directory Domain Services. Další informace najdete v tématu [o vlastnostech instalace klienta publikovaných na Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

- Pokud jste schéma služby Active Directory nerozšířili, přečtěte si část o [zřizování vlastností instalace klienta](#BKMK_Provision) , kde najdete informace o ukládání vlastností instalace v registru počítačů s Windows. Klient při instalaci nástroje používá tyto vlastnosti instalace.  

Další informace najdete v tématu [použití zásady skupiny k vzdálené instalaci softwaru](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a>Ruční instalace

Ručně nainstalujte klientský software do počítačů pomocí programu CCMSetup. exe. Tento program a jeho podpůrné soubory můžete najít ve složce Client v instalační složce nástroje Configuration Manager na serveru lokality. Lokalita sdílí tuto složku do sítě jako:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>`je název serveru primární lokality. `<site code>`je kód primární lokality, ke které je klient přiřazen. Chcete-li spustit program CCMSetup. exe z příkazového řádku na klientovi, připojte se k tomuto umístění v síti a pak příkaz spusťte.  

> [!IMPORTANT]  
> Pro přístup k instalačním souborům klienta musíte mít oprávnění správce.  

Program CCMSetup. exe zkopíruje všechny nezbytné požadavky do klientského počítače a zavolá balíček Instalační služba systému Windows (Client. msi), který nainstaluje klienta. Soubor Client. msi nelze spustit přímo.  

Chcete-li upravit chování instalace klienta, zadejte parametry příkazového řádku pro soubor CCMSetup. exe i Client. msi. Ujistěte se, že zadáte parametry CCMSetup, které `/` začínají předtím, než zadáte vlastnosti Client. msi. Příklad:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

V tomto příkladu se klient nainstaluje s následujícími možnostmi:  

|Možnost|Popis|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Tento parametr CCMSetup určuje bod správy SMSMP01 ke stažení požadovaných instalačních souborů klienta.|  
|`/logon`|Tento parametr CCMSetup určuje, že pokud se v počítači najde existující klient Configuration Manager, instalace by se měla zastavit.|  
|`SMSSITECODE=AUTO`|Tato vlastnost Client. msi určuje, že se klient pokusí najít Configuration Manager kód lokality, který se má použít, například pomocí Active Directory Domain Services.|  
|`FSP=SMSFP01`|Vlastnost Client. msi určuje, že záložní stavový bod s názvem SMSFP01 slouží k přijímání stavových zpráv odeslaných z klientského počítače.|  

Další informace najdete v tématu [informace o parametrech instalace a vlastnostech klienta](about-client-installation-properties.md).  

> [!TIP]  
> Postup pro instalaci klienta Configuration Manager na moderní zařízení s Windows 10 pomocí identity Azure Active Directory (Azure AD) najdete v tématu [instalace a přiřazení Configuration Manager klientů s Windows 10 pomocí Azure AD pro ověřování](deploy-clients-cmg-azure.md). Tato procedura je určena pro klienty v intranetu nebo Internetu.  

### <a name="manual-installation-examples"></a>Příklady ruční instalace

Tyto příklady jsou pro klienty připojené ke službě Active Directory v intranetu. Používají následující hodnoty:  

- **Mpserver**: Server, který je hostitelem bodu správy
- **FSPSERVER**: Server, který je hostitelem bodu stavu pro použití náhradní lokality  
- **ABC**: kód lokality  
- **contoso.com**: název domény  

Předpokládejme, že jste nakonfigurovali všechny systémové servery lokality s intranetovým plně kvalifikovaným názvem domény a publikovali informace o lokalitě ve službě Active Directory.  

Spusťte následující postup na klientském počítači:  

1. Přihlaste se jako místní správce.  
2. Namapujte jednotku Z `\\MPSERVER\SMS_ABC\Client`na.  
3. Přepněte příkazový řádek na jednotku Z.  

Pak spusťte jeden z následujících příkazů:  

#### <a name="manual-example-1"></a>Ruční příklad 1  

`CCMSetup.exe`  

Tento příkaz nainstaluje klienta bez dalších parametrů nebo vlastností. Klient se automaticky nakonfiguruje s vlastnostmi instalace klienta publikovanými na Active Directory Domain Services, včetně těchto nastavení:  

- Kód lokality: Toto nastavení vyžaduje, aby bylo síťové umístění klienta zahrnuto do skupiny hranic, kterou jste nakonfigurovali pro přiřazení klienta.  
- Bod správy.
- Bod záložního stavu.
- Komunikujte jenom pomocí protokolu HTTPS.  

Další informace najdete v tématu [o vlastnostech instalace klienta publikovaných na Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

#### <a name="manual-example-2"></a>Ruční příklad 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Tento příkaz přepíše automatickou konfiguraci, kterou Active Directory Domain Services poskytuje. Nevyžaduje, abyste zahrnuli síťové umístění klienta do skupiny hranic nakonfigurované pro přiřazení klienta. Místo toho instalace určuje tato nastavení:

- Kód lokality
- Intranetový bod správy
- Internetový bod správy
- Bod záložního stavu, který přijímá připojení z Internetu
- Použijte certifikát infrastruktury veřejných klíčů (Pokud je k dispozici) klienta, který má nejdelší dobu platnosti.

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a>Instalace přihlašovacího skriptu

Configuration Manager podporuje použití přihlašovacích skriptů k instalaci Configuration Manager klientského softwaru. Pomocí programového souboru CCMSetup. exe v přihlašovacím skriptu spusťte instalaci klienta.  

Instalace pomocí přihlašovacího skriptu používá stejné způsoby jako ruční instalace klienta. Zadejte parametr `/logon` instalace pro soubor CCMSsetup. exe. Pokud v počítači již existuje nějaká verze klienta, tento parametr brání instalaci klienta nástroje. Toto chování brání přeinstalaci klienta při každém spuštění přihlašovacího skriptu.  

Pokud neurčíte zdroj instalace pomocí `/Source` parametru a není-li zadán `/MP` žádný bod správy, ze kterého by bylo možné získat instalaci, soubor CCMSetup. exe vyhledá bod správy hledáním Active Directory Domain Services. K tomuto chování dochází pouze v případě, že jste rozšířili schéma pro Configuration Manager a publikovali jste web na Active Directory Domain Services. Případně může klient k vyhledání bodu správy použít službu DNS nebo WINS.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a>Instalace balíčků a programů

Pomocí Configuration Manager můžete vytvořit a nasadit balíček a program, který upgraduje klientský software pro vybraná zařízení. Configuration Manager poskytuje definiční soubor balíčku, který naplní vlastnosti balíčku obvykle používanými hodnotami. Přizpůsobení chování instalace klienta zadáním dalších parametrů a vlastností příkazového řádku.  

> [!NOTE]  
> Pomocí této metody nemůžete upgradovat klienty Configuration Manager 2007. Místo toho použijte automatický upgrade klienta, který automaticky vytvoří a nasadí balíček obsahující nejnovější verzi klienta. Další informace najdete v tématu [upgrade klientů](../manage/upgrade/upgrade-clients.md).  
>
> Další informace o migraci ze starších verzí klienta Configuration Manager najdete v tématu [Plánování strategie migrace klientů](../../migration/planning-a-client-migration-strategy.md).  

### <a name="create-a-package-and-program-for-the-client-software"></a>Vytvoření balíčku a programu pro klientský software  

Pomocí následujícího postupu můžete vytvořit balíček Configuration Manager a program, který můžete nasadit pro Configuration Manager klientských počítačů pro upgrade softwaru klienta.  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **balíčky** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit balíček z definice**.  

3. Na stránce **definice balíčku** v průvodci vyberte možnost **Microsoft** v seznamu **Vydavatel** a v seznamu **definice balíčku** vyberte možnost **Configuration Manager upgrade klienta** .  

4. Na stránce **zdrojové soubory** vyberte možnost **vždy získávat soubory ze zdrojové složky**.  

5. Na stránce **Zdrojová složka** vyberte možnost **Síťová cesta (název UNC)**. Pak zadejte síťovou cestu serveru a sdílenou složku, která obsahuje instalační soubory klienta.  

    > [!NOTE]  
    > Počítač, ve kterém je spuštěno nasazení Configuration Manager, musí mít přístup k zadané síťové složce. V opačném případě se instalace klienta nezdařila.  

    Chcete-li změnit některou z vlastností instalace klienta, upravte příkazový řádek CCMSetup. exe na kartě **Obecné** v dialogovém okně program **vlastnosti bezobslužného upgradu agenta Configuration Manager** . Výchozí vlastnosti instalace jsou `/noservice SMSSITECODE=AUTO`.  

6. Proveďte distribuci balíčku do všech distribučních bodů, které mají být hostitelem balíčku upgradu klienta. Pak balíček nasaďte do kolekcí zařízení, které obsahují klienty, které chcete upgradovat.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a>Zařízení s Windows spravovaná přes MDM Intune

Nasaďte klienta Configuration Manager do zařízení, která jsou zaregistrovaná v Microsoft Intune.

Tento postup platí pro tradičního klienta připojeného k intranetu. Používá tradiční metody ověřování klientů. Abyste se ujistili, že zařízení zůstane ve spravovaném stavu po instalaci klienta nástroje, musí být v intranetu a v rámci hranice Configuration Manager lokality.  

Postup pro instalaci klienta Configuration Manager do moderního zařízení s Windows 10 pomocí identity Azure AD najdete v tématu [instalace a přiřazení Configuration Manager klientů s Windows 10 pomocí Azure AD pro ověřování](deploy-clients-cmg-azure.md).

Po instalaci klienta Configuration Manager nemusíte zrušit registraci zařízení v Intune. Můžou používat Configuration Manager klienta a registraci MDM současně. Další informace najdete v tématu [Přehled spolusprávy](../../../comanage/overview.md).  

> [!Note]
> K instalaci klienta Configuration Manager do zařízení spravovaného přes Intune můžete použít jiné metody instalace klienta. Například pokud je zařízení spravované pomocí Intune v intranetu a připojené k doméně služby Active Directory, můžete k instalaci klienta Configuration Manager použít zásady skupiny.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Instalace klienta Configuration Manager pomocí Intune

1. V Intune [přidejte obchodní aplikaci pro Windows](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) , která obsahuje instalační soubor Configuration Manager klienta **CCMSetup. msi**. Tento soubor najdete ve `\bin\i386` složce instalačního adresáře Configuration Manager na serveru lokality.  

2. Do Intune Software Publisher zadejte parametry příkazového řádku. Tento příkaz můžete například použít u tradičního klienta na intranetu:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Příklad příkazu, který se má použít u moderního klienta s Windows 10 pomocí ověřování Azure AD, najdete v tématu [Příprava internetových zařízení na spolusprávu](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Přiřaďte aplikaci](https://docs.microsoft.com/mem/intune/apps/apps-deploy) ke skupině zaregistrovaných počítačů se systémem Windows.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a>Instalace bitové kopie operačního systému

Předinstalujte klienta Configuration Manager do referenčního počítače, který použijete k vytvoření image operačního systému.

> [!IMPORTANT]  
> Když použijete pořadí úloh Configuration Manager k nasazení image operačního systému, krok [připravit klienta nástroje ConfigMgr](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) zcela odebere klienta Configuration Manager.  

### <a name="prepare-the-client-computer-for-imaging"></a>Příprava klientského počítače na vytvoření bitové kopie  

1. Ručně nainstalujte Configuration Manager klientský software do referenčního počítače. Další informace najdete v tématu [Ruční instalace klientů Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    > Nezadávejte Configuration Manager kód lokality pro klienta ve vlastnostech příkazového řádku CCMSetup. exe.  

2. Na příkazovém řádku zadejte `net stop ccmexec` příkaz pro zastavení služby Hostitel agenta serveru SMS (Ccmexec. exe) v referenčním počítači.  

3. Odstraňte souboru SMSCFG. Soubor INI ze složky Windows v referenčním počítači.  

4. Odeberte všechny certifikáty, které jsou uložené v úložišti místního počítače v referenčním počítači. Pokud například používáte certifikáty PKI, před vytvořením bitové kopie počítače odeberte certifikáty z **osobního** úložiště pro **počítač** a **uživatele**.  

5. Pokud jsou klienti nainstalováni v jiné hierarchii Configuration Manager než v hierarchii referenčního počítače, odeberte důvěryhodný kořenový klíč z referenčního počítače.  

    > [!NOTE]  
    > Pokud klienti nemohou zadat dotaz na Active Directory Domain Services a vyhledat bod správy, pomocí důvěryhodného kořenového klíče určíte důvěryhodné body správy. Pokud nasadíte všechny bitové kopie klientů ve stejné hierarchii jako hlavní počítač, ponechejte důvěryhodný kořenový klíč na místě.
    >
    > Pokud nasadíte klienty v různých hierarchiích, odeberte důvěryhodný kořenový klíč. Tyto klienty taky můžete zřídit pomocí nového důvěryhodného kořenového klíče. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Použijte software pro vytváření imagí k zachycení image referenčního počítače.  

7. Nasaďte bitovou kopii na cílové počítače.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a>Počítače v pracovní skupině

Configuration Manager podporuje instalaci klienta pro počítače v pracovních skupinách. Nainstalujte klienta na počítače pracovní skupiny pomocí metody určené v tématu [Ruční instalace klientů Configuration Manager](#BKMK_Manual).  

### <a name="prerequisites"></a>Požadavky  

- Ručně nainstalujte klienta na každý počítač pracovní skupiny. Během instalace musí mít interaktivní uživatel práva místního správce.  

- Pro přístup k prostředkům v doméně serveru Configuration Manager lokality nakonfigurujte účet přístupu k síti pro lokalitu. Zadejte tento účet v součásti lokality pro distribuci softwaru. Další informace najdete v tématu [součásti lokality](../../servers/deploy/configure/site-components.md).  

### <a name="limitations"></a>Omezení  

- Klienti pracovní skupiny nemůžou najít body správy z Active Directory Domain Services. Místo toho používají DNS, službu WINS nebo jiný bod správy.  

- Globální roaming se nepodporuje. Klienti pracovní skupiny nemohou pro informace o lokalitě zadat dotaz na Active Directory Domain Services.  

- Metody zjišťování služby Active Directory nemůžou zjišťovat počítače v pracovních skupinách.  

- Nemůžete nasadit software pro uživatele počítačů pracovní skupiny.  

- K instalaci klienta nástroje na počítače pracovní skupiny nemůžete použít metodu nabízené instalace klienta.  

- Klienti pracovní skupiny nemohou používat protokol Kerberos k ověřování a mohou vyžadovat ruční schválení.  

- Nemůžete nakonfigurovat klienta pracovní skupiny jako distribuční bod. Configuration Manager vyžaduje, aby počítače distribučního bodu byly členy domény.  

### <a name="install-the-client-on-workgroup-computers"></a>Instalace klienta do počítačů v pracovní skupině  

Zkontrolujte požadavky a pak postupujte podle pokynů v části [Postup ruční instalace klientů Configuration Manager](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Pracovní skupina – příklad 1

Tento příklad provádí následující akce:

- Nainstaluje klienta pro správu intranetového klienta.
- Určuje kód lokality.
- Určuje příponu DNS pro vyhledání bodu správy  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Příklad pracovní skupiny 2

Tento příklad vyžaduje, aby klient byl v síťovém umístění, které je nakonfigurováno ve skupině hranic. Pokud tento požadavek není splněn, automatické přiřazení lokality nebude fungovat. Příkaz obsahuje záložní stavový bod na serveru FSPSERVER. Tato vlastnost pomáhá sledovat nasazení klientů a identifikovat problémy s komunikací klientů.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a>Internetová správa klientů  

> [!NOTE]  
> Tato část se nevztahuje na klienty, kteří používají [bránu pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md). Pokud chcete nainstalovat internetové klienty pomocí brány pro správu cloudu, přečtěte si téma [instalace a přiřazení Configuration Manager klientů Windows 10 pomocí Azure AD pro ověřování](deploy-clients-cmg-azure.md).  

Pokud lokalita Configuration Manager podporuje [internetovou správu klientů](../manage/plan-internet-based-client-management.md) pro klienty, kteří jsou někdy na intranetu a někdy na internetu, máte dvě možnosti, když instalujete klienty na intranet:  

- Při instalaci klienta nástroje použijte například `CCMHOSTNAME=<internet FQDN of the internet-based management point>` vlastnost Client. msi, a to pomocí ruční instalace nebo nabízených oznámení klienta. Když použijete tuto metodu, přímo přiřaďte klienta k lokalitě. Nemůžete použít automatické přiřazení lokality. Přečtěte si část [Ruční instalace Configuration Manager klientů](#BKMK_Manual) , která poskytuje příklad této metody konfigurace.  

- Nainstalujte klienta pro správu intranetového klienta a potom přiřaďte klientovi internetový bod správy klienta. Bod správy změňte pomocí vlastností klienta na stránce **Configuration Manager** v Ovládacích panelech nebo pomocí skriptu. Když používáte tuto metodu, můžete použít automatické přiřazení klienta. Další informace najdete v části [Postup konfigurace klientů pro správu internetových klientů po instalaci klienta](#BKMK_ConfigureIBCM_MP) .  

Pokud chcete instalovat klienty, kteří jsou na internetu, vyberte jednu z následujících podporovaných metod:  

- Poskytněte mechanismus pro tyto klienty k dočasnému připojení k intranetu pomocí sítě VPN. Pak klienta nainstalujte pomocí vhodné metody instalace klienta.  

- Použijte metodu instalace, která je nezávislá na Configuration Manager. Například zabalit zdrojové soubory instalace klienta na vyměnitelné médium a poslat médium uživatelům. Zdrojové soubory instalace klienta jsou umístěny ve `<installation path>\Client` složce na serveru Configuration Manager lokality. Na médiu zahrňte skript, který se ručně zkopíruje do složky klienta. Z této složky nainstalujte klienta pomocí souboru CCMSetup. exe a všech příslušných vlastností příkazového řádku CCMSetup.  

> [!NOTE]  
> Configuration Manager nepodporuje instalaci klienta přímo z internetového bodu správy nebo z internetového bodu aktualizace softwaru.

Klienti, kteří jsou spravováni přes Internet, musí komunikovat s internetovými systémy lokality. Než nainstalujete klienta nástroje, ujistěte se, že tito klienti mají také certifikáty infrastruktury veřejných klíčů (PKI). Tyto certifikáty nainstalujte nezávisle na Configuration Manager. Další informace najdete v tématu [požadavky na certifikát PKI](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalace klientů na internetu zadáním vlastností příkazového řádku služby CCMSetup  

1. Postupujte podle pokynů v části [Postup ruční instalace klientů Configuration Manager](#BKMK_Manual). Vždy zahrňte následující možnosti:  

    - Parametr příkazového řádku CCMSetup`/source:<local path of the copied Client folder>`  

    - Parametr příkazového řádku CCMSetup`/UsePKICert`  

    - Vlastnost Client. msi`CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Vlastnost Client. msi`SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Vlastnost Client. msi`SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Pokud má lokalita více než jeden internetový bod správy, nezáleží na tom, který parametr zadáte `CCMHOSTNAME` . Když se klient Configuration Manager připojí k určenému internetovému bodu správy, pošle klientovi seznam dostupných internetových bodů správy v lokalitě. Klient náhodně vybere jednu ze seznamu.

2. Pokud nechcete, aby klient kontroloval seznam odvolaných certifikátů (CRL), zadejte parametr `/NoCRLCheck`příkazového řádku CCMSetup.  

3. Pokud používáte internetový bod stavu pro použití náhradní lokality, určete vlastnost `FSP=<internet FQDN of the internet-based fallback status point>`Client. msi.  

4. Pokud instalujete klienta pro správu pouze internetových klientů, určete vlastnost `CCMALWAYSINF=1`Client. msi.  

5. Určete, zda je nutné zadat další parametry příkazového řádku služby CCMSetup. Pokud má například klient více než jeden platný certifikát PKI, bude pravděpodobně nutné zadat kritérium výběru certifikátu. Seznam dostupných vlastností najdete v tématu [informace o parametrech instalace a vlastnostech klienta](about-client-installation-properties.md).  

#### <a name="internet-based-example"></a>Příklad na internetu

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

Tento příklad nainstaluje klienta s následujícím chováním:

- Použijte zdrojové soubory ze složky na jednotce D.
- Použijte klientský certifikát PKI.
- Vyberte certifikát s nejdelší dobou platnosti.
- Správa pouze internetových klientů.
- Přiřaďte klientovi používání internetového bodu správy s názvem SERVER1.
- Přiřaďte internetový bod záložního stavu v doméně contoso.com.
- Přiřaďte klienta k webu ABC.  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a>Konfigurace klientů pro správu internetových klientů po instalaci klientů  

K přiřazení internetového bodu správy po instalaci klienta použijte jeden z následujících postupů. První vyžaduje ruční konfiguraci a je vhodná pro několik klientů. Druhý je vhodný pro konfiguraci mnoha klientů.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Konfigurace klientů pro správu internetových klientů po instalaci klientů z ovládacích panelů Configuration Manager  

1. Na straně klienta otevřete ovládací panely **Configuration Manager** .  

2. Na kartě **Internet** zadejte plně kvalifikovaný název domény (FQDN) internetového bodu správy jako **internetový plně kvalifikovaný název**domény.  

    > [!NOTE]  
    > Karta **Internet** je dostupná pouze v případě, že klient má klientský certifikát PKI.  

3. Pokud klient přistupuje k Internetu pomocí proxy server, zadejte nastavení proxy server.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Konfigurace klientů pro správu internetových klientů po instalaci klientů pomocí skriptu  

##### <a name="powershell"></a>PowerShell

1. Otevřete online editor PowerShellu, jako je například PowerShell ISE nebo Visual Studio Code. Můžete také použít textový editor, například Poznámkový blok.

2. Zkopírujte následující řádky kódu a vložte je do editoru. Nahraďte `'mp.contoso.com'` internetovým plně kvalifikovaným názvem domény internetového bodu správy.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > Poslední řádek je pouze pro ověření nové hodnoty bodu správy sítě Internet.
    >
    > Pokud chcete odstranit zadaný internetový bod správy, odeberte hodnotu plně kvalifikovaného názvu domény serveru v uvozovkách. Řádek se bude `$newInternetBasedManagementPointFQDN = ''`nacházet.

3. Uložte soubor s příponou. ps1.  

4. Spusťte skript se zvýšenými právy na klientských počítačích. Použijte jednu z těchto metod:  

    - Nasaďte soubor na stávající klienty nástroje Configuration Manager pomocí balíčku a programu.  

    - Spusťte soubor místně na stávajících Configuration Manager klientech dvojitým kliknutím na soubor skriptu v Průzkumníkovi souborů.  

Je možné, že bude nutné restartovat klienta, aby se změny projevily.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a>Zřídit vlastnosti instalace klienta

Zřídit vlastnosti instalace klienta pro klientské instalace na základě aktualizace softwaru a aktualizace softwaru. K zřizování počítačů s Configuration Manager vlastnostmi instalace klienta použijte Windows Zásady skupiny. Tyto vlastnosti jsou uloženy v registru počítače. Klient je při instalaci přečte. Tato procedura není normálně nutná, ale může být nutná pro některé scénáře instalace klienta, například:  

- Používáte nastavení zásad skupiny nebo metody instalace klienta na základě aktualizace softwaru. Nerozšířili jste schéma služby Active Directory pro Configuration Manager.  

- Chcete vyřadit vlastnosti instalace klienta na určitých počítačích.  

> [!NOTE]  
> Pokud jsou v příkazovém řádku programu CCMSetup. exe zadány jakékoli vlastnosti instalace, nebudou použity vlastnosti instalace zřízené na počítačích.

Šablona pro správu zásad skupiny s `ConfigMgrInstallation.adm` názvem se dodává na instalačním médiu Configuration Manager. Pomocí této šablony můžete klientským počítačům zřídit vlastnosti instalace.

> [!TIP]
> Ve výchozím nastavení `ConfigMgrInstallation.adm` nepodporuje řetězce větší než 255 znaků. Tato konfigurace může mít vliv na přidání více parametrů nebo parametrů s dlouhými hodnotami, například CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> Řešení tohoto problému:
>
> 1. Upravit `ConfigMgrInstallation.adm` v programu Poznámkový blok.
> 2. V případě vlastnosti `VALUENAME SetupParameters`změňte `MAXLEN` hodnotu na větší celé číslo. Například, `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Konfigurace a přiřazení vlastností instalace klienta pomocí objektu zásad skupiny  

1. Importujte šablonu pro správu ConfigMgrInstallation. adm do nového nebo existujícího objektu zásad skupiny (GPO) pomocí editoru, jako je Windows Editor objektů zásad skupiny. Tento soubor najdete ve `TOOLS\ConfigMgrADMTemplates` složce na instalačním médiu Configuration Manager.  

2. Otevřete vlastnosti importovaného nastavení **Konfigurovat nastavení nasazení klienta**.  

3. Vyberte **Povoleno**.  

4. V poli **CCMSetup** zadejte požadované vlastnosti příkazového řádku CCMSetup. Seznam všech vlastností příkazového řádku CCMSetup a příklady jejich použití najdete v tématu [informace o parametrech instalace a vlastnostech klienta](about-client-installation-properties.md).  

5. Přiřaďte objekt zásad skupiny počítačům, které chcete zřídit, pomocí Configuration Manager vlastností instalace klienta.  
