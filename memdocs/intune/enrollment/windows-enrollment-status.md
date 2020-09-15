---
title: Nastavení stránky stavu registrace
titleSuffix: Microsoft Intune
description: Nastavte stránku pozdravu pro uživatele, kteří registrují zařízení s Windows 10.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fc05ced647e8784333c2a20bc13c27aa2bf3447
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076120"
---
# <a name="set-up-the-enrollment-status-page"></a>Nastavení stránky stavu registrace
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
Stránka stavu registrace (ESP) zobrazuje průběh zřizování po registraci nového zařízení a také při přihlášení nových uživatelů k zařízení.  Správci IT tak můžou volitelně zabránit (blokovat) přístup k zařízení, dokud nebude plně zajištěný, a zároveň uživatelům poskytnout informace o úkolech zbývajících v procesu zřizování.

Protokol ESP se dá použít jako součást jakéhokoli scénáře zřizování služby [Windows autopilot](../../autopilot/index.yml) a dá se použít odděleně od Windows autopilota jako součást výchozího spouštěného prostředí (OOBE) pro službu Azure AD JOIN a také pro všechny nové uživatele, kteří se do zařízení přihlašují poprvé.

Můžete vytvořit více profilů stránek stavu registrace s různými konfiguracemi, které určují:

- Zobrazení průběhu instalace
- Blokování přístupu až do dokončení procesu zřizování
- Časové limity
- Povolené operace řešení potíží

Tyto profily jsou určené v pořadí podle priority. použije se nejvyšší platná priorita.  Každý profil protokolu ESP může být zaměřen na skupiny obsahující zařízení nebo uživatele.  Při určování, který profil se má použít, se budou dodržovat následující kritéria:

- Nejdřív se použije profil nejvyšší priority, který se na zařízení zacílí.
- Pokud se na zařízení necílí žádné profily, použije se profil nejvyšší priority cílený na aktuálního uživatele.  (To platí jenom ve scénářích, kdy je nějaký uživatel. Ve scénářích White šetrnější a samoobslužného nasazení se dá použít jenom cílení na zařízení.)
- Pokud nejsou žádné profily cílené na konkrétní skupiny, použije se výchozí profil protokolu ESP.

## <a name="available-settings"></a>Dostupná nastavení

K přizpůsobení chování stránky stavu registrace můžete nakonfigurovat následující nastavení:

<table>
<th align="left">Nastavení<th align="left">Yes<th align="left">No
<tr><td>Zobrazit průběh instalace aplikací a profilů<td>Zobrazí se stránka stav registrace.<td>Stránka stavu registrace se nezobrazuje.
<tr><td>Zablokovat používání zařízení, dokud se nenainstalují všechny aplikace a profily<td>Nastavení v této tabulce jsou dostupná k přizpůsobení chování stránky stavu registrace, aby uživatel mohl řešit potenciální problémy s instalací.
<td>Stránka stavu registrace se zobrazí bez dalších možností pro řešení chyb při instalaci.
<tr><td>Dovolit uživatelům resetovat zařízení, pokud dojde k chybě instalace<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>resetovat zařízení</b> .<td>Tlačítko <b>resetovat zařízení</b> se nezobrazí, pokud dojde k chybě instalace.
<tr><td>Povolí uživatelům používat zařízení, pokud dojde k chybě instalace.<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>pokračovat</b> .<td>Pokud dojde k chybě instalace, tlačítko <b>pokračovat</b> se nezobrazí.
<tr><td>Zobrazit chybu časového limitu v případě, že instalace trvá déle než zadaný počet minut<td colspan="2">Zadejte počet minut, po které se má čekat na dokončení instalace. Je zadaná výchozí hodnota 60 minut.
<tr><td>Zobrazit vlastní zprávu, když dojde k chybě<td>Je k dispozici textové pole, kde můžete zadat vlastní zprávu, která se zobrazí, pokud dojde k chybě instalace.<td>Zobrazí se výchozí zpráva: <br><b>Instalace překročila časový limit nastavený vaší organizací. Zkuste to znovu, nebo se obraťte na pracovníky podpory IT a požádejte ho o pomoc.<b>
<tr><td>Dovolit uživatelům shromažďovat protokoly o chybách instalace<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>shromáždit protokoly</b> . <br>Pokud uživatel klikne na toto tlačítko, zobrazí se výzva k výběru umístění pro uložení souboru protokolu <b>MDMDiagReport.cab</b><td>Pokud dojde k chybě instalace, tlačítko <b>shromáždit protokoly</b> se nezobrazí.
<tr><td>Zablokovat používání zařízení, dokud se tyto požadované aplikace neinstalují, pokud jsou přiřazené uživateli/zařízení<td colspan="2">Vyberte <b>vše</b> nebo <b>vybrané</b>. <br><br>Pokud <b>vyberete</b> tuto možnost, zobrazí se tlačítko <b>vybrat aplikace</b> , které vám umožní vybrat, které aplikace se musí nainstalovat, než zařízení povolí.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Zapnout výchozí stránku stavu registrace pro všechny uživatele

