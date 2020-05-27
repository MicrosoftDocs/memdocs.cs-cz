---
title: Vytvořit zásady podmíněného přístupu pro Exchange
titleSuffix: Microsoft Intune
description: Nakonfigurujte podmíněný přístup pro místní Exchange a starší verze Exchange Online vyhrazené v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 530d6de8194a1ca74b72567c98c5d2afcb327170
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990313"
---
# <a name="configure-exchange-on-premises-access-for-intune"></a>Konfigurace přístupu k místnímu Exchangi pro Intune

V tomto článku se dozvíte, jak nakonfigurovat podmíněný přístup pro místní Exchange na základě dodržování předpisů zařízením.

Pokud máte vyhrazené prostředí Exchange Online a potřebujete zjistit, jestli má novou, nebo starší verzi konfigurace, obraťte se prosím na správce svého účtu. Pokud chcete řídit přístup k e-mailům v místním systému Exchange nebo ve starším vyhrazeném prostředí Exchange Online, nakonfigurujte podmíněný přístup na místní Exchange v Intune.

## <a name="before-you-begin"></a>Před zahájením

Než budete moct nakonfigurovat podmíněný přístup, ověřte, že existují následující konfigurace:

- Vaše verze Exchange je **exchange 2010 SP3 nebo novější**. Podporuje se pole serveru pro klientský přístup (CAS) serveru Exchange.

- Nainstalovali jste a používali místní [Exchange Connector pro Exchange ActiveSync](exchange-connector-install.md), který připojuje Intune k místnímu Exchangi.

    >[!IMPORTANT]  
    >Intune podporuje více místních Exchange Connectorů pro každé předplatné.  Každý místní Exchange Connector je ale specifický pro jednoho tenanta Intune a nedá se použít s žádným jiným klientem.  Pokud máte více než jednu místní organizaci Exchange, můžete pro každou organizaci Exchange nastavit samostatný konektor.

- Konektor pro místní organizaci Exchange můžete nainstalovat na libovolný počítač, pokud tento počítač může komunikovat se serverem Exchange.

- Tento konektor podporuje **prostředí Exchange CAS**. Intune podporuje instalaci konektoru na server Exchange CAS přímo. Doporučujeme ji nainstalovat do samostatného počítače z důvodu dalšího zatížení, které konektor vloží na server. Při konfiguraci musíte konektor nastavit tak, aby komunikoval s jedním ze serverů Exchange CAS.

- Protokol **Exchange ActiveSync** je potřeba nakonfigurovat s ověřováním na základě certifikátů nebo zadávání přihlašovacích údajů uživateli.

- Pokud jsou zásady podmíněného přístupu nakonfigurované a cílené na uživatele, musí být předtím, než se uživatel může připojit k e-mailu, použít následující **zařízení** :
  - Musí být **zaregistrovaný** ve službě Intune nebo se musí jednat o počítač připojený k doméně.
  - **Musí být zaregistrované v Azure Active Directory**. Kromě toho musí být ve službě Azure Active Directory zaregistrované ID protokolu Exchange ActiveSync klienta.

- Pro zákazníky s Intune a Office 365 se služba Azure AD Device Registration Service (DRS) aktivuje automaticky. Zákazníci, kteří už mají nasazenou službu AD FS Device Registration Service, nevidí registrovaná zařízení v místní službě Active Directory. **To neplatí pro počítače s Windows ani zařízení Windows Phone**.

- **Musí splňovat** zásady dodržování předpisů, které jsou nasazené na toto zařízení.

- Pokud zařízení nesplňuje nastavení podmíněného přístupu, zobrazí se uživateli při přihlášení jedna z následujících zpráv:
  - Pokud zařízení není zaregistrované v Intune nebo není zaregistrované v Azure Active Directory, zobrazí se zpráva s pokyny k instalaci Portál společnosti aplikace, registraci zařízení a aktivaci e-mailu. Tento proces také přidruží ID protokolu Exchange ActiveSync zařízení k záznamu zařízení v Azure Active Directory.
  - Pokud zařízení nedodržuje předpisy, zobrazí se zpráva, která uživatele přesměruje na web Portál společnosti Intune nebo Portál společnosti aplikaci. Z portálu společnosti můžou najít informace o problému a jeho řešení.

### <a name="support-for-mobile-devices"></a>Podpora mobilních zařízení

