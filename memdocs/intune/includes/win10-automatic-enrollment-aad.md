## <a name="enable-windows-10-automatic-enrollment"></a>Povolení automatické registrace pro Windows 10

Automatická registrace umožňuje uživatelům, aby si svoje zařízení s Windows 10 zaregistrovali v Intune. Při registraci si uživatelé přidají pracovní účet do svého vlastního zařízení nebo připojí zařízení, která patří společnosti, ke službě Azure Active Directory. Na pozadí se zařízení zaregistruje a připojí ke službě Azure Active Directory. Po registraci je zařízení spravováno přes Intune.

**Požadavky**

- Předplatné Azure Active Directory Premium ([zkušební předplatné](https://go.microsoft.com/fwlink/?LinkID=816845))
- Odběr služby Microsoft Intune

### <a name="configure-automatic-mdm-enrollment"></a>Konfigurace automatického zápisu MDM

1. Přihlaste se k [portálu Azure Portal](https://portal.azure.com) a vyberte **Azure Active Directory**.

   ![Snímek obrazovky portálu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Vyberte **Mobilita (MDM a MAM)** .

   ![Snímek obrazovky portálu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Vyberte **Microsoft Intune**.

   ![Snímek obrazovky portálu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. Konfigurujte **Obor uživatele MDM**. Zadejte, která uživatelská zařízení by měla být spravována přes službu Microsoft Intune. Tato zařízení s Windows 10 se mohou automaticky zaregistrovat pro správu přes Microsoft Intune.

   - **Žádná** – automatická registrace MDM je zakázaná.
   - **Některá** – vyberte **Skupiny**, které můžou automaticky zaregistrovat svá zařízení s Windows 10.
   - **Všechna** – všichni uživatelé můžou automaticky zaregistrovat svá zařízení s Windows 10.

      > [!IMPORTANT]
      > U zařízení BYOD má přednost obor uživatele MAM, pokud jsou povolené obory uživatelů MAM i obor uživatele MDM (Automatická registrace MDM) pro všechny uživatele (nebo stejné skupiny uživatelů). Zařízení bude používat zásady Windows Information Protection (nedokončené výroby) (Pokud je nakonfigurujete) místo registrace MDM.
      >
      > U podnikových zařízení má obor uživatele MDM přednost, pokud je povolený oba obory. Zařízení zaregistrovaná v MDM.

   > [!NOTE]
   > Obor uživatele MDM musí být nastavený na skupinu Azure AD, která obsahuje uživatelské objekty.

   ![Snímek obrazovky portálu Azure Portal](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Použijte výchozí hodnoty pro následující adresy URL:
    - **Adresa URL podmínek použití MDM**
    - **Adresa URL zjišťování MDM**
    - **Adresa URL s předpisy služby MDM**

6. Vyberte **Uložit**.

Ve výchozím nastavení není pro službu povolené dvoufaktorové ověřování. Při registraci zařízení ale dvoufaktorové ověřování doporučujeme. Pokud chcete povolit dvoufaktorové ověřování, nakonfigurujte v Azure AD zprostředkovatele dvoufaktorového ověřování a u uživatelských účtů nakonfigurujte vícefaktorové ověřování. Informace najdete v článku [Začínáme s Azure Multi-Factor Authentication Serverem](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).
