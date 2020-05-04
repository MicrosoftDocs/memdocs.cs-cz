---
title: Kurz&#58; povolení spolusprávy pro zařízení v Internetu
titleSuffix: Configuration Manager
description: Přečtěte si, jak nakonfigurovat spolusprávu pro nová internetová zařízení s Windows 10 pomocí Configuration Manager a Microsoft Intune.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712712"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Kurz: povolení spolusprávy pro nová zařízení na internetu

Společně se správou můžete zajistit, aby se při správě počítačů ve vaší organizaci používaly Configuration Manager. Ve stejnou chvíli budete investovat do cloudu prostřednictvím použití Intune pro zabezpečení a moderní zřizování.

V tomto kurzu nastavíte spolusprávu zařízení s Windows 10 v prostředí, kde používáte Azure Active Directory (AD) i místní službu AD, ale nemáte [hybridní Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD). Prostředí Configuration Manager zahrnuje jednu primární lokalitu se všemi rolemi systému lokality umístěnými na stejném serveru, na serveru lokality. Tento kurz začíná místním prostředím, že vaše zařízení s Windows 10 už jsou zaregistrovaná v Intune. 

Pokud máte hybridní službu Azure AD, která se připojuje k místní službě AD pomocí Azure AD, doporučujeme vám náš doprovodný kurz, který [umožní spolusprávu pro Configuration Manager klienty](tutorial-co-manage-clients.md).

Tento kurz použijte v těchto případech:
  
- Máte zařízení s Windows 10, která se mají přenést do společné správy. Tato zařízení mohla být zřízená prostřednictvím Windows autopilotu nebo přímo od výrobce hardwaru.
- Máte zařízení s Windows 10 na internetu, která aktuálně spravujete pomocí Intune, ke kterému chcete přidat klienta Configuration Manager.

**V tomto kurzu provedete tyto kroky:**  
> [!div class="checklist"]  
> * Kontrola požadavků pro Azure a místní prostředí
> * Vyžádejte si veřejný certifikát SSL pro bránu pro správu cloudu (CMG).
> * Povolení služeb Azure v Configuration Manager
> * Nasazení a konfigurace brány pro správu cloudu  
> * Konfigurace bodu správy a klientů, aby používali CMG
> * Povolit spolusprávu v Configuration Manager
> * Konfigurace Intune pro instalaci klienta Configuration Manager

## <a name="prerequisites"></a>Požadavky  

### <a name="azure-services-and-environment"></a>Služby a prostředí Azure

