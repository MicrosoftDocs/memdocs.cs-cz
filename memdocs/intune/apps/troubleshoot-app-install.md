---
title: Řešení problémů s instalací aplikací
titleSuffix: Microsoft Intune
description: Pomocí podokna pro řešení potíží s Microsoft Intune můžete řešit potíže s instalací aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/21/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b613f364-0150-401f-b9b8-2b09470b34f4
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18fc3a70a89451deebe074ad8b5b8dc3a4a837f7
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325817"
---
# <a name="troubleshoot-app-installation-issues"></a>Řešení problémů s instalací aplikací

U zařízení spravovaných pomocí Microsoft Intune MDM může občas dojít k chybě instalace. Když k těmto chybám instalace dojde, může být obtížné pochopit, proč k nim došlo nebo je odstranit. Microsoft Intune poskytuje podrobnosti o chybách při instalaci aplikací, díky nimž si operátoři helpdesku a správci Intune poskytující pomoc uživatelům mohou zobrazit informace o aplikacích. Podokno pro řešení potíží v Intune poskytuje podrobnosti o chybě, včetně podrobností o spravovaných aplikacích na zařízení uživatele. V podokně **Spravované aplikace** jsou k dispozici podrobnosti o úplném životním cyklu aplikace pro jednotlivá zařízení. Můžete si zobrazit potíže s instalací, například to, kdy byla aplikace vytvořena, upravena, zacílena a dodána do zařízení.

> [!NOTE]
> Informace o chybách při instalaci konkrétní aplikace najdete v tématu [Reference k instalaci aplikace Intune](app-install-error-codes.md).

## <a name="app-troubleshooting-details"></a>Podrobnosti o řešení potíží s aplikací

Intune poskytuje podrobnosti o řešení potíží s aplikacemi nainstalovanými na konkrétním zařízení uživatele.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **řešení potíží + podpora**.
3. Klikněte na **Vybrat uživatele** a vyberte uživatele, pro kterého chcete řešit potíže. Zobrazí se podokno **Vybrat uživatele**.
4. Vyberte uživatele zadáním jména nebo e-mailové adresy. V dolní části podokna klikněte na **Vybrat**. V podokně **Řešení potíží** se zobrazí informace o řešení potíží pro daného uživatele. 
5. V seznamu **Zařízení** vyberte zařízení, u kterého chcete řešit potíže.
    ![Podokno Řešení potíží služby Intune](./media/troubleshoot-app-install/troubleshoot-app-install-01.png)
6. V podokně vybraného zařízení vyberte **Spravované aplikace**. Zobrazí se seznam spravovaných aplikací.
    ![Podrobnosti o konkrétním zařízení spravovaném pomocí Intune](./media/troubleshoot-app-install/troubleshoot-app-install-02.png)
