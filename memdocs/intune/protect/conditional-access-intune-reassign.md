---
title: Migrace podmíněného přístupu do Azure Portal
titleSuffix: Microsoft Intune
description: Znovu přiřaďte zásady podmíněného přístupu, které jste dříve vytvořili v klasickém portálu Intune, na Azure Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/02/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 301159ad-5f7e-4fcc-86c7-f72a71701ff4
ms.reviewer: chrisgree
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa5593486f51d28c33ed280c97f819426be60fa2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911314"
---
# <a name="reassign-conditional-access-policies-from-intune-classic-portal-to-the-azure-portal"></a>Změna přiřazení zásad podmíněného přístupu z klasického portálu Intune na Azure Portal

Počínaje novým Azure Portal poskytuje podmíněný přístup podporu více zásad pro jednotlivé aplikace, společně s větší úpravou. Pokud jste dříve vytvořili zásady podmíněného přístupu na klasickém portálu Intune, můžete je migrovat do Azure Portal. 

## <a name="before-you-begin"></a>Než začnete

Pokud jste připraveni přejít na Azure Portal, postupujte podle kroků v tomto tématu a znovu přiřaďte zásady podmíněného přístupu, které jste dříve vytvořili v klasickém portálu Intune:

- Shromážděte zásady podmíněného přístupu, které jste dříve vytvořili, abyste věděli, jaká nastavení budete později potřebovat znovu přiřadit.

- Podle pokynů v tomto tématu můžete tyto zásady znovu vytvořit na portálu Azure Portal.

- Až si ověříte, že nové zásady na Azure Portalu fungují podle očekávání, zakažte podmíněné zásady na klasickém portálu Intune.
<br /><br />
  - **Než zakážete** zásady podmíněného přístupu na klasickém portálu Intune, naplánujte, jak přesunete uživatele na nové zásady. Existují dvě metody:
<br /><br />
    - **Použít stejnou skupinu pro zahrnutí, na kterou použijete zásady vytvořené na portálu Azure Portal, a vytvořit novou skupinu pro vyloučení, na kterou použijete zásady z klasického portálu Intune**.
      - Postupně některé uživatele přesunete do skupiny pro vyloučení v klasickém portálu. Tím zabráníte, aby se použily zásady, na které cílí klasický portál Intune. Zásady vytvořené pro stejnou skupinu uživatelů na portálu Azure, na kterou jsou i zacílené, se použijí společně s těmi v klasickém portálu Intune. 
<br /><br />
    - **Vytvořte novou skupinu, do které se budou cílit zásady podmíněného přístupu v Azure Portal**. Pokud zvolíte tuto metodu, budete muset provést následující:
      - Postupně Odeberte uživatele ze skupin zabezpečení, na kterých jsou zacíleny zásady podmíněného přístupu na klasickém portálu Intune.
      - Až ověříte, že nové zásady u těchto uživatelů fungují, můžete zásady v klasickém portálu Intune vypnout. 
