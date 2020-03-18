---
title: Instalace aplikace Portál společnosti pro Windows | Dokumentace Microsoftu
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d65e3452-5bbf-4d26-a06e-401ddcc47f39
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 6a8c7212de97fbcb741d03cbcec57bafc4692484
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79324139"
---
# <a name="what-happens-if-you-install-the-company-portal-app-and-enroll-your-windows-device-in-intune"></a>Co se stane, když nainstaluji aplikaci Portál společnosti a zaregistruji zařízení s Windows v Intune?

Když nainstalujete aplikaci Portál společnosti a pak přes ni zaregistrujete zařízení s Windows nebo Windows Phone, umožníte tím firemní podpoře spravovat vaše zařízení a zajistit tak vyšší zabezpečení firemních dat. Toto téma popisuje, co se stane u zařízení se systémem starším než Windows 10. Informace pro zařízení s Windows 10 najdete v [souvisejícím tématu](about-cp-app-for-windows-10.md).  

## <a name="what-happens-to-all-windows-devices-after-enrollment"></a>Co se stane všem zařízením s Windows po registraci
Registrace zařízení s Windows nebo Windows Phone v Intune nabízí tyto možnosti:

- Přístup k podnikové síti, e-mailu a pracovním souborům

- Získání aplikací společnosti z webu Portál společnosti (__Poznámka__: Pro Windows 7 a Windows Vista je možné získat aplikace společnosti jenom z webu Portál společnosti.)

- Automatické nastavení e-mailového účtu vaší společnosti nebo školy

- Obnovení továrního nastavení telefonu v případě ztráty nebo odcizení

Když zaregistrujete zařízení, udělujete firemní podpoře oprávnění provést následující akce:

- Obnovit v zařízení výchozí tovární nastavení. To je užitečné v případě ztráty nebo odcizení zařízení.

- Odebrat obchodní aplikace a soubory, ale jenom takové, které jsou spojené se společností. *Vaše osobní data a nastavení odebrána nebudou.*

- Firemní podpora může vidět software nainstalovaný v zařízení, a to i software, který jste si nainstalovali sami.

- Nastavit požadavky na zařízení, třeba vyžadovat heslo k zařízení nebo PIN kód a tím lépe chránit data společnosti. Vaše firemní podpora může také omezit počet možných zadání nesprávného hesla. Když se tento počet překročí, může se zařízení zablokovat.

- Vyžadovat šifrování dat v zařízení kvůli ochraně dat společnosti v případě ztráty nebo odcizení zařízení.

- Vyžadovat, abyste přijali smluvní podmínky.

- Zabránit pořizování snímků dat souvisejících se společností.

## <a name="what-happens-to-all-windows-pcs-after-enrollment"></a>Co se stane všem počítačům s Windows po registraci

- Do vašeho počítače se nainstaluje software, který firemní podpoře umožní spravovat daný počítač a vám umožní přístup k prostředkům společnosti, jako jsou aplikace a informace o podpoře. Vaše firemní podpora může tento software automaticky aktualizovat.

- Do vašeho počítače se může nainstalovat služba Intune Endpoint Protection. Tento software vyhledává viry a malware.

- Firemní podpora může shromažďovat nebo odstraňovat data z pevného disku vašeho počítače.

- Firemní podpora může do vašeho počítače instalovat aplikace a aktualizace.

## <a name="what-happens-every-eight-hours-after-device-enrollment"></a>Co se stane každých 8 hodin po registraci zařízení

Přibližně každých osm hodin proběhne na zaregistrovaných zařízeních toto:

- Stažení všech zásad nebo aktualizací aplikací, které vám firemní podpora zpřístupnila.

- Odeslání všech aktualizací inventáře hardwaru.

- Odeslání všech aktualizací inventáře aplikací společnosti.

Pokud máte otázky, obraťte se na svou firemní podporu. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
