---
title: Podepisování a šifrování e-mailů pomocí S/MIME-Microsoft Intune – Azure | Microsoft Docs
description: Naučte se používat e-mailové digitální certifikáty v Microsoft Intune k podepisování a šifrování e-mailů v zařízeních. Tyto certifikáty se nazývají S/MIME a konfigurují se pomocí profilů konfigurace zařízení. Podpisové a šifrovací certifikáty využívají PKCS nebo privátní certifikáty a k importu certifikátů používají konektor.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 863fdd219e9d75ca61322c4eb976c2cdedfd4101
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813971"
---
# <a name="smime-overview-to-sign-and-encrypt-email-in-intune"></a>Přehled s/MIME k podepsání a šifrování e-mailu v Intune

E-mailové certifikáty (označované také jako certifikát S/MIME) poskytují pro vaši e-mailovou komunikaci navíc zabezpečení pomocí šifrování a dešifrování. Microsoft Intune můžou používat certifikáty S/MIME k podepisování a šifrování e-mailů na mobilních zařízeních s následujícími platformami:

- Android
- iOS/iPadOS
- macOS
- Windows 10 a novější

Intune může automaticky doručovat certifikáty šifrování S/MIME na všechny platformy. Certifikáty s/MIME jsou automaticky přidruženy k e-mailovým profilům, které používají nativního poštovního klienta v iOS a s Outlookem na zařízeních s iOS a Androidem. V případě platforem Windows a macOS a u jiných poštovních klientů v iOS a Androidu poskytuje Intune certifikáty, ale uživatelé musí v e-mailové aplikaci ručně povolit S/MIME a zvolit jejich certifikáty S/MIME.

Další informace o podepisování a šifrování e-mailu S/MIME pomocí Exchange najdete v části [S/MIME pro podepisování a šifrování zpráv](/Exchange/policy-and-compliance/smime).

Tento článek poskytuje přehled použití certifikátů S/MIME k podepisování a šifrování e-mailů v zařízeních.

## <a name="signing-certificates"></a>Podpisové certifikáty

Certifikáty používané k podepisování umožňují e-mailové aplikaci klienta bezpečně komunikovat s e-mailovým serverem.

Pokud chcete používat podpisové certifikáty, vytvořte šablonu v certifikační autoritě (CA), která se zaměřuje na podepisování. V článku o [konfiguraci šablony certifikátu serveru](/windows-server/networking/core-network-guide/cncg/server-certs/configure-the-server-certificate-template) najdete postup k vytvoření šablon certifikátu v certifikační autoritě Microsoft Active Directory.

Podpisové certifikáty v Intune používají certifikáty PKCS. [Konfigurace a používání certifikátů PKCS pomocí Intune](certficates-pfx-configure.md) popisuje, jak certifikát PKCS v prostředí Intune nasadit a používat. Tyto kroky zahrnují:

