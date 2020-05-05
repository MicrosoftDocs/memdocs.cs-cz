## <a name="enable-windows-10-automatic-enrollment"></a>Povolení automatické registrace pro Windows 10

Automatická registrace umožňuje uživatelům, aby si svoje zařízení s Windows 10 zaregistrovali v Intune. Při registraci si uživatelé přidají pracovní účet do svého vlastního zařízení nebo připojí zařízení, která patří společnosti, ke službě Azure Active Directory. Na pozadí se zařízení zaregistruje a připojí ke službě Azure Active Directory. Po registraci je zařízení spravováno přes Intune.

**Požadavky**

- Předplatné Azure Active Directory Premium ([zkušební předplatné](https://go.microsoft.com/fwlink/?LinkID=816845))
- Odběr služby Microsoft Intune

### <a name="configure-automatic-mdm-enrollment"></a>Konfigurace automatického zápisu MDM

1. Přihlaste se k [portálu Azure Portal](https://portal.azure.com) a vyberte **Azure Active Directory**.

   ![Snímek obrazovky webu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Vyberte **Mobilita (MDM a MAM)**.

   ![Snímek obrazovky webu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Vyberte **Microsoft Intune**.

   ![Snímek obrazovky webu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. Konfigurujte **Obor uživatele MDM**. Zadejte, která uživatelská zařízení by měla být spravovaná pomocí Microsoft Intune. Tato zařízení s Windows 10 se mohou automaticky zaregistrovat pro správu přes Microsoft Intune.

   - **Žádná** – automatická registrace MDM je zakázaná.
   - **Některá** – vyberte **Skupiny**, které můžou automaticky zaregistrovat svá zařízení s Windows 10.
   - **Všechna** – všichni uživatelé můžou automaticky zaregistrovat svá zařízení s Windows 10.

      > [!IMPORTANT]
      > Pro zařízení s Windows BYOD má obor uživatele MAM přednost, pokud jsou povolené obory uživatele MAM i obor uživatele MDM (Automatická registrace MDM) pro všechny uživatele (nebo stejné skupiny uživatelů). Zařízení nebude zaregistrované v MDM a zásady Windows Information Protection (nedokončené výroby) se použijí, pokud je nakonfigurujete.
      >
      > Pokud je vaším záměrem povolit automatickou registraci zařízení s Windows BYOD do MDM: Nakonfigurujte obor uživatele MDM na **All** (nebo **některé**a určete skupinu) a nakonfigurujte mam uživatelský rozsah na **none** (nebo **nějaký**a určete skupinu – zajistěte, aby uživatelé nejsou členy skupiny, které cílí na obory uživatelů MDM i mam).
      >
      >U [podnikových zařízení](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices)má obor uživatele MDM přednost, pokud jsou povolené obory uživatelů MDM i mam. Zařízení se automaticky zaregistruje v nakonfigurované MDM.

   > [!NOTE]
   > Obor uživatele MDM musí být nastavený na skupinu Azure AD, která obsahuje uživatelské objekty.

   ![Snímek obrazovky webu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Použijte výchozí hodnoty pro následující adresy URL:
    - **Adresa URL podmínek použití MDM**
    - **Adresa URL zjišťování MDM**
    - **Adresa URL s předpisy služby MDM**

6. Vyberte **Uložit**.

Ve výchozím nastavení služby není povoleno dvoufaktorové ověřování. Dvoufaktorové ověřování ale doporučujeme při registraci zařízení. Pokud chcete povolit dvoufaktorové ověřování, nakonfigurujte v Azure AD zprostředkovatele dvoufaktorového ověřování a u uživatelských účtů nakonfigurujte vícefaktorové ověřování. Informace najdete v článku [Začínáme s Azure Multi-Factor Authentication Serverem](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).
