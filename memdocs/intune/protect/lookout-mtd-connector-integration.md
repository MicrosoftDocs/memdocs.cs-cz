---
title: Nastavení integrace služby Lookout s Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o integraci Intune s funkcí Mobile Endpoint Security, jako je řešení ochrany před mobilními hrozbami, pro řízení přístupu mobilních zařízení k firemním prostředkům.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/11/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5b0d7644-3183-45ba-a165-0d82d70cb71e
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54e81a7b9614e1633fe9061fd13d1b99810ce43c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329219"
---
# <a name="set-up-lookout-mobile-endpoint-security-integration-with-intune"></a>Nastavení integrace zabezpečení mobilních koncových bodů pomocí Intune
S prostředím, které splňuje [požadavky](lookout-mobile-threat-defense-connector.md#prerequisites), můžete integrovat mobilní koncové body zabezpečení s Intune. Informace v tomto článku vás provedou nastavením integrace a konfigurací důležitých nastavení ve službě Intune pro použití s Intune.  

> [!IMPORTANT]
> Existujícího tenanta Lookout Mobile Endpoint Security, který ještě není přidružený k vašemu tenantovi Azure AD, nejde použít k integraci s Azure AD a Intune. Pokud chcete vytvořit nového tenanta Lookout Mobile Endpoint Security, obraťte se na podporu Lookoutu. Pomocí tohoto nového tenanta můžete připojit uživatele Azure AD.

## <a name="collect-azure-ad-information"></a>Shromáždění informací z Azure AD  
Pokud chcete integrovat se službou Intune, přidružíte svého tenanta pro zabezpečení vašeho mobilního prostředí koncových bodů k vašemu předplatnému služby Azure Active Directory (AD).

Pokud chcete povolit integraci předplatného mobilního koncového bodu zabezpečení s Intune, poskytněte podporuenterprisesupport@lookout.comvyhledávání následující informace:  

- **ID adresáře tenanta Azure AD**  

- **ID objektu skupiny Azure AD** pro skupinu s **úplným** přístupem ke konzole nástroje Mobile Endpoint Security (status)  
  Tuto skupinu uživatelů ve službě Azure AD vytvoříte tak, aby obsahovala uživatele, kteří mají *úplný přístup* k přihlašování do **konzoly pro hledání**. Uživatelé musí být členy této skupiny nebo volitelné skupiny *s omezeným* přístupem, aby se mohli přihlásit ke konzole pro hledání. 

- **ID objektu skupiny Azure AD** pro skupinu s **omezeným** přístupem ke konzole pro přístup *(volitelná skupina)* 
  Tuto volitelnou skupinu uživatelů ve službě Azure AD vytvoříte tak, aby obsahovala uživatele, kteří by neměli mít přístup k několika modulům konzoly pro vyhledávání v konfiguraci a registraci. Místo toho mají tito uživatelé přístup jen pro čtení k modulu **zásad zabezpečení** v konzole pro hledání. Aby se uživatelé mohli přihlásit ke konzole pro hledání, musí být členy této volitelné skupiny nebo povinným *úplným přístupem* .

 > [!TIP] 
 > Další podrobnosti o oprávněních najdete v [tomto článku](https://personal.support.lookout.com/hc/articles/114094105653) na webu Lookout.

### <a name="collect-information-from-azure-ad"></a>Shromažďování informací z Azure AD 

1. Přihlaste se k [Azure Portal](https://portal.azure.com) pomocí účtu globálního správce.

2. Přejděte na **Azure Active Directory** > **vlastnosti** a vyhledejte **ID adresáře**. Pomocí tlačítka *Kopírovat* zkopírujte ID adresáře a uložte ho do textového souboru.

   ![Vlastnosti služby Azure AD](./media/lookout-mtd-connector-integration/azure-ad-properties.png)  

3. V dalším kroku Najděte ID skupiny Azure AD pro účty, které používáte k udělení přístupu uživatelům Azure AD k konzole pro vyhledávání. Jedna skupina má *úplný přístup*a druhá skupina pro *omezený přístup* je volitelná. Pro získání *ID objektu*pro každý účet:  
   1. Chcete-li otevřít podokno *skupiny – všechny skupiny* , otevřete **Azure Active Directory** > **skupiny** .  

   2. Vyberte skupinu, kterou jste vytvořili pro *úplný přístup* , a otevřete její podokno *přehledu* .  

   3. Pomocí tlačítka *Kopírovat* zkopírujte ID objektu a uložte ho do textového souboru.  

   4. Pokud použijete tuto skupinu, opakujte postup pro skupinu *s omezeným* přístupem.  

      ![ID objektu skupiny Azure AD](./media/lookout-mtd-connector-integration/azure-ad-group-id.png)  

   Po shromáždění těchto informací se obraťte na podporu vyhledávání (e-mail: enterprisesupport@lookout.com). Podpora vyhledávání bude spolupracovat s vaším primárním kontaktem k připojení vašeho předplatného a vytvoření účtu vaší organizace pro hledání pomocí informací, které zadáte.  

## <a name="configure-your-lookout-subscription"></a>Konfigurace předplatného pro hledání  

Následující kroky se dokončí v konzole pro správu vyhledávání v podniku a umožní připojení ke službě vyhledávání pro zařízení zaregistrovaná v Intune (prostřednictvím dodržování předpisů zařízením) **a** neregistrovaných zařízení (prostřednictvím zásad ochrany aplikací).

Když podpora vyhledávání vytvoří účet pro hledání v podnikovém účtu, zaznamená vám podpora hledání na primární kontakt vaší společnosti e-mail s odkazem na přihlašovací adresu URL: https://aad.lookout.com/les?action=consent. 

### <a name="initial-sign-in"></a>Počáteční přihlášení  
Při prvním přihlášení ke konzole nástroje pro vyhledávání se zobrazí stránka souhlasu (https://aad.lookout.com/les?action=consent). Globální správce Azure AD stačí přihlásit a **přijmout**. Následné přihlášení nevyžaduje, aby uživatel měl tuto úroveň oprávnění Azure AD. 

 Zobrazí se stránka pro vyjádření souhlasu. Kliknutím na tlačítko **přijmout** dokončete registraci. 
   ![snímek obrazovky první přihlašovací stránky pro konzolu pro vyhledávání](./media/lookout-mtd-connector-integration/lookout_mtp_initial_login.png)

Když souhlasíte a souhlasíte, budete přesměrováni do konzoly pro hledání.

Po dokončení počátečního přihlášení a souhlasu se uživatelé, kteří se přihlásí ze služby https://aad.lookout.com , přesměrují do konzoly. Pokud se souhlas ještě neudělil, všechny pokusy o přihlášení mají za následek chybnou přihlašovací chybu.

### <a name="configure-the-intune-connector"></a>Konfigurace konektoru Intune  
Následující postup předpokládá, že jste dříve vytvořili skupinu uživatelů ve službě Azure AD za účelem testování vašeho nasazení vyhledávání. Osvědčeným postupem je začít s malou skupinou uživatelů, aby mohli správci Intune seznámit s integrací produktů. Po jejich znalosti můžete registraci rozšíříte do dalších skupin uživatelů.

1. Přihlaste se ke konzole nástroje pro [hledání](https://aad.lookout.com) a pak **na systémové** > **konektory**a pak vyberte **Přidat konektor**.  Vyberte **Intune**.

   ![Obrázek konzoly pro hledání s možností Intune na kartě konektory](./media/lookout-mtd-connector-integration/lookout_mtp_setup-intune-connector.png)

2. V podokně *Microsoft Intune* vyberte **nastavení připojení** a určete **frekvenci prezenčního signálu** v minutách. 

   ![Obrázek karty nastavení připojení s nakonfigurovanou frekvencí prezenčního signálu](./media/lookout-mtd-connector-integration/lookout-mtp-connection-settings.png)

3. Vyberte **Správa**registrací a **použijte následující skupiny zabezpečení Azure AD k identifikaci zařízení, která by se měla zaregistrovat v Lookout for Work**, zadejte *název skupiny* skupiny Azure AD, který se má použít pro hledání, a pak vyberte **Uložit změny**.

    ![snímek obrazovky zobrazující stránku registrace konektoru Intune](./media/lookout-mtd-connector-integration/lookout-mtp-enrollment.png)  

   **O používaných skupinách**:
   - Osvědčeným postupem je začít se skupinou zabezpečení Azure AD, která obsahuje malý počet uživatelů k testování integrace vyhledávání.
   - V **názvu skupiny** se rozlišují velká a malá písmena, jak je uvedeno ve **vlastnostech** skupiny zabezpečení v Azure Portal.  
   - Skupiny, které zadáte pro **správu** registrací, definují skupinu uživatelů, jejichž zařízení se budou registrovat s vyhledáváním. Když je uživatel ve skupině pro registraci, jejich zařízení ve službě Azure AD se zaregistrují a budou mít nárok na aktivaci v rámci služby. Když uživatel poprvé otevře aplikaci *Lookout for Work* na podporovaném zařízení, zobrazí se výzva k její aktivaci.

4. Vyberte **synchronizace stavu** a zajistěte, aby byl *stav zařízení* i *stav hrozby* nastaven **na zapnuto**.  Obě jsou potřeba, aby integrace se službou Intune správně fungovala.  

5. Vyberte možnost **Správa chyb**, zadejte e-mailovou adresu, která by měla přijímat zprávy o chybách, a pak vyberte **Uložit změny**.
 
   ![snímek obrazovky zobrazující stránku správy chyb konektoru Intune](./media/lookout-mtd-connector-integration/lookout-mtp-connector-error-notifications.png)

6. Pro dokončení konfigurace konektoru vyberte **vytvořit konektor** . Později, až budete s výsledky spokojeni, můžete registraci roztáhnout na další skupiny uživatelů.

## <a name="configure-intune-to-use-lookout-as-a-mobile-threat-defense-provider"></a>Konfigurace Intune pro použití jako poskytovatele ochrany před mobilními hrozbami
Až nakonfigurujete Intune, musíte nastavit připojení, které se bude [zobrazovat v Intune](mtd-connector-enable.md).  

## <a name="additional-settings-in-the-lookout-mes-console"></a>Další nastavení v konzole pro hledání na netržních modulech
Níže najdete další nastavení, která můžete konfigurovat v konzole nástroje pro vyhledávání.  

### <a name="configure-enrollment-settings"></a>Konfigurace nastavení registrace
V konzole prohledat v **systému vyberte systém** > **Spravovat** > **Nastavení registrace**registrace.  

- V poli **stav odpojeno**zadejte počet dní, než se nepřipojené zařízení označí jako odpojené.  

  Odpojená zařízení se považují za nevyhovující a přístup k firemním aplikacím se jim zablokuje na základě zásad podmíněného přístupu Intune. Můžete zadat hodnotu mezi 1 a 90 dny.

  ![Podívejte se na nastavení registrace v modulu System.](./media/lookout-mtd-connector-integration/lookout-console-enrollment-settings.png)

### <a name="configure-email-notifications"></a>Konfigurace e-mailových oznámení
Pokud chcete dostávat e-mailová upozornění na hrozby, přihlaste se ke [konzole pro hledání](https://aad.lookout.com) v prostředí s uživatelským účtem, který by měl dostávat oznámení.  

- Pokračujte na **Předvolby** a pak nastavte oznámení, která chcete **dostávat, a**pak změny **uložte** .  

- Pokud už nechcete dostávat e-mailová oznámení, nastavte oznámení na **vypnuto** a uložte změny.

  ![snímek obrazovky se stránkou předvolby se zobrazeným uživatelským účtem](./media/lookout-mtd-connector-integration/lookout-mtp-email-notifications.png)

## <a name="configure-threat-classifications"></a>Konfigurace klasifikací hrozeb  
Vyhledá se mobilní koncový bod zabezpečení, klasifikuje mobilní hrozby různých typů. Klasifikace hrozeb ve službě Lookout k nim má přiřazené výchozí úrovně rizika. Úrovně rizika lze kdykoli změnit tak, aby vyhovovaly vašim požadavkům vaší společnosti.

Informace o klasifikacích úrovně hrozeb a o tom, jak spravovat úrovně rizik, které jsou k nim přidružené, najdete v tématu [Reference k hrozbám hledání](https://enterprise.support.lookout.com/hc/articles/360011812974).

>[!IMPORTANT]
> Úrovně rizika představují důležitý aspekt zabezpečení mobilních koncových bodů, protože integrace Intune počítá dodržování předpisů zařízením podle těchto úrovní rizik za běhu.  
> 
> Správce Intune nastaví v zásadách pravidlo, které určí, že zařízení nedodržuje předpisy, pokud má aktivní hrozbu s minimální úrovní **Vysoká**, **střední**nebo **Nízká**. Zásady klasifikace hrozeb v rámci služby Mobile Endpoint Security přímo řídí výpočet dodržování předpisů zařízením v Intune.  

## <a name="monitor-enrollment"></a>Monitorování registrace
Po dokončení instalace se zobrazí výzva k zadání služby Mobile Endpoint Security do služby Azure AD pro zařízení, která odpovídají zadaným skupinám pro registraci.  Informace o zaregistrovaných zařízeních najdete v části **zařízení** v konzole nástroje pro hledání.  
- Počáteční stav zařízení *čeká na vyřízení*.  
- Stav zařízení se aktualizuje po instalaci, otevření a aktivaci aplikace *Lookout for Work* v zařízení.

Podrobnosti o tom, jak získat aplikaci *Lookout for Work* nasazenou na zařízení, najdete v tématu [Přidání aplikací pro hledání práce s Intune](mtd-apps-ios-app-configuration-policy-add-assign.md).

## <a name="next-steps"></a>Další kroky

- [Nastavení vyhledávacích aplikací pro zaregistrovaná zařízení](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Nastavení aplikací pro hledání neregistrovaných zařízení](mtd-add-apps-unenrolled-devices.md)
