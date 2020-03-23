---
title: Nastavení stránky stavu registrace
titleSuffix: Microsoft Intune
description: Nastavte na stránce s pozdravem uživatelé, kteří registrují zařízení s Windows 10.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/26/2019
ms.topic: conceptual
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
ms.openlocfilehash: 9bbb8738acbfdfa2317d754797dbb171c6a5d8ac
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326955"
---
# <a name="set-up-an-enrollment-status-page"></a>Nastavení stránky stavu registrace
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
Stránka stavu registrace (ESP) zobrazuje informace o instalaci zařízení s Windows 10 (verze 1803 a novější) během úvodní registrace zařízení. Příklad:
- Při použití [Windows autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/) 
- nebo kdykoli se spravované zařízení poprvé spustí po použití zásady stránky stavu registrace. 

Stránka stavu registrace pomáhá uživatelům pochopit stav svých zařízení během instalace zařízení. Můžete vytvořit více profilů stránek stavu registrace a použít je v různých skupinách, které obsahují uživatele. Profily můžete nastavit tak, aby:
- Zobrazovaly průběh instalace.
- Blokovaly používání, než se instalace dokončí.
- Určovaly, co může uživatel udělat, pokud se instalace zařízení nezdaří.

Můžete také nastavit pořadí priority pro každý profil na účet pro konfliktní přiřazení profilů pro stejného uživatele.

> [!NOTE]
> Stránka stavu registrace se může zaměřit jenom na uživatele, který patří do přiřazené skupiny, a v případě registrace pro všechny uživatele, kteří zařízení používají, se v zařízení nastavila zásada.  

## <a name="available-settings"></a>Dostupná nastavení

 K přizpůsobení chování stránky stavu registrace můžete nakonfigurovat následující nastavení:

<table>
<th align="left">Nastavení<th align="left">Ano<th align="left">Ne
<tr><td>Zobrazit průběh instalace aplikací a profilů<td>Zobrazí se stránka stav registrace.<td>Stránka stavu registrace se nezobrazuje.
<tr><td>Zablokovat používání zařízení, dokud se nenainstalují všechny aplikace a profily<td>Nastavení v této tabulce jsou dostupná k přizpůsobení chování stránky stavu registrace, aby uživatel mohl řešit potenciální problémy s instalací.
<td>Stránka stavu registrace se zobrazí bez dalších možností pro řešení chyb při instalaci.
<tr><td>Dovolit uživatelům resetovat zařízení, pokud dojde k chybě instalace<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>resetovat zařízení</b> .<td>Tlačítko <b>resetovat zařízení</b> se nezobrazí, pokud dojde k chybě instalace.
<tr><td>Povolí uživatelům používat zařízení, pokud dojde k chybě instalace.<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>pokračovat</b> .<td>Pokud dojde k chybě instalace, tlačítko <b>pokračovat</b> se nezobrazí.
<tr><td>Zobrazit chybu časového limitu v případě, že instalace trvá déle než zadaný počet minut<td colspan="2">Zadejte počet minut, po které se má čekat na dokončení instalace. Je zadaná výchozí hodnota 60 minut.
<tr><td>Zobrazit vlastní zprávu, když dojde k chybě<td>Je k dispozici textové pole, kde můžete zadat vlastní zprávu, která se zobrazí, pokud dojde k chybě instalace.<td>Zobrazí se výchozí zpráva: <br>Instalace <b>překročila časový limit nastavený vaší organizací. Zkuste to znovu, nebo se obraťte na pracovníky podpory IT a požádejte ho o pomoc.<b>
<tr><td>Dovolit uživatelům shromažďovat protokoly o chybách instalace<td>Pokud dojde k chybě instalace, zobrazí se tlačítko <b>shromáždit protokoly</b> . <br>Pokud uživatel klikne na toto tlačítko, zobrazí se výzva k výběru umístění pro uložení souboru protokolu <b>MDMDiagReport. cab.</b><td>Pokud dojde k chybě instalace, tlačítko <b>shromáždit protokoly</b> se nezobrazí.
<tr><td>Zablokovat používání zařízení, dokud se tyto požadované aplikace neinstalují, pokud jsou přiřazené uživateli/zařízení<td colspan="2">Vyberte <b>vše</b> nebo <b>vybrané</b>. <br><br>Pokud <b>vyberete</b> tuto možnost, zobrazí se tlačítko <b>vybrat aplikace</b> , které vám umožní vybrat, které aplikace se musí nainstalovat, než zařízení povolí.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Zapnout výchozí stránku stavu registrace pro všechny uživatele