- Stáhněte a nainstalujte Certificate Connector PFX pro podporu požadavků certifikátů PKCS. Konektor má stejné požadavky na síť jako [spravovaná zařízení](../fundamentals/intune-endpoints.md#access-for-managed-devices).
  > [!IMPORTANT]
  > Počínaje verzí Certificate Connector verze 6.2008.60.607 (vydané v srpnu 2020) Tento konektor podporuje nasazení certifikátů pro PCKS #12 žádosti o certifikát a zpracovává žádosti o soubory PFX importované do Intune pro šifrování e-mailů S/MIME pro konkrétního uživatele. Při používání profilů certifikátů PKCS už nemusíte používat konektor Microsoft Intune.
  > 
  > Další informace najdete v tématu [konektory certifikátů](certificate-connectors.md) .
- Vytvoření profilu důvěryhodných kořenových certifikátů pro vaše zařízení. Tento krok zahrnuje použití důvěryhodných kořenových a zprostředkujících certifikátů ve vaší certifikační autoritě a následné nasazení tohoto profilu do zařízení.
- Vytvoření profilu certifikátu PKCS pomocí šablony certifikátu, kterou jste vytvořili. Tento profil bude zařízením vystavovat podpisové certifikáty a nasadí do nich profil certifikátu PKCS.

Podpisový certifikát můžete také importovat konkrétnímu uživateli. Podpisový certifikát se nasadí přes jakékoli zařízení, které uživatel zaregistruje. Pokud chcete certifikáty importovat do Intune, použijte [rutiny PowerShellu, které jsou k dispozici na GitHubu](https://github.com/Microsoft/Intune-Resource-Access). Pokud chcete nasadit certifikát PKCS, který jste importovali do Intune k podepisování e-mailů, postupujte podle kroků v článku [Konfigurace a používání certifikátů PKCS pomocí Intune](certficates-pfx-configure.md). Tyto kroky zahrnují:

- Stažení a instalace konektoru certifikátu PFX pro Microsoft Intune. Tento konektor dodává importované certifikáty PKCS zařízením.
- Import podpisových certifikátů e-mailu S/MIME do Intune.
- Vytvoření importovaného profilu certifikátu PKCS. Tento profil dodává importované certifikáty PKCS odpovídajícím zařízením uživatele.

## <a name="encryption-certificates"></a>Certifikáty šifrování

Certifikáty používané k šifrování potvrzují, že šifrovaný e-mail bude moct dešifrovat pouze zamýšlený příjemce. Šifrování S/MIME je další vrstvou zabezpečení, kterou můžete u e-mailové komunikace použít.

Když odesíláte šifrovaný e-mail jinému uživateli, získá se veřejný klíč certifikátu šifrování tohoto uživatele a odeslaný e-mail se zašifruje. Příjemce e-mail dešifruje pomocí privátního klíče na svém zařízení. Uživatelé mohou k šifrování e-mailů používat historii certifikátů. Aby bylo možné e-mail úspěšně dešifrovat, musí se každý z těchto certifikátů nasadit do všech zařízení konkrétního uživatele.

Certifikáty šifrování e-mailu se doporučuje nevytvářet v Intune. Přestože Intune vystavování certifikátů PKCS, které podporují šifrování, umožňuje, vytváří pro každé zařízení jedinečný certifikát. Jedinečné certifikáty pro každé zařízení nejsou u šifrování pomocí S/MIME, u kterého by se certifikát šifrování měl sdílet mezi všemi zařízeními uživatele, vhodné.

Pokud chcete certifikáty S/MIME nasadit pomocí Intune, musíte všechny certifikáty šifrování uživatele importovat do Intune. Intune pak tyto certifikáty nasadí do každého zařízení, které uživatel zaregistruje. Pokud chcete certifikáty importovat do Intune, použijte [rutiny PowerShellu, které jsou k dispozici na GitHubu](https://github.com/Microsoft/Intune-Resource-Access).

Pokud chcete nasadit certifikát PKCS, který jste importovali do Intune k šifrování e-mailů, postupujte podle kroků v článku [Konfigurace a používání certifikátů PKCS pomocí Intune](certficates-pfx-configure.md). Tyto kroky zahrnují:

- Stažení a instalace konektoru certifikátu PFX pro Microsoft Intune. Tento konektor dodává importované certifikáty PKCS zařízením.
- Import certifikátů šifrování e-mailu S/MIME do Intune.
- Vytvoření importovaného profilu certifikátu PKCS. Tento profil dodává importované certifikáty PKCS odpovídajícím zařízením uživatele.

 > [!NOTE]
 > Intune importované certifikáty šifrování S/MIME odstraní, když se odeberou firemní data nebo když se uživatelé vyřadí ze správy. U certifikační autority se však certifikáty neodvolají.

## <a name="smime-email-profiles"></a>E-mailové profily S/MIME

Jakmile vytvoříte podpisové a šifrovací profily S/MIME, můžete [Povolit S/MIME pro nativní poštu iOS/iPadOS](../configuration/email-settings-ios.md).

## <a name="next-steps"></a>Další kroky

- [Použití protokolu SCEP pro certifikáty](certificates-scep-configure.md)
- [Použití certifikátů PKCS](certficates-pfx-configure.md)
- [Použití partnerské certifikační autority](certificate-authority-add-scep-overview.md)
- [Vystavení certifikátů PKCS z webové služby správce infrastruktury veřejných klíčů Symantec](certificates-digicert-configure.md)