---
title: Zařízení nemá certifikát | Dokumentace Microsoftu
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/04/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: df973b18-9166-417d-8aa3-49edd2bda256
searchScope:
- User help
ROBOTS: NOINDEX, NOFOLLOW
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 827780900904f4a04575b6ed6d1363112b8c6eec
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079922"
---
# <a name="your-android-device-is-missing-a-certificate-that-usually-comes-installed-on-your-phone"></a>Ve vašem zařízení s Androidem chybí certifikát, který je v telefonu obvykle nainstalovaný

Pokud zařízení není zaregistrované v Intune a chybí mu certifikát, který je obvykle nainstalovaný v telefonu, nebudete se moct přihlásit k aplikaci Portál společnosti. Při pokusu o přihlášení se zobrazí tato zpráva:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Tento problém můžete opravit, když si požadovaný certifikát stáhnete ze [stránky certifikátů Digicertu](https://www.digicert.com/digicert-root-certificates.htm).

1. Vyhledejte a stáhněte si certifikát __Baltimore CyberTrust Root__. Můžete si ho také stáhnout přímo [odsud](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).

2. Přetažením dolů z horní části obrazovky zobrazte seznam s posledními oznámeními a klepněte na **BaltimoreCyberTrustRoot.crt**.

3. Vaše zařízení vás vyzve k **pojmenování certifikátu**. Neměňte výchozí název certifikátu, který se zobrazí.

4. Zajistěte, aby bylo **použití přihlašovacích údajů** nastaveno na **použití pro sítě VPN a aplikace**, a pak klepněte na **OK**.

    ![screenshot-certificate-name-dialog-showing-baltimore-certificate-name](./media/andr-cert_install-2-add_cert_name.png)

5. Zavřete prohlížeč a aplikaci Portál společnosti.

6. Aplikaci Portál společnosti znovu otevřete. Teď už by mělo být možné se k aplikaci Portál společnosti přihlásit. Pokud stále nemůžete aplikaci Portál společnosti použít, obraťte se na svou firemní podporu pomocí informací uvedených na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980), a požádejte ji, aby vám sdělila další pokyny.

>[!NOTE]
> Pokud instalace tohoto certifikátu problém nevyřeší a zobrazí se vám jiná zpráva o chybějícím certifikátu, bude nutné provést další kroky k [instalaci chybějícího certifikátu](your-device-is-missing-an-IT-required-certificate-android.md).

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