Pokud chcete zapnout stránku Stav registrace, postupujte podle následujících kroků.
 
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** >  > Windows **registrace systému Windows** > **Stránka stavu registrace**.
2. V okně **Stránka stavu registrace** zvolte **Výchozí** > **Nastavení**.
3. U možnosti **Zobrazit průběh instalace aplikací a profilů** zvolte **Ano**.
4. Zvolte další nastavení, která chcete zapnout, a potom zvolte **Uložit**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Vytvoří profil stránky stavu registrace a přiřadí se ke skupině.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **registrace Windows** > **stavová stránka** > **vytvořit profil**.
2. Zadejte **Název** a **Popis**.
3. Zvolte **Vytvořit**.
4. Nový profil vyberte v seznamu **Stránka stavu registrace**.
5. Vyberte **Přiřazení** > **Vybrat skupiny** > vyberte skupiny, které mají tento profil používat > **Vybrat** > **Uložit**.
6. Vyberte **Nastavení** > vyberte nastavení, která chcete pro tento profil použít > **Uložit**.

## <a name="set-the-enrollment-status-page-priority"></a>Nastavení priority stránky stavu registrace

Uživatel může být v mnoha skupinách a mít velký počet profilů stránek stavu registrace. Chcete-li tyto konflikty zpracovat, můžete nastavit priority pro jednotlivé profily. Pokud má někdo více než jeden profil stránky stavu registrace, použije se k registraci zařízení jenom profil s nejvyšší prioritou.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** >  > Windows **registrace systému Windows** > **Stránka stavu registrace**.
2. Najeďte myší na profil v seznamu.
3. Pomocí tří svislých teček přetáhněte profil na požadované místo v seznamu.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Blokovat přístup k zařízení, do konkrétní aplikace je nainstalována.

Můžete určit aplikace, které je potřeba nainstalovat předtím, než uživatel může přístup k ploše.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** >  > Windows **registrace systému Windows** > **Stránka stavu registrace**.
2. Vyberte profil > **Nastavení**.
3. Pokud chcete **Zobrazit průběh instalace aplikací a profilů**, klikněte na **Ano** .
4. Vyberte možnost **Ano** pro **blokování použití zařízení, dokud nebudou nainstalovány všechny aplikace a profily**.
5. Vyberte možnost **Vybraná** pro **blokování použití zařízení, dokud se tyto požadované aplikace neinstalují, pokud jsou přiřazené uživateli nebo zařízení**.
6. Zvolte **vybrat aplikace** > zvolte aplikace > **Vyberte** > **Uložit**.

## <a name="enrollment-status-page-tracking-information"></a>Informace o sledování stránky stavu registrace

Existují tři fáze, ve kterých stránka stavu registrace sleduje informace pro; Příprava zařízení, nastavení zařízení a nastavení účtu.

### <a name="device-preparation"></a>Příprava zařízení

V případě přípravy zařízení se stránka stavu registrace sleduje:
- Ověření identity klíče čipu TPM (Trusted Platform Module) (Pokud je k dispozici)
- průběh přidávání Azure Active Directory
- Registrace do Intune
- Instalace rozšíření pro správu Intune

### <a name="device-setup"></a>Nastavení zařízení