- **Windows Phone 8,1 a novější** – vytvoření zásady podmíněného přístupu najdete v tématu [Vytvoření zásad podmíněného přístupu](../protect/create-conditional-access-intune.md) .
- **Nativní e-mailová aplikace v systému iOS/iPadOS** – vytvoření zásady podmíněného přístupu najdete v tématu [Vytvoření zásad podmíněného přístupu](../protect/create-conditional-access-intune.md) .
- **Poštovní klienti EAS, například Gmail v Androidu 4 nebo novějším** – vytvoření zásady podmíněného přístupu, najdete v tématu [Vytvoření zásad podmíněného přístupu](../protect/create-conditional-access-intune.md) .

- **Poštovní klienti EAS na Správci zařízení s Androidem** : Pokud chcete vytvořit zásadu podmíněného přístupu, přečtěte si téma [Vytvoření zásad podmíněného přístupu](../protect/create-conditional-access-intune.md) .

- **Poštovní klienti EAS na zařízeních s pracovním profilem Android** – na zařízeních s Androidem Work profilování jsou podporovaná jenom *Gmail* a *devět práce pro Android Enterprise* . Aby mohl podmíněný přístup pracovat s pracovními profily Androidu, musíte nasadit e-mailový profil pro aplikaci *Gmail* nebo *devět Work pro Android Enterprise* a tyto aplikace nasadit jako požadovanou instalaci. Po nasazení aplikace můžete nastavit podmíněný přístup na základě zařízení.


