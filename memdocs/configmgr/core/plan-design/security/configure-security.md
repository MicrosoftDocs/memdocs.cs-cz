---
title: Konfigurace zabezpečení
titleSuffix: Configuration Manager
description: Nakonfigurujte možnosti související se zabezpečením pro Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718662"
---
# <a name="configure-security-in-configuration-manager"></a>Konfigurace zabezpečení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám pomůžou nastavit možnosti týkající se zabezpečení pro Configuration Manager. Zahrnuje následující možnosti zabezpečení:
- [Komunikace s klientským počítačem](#BKMK_ConfigureClientPKI) pro klientské certifikáty PKI  
- [Podepisování a šifrování](#BKMK_ConfigureSigningEncryption)  
- [Správa na základě rolí](#BKMK_ConfigureRBA)  
- [Správa účtů](#BKMK_ManageAccounts)  
- [Konfigurace Azure Active Directory](#bkmk_azuread)  
- [Konfigurace ověřování poskytovatele služby SMS](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a>Konfigurovat nastavení pro klientské certifikáty PKI  

Chcete-li používat certifikáty infrastruktury veřejného klíče (PKI) pro připojení klientů k systémům lokalit, které používají službu Internet Information Services (IIS), použijte pro konfiguraci nastavení těchto certifikátů následující postup:  

#### <a name="to-configure-client-pki-certificate-settings"></a>Konfigurace nastavení klientského certifikátu PKI  

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte primární lokalitu, kterou chcete nakonfigurovat.  

2.  Na pásu karet vyberte možnost **vlastnosti**. Pak přejděte na kartu **komunikace s klientským počítačem** .  

    > [!Note]
    > Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

3.  Vyberte nastavení pro systémy lokalit, které používají službu IIS.  

    - **Pouze https**: klienti, kteří jsou přiřazeni k lokalitě, vždy používají klientský certifikát PKI, když se připojují k systémům lokality, které používají službu IIS.  

    - **Https nebo http**: nepožadujete, aby klienti používali certifikáty PKI.  

    - **Použijte Configuration Manager generované certifikáty pro systémy lokality http**: Další informace o tomto nastavení najdete v tématu [Rozšířená http](../hierarchy/enhanced-http.md).  

4.  Vyberte nastavení pro klientské počítače.  

    - **Použít klientský certifikát PKI (schopnost ověřování klientů), pokud je k dispozici**: Pokud jste zvolili nastavení server lokality protokolu **https nebo http** , zvolte tuto možnost, pokud chcete pro připojení HTTP použít certifikát PKI klienta. Klient používá tento certifikát místo certifikátu podepsaného svým držitelem k vlastnímu ověření systémů lokality. Pokud jste zvolili **jenom https**, tato možnost se automaticky zvolí.  

    Pokud je na klientovi k dispozici více než jeden platný klientský certifikát PKI, klikněte na tlačítko **Upravit** a proveďte konfiguraci metod výběru klientského certifikátu.  

    Další informace o metodě výběru klientského certifikátu naleznete v tématu [Planning for PKI client certificate selection](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **Klienti kontrolují seznam odvolaných certifikátů (CRL) pro systémy lokality**: Povolením tohoto nastavení pro klienty ZKONTROLUJETE seznam CRL vaší organizace pro odvolané certifikáty.  

    Další informace o kontrole CRL pro klienty naleznete v tématu [Planning for PKI certificate revocation](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Chcete-li importovat, zobrazit a odstranit certifikáty důvěryhodných kořenových certifikačních autorit, vyberte možnost **nastavit**.  

    Další informace najdete v tématu [plánování důvěryhodných kořenových certifikátů PKI a seznamu vystavitelů certifikátů](plan-for-security.md#BKMK_PlanningForRootCAs).  


Tento postup opakujte u všech primárních lokalit v hierarchii.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a>Konfigurace podepisování a šifrování  

Nakonfigurujte nejbezpečnější nastavení podpisování a šifrování pro systémy lokalit, která mohou všichni klienti podporovat. Tato nastavení jsou zvláště důležitá, když necháte klienty komunikovat se systémy lokalit přes protokol HTTP pomocí certifikátů podepsaných svými držiteli.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Konfigurace podpisování a šifrování pro lokalitu  

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte primární lokalitu, kterou chcete nakonfigurovat.  

2.  Na pásu karet vyberte **vlastnosti**a pak přepněte na kartu **podepisování a šifrování** .  

    Tato karta je dostupná pouze v primární lokalitě. Pokud nevidíte kartu **podepisování a šifrování** , ujistěte se, že nejste připojeni k lokalitě centrální správy nebo k sekundární lokalitě.  

3.  Nakonfigurujte možnosti podepisování a šifrování pro klienty, kteří budou komunikovat s lokalitou.  

    - **Vyžadovat podepisování**: klienti před odesláním do bodu správy podepisují data.  

    - **Vyžadovat SHA-256**: klienti při podepisování dat používají algoritmus SHA-256.  

    > [!WARNING]  
    >  **Nevyžadovat SHA-256** bez předchozího potvrzení, že všichni klienti podporují tento algoritmus hash. Tito klienti zahrnují ty, které mohou být v budoucnu přiřazeny k lokalitě.  
    >   
    >  Pokud zvolíte tuto možnost a klienti s certifikáty podepsanými držitelem nepodporují SHA-256, Configuration Manager je odmítne. Komponenta SMS_MP_CONTROL_MANAGER zaznamená zprávu s ID 5443.  

    - **Použití šifrování**: klienti šifrují data inventáře klienta a stavové zprávy před odesláním do bodu správy. Používají algoritmus 3DES.  

Tento postup opakujte u všech primárních lokalit v hierarchii.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a>Konfigurace správy na základě rolí  

Správa na základě rolí kombinuje role zabezpečení, rozsahy zabezpečení a přidělené kolekce k definování rozsahu správy pro jednotlivé správce. Obor zahrnuje objekty, které může uživatel zobrazit v konzole nástroje, a úlohy související s objekty, ke kterým mají oprávnění. Konfigurace správy na základě rolí platí pro všechny lokality v hierarchii.  

Další informace najdete v tématu [Konfigurace správy na základě rolí](../../servers/deploy/configure/configure-role-based-administration.md). Tento článek podrobně popisuje následující akce:  

-  Vytvoření vlastních rolí zabezpečení  

- Konfigurování rolí zabezpečení  

-  Konfigurování oborů zabezpečení pro objekt  

-  Konfigurování kolekcí pro správu zabezpečení  

-  Vytvoření nového správce  

- Úprava oboru správy správce  

> [!IMPORTANT]  
>  Váš vlastní rozsah správce definuje objekty a nastavení, které můžete přidělit, když konfigurujete správu na základě rolí pro dalšího správce. Informace o plánování správy na základě rolí najdete v tématu [základy správy na základě rolí](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a>Správa účtů, které Configuration Manager používá  

Configuration Manager podporuje účty systému Windows pro celou řadu různých úloh a použití. Chcete-li zobrazit účty, které jsou nakonfigurovány pro různé úlohy, a spravovat heslo, které Configuration Manager používá pro každý účet, použijte následující postup:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Správa účtů, které Configuration Manager používá  

1.  V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **zabezpečení**a pak zvolte uzel **účty** .  

2.  Chcete-li změnit heslo pro účet, vyberte účet v seznamu. Pak na pásu karet vyberte **vlastnosti** .  

3.  Kliknutím na **nastavit** otevřete dialogové okno **uživatelský účet systému Windows** . Zadejte nové heslo pro Configuration Manager, které chcete pro tento účet použít.  

    > [!NOTE]  
    >  Heslo, které zadáte, musí odpovídat heslu tohoto účtu ve službě Active Directory.  

Další informace najdete v tématu [účty používané v Configuration Manager](../hierarchy/accounts.md).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a>Konfigurace Azure Active Directory

Integrací Configuration Manager s Azure Active Directory (Azure AD) můžete zjednodušit a povolit cloudové prostředí. Umožňuje webu a klientům ověřování pomocí Azure AD. Další informace najdete v tématu Služba **Cloud Management** v části [Konfigurace služeb Azure](../../servers/deploy/configure/azure-services-wizard.md).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a>Konfigurace ověřování poskytovatele služby SMS

Počínaje verzí 1810 můžete určit minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. Další informace najdete v tématu [plánování poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Viz také

- [Plánování zabezpečení](plan-for-security.md)  

- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Komunikace mezi koncovými body](../hierarchy/communications-between-endpoints.md)  

- [Technické informace o kryptografických ovládacích prvcích](cryptographic-controls-technical-reference.md)  

- [Požadavky na certifikát PKI](../network/pki-certificate-requirements.md)  
