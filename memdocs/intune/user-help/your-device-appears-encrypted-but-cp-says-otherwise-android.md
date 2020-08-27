---
title: Vaše zařízení Android je zřejmě zašifrované | Microsoft Docs
description: Vyřešit stav šifrování v aplikaci Portál společnosti a Microsoft Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a6984f4e6eafee1f81340f483dc557fdb6091ec9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910753"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Šifrované zařízení, ale aplikace říkají jinak

Pokud Portál společnosti nebo aplikace Microsoft Intune říká, že vaše zařízení není šifrované, ale jste si jisti, že je to, zkuste postup v tomto článku.  

## <a name="add-a-startup-pin"></a>Přidání spouštěcího kódu PIN

Určitá zařízení s Androidem budou vyžadovat vytvoření spouštěcího PIN kódu, který zaručí, že je zařízení zabezpečené. Umístění tohoto nastavení bude v aplikaci **Nastavení** vašeho zařízení. Název a umístění nastavení se může lišit. Například na S7 Samsung Galaxy se toto nastavení označuje jako **zabezpečené spuštění**. Pokud ho chcete povolit a vytvořit heslo, přejdete na **Nastavení**  >  **zamykací obrazovka a zabezpečení**  >  **zabezpečené po spuštění**.  

## <a name="encrypt-the-entire-device"></a>Zašifrujte celé zařízení.

Tato část se týká pouze aplikace Portál společnosti. Některá zařízení vám dají na výběr, jestli chcete zašifrovat celé zařízení, nebo jenom využité místo. Vyberte možnost šifrování celého zařízení. Pokud jste vybrali možnost šifrování jenom využitého místa:

1. [Odebrat toto zařízení z portál společnosti](unenroll-your-device-from-intune-android.md).
2. Dešifrujte využité místo.  
3. Zašifruje celé zařízení.  
4. Zařízení znovu zaregistrujte.  

## <a name="downgrade-your-version-of-android"></a>Přechod na starší verzi Androidu

Tato část se týká pouze aplikace Portál společnosti. Pokud vaše zařízení nabízí možnost downgradu na Android 6,0 a novější, pak to udělejte. Pokud se pokusíte snížit množství zařízení, dojde ke ztrátě dat. Jinak doporučujeme, abyste se kvůli řešení tohoto problému obrátili na svou firemní podporu. Získejte kontaktní informace na firemní podporu na [webu portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Problémy konkrétních výrobců

Některá zařízení s Androidem verze 7,0 a novější šifrují data způsoby, které nejsou konzistentní s určitými standardy platformy Android. Tyto metody šifrování převedou informace o zařízení v nebezpečí. V důsledku toho tato zařízení nejsou podporována.

Nevyčerpávající seznam podporovaných zařízení s Androidem najdete v článku [podporované operační systémy a prohlížeče v Intune](/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Pokud zařízení není v seznamu uvedeno, obraťte se na výrobce zařízení nebo se obraťte na pracovníky podpory.

> [!Note]
> Microsoft spolupracuje s výrobci, aby vyřešil případné problémy, které při testování vyhledáme, nebo jestli si uživatelé nahlásí. Tento článek aktualizujeme vždy, když jsou k dispozici nové informace.

## <a name="update-devices"></a>Aktualizace zařízení

Pokud jste zařízení neaktualizovali na nejnovější verzi Androidu, přejdete do aplikace **Nastavení** vašeho zařízení a vyberte **aktualizovat**.  

## <a name="next-steps"></a>Další kroky

Potřebujete ještě další pomoc? Obraťte se na firemní podporu (kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980)) nebo napište <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">týmu Microsoft Android</a>.