Na stránce Stav registrace se sledují následující položky instalace zařízení (pokud jsou přiřazené ke všem zařízením nebo skupině zařízení, ve které je zařízení pro registraci členem):
- Zásady zabezpečení
  - Jeden poskytovatel konfiguračních služeb pro všechny registrace.
  - Skuteční poskytovatelé konfiguračních služeb nakonfigurovaných službou Intune se zde nesledují.
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
  - Jeden poskytovatel konfiguračních služeb pro všechny registrace.
  - Skuteční poskytovatelé konfiguračních služeb nakonfigurovaných službou Intune se zde nesledují.
- Aplikace
  - Počet obchodních aplikací Instalační služby MSI na jednoho uživatele, které jsou přiřazeny ke všem zařízením, všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
  - Počet obchodních aplikací Instalační služby MSI na jeden počítač, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
  - Aplikace obchodu pro obchod, aplikace pro Online Store a aplikace pro offline Store, které jsou přiřazené k některým z následujících objektů:
    - Všechna zařízení
    - Všichni uživatelé
    - Skupina uživatelů, ve které je uživatel, který zařízení registruje, členem s kontextem instalace nastaveným na hodnotu uživatel.
  - Aplikace Win32 (jenom Windows 10 verze 1903 a novější) 
- Profily připojení
  - Profily VPN a Wi-Fi, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.
- Certifikáty
  - Profily certifikátů, které jsou přiřazeny ke všem uživatelům nebo skupině uživatelů, jejímž členem uživatel provádějící registraci zařízení je.

### <a name="troubleshooting"></a>Odstraňování potíží
Nejčastější dotazy k řešení potíží.

- Proč se mi během fáze nastavení zařízení během nasazování pomocí automatického pilotního nasazení nenainstalovaly moje aplikace, které používají stránku stavu registrace?
  - Pokud chcete zajistit, aby se aplikace nainstalovaly během fáze nastavení zařízení autopilotu, ujistěte se, že 
        1. Aplikace se vybere pro blokování přístupu v seznamu vybraných aplikací.
        2. Cílíte na aplikace na stejnou skupinu zařízení Azure AD, ke které je váš profil autopilotu přiřazený. 

- Proč se stránka stavu registrace zobrazuje pro autopilotní nasazení, například když se uživatel poprvé přihlásí na Configuration Manager zařízení, které spoluvlastní Správa zaregistrovalo?  
  - Stránka stav registrace uvádí stav instalace pro všechny metody registrace, včetně
      - Autopilot
      - Configuration Manager spolusprávu
      - Když se nový uživatel přihlásí k zařízení, které má při prvním použití zásady stránky stavu registrace
      - Když je na zařízení, které je zřízené a nastavené jako nastavení spouštěné při **prvním zapnutí (OOBE)** , zapnutá možnost Zobrazit na stránce jenom první uživatel, který se do zařízení přihlásí, získá stav registrace.

- Jak můžu zakázat stránku stavu registrace, pokud byla nakonfigurovaná na zařízení?
  - Zásady stránky stavu registrace se v době registrace nastaví na zařízení. Chcete-li zakázat stránku stavu registrace, je nutné zakázat oddíly stránky stavu registrace uživatele a zařízení. Tyto oddíly zakážete vytvořením vlastního nastavení OMA-URI s následujícími konfiguracemi.

      Zakázat stránku stavu registrace uživatele:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Zakázat stav registrace zařízení – stránka:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Jak můžu shromáždit soubory protokolu?
  - Existují dva způsoby, jak můžete shromáždit soubory protokolu stránky stavu registrace:
      - Umožňuje uživatelům shromažďovat protokoly v zásadách ESP. Pokud na stránce Stav registrace dojde k vypršení časového limitu, může koncový uživatel zvolit možnost **shromažďovat protokoly**. Vložením jednotky USB můžete zkopírovat soubory protokolu na jednotku.
      - Otevřete příkazový řádek zadáním klávesy SHIFT + F10 a potom zadejte následující příkazový řádek, který vygeneruje soubory protokolu: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Známé problémy