#### <a name="to-set-up-conditional-access-for-android-work-profile-devices"></a>Nastavení podmíněného přístupu pro zařízení s pracovním profilem Androidu

  1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
  
  2. V případě **potřeby**Nasaďte aplikaci Gmail nebo devět Work.

  3. Vyberte **Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**, zadejte **název** a **Popis** profilu.

  4. Na **platformě**vyberte **Android Enterprise** a v **typ profilu**vyberte **e-mail** .

  5. Nakonfigurujte [Nastavení e-mailového profilu](https://docs.microsoft.com/intune/configuration/email-settings-android-enterprise#android-enterprise).

  6. Až budete hotovi, vyberte **OK**  >  **Create** a uložte změny.

  7. Po vytvoření e-mailového profilu [ho přiřaďte do skupin](https://docs.microsoft.com/intune/device-profile-assign).

  8. Nastavte [podmíněný přístup na základě zařízení](https://docs.microsoft.com/intune/protect/conditional-access-intune-common-ways-use#device-based-conditional-access).

> [!NOTE]
> Microsoft Outlook pro Android a iOS/iPadOS se nepodporuje prostřednictvím konektoru Exchange On-Premises Connector. Pokud chcete využít Azure Active Directory zásady podmíněného přístupu a zásady Intune App Protection s Outlookem pro iOS/iPadOS a Androidem pro vaše místní poštovní schránky, přečtěte si téma [použití hybridního moderního ověřování s Outlookem pro iOS/iPadOS a Android](https://docs.microsoft.com/Exchange/clients/outlook-for-ios-and-android/use-hybrid-modern-auth).

### <a name="support-for-pcs"></a>Podpora počítačů

Nativní **e-mailová** aplikace v Windows 8.1 a novějších verzích (při registraci do MDM pomocí Intune)

## <a name="configure-exchange-on-premises-access"></a>Konfigurace přístupu k místnímu Exchangi

Než budete moct pomocí následujícího postupu nastavit místní řízení přístupu Exchange, musíte pro místní Exchange nainstalovat a nakonfigurovat aspoň jeden místní [Exchange Connector pro Intune](exchange-connector-install.md) .

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Přejděte na přístup k Exchangi pro **správu tenanta**  >  **Exchange access**a pak vyberte **přístup k místnímu Exchangi**.

3. V podokně **přístup v místním systému Exchange** *Povolte řízení přístupu k místnímu systému Exchange*kliknutím na **Ano** .

   > [!div class="mx-imgBorder"]
   > ![Ukázkový snímek obrazovky s přístupem k místnímu systému Exchange](./media/conditional-access-exchange-create/exchange-on-premises-access.png)

4. V části **přiřazení**zvolte **Vybrat skupiny, které se mají zahrnout**, a potom vyberte jednu nebo víc skupin pro konfiguraci přístupu.

   Členové vybraných skupin mají zásady podmíněného přístupu pro přístup k místnímu systému Exchange, na které se vztahují. Uživatelé, kteří obdrží tuto zásadu, musí zaregistrovat svoje zařízení v Intune a splňovat profily dodržování předpisů předtím, než budou moct přistupovat k místnímu Exchangi.

   > [!div class="mx-imgBorder"]
   > ![Vyberte skupiny, které chcete zahrnout.](./media/conditional-access-exchange-create/select-groups.png)

5. Pokud chcete skupiny vyloučit, zvolte Vybrat skupiny, které se **mají vyloučit**, a potom vyberte jednu nebo víc skupin, které se nevztahují na požadavky na registraci zařízení a jestli mají být kompatibilní s profily dodržování předpisů, než budete mít přístup k místnímu Exchangi.

   Vyberte **Uložit** a uložte svou konfiguraci a vraťte se do podokna **přístup k Exchangi** .

6. Dále nakonfigurujte nastavení pro místní Exchange Connector služby Intune. V konzole vyberte v konzole **Správa tenanta**  >  **Exchange přístup** >  **na Exchange ActiveSync On-Premises Connector** a pak vyberte konektor pro organizaci Exchange, kterou chcete nakonfigurovat.

7. V případě **oznámení uživateli**vyberte možnost **Upravit** a otevřete pracovní postup **Upravit organizaci** , kde můžete upravit zprávu s *oznámením uživatele* .

   > [!div class="mx-imgBorder"]
   > ![Ukázka snímku pracovního postupu úpravy pracovní postup organizace pro oznámení](./media/conditional-access-exchange-create/edit-organization-user-notification.png)

   Upravte výchozí e-mailovou zprávu, která se pošle uživatelům, pokud jejich zařízení nedodržuje předpisy a chtějí získat přístup k místnímu Exchangi. Šablona zprávy používá jazyk využívající značky. Můžete si také prohlédnout náhled toho, jak zpráva vypadá při psaní.

   Vyberte **zkontrolovat + Uložit** **a uložte změny** a dokončete konfiguraci přístupu k místnímu Exchangi.

   > [!TIP]
   > Další informace o jazyku využívajícím značky najdete v [článku](https://en.wikipedia.org/wiki/Markup_language) na Wikipedii.

8. V dalším kroku vyberte **Upřesnit nastavení přístupu Exchange ActiveSync** a otevřete tak pracovní postup *Rozšířené nastavení přístupu Exchange ActiveSync* , ve kterém nakonfigurujete pravidla přístupu k zařízení.

   > [!div class="mx-imgBorder"]
   > ![Příklad obrazovky pracovní postup úpravy organizace pro pokročilá nastavení](./media/conditional-access-exchange-create/edit-organization-advanced-settings.png)

   - V případě **nespravovaného přístupu k zařízení**nastavte globální výchozí pravidlo pro přístup ze zařízení, která neovlivní podmíněný přístup nebo jiná pravidla:

     - **Povolení přístupu** – všechna zařízení můžou hned získat přístup k místnímu Exchangi. Zařízení, která patří uživatelům ve skupinách, které jste nakonfigurovali jako zahrnutá v předchozím postupu, se zablokují, pokud se později vyhodnotí jako nevyhovující předpisům nebo nejsou zaregistrovaná v Intune.

     - **Zablokovat přístup** a **umístit do karantény** – všechna zařízení hned zablokují přístup k místnímu Exchangi na začátku. Zařízení, která patří uživatelům ve skupinách, které jste nakonfigurovali tak, jak je uvedeno v předchozím postupu, získají přístup po registraci zařízení v Intune a vyhodnotí jako kompatibilní.

       Zařízení s Androidem *, která nepoužívají Samsung* Knox Standard, toto nastavení nepodporují a jsou vždycky zablokovaná.

   - V případě **výjimek platforem zařízení**vyberte **Přidat**a pak podle potřeby zadejte podrobnosti pro vaše prostředí.

      Pokud je nastavení **přístupu nespravovaného zařízení** nastavené na **blokované**, jsou zařízení, která jsou zaregistrovaná a kompatibilní, povolená i v případě, že je pro ně výjimka platformy zablokovaná.  

9. Výběrem **OK** uložte změny.

10. Vyberte **zkontrolovat + Uložit**a pak **Uložit** a uložte zásady podmíněného přístupu Exchange.

## <a name="next-steps"></a>Další kroky

V dalším kroku vytvoříte zásadu dodržování předpisů a přiřadíte ji uživatelům pro Intune, abyste mohli vyhodnotit jejich mobilní zařízení, přečtěte si téma Začínáme [s dodržováním předpisů zařízením](device-compliance-get-started.md).

[Řešení potíží s místním Exchange Connectorem Intune v Microsoft Intune](https://support.microsoft.com/help/4471887)
