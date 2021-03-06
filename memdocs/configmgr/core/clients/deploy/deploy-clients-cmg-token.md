---
title: Ověřování na základě tokenů pro CMG
titleSuffix: Configuration Manager
description: Zaregistrujte klienta v interní síti pro jedinečný token nebo vytvořte token pro hromadnou registraci pro Internetová zařízení.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 55997c9185a221d105aa8ad40bbb14021463d07b
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512695"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Ověřování založené na tokenech pro bránu pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

<!--5686290-->

Brána pro správu cloudu (CMG) podporuje mnoho typů klientů, ale i s [rozšířenými http](../../plan-design/hierarchy/enhanced-http.md), tito klienti vyžadují [certifikát pro ověřování klientů](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Tento požadavek na certifikát může být náročný na zřízení internetových klientů, kteří se často nepřipojují k interní síti, nelze se připojit Azure Active Directory (Azure AD) a nemusíte mít k dispozici metodu pro instalaci certifikátu vystaveného infrastrukturou veřejných klíčů.

Aby se tyto výzvy vyřešily od verze 2002, Configuration Manager rozšiřuje podporu zařízení tím, že vydává svoje vlastní ověřovací tokeny do zařízení. Pokud chcete plně využít tuto funkci, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. Kompletní scénář není funkční, dokud nebude verze klienta zároveň nejnovější. V případě potřeby se ujistěte, že [povýšíte novou verzi klienta na produkční](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)prostředí.

 Klienti poprvé registrují pro tyto tokeny pomocí jedné z následujících dvou metod:

- Interní síť

- Hromadná registrace

Klient Configuration Manager společně s bodem správy spravuje tento token, takže neexistuje žádná závislost verze operačního systému. Tato funkce je k dispozici pro libovolnou [podporovanou verzi operačního systému klienta](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Tyto metody podporují jenom scénáře správy zaměřené na zařízení.
>
> Microsoft doporučuje připojit zařízení k Azure AD. Internetová zařízení můžou pomocí Azure AD ověřit pomocí Configuration Manager. Také umožňuje scénářům zařízení i uživatele, zda je zařízení na internetu nebo připojeno k interní síti. Další informace najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="internal-network-registration"></a>Registrace interní sítě

Tato metoda vyžaduje, aby se klient nejdřív zaregistroval s bodem správy v interní síti. K registraci klienta obvykle dochází po instalaci hned po instalaci. Bod správy dává klientovi jedinečný token, který ukazuje, že používá certifikát podepsaný svým držitelem. Když se klient přenáší do Internetu, aby komunikoval s CMG, spáruje svůj certifikát podepsaný svým držitelem pomocí tokenu vydaného bodem správy.

Lokalita toto chování umožňuje ve výchozím nastavení.

## <a name="bulk-registration-token"></a>Token hromadné registrace

Pokud nemůžete instalovat a registrovat klienty v interní síti, vytvořte token pro hromadnou registraci. Tento token použijte, když se klient nainstaluje na internetové zařízení a zaregistruje se přes CMG. Registrační token pro hromadnou registraci má krátkou dobu platnosti a není uložený v klientovi nebo lokalitě. Umožňuje klientovi generovat jedinečný token, který se spáruje s certifikátem podepsaným svým držitelem, a umožňuje ověřování pomocí CMG.

> [!NOTE]
> Nepleťte si hromadné registrační tokeny s uživateli, kteří Configuration Manager problémy jednotlivým klientům. Token hromadné registrace umožňuje klientovi počáteční instalaci a komunikaci s lokalitou. Tato počáteční komunikace je dostatečně dlouhá, aby lokalita mohla vydat vlastní jedinečný token ověřování klientů. Klient pak použije ověřovací token pro veškerou komunikaci s lokalitou, zatímco je na internetu. Po počáteční registraci klient nepoužívá ani neukládá hromadnou registrační token.

Pokud chcete vytvořit hromadnou registrační token pro použití při instalaci klienta na internetových zařízeních, proveďte následující akce:

1. Přihlaste se k serveru lokality nejvyšší úrovně v hierarchii s oprávněními místního správce.

1. Otevřete příkazový řádek jako správce.

1. Spusťte nástroj ze `\bin\X64` složky instalačního adresáře Configuration Manager na serveru lokality: `BulkRegistrationTokenTool.exe` . Vytvořte nový token s `/new` parametrem. Například, `BulkRegistrationTokenTool.exe /new`. Další informace najdete v tématu [použití nástroje pro hromadnou registraci tokenu](#bulk-registration-token-tool-usage).

1. Zkopírujte token a uložte ho na bezpečném místě.

1. Nainstalujte klienta Configuration Manager do internetového zařízení. Zahrňte parametr instalace klienta: [**/regtoken**](about-client-installation-properties.md#regtoken). Následující příklad příkazového řádku obsahuje další požadované parametry a vlastnosti instalace:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Další informace o tomto příkazovém řádku najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Tento proces je podobný, ale nepoužívá vlastnosti Azure AD.

Chcete-li ověřit, zkontrolujte následující soubor protokolu pro podobnou položku:<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

Pokud chcete řešit potíže s instalací, zkontrolujte `%WinDir%\ccmsetup\logs\ccmsetup.log` klienta. Po instalaci si projděte téma `%WinDir%\ccm\logs\ClientIDManagerStartup.log` .

Na serveru zkontrolujte následující protokoly:

- [Protokoly CMG](../../plan-design/hierarchy/log-files.md#cloud-management-gateway)
- Bod správy
  - CCM_STS. log
  - MP_RegistrationManager. log
  - ClientAuth.log

### <a name="known-issues"></a>Známé problémy

Nelze vytvořit hromadnou registrační token v lokalitě, která má server lokality v pasivním režimu.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Použití nástroje pro hromadnou registraci tokenu

`BulkRegistrationTokenTool.exe`Nástroj je ve `\bin\X64` složce instalačního adresáře Configuration Manager na serveru lokality. Přihlaste se k serveru lokality a spusťte ho jako správce. Podporuje následující parametry příkazového řádku:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Zobrazí informace o použití.

Příklad: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Vytvořte nový registrační token pro hromadnou registraci.

Příklad: `BulkRegistrationTokenTool.exe /new`

Nástroj zobrazí následující informace:
  
- Identifikátor GUID, který lokalita používá ke sledování vydaných tokenů
- Doba platnosti tokenu, která je ve výchozím nastavení tři dny.
- Token hromadné registrace.

Token není uložený na klientovi nebo na webu. Nezapomeňte zkopírovat token z příkazového řádku a uložit je do zabezpečeného umístění.

#### <a name="lifetime"></a>/lifetime

`/new`K určení doby platnosti tokenu použijte parametr with. Zadejte celočíselnou hodnotu v minutách. Výchozí hodnota je 4 320 (tři dny). Maximální hodnota je 10 080 (sedm dní).

Příklad: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Správa tokenů hromadné registrace

V případě potřeby můžete zobrazit dříve vytvořené registrační tokeny a jejich životnosti v konzole Configuration Manager a v případě potřeby zablokovat jejich používání. Databáze lokality však nebude ukládat tokeny hromadné registrace.

### <a name="review-a-bulk-registration-token"></a>Kontrola hromadné registračního tokenu

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** .

2. Rozbalte položku **zabezpečení**a vyberte uzel **certifikáty** . Konzola obsahuje seznam všech certifikátů souvisejících s lokalitami a registračních tokenů pro hromadnou registraci v podokně podrobností.

3. Vyberte token hromadné registrace, který chcete zkontrolovat.

Můžete filtrovat nebo řadit podle sloupce **typ** . Identifikujte konkrétní registrační tokeny na základě identifikátoru GUID. Když vytváříte hromadnou registrační token, nástroj zobrazí identifikátor GUID.

### <a name="block-a-bulk-registration-token"></a>Blokování hromadné registračního tokenu

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** .

2. Rozbalte položku **zabezpečení**, vyberte uzel **certifikáty** a vyberte token hromadné registrace, který chcete blokovat.

3. Na kartě **Domů** na pásu karet nebo v místní nabídce klikněte pravým tlačítkem myši na možnost **blokovat**. Chcete-li odblokovat dříve blokované tokeny hromadné registrace, vyberte akci **odblokovat** .

## <a name="token-renewal"></a>Obnovení tokenu

Klient obnoví jedinečný, Configuration Manager vydaný token jednou za měsíc a je platný po dobu 90 dnů. Klient se nemusí připojovat k interní síti, aby mohl obnovit svůj token. Pokud je token stále platný, je připojení k lokalitě pomocí CMG dostatečné. Pokud se token během 90 dnů prodlouží, klient se musí přímo připojit k bodu správy v interní síti, aby získal nový token.

Nemůžete obnovit token hromadné registrace. Jakmile vyprší platnost tokenu hromadné registrace, vygenerujte novou službu pro registraci internetových zařízení pomocí CMG.

## <a name="see-also"></a>Viz také:

- [Plánování brány pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md)

- [Instalace a přiřazení Configuration Manager klientů s Windows 10, kteří používají Azure AD k ověřování](deploy-clients-cmg-azure.md)
