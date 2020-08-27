---
title: Použití certifikačních autorit (CA) třetích stran s SCEP v Microsoft Intune – Azure | Microsoft Docs
description: V Microsoft Intune můžete přidat dodavatele nebo certifikační autoritu (CA) třetí strany pro vydávání certifikátů do mobilních zařízení pomocí protokolu SCEP. V tomto přehledu poskytuje aplikace Azure Active Directory (Azure AD) službě Microsoft Intune oprávnění k ověření certifikátů. Potom při instalaci serveru SCEP k vystavování certifikátů použijete ID aplikace, ověřovací klíč a ID tenanta aplikace AAD.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8cb847410bf04b4d7d8132e2069b6ced1751b921
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913575"
---
# <a name="add-partner-certification-authority-in-intune-using-scep"></a>Přidání partnerské certifikační autority pomocí protokolu SCEP do Intune

Použijte certifikační autority (CA) třetích stran s Intune. CA třetích stran můžou zřídit mobilní zařízení s novými nebo obnovenými certifikáty pomocí Simple Certificate Enrollment Protocol (SCEP) a můžou podporovat zařízení s Windows, iOS/iPadOS, Androidem a macOS.

K použití této funkce potřebujete dvě věci: open-source rozhraní API a úlohy správce Intune.

**Část 1 – použití open-source rozhraní API**  
Microsoft vytvořil rozhraní API pro integraci s Intune. I když rozhraní API můžete ověřovat certifikáty, odesílat oznámení o úspěšnosti nebo neúspěchu a k komunikaci s Intune používat protokol SSL, konkrétně objekt pro vytváření soketů SSL.

Rozhraní API je k dispozici ke stažení z [veřejného úložiště GitHub rozhraní Intune SCEP API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation), abyste ho mohli použít ve svých řešeních. Pomocí tohoto rozhraní API se servery SCEP třetích stran spustíte vlastní ověřování výzvou proti Intune před tím, než SCEP zřídí certifikát pro zařízení.

Článek o [integraci s řešením pro správu Intune SCEP](scep-libraries-apis.md) obsahuje další podrobnosti o použití tohoto rozhraní API, jeho metodách a testování sestaveného řešení.

**Část 2 – Vytvoření aplikace a profilu**  
Pomocí aplikace Azure Active Directory (Azure AD) můžete delegovat práva, aby služba Intune zpracovávala žádosti protokolu SCEP přicházející ze zařízení. Aplikace Azure AD obsahuje hodnoty ID aplikace a ověřovacího klíče, které se používají v rámci řešení rozhraní API vytvořeného vývojářem. Správci pak vytvoří a nasadí profily certifikátů SCEP pomocí Intune a můžou si zobrazit sestavy o stavu nasazení na zařízeních.

Tento článek poskytuje přehled této funkce z pohledu správce, včetně vytvoření aplikace Azure AD.

## <a name="overview"></a>Přehled

Následující kroky poskytují přehled použití protokolu SCEP pro certifikáty v Intune:

1. Správce v Intune vytvoří profil certifikátu SCEP a potom profil cílí na uživatele nebo zařízení.
2. Zařízení se vrátí se změnami do Intune.
3. Intune vytvoří jedinečnou výzvu SCEP. Zároveň přidá dodatečné informace o kontrole integrity, jako je například očekávaný předmět a alternativní název subjektu.
4. Intune výzvu i informace o kontrole integrity zašifruje a podepíše a pak je odešle do zařízení s požadavkem SCEP.
5. Zařízení vygeneruje žádost o podepsání certifikátu (CSR) a na základě profilu certifikátu SCEP odeslaného z Intune vygeneruje pár veřejného a privátního klíče.
6. Žádost o podepsání certifikátu a zašifrovaná a podepsaná výzva se odešlou koncovému bodu externího serveru SCEP.
7. Server SCEP odešle žádost o podepsání certifikátu a výzvu do Intune. Intune pak podpis ověří, dešifruje datovou část a porovná žádost o podepsání certifikátu s informacemi o kontrole integrity.
8. Intune odešle zpět serveru SCEP odpověď a uvede, zda ověření výzvy proběhlo úspěšně, nebo ne.  
9. Pokud se výzva úspěšně ověřila, pak server SCEP vydá zařízení certifikát.

Následující diagram znázorňuje podrobný tok integrace externího serveru SCEP s Intune:

> [!div class="mx-imgBorder"]
> ![Způsob integrace externí certifikační autority SCEP s Microsoft Intune](./media/certificate-authority-add-scep-overview/scep-certificate-vendor-integration.png)

## <a name="set-up-third-party-ca-integration"></a>Nastavení integrace externí certifikační autority

### <a name="validate-third-party-certification-authority"></a>Ověření externí certifikační autority

