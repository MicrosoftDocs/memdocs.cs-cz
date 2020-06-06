---
title: Společná Správa internetových zařízení
titleSuffix: Configuration Manager
description: Přečtěte si, jak připravit Internetová zařízení s Windows 10 pro spolusprávu.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 66e6156466d0432aaa8b3b162263f8207bdc9d78
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455102"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Příprava internetových zařízení na spolusprávu

Tento článek se zaměřuje na druhou cestu ke společné správě pro nová internetová zařízení. Tento scénář se používá, když máte nová zařízení s Windows 10, která se připojí k Azure AD a automaticky se zaregistrují do Intune. Nainstalujete klienta Configuration Manager pro dosažení stavu spolusprávy.  

## <a name="windows-autopilot"></a>Windows Autopilot

Pro nová zařízení s Windows 10 můžete použít službu autopilotu ke konfiguraci funkce out of box (OOBE). Tento proces zahrnuje připojení zařízení ke službě Azure AD a registraci zařízení v Intune.  

Další informace najdete v tématu [Přehled modulu Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Pokud chcete nakonfigurovat, aby se zařízení automaticky zaregistrovala do Intune, když se připojí k Azure AD, přečtěte si téma [registrace zařízení s Windows pro Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Shromažďování informací z Configuration Manager

Použijte Configuration Manager ke shromáždění a hlášení informací o zařízení požadovaných službou Intune. Tyto informace zahrnují sériové číslo zařízení, identifikátor produktu Windows a identifikátor hardwaru. Používá se k registraci zařízení v Intune pro podporu Windows autopilotu.

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte uzel **vytváření** sestav, rozbalte položku **sestavy**a vyberte uzel **Hardware – obecné** .  

2. Spusťte sestavu, **informace o zařízení Windows autopilot**a podívejte se na výsledky.  

3. V prohlížeči sestav vyberte ikonu **exportovat** a zvolte možnost CSV (oddělený **čárkami)** .  

4. Po uložení souboru nahrajte data do Intune.  

Další informace najdete v tématu [Přidání zařízení v Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot pro existující zařízení
<!--1358333-->

[Windows autopilot pro stávající zařízení](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) je k dispozici ve Windows 10 verze 1809 nebo novější. Tato funkce umožňuje obnovení image a zřízení zařízení se systémem Windows 7 pro [uživatele se systémem Windows autopilot na základě](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) jednoho nativního Configuration Managerho pořadí úloh.

Další informace najdete v tématu [Windows autopilot pro existující zařízení pořadí úkolů](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Instalace klienta Configuration Manager

Pro Internetová zařízení ve druhé cestě je potřeba vytvořit aplikaci v Intune. Nasaďte tuto aplikaci na zařízení s Windows 10, která už Configuration Manager klientech.

> [!NOTE]
> Než tuto aplikaci přiřadíte do zařízení v Intune, ujistěte se, že zařízení důvěřují ověřovacímu certifikátu CMG serveru. Další informace najdete v tématu [CMG důvěryhodný kořenový certifikát pro klienty](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Pokud zařízení nedůvěřuje ověřovacímu certifikátu serveru CMG, zobrazí se chyba WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA v programu CCMSetup. log v klientovi.

### <a name="get-the-command-line-from-configuration-manager"></a>Získání příkazového řádku z Configuration Manager

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** .  

2. Vyberte objekt spoluspráva a pak na pásu karet klikněte na tlačítko **vlastnosti** .  

3. Na kartě **Povolení** zkopírujte příkazový řádek. Vložte ho do poznámkového bloku a uložte ho pro další proces.  

Příklad následujícího příkazového řádku:`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Rozhodněte, které vlastnosti příkazového řádku budete potřebovat pro vaše prostředí:  

- Ve všech scénářích jsou vyžadovány následující vlastnosti příkazového řádku:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Při použití služby Azure AD pro ověřování klientů místo certifikátů ověřování klientů založených na infrastruktuře PKI se vyžadují následující vlastnosti:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Pokud se klient přenese zpátky do intranetu, použijte následující vlastnost:
  - SMSMP  

- Pokud používáte vlastní certifikát PKI a váš seznam odvolaných certifikátů není publikovaný na internetu, vyžaduje se následující parametr:  
  - /noCRLCheck  

    Další informace najdete v tématu [plánování seznamů CRL](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Počínaje verzí 2002 použijte následující vlastnost pro spuštění pořadí úloh hned po registraci klienta:
  - PROVISIONTS

    Další informace najdete v tématu [o vlastnostech instalace klienta – PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Lokalita publikuje Další informace o službě Azure AD v bráně pro správu cloudu (CMG). Klient připojený ke službě Azure AD získá tyto informace z CMG během procesu CCMSetup pomocí stejného tenanta, ke kterému je připojený. Toto chování dále zjednodušuje registraci zařízení do spolusprávy v prostředí s více než jedním klientem služby Azure AD. Jediným ze dvou požadovaných vlastností CCMSetup jsou **CCMHOSTNAME** a **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Pokud už klienta Configuration Manager nasazujete z Intune, aktualizujte aplikaci Intune pomocí nového příkazového řádku a nového MSI. <!-- SCCMDocs-pr issue 3084 -->

Následující příklad obsahuje všechny tyto vlastnosti:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Další informace najdete v tématu [vlastnosti instalace klienta](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Vytvoření aplikace v Intune

1. Přejít do [centra pro správu Microsoft Endpoint Manageru](https://endpoint.microsoft.com)a potom rozbalte levé navigační podokno.  

2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.  

3. V části **jiné**vyberte **obchodní aplikaci**.  

4. Nahrajte soubor balíčku aplikace **CCMSetup. msi** . Tento soubor vyhledejte v následující složce na serveru Configuration Manager lokality: `<ConfigMgr installation directory>\bin\i386` .  

    > [!Tip]  
    > Při aktualizaci lokality se ujistěte, že tuto aplikaci aktualizujete také v Intune.  

5. Po aktualizaci aplikace nakonfigurujte informace o aplikaci pomocí příkazového řádku, který jste zkopírovali z Configuration Manager.  

> [!IMPORTANT]
> Pokud tento příkazový řádek upravíte, ujistěte se, že není delší než 1024 znaků. Pokud je délka příkazového řádku větší než 1024 znaků, instalace klienta se nezdařila.
