---
title: Integrace Windows Hello pro firmy s Microsoft Intune
titleSuffix: Microsoft Intune
description: Naučte se vytvářet zásady pro řízení použití Windows Hello pro firmy na spravovaných zařízeních během registrace zařízení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 64a76911725e5d596a80ecc67e42f088666017de
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531889"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integrace Windows Hello pro firmy s Microsoft Intune  

V rámci registrace zařízení můžete integrovat Windows Hello pro firmy (dříve Microsoft Passport for Work) s Microsoft Intune.

Hello pro firmy je alternativní metoda pro přihlašování pomocí účtu služby Active Directory nebo Azure Active Directory, která může nahradit hesla, čipové karty a virtuální čipové karty. Umožňuje používat k přihlášení místo hesla *gesto uživatele*. Gesto uživatele může být PIN, biometrické ověřování, jako je Windows Hello nebo externí zařízení, jako je třeba čtečka otisků prstů.

Intune se s Hello pro firmy integruje dvěma způsoby:

- **Celé tenanta**: zásady Intune se dají vytvořit v části *registrace zařízení*. Tato zásada cílí na celou organizaci (celého tenanta). Podporuje program Windows AutoPilot spouštěný při prvním zapnutí a použije se při registraci zařízení.
- **Diskrétní skupiny**: můžete nasadit zásady, které spravují Windows Hello pro firmy na zařízení, která jsou zaregistrovaná v Intune. Typy zásad, které mohou spravovat Windows Hello, zahrnují profily *ochrany identit* , které vytvoříte v části *Konfigurace zařízení*, různé *standardní hodnoty zabezpečení*a profily *ochrany účtů* služby Endpoint Security. Tyto typy profilů cílí na přiřazené uživatele nebo zařízení a použijí se při vrácení se změnami.

Pomocí tohoto článku můžete vytvořit výchozí zásadu pro službu Windows Hello pro firmy, která bude cílit na celou organizaci. Pokyny k vytváření profilů ochrany identit, které se použití u vybraných skupin uživatelů nebo zařízení, najdete v článku o [konfiguraci profilu ochrany identit](identity-protection-configure.md).  

> [!IMPORTANT]
> V desktopových a mobilních verzích Windows 10 před Anniversary Update šlo nastavit dva různé kódy PIN, které se daly použít k ověření prostředků:
> - **PIN zařízení** se používal k odemknutí zařízení a připojení k prostředkům cloudu.
> - **Pracovní PIN kód** se použil pro přístup k prostředkům Azure AD na osobních zařízeních uživatelů (BYOD).
> 
> Anniversary Update sloučil tyhle dva kódy do jediného PIN zařízení.
> Veškeré zásady konfigurace Intune, které mají nastaveno, že ovládají PIN zařízení, a také jakékoli nakonfigurované zásady Windows Hello pro firmy teď nastavují hodnotu tohoto nového kódu PIN.
> Pokud jste u obou typů zásad nastavili, že ovládají kód PIN, použijí se v zařízeních s desktopovými i mobilními verzemi Windows 10 zásady Windows Hello pro firmy.
> Abyste předešli konfliktům mezi zásadami a zajistili, že zásady kódu PIN se budou aplikovat správně, aktualizujte zásady Windows Hello pro firmy, tak aby odpovídaly nastavení zásad konfigurace. Potom požádejte uživatele, aby si svá zařízení synchronizovali v aplikaci Portál společnosti.



## <a name="create-a-windows-hello-for-business-policy"></a>Vytvoření zásad pro službu Windows Hello pro firmy

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Přejít na **zařízení**  >   **registrace registrace**  >  **zařízení**  >  **Windows registrace**  >  **Windows Hello pro firmy**. Otevře se podokno Windows Hello pro firmy.

3. Pro **konfiguraci Windows Hello pro firmy**vyberte z těchto možností:

     - **Povoleno**. Toto nastavení vyberte, pokud chcete konfigurovat nastavení Windows Hello pro firmy.  Když vyberete *povoleno*, další nastavení pro Windows Hello jsou viditelná a můžou být nakonfigurovaná pro zařízení.

    - **Zakázáno**. Pokud nechcete povolit Windows Hello pro firmy během registrace zařízení, vyberte tuto možnost. Když je tato možnost zakázaná, uživatelé nemůžou zřídit Windows Hello pro firmy s výjimkou Azure Active Directory připojených mobilních telefonů, kde se může zřizování vyžadovat. Když se nastaví jako *zakázané*, můžete nakonfigurovat další nastavení pro Windows Hello pro firmy, i když tato zásada nepovolí Windows Hello pro firmy.

    - **Není nakonfigurováno**. Toto nastavení vyberte, pokud k řízení nastavení Windows Hello pro firmy nechcete používat Intune. Všechna existující nastavení Windows Hello pro firmy v zařízeních s Windows 10 se nezmění. Žádná ostatní nastavení v podokně nejsou dostupná.