Pokud chcete zapnout stránku Stav registrace, postupujte podle následujících kroků.
 
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace registrace**  >  **stavová stránka**.
2. V okně **Stránka stavu registrace** zvolte **Výchozí** > **Nastavení**.
3. U možnosti **Zobrazit průběh instalace aplikací a profilů** zvolte **Ano**.
4. Zvolte další nastavení, která chcete zapnout, a potom zvolte **Uložit**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Vytvoří profil stránky stavu registrace a přiřadí se ke skupině.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace registrace**  >  **Stránka stav**  >  **vytvořit profil**.
2. Zadejte **Název** a **Popis**.
3. Vyberte **vytvořit**.
4. Nový profil vyberte v seznamu **Stránka stavu registrace**.
5. Zvolte **přiřazení**  >  **Vybrat skupiny** > zvolte skupiny, které chcete použít pro tento profil > **Vyberte**  >  **Uložit**.
6. Vyberte **Nastavení** > vyberte nastavení, která chcete pro tento profil použít > **Uložit**.

## <a name="set-the-enrollment-status-page-priority"></a>Nastavení priority stránky stavu registrace

Zařízení nebo uživatel může být v mnoha skupinách a má více cílových profilů stránky stavu registrace. Abyste mohli řídit, které profily se považují za první, můžete nastavit priority pro jednotlivé profily. ty s vyšší prioritou se považují za první.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace registrace**  >  **stavová stránka**.
2. Najeďte myší na profil v seznamu.
3. Pomocí tří svislých teček přetáhněte profil na požadované místo v seznamu.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Zablokovat přístup k zařízení, dokud není nainstalovaná konkrétní aplikace

Můžete určit, které aplikace se musí nainstalovat předtím, než se dokončí stránka stavu registrace (ESP).

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace registrace**  >  **stavová stránka**.
2. Vyberte profil > **Nastavení**.
3. Pokud chcete **Zobrazit průběh instalace aplikací a profilů**, klikněte na **Ano** .
4. Vyberte možnost **Ano** pro **blokování použití zařízení, dokud nebudou nainstalovány všechny aplikace a profily**.
5. Vyberte možnost **Vybraná** pro **blokování použití zařízení, dokud se tyto požadované aplikace neinstalují, pokud jsou přiřazené uživateli nebo zařízení**.
6. Zvolte **vybrat aplikace** > zvolte aplikace > **Vybrat**  >  **Uložit**.

V Intune se používají aplikace, které jsou zahrnuté v tomto seznamu, aby se vyfiltroval seznam, který by se měl považovat za blokující.  Neurčuje, které aplikace se mají nainstalovat.  Pokud například nakonfigurujete tento seznam tak, aby zahrnoval "App 1," App 2, "a" App 3 "a" App 3 "a" App 4 "jsou zaměřené na zařízení nebo uživatele, bude stránka stavu registrace sledovat pouze" App 3 ".  Aplikace "App 4" bude stále nainstalována, ale na stránce Stav registrace nebude čekat na dokončení.

Je možné zadat maximálně 100 aplikací.

## <a name="enrollment-status-page-tracking-information"></a>Informace o sledování stránky stavu registrace

Existují tři fáze, ve kterých stránka stavu registrace sleduje informace pro; Příprava zařízení, nastavení zařízení a nastavení účtu.

### <a name="device-preparation"></a>Příprava zařízení

V případě přípravy zařízení se stránka stavu registrace sleduje:

- Ověření identity klíče TPM (Trusted Platform Module) (je-li k dispozici)
- Proces připojení Azure Active Directory
- Registrace v Intune (MDM)
- Instalace rozšíření pro správu Intune (slouží k instalaci aplikací Win32)

### <a name="device-setup"></a>Nastavení zařízení

Stránka stav registrace sleduje následující položky nastavení zařízení:

- Zásady zabezpečení
  - Zásady pro Microsoft Edge, přiřazený přístup a veřejný prohlížeč jsou aktuálně sledovány.
  - Další zásady nejsou sledovány.
- Aplikace
  - Počet obchodních aplikací Instalační služby MSI na jeden počítač.
  - Obchodní aplikace pro Store s kontextem instalace = zařízení.
  - Offline aplikace pro Store a obchodní aplikace pro Store s kontextem instalace = zařízení.
  - Aplikace Win32 (jenom Windows 10 verze 1903 a novější) 
- Profily připojení
  - Profily VPN nebo Wi-Fi přiřazené ke skupině **Všechna zařízení** nebo ke skupině zařízení, jejímž členem je zařízení, které se registruje. Platí pouze pro zařízení Autopilot.
- Profily certifikátů přiřazené ke skupině **Všechna zařízení** nebo ke skupině zařízení, jejímž členem je zařízení, které se registruje. Platí pouze pro zařízení Autopilot.

### <a name="account-setup"></a>Nastavení účtu

