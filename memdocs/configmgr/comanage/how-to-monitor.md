---
title: Sledování spolusprávy
titleSuffix: Configuration Manager
description: Pomocí řídicího panelu spolusprávy můžete zkontrolovat informace o spoluspravovaných zařízeních.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e4516ca9baa7398322c204908c25248921a69d25
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268058"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Jak monitorovat spolusprávu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po povolení spolusprávy monitorujte zařízení spolusprávy pomocí následujících metod:

- [Řídicí panel pro spolusprávu](#co-management-dashboard)  

- [Zásady nasazení](#deployment-policies)

- [Data zařízení WMI](#wmi-device-data)

## <a name="co-management-dashboard"></a>Řídicí panel pro spolusprávu

Počínaje verzí 1802 se podívejte na řídicí panel s informacemi o spolusprávě. Řídicí panel vám pomůže zkontrolovat počítače, které jsou ve vašem prostředí spoluspravované. Grafy můžou identifikovat zařízení, která by mohla vyžadovat pozornost.<!--1356648-->

V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte uzel **spoluspráva** .

Počínaje verzí 1810 je řídicí panel spolusprávy vylepšený s podrobnějšími informacemi. <!--1358980-->

![Snímek obrazovky řídicího panelu spolusprávy](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>Společně spravovaná zařízení

*Platí pro verze 1802 a 1806.*

Zobrazuje procento spoluspravovaných zařízení v rámci vašeho prostředí.

![Dlaždice zařízení spoluspravovaná](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>Distribuce operačního systému klienta

*Platí pro všechny verze* 

Zobrazuje počet klientských zařízení na operační systém podle verze. Používá následující seskupení:  

- Windows 7 & 8. x
- Windows 10 nižší než 1709  
- Windows 10 1709 a novější  

    > [!Tip]  
    > Windows 10, verze 1709 a novější, je předpokladem pro spolusprávu.  

Najetím myší na oddíl grafu zobrazíte procento zařízení v dané skupině operačních systémů.

![Dlaždice distribuce operačního systému klienta](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>Stav spolusprávy (prstenec)

*Platí pro verze 1802 a 1806.*

Zobrazuje rozpis úspěšných nebo neúspěšných zařízení v následujících kategoriích:

- Úspěch, připojeno k hybridní službě Azure AD
- Úspěch, připojeno k Azure AD  
- Chyba: automatický zápis se nezdařil  

Najeďte myší na část grafu a zobrazte procento zařízení v této kategorii.

![Dlaždice se stavem spolusprávy (prstenec)](media/co-management-dashboard/Co-management-status-graph.PNG)

Vyberte oddíl grafu pro zobrazení seznamu zařízení pro danou kategorii.

![Seznam zařízení – selhání registrace](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>Stav spolusprávy (trychtýř)

*Platí pro verzi 1810 a novější.*

Trychtýřový graf, který zobrazuje počet zařízení s následujícími stavy z procesu registrace:
  
- Způsobilá zařízení
- Naplánované  
- Registrace zahájena  
- Zaregistrované  

![Dlaždice stavu spolusprávy (trychtýře)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Stav registrace spolusprávy

*Platí pro verzi 1810 a novější.*

Zobrazuje rozpis stavu zařízení v následujících kategoriích:

- Úspěch, připojeno k hybridní službě Azure AD  
- Úspěch, připojeno k Azure AD  
- Registrace, hybridní služba Azure AD – připojeno  
- Selhání, připojeno k hybridní službě Azure AD  
- Selhání, připojeno k Azure AD  
- Čeká se na přihlášení uživatele  

    > [!Note]  
    > Pokud chcete snížit počet zařízení v tomto stavu čekání, počínaje verzí 1906, nové spoluspravované zařízení teď automaticky zaregistruje službu Microsoft Intune na základě jejího tokenu *zařízení* Azure AD. Není nutné čekat, než se uživatel přihlásí k zařízení, aby se mohl spustit automatický zápis. Pro podporu tohoto chování musí zařízení používat Windows 10 verze 1803 nebo novější.
    >
    > Pokud token zařízení selhává, vrátí se k předchozímu chování s uživatelským tokenem. Vyhledejte v **protokolu ComanagementHandler. log** následující položku:`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Výběrem stavu v dlaždici přejdete na seznam zařízení v tomto stavu.  

![Dlaždice stavu registrace spolusprávy](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Přechod úlohy

*Platí pro všechny verze*

Zobrazí pruhový graf s počtem zařízení, která jste přešli na Microsoft Intune pro dostupné úlohy.

Seznam úloh se liší podle verze Configuration Manager. Další informace najdete v tématu [úlohy, které je možné převést do Intune](workloads.md).

Najeďte myší na část grafu a zobrazí se počet zařízení, která se převedla pro úlohy. 

![Pruhový graf přechodu úlohy](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Chyby registrace

*Platí pro verzi 1810 a novější.*

Tato tabulka představuje seznam chyb registrace ze zařízení. Tyto chyby můžou pocházet ze součásti MDM ve Windows, základního operačního systému Windows nebo klienta Configuration Manager.

Existují stovky možných chyb. V následující tabulce jsou uvedeny nejběžnější chyby.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Chyba | Description |
|---------|---------|
| 2147549183 (0x8000FFFF) | Registrace MDM se ještě nenakonfigurovala v Azure AD nebo se neočekává adresa URL pro registraci.<br><br>[Povolení automatické registrace pro Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licence uživatele je ve špatném stavu blokující registraci<br><br>[Přiřazení licencí k uživatelům](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Při pokusu o automatické registraci do Intune, ale konfigurace Azure AD se plně nepoužívá. Tento problém by měl být přechodný, jakmile se zařízení po krátkou dobu opakuje. |
| 2149056554 (0x 8018002A)<br>&nbsp; | Uživatel zrušil operaci.<br><br>Pokud registrace MDM vyžaduje vícefaktorové ověřování a uživatel se přihlásil s podporovaným Druhým faktorem, Windows zobrazí informační zprávu uživateli k registraci. Pokud uživatel nereaguje na informační oznámení, dojde k této chybě. Tento problém by měl být přechodný, protože Configuration Manager opakovat akci a vyzvat uživatele. Uživatelé by měli používat službu Multi-Factor Authentication při přihlašování k Windows. Informujte je také o tom, že toto chování očekáváte, a pokud se zobrazí výzva, proveďte akci. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Správa mobilních zařízení obecně není podporovaná. | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Serveru se nepovedlo ověřit uživatele.<br><br> Pro tohoto uživatele není k dispozici žádný token Azure AD. Ujistěte se, že se uživatel může ověřit ve službě Azure AD. |
| 2147942450 (0x 80070032)<br>&nbsp; | Automatická registrace MDM je podporovaná jenom v systémech Windows RS3 a vyšších.<br><br>Ujistěte se, že zařízení splňuje [minimální požadavky](overview.md#windows-10) pro spolusprávu. |
| 3400073293 | Neznáma odpověď účtu sféry uživatele ADAL<br><br>Zkontrolujte konfiguraci služby Azure AD a ujistěte se, že se uživatelé můžou úspěšně ověřit. | 
| 3399548929 | Vyžadovat přihlášení uživatele<br><br>Tento problém by měl být přechodný. K tomu dochází, když se uživatel rychle odhlásí předtím, než se stane úloha registrace. | 
| 3400073236 | Požadavek na token zabezpečení ADAL se nezdařil.<br><br>Zkontrolujte konfiguraci služby Azure AD a ujistěte se, že se uživatelé můžou úspěšně ověřit. |
| 2149122477 | Obecný problém HTTP |
| 3400073247 | ADAL – integrované ověřování systému Windows je podporované jenom v federovaném toku.<br><br>[Plánování implementace služby Hybrid Azure Active Directory JOIN](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | Server nebo proxy server nebyl nalezen.<br><br>Tento problém by měl být přechodný, pokud klient nemůže komunikovat s cloudem. Pokud s tím budou dál problémy, ujistěte se, že klient má konzistentní připojení k Azure. | 
| 2149056532 | Konkrétní platforma nebo verze není podporovaná.<br><br>Ujistěte se, že zařízení splňuje [minimální požadavky](overview.md#windows-10) pro spolusprávu. |
| 2147943568 | Element nebyl nalezen.<br><br>Tento problém by měl být přechodný. Pokud s tím budou dál problémy, kontaktujte podpora Microsoftu. |
| 2192179208 | K zpracování tohoto příkazu není k dispozici dostatek paměťových prostředků.<br><br>Tento problém by měl být přechodný, měl by se vyřešit sám při opakovaném pokusu o spuštění klienta. |
| 3399614467 | Pro tento kontrolní výraz se nepovedlo udělit autorizaci ADAL.<br><br>Zkontrolujte konfiguraci služby Azure AD a ujistěte se, že se uživatelé můžou úspěšně ověřit. |
| 2149056517 | Obecná chyba z management server, například Chyba přístupu k databázi<br><br>Tento problém by měl být přechodný. Pokud s tím budou dál problémy, kontaktujte podpora Microsoftu. |
| 2149134055 | Název WinHTTP se nevyřešil.<br><br>Klient nemůže přeložit název služby. Ověřte konfiguraci DNS. | 
| 2149134050 | časový limit pro Internet<br><br>Tento problém by měl být přechodný, pokud klient nemůže komunikovat s cloudem. Pokud s tím budou dál problémy, ujistěte se, že klient má konzistentní připojení k Azure. |

Další informace najdete v tématu [hodnoty chyb registrace MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).

## <a name="deployment-policies"></a>Zásady nasazení

V uzlu **nasazení** pracovního prostoru **monitorování** se vytvoří dvě zásady. Jedna zásada je určena pro pilotní skupinu a jednu pro produkční prostředí. Tyto zásady hlásí pouze počet zařízení, ve kterých Configuration Manager zásady používaly. Neberou v úvahu, kolik zařízení je zaregistrované v Intune, což je požadavek, aby se zařízení mohla spravovat společně.  

Provozní zásady (CoMgmtSettingsProd) jsou cílené na kolekci **všechny systémy** . Má podmínku použitelnosti, která kontroluje typ a verzi operačního systému. Pokud je klient operačním systémem serveru nebo ne Windows 10, zásada se nepoužije a neprovede se žádná akce.

## <a name="wmi-device-data"></a>Data zařízení WMI

Dotaz na **SMS_Client_ComanagementState** třídu služby WMI ve službě **root\sms\ site_ &lt; SITECODE>** oboru názvů na serveru lokality. V Configuration Manager můžete vytvořit vlastní kolekce, které vám pomůžou určit stav nasazení spolusprávy. Další informace o vytváření vlastních kolekcí najdete v tématu vytváření [kolekcí](../core/clients/manage/collections/create-collections.md).

Ve třídě WMI jsou k dispozici následující pole:  

- **MachineId**: jedinečné ID zařízení pro klienta Configuration Manager  

- **MDMEnrolled**: Určuje, jestli je zařízení zaregistrované v MDM.  

- **Autorita**: autorita, pro kterou je zařízení zaregistrované  

- **ComgmtPolicyPresent**: Určuje, zda Configuration Manager zásady spolusprávy existují v klientovi. Pokud je hodnota **MDMEnrolled** **0**, zařízení se nespravuje společně bez ohledu na to, jestli zásady spolusprávy existují v klientovi.  

Zařízení se spoluspravuje, když pole **MDMEnrolled** a pole **ComgmtPolicyPresent** mají hodnotu **1**.  