- Předplatné Azure ([bezplatná zkušební verze](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Odběr služby Microsoft Intune
  > [!TIP]  
  > Předplatné Enterprise mobility and Security (EMS) zahrnuje Azure Active Directory Premium i Microsoft Intune. Předplatné EMS ([bezplatná zkušební verze](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))  

- Intune je nakonfigurovaný k [automatické registraci zařízení](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune) .  

> [!TIP]
> Už nemusíte kupovat a přiřazovat k vašim uživatelům jednotlivé licence Intune ani EMS. Další informace najdete v tématu [Nejčastější dotazy k produktu a licencování](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Místní infrastruktura

- Configuration Manager aktuální větev verze 1810 nebo novější.
  
  Verze 1810 zavádí [Rozšířený protokol HTTP](../core/plan-design/hierarchy/enhanced-http.md), který se v tomto kurzu používá, aby nedocházelo k složitějším požadavkům PKI. Při použití rozšířeného protokolu HTTP musí být primární lokalita, kterou používáte ke správě klientů, nakonfigurovaná tak, aby používala Configuration Manager generované certifikáty pro systémy lokality HTTP.  

  Verze 1810 také zavádí jednodušší příkazový řádek pro internetovou instalaci klienta Configuration Manager.

- Autorita MDM musí být nastavená na Intune.  

### <a name="external-certificates"></a>Externí certifikáty

- CMG ověřovací certifikát serveru. Tento certifikát je certifikát SSL od poskytovatele veřejných a globálně důvěryhodných certifikátů. Například mimo jiné, DigiCert, Thawte nebo VeriSign. Tento certifikát exportujete jako. Soubor PFX s privátním klíčem  

- Později v tomto kurzu poskytujeme pokyny ke konfiguraci žádosti pro tento certifikát.

### <a name="permissions"></a>Oprávnění

V celém tomto kurzu použijte následující oprávnění k dokončení úkolů:

- Účet, který je *globálním správcem* pro Azure Active Directory (Azure AD)
- Účet, který je *správcem domény* v místní infrastruktuře  
- Účet, který je *úplný správce* pro *všechny* obory v Configuration Manager

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Vyžádání veřejného certifikátu pro bránu pro správu cloudu

Pokud jsou vaše zařízení připojená k Internetu, vyžaduje společná správa bránu pro správu cloudu Configuration Manager (CMG). CMG umožňuje, aby vaše Internetová zařízení s Windows 10 komunikovala s vaším místním nasazením Configuration Manager. K navázání vztahu důvěryhodnosti mezi zařízeními a Configuration Managerovým prostředím vyžaduje CMG certifikát SSL.

V tomto kurzu se používá veřejný certifikát nazvaný **certifikát ověřování serveru CMG** , který odvozuje autoritu od globálně důvěryhodného poskytovatele certifikátů. I když je možné nakonfigurovat spolusprávu pomocí certifikátů, které se odvozují od vaší místní certifikační autority společnosti Microsoft, používání certifikátů podepsaných svým držitelem je nad rámec tohoto kurzu.

**Ověřovací certifikát serveru CMG** slouží k šifrování komunikačních přenosů mezi klientem Configuration Manager a CMG. Certifikát se vrátí do důvěryhodného kořenového adresáře a ověří identitu serveru pro klienta. Veřejný certifikát obsahuje důvěryhodný kořenový adresář, na který již klienti Windows důvěřují.

O tomto certifikátu: 

- V Azure identifikujete jedinečný název služby CMG a potom v žádosti o certifikát zadáte tento název.  
- Vygenerujete žádost o certifikát na určitém serveru a pak odešlete žádost veřejnému poskytovateli certifikátů, abyste získali potřebný certifikát SSL.  
- Naimportujete do systému, který požadavek vygeneroval, na certifikát, který od poskytovatele obdržíte. Stejný počítač můžete použít k exportu certifikátu pro použití při pozdějším nasazení CMG do Azure.  
- Když se CMG nainstaluje, vytvoří v Azure službu CMG s použitím názvu, který jste zadali v certifikátu.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identifikace jedinečného názvu pro bránu pro správu cloudu v Azure

Když vyžádáte ověřovací certifikát serveru CMG, určíte, co musí být jedinečný název, abyste identifikovali *cloudovou službu (Classic)* v Azure. Ve výchozím nastavení používá veřejný cloud Azure *cloudapp.NET*a CMG je hostovaný v rámci domény cloudapp.NET jako * \<YourUniqueDnsName>. cloudapp.NET*.  

> [!TIP]  
> V tomto kurzu používá **ověřovací certifikát serveru CMG** plně kvalifikovaný název domény, který končí na *contoso.com*.  Po vytvoření CMG nakonfigurujeme záznam kanonického názvu (CNAME) ve veřejném DNS naší organizace. Tento záznam vytvoří alias pro CMG, který se mapuje na název, který používáme ve veřejném certifikátu.  

Před podáním žádosti o veřejný certifikát potvrďte, že je název, který chcete použít, dostupný v Azure. Službu nevytváříte přímo v Azure. Místo toho se k vytvoření cloudové služby při instalaci CMG Configuration Manager používá název zadaný ve veřejném certifikátu, který požadujete.  

1. Přihlaste se na web [Microsoft Azure Portal](https://portal.azure.com/).  

2. Vyberte **vytvořit prostředek**, zvolte kategorii **COMPUTE** a pak vyberte **cloudová služba**. Otevře se stránka cloudová služba (Classic).

3. Do pole **název DNS**zadejte název předpony pro cloudovou službu, kterou budete používat. Tato předpona musí být stejná jako ta, kterou použijete později při žádosti o certifikát publikování pro ověřovací certifikát serveru CMG. Používáme *MyCSG*, která vytvoří obor názvů *MyCSG.cloudapp.NET*. Rozhraní potvrdí, zda je název k dispozici nebo již používá jiná služba.  
 Jakmile ověříte, že je název, který chcete použít, dostupný, budete připraveni odeslat žádost o podepsání certifikátu (CSR).

### <a name="request-the-certificate"></a>Požádat o certifikát

Pomocí následujících informací odešlete žádost o podepsání certifikátu pro CMG k poskytovateli veřejného certifikátu. Změňte následující hodnoty tak, aby byly relevantní pro vaše prostředí.  

- *MyCMG* k identifikaci názvu služby brány pro správu cloudu
- *Contoso* jako název společnosti
- *Contoso.com* jako veřejná doména

K vygenerování žádostí o podepsání certifikátu (CSR) doporučujeme použít server primární lokality. Když certifikát obdržíte, musíte ho zaregistrovat na stejném serveru, který vygeneroval CSR, nebo nemůžete exportovat privátní klíč certifikátů, který je povinný.  

Když vygenerujete CSR, požádejte o typ poskytovatele klíčů verze 2. Podporují se jenom certifikáty verze 2.  

> [!TIP]  
> Když nasadíme CMG, nainstalujeme zároveň také distribuční bod cloudu (CDP). Ve výchozím nastavení, když nasadíte CMG, možnost **POVOLÍ CMG fungovat jako distribuční bod cloudu a vybere se obsah z úložiště Azure** . Společné umístění CDP na serveru pomocí nástroje CMG odstraňuje nutnost samostatného certifikátu a konfigurací pro podporu CDP. I když se CDP nepožaduje pro použití spolusprávy, je užitečný ve většině prostředí.  
>
> Pokud budete pro spolusprávu používat další distribuční body cloudu, budete muset pro každý další server požádat o samostatné certifikáty. Pro vyžádání veřejného certifikátu pro CDP použijte stejné podrobnosti jako u CSR pro bránu pro správu cloudu. Je potřeba změnit pouze běžný název, aby byl jedinečný pro každý CDP.  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Podrobnosti o CSR pro bránu pro správu cloudu

- **Běžný název**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Příklad: MyCSG.contoso.com  
- **Alternativní název subjektu**: totéž jako běžný název (CN)  
- **Organizace**: název vaší organizace  
- **Oddělení**: na organizaci  
- **Město**: podle vaší organizace  
- **Stav**: na organizaci  
- **Země**: na vaši organizaci  
- **Velikost klíče: 2048**  
- **Zprostředkovatel: zprostředkovatel kryptografických služeb Microsoft RSA SChannel**  

### <a name="import-the-certificate"></a>Importovat certifikát

Po přijetí veřejného certifikátu ho importujte do místního úložiště certifikátů počítače, který vytvořil CSR. Pak exportujte certifikát jako. Soubor PFX, abyste ho mohli použít pro CMG v Azure.  

Poskytovatelé veřejných certifikátů obvykle poskytují pokyny k importu certifikátu. Proces importu certifikátu by měl vypadat podobně jako v následujících pokynech:  

1. V počítači, do kterého se má certifikát importovat, vyhledejte soubor Certificate. pfx.  

2. Klikněte na soubor pravým tlačítkem a pak vyberte **nainstalovat PFX** .  

3. Po spuštění Průvodce importem certifikátu vyberte **Další**.  

4. Na stránce **soubor k importu** vyberte možnost **Další**.

5. Na stránce **heslo** zadejte do pole heslo heslo k privátnímu klíči a pak vyberte **Další**.  
  
   Vyberte možnost, aby se klíč exportovali.

6. Na **stránce úložiště certifikátů**vyberte možnost **automaticky vybrat úložiště certifikátů na základě typu certifikátu**a poté vyberte možnost **Další**.  

7. Vyberte **Finish** (Dokončit).

### <a name="export-the-certificate"></a>Export certifikátu

Exportujte *ověřovací certifikát serveru CMG* ze serveru. Po opětovném exportu se certifikát dá použít pro bránu pro správu cloudu v Azure.  

1. Na serveru, kam jste importovali veřejný certifikát SSL, spusťte **Certlm. msc** a otevřete konzolu Správce certifikátů.  

2. V konzole správce certifikátů vyberte **osobní certifikáty >**. Potom klikněte pravým tlačítkem na *ověřovací certifikát serveru CMG* , který jste zaregistrovali v předchozím postupu, a pak vyberte **všechny úlohy > exportovat**.  

3. V Průvodci exportem certifikátu vyberte možnost **Další**, vyberte možnost **Ano, exportovat privátní klíč**a potom klikněte na tlačítko **Další**.  

4. Na stránce formát souboru pro export vyberte **Personal Information Exchange-PKCS #12 (. PFX)**, vyberte **Další**a zadejte heslo. Jako název souboru zadejte název jako **C:\ConfigMgrCloudMGServer**. Na tento soubor se budete odkazovat při vytváření CMG v Azure.  

5. Vyberte **Další**a potvrďte následující nastavení před výběrem možnosti **Dokončit** pro dokončení exportu:  

   - Klíče exportu = Ano  
   - Zahrnout všechny certifikáty na cestě k certifikátu = Ano  
   - Formát souboru = Personal Information Exchange (*. pfx)  

6. Po dokončení exportu Najděte soubor. pfx a umístěte jeho kopii do **C:\Certs** Configuration Manager na serveru primární lokality, který bude spravovat internetové klienty. Složka certifikáty je dočasná složka, která se má použít při přesouvání certifikátů mezi servery. Když nasadíte bránu pro správu cloudu do Azure, přistupujete k souboru certifikátu ze serveru primární lokality.  

Po zkopírování certifikátu na server primární lokality můžete certifikát odstranit z osobního úložiště certifikátů na členském serveru.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Povolení služby Azure Cloud Services v Configuration Manager

Pokud chcete nakonfigurovat služby Azure v konzole Configuration Manager, použijte Průvodce konfigurací služeb Azure a vytvořte dvě aplikace Azure Active Directory (Azure AD).  

- **Serverová aplikace** – *Webová aplikace* ve službě Azure AD  
- **Klientská aplikace** – *nativní klientská* aplikace v Azure AD  

Z primárního serveru lokality spusťte následující postup.  

1. Z primárního serveru lokality otevřete konzolu Configuration Manager a v části **správa > Cloud Services > služby Azure**a vyberte **Konfigurovat služby Azure**.  

   Na stránce Konfigurovat službu Azure zadejte popisný název služby Cloud Management, kterou konfigurujete. Příklad: *Moje služba Cloud Management*.

   Pak vyberte **Správa cloudu**a pak vyberte **Další**.  

   > [!TIP]  
   > Další informace o konfiguracích, které provedete v průvodci, najdete v tématu [spuštění Průvodce službami Azure](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard) .

2. Na stránce **Vlastnosti aplikace** pro **webovou aplikaci**vyberte **Procházet** a otevřete dialogové okno **aplikace serveru** a pak vyberte **vytvořit**. Nakonfigurujte následující pole:

   - **Název aplikace**: zadejte popisný název aplikace, jako je třeba *Webová aplikace pro správu cloudu*.  

   - **Adresa URL domovské stránky**: tuto hodnotu nepoužívá Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení je `https://ConfigMgrService`tato hodnota.  

   - **Identifikátor URI ID aplikace**: Tato hodnota musí být v TENANTOVI Azure AD jedinečná. Je v přístupovém tokenu, který používá klient Configuration Manager k vyžádání přístupu ke službě. Ve výchozím nastavení je `https://ConfigMgrService`tato hodnota.  

   Pak vyberte **Přihlásit**se a zadejte účet globálního správce služby Azure AD. Tyto přihlašovací údaje se Configuration Manager neukládají. Tento uživatel nevyžaduje oprávnění v Configuration Manager a nemusí být stejný účet, který spouští Průvodce službami Azure.

   Po přihlášení se zobrazí výsledky. Kliknutím na **OK** zavřete dialogové okno vytvořit serverovou aplikaci a vraťte se na stránku vlastností aplikace.

3. Pro **nativní klientskou aplikaci**vyberte **Procházet** a otevřete dialogové okno **klientská aplikace** .

4. Výběrem **vytvořit** otevřete dialogové okno **vytvořit klientskou aplikaci** a pak nakonfigurujte následující pole:  

   - **Název aplikace**: zadejte popisný název aplikace, jako je například *nativní klientská aplikace pro správu cloudu*.

   - **Adresa URL odpovědi**: Tato hodnota není používána Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení je `https://ConfigMgrClient`tato hodnota.
   Pak vyberte **Přihlásit**se a zadejte účet globálního správce služby Azure AD. Podobně jako u webové aplikace se tyto přihlašovací údaje neukládají a nevyžadují oprávnění v Configuration Manager.

   Po přihlášení se zobrazí výsledky. Kliknutím na **OK** zavřete dialogové okno vytvořit klientskou aplikaci a vraťte se na stránku vlastností aplikace. Pak pokračujte výběrem **Další** .

5. Na stránce **Konfigurovat nastavení zjišťování** zaškrtněte políčko **Povolit Azure Active Directory zjišťování uživatelů**, vyberte **Další**a pak dokončete konfiguraci dialogů zjišťování pro vaše prostředí.  

6. Pokračujte na stránkách souhrn, průběh a dokončení a potom průvodce zavřete.  

   Služba Azure Services pro zjišťování uživatelů Azure AD je teď povolená v Configuration Manager.  Nechejte konzoli hned otevřenou.  

7. Otevřete prohlížeč a přihlaste se k [Azure Portal](https://portal.azure.com/).  

8. Vyberte **všechny služby > Azure Active Directory > registrace aplikací**a potom:

   1. Vyberte webovou aplikaci, kterou jste vytvořili.

   2. V **nastavení > požadovaná oprávnění**vyberte **udělit oprávnění**a pak vyberte **Ano**.  

   3. Vyberte aplikaci nativního klienta, kterou jste vytvořili.

   4. V **nastavení > požadovaná oprávnění**vyberte **udělit oprávnění**a pak vyberte **Ano**.  

9. V konzole Configuration Manager klikněte na **správa > přehled > Cloud Services > služby Azure**a vyberte svou službu Azure. Pak klikněte pravým tlačítkem na **Azure Active Directory zjišťování uživatelů** a vyberte **Spustit úplné zjišťování**. Kliknutím na **tlačítko Ano** potvrďte akci.  

10. Na serveru primární lokality otevřete Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT. log** a vyhledejte následující položku, abyste zkontrolovali, že zjišťování funguje: *úspěšně publikováno udx pro Azure Active Directory uživatele* .  

    Ve výchozím nastavení je soubor protokolu v *% Program_Files% \ Microsoft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Vytvoření Cloud Services v Azure

**V této části kurzu**provedete tyto kroky:

- Vytvoření cloudové služby CMG  
- Vytváření záznamů CNAME DNS pro obě služby  

### <a name="create-the-cmg"></a>Vytvoření CMG

Tento postup slouží k instalaci brány pro správu cloudu jako služby v Azure. CMG se nainstaluje do lokality nejvyšší úrovně v hierarchii. V tomto kurzu budeme používat primární lokalitu, kde byly certifikáty zaregistrované a exportované.

1. Na serveru primární lokality otevřete konzolu Configuration Manager a pak **> Přehled správy > Cloud Services > brána pro správu cloudu**a pak vyberte **vytvořit brána pro správu cloudu**.  

2. Na stránce **Obecné**:  

   1. Vyberte své cloudové prostředí pro **prostředí Azure**. V tomto kurzu se používá **AzurePublicCloud**.  

   2. Vyberte **nasazení Azure Resource Manager**.  
  
   3. **Přihlaste** se ke svému předplatnému Azure. Configuration Manager vyplní Další informace na základě informací, které jste nakonfigurovali, když jste povolili Azure Cloud Services pro Configuration Manager.  

   Pokračujte výběrem tlačítka **Next** (Další).  

3. Na stránce **Nastavení** vyhledejte a vyberte soubor s názvem **ConfigMgrCloudMGServer. pfx**, který je soubor, který jste exportovali po importu ověřovacího certifikátu serveru CMG. Po zadání hesla se **název služby** a **název nasazení** automaticky vyplní na základě podrobností v souboru certifikátu. pfx.

4. Nastavte **oblast**.

5. V případě **skupiny prostředků**použijte existující skupinu prostředků nebo vytvořte skupinu s popisným názvem, který nepoužívá mezery, například **CofigMgrCloudServices**. Pokud se rozhodnete vytvořit skupinu, skupina se přidá jako skupina prostředků v Azure.  

6. Pokud nejste připraveni ke konfiguraci škálování, použijte jednu (1) pro počet **instancí virtuálních počítačů**. Počet instancí virtuálních počítačů umožňuje u jedné Brána pro správu cloudu (CMG) cloudovou službu škálovat tak, aby podporovala více připojení klientů. Později můžete použít konzolu Configuration Manager k vrácení a úpravám počtu instancí virtuálních počítačů, které používáte.  

7. Povolte zaškrtávací políčko pro **ověření odvolání klientského certifikátu**.

8. Zaškrtněte políčko **Povolit funkci CMG jako distribuční bod cloudu a obsluhu obsahu z Azure Storage** , pokud chcete nasadit distribuční bod cloudu s CMG.

9. Pokračujte výběrem tlačítka **Next** (Další).

10. Zkontrolujte hodnoty na stránce **Výstraha** a pak vyberte **Další**.

11. Zkontrolujte stránku **Souhrn** a kliknutím na **Další** vytvořte cloudovou službu Brána pro správu cloudu. Kliknutím na tlačítko **Zavřít** dokončete průvodce.  

12. V uzlu Brána pro správu cloudu v konzole Configuration Manager si teď můžete zobrazit novou službu.  

### <a name="create-dns-cname-records"></a>Vytvoření záznamů CNAME DNS

Když vytvoříte položku DNS pro CMG, povolíte zařízení s Windows 10 uvnitř i mimo vaši podnikovou síť a použijete překlad IP adres, abyste v Azure našli cloudovou službu CMG.

Náš příklad záznamu CNAME používá následující podrobnosti:  

- Název společnosti je **Contoso** s veřejným oborem názvů DNS ***contoso.com***.  

- Název služby CMG je **MyCMG**, který se v Azure bude ***MyCMG.CloudApp.NET*** .  

Příklad záznamu CNAME: *MyCMG.contoso.com => my.cloudapp.NET*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Konfigurace bodu správy a klientů, aby používali CMG

Nakonfigurujte nastavení, která umožní místním bodům správy a klientům používat bránu pro správu cloudu.

Vzhledem k tomu, že pro komunikaci klientů používáme vylepšenou protokol HTTP, není nutné používat bod správy HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Vytvoření spojovacího bodu CMG

Umožňuje nakonfigurovat lokalitu tak, aby podporovala rozšířené protokoly HTTP.  

1. V konzole Configuration Manager klikněte na **správa > přehled > Konfigurace lokality > lokality**a otevřete vlastnosti primární lokality.  

2. Na kartě **komunikace s klientským počítačem** vyberte možnost *https nebo HTTP* pro **použití Configuration Manager vygenerované certifikáty pro systémy lokality http**a pak kliknutím na **OK** konfiguraci uložte.

    > [!Note]
    > Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

3. Nyní přejděte do části **správa > přehled > Konfigurace lokality > servery a role systému lokality** a vyberte server s bodem správy, do kterého chcete nainstalovat bod připojení brány pro správu cloudu.  

4. Vyberte **Přidat role systému lokality**a pak **Další**> **Další.**  

5. Vyberte **bod připojení brány pro správu cloudu** a pokračujte výběrem **Další** .  

6. Zkontrolujte výchozí výběry na stránce **bod připojení brány pro správu cloudu** a ujistěte se, že je vybraná možnost správné CMG. Pokud máte více bran pro správu cloudu, můžete použít rozevírací seznam a zadat jiný CMG. Po instalaci můžete také změnit CMG, které se používají. Pokračujte výběrem tlačítka **Next** (Další).

7. Výběrem **Další** spusťte instalaci a potom zobrazte výsledky na stránce dokončení.  Kliknutím na tlačítko **Zavřít** dokončete instalaci bodu připojení.

8. Nyní přejděte do části **správa > přehled > Konfigurace lokality > servery a role systému lokality** a otevřete **vlastnosti** bodu správy, kam jste nainstalovali bod připojení. Na kartě **Obecné** zaškrtněte políčko **povolení provozu brány pro správu cloudu Configuration Manager**a pak výběrem **OK** uložte konfiguraci.
   > [!TIP]  
   > I když není nutné povolit spolusprávu, doporučujeme provést stejnou úpravu pro všechny body aktualizace softwaru.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Konfigurace nastavení klienta pro směrování klientů na používání nástroje CMG

Pomocí nastavení klienta nakonfigurujete klienty Configuration Manager ke komunikaci s CMG.  

1. Otevřete **konzolu Configuration Manager > správa > přehled > nastavení klienta**a pak upravte **výchozí nastavení klienta**.  

2. Vyberte **Cloud Services**.

3. Na stránce **výchozí nastavení** nastavte následující nastavení na = **Ano**.  

   - **Automaticky registrovat nová zařízení s Windows 10 připojená k doméně pomocí Azure Active Directory**  

   - **Povolit klientům používat bránu pro správu cloudu**

   - **Povolení přístupu k distribučnímu bodu cloudu**

4. Na stránce **zásady klienta** nastavte **možnost povolit žádosti o zásady uživatele od internetových klientů** = **Ano**.

5. Uložte tuto konfiguraci výběrem tlačítka **OK**.

## <a name="enable-co-management-in-configuration-manager"></a>Povolit spolusprávu v Configuration Manager

S konfiguracemi Azure, rolemi systému lokality a nastaveními klienta můžete nakonfigurovat Configuration Manager pro povolení spolusprávy. Po povolení spolusprávy ještě před dokončením tohoto kurzu ale budete muset v Intune udělat několik konfigurací. Jedním z těchto kroků je konfigurace Intune pro nasazení klienta Configuration Manager. Tato úloha je snazší díky uložení příkazového řádku pro nasazení klienta, který je k dispozici v Průvodci konfigurací spolusprávy. To je důvod, proč umožníme spolusprávu hned předtím, než dokončíme konfigurace pro Intune.

> [!TIP]
> - Pokud povolíte spolusprávu, přiřadíte kolekci jako *pilotní skupinu*. Jedná se o skupinu, která obsahuje malý počet klientů pro otestování konfigurací spolusprávy. Před zahájením postupu doporučujeme vytvořit vhodnou kolekci. Pak můžete tuto kolekci vybrat bez ukončení postupu.
> - Configuration Manager počínaje verzí 1906 je možné, že budete potřebovat více kolekcí, protože pro každou úlohu můžete přiřadit jinou *pilotní skupinu* .

### <a name="enable-co-management-starting-in-version-1906"></a>Povolit spolusprávu počínaje verzí 1906

Pokud chcete povolit spolusprávu od verze Configuration Manager 1906, postupujte podle následujících pokynů:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Povolit spolusprávu ve verzi 1902 a novější

Pokud chcete povolit spolusprávu pro Configuration Manager verze 1902 a starší, postupujte podle následujících pokynů:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Nasazení klienta Configuration Manager pomocí Intune

Intune můžete použít k instalaci klienta Configuration Manager v zařízeních s Windows 10, která jsou aktuálně spravovaná jenom pomocí Intune.  

Pak když se dřív nespravované zařízení s Windows 10 zaregistruje do Intune, automaticky nainstaluje klienta Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Vytvoření aplikace Intune pro instalaci klienta Configuration Manager

1. Z primárního serveru lokality se přihlaste k [Azure Portal](https://portal.azure.com/) a v **> klientských aplikacích Intune > aplikace > přidat**.

2. Pro **Typ aplikace**: vyberte **obchodní aplikaci**.

3. Vyberte **soubor balíčku aplikace**a pak přejděte do umístění Configuration Manager souboru **CCMSetup. msi**a pak vyberte **otevřít > ok**.
Například *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*

4. Vyberte **informace o aplikaci**a pak zadejte následující podrobnosti:
   - **Popis**: Configuration Manager klienta  

   - **Vydavatel**: Microsoft  

   - **Argumenty příkazového řádku**: * \<zadejte příkaz **CCMSETUPCMD** Command line. Můžete použít příkazový řádek, který jste uložili* na stránce povolení v *Průvodci konfigurací spolusprávy. Tento příkazový řádek obsahuje názvy vaší cloudové služby a další hodnoty, které zařízením umožňují nainstalovat Configuration Manager klientský software. >*  

     Struktura příkazového řádku by se měla podobat tomuto příkladu pouze pomocí parametrů CCMSETUPCMD a SMSSiteCode:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Pokud nemáte k dispozici příkazový řádek, můžete zobrazit vlastnosti *CoMgmtSettingsProd* v konzole Configuration Manager a získat tak kopii příkazového řádku.

5. Vyberte **OK > přidat**.  Aplikace se vytvoří a bude k dispozici v konzole Intune. Po zpřístupnění aplikace můžete pomocí následující části nakonfigurovat Intune tak, aby se přidělil na zařízení s Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Přiřazení aplikace Intune k instalaci klienta Configuration Manager

Následující postup nasadí aplikaci pro instalaci klienta Configuration Manager, který jste vytvořili v předchozím postupu.

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com/).  Vyberte **všechny služby > Intune > klientské aplikace > aplikace**a pak vyberte **bootstrap instalace klienta nástroje ConfigMgr**, aplikaci, kterou jste vytvořili pro nasazení klienta Configuration Manager.  

2. Vyberte **přiřazení > přidat skupinu**.  Podle **potřeby**nastavte **Typ přiřazení** a pak použijte **zahrnuté skupiny** a **Vyloučené skupiny** , abyste nastavili skupiny Azure Active Directory (AD), které mají uživatele a zařízení, které chcete zúčastnit společné správy.  

3. Vyberte **OK** a pak konfiguraci **uložte** .
Tuto aplikaci teď vyžadují uživatelé a zařízení, ke kterým jste jim přiřadili. Poté, co aplikace nainstaluje klienta Configuration Manager do zařízení, je spravován spolusprávou.

## <a name="summary"></a>Souhrn

Po dokončení kroků konfigurace tohoto kurzu můžete začít společně spravovat vaše zařízení.

## <a name="next-steps"></a>Další kroky

- Kontrola stavu souběžně spravovaných zařízení pomocí [řídicího panelu spolusprávy](how-to-monitor.md)
- Použití nástroje [Windows autopilot](quickstart-autopilot.md) k zřizování nových zařízení
- Použití pravidel dodržování předpisů [podmíněného přístupu](quickstart-conditional-access.md) a Intune ke správě přístupu uživatelů k podnikovým prostředkům
