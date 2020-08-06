---
title: Řešení potíží při registraci zařízení
titleSuffix: Microsoft Intune
description: Návrhy pro řešení potíží s registrací zařízení v Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/09/2018
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6982ba0e-90ff-4fc4-9594-55797e504b62
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic;seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87f81c9f33fd267bcd57a14b59c88d36a937fecd
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865818"
---
# <a name="troubleshoot-device-enrollment-in-microsoft-intune"></a>Řešení potíží při registraci zařízení v Microsoft Intune

Tento článek popisuje návrhy pro řešení potíží s registrací [zařízení](device-enrollment.md) . Pokud tyto informace váš problém nevyřeší, přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md), ve kterém najdete další způsoby, jak získat nápovědu.

## <a name="initial-troubleshooting-steps"></a>První kroky při řešení potíží

Než začnete řešit potíže, ujistěte se, že jste správně nakonfigurovali Intune pro povolení registrace. Můžete si prostudovat informace o těchto požadavcích na konfiguraci:

- [Příprava registrace zařízení v Microsoft Intune](../fundamentals/setup-steps.md)
- [Nastavení správy zařízení s iOS/iPadOS a Mac](ios-enroll.md)
- [Nastavení správy pro zařízení Windows](windows-enroll.md)
- [Nastavení správy zařízení s Androidem](android-enroll.md) – nejsou třeba žádné další kroky

Můžete také zkontrolovat správné nastavení času a data na zařízení uživatele:

1. Restartujte zařízení.
2. Zkontrolujte, že nastavení času a data se přibližně shoduje s časem GMT (interval -12 až +12 hodin vzhledem k času GMT, podle časového pásma koncového uživatele).
3. Odinstalujte a znovu nainstalujte Portál společnosti Intune (pokud se používá).

Uživatelé spravovaných zařízení můžou pro vaši potřebu shromažďovat protokoly registrace a diagnostiky. Pokyny pro uživatele ke shromažďování protokolů najdete tady:

