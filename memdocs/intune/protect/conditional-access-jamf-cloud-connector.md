---
title: Integrace cloudového konektoru Jamf pro s Microsoft Intune
titleSuffix: Microsoft Intune
description: Pomocí cloudového konektoru Jamf se Microsoft Intune zásadami dodržování předpisů Azure Active Directory podmíněný přístup, který vám umožní integrovat a zabezpečit zařízení spravovaná Jamf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538403"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Použití cloudového konektoru Jamf s Microsoft Intune

Tento článek vám může pomáhat při instalaci konektoru Jamf cloudu pro integraci Jamf pro s Microsoft Intune. Cloudový konektor automatizuje řadu kroků, které jsou nutné při ruční konfiguraci integrace, jak je popsáno v části [integrace Jamf pro s Intune pro dodržování předpisů](../protect/conditional-access-integrate-jamf.md).

Při nastavování cloudového konektoru:

- Nastavení automaticky vytvoří aplikace Jamf pro v Azure a nahradí nutnost jejich ruční konfigurace.
- Můžete integrovat více instancí Jamf pro se stejným klientem Azure, který hostuje vaše předplatné Intune.

Připojení několika instancí Jamf pro s jedním klientem Azure se podporuje jenom v případě, že používáte cloudový konektor. Když použijete ručně nakonfigurované připojení, může se klient Azure integrovat jenom jedna instance Jamf.

Použití cloudového konektoru je volitelné:

- Pro nové klienty, kteří ještě neintegrují s Jamf, se můžete rozhodnout pro konfiguraci cloudového konektoru, jak je popsáno v tomto článku. Případně můžete integraci nakonfigurovat ručně, jak je popsáno v tématu [integrace Jamf pro s Intune pro dodržování předpisů](../protect/conditional-access-integrate-jamf.md) .
- U klientů, kteří už mají ruční konfiguraci, se můžete rozhodnout tuto integraci odebrat a pak nastavit cloudový konektor. Jak odebrat existující integraci a nastavení cloudového konektoru jsou popsány v tomto článku.

Pokud plánujete nahradit předchozí integraci pomocí cloudového konektoru Jamf:

