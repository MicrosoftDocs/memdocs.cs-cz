---
title: Úvod do profilů certifikátů
titleSuffix: Configuration Manager
description: Přečtěte si, jak profily certifikátů v Configuration Manager pracují se službou AD CS (Active Directory Certificate Services).
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722302"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Úvod k profilům certifikátů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Profily certifikátů pracují se službou AD CS (Active Directory Certificate Services) a s rolí služby zápisu síťových zařízení (NDES). Vytvořte a nasaďte ověřovací certifikáty pro spravovaná zařízení, aby uživatelé mohli snadno přistupovat k prostředkům organizace. Můžete například vytvořit a nasadit profily certifikátů, které zajistí uživatelům potřebné certifikáty pro připojení k síti VPN a bezdrátovým připojením.

Profily certifikátů mohou automaticky konfigurovat zařízení uživatelů pro přístup k prostředkům organizace, jako jsou sítě Wi-Fi a servery VPN. Uživatelé mají přístup k těmto prostředkům bez ruční instalace certifikátů nebo pomocí procesu mimo IP síť. Profily certifikátů usnadňují zabezpečení prostředků, protože můžete používat bezpečnější nastavení podporovaná infrastrukturou veřejných klíčů (PKI). Například vyžadovat ověření serveru pro všechna připojení Wi-Fi a VPN, protože jste nasadili požadované certifikáty na spravovaných zařízeních.

Profily certifikátů nabízejí následující možnosti správy:  

- Zápis a obnovení certifikátů z certifikační autority (CA) pro zařízení, která používají různé typy a verze operačního systému. Tyto certifikáty se pak dají použít pro připojení Wi-Fi a VPN.  

- Nasazení důvěryhodných kořenových certifikátů certifikačních autorit a certifikátů Zprostředkující certifikační autority Tyto certifikáty konfigurují řetěz důvěryhodnosti v zařízeních pro připojení VPN a Wi-Fi v případě, že je vyžadováno ověření serveru.  

- Monitorování a vytváření sestav s informacemi o instalovaných certifikátech.  

**Příklad 1**: všichni zaměstnanci se musí připojovat k Wi-Fi hotspotům ve více kancelářích poboček. Pokud chcete povolit snadné připojení k uživateli, nejdřív nasaďte certifikáty potřebné pro připojení k Wi-Fi. Pak nasaďte profily sítě Wi-Fi, které na certifikát odkazují.  

**Příklad 2**: máte na místě infrastrukturu PKI. Chcete přejít na flexibilnější a bezpečnější metodu nasazení certifikátů. Uživatelé potřebují přístup k prostředkům organizace ze svých osobních zařízení, aniž by to ohrozilo zabezpečení. Nakonfigurujte profily certifikátů pomocí nastavení a protokolů, které jsou podporované pro konkrétní platformu zařízení. Zařízení pak můžou tyto certifikáty automaticky vyžádat z internetového registračního serveru. Pak nakonfigurujte profily sítě VPN tak, aby používaly tyto certifikáty, takže zařízení bude mít přístup k prostředkům organizace.  

## <a name="types"></a>Typy

Existují tři typy profilů certifikátů:  

- **Certifikát důvěryhodné certifikační autority**: nasaďte důvěryhodnou kořenovou certifikační autoritu nebo certifikát zprostředkující certifikační autority. Tyto certifikáty tvoří řetěz důvěryhodnosti, pokud zařízení musí ověřit server.  

- **Simple Certificate Enrollment Protocol (SCEP)**: Vyžádejte si certifikát pro zařízení nebo uživatele pomocí protokolu SCEP. Tento typ vyžaduje roli služby zápisu síťových zařízení (NDES) na serveru se systémem Windows Server 2012 R2 nebo novějším.

    Chcete-li vytvořit profil certifikátu **Simple Certificate Enrollment Protocol (SCEP)** , nejprve vytvořte profil **certifikátu důvěryhodné certifikační autority** .

