---
title: Konfigurace klientů na používání publikování DNS
titleSuffix: Configuration Manager
description: Konfigurace Configuration Manager klientských počítačů pro vyhledání bodů správy pomocí publikování DNS.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713097"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Konfigurace klientských počítačů pro vyhledání bodů správy pomocí publikování DNS

*Platí pro: Configuration Manager (Current Branch)*

Klienti v Configuration Manager musí vyhledat bod správy, aby bylo možné dokončit přiřazení lokality, a jako probíhající proces zůstane spravován. Nejbezpečnější způsob hledání bodů správy v intranetu nabízí klientům služba AD DS (Active Directory Domain Services). Pokud však klienti nemohou tuto metodu umístění služby použít (nemáte-li například rozšířené schéma služby Active Directory nebo jsou-li klienti členy pracovní skupiny), použijte jako preferovanou metodu publikování DNS.  

> [!NOTE]  
>  Když instalujete klienta pro systémy Linux a UNIX, musíte zadat bod správy, který slouží jako počáteční kontaktní bod. Informace o tom, jak nainstalovat klienta nástroje pro Linux a UNIX, najdete v tématu [postup nasazení klientů na servery se systémy UNIX a Linux](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Před použitím publikování DNS pro body správy zkontrolujte, zda servery DNS v intranetu mají záznamy prostředků umístění služby (SRV RR) a odpovídající záznamy prostředků hostitele (A nebo AAA) pro body správy lokality. Záznamy prostředků umístění služby může vytvořit automaticky Configuration Manager nebo ručně Správce DNS, který vytváří záznamy ve službě DNS.  

 Další informace o publikování DNS jako metody umístění služby pro klienty Configuration Manager najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality pro Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Ve výchozím nastavení hledají klienti ve službě DNS body správy ve své doméně DNS. Pokud však v doméně klientů nejsou publikovány žádné body správy, je nutné ručně nakonfigurovat klienty s příponou DNS bodu správy. Tuto příponu DNS můžete u klientů nastavit v průběhu instalace klienta nebo po jejím dokončení:  

-   Chcete-li u klientů nastavit příponu bodu správy v průběhu instalace klienta, nastavte vlastnosti souboru CCMSetup Client.msi.  

-   Chcete-li u klientů nastavit příponu bodu správy po instalaci klienta, v Ovládacích panelech nastavte **Vlastnosti nástroje Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Nastavení přípony bodu správy v průběhu instalace klienta  

- Nainstalujte klienta s následující vlastností souboru CCMSetup Client.msi:  

  - **DnsSuffix =** * &lt;doména bodu správy\>*  

     Pokud má lokalita více bodů správy, které se nacházejí v různých doménách, zadejte pouze jednu doménu. Klienti si po připojení k bodu správy v této doméně stáhnou seznam dostupných bodů správy, který obsahuje i body správy v jiných doménách.  

    Další informace o vlastnostech příkazového řádku CCMSetup najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Nastavení přípony bodu správy po instalaci klienta  

1.  V Ovládacích panelech klientského počítače přejděte na položku **Configuration Manager**a poté dvakrát klikněte na možnost **Vlastnosti**.  

2.  Na kartě **Lokalita** zadejte příponu DNS bodu správy a poté klikněte na tlačítko **OK**.  

     Pokud má lokalita více bodů správy, které se nacházejí v různých doménách, zadejte pouze jednu doménu. Klienti si po připojení k bodu správy v této doméně stáhnou seznam dostupných bodů správy, který obsahuje i body správy v jiných doménách.
