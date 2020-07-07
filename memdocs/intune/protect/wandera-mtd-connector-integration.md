---
title: Nastavení integrace ochrany před mobilními hrozbami Wandera v Intune
titleSuffix: Intune on Azure
description: Jak nastavit řešení ochrany před mobilními hrozbami Wandera pomocí Microsoft Intune pro řízení přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc44bb114d6ff9089a01da2d0b7db7aa7527f4b5
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972143"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Integrace ochrany před mobilními hrozbami Wandera pomocí Intune  

Provedením následujících kroků Integrujte řešení ochrany před mobilními hrozbami Wandera do Intune.  

## <a name="before-you-begin"></a>Než začnete  

Než začnete s integrací Wandera do Intune, ujistěte se, že jsou splněné následující požadavky:

- Předplatné Intune
- Azure Active Directory přihlašovací údaje správce a přiřazenou roli, která může udělit následující oprávnění:

    - Přihlášení a čtení profilu uživatele
    - Přístup k adresáři jako přihlášený uživatel
    - Čtení dat z adresáře
    - Odesílání informací o rizikech zařízení do Intune
 
- Platné předplatné Wandera
    - Účet správce s oprávněními správce superuživatele

## <a name="integration-overview"></a>Přehled integrace

Povolení integrace ochrany před mobilními hrozbami mezi Wandera a Intune zahrnuje:

- Povolení služby UEM Connect pro Wandera k synchronizaci informací s Azure a Intune To zahrnuje metadata správy životního cyklu uživatelů a zařízení (LCM), spolu s úrovní hrozby pro zařízení ochrany před mobilními hrozbami (MTD).
- Vytvořte v Wandera profily aktivace, které definují chování při registraci zařízení.
- Nasaďte Wandera přes Air na spravovaná zařízení s iOS a Androidem.
- Nakonfigurujte Wandera pro samoobslužné služby koncového uživatele pomocí MAM – máme nespravovaná zařízení s iOS a Androidem.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Nastavení integrace ochrany před mobilními hrozbami Wandera

Nastavení integrace mezi Wandera a Intune nevyžaduje žádnou podporu od zaměstnanců Wandera a dá se snadno dosáhnout v řádu minut.

