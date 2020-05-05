---
title: Tipy pro řešení potíží pro zásady BitLockeru v Microsoft Intune
titleSuffix: Microsoft Intune
description: Popisuje, jak povolit šifrování BitLockeru na zařízení pomocí zásad Intune a jak ověřit, jestli se vaše zásada úspěšně nasadila do zařízení.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/29/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac6650f06abddd2633e73f39a6bf72d54e344a61
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079191"
---
# <a name="troubleshoot-bitlocker-policies-in-microsoft-intune"></a>Řešení potíží se zásadami BitLockeru v Microsoft Intune

Tento článek může správcům Intune pomáhat pochopit, jak zařízení s Windows 10 konfigurují BitLocker na základě zásad Intune. Tento článek také poskytuje pokyny k řešení problémů s nastavením BitLockeru na zařízeních, která spravujete pomocí Intune.  

## <a name="understanding-bitlocker"></a>Principy nástroje BitLocker

BitLocker Drive Encryption je služba poskytovaná operačními systémy Microsoft Windows, která umožňuje uživatelům šifrovat data na svých pevných discích. BitLocker podporuje šifrování pro jednotky operačního systému, vyměnitelné mediální jednotky a pevné datové jednotky. BitLocker také podporuje použití 256 šifrování pro lepší ochranu citlivých dat.  

Pomocí Microsoft Intune máte k dispozici následující metody pro správu nástroje BitLocker na zařízeních s Windows 10:

