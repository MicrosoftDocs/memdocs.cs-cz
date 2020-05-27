---
title: Přidávání skriptů PowerShellu do zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Vytvořte a spusťte skripty PowerShellu, přiřaďte zásady skriptu k Azure Active Directory skupinám, pomocí sestav můžete monitorovat skripty a Zobrazit postup odstranění skriptů přidaných do zařízení s Windows 10 v Microsoft Intune. Podívejte se také na některé běžné problémy a jejich řešení.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 768b6f08-3eff-4551-b139-095b3cfd1f89
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8d75208de7cc6697699d79e3a52df742f605fdb
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990727"
---
# <a name="use-powershell-scripts-on-windows-10-devices-in-intune"></a>Použití skriptů PowerShellu na zařízeních s Windows 10 v Intune

Rozšíření pro správu Microsoft Intune slouží k nahrání skriptů PowerShellu v Intune, aby se spouštěla na zařízeních s Windows 10. Rozšíření pro správu zlepšuje správu mobilních zařízení (MDM) systému Windows 10 a usnadňuje přechod na moderní správu.

Tato funkce platí pro:

- Windows 10 a novější (s výjimkou Windows 10 Home)

> [!NOTE]
> Po splnění požadavků rozšíření správy Intune se automaticky nainstaluje rozšíření pro správu Intune, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32. Další informace najdete v tématu [požadavky](../apps/intune-management-extension.md#prerequisites)rozšíření pro správu Intune.

## <a name="move-to-modern-management"></a>Přechod na moderní správu

Prostředí IT pro koncové uživatele prochází digitální transformací. Klasický, tradiční se zaměřuje na platformu zařízení, zařízení vlastněná firmou, uživatele, kteří pracují z kanceláře, a různé ruční a aktivní procesy IT. Moderní pracoviště používá mnoho platforem, které jsou vlastněny uživatelem a firmou, umožňuje uživatelům pracovat odkudkoli a poskytuje automatizované a proaktivní procesy IT.

Služby MDM, například Microsoft Intune, můžou spravovat mobilní a desktopová zařízení s Windows 10. Integrovaný klient pro správu Windows 10 komunikuje s Intune a spouští úlohy podnikového řízení. Je možné, že budete potřebovat některé úlohy, jako je například Pokročilá konfigurace zařízení a řešení potíží. Pro správu aplikací Win32 můžete použít funkci [Správa aplikací Win32](app-management.md) na zařízeních s Windows 10.

Rozšíření pro správu Intune doplňují součásti Windows 10 MDM v krabicích. Můžete vytvořit PowerShellové skripty pro spouštění na zařízeních s Windows 10. Například vytvořte skript PowerShellu, který provede pokročilé konfigurace zařízení. Pak tento skript nahrajte do Intune, přiřaďte ho ke skupině Azure Active Directory (AD) a spusťte skript. Pak můžete monitorovat stav spuštění skriptu od začátku do konce.

## <a name="prerequisites"></a>Požadavky

Rozšíření pro správu Intune má následující požadavky. Po splnění požadavků se rozšíření pro správu Intune nainstaluje automaticky, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32.

- Zařízení se systémem Windows 10 verze 1607 nebo novější. Pokud je zařízení zaregistrované pomocí [hromadného automatického zápisu](../enrollment/windows-bulk-enroll.md), musí na zařízeních běžet Windows 10 verze 1709 nebo novější. Rozšíření pro správu Intune není v režimu S Windows 10 podporované, protože režim S neumožňuje spouštění aplikací, které nejsou ve Storu. 
  
- Zařízení připojená k Azure Active Directory (AD), včetně:  
  
  - Připojení k hybridní službě Azure AD: zařízení připojená k Azure Active Directory (AD) a také připojená k místní službě Active Directory (AD). Pokyny najdete v tématu [Plánování implementace služby hybrid Azure Active Directory JOIN](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) .
  
  > [!TIP]
  > Ujistěte se, že jsou zařízení [připojená](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network) k Azure AD. Zařízení, která jsou [registrována](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) pouze ve službě Azure AD, nebudou přijímat vaše skripty.  

- Zařízení zaregistrovaná v Intune, včetně:

  - Zařízení zaregistrovaná v zásadách skupiny (GPO). Pokyny najdete v tématu [registrace zařízení s Windows 10 automaticky pomocí Zásady skupiny](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) .
  
  - Ručně zaregistrovaná zařízení do Intune, což je v těchto případech:
  
    - [Automatický zápis do Intune](../enrollment/quickstart-setup-auto-enrollment.md) je povolený ve službě Azure AD. Koncový uživatel se k zařízení přihlásí pomocí místního uživatelského účtu, ručně připojí zařízení do služby Azure AD a pak se k zařízení přihlásí pomocí svého účtu Azure AD.
    
    NEBO  
    
    - Uživatel se přihlásí k zařízení pomocí svého účtu služby Azure AD a potom se zaregistruje v Intune.

  - Spoluspravovaná zařízení, která používají Configuration Manager a Intune. Ujistěte se, že úlohy **aplikace** jsou nastavené na **pilotní nasazení Intune** nebo **Intune**. Pokyny najdete v následujících článcích: 
  
    - [Co je společná správa](https://docs.microsoft.com/configmgr/comanage/overview) 
    - [Zatížení klientských aplikací](https://docs.microsoft.com/configmgr/comanage/workloads#client-apps)
    - [Postup přepnutí úloh Configuration Manager do Intune](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)
  
> [!NOTE]
> Informace o používání virtuálních počítačů s Windows 10 najdete v tématu [používání virtuálních počítačů s Windows 10 s Intune](../fundamentals/windows-10-virtual-machines.md).

## <a name="create-a-script-policy-and-assign-it"></a>Vytvoření zásady skriptu a její přiřazení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **PowerShell skripty**  >  **Přidat**.

    ![Přidávání a používání skriptů PowerShellu v Microsoft Intune](./media/intune-management-extension/mgmt-extension-add-script.png)

3. V části **základy**zadejte následující vlastnosti a vyberte **Další**:
    - **Název**: zadejte název skriptu PowerShellu. 
    - **Popis**: zadejte popis skriptu PowerShellu. Toto nastavení není povinné, ale doporučujeme ho zadat.
4. V **nastavení skriptu**zadejte následující vlastnosti a vyberte **Další**:
    - **Umístění skriptu**: přejděte do skriptu PowerShellu. Skript musí být menší než 200 KB (ASCII).
    - **Spusťte tento skript pomocí přihlašovacích údajů přihlášeného**: vyberte **Ano** a spusťte skript s přihlašovacími údaji uživatele v zařízení. Pokud chcete skript spustit v kontextu systému, vyberte **ne** (výchozí). Mnoho správců zvolí **Ano**. Pokud je nutné skript spustit v kontextu systému, klikněte na tlačítko **ne**.
    - **Vymáhat kontrolu podpisu skriptu**: vyberte **Ano** , pokud musí být skript podepsaný důvěryhodným vydavatelem. Pokud není nutný žádný požadavek na podepsání skriptu, vyberte **ne** (výchozí). 
    - **Spustit skript v 64 hostitelském hostiteli PowerShellu**: vyberte **Ano** , pokud chcete skript spustit v 64ovém hostiteli PowerShellu na 64 bitové klientské architektury. Pokud vyberete **ne** (výchozí), spustí se skript v hostiteli powershellu 32.

      Při nastavení na **Ano** nebo **ne**použijte následující tabulku pro nové a existující chování zásad:

      | Spustit skript v 64 hostitele PS | Architektura klienta | Nový skript PS | Existující skript zásad PS |
      | --- | --- | --- | --- | 
      | Ne | 32bitová  | 32 podporovaný hostitel PS | Spouští se jenom v 32 hostitelích PS, který funguje na 32 64 a 32bitových architekturách. |
      | Ano | 64bitová | Spustí skript v 64-bitovém hostiteli PS pro 64 bitové architektury. Pokud běžela na 32-bit, skript se spustí na 32ém hostiteli PS. | Spustí skript v 32-bitovém hostiteli PS. Pokud se toto nastavení změní na 64-bit, otevře se skript (nespustí se) v 64ém hostiteli PS a nahlásí výsledky. Pokud běžela na 32-bit, skript se spustí v 32m hostiteli PS. |

5. Vyberte **značky oboru**. Značky oboru jsou volitelné. [Použijte řízení přístupu na základě role (RBAC) a značky oboru pro distribuované oddělení IT](../fundamentals/scope-tags.md) s dalšími informacemi.

    Přidání značky oboru:

    1. Zvolte **možnost vyberte značky oboru** > v seznamu vyberte existující značku oboru > **Vyberte**.

    2. Po dokončení vyberte **Další**.

6. Vyberte **přiřazení**  >  **Vybrat skupiny, které chcete zahrnout**. Zobrazí se existující seznam skupin Azure AD.

    1. Vyberte jednu nebo více skupin, které zahrnují uživatele, jejichž zařízení obdrží skript. Zvolte **Vybrat**. Skupiny, které jste zvolili, se zobrazí v seznamu a budou dostávat vaše zásady.

        > [!NOTE]
        > Skripty PowerShellu v Intune můžou být cílené na skupiny zabezpečení zařízení Azure AD nebo na skupiny zabezpečení uživatelů Azure AD.

    2. Vyberte **Další**.

        ![Přiřazení nebo nasazení skriptu PowerShellu do skupin zařízení v Microsoft Intune](./media/intune-management-extension/mgmt-extension-assignments.png)

7. V okně **Revize a přidat**se zobrazí souhrn nastavení, které jste nakonfigurovali. Vyberte **Přidat** a uložte skript. Když vyberete **Přidat**, zásada se nasadí do skupin, které jste zvolili.

## <a name="important-considerations"></a>Důležité informace

- Když jsou skripty nastavené na kontext uživatele a koncový uživatel má práva správce, skript PowerShellu se ve výchozím nastavení spustí s oprávněním správce.

- Koncoví uživatelé se nemusí přihlašovat k zařízení, aby mohli spouštět skripty PowerShellu.

- Agent rozšíření pro správu Intune kontroluje v Intune každou hodinu a po každém restartování pro všechny nové skripty nebo změny. Po přiřazení zásad ke skupinám Azure AD se powershellový skript spustí a zobrazí se výsledky spuštění. Jakmile se skript spustí, znovu se spustí, pokud nedojde ke změně skriptu nebo zásad. Pokud se skript nepovede, Agent rozšíření pro správu Intune se pokusí znovu spustit skript třikrát po dalších 3 po sobě jdoucích agentů rozšíření pro správu Intune.

- Pro sdílená zařízení se PowerShellový skript spustí pro každého nového uživatele, který se přihlásí.

### <a name="failure-to-run-script-example"></a>Nepovedlo se spustit příklad skriptu.
8 DOP.
  -  Vrátit se změnami
  -  Spustit skript **ConfigScript01**
  -  Skript selhává

9:00
  -  Vrátit se změnami
  -  Spustit skript **ConfigScript01**
  -  Skript se nezdařil (počet opakování = 1)

OD 10 DOP.
  -  Vrátit se změnami
  -  Spustit skript **ConfigScript01**
  -  Skript se nezdařil (počet opakování = 2)
  
11 AM
  -  Vrátit se změnami
  -  Spustit skript **ConfigScript01**
  -  Skript se nezdařil (počet opakování = 3)

12:00
  -  Vrátit se změnami
  - Neudělaly se žádné další pokusy o spuštění skriptu **ConfigScript01**.
  - Pokud se ve skriptu nebudou provádět žádné další změny, nebudou provedeny žádné další pokusy o spuštění skriptu.


## <a name="monitor-run-status"></a>Monitorovat stav spuštění

Na portálu Azure Portal můžete monitorovat stav spuštění powershellových skriptů u uživatelů a zařízení.

V části **Powershellové skripty** vyberte skript, který chcete monitorovat, zvolte **Monitorovat** a pak zvolte jednu z následujících sestav:

- **Stav zařízení**
- **Stav uživatele**

## <a name="intune-management-extension-logs"></a>Protokoly rozšíření pro správu Intune

Protokoly agenta v klientském počítači jsou obvykle v systému `\ProgramData\Microsoft\IntuneManagementExtension\Logs` . K zobrazení těchto souborů protokolu můžete použít [CMTrace. exe](https://docs.microsoft.com/configmgr/core/support/cmtrace) .

![Snímek obrazovky nebo ukázkový protokol agenta CMTrace v Microsoft Intune](./media/apps-win32-app-management/apps-win32-app-10.png)  

## <a name="delete-a-script"></a>Odstranění skriptu

V části **Powershellové skripty** klikněte pravým tlačítkem na skript a vyberte **Odstranit**.

## <a name="common-issues-and-resolutions"></a>Běžné problémy a jejich řešení

### <a name="issue-intune-management-extension-doesnt-download"></a>Problém: rozšíření pro správu Intune se nestáhne.

**Možná řešení**:

- Zařízení není připojené ke službě Azure AD. Ujistěte se, že zařízení splňují [požadavky](#prerequisites) (v tomto článku). 
- Neexistují žádné skripty PowerShellu ani aplikace Win32 přiřazené ke skupinám, které uživatel nebo zařízení patří.
- Zařízení se nemůže vrátit se změnami do služby Intune, protože není k dispozici přístup k Internetu, nemá přístup ke službám nabízených oznámení Windows (WNS) atd.
- Zařízení je v režimu S. Rozšíření pro správu Intune se nepodporuje na zařízeních, která běží v režimu S. 

Pokud chcete zjistit, jestli je zařízení automaticky zaregistrované, můžete:

  1. Přejděte na **Nastavení**  >  **účty**  >  **přístup do práce nebo do školy**.
  2. Vyberte připojený účet > **informace**.
  3. V části **Pokročilá diagnostická sestava**vyberte **vytvořit sestavu**.
  4. Otevřete `MDMDiagReport` ve webovém prohlížeči.
  5. Vyhledejte vlastnost **MDMDeviceWithAAD** . Pokud vlastnost existuje, zařízení se automaticky zaregistruje. Pokud tato vlastnost neexistuje, zařízení se automaticky nezaregistruje.

[Povolení automatické registrace Windows 10](../enrollment/windows-enroll.md#enable-windows-10-automatic-enrollment) zahrnuje postup konfigurace automatického zápisu v Intune.

### <a name="issue-powershell-scripts-do-not-run"></a>Problém: skripty PowerShellu se nespustí.

**Možná řešení**:

- Skripty PowerShellu se nespustí při každém přihlášení. Spustí:

  - Když je skript přiřazený k zařízení
  - Pokud skript změníte, nahrajte ho a přiřaďte ho uživateli nebo zařízení.
  
    > [!TIP]
    > **Rozšíření pro správu Microsoft Intune** je služba, která běží na zařízení stejně jako jakákoli jiná služba uvedená v aplikaci služby (Services. msc). Po restartování zařízení se tato služba může také restartovat a vyhledat všechny přiřazené skripty PowerShellu se službou Intune. Pokud je služba **rozšíření správy Microsoft Intune** nastavena na ruční, služba se po restartování zařízení nemusí restartovat.

- Ujistěte se, že jsou zařízení [připojená k Azure AD](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network). Zařízení, která jsou připojená jenom k vašemu pracovišti nebo organizaci ([zaregistrovaná](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) ve službě Azure AD), nebudou dostávat skripty.
- Klient rozšíření pro správu Intune se jednou za hodinu kontroluje v případě jakýchkoli změn ve skriptu nebo zásadách v Intune.
- Potvrďte, že je rozšíření pro správu Intune stažené do `%ProgramFiles(x86)%\Microsoft Intune Management Extension` .
- Skripty se nespouštějí na rozbočovačích Surface nebo Windows 10 v režimu S.
- Zkontrolujte případné chyby v protokolech. Viz [protokoly rozšíření pro správu Intune](#intune-management-extension-logs) (v tomto článku).
- V případě možných problémů s oprávněními zkontrolujte, jestli jsou vlastnosti skriptu PowerShellu nastavené na `Run this script using the logged on credentials` . Také ověřte, zda má přihlášený uživatel příslušná oprávnění ke spuštění skriptu.

- Chcete-li izolovat problémy skriptování, můžete:

  - Zkontrolujte konfiguraci spouštění PowerShellu na vašich zařízeních. Pokyny najdete v tématu [zásady spouštění prostředí PowerShell](https://docs.microsoft.com/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-6) .
  - Spusťte ukázkový skript pomocí rozšíření pro správu Intune. Vytvořte například `C:\Scripts` adresář a poskytněte všem úplnému řízení. Spusťte tento skript:

    ```powershell
    write-output "Script worked" | out-file c:\Scripts\output.txt
    ```

    V případě úspěchu by měl být vytvořen výstup. txt a měl by obsahovat text "skript fungoval".

  - Pokud chcete otestovat spuštění skriptu bez Intune, spusťte skripty v účtu System pomocí [nástroje PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec) místně:

    `psexec -i -s`  
    
  - Pokud skript hlásí, že se úspěšně zdařil, ale neúspěšně neuspěl, je možné, že vaše antivirová služba může být AgentExecutorá do izolovaného prostoru. Následující skript vždy hlásí selhání v Intune. Jako test můžete použít tento skript:
  
    ```powershell
    Write-Error -Message "Forced Fail" -Category OperationStopped
    mkdir "c:\temp" 
    echo "Forced Fail" | out-file c:\temp\Fail.txt
    ```

    Pokud skript ohlásí úspěch, podívejte se na text `AgentExecutor.log` pro potvrzení výstupu chyby. Pokud se skript spustí, musí být délka >2.

  - Chcete-li zachytit soubory. Error a. Output, následující fragment kódu spustí skript prostřednictvím AgentExecutor do PSx86 ( `C:\Windows\SysWOW64\WindowsPowerShell\v1.0` ). Udržuje protokoly pro vaši kontrolu. Mějte na paměti, že rozšíření pro správu Intune po spuštění skriptu vyčistí protokoly:
  
    ```powershell
    $scriptPath = read-host "Enter the path to the script file to execute"
    $logFolder = read-host "Enter the path to a folder to output the logs to"
    $outputPath = $logFolder+"\output.output"
    $errorPath =  $logFolder+"\error.error"
    $timeoutPath =  $logFolder+"\timeout.timeout"
    $timeoutVal = 60000 
    $PSFolder = "C:\Windows\SysWOW64\WindowsPowerShell\v1.0"
    $AgentExec = "C:\Program Files (x86)\Microsoft Intune Management Extension\agentexecutor.exe"
    &$AgentExec -powershell  $scriptPath $outputPath $errorPath $timeoutPath $timeoutVal $PSFolder 0 0
    ```

## <a name="next-steps"></a>Další kroky

[Monitorování](../configuration/device-profile-monitor.md) a [řešení potíží s](../configuration/device-profile-troubleshoot.md) profily
