---
title: Co se stane, když zrušíte registraci zařízení s Windows? | Dokumentace Microsoftu
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2017
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 47e03edb-0c57-4e25-8e89-4a1069267b8c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a742b5176d5b8dbc7e857e5c5e61c2fc80675166
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882338"
---
# <a name="what-happens-if-you-unenroll-your-windows-device-from-intune"></a>Co se stane, když zrušíte registraci zařízení s Windows v Intune?

Pomocí odkazů na pravé straně této stránky v části **v tomto článku**najdete informace o typu zařízení, které používáte.


## <a name="windows-10-windows-81-windows-8-windows-7-windows-vista"></a>Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista

- Vaše zařízení se už nebude zobrazovat v Portál společnosti a už nemůžete z Portál společnosti instalovat aplikace.

- Pokud jste nainstalovali klientský software Intune, bude z počítače odebrán.

- Z počítače se odebere software Intune Endpoint Protection. Pokud je v počítači nainstalovaný jiný software antivirové ochrany a je zakázaný, může být po odebrání softwaru Intune Endpoint Protection znovu povolený. Po odebrání počítače z Portálu společnosti zkontrolujte svůj počítač.

    > [!IMPORTANT]
    > Pokud tento jiný software antivirové ochrany nebude znovu povolen a nebude nainstalován žádný jiný software antivirové ochrany, může být počítač od daného okamžiku ohrožen a zvýší se tím riziko napadení viry a malwarem.

- Už nebudou platit nastavení, která se v zařízení změnila od jeho přidání (třeba zakázání fotoaparátu/kamery).

- Počítač se už nebude automaticky aktualizovat prostřednictvím aktualizací softwaru nebo antivirového programu ze služby Intune. V závislosti na svém nastavení ale může počítač nadále získávat aktualizace prostřednictvím služeb Windows Server Update Services, Windows Update nebo Microsoft Update.

Kromě toho pro Windows 8.1 platí:

- V zařízení už nemůžete používat firemní aplikace ani data společnosti.

- Některé e-mailové aplikace, jako je Windows Mail, nemůžou získat přístup k firemnímu e-mailu, který je v zařízení už

- Je možné, že se nebudete moct připojit k podnikové síti pomocí Wi-Fi nebo virtuální privátní sítě.

- Je možné, že už v zařízení nebudete mít přístup k některým prostředkům společnosti, jako jsou sdílené složky nebo interní weby.

## <a name="windows-10-mobile-and-windows-phone-81"></a>Windows 10 Mobile a Windows Phone 8.1

- Aplikace Portál společnosti se z vašeho zařízení odinstaluje. To znamená, že se vaše zařízení už nebude zobrazovat v Portál společnosti a nemůžete instalovat aplikace z aplikace Portál společnosti nebo webu Portál společnosti.

- V zařízení už nemůžete používat firemní aplikace ani data společnosti.

- Už nebudou platit nastavení, která se v zařízení změnila od jeho přidání (třeba zakázání fotoaparátu/kamery nebo vyžadování určité délky hesla).

    > [!IMPORTANT]
    > Jedinou výjimkou jsou zásady šifrování, které budou platit dále. Pokud zásady vaší společnosti vyžadovaly, abyste svůj Windows Phone zašifrovali, je jediným způsobem, jak šifrování zrušit, obnovení výchozího továrního nastavení telefonu pomocí nabídky **Nastavení**.

## <a name="windows-rt-running-windows-81"></a>Windows RT s Windows 8.1

- Aplikace Portál společnosti se z vašeho zařízení odinstaluje. To znamená, že vaše zařízení se už nebude zobrazovat v Portál společnosti a nebudete moct instalovat aplikace z Portál společnosti.

- V zařízení už nemůžete používat firemní aplikace ani data společnosti.

- Už nebudou platit nastavení, která se v zařízení změnila od jeho přidání (třeba zakázání fotoaparátu/kamery nebo vyžadování určité délky hesla).

- Je možné, že se už nebudete moct připojit k podnikové síti pomocí Wi-Fi nebo virtuální privátní sítě.

- Je možné, že už v zařízení nebudete mít přístup k některým prostředkům společnosti, jako jsou sdílené složky nebo interní weby.

- Některé e-mailové aplikace, jako je Windows Mail, nemůžou získat přístup k firemnímu e-mailu, který je v zařízení už

Při odebrání zařízení se systémem Windows RT dojde k následujícímu:

- Aplikace Portál společnosti se z vašeho zařízení odinstaluje. To znamená, že vaše zařízení se už nebude zobrazovat v Portál společnosti a nebudete moct instalovat aplikace z Portál společnosti.

- V zařízení už nemůžete používat firemní aplikace ani data společnosti.

- Už nebudou platit nastavení, která se v zařízení změnila od jeho přidání (třeba zakázání fotoaparátu/kamery nebo vyžadování určité délky hesla).

Pokud máte otázky, obraťte se na svou firemní podporu. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