7. V seznamu vyberte aplikaci, u které sloupec **Stav instalace** označuje chybu.
    ![Vybraná aplikace, u které jsou zobrazeny podrobnosti o chybě instalace.](./media/troubleshoot-app-install/troubleshoot-app-install-03.png)

    > [!Note]  
    > Stejná aplikace může být přiřazena k více skupinám, ale s různými zamýšlenými akcemi (záměry) pro aplikaci. Zjištěný záměr pro aplikaci bude například zobrazovat **vyloučeno**, pokud byla aplikace vyloučena pro uživatele během přiřazování aplikace. Další informace najdete v tématu [Řešení konfliktů mezi záměry aplikace](apps-deploy.md#how-conflicts-between-app-intents-are-resolved).<br><br>
    > Pokud dojde k chybě instalace požadované aplikace, vy nebo váš tým technické podpory bude moci synchronizovat zařízení a zopakovat pokus o instalaci.

Podrobnosti o chybě při instalaci aplikace označí problém. Tyto podrobnosti můžete použít k určení nejvhodnějších kroků pro vyřešení problému. Další informace o řešení potíží s instalací aplikací najdete v tématu chyby [instalace aplikace pro Android](app-install-error-codes.md#android-app-installation-errors) a [chyby instalace aplikace pro iOS](app-install-error-codes.md#ios-and-ipados-app-installation-errors).

> [!Note]  
> Do podokna **řešení potíží** se dostanete také tak, že v prohlížeči přejdete na adresu: [https://aka.ms/intunetroubleshooting](https://aka.ms/intunetroubleshooting).

## <a name="user-group-targeted-app-installation-does-not-reach-device"></a>Instalace cílené aplikace skupiny uživatelů nedosahuje zařízení.
Pokud máte problémy s instalací aplikací, je třeba vzít v úvahu následující akce:
- Pokud se aplikace v Portál společnosti nezobrazí, ujistěte se, že je aplikace nasazená s **dostupným** záměrem a že uživatel přistupuje k Portál společnosti s typem zařízení, který aplikace podporuje.
- Pro zařízení s Windows BYOD musí uživatel do zařízení přidat pracovní účet.
- Ověřte, jestli uživatel překračuje limit zařízení AAD:
  1. Přejděte na [Azure Active Directory nastavení zařízení](https://portal.azure.com/#pane/Microsoft_AAD_IAM/DevicesMenupane/DeviceSettings/menuId).
  2. Poznamenejte si hodnotu nastavenou pro **maximální počet zařízení na uživatele**.
  3. Přejděte na [Azure Active Directory uživatelé](https://portal.azure.com/#pane/Microsoft_AAD_IAM/UsersManagementMenupane/AllUsers).
  4. Vyberte ovlivněného uživatele a klikněte na **zařízení**.
  5. Pokud uživatel překročí nastavený limit, pak odstraňte všechny zastaralé záznamy, které už nepotřebujete.
- V případě zařízení se systémem iOS/iPadOS DEP se ujistěte, že je uživatel v podokně Přehled zařízení Intune uveden jako **zapsaný uživatelem** . Pokud se zobrazuje NA, pak Nasaďte zásadu konfigurace pro Portál společnosti Intune. Další informace najdete v tématu [Konfigurace aplikace Portál společnosti](app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices).

## <a name="win32-app-installation-troubleshooting"></a>Řešení potíží s instalací aplikace Win32

Vyberte aplikaci Win32 nasazenou pomocí rozšíření pro správu Intune. Při neúspěšné instalaci aplikace Win32 můžete vybrat možnost **shromáždit protokoly** . 

> [!IMPORTANT]
> Možnost **shromáždit protokoly** nebude povolena, pokud byla aplikace Win32 úspěšně nainstalována do zařízení.<p>Předtím, než budete moct shromažďovat informace protokolu aplikace Win32, je nutné nainstalovat rozšíření správy Intune na klienta Windows. Rozšíření pro správu Intune se nainstaluje při nasazení skriptu PowerShellu nebo aplikace Win32 do skupiny zabezpečení uživatele nebo zařízení. Další informace najdete v tématu [rozšíření pro správu Intune – předpoklady](intune-management-extension.md#prerequisites).

### <a name="collect-log-file"></a>Shromáždit soubor protokolu

Pokud chcete shromáždit protokoly instalace aplikace Win32, postupujte podle kroků uvedených v části [Podrobnosti o odstraňování potíží s aplikací](troubleshoot-app-install.md#app-troubleshooting-details). Pak pokračujte následujícími kroky:

1. Klikněte na možnost **shromáždit protokoly** v podokně **Podrobnosti o instalaci** .

    <image alt="Win32 app installation details - Collect log option" src="./media/troubleshoot-app-install/troubleshoot-app-install-04.png" width="500" />

2. Zadáním cest k souborům s názvy souborů protokolu zahajte proces shromažďování souborů protokolu a klikněte na tlačítko **OK**.

    > [!NOTE]
    > Shromažďování protokolů bude trvat méně než dvě hodiny. Podporované typy souborů: *. log,. txt,. dmp,. cab,. zip,. XML,. evtx a. evtl*. Povoluje se maximálně 25 cest k souborům.

3. Po shromáždění souborů protokolu můžete vybrat odkaz **protokoly** ke stažení souborů protokolu.

    <image alt="Win32 app log details - Download logs" src="./media/troubleshoot-app-install/troubleshoot-app-install-05.png" width="500" />

    > [!NOTE]
    > Zobrazí se oznámení o úspěchu shromažďování protokolu aplikace.

#### <a name="win32-log-collection-requirements"></a>Požadavky na shromažďování protokolů Win32

Existují specifické požadavky, které je nutné dodržovat ke shromáždění souborů protokolu:

- Je nutné zadat úplnou cestu k souboru protokolu. 
- Pro shromažďování protokolů můžete zadat proměnné prostředí, například následující:<br>
  *% PROGRAMFILES%,% SLOŽKA PROGRAMDATA%% PUBLIC%,% WINDIR%,% TEMP%,% TMP%*
- Jsou povoleny pouze přesné přípony souborů, například:<br>
  *. log,. txt,. dmp,. cab,. zip,. XML*
- Maximální soubor protokolu k nahrání je 60 MB nebo 25 souborů, podle toho, co nastane dřív. 
- Pro aplikace, které splňují požadovaný, dostupný a odinstalační záměr přiřazení aplikace, je povolená kolekce protokolů instalace aplikace Win32.
- Uložené protokoly jsou zašifrované, aby chránily jakékoli osobní identifikovatelné informace obsažené v protokolech.
- Při otevírání lístků podpory pro chyby aplikací Win32 připojte související protokoly selhání pomocí výše uvedených kroků.

## <a name="troubleshooting-apps-from-the-microsoft-store"></a>Řešení problémů s aplikacemi z Microsoft Storu

Informace v tématu [Řešení problémů s vytvářením balíčků, nasazením a dotazy aplikací pro Microsoft Store](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx) vám pomůžou s řešením běžných problémů, na které můžete narazit při instalaci aplikací z Microsoft Storu, ať už k ní využíváte službu Intune, nebo jiný nástroj.

## <a name="app-troubleshooting-resources"></a>Prostředky pro řešení potíží s aplikací
- [Nasazení aplikací Visio a Project jako součást nasazení sady Office pro plus](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Deploying-Visio-and-Project-as-part-of-your-Office/ba-p/701795)
- [Proveďte kroky k zajištění, aby se aplikace MSfB nasazené prostřednictvím Intune nainstalovaly ve Windows 10 1903.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Take-Action-to-Ensure-MSfB-Apps-deployed-through/ba-p/658864)
- [Řešení potíží s nasazením aplikací MSI v Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-MSI-App-deployments-in-Microsoft/ba-p/359125)
- [Osvědčené postupy pro distribuci softwaru do Intune Classic Windows PC Agent](https://support.microsoft.com/en-us/help/2583929/best-practices-for-intune-software-distribution-to-windows-pc)

## <a name="next-steps"></a>Další kroky

- Další informace o řešení potíží s Intune najdete v článku [Použití portálu pro řešení potíží k poskytování pomoci uživatelům ve vaší společnosti](../fundamentals/help-desk-operators.md). 
- Zjistěte další informace o známých problémech v Microsoft Intune. Další informace najdete v tématu [úspěšnost zákazníka v Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Potřebujete další pomoc? Přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
