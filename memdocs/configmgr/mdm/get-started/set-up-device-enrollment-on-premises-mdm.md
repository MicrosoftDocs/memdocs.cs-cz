---
title: Nastavení registrace pro místní MDM
titleSuffix: Configuration Manager
description: Udělte uživatelům oprávnění k registraci svých zařízení pro místní správu mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721840"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Nastavení registrace zařízení pro místní správu mobilních zařízení (MDM) v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Posledním krokem pro nastavení místní správy mobilních zařízení (MDM) je umožnit uživatelům registraci svých zařízení. Pomocí Configuration Manager nastavení klienta můžete uživatelům udělit oprávnění k registraci zařízení v místní správě mobilních zařízení (MDM).

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> Vytvoření profilu zápisu

Pokud chcete zadat nastavení potřebná k tomu, aby mohli uživatelé registrovat mobilní zařízení, přidejte do výchozího nastavení klienta nový profil zápisu. Tento profil se pak použije pro všechny uživatele v Configuration Manager lokalitě.

> [!NOTE]
> Tento proces používá **výchozí nastavení klienta**, které se automaticky použije pro všechna zařízení a uživatele. Případně můžete vytvořit vlastní nastavení klienta a pak ho nasadit do kolekcí podle svého výběru. Tato alternativní metoda vyžaduje aspoň dvě vlastní nastavení klienta, jednu pro nastavení *zařízení* a jednu pro *uživatelská* nastavení. Další informace najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **nastavení klienta** . Otevřete **výchozí nastavení klienta** a vyberte skupinu **registrace** .

1. V části nastavení zařízení zadejte **interval dotazování pro moderní zařízení (minuty)**. Ve výchozím nastavení je tento interval 60 minut.

1. V části nastavení uživatele povolte možnost **Povolit uživatelům registrovat moderní zařízení**.

1. Pro **profil registrace moderního zařízení**vyberte **nastavit profil**. V okně registrační profil vyberte **vytvořit**.

1. V okně vytvořit registrační profil zadejte následující informace:

    - Jedinečný a popisný **název** registračního profilu.

    - Volitelný **Popis** k poskytnutí dalších informací o profilu.

    - Vyberte **kód lokality pro správu** , která obsahuje bod správy zařízení. Kliknutím na **tlačítko OK** uložte a zavřete.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Konfigurovat další nastavení klienta

Existují další nastavení klienta ke konfiguraci zařízení po jejich registraci. Obecnější informace najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager podporuje následující nastavení klienta pro místní správu mobilních zařízení (MDM):

- **Zásady klienta**: Tato nastavení určují frekvenci stahování zásad klienta do zařízení. Můžete také povolit nastavení pro zásady uživatele. Další informace najdete v tématu [o nastavení klienta – zásady klienta](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Nasazení softwaru**: nastavte interval pro vyhodnocení nasazení softwaru. Další informace najdete v tématu informace [o nastavení klienta – nasazení softwaru](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > Pro místní správu mobilních zařízení (MDM) se dá nastavení nasazení softwaru použít jenom jako výchozí nastavení klienta.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Vyhledat uživatele

Aby uživatelé mohli přijímat nastavení klienta s profilem registrace pro místní správu mobilních zařízení (MDM), lokalita zjistí svůj uživatelský účet ve službě Active Directory. Když chcete mít jistotu, že profil registrace dostali všichni uživatelé, kteří ho potřebují, spusťte funkci zjišťování uživatelů služby Active Directory. Další informace najdete v tématu [zjišťování uživatelů služby Active Directory](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Instalace důvěryhodného kořenového certifikátu

Zařízení připojená k doméně získají kořenový certifikát důvěryhodnosti pro důvěryhodnou komunikaci se servery hostujícími role systému lokality. Služba Active Directory Certificate Services automaticky distribuuje důvěryhodný kořenový certifikát. Počítače, které nejsou připojené k doméně a mobilní zařízení, potřebují tento certifikát nainstalovat jiným způsobem, aby bylo možné registraci.

> [!NOTE]
> Pokud jsou certifikáty webového serveru vydávány veřejnou certifikační autoritou, většina zařízení už tyto certifikační autority důvěřuje. Pokud váš návrh zahrnuje použití jednoho z těchto veřejných certifikačních autorit, nemusíte tento krok provádět.

Po [exportu důvěryhodného kořenového certifikátu](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)ho budete muset nainstalovat do zařízení, která ho budou potřebovat k registraci. Například zařízení, která nejsou připojená k doméně a nemohou je automaticky získat ze služby Active Directory. Proces, který použijete, bude záviset na následujících faktorech:

- Konkrétní typy zařízení a technické možnosti
- Verze operačního systému
- Požadavky na vaše podnikání, zabezpečení a uživatelské prostředí

Následující seznam obsahuje příklady metod pro doručení a instalaci důvěryhodného kořenového certifikátu na zařízeních:

- Sdílená složka

- Příloha e-mailu

- Paměťová karta

- Připojené zařízení

- Cloudové úložiště (třeba OneDrive)

- Bezkontaktní komunikace (NFC)

- Skener čárových kódů

- Zřizovací balíček softwaru spouštěného při prvním zapnutí počítače

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Ruční instalace důvěryhodného kořenového certifikátu v systému Windows

1. V zařízení, které se má zaregistrovat, přejděte v Průzkumníkovi souborů do souboru důvěryhodného kořenového certifikátu (. cer) a **otevřete** ho.

1. V okně certifikát vyberte **nainstalovat certifikát**.

1. V Průvodci importem certifikátu vyberte **místní počítač**a potom klikněte na tlačítko **Další** a pokračujte jako správce.

1. Na stránce úložiště certifikátů vyberte možnost **umístit všechny certifikáty do následujícího úložiště**a pak vyberte **Procházet**.

1. V okně vybrat úložiště certifikátů vyberte **Důvěryhodné kořenové certifikační autority**a pak vyberte **OK**.

1. Dokončení a průvodce.

## <a name="next-step"></a>Další krok

> [!div class="nextstepaction"]
> [Registrovat zařízení](../deploy-use/enroll-devices-on-premises-mdm.md)