U nastavení účtu se na stránce Stav registrace sleduje následující položky, pokud jsou přiřazené k aktuálně přihlášenému uživateli:

- Zásady zabezpečení
  - Zásady pro Microsoft Edge, přiřazený přístup a veřejný prohlížeč jsou aktuálně sledovány.
  - Další zásady nejsou sledovány.
- Aplikace
  - Počet obchodních aplikací Instalační služby MSI na jednoho uživatele, které jsou přiřazeny ke všem zařízením, všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
  - Počet obchodních aplikací Instalační služby MSI na jeden počítač, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
  - Aplikace obchodu pro obchod, aplikace pro Online Store a aplikace pro offline Store, které jsou přiřazené k některým z následujících objektů:
    - All Devices
    - Všichni uživatelé
    - Skupina uživatelů, ve které je uživatel, který zařízení registruje, členem s kontextem instalace nastaveným na hodnotu uživatel.
  - Aplikace Win32 (jenom Windows 10 verze 1903 a novější) 
- Profily připojení
  - Profily VPN a Wi-Fi, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
- Certifikáty
  - Profily certifikátů, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.

### <a name="known-issues"></a>Známé problémy

Níže jsou uvedené známé problémy související se stránkou stavu registrace.

- Když se profil ESP zakáže, neodebere se zásada protokolu ESP ze zařízení a uživatelé budou při prvním přihlášení do zařízení získat protokol ESP. Zásada není odebrána, pokud je profil protokolu ESP zakázán. Chcete-li zakázat protokol ESP, je nutné nasadit OMA-URI. Pokyny k zakázání protokolu ESP pomocí OMA-URI najdete výše. 
- Restartování během instalace zařízení vynutí, aby uživatel před přechodem ke fázi nastavení účtu zadal svoje přihlašovací údaje. Přihlašovací údaje uživatele se během restartování neuchovávají. Uživatel musí zadat své přihlašovací údaje, aby mohla stránka stavu registrace pokračovat. 
- Při registraci pracovního a školního účtu ve verzích Windows 10, které jsou nižší než 1903, se na stránce Stav registrace vždycky vyprší časový limit. Stránka stavu registrace čeká na dokončení registrace Azure AD. Problém je opravený ve Windows 10 verze 1903 a novějším.  
- Hybridní nasazení Azure AD autopilotu s protokolem ESP trvá déle, než je doba trvání definovaná v profilu ESP. V hybridních nasazeních autopilotu služby Azure AD bude protokol ESP trvat 40 minut déle než hodnota nastavená v profilu ESP. Tato prodleva udává čas, po který konektor on-Prem AD vytvoří nový záznam zařízení ve službě Azure AD. 
- Přihlašovací stránka Windows není předem naplněná uživatelským jménem v režimu řízeného uživatelem automatického pilotního nasazení. Pokud dojde k restartování během fáze instalace zařízení v protokolu ESP:
  - přihlašovací údaje uživatele nejsou zachovány.
  - uživatel musí znovu zadat přihlašovací údaje, než bude pokračovat ve fázi nastavení zařízení do fáze nastavení účtu.
- Protokol ESP je zablokovaný po dlouhou dobu, nebo nikdy nedokončuje "identifikační" fázi. Intune počítá zásady protokolu ESP v rámci identifikační fáze. Pokud aktuálnímu uživateli není přiřazená licence Intune, nemůže zařízení nikdy dokončit výpočetní zásady ESP.  
- Konfigurace řízení aplikací v programu Microsoft Defender způsobí při autopilotu dotaz na restartování. Konfigurace aplikace v programu Microsoft Defender (AppLocker CSP) vyžaduje restart. Pokud je tato zásada nakonfigurovaná, může při autopilotu dojít k restartování zařízení. V současné době neexistuje způsob, jak potlačit nebo odložit restartování.
- Pokud je zásada DeviceLock ( https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) povolená jako součást profilu ESP, automatické přihlášení k počátečnímu počítači nebo ploše uživatele by mohlo selhat unexpectantly ze dvou důvodů.
  - Pokud se zařízení před ukončením fáze nastavení zařízení ESP nerestartuje, může se uživateli zobrazit výzva k zadání přihlašovacích údajů Azure AD. Tato výzva se zobrazí místo úspěšného automatického přihlášení, kde se uživateli zobrazí animace prvního přihlašování Windows.
  - Automatické přihlašování se nepovede, pokud se zařízení restartuje po zadání přihlašovacích údajů Azure AD, ale ještě před tím, než se ukončí fáze nastavení zařízení ESP. K této chybě dochází, protože fáze nastavení zařízení ESP nebyla nikdy dokončena. Alternativním řešením je resetování zařízení.

## <a name="next-steps"></a>Další kroky

Po nastavení stránek pro zápis do systému Windows se naučíte [spravovat zařízení s Windows](../remote-actions/device-management.md).

[Řešení potíží se stránkou stavu registrace systému Windows](https://docs.microsoft.com/troubleshoot/mem/intune/understand-troubleshoot-esp#troubleshooting)