- **Zásady konfigurace zařízení** – některé integrované možnosti zásad jsou k dispozici v Intune, když vytváříte profil konfigurace zařízení pro správu služby Endpoint Protection. Pokud chcete najít tyto možnosti, [vytvořte profil zařízení pro Endpoint Protection](endpoint-protection-configure.md#create-a-device-profile-containing-endpoint-protection-settings), vyberte **Windows 10 a novější** pro *platformu*a pak vyberte kategorii **šifrování Windows** pro *Nastavení*. 

   Informace o dostupných možnostech a funkcích si můžete přečíst tady: [šifrování Windows](https://docs.microsoft.com/intune/endpoint-protection-windows-10#windows-encryption).

- **Security baselines** - Směrné[plány](security-baselines.md) zabezpečení standardních hodnot zabezpečení jsou známé skupiny nastavení a výchozí hodnoty, které doporučuje příslušný bezpečnostní tým k zabezpečení zařízení s Windows. Různé zdroje standardních hodnot, jako jsou *základní hodnoty zabezpečení MDM* nebo *standardní hodnoty ATP v programu Microsoft Defender* , můžou spravovat stejné nastavení i jiná nastavení. Můžou taky spravovat stejná nastavení, která spravujete pomocí zásad konfigurace zařízení. 

Pro hardware, který je kompatibilní s moderní pohotovostní úsporou a HSTI při použití některé z těchto funkcí, se šifrování zařízení BitLockeru automaticky zapne při každém připojení zařízení do Azure AD. Azure AD poskytuje portál, ve kterém se zálohují taky klíče pro obnovení, takže uživatelé můžou v případě potřeby získat vlastní obnovovací klíč pro samoobslužné služby.

Je také možné, že nastavení nástroje BitLocker jsou spravovaná jiným způsobem, například Zásady skupiny, nebo ručně nastaveným uživatelem zařízení.

Bez ohledu na to, jak se na zařízení aplikují nastavení, zásady BitLockeru využívají [CSP nástroje BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) ke konfiguraci šifrování na zařízení. Zprostředkovatel kryptografických služeb BitLocker je integrovaný do systému Windows a když Intune nasadí zásady BitLockeru na přiřazené zařízení, je na zařízení CSP nástroje BitLocker, které zapisuje příslušné hodnoty do registru Windows, aby se nastavení ze zásad projevilo.

Pokud se chcete dozvědět víc o BitLockeru, podívejte se na následující zdroje informací:

- [BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)
- [Přehled nástroje BitLocker a požadavky – Nejčastější dotazy](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview-and-requirements-faq)

Teď, když máte obecné informace o tom, co tyto zásady dělají a jak fungují, si přečtěte, jak můžete ověřit, jestli se nastavení BitLockeru úspěšně netýká klienta Windows.

## <a name="verify-the-source-of-bitlocker-settings"></a>Ověření zdroje nastavení BitLockeru

Když prozkoumáte problém nástroje BitLocker na zařízení s Windows 10, je nutné nejprve určit, zda se jedná o problém s Intune nebo s Windows. Po zjištění pravděpodobnějšího zdroje selhání se můžete zaměřit na správné místo na vaše úsilí při řešení potíží a v případě potřeby získat podporu od správného týmu.  

Jako první krok určete, jestli se zásady Intune úspěšně nasadily do cílového zařízení. V následujícím příkladu máte zásady konfigurace zařízení, které nasazují nastavení šifrování Windows (BitLocker), jak je znázorněno níže:

![Zásady konfigurace pro šifrování zařízení s Windows s nastavením](./media/troubleshooting-bitlocker-policies/settings.png)

Jak si můžete ověřit, že se nastavení pro cílové zařízení nastavila? Toto je několik způsobů, jak to provést.

### <a name="device-configuration-policy-device-status"></a>Stav zařízení zásady konfigurace zařízení  

Když ke konfiguraci BitLockeru použijete zásady konfigurace zařízení, můžete na portálu Intune zjistit stav zásad.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost**profily konfigurace** **zařízení** > a potom vyberte profil, který obsahuje nastavení nástroje BitLocker.

3. Až vyberete profil, který chcete zobrazit, vyberte **stav zařízení**. Zobrazí se zařízení přiřazená k profilu a sloupec *stav zařízení* indikuje, jestli se v zařízení úspěšně nasadil profil.

Nezapomeňte, že mezi zařízením, které přijímá zásady BitLockeru, může docházet k prodlevě a plně zašifrované jednotce.  

### <a name="use-control-panel-on-the-client"></a>Použití ovládacích panelů na klientovi  

Na zařízení s povoleným BitLockerem a zašifrovanou jednotkou můžete zobrazit stav nástroje BitLocker v ovládacím panelu zařízení. Na zařízení otevřete **Ovládací panely** > **systém a** > **Nástroj BitLocker Drive Encryption**zabezpečení. Zobrazí se potvrzení, jak je vidět na následujícím obrázku.  

![BitLocker je zapnutý v Ovládacích panelech.](./media/troubleshooting-bitlocker-policies/control-panel.png)

### <a name="use-a-command-prompt"></a>Použití příkazového řádku  

Na zařízení, které povolilo nástroj BitLocker a zašifroval jednotku, spusťte příkazový řádek s přihlašovacími údaji správce `manage-bde -status`a spusťte příkaz. Výsledky by měly vypadat podobně jako v následujícím příkladu:  
![Výsledek příkazu status](./media/troubleshooting-bitlocker-policies/command.png)

V tomto příkladu:

- Je **zapnutá** **ochrana BitLockeru**
- **Zašifrované procento** je **100%** .
- **Metoda šifrování** je **XTS-AES 256**

Pomocí následujícího příkazu můžete také kontrolovat **ochrany klíčů** :

```cmd
Manage-bde -protectors -get c:
```

Nebo s PowerShellem:

```powershell
Confirm-SecureBootUEFI
```

### <a name="review-the-devices-registry-key-configuration"></a>Kontrola konfigurace klíče registru zařízení

Po úspěšném nasazení zásad BitLockeru do zařízení se podívejte na následující klíč registru na zařízení, kde můžete zkontrolovat konfiguraci nastavení BitLockeru: *HKEY_LOCAL_MACHINE \software\microsoft\policymanager\current\device\bitlocker*. Tady je příklad:

![Klíč registru BitLockeru](./media/troubleshooting-bitlocker-policies/registry.png)

Tyto hodnoty konfiguruje CSP nástroje BitLocker. Ověřte, že hodnoty klíčů odpovídají nastavením zadaným ve zdroji zásad šifrování systému Windows v Intune. Další informace o jednotlivých nastaveních najdete v tématu [CSP nástroje BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp).

> [!NOTE]
> Windows Prohlížeč událostí bude obsahovat také různé informace týkající se nástroje BitLocker. Seznam obsahuje příliš mnoho, ale hledání pomocí **nástroje BITLOCKER API** vám poskytne spoustu užitečných informací.

### <a name="check-the-mdm-diagnostics-report"></a>Podívejte se na zprávu o diagnostice MDM.

V zařízení, které má zapnutý nástroj BitLocker, můžete vygenerovat a zobrazit diagnostickou zprávu MDM z cílového zařízení a ověřit, jestli je přítomná zásada BitLockeru. Pokud vidíte nastavení zásad v sestavě, je to další oznámení, že se zásady úspěšně nasadily. *Microsoft pomáhá* video na následujícím odkazu vysvětluje, jak zachytit diagnostickou zprávu MDM ze zařízení s Windows.

> [!VIDEO https://www.youtube.com/embed/WKxlcjV4TNE]

Při analýze sestavy diagnostiky MDM se obsah může zdát za poněkud matoucí. Tady je příklad, který ukazuje, co se v sestavě koreluje s nastavením v zásadě:

![Příklad sestavy diagnostiky MDM](./media/troubleshooting-bitlocker-policies/report.png)

Výsledek výstupu zobrazuje hodnoty, které odpovídají hodnotám z vašich zásad BitLockeru:

![Výsledek výstupu zobrazuje hodnoty ](./media/troubleshooting-bitlocker-policies/output.png)

Výsledky výstupu diagnostiky MDM:

```asciidoc
EncryptionMethodWithXtsOsDropDown: 7 (The value 7 refers to the 256 bit encryption)
EncryptionMethodWithXtsFdvDropDown: 6 (The value 6 refers to the 128 bit encryption)
EncryptionMethodWithXtsRdvDropDown: 6 (The value 6 refers to the 128 bit encryption)
```

Na [dokumentaci k nástroji BITLOCKER CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) můžete odkazovat, abyste viděli, co každá hodnota znamená. V tomto příkladu je fragment kódu sdílen na následujícím obrázku.

![Účely hodnot](./media/troubleshooting-bitlocker-policies/shared-example.png)

Podobně můžete zobrazit všechny hodnoty a ověřit je pomocí odkazu CSP nástroje BitLocker.

> [!TIP]
> Hlavním účelem diagnostické sestavy MDM je pomáhat podpora Microsoftu při odstraňování potíží. Pokud otevřete případ podpory pro Intune a problém zahrnuje klienty Windows, je vždycky vhodné tuto sestavu shromáždit a zahrnout do žádosti o podporu.

## <a name="troubleshooting-bitlocker-policy"></a>Řešení potíží se zásadami BitLockeru

Teď byste měli mít dobrý nápad, jak ověřit, že zásady BitLockeru se úspěšně nasadily přes Intune, které vám umožní využít konfiguraci BitLockeru na CSP zprostředkovatele kryptografických služeb nástroje BitLocker v systému WIndows.

**Zásada nedorazila na zařízení** , pokud vaše zásada Intune není k dispozici v žádné kapacitě:

- **Je zařízení správně zaregistrované do Microsoft Intune?** Pokud ne, budete ji muset vyřešit, abyste mohli řešit problémy, které jsou specifické pro danou zásadu. Pomoc s řešením problémů s registrací ve Windows najdete [tady](../enrollment/troubleshoot-windows-enrollment-errors.md).

- **Je na zařízení aktivní síťové připojení?** Pokud je zařízení v režimu v letadle nebo vypnuté, nebo pokud má uživatel zařízení v místě bez služby, zásada se doručí nebo nebude platit, dokud se neobnoví síťové připojení.

- **Nasadila se zásada BitLockeru do správné skupiny uživatelů nebo zařízení?** Ověřte, jestli je správný uživatel nebo zařízení členem skupin, které cílíte.

**Zásada je k dispozici, ale ne všechna nastavení byla úspěšně nakonfigurována** – když vaše zásada Intune dosáhne zařízení, ale ne všechny konfigurace jsou nastaveny:

- **Selže nasazení celé zásady, nebo se jedná o pouze určitá nastavení, která neplatí?** Pokud se rozhodnete, že jste se seznámili se scénářem, kde se nevztahují jenom některá nastavení zásad, Projděte si následující požadavky:

  1. **Ne všechna nastavení nástroje BitLocker jsou podporovaná ve všech verzích Windows**.
     Zásady se v zařízení přinášejí jako jedna jednotka, takže pokud se některá nastavení uplatní a jiné ne, můžete si být jistí, že je obdržená samotná zásada. V tomto scénáři je možné, že verze Windows na zařízení nepodporuje problematická nastavení. Podrobnosti o požadavcích na verzi jednotlivých nastaveních najdete v dokumentaci k [nástroji BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) v dokumentaci k Windows.

  2. **BitLocker není podporován na všech hardwarových počítačích**.
     I v případě, že máte správnou verzi Windows, je možné, že základní hardware zařízení nesplňuje požadavky na šifrování BitLockeru. [Požadavky na systém pro nástroj BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview#system-requirements) najdete v dokumentaci k systému Windows, ale hlavní akce, které je třeba ověřit, že má zařízení kompatibilní čip TPM (1,2 nebo novější) a firmware systému BIOS kompatibilní se standardem TCG (Trusted Computing Group) nebo rozhraní UEFI.
     
**Šifrování BitLockeru se neprovádí v tichém režimu** – nakonfigurovali jste zásady Endpoint Protection s nastavením upozornění pro jiné šifrování disku, které se nastaví jako zablokované a Průvodce šifrováním se pořád zobrazuje:

- **Potvrzení, že verze Windows podporuje tiché šifrování** To vyžaduje minimálně verzi 1803. Pokud uživatel není na zařízení správce, než vyžaduje minimální verzi 1809. Navíc 1809 přidání podpory pro zařízení, která nepodporují moderní pohotovostní režim

**Zařízení šifrované bitlockerem se zobrazuje jako nevyhovující zásadám dodržování předpisů Intune** – k tomuto problému dochází, když šifrování nástrojem BitLocker není dokončené. Šifrování BitLockeru může trvat dlouhou dobu, a to na základě faktorů, jako je velikost disku, počet souborů a nastavení nástroje BitLocker. Po dokončení šifrování se zařízení zobrazí jako vyhovující. Zařízení se taky můžou dočasně nedodržující předpisy hned po poslední instalaci aktualizací WIndows.

**Zařízení se šifrují pomocí 128 bitových algorithim, když jsou specifické pro zásady 256 bit** – ve výchozím nastavení Windows 10 zašifruje jednotku pomocí šifrování XTS-AES 128-bit. V této příručce najdete [nastavení 256 šifrování pro BitLocker při autopilotu](https://techcommunity.microsoft.com/t5/intune-customer-success/setting-256-bit-encryption-for-bitlocker-during-autopilot-with/ba-p/323791#).


**Ukázkové šetření**

- Nasadíte zásadu BitLockeru na zařízení s Windows 10 a nastavení **Šifrovat zařízení** zobrazuje na portálu stav **Chyba** .

- Jak název naznačuje, toto nastavení umožňuje správci vyžadovat zapnutí šifrování pomocí *šifrování zařízení > bitlockerem*. Pomocí výše uvedených tipů pro řešení potíží nejprve ověřte zprávu o diagnostice MDM. Sestava potvrdí, že na zařízení byla nasazena správná zásada:

  ![Sestava potvrdí, že se na zařízení nasadí správná zásada.](./media/troubleshooting-bitlocker-policies/mdm-report.png)

- Můžete také ověřit úspěch v registru:

  ![Hodnota registru RequiredDeviceEncryption ukazuje 1](./media/troubleshooting-bitlocker-policies/registry-confirm.png)

- V dalším kroku zkontrolujete stav čipu TPM pomocí prostředí PowerShell a zjistíte, že čip TPM není na zařízení k dispozici:

  ![Kontrola stavu čipu TPM pomocí prostředí PowerShell](./media/troubleshooting-bitlocker-policies/tpm-command.png)

- Vzhledem k tomu, že nástroj BitLocker spoléhá na čip TPM, může dojít k tomu, že nástroj BitLocker neselže kvůli potížím se službou Intune nebo zásadou, ale místo toho, aby samotné zařízení nemá čip TPM nebo čip TPM není v systému BIOS zakázán.

   > Jako další tip můžete potvrdit stejné v Prohlížeč událostí Windows v části **protokoly aplikací a služeb****Microsoft** > **Windows** > **BitLocker API**. V protokolu událostí **rozhraní API BitLockeru** najdete ID události 853, což znamená, že čip TPM není k dispozici:

  ![ID události 853](./media/troubleshooting-bitlocker-policies/event-error.png)

  > [!NOTE]
  > Stav čipu TPM můžete také ověřit spuštěním **čipu TPM. msc** na zařízení.

## <a name="summary"></a>Souhrn

Když vyřešíte problémy se zásadami BitLockeru v Intune a můžete potvrdit, že zásada dosáhne zamýšleného zařízení, je možné, že problém nesouvisí přímo s Intune. Problém je pravděpodobnější, že se jedná o problém s operačním systémem Windows nebo s hardwarem. V takovém případě začněte hledat v jiných oblastech, jako je například konfigurace čipu TPM nebo rozhraní UEFI a zabezpečené spouštění).

## <a name="next-steps"></a>Další kroky  

V následující části najdete další zdroje informací, které mohou při práci s nástrojem BitLocker pomáhat:

- [Dokumentace k produktu BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)
- [Systémové požadavky BitLockeru](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview#system-requirements)
- [Nejčastější dotazy k nástroji BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-frequently-asked-questions)
- [Dokumentace k nástroji BitLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)
- [Nastavení zásad šifrování Windows v Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10#windows-encryption)
- [Automatické šifrování nástrojem BitLocker nezávislé na hardwaru pomocí AAD/MDM](https://blogs.technet.microsoft.com/home_is_where_i_lay_my_head/2017/06/07/hardware-independent-automatic-bitlocker-encryption-using-aadmdm/)
- [Zásady CSP pro šifrování BitLockeru na zařízeních s automatickým pilotem](https://techcommunity.microsoft.com/t5/Windows-10-security/CSP-policy-for-bitLocker-encryption-on-autopilot-devices/m-p/284537)
- [Návod k vytváření a nasazování zásad BitLockeru pomocí Intune](https://blogs.technet.microsoft.com/cbernier/2017/07/11/windows-10-intune-windows-bitlocker-management-yes/)