Před provedení integrace externích certifikačních autorit s Intune zkontrolujte, že vybraná certifikační autorita podporuje Intune. Zde je seznam [partnerů externí certifikační autority](#third-party-certification-authority-partners) (v tomto článku). Další informace můžete také získat z pokynů vaší certifikační autority. Certifikační autorita může obsahovat specifické instalační pokyny pro implementaci.

### <a name="authorize-communication-between-ca-and-intune"></a>Autorizace komunikace mezi certifikační autoritou a Intune

Pokud chcete externímu serveru SCEP povolit spuštění vlastního ověření výzvy pomocí Intune, vytvořte aplikaci ve službě Azure AD. Tato aplikace poskytne Intune delegovaná práva k ověřování žádostí protokolu SCEP.

Ujistěte se, že máte k registraci aplikace Azure AD potřebná oprávnění. Viz [požadovaná oprávnění](/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions)v dokumentaci k Azure AD.

#### <a name="create-an-application-in-azure-active-directory"></a>Vytvoření aplikace v Azure Active Directory  

1. V [Azure Portal](https://portal.azure.com)klikněte na registrace **Azure Active Directory**  >  **aplikace**a pak vyberte **Nová registrace**.  

2. Na stránce **zaregistrovat aplikaci** zadejte následující podrobnosti:  
   - V části **název** zadejte smysluplný název aplikace.  
   - V části **podporované typy účtů** vyberte **účty v libovolném organizačním adresáři**.  
   - Pro **identifikátor URI přesměrování**ponechte výchozí nastavení web a potom zadejte adresu URL pro přihlášení k serveru SCEP třetí strany.  

3. Vyberte **Registrovat** , chcete-li vytvořit aplikaci a otevřít stránku Přehled pro novou aplikaci.  

4. Na stránce **Přehled** aplikace ZKOPÍRUJTE hodnotu **ID aplikace (klienta)** a zaznamenejte ji pro pozdější použití. Tuto hodnotu budete potřebovat později.  

5. V navigačním podokně pro aplikaci přejdete na **certifikáty & tajných** kódů v části **Spravovat**. Vyberte tlačítko **nový tajný klíč klienta** . Zadejte hodnotu v popisu, vyberte libovolnou možnost pro **vypršení platnosti**a pak zvolte **Přidat** , aby se vygenerovala *hodnota* pro tajný klíč klienta. 
   > [!IMPORTANT]  
   > Než tuto stránku opustíte, zkopírujte hodnotu pro tajný klíč klienta a zaznamenejte ho pro pozdější použití s implementací CA třetí strany. Tato hodnota se znovu nezobrazí. Nezapomeňte si projít doprovodné materiály k vaší certifikační autoritě od třetí strany, jak si přeje nakonfigurovat ID aplikace, ověřovací klíč a ID tenanta.  

6. Poznamenejte si **ID tenanta**. ID tenanta je text domény za znakem @ při přihlašování k účtu. Pokud je váš účet například *admin@name.onmicrosoft.com* , vaše ID tenanta je **Name.onmicrosoft.com**.  

7. V navigačním podokně aplikace otevřete v nabídce **Spravovat** **oprávnění rozhraní API** a pak vyberte **Přidat oprávnění**.  

8. Na stránce **požádat o oprávnění API** vyberte **Intune**a pak vyberte **oprávnění aplikace**. Zaškrtněte políčko pro **scep_challenge_provider** (ověření výzvou SCEP).  

   Pokud chcete tuto konfiguraci uložit, vyberte **Přidat oprávnění** .  

9. Zůstat na stránce **oprávnění rozhraní API** a vyberte možnost **udělit souhlas správce pro Microsoft**a potom vyberte **Ano**.  
   
   Proces registrace aplikace v Azure AD je dokončený.

### <a name="configure-and-deploy-a-scep-certificate-profile"></a>Konfigurace a nasazení profilu certifikátu SCEP
Vytvořte jako správce profil certifikátu SCEP, který bude cílit na uživatele nebo zařízení. Pak profil přiřaďte.

- [Vytvoření profilu certifikátu SCEP](certificates-profile-scep.md#create-a-scep-certificate-profile)

- [Přiřazení profilu certifikátu](certificates-profile-scep.md#assign-the-certificate-profile)

## <a name="removing-certificates"></a>Odebrání certifikátů

Po zrušení registrace nebo vymazání zařízení se certifikáty odeberou. Certifikátů se neodvolávají.

## <a name="third-party-certification-authority-partners"></a>Partneři externí certifikační autority
Následující externí certifikační autority podporují Intune:

- [DigiCert](https://knowledge.digicert.com/tutorials/microsoft-intune.html)
- [EJBCA](https://doc.primekey.com/ejbca/ejbca-integration/integrating-with-third-party-applications/microsoft-intune-device-certificate-enrollment)
- [Entrust Datacard](https://go.entrustdatacard.com/pki/intune/)
- [EverTrust](https://evertrust.fr/en/products/)
- [GlobalSign](https://downloads.globalsign.com/acton/attachment/2674/f-6903f60b-9111-432d-b283-77823cc65500/1/-/-/-/-/globalsign-aeg-microsoft-intune-integration-guide.pdf)
- [IDnomic](https://www.idnomic.com/)
- [SCEPman](https://azuremarketplace.microsoft.com/marketplace/apps/gluckkanja.scepman)
- [Sectigo](https://sectigo.com/products)
- [Venafi](https://www.venafi.com/platform/enterprise-mobility)


Pokud jste externí certifikační autoritou a máte zájem o integraci svého produktu s Intune, projděte si pokyny rozhraní API:

- [Úložiště GitHub rozhraní Intune SCEP API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Pokyny pro externí certifikační autority k rozhraní Intune SCEP API](scep-libraries-apis.md)

## <a name="see-also"></a>Viz také

- [Konfigurace profilů certifikátů](certificates-scep-configure.md)
- [Úložiště GitHub rozhraní Intune SCEP API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Pokyny pro externí certifikační autority k rozhraní Intune SCEP API](scep-libraries-apis.md)