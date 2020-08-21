---
title: Vytvoření profilů certifikátů SCEP
titleSuffix: Configuration Manager
description: Naučte se používat profily certifikátů ke zřízení spravovaných zařízení s certifikáty, které potřebují.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f1ea48887f89cf06ed4b41d0de0dfc24e9d508
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697122"
---
# <a name="create-certificate-profiles"></a>Vytváření profilů certifikátů

*Platí pro: Configuration Manager (Current Branch)*

Použijte profily certifikátů v Configuration Manager ke zřízení spravovaných zařízení s certifikáty, které potřebují pro přístup k prostředkům společnosti. Před vytvořením profilů certifikátů nastavte infrastrukturu certifikátů, jak je popsáno v tématu [Nastavení infrastruktury certifikátů](certificate-infrastructure.md).  

> [!TIP]
> Pro spoluspravovaná zařízení zvažte přesunutí [úlohy **zásad přístupu k prostředkům** ](../../comanage/workloads.md#resource-access-policies) do Intune. Pak tyto certifikáty spravujte pomocí zásad Intune. Další informace najdete v tématu [Jak přepínat úlohy](../../comanage/how-to-switch-workloads.md).

Tento článek popisuje, jak vytvořit profily certifikátů důvěryhodných kořenových a Simple Certificate Enrollment Protocol (SCEP). Pokud chcete vytvořit profily certifikátů PFX, přečtěte si téma [Vytvoření profilů certifikátů](../../mdm/deploy-use/create-pfx-certificate-profiles.md)PFX.

Postup vytvoření profilu certifikátu:

1. Spusťte Průvodce vytvořením profilu certifikátu.
1. Zadejte obecné informace o certifikátu.
1. Konfigurujte certifikát důvěryhodné certifikační autority (CA).  
1. Nakonfigurujte informace o certifikátu SCEP.  
1. Zadejte podporované platformy profilu certifikátu.

## <a name="start-the-wizard"></a>Spustit Průvodce  

Postup při spuštění profilu vytvoření certifikátu:

1. V konzole Configuration Manager přejděte do pracovního prostoru **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**, rozbalte položku **přístup k prostředkům společnosti**a potom vyberte uzel **profily certifikátů** .  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit profil certifikátu**.  

## <a name="general"></a>Obecné

Na stránce **Obecné** v Průvodci vytvořením profilu certifikátu zadejte následující informace:  

- **Název**: Zadejte jedinečný název profilu certifikátu. Opět můžete použít maximálně 256 znaků.  

- **Popis**: zadejte popis, který poskytne přehled profilu certifikátu. Zahrňte také další důležité informace, které ji pomáhají identifikovat v konzole Configuration Manager. Opět můžete použít maximálně 256 znaků.  

- Zadejte typ profilu certifikátu, který chcete vytvořit:

  - **Certifikát důvěryhodné certifikační autority**: Tento typ vyberte, pokud chcete nasadit certifikát důvěryhodné kořenové certifikační autority (CA) nebo zprostředkující certifikační autority, abyste mohli vytvořit řetěz certifikátů, kdy musí uživatel nebo zařízení ověřit jiné zařízení. Takovým zařízením může být třeba server RADIUS (Remote Authentication Dial-In User Service) nebo server VPN (virtuální privátní síť).
  
    Než budete moct vytvořit profil certifikátu SCEP, nakonfigurujte taky profil certifikátu důvěryhodné certifikační autority. V takovém případě musí být certifikát důvěryhodné certifikační autority pro certifikační autoritu, která vydá certifikát uživateli nebo zařízení.  

  - **Nastavení Simple Certificate Enrollment Protocol (SCEP)**: Tento typ vyberte, pokud chcete požádat o certifikát pro uživatele nebo zařízení s Simple Certificate Enrollment Protocol a službou role služby zápisu síťových zařízení (NDES).

  - **Nastavení PFX (Personal Information Exchange PKCS) #12 (PFX) – import**: tuto možnost vyberte, pokud chcete importovat certifikát PFX. Další informace najdete v tématu [import profilů certifikátů PFX](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Nastavení programu Personal Information Exchange PKCS #12 (PFX) – vytvořit**: tuto možnost vyberte, pokud chcete zpracovávat certifikáty PFX pomocí certifikační autority. Další informace najdete v tématu [Vytvoření profilů certifikátů PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Certifikát důvěryhodné certifikační autority  

> [!IMPORTANT]  
> Než vytvoříte profil certifikátu SCEP, nakonfigurujte aspoň jeden profil certifikátu důvěryhodné certifikační autority.
>
> Po nasazení certifikátu můžete při změně některé z těchto hodnot požádat o nový certifikát:
>
> - Zprostředkovatel úložiště klíčů
> - Název šablony certifikátu
> - Typ certifikátu
> - Formát názvu subjektu
> - Alternativní název subjektu
> - Období platnosti certifikátu
> - Použití klíče
> - Velikost klíče
> - Rozšířené použití klíče
> - Certifikát kořenové certifikační autority

1. Na stránce **Certifikát důvěryhodné CA** v Průvodci vytvořením profilu certifikátu zadejte následující informace:  

    - **Soubor certifikátu**: vyberte **importovat**a pak přejděte k souboru certifikátu.  

    - **Cílové úložiště**: U zařízení, která mají víc úložišť certifikátů, určete, kam se má certifikát uložit. U zařízení, která mají jenom jedno úložiště, se toto nastavení bude ignorovat.  

2. Pomocí hodnoty **kryptografický otisk certifikátu** ověřte, že jste naimportovali správný certifikát.  

## <a name="scep-certificates"></a>Certifikáty SCEP

### <a name="1-scep-servers"></a>1. SCEP servery

Na stránce **Servery SCEP** Průvodce vytvořením profilu certifikátu zadejte adresy URL pro servery NDES, které budou vydávat certifikáty prostřednictvím SCEP. Adresu URL služby NDES můžete automaticky přiřadit na základě konfigurace bodu registrace certifikátu nebo přidat adresy URL ručně.  

### <a name="2-scep-enrollment"></a>2. zápis SCEP

Dokončete stránku **pro zápis SCEP** v Průvodci vytvořením profilu certifikátu.

- **Opakování**: zadejte, kolikrát se zařízení automaticky znovu pokusí o certifikát na server NDES. Toto nastavení podporuje scénář, ve kterém musí žádost o certifikát před přijetím schválit správce certifikační autority. Obvykle se používá v prostředích s vysokými nároky na zabezpečení nebo v případech, kdy certifikát nevydává podniková CA, ale samostatná CA. Můžete ho použít taky při testování – umožní vám zkontrolovat nastavení žádosti o certifikát, než ji zpracuje vydávající CA. Toto nastavení používejte v kombinaci s nastavením **Zpoždění opakovaného pokusu (minuty)** .  

- **Zpoždění opakovaného pokusu (minuty)**: Zadejte interval (v minutách) mezi jednotlivými pokusy o registraci v případě, že používáte schválení správcem CA, než vydávající CA zpracuje žádost o certifikát. Pokud pro účely testování používáte schválení správce, zadejte nízkou hodnotu. Poté, co žádost schválíte, nebudete čekat dlouhou dobu, než se žádost o certifikát znovu pokusí.

    Pokud používáte schválení správcem v produkční síti, zadejte vyšší hodnotu. Díky tomuto chování může správce certifikační autority schválit nebo odmítnout schválení, která čekají na schválení.  

- **Limit obnovení (%)**: Zadejte procento životnosti certifikátu zbývající v okamžiku, kdy zařízení požádá o obnovení certifikátu.  

- **Zprostředkovatel úložiště klíčů (KSP)**: Určete, kam se má uložit klíč k certifikátu. Vyberte jednu z těchto hodnot:  

  - **Instalovat do čipu TPM (Trusted Platform Module), pokud je dostupný**: Nainstaluje klíč do čipu TPM. Pokud čip TPM neexistuje, nainstaluje se klíč do poskytovatele úložiště pro softwarový klíč.  

  - **Instalovat do čipu TPM (Trusted Platform Module), jinak selhání**: Nainstaluje klíč do čipu TPM. Pokud modul TPM neexistuje, instalace se nezdařila.  

  - **Nainstalovat do Windows Hello pro firmy, jinak chyba**: Tato možnost je k dispozici pro zařízení s Windows 10. Umožňuje uložit certifikát do úložiště Windows Hello pro firmy, které je chráněné službou Multi-Factor Authentication. Další informace najdete v tématu [Windows Hello pro firmy](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Tato možnost nepodporuje přihlášení pomocí čipové karty pro použití rozšířeného klíče na stránce vlastností certifikátu.

  - **Instalovat do zprostředkovatele úložiště klíčů pro software**: Nainstaluje klíč do zprostředkovatele úložiště klíčů pro software.  

- **Zařízení pro zápis certifikátu**: Pokud nasadíte profil certifikátu do kolekce uživatelů, povolte zápis certifikátů pouze na primárním zařízení uživatele nebo na jakémkoli zařízení, ke kterému se uživatel přihlašuje.

    Pokud nasadíte profil certifikátu do kolekce zařízení, povolte zápis certifikátů jenom pro primárního uživatele zařízení nebo pro všechny uživatele, kteří se k zařízení přihlásí.  

### <a name="3-certificate-properties"></a>3. vlastnosti certifikátu

Na stránce **Vlastnosti certifikátu** v Průvodci vytvořením profilu certifikátu zadejte následující informace:  

- **Název šablony certifikátu**: vyberte název šablony certifikátu, kterou jste nakonfigurovali v NDES a přidali do vydávající certifikační autority. Aby bylo možné procházet šablony certifikátů, váš uživatelský účet potřebuje pro šablonu certifikátu oprávnění **ke čtení** . Pokud certifikát nemůžete **Vyhledat** , zadejte jeho název.  

  > [!IMPORTANT]
  > Pokud název šablony certifikátu obsahuje znaky, které nejsou ASCII, certifikát se nesadí. (Jeden příklad těchto znaků je z čínské abecedy.) Aby se zajistilo, že se certifikát nasadí, vytvořte nejdřív kopii šablony certifikátu v certifikační autoritě. Pak přejmenujte kopii pomocí znaků ASCII.  

  - Pokud *přejdete* na možnost vyberte název šablony certifikátu, některá pole na stránce se automaticky naplní ze šablony certifikátu. V některých případech tyto hodnoty nemůžete změnit, pokud si nejste zvolili jinou šablonu certifikátu.  

  - Pokud *zadáte* název šablony certifikátu, ujistěte se, že název přesně odpovídá jedné z šablon certifikátů. Musí odpovídat názvům uvedeným v registru serveru NDES. Ujistěte se, že zadáte název šablony certifikátu, a ne zobrazovaný název šablony certifikátu.  

    Názvy šablon certifikátů zjistíte tak, že přejdete do následujícího klíče registru: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP` . Vypíše šablony certifikátů jako hodnoty pro **EncryptionTemplate**, **GeneralPurposeTemplate**a **SignatureTemplate**. Výchozí hodnota všech tří šablon certifikátů je **IPSECIntermediateOffline**a je namapovaná na zobrazované jméno šablony **IPSec (žádost offline)**.  

    > [!WARNING]  
    > Když zadáte název šablony certifikátu, Configuration Manager nemůže ověřit obsah šablony certifikátu. Možná budete moct vybrat možnosti, které šablona certifikátu nepodporuje. výsledkem může být neúspěšná žádost o certifikát. Když k tomuto chování dojde, zobrazí se chybová zpráva pro w3wp.exe v souboru CPR. log, že název šablony v žádosti o podepsání certifikátu (CSR) a výzva se neshodují.  
    >
    > Když zadáte název šablony certifikátu, která je určená pro hodnotu **GeneralPurposeTemplate** , vyberte možnost **šifrování klíče** a možnosti **digitálního podpisu** pro tento profil certifikátu. Pokud chcete v tomto profilu certifikátu povolit jenom možnost **šifrování klíče** , zadejte název šablony certifikátu pro klíč **EncryptionTemplate** . Naopak v případě, že chcete pro tento profil certifikátu povolit pouze možnost **Digitální podpis** , zadejte název šablony certifikátu pro klíč **SignatureTemplate** .  

- **Typ certifikátu**: Určete, jestli chcete certifikát nasadit na zařízení nebo uživatele.  

- **Formát názvu subjektu**: Vyberte způsob, jakým Configuration Manager automaticky vytvoří název subjektu v žádosti o certifikát. Pokud je certifikát určený pro uživatele, můžete do názvu subjektu zahrnout taky e-mailovou adresu uživatele.

    > [!NOTE]  
    > Pokud vyberete **číslo IMEI** nebo **sériové číslo**, můžete rozlišovat mezi různými zařízeními, která patří stejnému uživateli. Například tato zařízení by mohla sdílet běžný název, ale ne číslo IMEI nebo sériové číslo. Pokud zařízení nehlásí IMEI nebo sériové číslo, certifikát se vydává společně s běžným názvem.

- **Alternativní název subjektu**: Určete způsob, jakým Configuration Manager automaticky vytvoří hodnoty pro alternativní název subjektu (San) v žádosti o certifikát. Pokud jste zvolili třeba uživatelský typ certifikátu, můžete do alternativního názvu subjektu zahrnout hlavní název uživatele (UPN). Pokud se klientský certifikát ověří na serveru NPS (Network Policy Server), nastavte alternativní název subjektu na hlavní název uživatele (UPN).  

- **Období platnosti certifikátu**: Pokud nastavíte vlastní období platnosti ve vydávající certifikační autoritě, zadejte dobu zbývající do vypršení platnosti certifikátu.

    > [!TIP]
    > Pomocí následujícího příkazového řádku nastavte vlastní období platnosti: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Další informace o tomto příkazu najdete v tématu [infrastruktura certifikátů](certificate-infrastructure.md).  

    Můžete zadat hodnotu nižší, než je období platnosti zadané v šabloně certifikátu, ne však vyšší. Pokud je například období platnosti certifikátu v šabloně certifikátu dva roky, můžete zadat hodnotu jeden rok, ale ne pět let. Hodnota musí být zároveň nižší než zbývající doba platnosti certifikátu vydávající CA.  

- **Použití klíče**: Zadejte možnosti použití klíče pro certifikát. Vybírat můžete z těchto možností:  

  - **Šifrování klíče**: Umožňuje výměnu klíče jenom v případě, že je klíč zašifrovaný.  

  - **Digitální podpis**: Umožňuje výměnu klíče jenom v případě, že se k ochraně klíče využívá digitální podpis.  

  Pokud jste pro šablonu certifikátu provedli procházení, nemůžete tato nastavení změnit, pokud nevyberete jinou šablonu certifikátu.  

  Nakonfigurujte vybranou šablonu certifikátu pomocí jedné nebo obou možností použití klíče výše. V takovém případě se v souboru protokolu bodu registrace certifikátu zobrazí následující zpráva, **CRP. log**: **použití klíče v CSR a Challenge se neshoduje** .  

- **Velikost klíče (bity)**: Vyberte velikost klíče v bitech.  

- **Rozšířené použití klíče**: přidejte hodnoty pro zamýšlený účel certifikátu. Ve většině případů certifikát vyžaduje **Ověření klienta**, aby se mohl uživatel nebo zařízení ověřit na serveru. Můžete přidat jakákoli další použití klíče podle potřeby.  

- **Hashovací algoritmus:** Vyberte jeden z dostupných typů hashovacího algoritmu, který chcete s tímto certifikátem použít. Vyberte nejsilnější úroveň zabezpečení, kterou připojované zařízení podporuje.  

  > [!NOTE]  
  > **SHA-2** podporuje SHA-256, SHA-384 a SHA-512. **SHA-3** podporuje pouze SHA-3.  

- **Certifikát kořenové certifikační autority**: vyberte profil certifikátu od kořenové certifikační autority, který jste předtím nakonfigurovali a nasadili pro uživatele nebo zařízení. Tento certifikát certifikační autority musí být kořenovým certifikátem certifikační autority, která bude vydávat certifikát, který konfigurujete v tomto profilu certifikátu.  

  > [!IMPORTANT]  
  > Pokud zadáte certifikát od kořenové certifikační autority, který není pro uživatele nebo zařízení nasazený, nespustí Configuration Manager žádost o certifikát, kterou konfigurujete v tomto profilu certifikátu.  

## <a name="supported-platforms"></a>Podporované platformy  

Na stránce **podporované platformy** v Průvodci vytvořením profilu certifikátu vyberte verze operačních systémů, do kterých chcete nainstalovat profil certifikátu. Zvolením **možnosti Vybrat vše** nainstalujte profil certifikátu do všech dostupných operačních systémů.

## <a name="next-steps"></a>Další kroky

Nový profil certifikátu se zobrazí v uzlu **profily certifikátů** v pracovním prostoru **prostředky a kompatibilita** . Je připravená na nasazení pro uživatele nebo zařízení. Další informace najdete v tématu [nasazení profilů](deploy-wifi-vpn-email-cert-profiles.md).