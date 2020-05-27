---
title: Registrace zařízení s Windows 10 v Portál společnosti Intune | Microsoft Docs
description: Postup registrace zařízení s Windows 10 v Portál společnosti Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/21/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 812e82df-76df-402b-bfe9-29302838f40e
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jieyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: cffdadab0518fbc6a52d0f2bf60752c165fd1c3e
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881500"
---
# <a name="enroll-windows-10-devices-with-intune-company-portal"></a>Registrace zařízení s Windows 10 pomocí Portál společnosti Intune

Použijte Portál společnosti Intune k registraci zařízení s Windows 10 v rámci správy vaší organizace. Tento článek popisuje, jak zaregistrovat zařízení ve Windows 10 verze 1607 a novějších a Windows 10 verze 1511 a starší. Než začnete, ujistěte se, že jste [na svém zařízení ověřili verzi](windows-enrollment-company-portal.md#find-windows-10-version-number) , abyste mohli postupovat podle správných kroků.  

Windows 10 se podporuje napříč různými typy zařízení, včetně stolních počítačů, telefonů a tabletů. Postup registrace je stejný u libovolného zařízení, které používáte. Vaše obrazovka ale může vypadat trochu jinak než obrázky uvedené v tomto článku.  
</br>
> [!VIDEO https://www.youtube.com/embed/TKQxEckBHiE?rel=0]

## <a name="enroll-windows-10-version-1607-and-later-device"></a>Registrace zařízení s Windows 10 verze 1607 a novější 
Tento postup popisuje, jak zaregistrovat zařízení, které běží ve Windows 10 verze 1607 a novější.  

1. Přejděte na **Start**. Pokud jste na zařízení s Windows 10 Mobile, pokračujte na seznam **všechny aplikace** .

2. Otevřete aplikaci **Nastavení**. Pokud aplikace není v seznamu aplikací snadno dostupná, otevřete panel hledání a zadejte "nastavení".

3. Vyberte **účty**  >  **přístup do práce nebo do školy**  >  **připojit**.  


    ![Vyberte možnost Nastavit pracovní nebo školní účet.](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

4. Pokud se chcete dostat na přihlašovací stránku Intune vaší organizace, zadejte svou pracovní nebo školní e-mailovou adresu. Pak vyberte **Další**.  


   ![Zadejte svůj pracovní nebo školní účet](./media/w10-enroll-rs1-set-up-work-or-school-account.png)  

5. Přihlaste se k Intune ze svého pracovního nebo školního účtu.  


    ![Přidání pracovního nebo školního účtu](./media/w10-enroll-rs1-enter-your-credentials.png)  

    Nakonec se zobrazí zpráva, že vaše společnost nebo škola zaregistruje vaše zařízení.

6. Pokud vaše organizace vyžaduje, abyste si nastavili PIN kód pro Windows Hello, budete vyzváni k zadání ověřovacího kódu. Zadejte kód a pokračujte podle pokynů na obrazovce a vytvořte PIN kód.  

7. Na stránce **, kterou jste nastavili!** vyberte **Hotovo**. Právě jste svoje zařízení zaregistrovali.  

8. Pokud chcete dvakrát ověřit připojení, přejděte zpátky na **Nastavení**  >  **účty**  >  **přístup do práce nebo do školy**.  Váš účet by se teď měl zobrazit v seznamu.  


    ![Ověření, zda bylo připojení správně nastaveno](./media/w10-enroll-rs1-validate-successful-enrollment.png)  

Stále nemáte přístup k pracovním nebo školním e-mailům, souborům nebo jiným datům? Naučte se [řešit potíže s účty](troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school).  

## <a name="enroll-windows-10-version-1511-and-earlier-device"></a>Registrace zařízení s Windows 10 verze 1511 a starší  
Tento postup popisuje, jak zaregistrovat zařízení, které běží ve Windows 10 verze 1511 a starší.  

1. Přejděte na **Start**. Pokud jste na zařízení s Windows 10 Mobile, pokračujte na seznam **všechny aplikace** .

2. Otevřete aplikaci **Nastavení**. Pokud aplikace není v seznamu aplikací snadno dostupná, otevřete panel hledání a zadejte "nastavení".

3. Vyberte **účty**  >  , které**váš účet máte**.  


    ![Vyberte svůj účet.](./media/W10-enroll-2-accounts-your-account.png)  

5. Vyberte **Přidat pracovní nebo školní účet**.  


    ![Vyberte možnost přidat pracovní nebo školní účet.](./media/w10-enroll-3-add-work-school-acct.png)  

6. Přihlaste se pomocí přihlašovacích údajů svého pracovního nebo školního účtu.  


    ![Přihlášení](./media/W10-enroll-4-sign-in.png)  

Stále nemáte přístup k pracovním nebo školním e-mailům, souborům nebo jiným datům? Naučte se [řešit problémy související s účtem](troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-your-account) během registrace.  

## <a name="it-administrator-support"></a>Podpora správce IT   

Pokud jste správcem IT a máte potíže s registrací zařízení, přečtěte si téma řešení potíží s registrací [zařízení s Windows v Microsoft Intune](https://support.microsoft.com/help/4469913). V tomto článku jsou uvedené běžné chyby, jejich příčiny a kroky, jak je vyřešit. 

## <a name="next-steps"></a>Další kroky  
Pokud potřebujete pomoc s Portál společnosti nebo registrací, obraťte se na tým podpory pro IT organizace. Kontaktní údaje najdete na [webu portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980). Přihlaste se k webu pomocí svého pracovního nebo školního účtu.  

 

