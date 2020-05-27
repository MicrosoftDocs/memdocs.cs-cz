---
title: Správa aplikací VPP z Microsoft Store pro firmy
titleSuffix: Microsoft Intune
description: Přečtěte si, jak můžete synchronizovat aplikace v Intune z Microsoft Store pro firmy.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ed5d3f0-2749-45cd-b6bf-fd8c7c08bc1b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ed7852a5aaf09a99823035d12bf2aa9139c1c02
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990223"
---
# <a name="how-to-manage-volume-purchased-apps-from-the-microsoft-store-for-business-with-microsoft-intune"></a>Jak spravovat hromadně zakoupené aplikace z Microsoft Store pro firmy pomocí Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

[Microsoft Store pro firmy](https://www.microsoft.com/business-store) je místo, kde můžete najít a zakoupit aplikace pro svou organizaci, a to jednotlivě i hromadně. Pokud Store propojíte s Microsoft Intune, můžete hromadně zakoupené aplikace spravovat z Azure Portalu. Příklad:

* Seznam aplikací, které jste zakoupili (nebo které jsou zdarma) můžete synchronizovat z obchodu s Intune.
* Aplikace, které jsou synchronizované, se zobrazí v konzole pro správu Intune. Tyto aplikace můžete přiřadit stejně jako všechny ostatní aplikace.
* Licencované verze aplikací v režimu online i offline jsou synchronizovány do Intune. Názvy aplikací budou na portálu připojeny "online" nebo "offline".
* V konzole pro správu Intune můžete sledovat, kolik licencí je dostupných a kolik se jich právě používá.
* Pokud není dostupný dostatečný počet licencí, blokuje Intune přiřazení a instalaci aplikací.
* Aplikace spravované přes Microsoft Store pro firmy automaticky odvolají licence, když uživatel opustí podnik nebo když správce odebere uživatele a jeho zařízení.

## <a name="before-you-start"></a>Než začnete

Než začnete synchronizovat a přiřazovat aplikace z Microsoft Storu pro firmy, přečtěte si následující informace:

- Nakonfigurujte Intune jako autoritu správy mobilních zařízení pro svoji organizaci.
- Musíte mít zaregistrovaný účet v Microsoft Storu pro firmy.
- Až přidružíte účet ve Microsoft Storu pro firmy k Intune, už nebude možné tento účet změnit.
- Aplikace zakoupené ze Storu se nedají do služby Intune přidat ručně ani z ní ručně odebrat. Dají se jenom synchronizovat s Microsoft Storem pro firmy.
- Portál Intune synchronizuje aplikace s online i offline licencemi, které jste zakoupili v Microsoft Storu pro firmy. Tyto aplikace můžete nasadit pro skupiny zařízení nebo skupiny uživatelů.
- Instalace online aplikací se spravují ve Storu.
- V Intune se můžou synchronizovat také offline aplikace, které jsou bezplatné. Tyto aplikace instaluje Intune, nikoli Store.
- Aby bylo možné tuto funkci používat, musí být zařízení připojená k Active Directory Domain Services, připojenému k Azure AD nebo na pracovišti.
- Zaregistrovaná zařízení musí používat Windows 10 verze 1511 nebo novější.

> [!NOTE]
> Pokud zakážete úložiště na spravovaných zařízeních (ručně prostřednictvím zásad nebo Zásady skupiny), instalace licencovaných aplikací online se nezdaří.

## <a name="associate-your-microsoft-store-for-business-account-with-intune"></a>Přidružení účtu v Microsoft Storu pro firmy k Intune

Než povolíte synchronizaci v konzole služby Intune, musíte svůj účet ve Storu nakonfigurovat tak, aby používal Intune jako nástroj pro správu:

1. Ujistěte se, že se k [Microsoft Store pro firmy](https://www.microsoft.com/business-store) přihlašujete pomocí stejného účtu tenanta, který používáte k přihlášení do Intune.
2. V obchodě obchodu zvolte kartu **Spravovat** , vyberte **Nastavení**a klikněte na kartu **rozmístit** .
3. Pokud nebudete mít **Microsoft Intune** k dispozici jako nástroj pro správu mobilních zařízení, vyberte **Přidat Nástroj pro správu** a přidejte **Microsoft Intune**. Pokud nemáte **Microsoft Intune** aktivované jako nástroj pro správu mobilních zařízení, klikněte na tlačítko **aktivovat** vedle **Microsoft Intune**. Počítejte s tím, že byste měli aktivovat **Microsoft Intune** místo **registrace Microsoft Intune**.

> [!NOTE]
> Dřív bylo možné přidružit k Microsoft Storu pro firmy jenom jeden nástroj pro správu na přiřazování aplikací. Teď už jich můžete přidružit více, například Intune a Configuration Manager.

Teď můžete pokračovat a nastavit synchronizaci v konzole Intune.

## <a name="configure-synchronization"></a>Konfigurace synchronizace

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**  >  **Microsoft Store pro firmy**.
3. Klikněte na **Povolit**.
4. Pokud jste to ještě neudělali, klikněte na odkaz pro registraci Microsoft Storu pro firmy a podle předchozího postupu přidružte svůj účet.
5. V rozevíracím seznamu **Jazyk** vyberte jazyk, ve kterém se aplikace z Microsoft Storu pro firmy zobrazují na portálu Azure Portal. Bez ohledu na jazyk, ve kterém se budou zobrazovat, se nainstalují v jazyce koncového uživatele, pokud je dostupný.
6. Kliknutím na **Synchronizovat** přeneste aplikace zakoupené v Microsoft Storu do Intune.

## <a name="synchronize-apps"></a>Synchronizace aplikací

1. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**  >  **Microsoft Store pro firmy**.
2. Kliknutím na **Synchronizovat** přeneste aplikace zakoupené v Microsoft Storu do Intune.

> [!NOTE]
> Aplikace s šifrovanými balíčky aplikací se v současné době nepodporují a nebudou se synchronizovat s Intune.

## <a name="assign-apps"></a>Přiřazení aplikací

Aplikace ze Storu se přiřazují stejně jako jakékoli jiné aplikace Intune. Další informace najdete v článku [Jak přiřadit aplikace do skupin pomocí Microsoft Intune](apps-deploy.md).

Offline aplikace mohou být cílené na skupiny uživatelů, skupiny zařízení nebo skupiny s uživateli a zařízeními.
Offline aplikace se dají nainstalovat pro konkrétního uživatele na zařízení nebo pro všechny uživatele na zařízení.

Když přiřadíte aplikaci z Microsoft Storu pro firmy, využije licenci každý uživatel, který si ji nainstaluje. Když využijete všechny dostupné licence přiřazené aplikace, nebudete už moct přiřadit žádné další kopie. Proveďte jednu z následujících akcí:

* Odinstalovat aplikaci z některých zařízení.
* Omezit rozsah aktuálního přiřazení tak, aby jeho cílem byli jen uživatelé, pro které máte dost licencí.
* Zakoupit v Microsoft Storu pro firmy další kopie příslušné aplikace.

## <a name="remove-apps"></a>Odebrání aplikací

Pokud chcete odebrat aplikaci, která se synchronizuje s Microsoft Storem pro firmy, musíte se k Microsoft Storu pro firmy přihlásit a aplikaci vrátit. Proces je stejný, ať už je aplikace volná, nebo ne. V případě bezplatné aplikace bude obchod vracet $0. Následující příklad ukazuje refundaci bezplatné aplikace. 

![Snímek obrazovky s podrobnostmi o odebírané aplikaci](./media/windows-store-for-business/microsoft-store-for-business-01.png)

> [!NOTE]
> Odebrání viditelnosti aplikace v soukromém úložišti nezabrání v Intune synchronizaci aplikace. Abyste aplikaci mohli úplně odebrat, musíte ji vrátit.

## <a name="next-steps"></a>Další kroky

* [Správa multilicenčních aplikací a knih pomocí Microsoft Intune](vpp-apps.md)
