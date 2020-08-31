---
title: Požadavky na heslo pro zařízení zaregistrovaná v Intune | Microsoft Docs
description: Tento článek popisuje, jak splňovat požadavky na heslo vaší organizace, abyste měli přístup k síti.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057283"
---
# <a name="device-password-requirements"></a>Požadavky na heslo zařízení  

Pokud vaše heslo zařízení nesplňuje požadavky na zabezpečení vaší organizace, zobrazí se zpráva od Portál společnosti. Požadavky na heslo jsou zavedeny k ochraně dat vaší organizace před neoprávněným přístupem. Dokud nevytvoříte bezpečnější heslo, může být zablokován přístup k síti vaší organizace.  

Portál společnosti pošle jednu zprávu na požadavek na heslo, takže se může najednou zobrazit víc než jedna zpráva. Klepnutím na libovolnou zprávu zobrazíte další podrobnosti (pokud jsou k dispozici).  

V tomto článku jsou uvedené všechny zprávy týkající se hesla, které byste mohli získat, a další podrobnosti o jednotlivých požadavcích, které jsou na platformě operačního systému k dispozici.     

## <a name="change-password-passcode-pin"></a>Změnit heslo, heslo, PIN  

Obecně platí, že pokud chcete získat přístup k nastavení hesla, můžete na zařízení otevřít aplikaci nastavení a vyhledat *zamykací obrazovku* nebo *nastavení zabezpečení*.  

Následující články popisují, jak aktualizovat heslo zařízení podle platformy operačního systému. Pokud chcete získat nejaktuálnější pokyny pro konkrétní zařízení, přečtěte si dokumentaci od výrobce zařízení.  

