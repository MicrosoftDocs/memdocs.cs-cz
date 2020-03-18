---
title: 'Rychlý start: Bezplatné vyzkoušení Microsoft Intune'
titleSuffix: ''
description: V tomto rychlém startu vytvoříte bezplatné zkušební předplatné, dozvíte se o podporovaných konfiguracích a síťových požadavcích a případně také můžete nakonfigurovat název vlastní domény.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83107121b05b2126e4c6b2b377baf57ee069f917
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326831"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>Rychlý start: Bezplatné vyzkoušení Microsoft Intune

Microsoft Intune slouží ke správě zařízení a aplikací, a pomáhá tak chránit firemní data vašich pracovníků. V tomto rychlém startu vytvoříte bezplatné předplatné, abyste si mohli vyzkoušet Intune v testovacím prostředí.

Intune poskytuje správu mobilních zařízení (MDM) a správu mobilních aplikací (MAM) ze zabezpečené cloudové služby spravované pomocí centra pro správu Microsoft Endpoint Manageru. S Intune máte jistotu, že máte firemní prostředky svých pracovníků (data, zařízení a aplikace) správně nakonfigurované, přístupné a aktualizované a že odpovídají firemním zásadám a požadavkům souvisejícím s dodržováním předpisů.

## <a name="prerequisites"></a>Požadavky
Než budete nastavovat Microsoft Intune, projděte si následující požadavky:

