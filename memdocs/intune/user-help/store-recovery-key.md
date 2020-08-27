---
title: Uložení obnovovacího klíče do Intune prostřednictvím webu Portál společnosti
description: Nahrajte a uložte obnovovací klíč zařízení z Portál společnosti webu.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910787"
---
# <a name="store-your-personal-filevault-key"></a>Uložte si svůj osobní klíč trezoru. 

Uložte si klíč trezoru pro vaše osobní zařízení macOS. Kromě splnění požadavků na šifrování ukládá váš klíč do Intune tyto akce: 

* Klíč můžete snadno a rychle načíst nebo otočit z libovolného zařízení. 
* Pokud potřebujete načíst nebo otočit klíč a nemůžete získat přístup k aplikacím nebo webům, požádejte o pomoc pracovníka podpory.


## <a name="retrieve-or-rotate-the-key"></a>Načíst nebo otočit klíč

Pokud se z vašeho zařízení zamknete, můžete si klíč načíst z těchto umístění:
   
- Web portálu společnosti
- Aplikace Portál společnosti pro iOS/iPadOS 
- Aplikace Portál společnosti pro Android
- Aplikace Intune
 
 Oddělení IT, kteří mají přístup správce k Intune, může váš osobní obnovovací klíč otočit za vás, pokud se z vašeho zařízení zamknete. Můžou také zobrazovat klíče, ale jenom ty, které patří do zařízení vlastněných společností. Podpora pro ostatní uživatele nemůže zobrazit klíče pro obnovení, které patří do osobních zařízení.   


## <a name="do-i-need-to-store-my-key"></a>Potřebuji uložit svůj klíč?  
Pracovník podpory IT vám pošle informace o tom, jestli je potřeba nahrát osobní obnovovací klíč. Pokud to záleží na tom, jak IT oddělení vaší organizace obvykle komunikuje s vámi, může obdržet oznámení od aplikací Portál společnosti pro iOS/iPadOS nebo Android. 

Klíč pro obnovení doporučujeme nahrát jenom v případě, že spadají do jedné z následujících kategorií:
* Před registrací zařízení ve vaší organizaci jste zašifroval. 
* Zařízení jste sami zašifrovali přes Předvolby systému macOS.   

V závislosti na zásadách vaší organizace může být blokován přístup k firemním prostředkům na vašem zařízení, dokud neodešlete svůj klíč.  

## <a name="upload-personal-recovery-key"></a>Nahrát osobní obnovovací klíč 
Provedením těchto kroků uložte klíč úložiště osobních úložišť pro šifrované zařízení Mac.  


1. Navštivte [web portál společnosti](https://portal.manage.microsoft.com) a přihlaste se pomocí svého školního nebo pracovního účtu. 
2. Vyberte šifrované zařízení.
3. Vyberte **obnovovací klíč úložiště**.  
4. Zadejte svůj 24 znaků alfanumerický klíč trezoru.  
5. Zadejte klíč znovu. Pak vyberte **Uložit**.
6. Portál společnosti se pokusí ověřit, otočit a uložit váš osobní obnovovací klíč. Po uložení klíče není nutná žádná další akce. Pokud necháte web před dokončením nahrávání, můžete zobrazit jeho stav na stránce Podrobnosti o zařízení při příštím přihlášení.  

Další informace o zprávách, které se mohou zobrazit během tohoto procesu, naleznete v tématu [portál společnosti Messages](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Zprávy na Portálu společnosti

|Zpráva  |Význam  |
|---------|---------|
|Klíče se musí shodovat. Ověřte klíče a zkuste to znovu.     | V poli **Potvrdit obnovovací klíč** se zobrazí informace o tom, že se klíče vzájemně neshodují. Znovu zadejte klíče do obou polí a pak zkuste operaci uložit znovu.        |
|Nepovedlo se aktualizovat obnovovací klíč pro zařízení.| Zobrazí se jako informační zpráva v horní části obrazovky, která vám umožní zjistit, že Portál společnosti nemohl uložit obnovovací klíč. Další podrobnosti získáte, když vyberete šifrované zařízení. Pak si přečtěte zprávu v horní části stránky pro další kroky. |
|Nepovedlo se nám nahrát váš obnovovací klíč. Ověřte, zda jste zadali správný klíč, a akci opakujte. Pokud se problém opakuje, zkuste klíč ručně otočit. Klepnutím zobrazíte další informace.     | Zobrazí se na stránce s podrobnostmi o zařízení a může to znamenat několik věcí: první, Portál společnosti nešlo otočit a uložit klíč, protože zadaný klíč není správný. Ověřte, že máte správný klíč, a zkuste to znovu. Druhou možností je, že vaše zařízení se během chvilky nevrátilo do vaší organizace. Pokud chcete synchronizovat nejnovější aktualizace z vaší organizace, vyberte zařízení > **Status**  >  **přístup k kontrole**stavu. Pak zkuste znovu uložit obnovovací klíč. Nakonec, pokud potíže potrvají, může to znamenat, že vaše organizace na jejich straně nepovolila trezor. Obraťte se na pracovníky podpory IT a dejte jim jistotu, že vaše zařízení synchronizujete, ale stále nemůžete uložit svůj klíč trezoru.         |
|Obnovovací klíč byl aktualizován. Pokud se někdy zamknete ze zařízení a potřebujete načíst svůj klíč, přihlaste se k Portál společnosti a vyberte **získat obnovovací klíč**.    | Zobrazí se na stránce s podrobnostmi o zařízení. Klíč, který jste uložili, byl úspěšně otočen a je uložen nový osobní obnovovací klíč.    |



## <a name="it-pro-support"></a>Podpora IT pro

Pokud jste pracovníkem podpory IT a chcete nakonfigurovat a spravovat šifrování trezoru pro zařízení Mac ve vaší organizaci, přečtěte si téma [použití šifrování disku trezoru úložiště pro MacOS s Intune](../protect/encrypt-devices-filevault.md).  

## <a name="next-steps"></a>Další kroky

Klíč můžete kdykoli získat z Portál společnosti webu, aplikace Intune a Portál společnosti aplikací pro iOS a Android a použít ho pro přístup k zařízení Mac. Informace o načtení obnovovacího klíče najdete v tématu [získání obnovovacího klíče](get-recovery-key-cpweb.md).

Zjistěte, co dalšího můžete dělat na webu Portál společnosti. Seznam akcí najdete v tématu věnovaném [použití portál společnosti Intune webu](using-the-intune-company-portal-website.md) .  

Potřebujete ještě další pomoc? Obraťte se na pracovníky podpory IT. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).