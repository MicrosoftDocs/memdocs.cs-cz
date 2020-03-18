---
title: Nastavení podmíněného přístupu na základě zařízení s Intune
titleSuffix: Microsoft Intune
description: Naučte se vytvářet zásady podmíněného přístupu na základě zařízení, které jsou založené na Microsoft Intune dodržování předpisů zařízením a správu mobilních aplikací.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43fedfe33f39e7301dfa0bb57fc45b01914c7d64
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329471"
---
# <a name="create-a-device-based-conditional-access-policy"></a>Vytvoření zásady podmíněného přístupu na základě zařízení

V Intune můžete rozšířit podmíněný přístup v Azure Active Directory tím, že přidáte dodržování předpisů mobilním zařízením pro řízení přístupu. Díky zásadám dodržování předpisů Intune, které definují požadavky na dodržování předpisů pro zařízení, můžete použít stav dodržování předpisů zařízení, abyste povolili nebo zablokovali přístup k vašim aplikacím a službám. Můžete to udělat tak, že vytvoříte zásadu podmíněného přístupu, která používá nastavení **vyžadovat, aby zařízení bylo označené jako vyhovující**.

Zásady podmíněného přístupu určují aplikace nebo služby, které chcete chránit, podmínky, za kterých se dají přistupovat k aplikacím nebo službám, a uživatelům, pro které se zásady vztahují. I když je podmíněný přístup funkcí Azure AD Premium, uzel podmíněného přístupu, ke kterému přistupujete z *Intune* , je stejný uzel, ke kterému se přistupuje z *Azure AD*.

> [!IMPORTANT]
> Před nastavením podmíněného přístupu budete muset nastavit zásady dodržování předpisů zařízením v Intune, které budou vyhodnocovat zařízení na základě toho, jestli splňují konkrétní požadavky. Přečtěte si téma Začínáme [se zásadami dodržování předpisů zařízeními v Intune](device-compliance-get-started.md).

## <a name="create-conditional-access-policy"></a>Vytvořit zásady podmíněného přístupu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **podmíněný přístup** > **zásady** > **nové zásady**.
  ![vytvořit nové zásady podmíněného přístupu](./media/create-conditional-access-intune/create-ca.png)

3. V části **Přiřazení** vyberte **Uživatelé a skupiny**.

4. Na kartě **Zahrnout** Určete uživatele nebo skupiny, pro které platí tyto zásady podmíněného přístupu. Po zvolení skupin nebo uživatelů, kteří mají být zahrnuti, použijte kartu **vyloučit** , pokud existují uživatelé, role nebo skupiny, které chcete vyloučit z těchto zásad.

   - **Všichni uživatelé**: tuto možnost vyberte, pokud chcete zásady použít pro všechny uživatele a skupiny, včetně interních uživatelů a uživatelů typu Host.

   - **Vyberte uživatelé a skupiny**: Vyberte tuto možnost a zadejte jednu nebo více z následujících možností:
  
     1. **Všichni uživatelé typu Host**: tuto možnost vyberte, pokud chcete zahrnout nebo vyloučit externí uživatele typu Host (například partneři, externí spolupracovníci).

     2. **Role adresáře**: vyberte jednu nebo více rolí Azure AD, chcete-li zahrnout nebo vyloučit uživatele, kteří jsou přiřazeni k těmto rolím.

     3. **Uživatelé a skupiny**: tuto možnost vyberte, pokud chcete hledat a vybrat jednotlivé uživatele nebo skupiny, které chcete zahrnout nebo vyloučit.

        > [!TIP]
        > Otestujte zásadu s menší skupinou uživatelů, abyste se ujistili, že funguje podle očekávání.

5. Vyberte **Hotovo**.

6. V části **přiřazení**vyberte **cloudové aplikace nebo akce**.

7. Na kartě **Zahrnout** použijte dostupné možnosti k identifikaci aplikací a služeb, které chcete chránit pomocí těchto zásad podmíněného přístupu. Pak můžete použít kartu **vyloučit** , pokud existují nějaké aplikace nebo služby, které chcete z této zásady vyloučit.

   - **Všechny cloudové aplikace**: tuto možnost vyberte, pokud chcete zásady použít pro všechny aplikace.
     > [!IMPORTANT]
     > V tomto seznamu je obsažena aplikace Microsoft Azure Management pro přístup k Azure Portal. Nezapomeňte použít kartu **vyloučit** buď zde, nebo v možnostech **uživatelů a skupin** , abyste se ujistili, že jste (nebo uživatelé nebo skupiny, které určíte), se budou moci přihlásit k Azure Portal. 

   - **Vybrat aplikace**: Vyberte tuto možnost, zvolte **Vybrat**a pak pomocí seznamu aplikace vyhledejte a vyberte aplikace nebo služby, které chcete chránit.

   Až budete připraveni, vyberte **Hotovo**.