- [Nastavení hesla zařízení s Windows 10](set-or-change-your-password-windows.md)  
- [Nastavení hesla pro zařízení s iOS](set-or-change-your-passcode-ios.md)  
- [Nastavení PIN kódu nebo hesla zařízení s Androidem](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Pokud jste změnili heslo tak, aby splňovalo požadavky, ale stále probíhá příjem oznámení, restartujte zařízení.  

Konkrétní otázky týkající se požadavků na heslo vaší organizace vám poskytne pracovník podpory IT.  

## <a name="windows-10-password-requirements"></a>Požadavky na heslo pro Windows 10

| Zpráva | Jak problém vyřešit |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Heslo je povinné. | Nastavte heslo. Vaše organizace vyžaduje, abyste zadali heslo k odemknutí zařízení. |
| Heslo je příliš jednoduché. |  Ujistěte se, že heslo neobsahuje sekvenční ani opakující se čísla, například 1234 nebo 1111. |
| Heslo je příliš krátké.| Aktualizujte nebo nastavte heslo o více znaků. Vaše organizace vyžaduje, aby vaše heslo bylo určitou délkou. To, co se ve skutečnosti zvolí, se liší, ale minimální délka, kterou může vyžadovat, je 4 znaky a maximální hodnota je 16. |
| Heslo může obsahovat pouze čísla. | Nastavte heslo, které obsahuje pouze čísla.|
| Heslo může obsahovat jenom alfanumerické znaky. | Nastavte heslo, které obsahuje kombinaci čísel a písmen.|
| Heslo musí obsahovat složité znaky. | Přidejte složité znaky, jako jsou čísla, Velká písmena a symboly jako `$` , `%` a `#` . Vaše organizace vyžaduje kombinaci písmen, číslic a jiných než alfanumerických znaků, aby ji ostatní mohli uhodnout a heslo.|  
| Platnost hesla vypršela. | Nastavte nové heslo. Vaše organizace vyžaduje, abyste po určitém počtu dnů změnili heslo. |
| Heslo bylo použito v nedávné době. | Vyberte heslo, které jste předtím nepoužili. Vaše organizace vyžaduje, abyste před opětovným použitím hesla prošli určitou dobu. |

## <a name="ios-passcode-requirements"></a>požadavky na přístupový kód pro iOS

| Zpráva | Jak problém vyřešit |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Heslo je povinné.| Nastavte heslo. Vaše organizace vyžaduje, abyste zadali heslo k odemknutí zařízení. |
| Heslo je příliš jednoduché. |  Ujistěte se, že heslo neobsahuje sekvenční ani opakující se čísla, například 1234 nebo 1111. |
| Heslo je příliš krátké. | Aktualizujte nebo nastavte heslo s více znaky. Vaše organizace vyžaduje, aby váš přístupový kód měl určitou délku. To, co se ve skutečnosti zvolí, se liší, ale minimální délka, kterou může vyžadovat, je 4 znaky a maximální hodnota je 14. Když změníte heslo, může se zobrazit výzva od společnosti Apple, která oznamuje, že chcete zadat 6 nebo více znaků. Tato zpráva je jenom doporučení systému Apple. Pokud vaše organizace vyžaduje jenom heslo, které má 4 nebo 5 znaků, nemusíte zadávat heslo s 6 číslicemi.|  
| Heslo musí obsahovat jenom číslice. | Nastavte heslo, které obsahuje pouze čísla.|
| Heslo může obsahovat jenom alfanumerické znaky.| Nastavte heslo, které obsahuje kombinaci čísel a písmen.|
| Heslo musí obsahovat jiné než alfanumerické znaky. | Přidejte speciální znaky, jako například `&` , `!` , `$` , `%` a `#` . Vaše organizace vyžaduje kombinaci písmen, číslic a jiných než alfanumerických znaků, aby ji ostatní mohli uhodnout a heslo.|
| Platnost hesla vypršela. | Nastavte nové heslo. Vaše organizace vyžaduje, abyste po určitém počtu dnů změnili heslo. |
| Vaše heslo bylo použito příliš nedávno.| Vyberte si heslo, které jste předtím nepoužili. Vaše organizace vyžaduje, abyste před opětovným použitím hesla prošli určitou dobu. |
|Vyžaduje se ověření dotykového ID nebo ID obličeje. | Nastavte Touch ID nebo ID obličeje. Vaše organizace vyžaduje, abyste před použitím automatického vyplňování hesel nebo informací o kreditních kartách ověřili jednu z těchto metod. | 

## <a name="macos-password-requirements"></a>macOS požadavky na heslo
| Zpráva | Jak problém vyřešit |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Heslo je povinné. | Nastavte heslo. Vaše organizace vyžaduje, abyste zadali heslo k odemknutí zařízení. |
| Heslo je příliš jednoduché.|  Ujistěte se, že heslo neobsahuje sekvenční ani opakující se čísla, například 1234 nebo 1111. |
| Heslo je příliš krátké. | Aktualizujte nebo nastavte heslo o více znaků. Vaše organizace vyžaduje, aby vaše heslo bylo určitou délkou.|
| Heslo může obsahovat pouze čísla. | Nastavte heslo, které obsahuje pouze čísla.|
| Heslo může obsahovat jenom alfanumerické znaky. | Nastavte heslo, které obsahuje kombinaci čísel a písmen.|
| Heslo musí obsahovat jiné než alfanumerické znaky. | Přidejte speciální znaky, jako například `&` , `!` , `$` , `%` a `#` . Vaše organizace vyžaduje kombinaci písmen, číslic a jiných než alfanumerických znaků, aby ji ostatní mohli uhodnout a heslo.|
| Platnost hesla vypršela. | Nastavte nové heslo. Vaše organizace vyžaduje, abyste po určitém počtu dnů změnili heslo. |
| Heslo bylo použito v nedávné době. | Vyberte heslo, které jste předtím nepoužili. Vaše organizace vyžaduje, abyste před opětovným použitím hesla prošli určitou dobu. |

## <a name="android-password-requirements"></a>Požadavky na heslo pro Android
| Zpráva | Jak problém vyřešit |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Heslo je povinné. | Nastavte heslo nebo PIN kód. Vaše organizace vyžaduje, abyste zadali heslo k odemknutí zařízení. |
| Heslo je příliš jednoduché. |  Ujistěte se, že vaše heslo nebo PIN kód neobsahuje pořadové ani opakující se číslo, například 1234 nebo 1111. |
| Heslo je příliš krátké. | Aktualizujte nebo nastavte heslo o více znaků. Vaše organizace vyžaduje, aby vaše heslo bylo určitou délkou.|
| Heslo musí obsahovat čísla. | Nastavte heslo nebo PIN kód, který obsahuje čísla.|
| Heslo musí obsahovat písmena. | Nastavte heslo obsahující písmena z abecedy.|
| Heslo musí obsahovat alfanumerické znaky. | Nastavte heslo, které obsahuje kombinaci čísel a písmen.|
| Heslo musí obsahovat alfanumerické znaky a symboly. | Nastavte heslo, které obsahuje kombinaci písmen, číslic a speciálních znaků, například `&` , `!` ,, `$` `%` a `#` . |
| Heslo musí používat biometrickou technologii.| Nastavte si zařízení pro použití biometrického ověřování, jako je otisk prstu nebo rozpoznávání obličeje.
| Platnost hesla vypršela. | Nastavte nové heslo. Vaše organizace vyžaduje, abyste po určitém počtu dnů změnili heslo. |
| Heslo bylo použito v nedávné době. | Vyberte heslo, které jste předtím nepoužili. Vaše organizace vyžaduje, abyste před opětovným použitím hesla prošli určitou dobu. |

## <a name="next-steps"></a>Další kroky
Pokud jste si aktualizovali heslo a pořád budete dostávat zprávy týkající se hesla, zkuste zařízení restartovat. 

Potřebujete ještě další pomoc? Obraťte se na pracovníky podpory IT. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  