- Pomocí tohoto [postupu můžete odebrat aktuální konfiguraci](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), která zahrnuje odstranění podnikových aplikací pro Jamf pro a zakázání ruční integrace. Pak můžete použít [postup pro konfiguraci cloudového konektoru](#configure-the-cloud-connector-for-a-new-tenant).
- Nebudete muset znovu registrovat zařízení. Zařízení, která THT jsou už zaregistrovaná, můžou používat cloudový konektor bez další konfigurace.
- Nezapomeňte cloudový konektor nakonfigurovat do 24 hodin od odebrání ruční integrace, aby mohla zaregistrovaná zařízení nadále hlásit svůj stav.

Další informace o cloudovém konektoru Jamf najdete v tématu [Konfigurace integrace Intune MacOS pomocí cloudového konektoru](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) v docs.jamf.com.

## <a name="prerequisites"></a>Požadavky

**Produkty a služby**:  
- Jamf pro 10,18 nebo novější
- Uživatelský účet Jamf pro s oprávněními podmíněného přístupu  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Aplikaci Portál společnosti pro macOS](https://aka.ms/macoscompanyportal)
- zařízení macOS s operačním systémem X 10,12 Yosemite nebo novějším

**Síť**:  
Aby bylo možné správně integrovat Jamf a Intune, musí být k dispozici následující porty a koncové body:

- **Intune**: port 443
- **Apple**: porty 2195, 2196 a 5223 (nabízená oznámení do Intune)
- **Jamf**: porty 80 a 5223

- Koncové body:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Aby APNS fungovalo správně v síti, musíte povolit odchozí připojení k a přesměrování z následujících portů:

- Blok Apple 17.0.0.0/8 přes porty TCP 5223 a 443 ze všech klientských sítí.
- Porty 2195 a 2196 ze serverů Jamf pro.

Další informace o těchto portech najdete v následujících článcích:

- [Požadavky na konfiguraci sítě a šířku pásma Intune](../fundamentals/network-bandwidth-use.md).
- [Síťové porty používané službou Jamf pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) v jamf.com.
- [Porty TCP a UDP používané softwarovými produkty společnosti Apple](https://support.apple.com/HT202944) v support.Apple.com

**Účty**:  
Postupy v tomto článku vyžadují použití účtů s následujícími oprávněními:

- **Konzola Jamf pro**: účet s oprávněními pro správu Jamf pro
- **Centrum pro správu Microsoft Endpoint Management**: globální správce
- **Azure Portal**: globální správce

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Odebrat integraci Jamf pro u dřív nakonfigurovaného tenanta

Pomocí následujícího postupu odeberte ručně nakonfigurovanou integraci Jamf pro z vašeho tenanta Azure *předtím, než* budete moct cloudový konektor nakonfigurovat.

Pokud jste ještě nevytvořili připojení mezi Jamf pro a Intune nebo máte jedno nebo víc připojení, která už cloudový konektor používají, přeskočte tento postup a začněte s [konfigurací cloudového konektoru pro nového tenanta](#configure-the-cloud-connector-for-a-new-tenant).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Odebrat ručně nakonfigurovanou integraci Jamf pro

1. Přihlaste se ke konzole Jamf pro.

2. Vyberte **Nastavení** (ikona ozubeného kolečka v pravém horním rohu) a pak přejděte k**podmíněnému přístupu** **globálního řízení** > .

   ![Přejít na podmíněný přístup](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Vyberte **Upravit**.

4. Zrušte zaškrtnutí políčka **Povolit integraci Intune pro MacOS**.

   Pokud zrušíte výběr tohoto nastavení, zakážete připojení, ale uložíte konfiguraci.

5. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a přečtěte si**správu partnerského zařízení** **pro správu** > tenanta.

   V uzlu **Správa partnerského zařízení** odstraňte **ID aplikace** v poli **Zadejte ID aplikace Azure Active Directory pro Jamf** a pak vyberte **Uložit**.

   ID aplikace je ID podnikové aplikace Azure, která se vytvořila v Azure, když nastavíte ruční integraci, pokud Jamf pro.

6. Přihlaste se k [Azure Portal](https://portal.azure.com/) pomocí účtu, který má oprávnění globálního správce, a přejít na **Azure Active Directory** > **podnikové aplikace**.

   Vyhledejte dvě aplikace Jamf a odstraňte je. Nové aplikace se automaticky vytvoří při konfiguraci konektoru Jamf cloudu v dalším postupu.

   ![Vyberte aplikace Jamf, které chcete odstranit.](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Po zakázání integrace v Jamf pro a odstranění podnikových aplikací zobrazí uzel **Správa partnerského zařízení** stav připojení **ukončeno**.

   ![Stav připojení se ukončil.](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Teď, když jste úspěšně odebrali ruční konfiguraci pro integraci Jamf pro, můžete nastavit integraci pomocí cloudového konektoru. Pokud to chcete udělat, přečtěte si téma [Konfigurace cloudového konektoru pro nového tenanta](#configure-the-cloud-connector-for-a-new-tenant) v tomto článku.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Konfigurace cloudového konektoru pro nového tenanta

Následující postup slouží ke konfiguraci konektoru Jamf Cloud pro integraci Jamf pro a Microsoft Intune v těchto případech:

- Nemáte žádnou integraci mezi Jamf pro a Intune nakonfigurovanou pro vašeho tenanta Azure.
- Už máte cloudový konektor nastavený mezi Jamf pro a Intune ve vašem tenantovi Azure a chcete integrovat další instanci Jamf s vaším předplatným.

Pokud teď máte ručně nakonfigurovanou integraci mezi Intune a Jamf pro, přečtěte si téma [Odebrání integrace Jamf pro dřív nakonfigurovaného tenanta](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) v tomto článku, aby se tato integrace odebrala ještě před tím, než budete pokračovat. Předtím, než budete moct úspěšně nastavit Jamf Cloud Connector, se vyžaduje odebrání ručně nakonfigurované integrace.

### <a name="create-a-new-connection"></a>Vytvoření nového připojení

1. Přihlaste se ke konzole Jamf pro.

2. V pravém horním corner0u vyberte **Nastavení** (ikona ozubeného kolečka a pak přejděte na**podmíněný přístup** **globálního řízení** > .

   ![Přejít na podmíněný přístup](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Vyberte **Upravit**.

4. Zaškrtněte políčko **Povolit integraci Intune pro MacOS**.
   - Toto nastavení vyberte, pokud chcete, aby aplikace Jamf pro odesílala aktualizace inventáře Microsoft Intune.
   - Toto nastavení můžete zrušit zaškrtnutím tohoto políčka zakážete připojení, ale uložíte konfiguraci.

   > [!IMPORTANT]
   > Pokud je už vybraná **možnost povolit integraci Intune pro MacOS** a *Typ připojení* je nastavený na **Ruční**, musíte tuto integraci odebrat, než budete pokračovat. Než budete pokračovat, přečtěte si téma [Odebrání integrace s Jamf pro dříve nakonfigurovaného tenanta](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) v tomto článku.

5. V části *Typ připojení*vyberte **cloudový konektor**.

   ![Výběr cloudového konektoru v konzole Jamf pro](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. V místní nabídce **svrchovaného cloudu** vyberte umístění vašeho cloudu z svrchovaného cloudu od Microsoftu.

7. Vyberte jednu z následujících možností na úvodní stránce pro počítače, které nerozpoznají Microsoft Azure:
   - **Výchozí stránka pro registraci zařízení Jamf pro** – v závislosti na stavu zařízení MacOS Tato možnost přesměruje uživatele na portál pro registraci zařízení Jamf pro (pro registraci v Jamf pro) nebo aplikaci Portál společnosti Intune (k registraci v Azure AD).
   - **Stránka odepření přístupu**
   - **Vlastní adresa URL**

8. Vyberte **Connect** (Připojit). Budete přesměrováni a zaregistrujete aplikace Jamf pro v Azure.

   Po zobrazení výzvy zadejte přihlašovací údaje pro Microsoft Azure a podle pokynů na obrazovce udělte požadovaná oprávnění. Udělíte oprávnění pro **cloudový konektor**a znovu pro **aplikaci registrace uživatele cloudového konektoru**. Obě aplikace se registrují v Azure jako podnikové aplikace.

   Po udělení oprávnění pro obě aplikace se otevře stránka **ID aplikace** .

9. Na stránce **ID aplikace** vyberte **Kopírovat a otevřete Intune**.

   ![ID aplikace](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   *ID aplikace* se zkopíruje do systémové schránky pro použití v dalším kroku a otevře se uzel **Správa partnerského zařízení** v *centru pro správu Microsoft Endpoint Manageru* . ( > **Správa partnerského zařízení****správy klientů**).

10. V uzlu **Správa partnerského zařízení** *vložte* **ID aplikace** do pole **Zadejte ID Azure Active Directory aplikace pro Jamf** a pak vyberte **Uložit**.

    ![Konfigurace správy partnerského zařízení](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Vraťte se na stránku ID aplikace v Jamf pro a vyberte **Potvrdit**.

12. Jamf pro se dokončí a otestuje konfiguraci a na stránce nastavení podmíněného přístupu se zobrazí úspěšné nebo neúspěšné připojení. Následující obrázek představuje příklad úspěchu:

    ![Úspěšná konfigurace je potvrzená v Jamf pro.](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. V centru pro správu Microsoft Endpoint Manageru aktualizujte uzel **Správa partnerského zařízení** . Připojení by se teď mělo zobrazovat jako **aktivní**:

    ![Stav připojení je aktivní.](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Po úspěšném navázání spojení mezi Jamf pro a Microsoft Intune odesílá Jamf pro každý počítač, který je zaregistrován ve službě Azure AD, Microsoft Intune informace o inventáři. Stav inventáře podmíněného přístupu můžete zobrazit pro uživatele a počítač v kategorii účet místního uživatele v informacích o inventáři počítače v Jamf pro.

Po integraci jedné instance Jamf pro pomocí cloudového konektoru Jamf můžete stejný postup použít ke konfiguraci dalších instancí Jamf pro se stejným předplatným služby Intune ve vašem tenantovi Azure.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Nastavení zásad dodržování předpisů a registrace zařízení

Po nakonfigurování integrace mezi Intune a Jamf je potřeba [použít zásady dodržování předpisů pro zařízení spravovaná Jamf](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Odpojení služby Jamf pro a Intune

Pokud potřebujete odebrat integraci Jamf pro s Intune, použijte následující postup k odebrání připojení z konzoly Jamf pro. Tyto informace platí pro cloudový konektor i pro ručně nakonfigurovanou integraci.

1. V Jamf pro přejděte do **globálního řízení** > **podmíněný přístup**. Na kartě **integrace MacOS Intune** vyberte **Upravit**.

2. Zrušte zaškrtnutí políčka **Povolit integraci Intune pro MacOS** .

3. Vyberte **Uložit**. Jamf pro pošle vaši konfiguraci do Intune a integrace se ukončí.

4. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Vyberte možnost konektory **správy** > **tenanta a tokeny** > **Správa partnerského zařízení** a ověřte, zda je stav nyní **ukončen**.

   > [!NOTE]
   > Zařízení Mac vaší organizace budou odebrána v den (3 měsíce), který je zobrazený ve vaší konzole.

## <a name="get-support-for-the-cloud-connector"></a>Získat podporu pro cloudový konektor

Vzhledem k tomu, že cloudový konektor automaticky vytvoří podnikovou aplikaci Azure, která je nezbytná pro integraci, měla by být vaše první kontaktní bod pro podporu **Jamf**. Mezi možnosti patří:

- E-mailová podpora na`support@jamf.com`
- Použijte portál podpory na adrese Jamf:https://www.jamf.com/support/ 


Před kontaktováním podpory:

- Zkontrolujte požadavky, jako jsou například porty a verze produktu, které používáte.
- Ověřte, že se nezměnila oprávnění pro následující dvě aplikace Jamf pro vytvořené v Azure. Změny oprávnění aplikací nejsou službou Intune podporované a můžou způsobit selhání integrace.

  **Aplikace pro registraci uživatele cloudového konektoru**:
  - Název rozhraní API: Microsoft Graph
    - Oprávnění: přihlášení a čtení profilu uživatele
    - Typ: delegovaný
    - Uděleno prostřednictvím: souhlas správce
    - Udělil (a): Správce

  **Aplikace cloudového konektoru**:
  - Název rozhraní API: Microsoft Graph (instance 1)
    - Oprávnění: přihlášení a čtení profilu uživatele
    - Typ: delegovaný
    - Uděleno prostřednictvím: souhlas správce
    - Udělil (a): Správce

  - Název rozhraní API: Microsoft Graph (instance 2)
    - Oprávnění: čtení dat adresáře
    - Typ: aplikace
    - Uděleno prostřednictvím: souhlas správce
    - Udělil (a): Správce

  - Název rozhraní API: Intune API
    - Oprávnění: Microsoft Intune pro odeslání atributu zařízení
    - Typ: aplikace
    - Uděleno prostřednictvím: souhlas správce
    - Udělil (a): Správce

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Běžné otázky týkající se cloudového konektoru Jamf

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Jaká data se sdílejí přes cloudový konektor?

Cloudový konektor se ověřuje pomocí Microsoft Azure a odesílá data inventáře zařízení z Jamf pro do Azure. Kromě toho konektor cloudu spravuje zjišťování služeb v Azure, výměně tokenů, chybách komunikace a zotavení po havárii.

### <a name="where-is-device-inventory-data-stored"></a>Kde se ukládají data inventáře zařízení?

Data inventáře zařízení se ukládají v databázi Jamf pro.

### <a name="what-credentials-are-stored"></a>Jaké přihlašovací údaje jsou uložené?

Neukládají se žádné přihlašovací údaje. Při konfiguraci cloudového konektoru musí správci souhlasit s přidáním aplikace Jamf multi-tenant a nativní aplikace macOS Connector do svého tenanta Azure AD. Po přidání víceklientské aplikace vyžádá cloudový konektor přístup k tokenům pro interakci s rozhraním API Azure. Přístup k aplikaci se dá kdykoli odvolat v Microsoft Azure, aby se omezil přístup.

### <a name="how-is-data-encrypted"></a>Jak se šifrují data?

Cloudový konektor používá protokol TLS (Transport Layer Security) pro data odesílaná mezi Jamf pro a Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Jak Jamf ví, ke kterému zařízení je přidružená ta instance Jamf pro?

Jamf pro používá mikroslužby v AWS ke správnému směrování informací o zařízení do správné instance.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Můžu přepínat z použití cloudového konektoru na typ ručního připojení?

Ano. Typ připojení můžete změnit zpátky na ruční a postupovat podle pokynů k ruční instalaci. Pokud máte nějaké otázky, měli byste je směrovat na Jamf, kde najdete pomoc.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Změnila se oprávnění pro jednu nebo obě požadované aplikace (*cloudový konektor* a *aplikace pro registraci uživatelů cloudového*konektoru) a registrace nefunguje, je tato podpora?

Změna oprávnění pro aplikace není podporovaná.

## <a name="next-steps"></a>Další kroky

- [Použití zásad dodržování předpisů pro zařízení spravovaná aplikací Jamf](../protect/conditional-access-assign-jamf.md)
- [Data Jamf odesílají do Intune.](../protect/data-jamf-sends-to-intune.md)