4. Pokud jste v předchozím kroku vybrali **Povoleno**, nakonfigurujte požadovaná nastavení, která se použijí pro všechna zaregistrovaná zařízení s Windows 10 a Windows 10 Mobile. Po konfiguraci těchto nastavení vyberte **Uložit**.

   - **Použít čip TPM (Trusted Platform Module)**:

     Čip TPM poskytuje další úroveň zabezpečení dat. Vyberte jednu z těchto hodnot:

     - **Požadované** (výchozí). Windows Hello pro firmy můžou zřídit jenom zařízení s přístupným čipem TPM.
     - **Preferované**. Zařízení se nejdřív pokusí použít čip TPM. Pokud tato možnost není k dispozici, můžou použít softwarové šifrování.

   - **Minimální délka kódu PIN** a **Maximální délka kódu PIN**:

     Konfiguruje zařízení, aby k zajištění bezpečného přihlášení vyžadovala minimální a maximální délky kódu PIN. Výchozí délka kódu PIN je 6 znaků, ale můžete vynutit minimální délku 4 znaky. Maximální délka kódu PIN je 127 znaků.

   - **Malá písmena v PIN kódu**, **velká písmena v PIN kódu**a **speciální znaky v PIN kódu**.

     Silnější kódy PIN můžete vynutit tím, že se v nich bude vyžadovat použití velkých a malých písmen a speciálních znaků. U každého vyberte možnost z:

     - **Povoleno**. Uživatelé můžou ve svém PIN kódu použít typ znaku, ale není to povinné.

     - **Požadováno**. Uživatelé musí ve svém kódu PIN použít aspoň jeden z těchto typů znaků. Běžnou praxí třeba je vyžadovat použití nejméně jednoho velkého písmena, jednoho malého písmena a jednoho speciálního znaku.

     - **Není povolené** (výchozí). Uživatelé nesmí tyto typy znaků ve svém kódu PIN používat. (To je také chování, pokud nastavení není nakonfigurováno.)

       Mezi speciální znaky patří: **! "# $% &amp; ' () &#42; +,-. / : ; &lt; = &gt; ? @ [\] ^ _ &#96; {&#124;} ~**

   - **Doba platnosti kódu PIN (dny)**:

     Je dobrým zvykem zadat pro kód PIN dobu platnosti, po jejímž uplynutí ho uživatel musí změnit. Výchozí hodnota je 41 dnů.

   - **Pamatovat si historii kódů PIN**:

     Pomocí tohoto nastavení můžete zabránit opakovanému použití předchozích kódů PIN. Ve výchozím nastavení se nedají znovu použít posledních 5 kódů PIN.

   - **Povolení biometrického ověřování**:

     Jako alternativu ke kódu PIN pro Windows Hello pro firmy umožňuje biometrické ověřování, například rozpoznávání obličeje nebo otisků prstů. Uživatelé ale stejně musí nakonfigurovat pracovní PIN kód pro případ, že se biometrické ověření nepovede. Vybírejte z těchto možností:

     - **Ano**. Windows Hello pro firmy umožňuje biometrické ověřování.
     - **Ne**. Windows Hello pro firmy neumožňuje biometrické ověřování (pro všechny typy účtů).

   - **Používat rozšířenou ochranu proti falšování identity, pokud je dostupná**:

     Nakonfiguruje, jestli se v zařízeních, které ji podporují, používají funkce ochrany proti falšování identity Windows Hello. Například detekce fotografie obličeje místo reálné plochy.

     Pokud je tato hodnota nastavená na **Ano**, Windows vyžaduje, aby všichni uživatelé používali pro funkce obličeje ochranu proti falšování identity, pokud je tato podpora podporovaná.

   - **Povolení přihlášení telefonem**:

     Pokud je tato možnost nastavená na hodnotu **Ano**, uživatelé můžou použít vzdálenou službu Passport, která bude sloužit jako přenosné doprovodné zařízení pro ověřování stolního počítače. Stolní počítač musí být připojený ke službě Azure Active Directory a v doprovodném zařízení musí být nakonfigurovaný PIN kód pro Windows Hello pro firmy.

## <a name="windows-holographic-for-business-support"></a>Podpora Windows Holographic for Business

Windows Holografick pro firmy podporuje následující nastavení pro Windows Hello pro firmy:

- Použít čip TPM (Trusted Platform Module)
- Minimální délka PIN kódu
- Maximální délka PIN kódu
- Malá písmena v PIN kódu
- Velká písmena v PIN kódu
- Speciální znaky v PIN kódu
- Vypršení platnosti PIN kódu (v dnech)
- Pamatovat si historii PIN kódů

## <a name="next-steps"></a>Další kroky

Další informace o Windows Hello pro firmy najdete v [příručce](https://technet.microsoft.com/library/mt589441.aspx) v dokumentaci k Windows 10.
