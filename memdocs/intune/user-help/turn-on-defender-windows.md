---
title: Zapnutí programu Windows Defender | Microsoft Docs
description: Přečtěte si, jak zapnout program Windows Defender a umožnit mu tak přístup k prostředkům společnosti.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: eded7186c670699fa654b0a1be1a7d46c027a56a
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/10/2020
ms.locfileid: "88047973"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Zapnutí přístupu k prostředkům společnosti pro program Windows Defender

Organizace chtějí zajistit, aby zařízení přistupující k prostředkům byla zabezpečená, aby mohla vyžadovat použití [programu Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx). Windows Defender je antivirový software, který je součástí systému Windows, a může přispět k ochraně zařízení před viry a jiným malwarem a hrozbami. 

Tento článek popisuje, jak aktualizovat nastavení zařízení tak, aby splňovala požadavky na antivirový software vaší organizace a vyřešila problémy s přístupem. 

## <a name="turn-on-windows-defender"></a>Zapnutí programu Windows Defender
K zapnutí programu Windows Defender na svém zařízení proveďte následující kroky. 

1. Vyberte nabídku **Start** .
2. Na panelu hledání zadejte **Zásady skupiny**.
3. Vyberte **upravit zásady skupiny**. Otevře se Editor místních zásad skupiny.
4. Vyberte **Konfigurace počítače**  >  **šablony pro správu**  >  **součásti systému Windows**  >  **antivirová ochrana v programu Windows Defender**. 
5. Posuňte se do dolní části seznamu a vyberte **vypnout antivirovou ochranu v programu Windows Defender**.  
6. Vyberte **zakázáno** nebo **není nakonfigurováno**. Tato možnost může být intuitivní, pokud chcete tyto možnosti vybrat, protože názvy navrhují vypnutí programu Windows Defender. Nedělejte si starosti, tyto možnosti skutečně zajišťují, že jsou zapnuté. 
7. Vyberte **použít**  >  **OK**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Zapnutí ochrany v reálném čase a v cloudu

Provedením následujících kroků zapněte ochranu v reálném čase a cloudovou ochranu. Tyto antivirové funkce společně chrání před spywarem a můžou doručovat opravy problémů s malwarem přes Cloud. 

1. Vyberte nabídku **Start** ,
2. Na panelu hledání zadejte **zabezpečení systému Windows**. Vyberte výsledek porovnání. 
3. Vyberte **antivirová & ochrana před hrozbami**.
4. V části **antivirová & nastavení ochrany před hrozbami**vyberte **Spravovat nastavení**.
5. Překlopte každý přepínač v rámci **ochrany v reálném čase** a **ochrany s ochranou cloudu** , abyste je mohli zapnout. 

Pokud se tyto možnosti nezobrazí na obrazovce, můžou být skryté. Proveďte následující kroky, aby byly viditelné.  

1. Vyberte **Start**, otevřete **Ovládací panely**.
2. Na panelu hledání zadejte **Zásady skupiny**.
3. Vyberte **upravit zásady skupiny**. Otevře se Editor místních zásad skupiny.
3. Vyberte možnost **Konfigurace počítače**  >  **šablony pro správu**  >  **součásti systému Windows**  >  Ochrana proti**Windows Security**  >  **virům a hrozbám**zabezpečení systému Windows.
4. Vyberte **Skrýt oblast ochrany před viry a hrozbami**.
5. Vyberte **zakázané**  >  **použít**  >  **OK**.  

## <a name="update-your-antivirus-definitions"></a>Aktualizace antivirových definic
Provedením následujících kroků aktualizujte definice antivirové ochrany.  
1. Vyberte nabídku **Start** ,
2. Na panelu hledání zadejte **zabezpečení systému Windows**. Vyberte výsledek porovnání. 
3. Vyberte **antivirová & ochrana před hrozbami**.
4. V části **antivirová & aktualizace ochrany před internetovými útoky**vyberte **Vyhledat aktualizace**. Pokud tuto možnost nevidíte na obrazovce, proveďte při [Zapnutí ochrany v reálném čase](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection)první sadu kroků. Pak zkuste aktualizace znovu zkontrolovat. 

## <a name="next-steps"></a>Další kroky  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Jeho kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