- **Personal Information Exchange (. pfx)**: Vyžádejte si certifikát a. pfx (označovaný také jako PKCS #12) pro zařízení nebo uživatele.<!--1321368--> Existují dvě metody vytvoření profilů certifikátů PFX:

  - [Importovat přihlašovací údaje](../../mdm/deploy-use/import-pfx-certificate-profiles.md) z existujících certifikátů
  - [Definování certifikační](../../mdm/deploy-use/create-pfx-certificate-profiles.md) autority pro zpracování požadavků

  > [!Note]  
  > Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  Můžete použít Microsoft nebo pověřit jako certifikační autoritu pro certifikáty **Personal Information Exchange (. pfx)** .

## <a name="requirements"></a>Požadavky

Chcete-li nasadit profily certifikátů používající protokol SCEP, nainstalujte bod registrace certifikátu na server systému lokality. Nainstalujte také modul zásad pro NDES a modul zásad Configuration Manager na serveru, na kterém běží Windows Server 2012 R2 nebo novější. Tento server vyžaduje roli služby Active Directory Certificate Services. Vyžaduje také pracovní NDES, který je přístupný pro zařízení, která vyžadují certifikáty. Pokud se vaše zařízení musí zaregistrovat pro certifikáty z Internetu, musí být váš server NDES dostupný z Internetu. Pokud například chcete bezpečně povolit provoz na server NDES z Internetu, můžete použít službu [Azure Application proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

Certifikáty PFX také vyžadují bod registrace certifikátu. Zadejte také certifikační autoritu (CA) certifikátu a příslušné přihlašovací údaje pro přístup. Můžete zadat Microsoft nebo pověřit jako certifikační autority.  

Další informace o tom, jak NDES podporuje modul zásad, aby Configuration Manager mohl nasazovat certifikáty, najdete v tématu [použití modulu zásad se službou zápisu síťových zařízení](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

V závislosti na požadavcích Configuration Manager podporuje nasazení certifikátů do různých úložišť certifikátů v různých typech zařízení a operačních systémech. Jsou podporovány následující zařízení a operační systémy:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Pro správu Windows Phone 8,1 a Windows 10 Mobile použijte Configuration Manager místní MDM. Další informace najdete v tématu [místní MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Typickým scénářem pro Configuration Manager je instalace důvěryhodných kořenových certifikátů CA pro ověřování serverů Wi-Fi a VPN. Typická připojení používají následující protokoly:

- Protokoly ověřování: EAP-TLS, EAP-TTLS a PEAP
- Protokoly tunelového připojení VPN: IKEv2, L2TP/IPsec a Cisco IPsec

Než může zařízení požadovat certifikáty pomocí profilu certifikátu SCEP, musí být v zařízení nainstalovaný certifikát pro kořenovou certifikační autoritu organizace.  

V profilu certifikátu SCEP můžete zadat nastavení pro vyžádání přizpůsobených certifikátů pro různá prostředí nebo požadavky na připojení. **Průvodce vytvořením profilu certifikátu** obsahuje dvě stránky parametrů registrace. První **zápis SCEP**obsahuje nastavení požadavku na zápis a místa instalace certifikátu. Druhá s názvem **Vlastnosti certifikátu**popisuje vlastní požadovaný certifikát.  

## <a name="deploy"></a>Nasazení

Když nasadíte profil certifikátu SCEP, klient Configuration Manager tyto zásady zpracuje. Pak vyžádá heslo výzvy SCEP z bodu správy. Zařízení vytvoří pár veřejného a privátního klíče a vygeneruje žádost o podepsání certifikátu (CSR). Odešle tento požadavek na server NDES. Server NDES předá požadavek do systému lokality bodu registrace certifikátu prostřednictvím modulu zásad NDES. Bod registrace certifikátu ověří požadavek, zkontroluje heslo pro výzvu SCEP a ověří, že žádost nebylo manipulováno. Pak žádost schválí nebo zamítne. Pokud je schválen, server NDES odešle žádost o podepsání do připojené certifikační autority (CA) pro podepsání. Certifikační autorita podepíše požadavek a potom vrátí certifikát do žádajícího zařízení.

Nasaďte profily certifikátů do kolekcí uživatelů nebo zařízení. Můžete zadat cílové úložiště pro každý certifikát. Pravidla použitelnosti určují, jestli zařízení může certifikát nainstalovat.

Když nasadíte profil certifikátu do uživatelské kolekce, určí [spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) , které ze zařízení uživatelů tyto certifikáty instalují. Když nasadíte profil certifikátu s uživatelským certifikátem do kolekce zařízení, ve výchozím nastavení každé primární zařízení uživatele nainstaluje certifikáty. Pokud chcete certifikát nainstalovat na kterékoli ze zařízení uživatelů, změňte toto chování na stránce **pro zápis SCEP** v **Průvodci vytvořením profilu certifikátu**. Pokud se zařízení nacházejí v pracovní skupině, Configuration Manager neprovádí nasazení uživatelských certifikátů.  

## <a name="monitor"></a>Monitorování

Nasazení profilů certifikátů můžete monitorovat zobrazením výsledků nebo sestav dodržování předpisů. Další informace najdete v tématu [monitorování profilů certifikátů](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Automatické odvolání

Configuration Manager automaticky odvolává certifikáty uživatelů a počítačů, které byly nasazeny pomocí profilů certifikátů v následujících situacích:  

- Zařízení je vyřazené ze správy Configuration Manager.  

- Zařízení je blokované z hierarchie Configuration Manager.  

Při odvolání certifikátu server lokality zašle příkaz k odvolání vydávající certifikační autoritě. Jako důvod odvolání je uveden **Ukončení provádění operací**.

> [!NOTE]
> Aby byl certifikát správně odvolán, účet počítače pro lokalitu nejvyšší úrovně v hierarchii potřebuje oprávnění k **vydávání a správě certifikátů** v certifikační autoritě.
>
> Pro zvýšení zabezpečení můžete také omezit správce certifikační autority v certifikační autoritě. Pak tomuto účtu udělte jenom oprávnění ke konkrétní šabloně certifikátu, kterou použijete pro profily SCEP v lokalitě.

## <a name="next-steps"></a>Další kroky

- [Vytváření profilů certifikátů](create-certificate-profiles.md)

- [Konfigurace infrastruktury certifikátu](certificate-infrastructure.md)
