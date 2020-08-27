---
title: Nastavení Windows Hello pro firmy v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení PIN, biometriky a ochrany proti falšování obsahu v profilu ochrany identity, abyste mohli používat a konfigurovat Windows Hello pro firmy na zařízeních s Windows 10 v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: ce4795dd060d29b62887fbf5496b2f2706ba954f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909104"
---
# <a name="windows-10-device-settings-to-enable-windows-hello-for-business-in-intune"></a>Nastavení zařízení s Windows 10 pro povolení Windows Hello pro firmy v Intune

Tento článek obsahuje seznam a popis nastavení Windows Hello pro firmy, která můžete řídit na zařízeních s Windows 10 v Intune. Jako správce služby Intune můžete nakonfigurovat a přiřadit tato nastavení zařízením s Windows 10 jako součást řešení správy mobilních zařízení (MDM). 

Další informace o těchto nastaveních najdete v části [Konfigurace nastavení zásad Windows Hello pro firmy](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings)v dokumentaci k Windows Hello.


Další informace o profilech Windows Hello pro firmy v Intune najdete v tématu [Konfigurace identity Protection](identity-protection-configure.md).

## <a name="before-you-begin"></a>Než začnete

[Vytvořte konfigurační profil](identity-protection-configure.md#create-the-device-profile).

## <a name="windows-hello-for-business"></a>Windows Hello pro firmy
- **Konfigurace Windows Hello pro firmy**:
  - **Nenakonfigurováno** – toto nastavení vyberte, pokud nechcete použít Intune k řízení nastavení Windows Hello pro firmy. Veškerá stávající nastavení Windows Hello pro firmy v zařízeních s Windows 10 se nezmění. Žádná ostatní nastavení v podokně nejsou dostupná.

  - **Zakázáno** – Pokud nechcete používat Windows Hello pro firmy, vyberte toto nastavení. Všechna ostatní nastavení na obrazovce jsou nedostupná.
  - **Povoleno** – toto nastavení vyberte, pokud chcete nakonfigurovat nastavení Windows Hello pro firmy.  
  
  **Výchozí**: Nenakonfigurováno

  Pokud je nastaveno na *povoleno*, jsou k dispozici následující nastavení:

  - **Minimální délka PIN kódu**  
    Zadejte minimální délku PIN kódu pro zařízení, aby se usnadnilo zabezpečení přihlášení. Výchozí hodnoty zařízení s Windows jsou šest znaků, ale toto nastavení může vyhovět minimálně čtyř až 127 znaků. 

    **Výchozí**: *Nenakonfigurováno*

  - **Maximální délka PIN kódu**  
  Zadejte maximální délku PIN kódu pro zařízení, aby se usnadnilo zabezpečení přihlášení. Výchozí hodnoty zařízení s Windows jsou šest znaků, ale toto nastavení může vyhovět minimálně čtyř až 127 znaků.  

    **Výchozí**: *Nenakonfigurováno*  

  - **Malá písmena v PIN kódu**  
    Silnější kód PIN můžete vynutíte tak, že koncoví uživatelé budou obsahovat malá písmena. Možnosti:

    - **Nepovoleno** – zablokuje uživatelům používání malých písmen v PIN kódu. K tomuto chování dochází také v případě, že nastavení není nakonfigurováno.
    - **Povoleno** – povolit uživatelům používat malá písmena v PIN kódu, ale není to povinné.
    - **Požadováno** – uživatelé musí v PIN kódu použít aspoň jedno malé písmeno. Běžnou praxí třeba je vyžadovat použití nejméně jednoho velkého písmena, jednoho malého písmena a jednoho speciálního znaku.

  - **Velká písmena v PIN kódu**  
    Můžete vynutí silnější PIN kód tím, že koncovým uživatelům zadáte velká písmena. Možnosti:

    - **Nepovoleno** – zablokuje uživatelům používání velkých písmen v PIN kódu. K tomuto chování dochází také v případě, že nastavení není nakonfigurováno.
    - **Povoleno** – povolí uživatelům používat v PIN kódu velká písmena, ale není to povinné.
    - **Požadováno** – uživatelé musí v PIN kódu použít aspoň jedno velké písmeno. Běžnou praxí třeba je vyžadovat použití nejméně jednoho velkého písmena, jednoho malého písmena a jednoho speciálního znaku.

  - **Speciální znaky v PIN kódu**  
    Silnější kód PIN můžete vynutíte tak, že koncoví uživatelé budou obsahovat speciální znaky. Mezi speciální znaky patří: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    Možnosti:
    - **Nepovoleno** – zablokuje uživatelům používání speciálních znaků v PIN kódu. K tomuto chování dochází také v případě, že nastavení není nakonfigurováno.
    - **Povoleno** – povolí uživatelům používat v PIN kódu velká písmena, ale není to povinné.
    - **Požadováno** – uživatelé musí v PIN kódu použít aspoň jedno velké písmeno. Běžnou praxí třeba je vyžadovat použití nejméně jednoho velkého písmena, jednoho malého písmena a jednoho speciálního znaku.

    **Výchozí**: nepovolené

  - **Vypršení platnosti PIN kódu (dny)**  
    Je dobrým zvykem zadat pro kód PIN dobu platnosti, po jejímž uplynutí ho uživatel musí změnit. Výchozí hodnoty pro zařízení s Windows jsou 41 dnů.

    **Výchozí**: Nenakonfigurováno

  - **Pamatovat si historii kódů PIN**  
    Pomocí tohoto nastavení můžete zabránit opakovanému použití předchozích kódů PIN. Zařízení s Windows se standardně zabraňují opakovanému použití posledních pěti kódů PIN.  

    **Výchozí**: Nenakonfigurováno  

  - **Povolit obnovení PIN kódu**   
    Umožňuje uživateli používat službu obnovení PIN kódu pro Windows Hello pro firmy. 
    
    - **Povoleno** – tajný klíč pro obnovení PIN kódu je uložený na zařízení a uživatel může v případě potřeby změnit PIN kód.  
    - **Zakázáno** – tajný klíč pro obnovení není vytvořený nebo uložený.

    **Výchozí**: Nenakonfigurováno

  - **Použít čip TPM (Trusted Platform Module)**   
    Čip TPM poskytuje další úroveň zabezpečení dat.  

    - **Pro Windows** Hello pro firmy můžou zřídit jenom zařízení s PŘÍSTUPNÝM čipem TPM.
    - **Nenakonfigurováno** – zařízení se nejdřív pokusí použít čip TPM. Pokud není dostupný, můžou použít softwarové šifrování.
    
    **Výchozí**: Nenakonfigurováno

  - **Povolení biometrického ověřování**  
     Jako alternativu ke kódu PIN pro Windows Hello pro firmy umožňuje biometrické ověřování, například rozpoznávání obličeje nebo otisků prstů. Uživatelé ale stejně musí nakonfigurovat pracovní PIN kód pro případ, že se biometrické ověření nepovede. Vybírejte z těchto možností:

    - **Povolit** – Windows Hello pro firmy umožňuje biometrické ověřování.
    - **Nenakonfigurováno** – Windows Hello pro firmy neumožňuje biometrické ověřování (pro všechny typy účtů).

    **Výchozí**: Nenakonfigurováno

  - **Použít vylepšenou ochranu proti falšování identity, pokud je dostupná**  
    Konfiguruje, jestli se v zařízení použijí funkce ochrany proti falšování identity Windows Hello, pokud je zařízení podporuje (třeba rozpoznání fotografie tváře místo skutečné tváře).  
    - **Povolit** – Windows vyžaduje, aby všichni uživatelé používali pro funkce obličeje ochranu proti falšování identity, pokud je tato možnost podporovaná.
    - **Nenakonfigurováno** – Windows respektuje konfigurace ochrany proti falšování identity na zařízení.

    **Výchozí**: Nenakonfigurováno

  - **Certifikát pro místní prostředky**  

    - **Povolit** – umožní Windows Hello pro firmy používat certifikáty k ověřování pro místní prostředky.
    - **Nenakonfigurováno** – zabrání Windows Hello pro firmy v používání certifikátů k ověřování pro místní prostředky. Místo toho zařízení používají výchozí chování *místního ověřování důvěryhodného klíče*. Další informace najdete v tématu [uživatelský certifikát pro místní ověřování](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) v dokumentaci k Windows Hello.  

  **Výchozí**: Nenakonfigurováno

- **Použití bezpečnostních klíčů pro přihlášení**  
  Toto nastavení je k dispozici pro zařízení s Windows 10 verze 1903 nebo novější. Pomocí této služby můžete spravovat podporu pro použití klíčů zabezpečení Windows Hello pro přihlášení.  

  - **Povoleno** – uživatelé můžou použít bezpečnostní klíč Windows Hello jako přihlašovací údaje pro počítače, na které cílí tato zásada. 
  - **Zakázáno** – klíče zabezpečení jsou zakázané a uživatelé je nemůžou používat k přihlašování k počítačům.   

  **Výchozí**: Nenakonfigurováno

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](../configuration/device-profile-assign.md) a [monitorujte jeho stav](../configuration/device-profile-monitor.md).