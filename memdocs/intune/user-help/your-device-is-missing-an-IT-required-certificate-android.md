---
title: Instalace chybějícího požadovaného certifikátu
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 162a5c2ff02a762578fb6f52b60b6ff404862329
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546704"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Instalace chybějícího certifikátu požadovaného vaší organizací  

Pokud zařízení není zaregistrované v Intune a chybí mu požadovaný certifikát, nebudete se moct přihlásit k aplikaci Portál společnosti. Při pokusu o přihlášení se zobrazí tato zpráva:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

K dispozici jsou dvě možnosti, jak si můžete zkusit stáhnout požadovaný certifikát a zaregistrovat své zařízení. 

- Povolit přístup z prohlížeče v aplikaci Portál společnosti.
- Identifikujte chybějící certifikát na firemním nebo školním počítači. Pak na internetu vyhledejte chybějící certifikát. 

Nejprve proveďte kroky pro povolení přístupu z prohlížeče. Pokud pořád nemůžete zaregistrovat svoje zařízení, postupujte podle pokynů k vyhledání certifikátu na internetu. 

## <a name="enable-browser-access"></a>Povolit přístup z prohlížeče
Pokud chcete povolit přístup z prohlížeče, proveďte tyto kroky. Po povolení přístupu Portál společnosti nainstaluje příslušný certifikát a bude pokračovat v registraci.    

1. V aplikaci Portál společnosti přejděte do pravého horního rohu a vyberte nabídku.  
2. Vyberte **Nastavení**.  
3. V poli **Povolit přístup z prohlížeče**vyberte **Povolit**.  
4. Na obrazovce Správce zařízení vyberte **aktivovat**. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Identifikujte a stáhněte chybějící certifikát prostřednictvím vyhledávání na webu
Provedením těchto kroků ručně identifikujte a nainstalujete certifikát do svého zařízení.  

1. Na počítači otevřete aplikaci Internet Explorer. Pokud nemáte počítač, který byste k těmto účelům mohli využít, obraťte se na firemní podporu. Kontaktní informace na svou firemní podporu najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).

2. Přejděte na [web Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980) a přihlaste se pomocí pracovních nebo školních přihlašovacích údajů.

3. Na adresním řádku prohlížeče vyberte úplně vpravo symbol, který vypadá jako visací zámek, jak je vidět na následujícím snímku obrazovky.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Pokud se symbol visacího zámku nezobrazuje, přestaňte a kontaktujte firemní podporu. Zámek znamená, že jste úspěšně přihlášení. Proto byste neměli pokračovat, dokud tento symbol neuvidíte.

4. Vyberte **Zobrazit certifikáty**.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Zvolte kartu **cesta k certifikátu** a potom určete certifikát, který potřebujete získat z Internetu. Název certifikátu, který potřebujete, se zobrazí na stejné pozici jako název zvýrazněný na předchozím snímku obrazovky s příkladem.

6. Pomocí vyhledávacího webu jako Bing nebo Google vyhledejte název chybějícího certifikátu, který jste určili v předchozí části. Název certifikátu může mít různé přípony, třeba .crt nebo .pem.

7. Stáhněte si kořenový certifikát z webu.

8. Po stažení certifikátu si přetažením dolů z horní části zařízení otevřete oznámení a potom v seznamu oznámení klepněte na název požadovaného certifikátu.

4. V dialogovém okně **Název certifikátu** zobrazeném na následujícím snímku obrazovky přijměte výchozí název certifikátu.

5. Zajistěte, aby bylo **použití přihlašovacích údajů** nastaveno na **použití pro sítě VPN a aplikace**, a pak klepněte na **OK**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Zavřete aplikaci Portál společnosti.

7. Aplikaci Portál společnosti znovu otevřete. Teď už by mělo být možné se k aplikaci Portál společnosti přihlásit. Pokud potřebujete pomoc, obraťte se na firemní podporu.

Pokud se vám stejná zpráva typu Chybějící certifikát už zobrazila a už jste použili popsaný postup, pravděpodobně je ještě další certifikát, s jehož instalací vám musí pomoct firemní podpora. Obraťte se o pomoc na firemní podporu prostřednictvím kontaktních informací, které jsou dostupné na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).

## <a name="next-steps"></a>Další kroky  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  