- [Podporované operační systémy a prohlížeče](supported-devices-browsers.md)
- [Požadavky týkající se konfigurace sítě a šířky pásma](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Registrace bezplatné zkušební verze Microsoft Intune

Intune si můžete zdarma vyzkoušet. Zkušební doba je 30 dní. Pokud už máte svůj pracovní nebo školní účet, **přihlaste se** s jeho použitím a přidejte Intune k svému předplatnému. V opačném případě si můžete **zaregistrovat** pro svoji organizaci nový účet Intune.

> [!IMPORTANT]
> Když si zaregistrujete nový účet, nebude možné s ním kombinovat stávající pracovní nebo školní účet.

1. Přejděte na stránku [zkušební verze Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2019088) a vyplňte formulář.

    ![Snímek obrazovky s webovou stránkou registrace účtu zkušební verze Microsoft Intune](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    Pokud většina pracovníků IT oddělení a uživatelů používá jiné národní prostředí než vy, můžete toto národní prostředí vybrat v části **Země nebo oblast**. Azure používá místní informace k poskytování správných služeb. Toto nastavení nemůžete později změnit.

2. Vytvořte si účet. Použijte k tomu název společnosti, za který přidáte **.onmicrosoft.com**. 

    ![Snímek obrazovky zkušebního účtu Intune – nový proces přihlašovacích údajů](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    Pokud má vaše organizace vlastní doménu, kterou chcete použít bez **. onmicrosoft.com**, můžete ji změnit v centru pro správu Microsoft 365 popsané dále v tomto článku.

3. Na konci registrace si můžete prohlédnout informace o novém účtu.

    ![Obrázek s informacemi o účtu](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Přihlášení k Intune ve službě Microsoft Endpoint Manager

Pokud ještě nejste přihlášení k portálu, proveďte následující kroky:

1. Otevřete nové okno prohlížeče a do adresního řádku zadejte **https://devicemanagement.microsoft.com** . 
2. Přihlaste se pomocí ID uživatele, které jste provedli v krocích uvedených výše ( *yourID@yourdomain* . onmicrosoft.com).

    ![Obrázek přihlašovací stránky portálu](./media/free-trial-sign-up/azure-portal-signin.png)

Když si zaregistrujete zkušební verzi, přijde vám e-mailová zpráva s informacemi o vašem účtu a e-mailovou adresou, kterou jste zadali při registraci. Ta potvrzuje, že je vaše zkušební verze aktivní.

> [!TIP]
> Při práci s Microsoft Endpoint Managerem můžete mít lepší výsledky pracovat s prohlížečem v normálním režimu, nikoli v privátním režimu.

## <a name="confirm-the-mdm-authority-in-intune"></a>Potvrzení autority MDM v Intune

Ve výchozím nastavení se Autorita MDM nastaví při vytváření bezplatné zkušební verze. Pomocí následujících kroků můžete potvrdit, že je Autorita MDM nastavená:

1. Pokud ještě nejste přihlášení, přihlaste se ke službě Microsoft Endpoint Manager.
2. Klikněte na **Správa tenanta**.
3. Zobrazit podrobnosti o tenantovi. **Autorita MDM** by měla být nastavená na **Microsoft Intune**.

Pokud se po přihlášení ke službě Microsoft Endpoint Manager zobrazí oranžová zpráva oznamující, že jste ještě nestavili autoritu MDM, můžete ji aktivovat v tuto chvíli. Nastavení autority pro správu mobilních zařízení (MDM) určuje způsob správy zařízení. Napřed je potřeba nastavit autoritu pro správu mobilních zařízení, aby si uživatelé mohli zaregistrovat do správy zařízení.

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>Pokud chcete nastavit autoritu MDM na Intune, postupujte podle těchto kroků:

1. Otevřete nové okno prohlížeče a do adresního řádku zadejte **https://portal.azure.com** . 
2. Zvolte **Všechny služby** > **Microsoft Intune**.
3. Vyberte informační zprávu, že nemáte aktivovanou správu zařízení. Pokud se nezobrazuje, vyberte **Registrace zařízení**. Pokud správa zařízení není aktivovaná, zobrazí se okno **Zvolte autoritu MDM**.

    > [!NOTE]
    > Pokud jste nastavili autoritu MDM, v okně **registrace zařízení** se zobrazí hodnota Autorita MDM. Oranžová informační zpráva se zobrazí jenom v případě, že jste autoritu MDM ještě nenastavili. 

    ![Obrázek okna Zvolte autoritu MDM](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. Pokud vaše Autorita MDM není nastavená, nastavte v části **zvolit autoritu MDM**autoritu MDM na **autoritu MDM pro Intune**.

Další informace o autoritě MDM najdete v článku [Nastavení autority pro správu mobilních zařízení](mdm-authority-set.md).

## <a name="configure-your-custom-domain-name-optional"></a>Konfigurace vlastního názvu domény (volitelné)

Jak je uvedeno výše, pokud má vaše organizace vlastní doménu, kterou chcete použít bez **. onmicrosoft.com**, můžete ji změnit v centru pro správu Microsoft 365. Pomocí následujících kroků můžete přidat, ověřit a nakonfigurovat vlastní název domény.  

> [!IMPORTANT]
> Nelze přejmenovat ani odebrat *úvodní* část názvu domény **onmicrosoft.com** . Můžete ale přidat, ověřit nebo odebrat *vlastní* názvy domén používané v Intune, abyste zachovali, že vaše obchodní identita bude jasná. Další informace najdete v tématu [Konfigurace vlastního názvu domény](custom-domain-name-configure.md).

1. Přejít na [Centrum pro správu Microsoft 365](https://admin.microsoft.com) a přihlaste se pomocí účtu správce.

2. V navigačním podokně zvolte **Nastavení** > **Domény** > **Přidat doménu**.

3. Zadejte název vlastní domény. Pak vyberte **Další**.

   ![Snímek obrazovky centra pro správu Microsoft 365 – přidat doménu](./media/free-trial-sign-up/domain-custom-add.png)

4. Ověřte, že jste vlastníkem domény, kterou jste zadali v předchozím kroku. 
    
    Pokud vyberete, že chcete **poslat kód e-mailem**, odešle se e-mail kontaktu, který je zaregistrovaný u domény. Jakmile dostanete e-mail, zkopírujte kód a zadejte ho do pole označeného **Sem napište ověřovací kód**. Pokud se ověřovací kód shoduje, přidá se doména do tenanta. Zobrazený e-mail vám nemusí být povědomý. Některé registrátory skrývají reálnou e-mailovou adresu. I tato e-mailová adresa může být odlišná, a to, co se zadalo při registraci domény.

   ![Snímek obrazovky centra pro správu Microsoft 365 – ověření domény](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > Podrobné informace o ověření záznamu TXT najdete v článku [Vytvoření záznamů DNS pro Office 365 u libovolného poskytovatele hostingu DNS](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166).

## <a name="admin-experiences"></a>Prostředí pro správu

K dispozici jsou dva portály, které budete používat nejčastěji:
- Centrum pro správu Microsoft Endpoint Manageru ([https://devicemanagement.microsoft.com/](https://devicemanagement.microsoft.com/)) je tam, kde můžete prozkoumat [Možnosti Intune](what-is-intune.md). V takovém případě bude správce spolupracovat s Intune.
- Pokud pro tuto možnost nepoužíváte Azure Active Directory, můžete přidat a spravovat uživatele v centru pro správu Microsoft 365 ([https://admin.microsoft.com](https://admin.microsoft.com)). Můžete také spravovat další oblasti svého účtu, včetně fakturace a podpory.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste vytvořili bezplatné předplatné, abyste si mohli vyzkoušet Intune v testovacím prostředí. Další informace o nastavení Intune najdete v článku [Nastavení Intune](setup-steps.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Vytvoření uživatele a přiřazení licence tomuto uživateli](quickstart-create-user.md)