8. V části **přiřazení**vyberte **podmínky**.

   - **Riziko přihlášení**: vyberte *Ano* , pokud chcete s touto zásadou používat Azure AD Identity Protection zjišťování rizik při přihlašování, a pak zvolte úrovně rizika přihlašování, na které se zásady mají vztahovat.

   - **Platformy zařízení**: na kartě **Zahrnout** určete platformy zařízení, pro které chcete tyto zásady podmíněného přístupu použít. K vyloučení platforem z této zásady použijte kartu **vyloučit** .

   - **Umístění**: na kartě **Zahrnout** určete, jestli se zásada vztahuje na:
     - Jakékoli umístění
     - Důvěryhodná síťová umístění, která jsou pod kontrolou vašeho IT oddělení
     - Konkrétní síťová umístění.

     Pomocí karty **vyloučit** z těchto zásad vylučte síťová umístění.

   - **Klientské aplikace**: Pokud chcete určit, jestli se má zásada vztahovat na aplikace prohlížeče, mobilní aplikace a desktopové klienty, vyberte *Ano* .

   - **Stav zařízení**: zásady podmíněného přístupu se použijí na všechny stavy zařízení, pokud nevyberete Ano a výslovně vyloučíte stav zařízení, připojené k hybridní službě Azure AD nebo zařízení označené jako kompatibilní (nebo obojí).

     > [!TIP]
     > Pokud chcete chránit oba klienty pro **moderní ověřování** i **klienty Exchange ActiveSync**, vytvořte dvě samostatné zásady podmíněného přístupu, jednu pro každý typ klienta. I když Exchange ActiveSync podporuje moderní ověřování, jediná podmínka, kterou podporuje Exchange ActiveSync, je platforma. Další podmínky, včetně Multi-Factor Authentication, se nepodporují. Pokud chcete efektivně chránit přístup k Exchangi Online z Exchange ActiveSync, vytvořte zásadu podmíněného přístupu, která určuje cloudovou aplikaci Office 365 Exchange Online a klientskou aplikaci Exchange ActiveSync se zásadami použít jenom pro vybrané podporované platformy.

9. Vyberte **Hotovo**.

10. V části **Ovládací prvky přístupu** zvolte **Udělení**. Nakonfigurujte, co se stane na základě podmínek, které jste nastavili.  Můžete vybrat z následujících možností:

    - **Blokovat přístup**: uživatelům zadaným v této zásadě bude odepřen přístup k aplikacím za podmínek, které jste zadali.
    - **Udělení přístupu**: uživatelům zadaným v této zásadě se udělí přístup, ale můžete potřebovat některou z následujících akcí:
      - **Vyžadovat vícefaktorové ověřování**: uživatel bude muset provést další požadavky na zabezpečení, jako je telefonní hovor nebo text.
      - **Vyžadovat, aby zařízení bylo označené jako vyhovující**: zařízení musí být kompatibilní s Intune. Pokud zařízení nedodržuje předpisy, zobrazí se uživateli možnost zaregistrovat zařízení v Intune.
      - **Vyžadovat zařízení připojené k hybridní službě Azure AD**: zařízení musí být připojená k hybridní službě Azure AD.
      - **Vyžadovat schválenou klientskou aplikaci**: zařízení musí používat schválené klientské aplikace. 
      - **Pro více ovládacích prvků**: vyberte **vyžadovat všechny vybrané ovládací prvky** , aby se všechny požadavky vynutily, když se zařízení pokusí o přístup k aplikaci.

      ![Nastavení udělení řízení přístupu](./media/create-conditional-access-intune/create-ca-grant-access-settings.png)

11. V části **Povolit zásadu** vyberte **Zapnuto**.

12. Vyberte **Vytvořit**.

## <a name="next-steps"></a>Další kroky

[Podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md)

[Řešení potíží s podmíněným přístupem Intune](https://support.microsoft.com/help/4456106)
