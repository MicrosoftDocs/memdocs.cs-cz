---
title: Použití odvozených přihlašovacích údajů pro mobilní zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Použijte odvozená pověření na mobilních zařízeních jako metodu ověřování pro VPN, e-maily, profily Wi-Fi, aplikace a šifrování S/MIME a šifrování. Odvozené přihlašovací údaje jsou implementací pokynů pro NIST pro speciální publikaci 800-157.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3724e425ab284d63dbe1e64dcd236509744abe10
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329403"
---
# <a name="use-derived-credentials-in-microsoft-intune"></a>Použití odvozených přihlašovacích údajů v Microsoft Intune

*Tento článek se týká zařízení se systémem iOS.*

V prostředí, kde se pro ověřování, šifrování a podepisování vyžadují čipové karty, teď můžete pomocí Intune zřídit mobilní zařízení s certifikátem, který je odvozený od čipové karty uživatele. Tento certifikát se nazývá *odvozené přihlašovací údaje*. Intune [podporuje několik odvozených vystavitelů přihlašovacích údajů](#supported-issuers), i když v jednom okamžiku můžete použít jenom jednoho vystavitele na tenanta.

Odvozené přihlašovací údaje jsou implementací pokynů National Institute of Standards and Technology (NIST) pro odvozená pověření PIV (Personal Identity Verification) jako součást speciální publikace (SP) 800-157.

**S implementací Intune**:

- Správce Intune nakonfiguruje svého tenanta tak, aby fungoval s podporovaným vystavitelem odvozeného pověření. Nemusíte konfigurovat žádné konkrétní nastavení Intune v systému odvozeného vystavitele přihlašovacích údajů.

- Správce Intune Určuje **odvozená pověření** jako *metodu ověřování* pro následující objekty:

  - Běžné typy profilů, jako jsou Wi-Fi, VPN a e-maily, včetně aplikace pro iOS/iPadOS Native mail

  - Ověřování aplikací

  - Podepisování a šifrování S/MIME

- Uživatelé získávají odvozené přihlašovací údaje pomocí své čipové karty na počítači, aby se ověřily u odvozeného vystavitele přihlašovacích údajů. Vystavitel pak vydá mobilnímu zařízení certifikát, který je odvozený z čipové karty.

- Jakmile zařízení obdrží odvozená pověření, použije se k ověřování a podepisování a šifrování S/MIME, když aplikace nebo profily přístupu k prostředkům vyžadují odvozená pověření. 

## <a name="prerequisites"></a>Požadavky

Než nakonfigurujete svého tenanta na použití odvozených přihlašovacích údajů, přečtěte si následující informace.

### <a name="supported-platforms"></a>Podporované platformy

Intune podporuje odvozená pověření na těchto platformách operačního systému:

- iOS/iPadOS

### <a name="supported-issuers"></a>Podporovaná Vystavitelé

Intune podporuje jeden odvozený Vystavitel přihlašovacích údajů na každého tenanta. Intune můžete nakonfigurovat tak, aby fungoval s následujícími vystaviteli:

- **DISA purebred**: https://cyber.mil/pki-pke/purebred/
- **Entrust Datacard**: https://www.entrustdatacard.com/
- **Intercede**: https://www.intercede.com/

Důležité informace o používání různých vystavitelů najdete v pokynech k tomuto vystaviteli.<!-- , including the issuers end-user workflow-->. Další informace najdete v tématu [plánování odvozených přihlašovacích údajů](#plan-for-derived-credentials) v tomto článku.

> [!IMPORTANT]  
> Pokud odstraníte odvozeného vystavitele přihlašovacích údajů z vašeho tenanta, odvozené přihlašovací údaje, které byly vytvořeny prostřednictvím tohoto vystavitele, nebudou nadále fungovat.
>
> Viz [Změna odvozeného vystavitele přihlašovacích údajů](#change-the-derived-credential-issuer) dále v tomto článku.

### <a name="company-portal-app"></a>Aplikace Portál společnosti

Naplánujte nasazení aplikace Portál společnosti Intune do zařízení, která se zaregistrují pro odvozená pověření. Uživatelé zařízení používají aplikaci Portál společnosti k zahájení procesu registrace přihlašovacích údajů.

Informace o zařízeních s iOS/iPadOS najdete v tématu [Přidání aplikací ze Storu pro iOS/iPadOS do Microsoft Intune](../apps/store-apps-ios.md).

## <a name="plan-for-derived-credentials"></a>Plánování odvozených přihlašovacích údajů

Před nastavením odvozeného vystavitele přihlašovacích údajů si probereme následující skutečnosti.

### <a name="1-review-the-documentation-for-your-chosen-derived-credential-issuer"></a>1) Přečtěte si dokumentaci k vybranému vystaviteli odvozeného pověření.  

Před konfigurací vystavitele si prostudujte dokumentaci k tomuto vydavateli, abyste porozuměli tomu, jak jejich systém poskytuje odvozená pověření do zařízení.

V závislosti na vystaviteli, který si zvolíte, možná budete potřebovat pracovníky, kteří budou k dispozici v době registrace a pomáhat uživatelům s dokončením procesu. Měli byste taky zkontrolovat aktuální konfigurace Intune, abyste měli jistotu, že neblokují přístup, který je nezbytný pro zařízení nebo uživatele k dokončení žádosti o přihlašovací údaje.

Můžete například použít podmíněný přístup k blokování přístupu k e-mailu pro zařízení, která nedodržují předpisy. Pokud spoléháte na e-mailová oznámení, která uživatele informují o spuštění odvozeného procesu registrace přihlašovacích údajů, uživatelé nemusí tyto pokyny dostávat, dokud nebudou kompatibilní se zásadami.

Podobně některé z odvozených pracovních postupů žádostí o přihlašovací údaje vyžadují použití kamery zařízení k naskenování kódu QR na obrazovce. Tento kód propojuje toto zařízení s požadavkem na ověření, ke kterému došlo u odvozeného vystavitele přihlašovacích údajů s přihlašovacími údaji uživatele čipové karty. Pokud zásady konfigurace zařízení blokují použití kamery, uživatel nemůže dokončit odvozenou žádost o zápis přihlašovacích údajů.

Obecné informace:

- Najednou můžete nakonfigurovat jenom jednoho vystavitele pro každého tenanta a tento Vystavitel je dostupný pro všechny uživatele a podporovaná zařízení ve vašem tenantovi.

- Uživatelé nebudou informováni o tom, že se musí zaregistrovat pro odvozené přihlašovací údaje, dokud je neurčíte pomocí zásad, které vyžadují odvozená pověření.

- Oznámení může být prostřednictvím oznámení aplikace pro Portál společnosti, prostřednictvím e-mailu nebo obou. Pokud se rozhodnete používat e-mailová oznámení a používáte povolený podmíněný přístup, uživatelé nemusí dostávat e-mailová oznámení, pokud jejich zařízení nedodržuje předpisy.

### <a name="2-review-the-end-user-workflow-for-your-chosen-issuer"></a>2) Zkontrolujte pracovní postup koncového uživatele pro zvoleného vystavitele.

Následují klíčové důležité požadavky pro každého podporovaného partnera.  Seznámení s těmito informacemi vám umožní zajistit, aby zásady a konfigurace Intune neblokovaly uživatelům a zařízením možnost úspěšného dokončení registrace pro odvozené přihlašovací údaje od tohoto vystavitele.

#### <a name="disa-purebred"></a>DISA purebred

Zkontrolujte [pracovní postup uživatele pro DISA purebred](https://docs.microsoft.com/user-help/enroll-ios-device-disa-purebred). Mezi klíčové požadavky tohoto pracovního postupu patří:

- Uživatelé potřebují přístup k počítači nebo veřejnému terminálu, kde můžou používat čipovou kartu k ověření vystavitele.

- Zařízení, která se budou registrovat pro odvozené přihlašovací údaje, musí nainstalovat aplikaci Portál společnosti Intune.

- Pomocí Intune [Nasaďte aplikaci DISA purebred](#deploy-the-disa-purebred-app) do zařízení, která se zaregistrují pro odvozené přihlašovací údaje. Tato aplikace se musí nasadit přes Intune, aby se spravovala a pak mohla pracovat s aplikací Portál společnosti Intune. Tuto aplikaci používají uživatelé zařízení k dokončení odvozené žádosti o přihlašovací údaje.

- Aplikace DISA purebred vyžaduje [síť VPN pro jednotlivé aplikace](../configuration/vpn-settings-configure.md) , která zajistí, že aplikace bude mít přístup k DISA purebred během registrace pro odvozené přihlašovací údaje.

- Uživatelé zařízení musí během procesu registrace spolupracovat s živým agentem. Během registrace se uživateli při pokračování v procesu registrace přidávají časově omezená hesla s časovým omezením.

Informace o tom, jak získat a nakonfigurovat aplikaci DISA purebred, najdete v části [nasazení aplikace DISA purebred](#deploy-the-disa-purebred-app) dále v tomto článku.

#### <a name="entrust-datacard"></a>Entrust Datacard

Zkontrolujte [pracovní postup uživatele pro Entrust Datacard](https://docs.microsoft.com/user-help/enroll-ios-device-entrust-datacard). Mezi klíčové požadavky tohoto pracovního postupu patří:

- Uživatelé potřebují přístup k počítači nebo veřejnému terminálu, kde můžou používat čipovou kartu k ověření vystavitele.

- Zařízení, která se budou registrovat pro odvozené přihlašovací údaje, musí nainstalovat aplikaci Portál společnosti Intune.

- Použití kamery zařízení k naskenování kódu QR, který propojuje požadavek na ověření s použitím odvozené žádosti o přihlašovací údaje z mobilního zařízení.

#### <a name="intercede"></a>Intercede

Zkontrolujte [pracovní postup uživatele pro Intercede](https://docs.microsoft.com/user-help/enroll-ios-device-intercede). Mezi klíčové požadavky tohoto pracovního postupu patří:

- Uživatelé potřebují přístup k počítači nebo veřejnému terminálu, kde můžou používat čipovou kartu k ověření vystavitele.

- Zařízení, která se budou registrovat pro odvozené přihlašovací údaje, musí nainstalovat aplikaci Portál společnosti Intune.

- Použití kamery zařízení k naskenování kódu QR, který propojuje požadavek na ověření s použitím odvozené žádosti o přihlašovací údaje z mobilního zařízení.

### <a name="3-deploy-a-trusted-root-certificate-to-devices"></a>3) nasazení důvěryhodného kořenového certifikátu do zařízení

Důvěryhodný kořenový certifikát se používá s odvozenými přihlašovacími údaji k ověření, že je řetěz certifikátů odvozených přihlašovacích údajů platný a důvěryhodný. I když nejsou přímo odkazovány podle zásad, je vyžadován důvěryhodný kořenový certifikát. Viz téma [Konfigurace profilu certifikátu pro vaše zařízení v Microsoft Intune](certificates-configure.md).

### <a name="4-provide-end-user-instructions-for-how-to-get-the-derived-credential"></a>4) poskytněte pokyny pro koncové uživatele, jak získat odvozené přihlašovací údaje.

Vytvořte a poskytněte uživatelům pokyny k tomu, jak spustit odvozený proces registrace přihlašovacích údajů a přejít na odvozený pracovní postup registrace přihlašovacích údajů pro zvoleného vystavitele.

Doporučujeme zadat adresu URL, která bude hostovat vaše doprovodné materiály. Tuto adresu URL zadáte při konfiguraci vystavitele odvozeného pověření pro vašeho tenanta a tato adresa URL je zpřístupněna v rámci aplikace Portál společnosti. Pokud nezadáte svoji vlastní adresu URL, Intune poskytuje odkaz na obecné podrobnosti. Tyto podrobnosti nemůžou pokrýt všechny scénáře a nemusí být pro vaše prostředí správné.

### <a name="5-deploy-intune-policies-that-require-derived-credentials"></a>5) nasazení zásad Intune, které vyžadují odvozenou přihlašovací údaje

Vytvořte nové zásady nebo upravte stávající zásady pro použití odvozených přihlašovacích údajů. Odvozené přihlašovací údaje nahrazují jiné metody ověřování pro ověřování aplikací, Wi-Fi, VPN, e-maily a pro podepisování a šifrování S/MIME.

Vyhněte se vyžadování použití odvozeného pověření pro přístup k procesu, který použijete jako součást procesu k získání odvozeného pověření, protože může uživatelům zabránit v dokončení žádosti.

## <a name="set-up-a-derived-credential-issuer"></a>Nastavení odvozeného vystavitele přihlašovacích údajů

Před vytvořením zásad, které vyžadují použití odvozených přihlašovacích údajů, nastavte vystavitele přihlašovacích údajů v konzole Intune. Odvozený Vystavitel přihlašovacích údajů je nastavení v rámci tenanta. Klienti podporují pouze jednoho vystavitele najednou.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost **Správa tenanta** > **konektory a tokeny** > **odvozených přihlašovacích údajů**.

    > [!div class="mx-imgBorder"]
    > ![nakonfigurovat odvozené přihlašovací údaje v konzole](./media/derived-credentials/configure-provider.png)

3. Zadejte popisný **Zobrazovaný název** pro odvozenou zásadu vystavitele přihlašovacích údajů.  Tento název se nezobrazuje uživatelům zařízení.

4. U **vystavitele odvozeného pověření**vyberte vystavitele odvozeného pověření, které jste si zvolili pro vašeho tenanta:
   - DISA purebred
   - Entrust Datacard
   - Intercede  

5. Zadejte **adresu URL pro odvozenou přihlašovací údaje** , která poskytuje odkaz na umístění, které obsahuje vlastní pokyny, které uživatelům pomůžou získat odvozené přihlašovací údaje pro vaši organizaci. Pokyny by měly být specifické pro vaši organizaci a pracovní postup, který je nezbytný k získání přihlašovacích údajů od zvoleného vystavitele. Odkaz se zobrazí v aplikaci Portál společnosti a měl by být přístupný ze zařízení.

   Pokud nezadáte svoji vlastní adresu URL, Intune poskytuje odkaz na obecné podrobnosti, které nemůžou pokrýt všechny scénáře. Tyto obecné doprovodné materiály nemusí být pro vaše prostředí přesné.

6. Vyberte jednu nebo více možností pro **Typ oznámení**. Typy oznámení jsou metody, které slouží k informování uživatelů o následujících scénářích:

   - Pokud chcete získat nové odvozené přihlašovací údaje, zaregistrujte zařízení pomocí vystavitele.
   - Získejte nové odvozené přihlašovací údaje, když se aktuální přihlašovací údaje blíží k vypršení platnosti.
   - Použijte odvozené přihlašovací údaje se zásadou pro ověřování Wi-Fi, VPN, e-mailu nebo aplikací a pro podepisování a šifrování S/MIME.

7. Až budete připraveni, vyberte **Save (Uložit** ) a dokončete konfiguraci odvozeného vystavitele přihlašovacích údajů.

Po uložení konfigurace můžete provádět změny ve všech polích s výjimkou *odvozeného vystavitele přihlašovacích údajů*.  Informace o změně vystavitele najdete v tématu [Změna odvozeného vystavitele přihlašovacích údajů](#change-the-derived-credential-issuer).

## <a name="deploy-the-disa-purebred-app"></a>Nasazení aplikace DISA purebred

*Tato část platí pouze v případě, že používáte DISA purebred*.

Pokud chcete jako svého odvozeného vystavitele přihlašovacích údajů pro Intune použít **DISA purebred** , musíte získat aplikaci DISA purebred a pak pomocí Intune tuto aplikaci nasadit do zařízení. Uživatelé zařízení používají aplikaci na svém zařízení k vyžádání odvozených přihlašovacích údajů z DISA purebred.

Kromě nasazení aplikace v Intune nakonfigurujte síť VPN Intune na aplikaci pro aplikaci DISA purebred.

**Proveďte následující úlohy**:
  
1. Stáhněte si [aplikaci DISA purebred](https://cyber.mil/pki-pke/purebred/).
2. Nasaďte aplikaci DISA purebred v Intune.  Přečtěte si téma [Přidání obchodní aplikace pro iOS/iPadOS do Microsoft Intune](../apps/lob-apps-ios.md).
3. Pro aplikaci DISA purebred [Vytvořte síť VPN pro jednotlivé aplikace](../configuration/vpn-settings-configure.md) .

## <a name="use-derived-credentials-for-authentication-and-smime-signing-and-encryption"></a>Použití odvozených přihlašovacích údajů pro ověřování a podepisování a šifrování S/MIME

Můžete zadat **odvozená pověření** pro následující typy profilů a účely:

- [Aplikace](#use-derived-credentials-for-app-authentication)
- [E-mail](../configuration/email-settings-ios.md)
- [VPN](../configuration/vpn-settings-ios.md)
- [Podepisování a šifrování S/MIME](certificates-s-mime-encryption-sign.md)
- [Wi-Fi](../configuration/wi-fi-settings-ios.md)

  Pro profily sítě Wi-Fi je *metoda ověřování* dostupná jenom v případě, že je **typ protokolu EAP** nastavený na jednu z následujících hodnot:
  - EAP – TLS
  - EAP-TTLS
  - PEAP

### <a name="use-derived-credentials-for-app-authentication"></a>Použití odvozených přihlašovacích údajů pro ověřování aplikací

Použijte odvozená pověření pro ověřování pomocí certifikátů u webů a aplikací. Postup při doručování odvozených přihlašovacích údajů pro ověřování aplikací:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **odvozená pověření pro profil zařízení s iOS/iPadOS**.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **Platforma**: vyberte **iOS/iPadOS**.
    - **Typ profilu**: vyberte **odvozené přihlašovací údaje**.

4. Výběrem **OK** uložte změny.
5. Po dokončení vyberte **OK** > **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .
6. Vyberte nové > **přiřazení**profilu. Vyberte skupiny, které by měly tuto zásadu přijímat.
 
Uživatelé obdrží aplikaci nebo e-mailové oznámení v závislosti na nastaveních, která jste zadali při vytváření odvozeného vystavitele přihlašovacích údajů. Oznámení informuje uživatele o spuštění Portál společnosti tak, aby bylo možné zpracovat odvozené zásady pověření.

## <a name="renew-a-derived-credential"></a>Obnovení odvozeného pověření

Odvozené přihlašovací údaje se nedají rozšířit ani prodloužit. Místo toho musí uživatelé použít pracovní postup žádosti o přihlašovací údaje k vyžádání nového odvozeného pověření pro zařízení.

Pokud nakonfigurujete jednu nebo více metod pro **Typ oznámení**, Intune automaticky upozorní uživatele, když aktuální odvozené přihlašovací údaje dosáhnou 80% svého životního rozsahu. Oznámení směruje uživatele, aby procházeli procesem žádosti o přihlašovací údaje, aby získal nové odvozené přihlašovací údaje.

Jakmile zařízení obdrží nové odvozené přihlašovací údaje, zásady využívající odvozená pověření se znovu nasadí do daného zařízení.


## <a name="change-the-derived-credential-issuer"></a>Změna odvozeného vystavitele přihlašovacích údajů

Na úrovni tenanta můžete změnit vystavitele přihlašovacích údajů, i když klient v jednom okamžiku podporuje jenom jeden Vystavitel.

Po změně vystavitele se uživatelům zobrazí výzva, aby od nového vystavitele obdržela nové odvozené přihlašovací údaje. Musí tak učinit, aby mohli použít odvozená pověření k ověřování.

### <a name="change-the-issuer-for-your-tenant"></a>Změna vystavitele pro vašeho tenanta

> [!IMPORTANT]  
> Pokud odstraníte vystavitele a ihned znovu nakonfigurujete téhož vystavitele, musíte pořád aktualizovat profily a zařízení, aby se použily odvozené přihlašovací údaje od tohoto vystavitele. Odvozené přihlašovací údaje, které byly získány před odstraněním vystavitele, již nejsou platné.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost **Správa tenanta** > **konektory a tokeny** > **odvozených přihlašovacích údajů**.
3. Vyberte **Odstranit** pro odebrání aktuálního odvozeného vystavitele přihlašovacích údajů.
4. Nakonfigurujte nového vystavitele.

### <a name="update-profiles-that-use-derived-credentials"></a>Aktualizovat profily používající odvozené přihlašovací údaje

Po odstranění vystavitele a přidání nového proveďte úpravu každého profilu, který používá odvozené přihlašovací údaje. Toto pravidlo platí i v případě, že jste obnovili předchozího vystavitele. Jakékoli úpravy profilu aktivují aktualizaci, včetně jednoduchého úprav v *popisu*profilu.

### <a name="update-derived-credentials-on-devices"></a>Aktualizace odvozených přihlašovacích údajů na zařízeních

Po odstranění vystavitele a přidání nového musí uživatel zařízení požádat o nové odvozené přihlašovací údaje. Toto pravidlo platí i v případě, že přidáte téhož vystavitele, který jste odebrali. Proces žádosti o nové odvozené přihlašovací údaje je stejný jako při registraci nového zařízení nebo při obnovení stávajícího přihlašovacího údaje.

## <a name="next-steps"></a>Další kroky

[Vytvořte profily konfigurace zařízení](../configuration/device-profile-create.md).