- [Odeslání chyb registrace zařízení s Androidem správci IT](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-using-cable-android)
- [Odeslání chyb iOS/iPadOS správci IT](https://docs.microsoft.com/mem/intune/user-help/send-errors-to-your-it-admin-ios)


## <a name="general-enrollment-issues"></a>Obecné problémy s registrací
K těmto problémům může docházet na všech platformách zařízení.

### <a name="device-cap-reached"></a>Dosáhlo se maximálního počtu zařízení
**Problém:** Uživatel obdrží při registraci chybu (například **portál společnosti dočasně nedostupné**).

**Rozhodnutí**

#### <a name="check-number-of-devices-enrolled-and-allowed"></a>Kontrola počtu zaregistrovaných a povolených zařízení

Podle následujícího postupu zkontrolujte, jestli nemá uživatel přiřazeno více zařízení, než je maximální povolený počet:

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **omezení registrace**  >  **zařízení omezení limitu**. Poznamenejte si hodnotu uvedenou ve sloupci **Limit počtu zařízení**.

2. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zvolte **Uživatelé**  >  **Všichni uživatelé** > vyberte **zařízení**> uživatele. Poznamenejte si počet zařízení.

3. Pokud se počet zaregistrovaných zařízení, která se už shodují s omezením limitu počtu zařízení, nemůžou zaregistrovat, dokud:
    - [nebudou odebrána existující zařízení](../remote-actions/devices-wipe.md), nebo
    - nezvýšíte limit počtu zařízení [nastavením omezení zařízení](enrollment-restrictions-set.md).

Pokud se chcete vyhnout dosažení limitu počtu zařízení, nezapomínejte odebírat zastaralá zařízení.

> [!NOTE]
> 
> Limitu registrace zařízení se můžete vyhnout tak, že použijete účet správce registrace zařízení, jak je popsáno v tématu [Registrace firemních zařízení pomocí správce registrace zařízení v Microsoft Intune](device-enrollment-manager-enroll.md).
> 
> Pokud se pro přihlašovací údaje uživatele, jehož účet přidáte do účtu správců registrace zařízení, vynucuje zásada podmíněného přístupu, nebude možné dokončit registraci.

### <a name="company-portal-temporarily-unavailable"></a>Portál společnosti není dočasně k dispozici
**Problém:** Uživateli se na zařízení zobrazí chyba **Portál společnosti není dočasně k dispozici**.

**Rozhodnutí**

1. Odeberte ze zařízení aplikaci Portál společnosti Intune.

2. V zařízení otevřete prohlížeč, přejděte na [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) adresu a zkuste přihlášení uživatele.

3. Pokud se uživateli nepodaří přihlásit se, měl by zkusit jinou síť.

4. Pokud se to nepovede, ověřte, jestli se přihlašovací údaje uživatele správně synchronizovaly s Azure Active Directory.

5. Pokud se uživatel úspěšně přihlásí, zařízení se systémem iOS/iPadOS vás vyzve k instalaci aplikace Portál společnosti Intune a registraci. Na zařízení s Androidem budete muset aplikaci Portál společnosti Intune nainstalovat ručně. Potom se můžete zkusit znovu zaregistrovat.

### <a name="mdm-authority-not-defined"></a>Není definována autorita MDM
**Problém:** Zobrazí se chyba **Není definována autorita MDM**.

**Rozhodnutí**

1. Ověřte, že je [správně nastavená](../fundamentals/mdm-authority-set.md) autorita MDM.
    
2. Ověřte, že přihlašovací údaje uživatele byly správně synchronizovány s Azure Active Directory. Můžete ověřit, že hlavní název uživatele (UPN) odpovídá informacím služby Active Directory v centru pro správu Microsoft 365.
    Pokud hlavní název uživatele neodpovídá údajům služby Active Directory:

    1. Vypněte na místním serveru službu DirSync.

    2. Odstraňte neodpovídajícího uživatele ze seznamu uživatelů na **portálu účtů Intune** .

    3. Počkejte zhruba hodinu, aby měla služba Azure dost času odebrat nesprávná data.

    4. Znovu zapněte službu DirSync a zkontrolujte, jestli je teď uživatel správně synchronizovaný.

### <a name="unable-to-create-policy-or-enroll-devices-if-the-company-name-contains-special-characters"></a>Pokud název společnosti obsahuje speciální znaky, není možné vytvořit zásadu ani registrovat zařízení
**Problém:** Nemůžete vytvořit zásadu nebo zaregistrovat zařízení.

**Řešení:** V [centru pro správu Microsoft 365](https://admin.microsoft.com/)odstraňte speciální znaky z názvu společnosti a uložte informace o společnosti.

### <a name="unable-to-sign-in-or-enroll-devices-when-you-have-multiple-verified-domains"></a>Pokud máte více ověřených domén, není možné se přihlásit nebo zaregistrovat zařízení
**Problém:** Když do AD FS přidáte druhou ověřenou doménu, můžou se vyskytnout potíže. Uživatelé s příponou hlavního názvu uživatele (UPN) druhé domény nemusí být schopni přihlásit se na portály nebo zaregistrovat zařízení.


<strong>Řešení:</strong> Zákazníci s předplatným Microsoft Office 365 musí pro každou příponu nasadit samostatnou instanci federační služby AD FS 2.0, pokud:
- používají jednotné přihlašování (SSO) prostřednictvím služby AD FS 2.0 a
- mají pro přípony UPN uživatelů v rámci své organizace více domén nejvyšší úrovně (například @contoso.com nebo @fabrikam.com).


[Kumulativní aktualizace pro službu AD FS 2.0](https://support.microsoft.com/kb/2607496) ve spojení s přepínačem <strong>SupportMultipleDomain</strong> umožňuje zajistit, aby server AD FS podporoval tento scénář bez vyžadování dalších serverů služby AD FS 2.0. Další informace najdete v [tomto blogu](https://blogs.technet.microsoft.com/abizerh/2013/02/05/supportmultipledomain-switch-when-managing-sso-to-office-365/).


## <a name="android-issues"></a>Problémy na zařízeních s Androidem

### <a name="android-enrollment-errors"></a>Chyby registrace zařízení s Androidem

Následující tabulka obsahuje chyby, které se můžou koncovým uživatelům zobrazit při registraci zařízení s Androidem v Intune.

|Chybová zpráva|Problém|Řešení|
|---|---|---|
|**Správce IT musí přiřadit licence pro přístup**<br>Váš správce IT vám neudělil přístup k této aplikaci. Požádejte ho o pomoc nebo to zkuste znovu později.|Zařízení není možné zaregistrovat, protože účet uživatele nemá potřebnou licenci.|Aby si mohli uživatelé zaregistrovat svoje zařízení, musí mít přiřazenou potřebnou licenci. Tato zpráva znamená, že uživatel má špatný typ licence pro danou autoritu pro správu mobilních zařízení. Uživatelům se tato chyba například zobrazí, pokud platí obě následující podmínky:<ol><li>Jako autorita pro správu mobilních zařízení je nastavená služba Intune.</li><li>Uživatel používá licenci nástroje System Center 2012 R2 Configuration Manager.</li></ol>Přečtěte si informace o tom, jak [přiřadit licence Intune k uživatelským účtům](/intune/licenses-assign).|
|**Správce IT musí nastavit autoritu MDM.**<br>Zdá se, že váš správce IT nenastavil autoritu MDM. Požádejte ho o pomoc nebo to zkuste znovu později.|Autorita pro správu mobilních zařízení není definovaná.|Autorita pro správu mobilních zařízení není v Intune nastavená. Přečtěte si, jak [nastavit autoritu pro správu mobilních zařízení](/intune/mdm-authority-set).|


### <a name="devices-fail-to-check-in-with-the-intune-service-and-display-as-unhealthy-in-the-intune-admin-console"></a>Zařízení se nepodařilo registrovat ve službě Intune a jeho stav v konzole pro správu se zobrazuje jako Není v pořádku
**Problém:** Některá zařízení Samsung s Androidem verze 4.4.x a 5.x můžou ukončit registraci ve službě Intune. Pokud se zařízení nezaregistrují, platí pro ně tyto podmínky:

- Nemůžou přijímat zásady, aplikace a vzdálené příkazy ze služby Intune.
- V konzole pro správu se jako stav správy zobrazuje **Není v pořádku**.
- Uživatelé, kteří jsou chráněni zásadami podmíněného přístupu, můžou ztratit přístup k podnikovým prostředkům.

Software Samsung Smart Manager, který se dodává s některými zařízeními Samsung, může deaktivovat Portál společnosti Intune a jeho součásti. Když je Portál společnosti v neaktivním stavu, nemůže běžet na pozadí a nemůže kontaktovat službu Intune.

**#1 řešení:**

Řekněte uživatelům, aby aplikaci Portál společnosti spouštěli ručně. Po restartování aplikace se zařízení zaregistruje pomocí služby Intune.

> [!IMPORTANT]
> Ruční spuštění aplikace Portál společnosti je dočasné řešení, protože Samsung Smart Manager může aplikaci Portál společnosti znovu deaktivovat.

**#2 řešení:**

Řekněte uživatelům, aby se pokusili upgradovat na Android 6.0. Problém s deaktivací neplatí pro zařízení s Androidem 6.0. Pokud chcete zjistit, jestli je aktualizace k dispozici, přejděte na **Nastavení**  >  **o**  >  **ručním stažení aktualizací** zařízení > postupujte podle pokynů.

**#3 řešení:**

Pokud řešení 2 nefunguje, nechte uživatele provést následující postup, aby Smart Manager vyloučil aplikaci Portál společnosti:

1. Na zařízení spusťte aplikaci Smart Manager.

   ![Výběr ikony Smart Manager na zařízení](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-icon.png)

2. Zvolte dlaždici **Battery** (Baterie).

   ![Výběr dlaždice Battery](./media/troubleshoot-device-enrollment-in-intune/smart-manager-battery-tile.png)

3. V části **App power saving** (Úspora energie aplikace) nebo **App optimization** (Optimalizace aplikace) vyberte **Detail** (Podrobnosti).

   ![Výběr možnosti Detail (Podrobnosti) v části App power saving (Úspora energie aplikace) nebo App optimization (Optimalizace aplikace)](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-power-saving-detail.png)

4. V seznamu aplikací vyberte **Portál společnosti**.

   ![Výběr aplikace Portál společnosti ze seznamu aplikací](./media/troubleshoot-device-enrollment-in-intune/smart-manager-company-portal.png)

5. Zvolte **Turned off** (Vypnuto).

   ![Výběr možnosti Turned off (Vypnuto) v dialogovém okně App optimization (Optimalizace aplikace)](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-optimization-turned-off.png)

6. V části **App power saving** (Snížení spotřeby aplikace) nebo **App optimization** (Optimalizace aplikace) ověřte, že je Portál společnosti vypnutý.

   ![Ověření, že je Portál společnosti vypnutý](./media/troubleshoot-device-enrollment-in-intune/smart-manager-verify-comp-portal-turned-off.png)


### <a name="profile-installation-failed"></a>Neúspěch instalace profilu
**Problém:** Na zařízení s Androidem se zobrazí chybová zpráva **Instalace profilu se nezdařila**.

**Rozhodnutí**

1. Zkontrolujte, jestli má uživatel přiřazenou příslušnou licenci pro verzi služby Intune, kterou používáte.

2. Zkontrolujte, jestli už zařízení není zaregistrované pomocí jiného poskytovatele správy mobilních zařízení (MDM).

3. Zkontrolujte, jestli už v zařízení není nainstalovaný profil správy.

4. Potvrďte, že Chrome pro Android je výchozím prohlížečem a že jsou povolené soubory cookie.

### <a name="android-certificate-issues"></a>Problémy s certifikáty Androidu

**Problém:** Uživatelům se na zařízení zobrazí následující zpráva: *Nemůžete se přihlásit, protože vašemu zařízení chybí požadovaný certifikát.*

**Řešení 1**:

Uživatel možná bude moct načíst chybějící certifikát podle pokynů v tématu [Zařízení nemá požadovaný certifikát](../user-help/your-device-is-missing-an-IT-required-certificate-android.md). Pokud chyba přetrvává, vyzkoušejte Řešení 2.

**Řešení 2**:

Uživatelům se může po tom, co zadali svoje podnikové přihlašovací údaje a byli přesměrováni na federované přihlašování, nadále zobrazovat chyba chybějícího certifikátu. V tom případě může tato chyba znamenat, že na vašem serveru Active Directory Federation Services (AD FS) chybí zprostředkující certifikát.

Příčinou chyby certifikátu je, že zařízení s Androidem vyžadují zahrnutí zprostředkujících certifikátů do odpovědi [SSL Server hello](https://technet.microsoft.com/library/cc783349.aspx). Momentálně výchozí instalace serveru AD FS nebo proxy serveru WAP – AD FS odesílá v odpovědi SSL Server hello na zprávu SSL Client hello jenom certifikát SSL služby AD FS.

Pokud chcete problém vyřešit, naimportujte certifikáty do osobních certifikátů počítačů na serveru nebo proxy serverech AD FS následujícím způsobem:

1. Na serverech ADFS a proxy serveru klikněte pravým tlačítkem na **Start**  >  **Spustit**  >  **Certlm. msc** a spusťte konzolu pro správu certifikátů místního počítače.
2. Rozbalte **Osobní** a zvolte **Certifikáty**.
3. Najděte certifikát pro vaši komunikaci služby AD FS (veřejně podepsaný certifikát) a poklikáním zobrazte jeho vlastnosti.
4. Vyberte kartu **cesta** k certifikátu pro zobrazení nadřazených certifikátů certifikátu/s.
5. U každého nadřazeného certifikátu zvolte **Zobrazit certifikát**.
6. Zvolit **Podrobnosti**  >  **Kopírovat do souboru...**
7. Postupujte podle pokynů průvodce a exportujte nebo uložte veřejný klíč nadřazeného certifikátu do zvoleného umístění souboru.
8. Klikněte pravým tlačítkem na **certifikáty**  >  **všechny úkoly**  >  **importovat**.
9. Postupujte podle pokynů průvodce a naimportujte nadřazené certifikáty do **Místní počítač\Osobní\Certifikáty**.
10. Restartujte servery AD FS.
11. Výše uvedené kroky zopakujte na všech serverech a proxy serverech AD FS.

K ověření správné instalace certifikátu můžete použít diagnostický nástroj, který je k dispozici na [https://www.digicert.com/help/](https://www.digicert.com/help/) . Do pole **Adresa serveru** zadejte plně kvalifikovaný název domény serveru ADFS (IE: STS.contso.com) a klikněte na **ověřit server**.

**Pokud chcete ověřit, jestli se certifikát správně nainstaloval**:

Následující kroky popisují jednom jeden z mnoha způsobů a nástrojů, pomocí kterých můžete ověřit, jestli se certifikát správně nainstaloval.

1. Přejděte na [bezplatný nástroj Digicert](https://www.digicert.com/help/).
2. Zadejte plně kvalifikovaný název domény AD FS serveru (například sts.contoso.com) a vyberte možnost **ověřit server**.

Pokud je certifikát serveru správně nainstalovaný, uvidíte ve výsledcích všechny značky zaškrtnutí. Pokud výše uvedený problém existuje, zobrazí se v části sestava "název certifikátu odpovídá" červené X "a" certifikát SSL je správně nainstalován ".


## <a name="iosipados-issues"></a>problémy s iOS/iPadOS

### <a name="iosipados-enrollment-errors"></a>chyby registrace pro iOS/iPadOS
Následující tabulka obsahuje chyby, které se můžou koncovým uživatelům zobrazit při registraci zařízení se systémem iOS nebo iPadOS v Intune.

|Chybová zpráva|Problém|Řešení|
|-------------|-----|----------|
|NoEnrollmentPolicy|Nepovedlo se najít žádné zásady registrace|Ověřte, že jsou nastavené všechny požadavky na registraci, jako je třeba certifikát Apple Push Notification Service (APNs), a že je povolená možnost iOS/iPadOS jako platforma. Pokyny najdete v tématu [Nastavení správy zařízení se systémy iOS/iPadOS a Mac](ios-enroll.md).|
|DeviceCapReached|Už máte příliš mnoho registrovaných mobilních zařízení.|Než bude moct uživatel zaregistrovat další mobilní zařízení, musí odebrat jedno ze svých aktuálně zaregistrovaných mobilních zařízení z Portálu společnosti. Přečtěte si pokyny pro typ zařízení, které používáte: [Android](../user-help/unenroll-your-device-from-intune-android.md), [iOS/iPadOS](../user-help/unenroll-your-device-from-intune-ios.md), [Windows](../user-help/unenroll-your-device-from-intune-windows.md).|
|APNSCertificateNotValid|Došlo k potížím s certifikátem, který umožňuje komunikaci mobilního zařízení s podnikovou sítí.<br /><br />|Apple Push Notification Service (APNs) poskytuje kanál pro kontaktování registrovaných zařízení se systémem iOS/iPadOS. Registrace bude neúspěšná a zobrazí se tato zpráva, pokud:<ul><li>kroky k získání certifikátu APNs nebyly provedeny, nebo</li><li>platnost certifikátu APNs vypršela.</li></ul>Přečtěte si informace o nastavení uživatelů v tématu [Synchronizace služby Active Directory a přidání uživatelů do Intune](../fundamentals/users-add.md) a článku o [uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).|
|AccountNotOnboarded|Došlo k potížím s certifikátem, který umožňuje komunikaci mobilního zařízení s podnikovou sítí.<br /><br />|Apple Push Notification Service (APNs) poskytuje kanál pro kontaktování registrovaných zařízení se systémem iOS/iPadOS. Registrace bude neúspěšná a zobrazí se tato zpráva, pokud:<ul><li>kroky k získání certifikátu APNs nebyly provedeny, nebo</li><li>platnost certifikátu APNs vypršela.</li></ul>Další informace najdete v [Microsoft Intune nastavení správy pro iOS/iPadOS a Mac pomocí](ios-enroll.md).|
|DeviceTypeNotSupported|Uživatel se možná pokusil o registraci zařízení s jiným systémem než iOS. Typ mobilního zařízení, které se pokoušíte registrovat, není podporovaný.<br /><br />Potvrďte, že na zařízení běží iOS/iPadOS verze 8,0 nebo novější.<br /><br />|Ujistěte se, že na zařízení uživatele běží iOS/iPadOS verze 8,0 nebo novější.|
|UserLicenseTypeInvalid|Zařízení nemůžete zaregistrovat, protože uživatelský účet ještě není členem požadované skupiny uživatelů.<br /><br />|Uživatelé můžou svoje zařízení registrovat až potom, co se stanou členy správné skupiny uživatelů. Tato zpráva znamená, že uživatel má špatný typ licence pro danou autoritu pro správu mobilních zařízení. Uživatelům se tato chyba například zobrazí, pokud platí obě následující podmínky:<ol><li>Jako autorita pro správu mobilních zařízení je nastavená služba Intune.</li><li>Uživatel používá licenci nástroje System Center 2012 R2 Configuration Manager.</li></ol>Další informace najdete v následujících článcích:<br /><br />Přečtěte si téma [Nastavení správy pro iOS/iPadOS a Mac pomocí Microsoft Intune](ios-enroll.md) a informací o nastavení uživatelů v tématu [synchronizace služby Active Directory a přidání uživatelů do Intune](../fundamentals/users-add.md) a [uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).|
|MdmAuthorityNotDefined|Autorita pro správu mobilních zařízení není definovaná.<br /><br />|Autorita pro správu mobilních zařízení není v Intune nastavená.<br /><br />Projděte si položku č. 1 v části „Krok 6: Registrace mobilních zařízení a instalace aplikace“ v tématu [Začínáme s 30denní zkušební verzí Microsoft Intune](../fundamentals/free-trial-sign-up.md).|

### <a name="devices-are-inactive-or-the-admin-console-cant-communicate-with-them"></a>Zařízení nejsou aktivní nebo s nimi nemůže konzola správce komunikovat
**Problém:** zařízení s iOS/iPadOS se nevrací se změnami ve službě Intune. Zařízení se musí pravidelně registrovat ve službě, aby si zachovala přístup ke chráněným podnikovým prostředkům. Pokud se zařízení nezaregistrují, platí pro ně tyto podmínky:

- Nemůžou přijímat zásady, aplikace a vzdálené příkazy ze služby Intune.
- V konzole pro správu se jako stav správy zobrazuje **Není v pořádku**.
- Uživatelé, kteří jsou chráněni zásadami podmíněného přístupu, můžou ztratit přístup k podnikovým prostředkům.

**Řešení:** Podělte se s koncovými uživateli o následující řešení, která jim pomůžou znovu získat přístup k podnikovým prostředkům.

Když uživatelé spustí aplikaci Portál společnosti pro iOS/iPadOS, může zjistit, jestli zařízení ztratilo kontakt s Intune. Pokud aplikace zjistí, že zařízení nemá kontakt, pokusí se automaticky synchronizovat s Intune a znovu se připojit (uživateli se zobrazí zpráva **Probíhá pokus o synchronizaci...**). ).

  ![Oznámení Probíhá pokus o synchronizaci](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_trying_to_sync_notification.png)

Pokud je synchronizace úspěšná, zobrazí se v aplikaci iOS/iPadOS Portál společnosti **úspěšné** vložení vloženého oznámení, které indikuje, že je vaše zařízení v dobrém stavu.

  ![Oznámení Úspěšná synchronizace](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_sync_successful_notification.png)

Pokud synchronizace neproběhne úspěšně, uživatelé uvidí oznámení, že v aplikaci pro iOS/iPadOS Portál společnosti aplikace **nedokáže synchronizovat** vložené oznámení.

  ![Oznámení Nelze synchronizovat](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_unable_to_sync_notification.png)

Pokud chcete problém opravit, musíte vybrat tlačítko **Nastavit**, které se nachází vpravo od oznámení **Nelze synchronizovat**. Po výběru tlačítka Nastavit se zobrazí obrazovka pro nastavení firemního přístupu, kde můžete podle zobrazovaných pokynů zaregistrovat zařízení.

  ![Obrazovka Nastavení firemního přístupu](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_company_access_setup.png)

Po registraci se zařízení vrátí do stavu správné funkce a znovu získá přístup k podnikovým prostředkům.

### <a name="verify-ws-trust-13-is-enabled"></a>Ověření, že koncový bod WS-Trust 1.3 je povolený
**Problém** Automatické registrace zařízení (ADE) zařízení s iOS/iPadOS nejde zaregistrovat.

Registrace zařízení ADE s přidružením uživatele vyžaduje, aby bylo povoleno zadání uživatelského jména/smíšeného koncového bodu WS-Trust 1,3, aby bylo možné žádat o tokeny uživatelů. Active Directory má tento koncový bod ve výchozím nastavení povolený. Seznam povolených koncových bodů získáte použitím rutiny PowerShellu Get-AdfsEndpoint a vyhledáním koncového bodu trust/13/UsernameMixed. Příklad:

```powershell
Get-AdfsEndpoint -AddressPath "/adfs/services/trust/13/UsernameMixed"
```

Další informace najdete v [dokumentaci k rutině Get-AdfsEndpoint](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

Další informace najdete v tématu [Doporučené postupy zabezpečení služby AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/best-practices-securing-ad-fs). Získání pomoci při určování, jestli máte koncový bod WS-Trust 1.3 Username/Mixed ve svém zprostředkovateli identity federace povolený:
- Pokud používáte službu ADFS, obraťte se na podporu Microsoftu.
- Obraťte se na poskytovatele identity třetí strany.


### <a name="profile-installation-failed"></a>Neúspěch instalace profilu
**Problém:** Uživateli se zobrazí chyba **Instalace profilu se nezdařila** v zařízení se systémem iOS/iPadOS.

### <a name="troubleshooting-steps-for-failed-profile-installation"></a>Postup řešení potíží při neúspěšné instalaci profilu

1. Zkontrolujte, jestli má uživatel přiřazenou příslušnou licenci pro verzi služby Intune, kterou používáte.

2. Zkontrolujte, jestli už zařízení není zaregistrované pomocí jiného poskytovatele správy mobilních zařízení (MDM).

3. Zkontrolujte, jestli už v zařízení není nainstalovaný profil správy.

4. [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com)Po zobrazení výzvy přejděte na adresu a pokuste se nainstalovat profil.

5. Potvrďte, že je prohlížeč Safari pro iOS/iPadOS výchozím prohlížečem a že jsou soubory cookie povolené.

### <a name="users-iosipados-device-is-stuck-on-an-enrollment-screen-for-more-than-10-minutes"></a>Zařízení iOS/iPadOS uživatele se zablokuje na obrazovce pro registraci po dobu delší než 10 minut.

**Problém**: Při registraci zařízení může dojít k uvíznutí na některé z těchto dvou obrazovek:
- Čeká se na konečnou konfiguraci od "Microsoft".
- Aplikace Asistovaný přístup není k dispozici. Obraťte se prosím na správce.

Tento problém může nastat, když:
- dojde k dočasnému výpadku služeb Apple, nebo
- registrace zařízení s iOS/iPadOS je nastavená tak, aby používala tokeny VPP, jak je znázorněno v tabulce, ale v tokenu VPP je něco špatného.

| Nastavení registrace | Hodnota |
| ---- | ---- |
| Platforma | iOS/iPadOS |
| Spřažení uživatele | Zaregistrovat s přidružením uživatele |
|Ověřit na Portálu společnosti místo v Průvodci nastavením Applu | Ano |
| Nainstalovat Portál společnosti pomocí VPP | Použít token: adresa tokenu |
| Spustit Portál společnosti v režimu Jedna aplikace, dokud neproběhne ověření | Ano |

**Řešení**: Pokud chcete tento problém odstranit, je nutné provést tyto akce:
1. Určení, jestli je s tokenem VPP něco v nepořádku, a případná oprava tokenu VPP
2. Identifikace zařízení, která jsou blokovaná
3. Vymazání ovlivněných zařízení
4. Předání pokynu uživateli, aby proces registrace znovu zahájil

#### <a name="determine-if-theres-something-wrong-with-the-vpp-token"></a>Určení, jestli je s tokenem VPP něco v nepořádku
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS**  >  **tokeny programu registrace** > název tokenu > **profily** > název profilu > **Spravovat**  >  **vlastnosti**.
2. Zkontrolujte vlastnosti, abyste zjistili, jestli se zobrazují nějaké chyby, které se podobají těmto:
    - Platnost tohoto tokenu vypršela.
    - Na tento token se nevztahují licence pro Portál společnosti.
    - Tento token používá jiná služba.
    - Tento token používá jiný tenant.
    - Tento token se odstranil.
3. Odstraňte problémy s tokenem.

#### <a name="identify-which-devices-are-blocked-by-the-vpp-token"></a>Identifikace zařízení, která token VPP blokuje
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**k > **iOS enrollment**  >  **tokeny programu registrace** iOS > název tokenu > **zařízení**.
2. Vyfiltrujte sloupec **Stav profilu** podle hodnoty **Blokováno**.
3. Poznamenejte si sériová čísla všech zařízení s hodnotou **Blokováno**.

#### <a name="remotely-wipe-the-blocked-devices"></a>Vzdálené vymazání blokovaných zařízení
Po dokončení řešení problémů s tokenem VPP musíte zařízení, která jsou blokovaná, vymazat.
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **všechna zařízení**  >  **Columns**  >  .**sériové číslo**se  >  **vztahuje**. 
2. Každé blokované zařízení vyberte v seznamu **Všechna zařízení** a zvolte **Vymazání** > **Ano**.

#### <a name="tell-the-users-to-restart-the-enrollment-process"></a>Předání pokynu uživatelům, aby proces registrace znovu zahájili
Po vymazání blokovaných zařízení můžete uživatelům předat pokyn, aby proces registrace znovu zahájili.

## <a name="macos-issues"></a>Problémy s macOS

### <a name="macos-enrollment-errors"></a>Chyby registrace zařízení s macOS
**Chybová zpráva 1:** vypadá to, že *používáte virtuální počítač. Ujistěte se, že jste plně nakonfigurovali svůj virtuální počítač, včetně sériového čísla a hardwarového modelu. Pokud se nejedná o virtuální počítač, obraťte se prosím na podporu.*  

**Chybová zpráva 2:** máme *problémy s tím, jak vaše zařízení spravuje. K tomuto problému může dojít, pokud používáte virtuální počítač, máte omezené sériové číslo, nebo pokud je toto zařízení již přiřazeno někomu jinému. Zjistěte, jak tyto problémy vyřešit, nebo se obraťte na firemní podporu.*

**Problém:** Příčinou této zprávy může být některý z následujících důvodů:  
- Virtuální počítač s macOS není správně nakonfigurovaný.  
- Povolili jste omezení zařízení, která vyžadují, aby zařízení bylo ve firemním vlastnictví nebo mělo v Intune zaregistrované sériové číslo.  
- Zařízení už je zaregistrované a je v Intune pořád přiřazené k někomu jinému.  

**Řešení:** Napřed se obraťte na uživatele a zjistěte, které problémy ovlivňují jeho zařízení. Pak proveďte nejvhodnější z následujících řešení:

- Pokud uživatel registruje virtuální počítač kvůli testování, ověřte, že je plně nakonfigurovaný, aby služba Intune dokázala rozpoznat jeho sériové číslo a model hardwaru. Přečtěte si další informace o tom, jak v Intune [nastavit virtuální počítače](macos-enroll.md#enroll-virtual-macos-machines-for-testing).
- Pokud má vaše organizace zapnuté omezení registrace, které blokuje osobní zařízení s macOS, musíte do Intune ručně [přidat sériové číslo osobního zařízení](corporate-identifiers-add.md#manually-enter-corporate-identifiers).  
- Pokud je zařízení v Intune pořád přiřazené k jinému uživateli, nepoužil jeho předchozí vlastník aplikaci Portál společnosti, aby ho odebral nebo obnovil tovární nastavení. Záznam zastaralého zařízení vyčistíte v Intune takto:  

    1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)se přihlaste pomocí přihlašovacích údajů pro správu.
    2. Vyberte **zařízení**  >  **všechna zařízení**.  
    3. Najděte zařízení s problematickou registrací. Výsledky můžete upřesnit hledáním podle názvu zařízení nebo adresy MAC/hardwaru.
    4. Vyberte toto zařízení > **Odstranit**. Odstraňte všechny ostatní záznamy spojené s tímto zařízením.  

## <a name="pc-issues"></a>Problémy na počítači

|Chybová zpráva|Problém|Řešení|
|---|---|---|
|**Správce IT musí přiřadit licence pro přístup**<br>Váš správce IT vám neudělil přístup k této aplikaci. Požádejte ho o pomoc nebo to zkuste znovu později.|Zařízení není možné zaregistrovat, protože účet uživatele nemá potřebnou licenci.|Aby si mohli uživatelé zaregistrovat svoje zařízení, musí mít přiřazenou potřebnou licenci. Tato zpráva znamená, že uživatel má špatný typ licence pro danou autoritu pro správu mobilních zařízení. Uživatelům se tato chyba například zobrazí, pokud platí obě následující podmínky: <ol><li>Jako autorita pro správu mobilních zařízení je nastavená služba Intune.</li><li>Uživatel používá licenci nástroje System Center 2012 R2 Configuration Manager.</li></ol>Přečtěte si informace o tom, jak [přiřadit licence Intune k uživatelským účtům](../fundamentals/licenses-assign.md).|

### <a name="the-machine-is-already-enrolled---error-hr-0x8007064c"></a>Počítač už je zaregistrovaný – chyba hr 0x8007064c

**Problém:** Registrace selže s chybou **Počítač už je zaregistrovaný**. V protokolu registrace se zobrazuje chyba **hr 0x8007064c**.

Důvodem může být to, že počítač:

- byl zaregistrován dříve, nebo
- je na něm klonovaná image počítače, který už je zaregistrovaný.
Na počítači se stále nachází certifikát předchozího účtu.

**Rozhodnutí**

1. V nabídce **Start** zadejte **Spustit** -> **MMC**.
1. Vyberte **soubor**  >  **Přidat/odebrat moduly snap-in**.
1. Poklikejte na **Certifikáty**, zvolte **Účet počítače** > **Další** a vyberte **Místní počítač**.
1. Poklikejte na **Certifikáty (místní počítač)** a zvolte **Osobní/Certifikáty**.
1. Vyhledejte certifikát Intune, který vystavila certifikační autorita Sc_Online_Issuing. Pokud existuje, odstraňte ho.
1. Pokud existuje klíč registru **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\OnlineManagement regkey**, odstraňte ho a s ním i všechny podklíče.
1. Zkuste se znovu zaregistrovat.
1. Pokud ani tak není možné počítač zaregistrovat, vyhledejte a odstraňte klíč **KEY_CLASSES_ROOT\Installer\Products\6985F0077D3EEB44AB6849B5D7913E95**, pokud existuje.
1. Zkuste se znovu zaregistrovat.

    > [!IMPORTANT]
    > Tato část, metoda nebo úloha obsahují kroky, které vám pomohou s úpravou registru. Pokud však upravíte registr nesprávně, může dojít k vážným problémům. Proto je důležité, abyste pečlivě postupovali podle těchto kroků. Pro zvýšení ochrany před upravováním registr zálohujte. Pak budete moct v případě problémů registr obnovit.
    > Další informace o tom, jak zálohovat a obnovovat registr, najdete v tématu [Postup zálohování a obnovení registru v systému Windows](https://support.microsoft.com/kb/322756).

## <a name="general-enrollment-error-codes"></a>Obecné kódy chyb registrace

|Kód chyby|Možný problém|Navrhované řešení|
|--------------|--------------------|----------------------------------------|
|0x80CF0437 |Na hodinách klientského počítače není nastavený správný čas.|Zkontrolujte, jestli jsou na klientském počítači správně nastavené hodiny a časové pásmo.|
|0x80240438, 0x80CF0438, 0x80CF402C|Nedá se připojit ke službě Intune. Zkontrolujte nastavení proxy serveru klienta.|Ověřte, že Intune podporuje konfiguraci proxy serveru na klientském počítači. Ověřte, že klientský počítač má přístup na internet.|
|0x80240438, 0x80CF0438|Není nakonfigurované nastavení proxy serveru v Internet Exploreru a v místním systému.|Nedá se připojit ke službě Intune. Zkontrolujte nastavení proxy serveru klienta. Ověřte, že Intune podporuje konfiguraci proxy serveru na klientském počítači. Ověřte, že klientský počítač má přístup na internet.|
|0x80043001, 0x80CF3001, 0x80043004, 0x80CF3004|Registrační balíček je zastaralý.|Z pracovního prostoru Správa si stáhněte aktuální balíček klientského softwaru a nainstalujte ho.|
|0x80043002, 0x80CF3002|Účet je v režimu údržby.|Když je účet v režimu údržby, nemůžete registrovat nové klientské počítače. Pokud si chcete prohlédnout nastavení svého účtu, přihlaste se k němu.|
|0x80043003, 0x80CF3003|Účet je odstraněný.|Ověřte, že je váš účet a předplatné Intune pořád aktivní. Pokud si chcete prohlédnout nastavení svého účtu, přihlaste se k němu.|
|0x80043005, 0x80CF3005|Klientský počítač byl vyřazen z provozu.|Pár hodin počkejte, odeberte z počítače všechny starší verze klientského softwaru s pak zkuste nainstalovat klientský software znova.|
|0x80043006, 0x80CF3006|Bylo dosaženo maximálního počtu licencí povolených pro účet.|Abyste mohli ve službě zaregistrovat další klientské počítače, musí si vaše organizace koupit další licence.|
|0x80043007, 0x80CF3007|Ve složce s instalačním programem se nenašel soubor certifikátu.|Než začnete s instalací, extrahujte všechny soubory. Extrahované soubory nepřejmenovávejte ani nepřesunujte: všechny soubory musí být ve stejné složce, jinak se instalace nepovede.|
|0x8024D015, 0x00240005, 0x80070BC2, 0x80070BC9, 0x80CFD015|Software nejde nainstalovat, protože se čeká na restartování klientského počítače.|Restartujte počítač a pak zkuste nainstalovat klientský software znova.|
|0x80070032|Na klientském počítači se nenašel minimálně jeden softwarový produkt, který je podmínkou pro instalaci klientského softwaru.|Ujistěte se, že jsou na klientském počítači nainstalované všechny požadované aktualizace, a pak zkuste nainstalovat klientský software znova.|
|0x80043008, 0x80CF3008|Nepodařilo se spustit službu Microsoft Online Management Updates.|Kontaktujte podporu podle pokynů v tématu [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).|
|0x80043009, 0x80CF3009|Klientský počítač je ve službě už zaregistrovaný.|Abyste mohli klientský počítač ve službě zaregistrovat znovu, musíte ho nejdřív vyřadit.|
|0x8004300B, 0x80CF300B|Instalační balíček klientského softwaru nejde spustit, protože verze Windows, která běží na klientovi, není podporovaná.|Intune nepodporuje verzi Windows, která běží na klientském počítači.|
|0xAB2|Instalační služba systému Windows nemohla získat přístup k modulu VBScript runtime pro vlastní akci.|Tato chyba je způsobená nějakou vlastní akcí založenou na dynamických knihovnách DLL (Dynamic-Link Library). Při odstraňování potíží s knihovnou DLL budete možná muset použít nástroje, které jsou popsány v [Podpora Microsoftu KB198038: užitečné nástroje pro problémy s balíčkem a nasazením](https://support.microsoft.com/kb/198038).|
|0x80cf0440|Připojení ke koncovému bodu služby bylo ukončeno.|Zkušební nebo placený účet je pozastaven. Vytvořte nový zkušební nebo placený účet a pak opakujte pokus o registraci.|

## <a name="next-steps"></a>Další kroky

Pokud vám tyto informace o řešení potíží nepomohly, obraťte se na podpora Microsoftu, jak je popsáno v tématu [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