<br /><br />
- Pokud máte nastavení zásad podmíněného přístupu nakonfigurovaná tak, aby na klasickém portálu Intune používala Exchange ActiveSync (EAS), přečtěte si [pokyny v tomto tématu](#reassign-intune-device-based-conditional-access-policies-for-eas-clients) , abyste změnili **přiřazení nastavení zásad podmíněného přístupu EAS v Azure Portal**.

### <a name="to-verify-your-device-based-conditional-access-policies-in-the-intune-classic-portal"></a>Ověření zásad podmíněného přístupu na základě zařízení v klasickém portálu Intune

1. Přejděte na [klasický portál Intune](https://manage.microsoft.com) a přihlaste se pomocí svých přihlašovacích údajů.

2. Zvolte z levé nabídky možnost **Zásady**.

3. Zvolte **podmíněný přístup**a pak vyberte cloudovou službu Microsoftu (třeba Exchange Online nebo SharePoint Online), pro kterou jste vytvořili zásadu podmíněného přístupu.

4. Poznamenejte si nastavení podmíněného přístupu a podívejte se na ně při vytváření stejných zásad podmíněného přístupu v Azure Portal.

### <a name="app-and-device-based-conditional-access-policies-working-together"></a>Společné fungování zásad podmíněného přístupu podle aplikací a zařízení

Okno **Intune App Protection** na portálu Azure Portal umožňuje správcům nastavit podmíněná pravidla podle aplikací tak, aby přístup k firemním prostředkům mohly získat jenom aplikace podporující zásady ochrany aplikací Intune. Tyto zásady podmíněného přístupu na základě aplikace můžete překrývat pomocí zásad podmíněného přístupu na základě zařízení. Podmíněné zásady podle zařízení a aplikací můžete zkombinovat (logický operátor A) nebo poskytnout jednu z možností (logický operátor NEBO). Pokud jsou požadavky zásad podmíněného přístupu následující:

- Vyžadovat vyhovující zařízení **A** použít schválenou aplikaci
  - Zásady podmíněného přístupu byste měli nastavit pomocí okna [Azure Active Directory podmíněný přístup](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) a v okně [Intune App Protection](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0).
<br /><br />
- Vyžadovat vyhovující zařízení **NEBO** použít schválenou aplikaci
  - Zásady podmíněného přístupu byste měli nastavit pomocí [klasického portálu Intune](https://manage.microsoft.com) a okna [Intune App Protection](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0).

> [!TIP] 
> Toto téma obsahuje snímky obrazovky srovnávající činnosti koncového uživatele na klasickém portálu Intune i na portálu Azure Portal.

## <a name="reassign-intune-device-based-conditional-access-policies"></a>Změna přiřazení zásad podmíněného přístupu na základě zařízení v Intune

1. Přejděte na [podmíněný přístup v Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)a přihlaste se pomocí svých přihlašovacích údajů.

2. Zvolte **Nové zásady**.

3. Zadejte název pro tuto zásadu.

4. V **části přiřazení**vyberte **Uživatelé a skupiny** , pro které chcete cílit na nové zásady podmíněného přístupu.

    ![Obrázek, který porovnává uživatelské rozhraní skupiny uživatelů mezi Intune a portály Azure](./media/conditional-access-intune-reassign/reassign-ca-1.png)

    > [!IMPORTANT] 
    > Výběr, který provedete pro portál Azure Portal, musí odpovídat výběru, který jste provedli pro portál Classic. Pokud máte třeba na klasickém portálu Intune vybrané všechny uživatele, vyberte **Všichni uživatelé** na portálu Azure Portal. Kromě toho, pokud jste na klasickém portálu Intune zvolili možnost **Vyloučené skupiny** , vylučte také tyto vybrané skupiny v Azure Portal.

5. Jakmile svou skupinu zvolíte, klikněte na **Vybrat** a pak na **Hotovo**.

6. V části **Přiřazení** zvolte **Cloudové aplikace**.

7. V okně **Cloudové aplikace** zvolte **Vybrat aplikace**.

8. Zvolte aplikaci, na kterou chcete nové zásady podmíněného přístupu použít, a klikněte na **Vybrat**.

9. Klikněte na **Hotovo**.

    ![Obrázek porovnání uživatelského rozhraní cloudové aplikace mezi službami Intune a portály Azure](./media/conditional-access-intune-reassign/reassign-ca-3.png)

    > [!TIP] 
    > Pokud máte více aplikací se stejnými zásadami, můžete zvážit jejich sloučení na portálu Azure Portal do jedné zásady.

10. V části **Přiřazení** zvolte **Podmínky**.

11. V okně **Podmínky** zvolte **Platformy zařízení** a pak vyberte příslušné platformy zařízení.

12. Až budete s výběrem platforem zařízení hotoví, dvakrát klikněte na **Hotovo**.

    ![Obrázek, který porovnává uživatelské rozhraní platformy zařízení na portálech Intune a Azure Portal](./media/conditional-access-intune-reassign/reassign-ca-4.png)

    > [!TIP] 
    > Pokud jste vybrali jednotlivé platformy na klasickém portálu Intune, vyberte jednotlivé platformy i na portálu Azure Portal.

    > [!NOTE] 
    > Připojení k doméně a možnosti vyhovění předpisům pro Windows můžete specifikovat později.

13. V části **Přiřazení** zvolte **Podmínky**.

14. V okně **Podmínky** zvolte **Klientské aplikace** a pak vyberte příslušné klientské aplikace.

15. Až budete s výběrem klientských aplikací hotoví, dvakrát klikněte na **Hotovo**.

    ![Obrázek, který porovnává uživatelské rozhraní klientských aplikací mezi Intune a portály Azure](./media/conditional-access-intune-reassign/reassign-ca-6.png)

16. Pokud jste na klasickém portálu Intune zvolili nastavení prohlížeče, vyberte na portálu Azure Portal **Prohlížeč** i **Mobilní aplikace a desktopoví klienti**. V případě, že jste na klasickém portálu Intune nastavení prohlížeče nezvolili, vyberte jenom **Mobilní aplikace a desktopoví klienti**. 

17. V části **Ovládací prvky přístupu** zvolte **Udělení**.

18. V části **Udělení ovládacích prvků přístupu** zvolte **Vyžadovat, aby zařízení bylo označené jako vyhovující** a pak klikněte na **Vybrat**.

19. Pokud máte zásadu, která vyžaduje zařízení s Windows připojená k doméně, a zároveň chcete povolit zařízení s Windows zaregistrovaná v Intune a vyhovující, zvolte **Vyžadovat zařízení připojené k doméně**, **Vyžadovat, aby zařízení bylo označené jako vyhovující** a **Vyžadovat jeden z vybraných ovládacích prvků**.

20. Pokud zařízení s Windows zaregistrovaná v Intune a vyhovující nepovolujete, vylučte zásadu pro Windows z aktuální zásady. Pak vytvořte samostatnou zásadu s **Platformou zařízení** nastavenou na **Windows**, zahrňte další výše uvedené podmínky a v části pro **Udělení ovládacích prvků přístupu** zvolte **Vyžadovat zařízení připojené k doméně**.

21. V okně **Nová** zásada podmíněného přístupu zapněte přepínač **Povolit zásadu** a pak klikněte na **vytvořit**.

    ![Porovnání povolení uživatelského rozhraní zásad podmíněného přístupu mezi Intune a Azure](./media/conditional-access-intune-reassign/reassign-ca-11.png)

## <a name="reassign-intune-device-based-conditional-access-policies-for-eas-clients"></a>Změna přiřazení zásad podmíněného přístupu na základě zařízení v Intune pro klienty EAS

Pokud jste nakonfigurovali nastavení Exchange ActiveSync jako součást zásady Exchange Online na klasickém portálu Intune, musíte v Azure Portal vytvořit druhou zásadu podmíněného přístupu.

1. Přejděte na [podmíněný přístup v Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)a přihlaste se pomocí svých přihlašovacích údajů.

2. Zvolte **Nové zásady**.

3. Zadejte název pro tuto zásadu.

4. V části **přiřazení** vyberte **Uživatelé a skupiny** , pro které chcete cílit na nové zásady podmíněného přístupu.

    ![Obrázek znázorňující porovnání uživatelského rozhraní skupiny uživatelů mezi portály Azure a portály Intune](./media/conditional-access-intune-reassign/reassign-ca-12.png)

    > [!IMPORTANT] 
    > Výběr, který provedete pro Azure Portal, musí odpovídat výběru, který jste provedli pro Azure Portal. Pokud máte třeba na klasickém portálu Intune vybrané všechny uživatele, vyberte **Všichni uživatelé** na portálu Azure Portal. Kromě toho, pokud jste na klasickém portálu Intune zvolili možnost **Vyloučené skupiny** , vylučte také tyto vybrané skupiny v Azure Portal.

5. Jakmile svou skupinu zvolíte, klikněte na **Vybrat** a pak na **Hotovo**.

6. V části **Přiřazení** zvolte **Cloudové aplikace**.

7. V okně **Cloudové aplikace** klikněte na **Vybrat aplikace** a zvolte **Exchange Online**. Pak klikněte na **Vybrat** a **Hotovo**.

    ![Obrázek srovnání uživatelského rozhraní cloudových aplikací mezi Intune a portály Azure](./media/conditional-access-intune-reassign/reassign-ca-14.png)

    > [!IMPORTANT] 
    > Zásady podmíněného přístupu pro klienty EAS nemohou zahrnovat žádnou další cloudovou aplikaci.

8. V okně **Podmínky** zvolte **Klientské aplikace** a pak vyberte příslušné klientské aplikace. Pokud jste se rozhodli blokovat klienty, kteří nejsou podporováni službou Intune, použijte možnost **použít zásadu pouze pro podporované platformy** .

    ![Obrázek znázorňující porovnání uživatelského rozhraní klientských aplikací mezi portály Azure a portály Intune](./media/conditional-access-intune-reassign/reassign-ca-15.png)

9. Až budete s výběrem klientských aplikací hotoví, dvakrát klikněte na **Hotovo**.

10. V části **Ovládací prvky přístupu** zvolte **Udělení**.

11. V části **Udělení ovládacích prvků přístupu** zvolte **Vyžadovat, aby zařízení bylo označené jako vyhovující** a pak klikněte na **Vybrat**.

    ![Obrázek, který porovnává uživatelské rozhraní pro udělení přístupu mezi Intune a portály Azure](./media/conditional-access-intune-reassign/reassign-ca-16.png)

12. V okně **Nová** zásada podmíněného přístupu zapněte přepínač **Povolit zásadu** a pak klikněte na **vytvořit**.

    ![Porovnání povolení uživatelského rozhraní zásad podmíněného přístupu mezi Intune a Azure](./media/conditional-access-intune-reassign/reassign-ca-17.png)

> [!NOTE]
> Pokud nakonfigurujete možnost **Platformy zařízení**, uložení zásad se nezdaří a zobrazí se chyba „Konfigurace zásad není podporovaná“. Exchange ActiveSync nemůže identifikovat platformu, kterou používá připojující se zařízení. Při vytváření zásad pro zařízení Exchange ActiveSync se proto konfigurace specifických platforem zařízení nepodporuje.

## <a name="disable-conditional-access-policies-in-the-intune-classic-portal"></a>Vypnutí zásad podmíněného přístupu na klasickém portálu Intune

Po přeřadíte zásady podmíněného přístupu v Azure Portal je důležité postupně zakázat zásady podmíněného přístupu, které jste dříve vytvořili v klasickém portálu Intune. Kromě toho může být potřeba použít stejnou skupinu zabezpečení k uplatnění zásad podmíněného přístupu vytvořených v Azure Portal.

> [!NOTE]
> Než zakážete zásady podmíněného přístupu na klasickém portálu Intune, přečtěte si část [než začnete](#before-you-begin) na začátku tohoto tématu.

### <a name="to-disable-the-conditional-access-policies"></a>Zakázání zásad podmíněného přístupu

Vzhledem k tomu, že MDM byla odebrána z klasického portálu Intune, byl k dispozici následující odkaz pro zobrazení nebo zakázání těchto klasických zásad:

[https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies](https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies)

## <a name="see-also"></a>Viz také

- [Běžné způsoby použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md)
- [Podmíněný přístup na základě aplikace s Intune](app-based-conditional-access-intune.md)
- [Podmíněný přístup v Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)