### <a name="enable-support-for-wandera-in-intune"></a>Povolení podpory pro Wandera v Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**  >  **ochrany před mobilními hrozbami**  >  **Přidat**.
3. Na stránce **Přidat konektor** použijte rozevírací seznam a vyberte **Wandera**. A pak vyberte **vytvořit**.  
4. V podokně obrana proti mobilním hrozbám vyberte konektor **Wandera** MTD ze seznamu konektorů a otevřete tak podokno **Upravit konektor** . Vyberte **otevřít konzolu pro správu Wandera** , otevřete [paprskový](https://radar.wandera.com/login), konzolu pro správu Wandera a přihlaste se. 
5. V konzole Wandera PAPRSKy přejděte na **integrace > UEM Integration**a vyberte kartu **UEM připojit** . použijte rozevírací seznam dodavatel modulu EMM a vyberte možnost **Microsoft Intune**.
6. Zobrazí se obrazovka podobná následujícímu, která značí, že udělení oprávnění je nutné k dokončení integrace:

   ![Integrace a oprávnění](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Vedle synchronizace uživatelů a zařízení Intune klikněte na tlačítko udělení a zahajte tak proces poskytování souhlasu Wandera k provádění funkcí řízení životního cyklu (LCM) pomocí Azure a Intune.
8. Po zobrazení výzvy vyberte nebo zadejte svoje přihlašovací údaje správce Azure. Zkontrolujte požadovaná oprávnění a potom zaškrtněte políčko pro vyjádření souhlasu jménem vaší organizace. Nakonec kliknutím na přijmout potvrďte integraci LCM.

   ![Přijmout oprávnění](./media/wandera-mtd-connector-integration/permissions.png)

10. Vrátíte se automaticky zpátky do konzoly pro správu PAPRSKů.  Pokud byla autorizace úspěšná, zobrazí se vedle tlačítka pro udělení zelený znak zaškrtnutí.
11. Opakujte postup souhlasu pro zbývající uvedená integrace kliknutím na jejich odpovídající tlačítka udělit, dokud nebudete mít zelený symbol zaškrtnutí vedle každého.

    ![Skupina synchronizace](./media/wandera-mtd-connector-integration/sync-group-name.png)

12. Vraťte se do konzoly Intune a pokračujte v úpravách konektoru Wandera MTD. Nastavte všechny dostupné přepínače na zapnuto a pak konfiguraci uložte.

    ![Povolit Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune a Wandera jsou teď připojené.

## <a name="create-activation-profiles-in-wandera"></a>Vytvoření profilů aktivace v Wandera

Nasazení založená na Intune se usnadňují pomocí profilů aktivace Wandera definovaných v PAPRSKech.  Každý aktivační profil definuje konkrétní možnosti konfigurace, jako jsou požadavky na ověřování, možnosti služby a počáteční členství ve skupině.

Po vytvoření profilu aktivace v Wandera ho přiřadíte uživatelům a zařízením v Intune.  I když je aktivační profil univerzální napříč platformami zařízení a strategiemi správy, níže uvedené kroky definují, jak nakonfigurovat Intune na základě těchto rozdílů.

Tento postup předpokládá, že jste v Wandera vytvořili aktivační profil, který chcete nasadit přes Intune na cílová zařízení. Další podrobnosti o vytváření a používání profilů aktivace Wandera najdete v [Průvodci aktivačními profily](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links) .

> [!NOTE]
> Když vytváříte aktivační profily pro nasazení prostřednictvím Intune nebo MAM-WE, nezapomeňte nastavit přidruženého uživatele na ověřování od poskytovatele identity > Azure Active Directory možnost pro maximální zabezpečení, kompatibilitu s více platformami a jednodušší prostředí koncového uživatele.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Nasazení Wandera do zařízení spravovaných přes MDM

U zařízení s iOS a Androidem, která jsou spravovaná pomocí Intune, se Wandera dá nasadit přes Air pro rychlé aktivace založené na nabízených oznámeních. Ujistěte se, že jste už vytvořili aktivační profily, které potřebujete, než budete pokračovat v této části. Nasazení Wandera do spravovaných zařízení zahrnuje:
- Přidání profilů konfigurace Wandera do Intune a přiřazení k cílovým zařízením
- Přidání aplikace Wandera a příslušných konfigurací aplikace do Intune a přiřazení k cílovým zařízením.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>Konfigurace a nasazení konfiguračních profilů pro iOS 

V této části stáhnete **požadované** konfigurační soubory zařízení s iOS a pak je doručíte přes Air přes MDM na vaše zařízení spravovaná přes Intune.

1. V **paprskovém**prostředí přejděte do aktivačního profilu, který chcete nasadit (zařízení > aktivace), a pak klikněte na **kartu strategie nasazení > spravovaná zařízení > Microsoft Endpoint Manager**.
2. Rozbalte oddíly **Apple iOS pod dohledem** nebo Apple iOS, které nejsou **pod dohledem** , na základě konfigurace loďstva zařízení.
3. Stáhněte si poskytnuté konfigurační profily a připravte je, abyste je nahráli v následujícím kroku.
4. Otevřete **Microsoft Intune konzolu pro správu** a přejděte na **zařízení > iOS/iPadOS > konfiguračních profilů**.  Klikněte na **Vytvořit profil**.
5. Na panelu, který se zobrazí, zvolte v části **platforma**možnost **iOS/iPadOS** a pak na **vlastní** v části profil. Pak klikněte na **vytvořit**.
6. Do pole **název** zadejte popisný název pro konfiguraci. v ideálním případě se přiřadíte k tomu, co jste pojmenovali profil aktivace v paprskech. To vám usnadní křížové odkazy v budoucnu. Případně můžete v případě potřeby zadat kód aktivačního profilu. Doporučujeme, abyste zjistili, jestli je konfigurace pro zařízení pod dohledem nebo bez dohledu, podle přípony názvu jako takového.
7. Volitelně můžete zadat **Popis** poskytující další podrobnosti pro ostatní správce týkající se účelu nebo použití konfigurace. Klikněte na **Další**.
8. Klikněte na **Vybrat soubor** a vyhledejte stažený konfigurační profil, který odpovídá příslušnému aktivačnímu profilu staženému v kroku 3. Pokud jste stáhli obojí, je vhodné vybrat profil v režimu pod dohledem nebo bez dohledu. Klikněte na **Další**.
   <!-- image placeholder - ending future availability -->
9.  Definujte **značky oboru** podle požadavků v postupech správy RBAC v Intune.  Klikněte na **Další**.
10. **Přiřaďte** konfigurační profil skupinám uživatelů nebo zařízení, které by měly mít nainstalované Wandera.  Doporučujeme začít se skupinou testu a potom po ověření správné práce s aktivací rozšířit. Klikněte na **Další**.
11. Podle potřeby zkontrolujte konfiguraci správných úprav a kliknutím na **vytvořit** vytvořte a nasaďte konfigurační profil.

> [!NOTE]
> Wandera nabízí profil rozšířeného nasazení pro zařízení s iOS pod dohledem. Pokud máte smíšené loďstvo zařízení pod dohledem a bez dohledu, podle potřeby opakujte výše uvedené kroky pro jiný typ profilu. Pro všechny budoucí aktivační profily, které se mají nasadit přes Intune, se musí použít stejný postup. Pokud máte smíšené loďstvo zařízení s iOS pod dohledem a bez dohledu a potřebujete pomoc s dohledem na základě přiřazení zásad založených na režimu, obraťte se prosím na podporu Wandera. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Nasazení Wandera do zařízení MAM
Pro zařízení, která nespravuje Intune a jsou (MAM), využívá Wandera integrované prostředí pro registraci na základě ověřování k aktivaci a ochraně firemních dat v aplikacích s podporou MAM. 

Následující části popisují, jak nakonfigurovat Wandera a Intune, aby koncoví uživatelé mohli bezproblémově aktivovat Wandera předtím, než budou mít přístup k firemním datům. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Konfigurace zřizování zařízení Azure v profilu aktivace Wandera
Aktivační profily, které se mají používat s MAM – k dispozici je potřeba, abyste měli přidružené uživatelské nastavení > Azure Active Directory možnost ověřený zprostředkovatelem identity.
1. V **paprskovém portálu Wandera** vyberte existující nebo vytvořte nový, aktivační profil, který mam – zařízení budou používána během registrace v zařízeních > aktivací. 
2. Klikněte na **kartu strategie nasazení a pak na nespravovaná zařízení** přejděte do části **Azure Device Provisioning** .
3. Do příslušného textového pole zadejte **ID tenanta Azure AD** . Pokud nemáte ID tenanta na ruce, klikněte na odkaz **získat ID tenanta** a otevřete službu Azure AD na nové kartě, kde můžete tuto hodnotu snadno zkopírovat do schránky.
4. Volitelné Zadejte **ID skupiny** pro omezení aktivací uživatelů na konkrétní skupiny.
   - Pokud je definováno jedno nebo více **ID skupiny** , uživatel aktivuje mam-musíme být členem aspoň jedné z určených skupin pro aktivaci pomocí tohoto aktivačního profilu.
   - Můžete nastavit víc aktivačních profilů nakonfigurovaných se stejným ID tenanta Azure, ale s různými ID skupin. To umožňuje registrovat zařízení do Wandera na základě členství ve skupinách Azure a povolit v době aktivace odlišné možnosti podle skupin.
   - Můžete nakonfigurovat jeden "výchozí" aktivační profil, který neurčuje žádné ID skupiny.  Tato skupina bude sloužit jako zachytávací vše pro všechny aktivace, ve kterých ověřený uživatel není členem skupiny s přidružením k jinému aktivačnímu profilu.
5. V pravém horním rohu stránky klikněte na **Uložit** .

## <a name="next-steps"></a>Další kroky
- Když máte profily aktivace Wandera načtené v PAPRSKech, vytvořte v Intune klientské aplikace, které nasadí aplikaci Wandera na zařízení s Androidem a iOS/iPadOS. Konfigurace aplikace Wandera poskytuje základní funkce pro bezplatné navýšení konfiguračních profilů zařízení a doporučuje se pro všechna nasazení. Další informace najdete v tématu [Přidání aplikací MTD](mtd-apps-ios-app-configuration-policy-add-assign.md) pro postupy a vlastní podrobnosti specifické pro aplikace Wandera. 
- Teď, když máte Wandera integrovanou se správcem koncových bodů, teď můžete ladit konfiguraci, zobrazovat sestavy a v rámci vašeho loďstva mobilních zařízení mnohem nasazovat. Podrobné pokyny pro konfiguraci najdete v tématu [průvodce Začínáme Support Center](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) v dokumentaci k Wandera.
