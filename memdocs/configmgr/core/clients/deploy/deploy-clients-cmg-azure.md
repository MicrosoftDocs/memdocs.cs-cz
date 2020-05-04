---
title: Instalace klienta se službou Azure AD
titleSuffix: Configuration Manager
description: Instalace a přiřazení klienta Configuration Manager v zařízeních s Windows 10 pomocí Azure Active Directory pro ověřování
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a55440e7ba61ec62d9f0c91c0a23b98bab5884c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713496"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalace a přiřazení Configuration Manager klientů s Windows 10, kteří používají Azure AD k ověřování

Pokud chcete nainstalovat klienta Configuration Manager na zařízeních s Windows 10 pomocí ověřování Azure AD, Integrujte Configuration Manager s Azure Active Directory (Azure AD). Klienti můžou být na intranetu, který komunikuje přímo s bodem správy s povoleným protokolem HTTPS nebo libovolným bodem správy v lokalitě s povoleným rozšířeným protokolem HTTP. Můžou se také jednat o internetovou komunikaci prostřednictvím CMG nebo k internetovému bodu správy. Tento proces pomocí Azure AD ověřuje klienty na Configuration Manager lokalitě. Azure AD nahrazuje nutnost konfigurovat a používat certifikáty pro ověřování klientů.

Nastavení Azure AD může být pro některé zákazníky snazší než nastavení infrastruktury veřejných klíčů pro ověřování založené na certifikátech. K dispozici jsou funkce, které vyžadují připojení lokality do služby Azure AD, ale nemusí nutně vyžadovat, aby klienti byli připojeni k Azure AD.<!-- SCCMDocs issue 1259 --> Další informace najdete v těchto článcích:

- [Plánování Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Použití Azure AD pro spolusprávu](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Před zahájením

- Tenant Azure AD je předpokladem  

- Požadavky na zařízení:  

  - Windows 10  

  - Připojeno k Azure AD, buď čistě cloudová doména připojená k doméně, nebo služba Azure AD – připojeno  

- Požadavky uživatele:  

  - Přihlášený uživatel musí být identita Azure AD.

  - Pokud je uživatel federované nebo synchronizovanou identitou, musíte použít Configuration Manager [zjišťování uživatelů služby Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) a taky [zjišťování uživatelů Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). Další informace o hybridních identitách najdete v tématu [definice strategie přijetí hybridní identity](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Kromě [stávajících požadavků](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) pro roli systému lokality bodu správy povolte také **ASP.NET 4,5** na tomto serveru. Zahrňte všechny další možnosti, které se automaticky vyberou při povolování ASP.NET 4,5.  

- Určete, jestli váš bod správy potřebuje HTTPS. Další informace najdete v tématu [Povolení bodu správy pro protokol HTTPS](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Volitelně můžete nastavit [bránu pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md) (CMG) pro nasazení internetových klientů. U místních klientů, kteří se ověřují pomocí Azure AD, nepotřebujete CMG.  

> [!TIP]
> Počínaje verzí 2002,<!--5686290--> Configuration Manager rozšiřuje podporu internetových zařízení, která se často nepřipojují k interní síti, nelze se připojit k Azure Active Directory (Azure AD) a nemusíte mít k dispozici metodu pro instalaci certifikátu vystaveného infrastrukturou veřejných klíčů. Další informace najdete v tématu [ověřování založené na tokenech pro CMG](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Konfigurace služeb Azure pro správu cloudu

Připojte svůj Configuration Manager web k Azure AD jako první krok. Podrobnosti o tomto procesu najdete v tématu [Konfigurace služeb Azure](../../servers/deploy/configure/azure-services-wizard.md). Umožňuje vytvořit připojení ke službě **Cloud Management** .

Povolte [zjišťování uživatelů Azure AD](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) jako součást připojování ke **správě cloudu**.

Po dokončení těchto akcí je vaše lokalita Configuration Manager připojená k Azure AD.

## <a name="configure-client-settings"></a>Konfigurace nastavení klientů

Tato nastavení klienta se můžou připojit k zařízením s Windows 10 pomocí Azure AD. Umožňují taky internetovým klientům používat CMG a cloudový distribuční bod.

1. Nakonfigurujte následující nastavení klienta v části **Cloud Services** s použitím informací v tématu [Konfigurace nastavení klienta](configure-client-settings.md).  

    - **Povolit přístup k distribučnímu bodu cloudu**: Povolením tohoto nastavení umožníte, aby zařízení s internetem získalo požadovaný obsah pro instalaci klienta Configuration Manager. Pokud není obsah dostupný v distribučním bodě cloudu, zařízení mohou načíst obsah z CMG. Nástroj Bootstrap instalace klienta opakuje distribuční bod cloudu po dobu čtyř hodin, než se vrátí k CMG.<!--495533-->  

    - **Automaticky registrovat nová zařízení s Windows 10 připojená k doméně pomocí Azure Active Directory**: nastavte na **Ano** nebo **ne**. Výchozí nastavení je **Ano**. Toto chování je zároveň výchozí ve Windows 10 verze 1709.

    - **Povolit klientům používat bránu pro správu cloudu**: nastavte na **Ano** (výchozí) nebo **ne**.  

2. Nasaďte nastavení klienta do požadované kolekce zařízení. Nesaďte tato nastavení do kolekcí uživatelů.

Pokud chcete potvrdit, že je zařízení připojené ke službě Azure `dsregcmd.exe /status` AD, spusťte příkaz v příkazovém řádku. Pokud je zařízení připojené k Azure AD, zobrazí se v poli **AzureAdjoined** ve výsledcích hodnota **Ano** .

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instalace a registrace klienta pomocí Azure AD identity

Pokud chcete klienta ručně nainstalovat pomocí Azure AD identity, nejdřív si přečtěte obecný postup [Ruční instalace klientů](deploy-clients-to-windows-computers.md#BKMK_Manual).

 > [!Note]  
 > Zařízení potřebuje přístup k Internetu, aby mohl kontaktovat službu Azure AD, ale nemusí být založené na internetu.

Následující příklad ukazuje obecnou strukturu příkazového řádku:`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Další informace najdete v tématu [vlastnosti instalace klienta](about-client-installation-properties.md).

Parametr **/MP** a vlastnost **CCMHOSTNAME** určují jednu z následujících možností v závislosti na scénáři:

- Místní bod správy. Zadejte pouze parametr **/MP** . Vlastnost **CCMHOSTNAME** se nevyžaduje.
- Brána pro správu cloudu
- Internetový bod správy

Vlastnost **SMSMP** Určuje buď místní, nebo internetový bod správy.

V tomto příkladu se používá brána pro správu cloudu. Nahrazuje ukázkové hodnoty:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Lokalita publikuje Další informace o službě Azure AD v bráně pro správu cloudu (CMG). Klient připojený ke službě Azure AD získá tyto informace z CMG během procesu CCMSetup pomocí stejného tenanta, ke kterému je připojený. Toto chování dále zjednodušuje instalaci klienta v prostředí s více než jedním klientem služby Azure AD. Jediným ze dvou požadovaných vlastností CCMSetup jsou **CCMHOSTNAME** a **SMSSiteCode**.<!--3607731-->

Pokud chcete automatizovat instalaci klienta pomocí identity Azure AD prostřednictvím Microsoft Intune, přečtěte si téma [Příprava internetových zařízení pro spolusprávu](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## <a name="next-steps"></a>Další kroky

Po dokončení můžete nadále [monitorovat a spravovat klienty](../manage/monitor-clients.md).