Níže jsou uvedené známé problémy. 
- Když se profil ESP zakáže, neodebere se zásada protokolu ESP ze zařízení a uživatelé budou při prvním přihlášení do zařízení získat protokol ESP. Zásada není odebrána, pokud je profil protokolu ESP zakázán. Chcete-li zakázat protokol ESP, je nutné nasadit OMA-URI. Pokyny k zakázání protokolu ESP pomocí OMA-URI najdete výše. 
- Čekání na restartování bude vždy způsobit časový limit. K vypršení časového limitu dojde, protože je nutné restartovat zařízení. Aby bylo možné dokončit položku sledovanou na stránce stavu registrace, je nutné restartovat počítač. Restartování způsobí, že se stránka stavu registrace ukončí a po restartování zařízení nevstoupí v nastavení účtu po restartování.  Zvažte nevyžadování restartování při instalaci aplikace. 
- Restartování během instalace zařízení vynutí, aby uživatel před přechodem ke fázi nastavení účtu zadal svoje přihlašovací údaje. Přihlašovací údaje uživatele se během restartování neuchovávají. Uživatel musí zadat své přihlašovací údaje, aby mohla stránka stavu registrace pokračovat. 
- Při registraci pracovního a školního účtu ve verzích Windows 10, které jsou nižší než 1903, se na stránce Stav registrace vždycky vyprší časový limit. Stránka stavu registrace čeká na dokončení registrace Azure AD. Problém je opravený ve Windows 10 verze 1903 a novějším.  
- Hybridní nasazení Azure AD autopilotu s protokolem ESP trvá déle, než je doba trvání definovaná v profilu ESP. V hybridních nasazeních autopilotu služby Azure AD bude protokol ESP trvat 40 minut déle než hodnota nastavená v profilu ESP. Tato prodleva udává čas, po který konektor on-Prem AD vytvoří nový záznam zařízení ve službě Azure AD. 
- Přihlašovací stránka Windows není předem naplněná uživatelským jménem v režimu řízeného uživatelem automatického pilotního nasazení. Pokud dojde k restartování během fáze instalace zařízení v protokolu ESP:
    - přihlašovací údaje uživatele nejsou zachovány.
    - uživatel musí znovu zadat přihlašovací údaje, než bude pokračovat ve fázi nastavení zařízení do fáze nastavení účtu.
- Protokol ESP je zablokovaný po dlouhou dobu, nebo nikdy nedokončuje "identifikační" fázi. Intune počítá zásady protokolu ESP v rámci identifikační fáze. Pokud aktuálnímu uživateli není přiřazená licence Intune, nemůže zařízení nikdy dokončit výpočetní zásady ESP.  
- Konfigurace řízení aplikací v programu Microsoft Defender způsobí při autopilotu dotaz na restartování. Konfigurace aplikace v programu Microsoft Defender (AppLocker CSP) vyžaduje restart. Pokud je tato zásada nakonfigurovaná, může při autopilotu dojít k restartování zařízení. V současné době neexistuje způsob, jak potlačit nebo odložit restartování.
- Pokud je zásada DeviceLock (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) povolená jako součást profilu ESP, automatické přihlášení k POČÁTEČNÍmu počítači nebo ploše uživatele by mohlo selhat unexpectantly ze dvou důvodů.
  - Pokud se zařízení před ukončením fáze nastavení zařízení ESP nerestartuje, může se uživateli zobrazit výzva k zadání přihlašovacích údajů Azure AD. Tato výzva se zobrazí místo úspěšného automatického přihlášení, kde se uživateli zobrazí animace prvního přihlašování Windows.
  - Automatické přihlašování se nepovede, pokud se zařízení restartuje po zadání přihlašovacích údajů Azure AD, ale ještě před tím, než se ukončí fáze nastavení zařízení ESP. K této chybě dochází, protože fáze nastavení zařízení ESP nebyla nikdy dokončena. Alternativním řešením je resetování zařízení.

## <a name="next-steps"></a>Další kroky
Po nastavení stránek registrace zařízení s Windows se naučte spravovat zařízení s Windows. Další informace najdete v článku [Co je správa zařízení v Microsoft Intune](../remote-actions/device-management.md).