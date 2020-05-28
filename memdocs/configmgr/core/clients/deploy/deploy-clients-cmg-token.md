---
title: Ověřování na základě tokenů pro CMG
titleSuffix: Configuration Manager
description: Zaregistrujte klienta v interní síti pro jedinečný token nebo vytvořte token pro hromadnou registraci pro Internetová zařízení.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6b33027d67329b883f401168795c1b466ded1a7
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709382"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Ověřování založené na tokenech pro bránu pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

<!--5686290-->

Brána pro správu cloudu (CMG) podporuje mnoho typů klientů, ale i s [rozšířenými http](../../plan-design/hierarchy/enhanced-http.md), tito klienti vyžadují [certifikát pro ověřování klientů](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Tento požadavek na certifikát může být náročný na zřízení internetových klientů, kteří se často nepřipojují k interní síti, nelze se připojit Azure Active Directory (Azure AD) a nemusíte mít k dispozici metodu pro instalaci certifikátu vystaveného infrastrukturou veřejných klíčů.

Aby se tyto výzvy vyřešily od verze 2002, Configuration Manager rozšiřuje podporu zařízení následujícími způsoby:

- Registrace k interní síti pro jedinečný token

- Vytvoření hromadné registračního tokenu pro Internetová zařízení

Pokud chcete plně využít tuto funkci, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. Kompletní scénář není funkční, dokud nebude verze klienta zároveň nejnovější. V případě potřeby se ujistěte, že [povýšíte novou verzi klienta na produkční](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)prostředí.

Klient Configuration Manager společně s bodem správy spravuje tento token, takže neexistuje žádná závislost verze operačního systému. Tato funkce je k dispozici pro libovolnou [podporovanou verzi operačního systému klienta](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Tyto metody podporují jenom scénáře správy zaměřené na zařízení.
>
> Microsoft doporučuje připojit zařízení k Azure AD. Internetová zařízení můžou pomocí Azure AD ověřit pomocí Configuration Manager. Také umožňuje scénářům zařízení i uživatele, zda je zařízení na internetu nebo připojeno k interní síti. Další informace najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Zaregistrujte se do interní sítě.

Tato metoda vyžaduje, aby se klient nejdřív zaregistroval s bodem správy v interní síti. K registraci klienta obvykle dochází po instalaci hned po instalaci. Bod správy dává klientovi jedinečný token, který ukazuje, že používá certifikát podepsaný svým držitelem. Když se klient přenáší do Internetu, aby komunikoval s CMG, spáruje svůj certifikát podepsaný svým držitelem pomocí tokenu vydaného bodem správy. Klient obnoví token jednou za měsíc a je platný po 90 dnech.

Lokalita toto chování umožňuje ve výchozím nastavení.

## <a name="create-a-bulk-registration-token"></a>Vytvoření tokenu hromadné registrace

Pokud nemůžete instalovat a registrovat klienty v interní síti, vytvořte token pro hromadnou registraci. Tento token použijte, když se klient nainstaluje na internetové zařízení a zaregistruje se přes CMG. Registrační token pro hromadnou registraci má krátkou dobu platnosti a není uložený v klientovi nebo lokalitě. Umožňuje klientovi generovat jedinečný token, který se spáruje s certifikátem podepsaným svým držitelem, a umožňuje ověřování pomocí CMG.

1. Přihlaste se k serveru lokality nejvyšší úrovně v hierarchii s oprávněními místního správce.

1. Otevřete příkazový řádek jako správce.

1. Spusťte nástroj ze `\bin\X64` složky instalačního adresáře Configuration Manager na serveru lokality: `BulkRegistrationTokenTool.exe` . Vytvořte nový token s `/new` parametrem. Například, `BulkRegistrationTokenTool.exe /new`. Další informace najdete v tématu [použití nástroje pro hromadnou registraci tokenu](#bulk-registration-token-tool-usage).

1. Zkopírujte token a uložte ho na bezpečném místě.

1. Nainstalujte klienta Configuration Manager do internetového zařízení. Zahrňte parametr instalace klienta: [**/regtoken**](about-client-installation-properties.md#regtoken). Následující příklad příkazového řádku obsahuje další požadované parametry a vlastnosti instalace:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Další informace o tomto příkazovém řádku najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Tento proces je podobný, ale nepoužívá vlastnosti Azure AD.

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

#### <a name="to-review-a-bulk-registration-token"></a>Postup při kontrole hromadných registračních tokenů

1. V konzole Configuration Manager klikněte na možnost **Správa**.

2. V pracovním prostoru Správa rozbalte položku **zabezpečení**a klikněte na položku **certifikáty**. Konzola obsahuje seznam všech certifikátů souvisejících s lokalitami a registračních tokenů pro hromadnou registraci v podokně podrobností.

3. Vyberte token hromadné registrace, který chcete zkontrolovat.

Můžete identifikovat konkrétní registrační tokeny na základě identifikátoru GUID. V době vytváření tokenu se zobrazují identifikátory GUID pro tokeny hromadné registrace. V případě potřeby můžete také filtrovat nebo řadit podle sloupce **typ** .

#### <a name="to-block-a-bulk-registration-token"></a>Blokování hromadné registračního tokenu

1. V konzole Configuration Manager klikněte na možnost **Správa**.

2. V pracovním prostoru Správa rozbalte položku **zabezpečení**, klikněte na položku **certifikáty**a vyberte token hromadné registrace, který chcete blokovat.

3. Na kartě **Domů** na panelu nástrojů nebo v nabídce obsahu klikněte pravým tlačítkem myši na položku **blokovat**. Naopak můžete zrušit blokování dříve blokovaných hromadných registračních tokenů tak, že na kartě **Domů** na pásu karet nebo v nabídce obsah kliknete pravým tlačítkem na položku **odblokovat** .

## <a name="see-also"></a>Viz také

- [Plánování brány pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md)

- [Instalace a přiřazení Configuration Manager klientů s Windows 10, kteří používají Azure AD k ověřování](deploy-clients-cmg-azure.md)
