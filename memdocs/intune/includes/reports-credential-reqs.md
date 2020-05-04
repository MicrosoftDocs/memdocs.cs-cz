<!-- This include is part of the Intune Data Warehouse documentation. -->

## <a name="azure-ad-and-intune-credential-requirements"></a>Požadavky na přihlašovací údaje pro Azure AD a Intune

Ověřování a autorizace jsou založené na přihlašovacích údajích Azure AD a řízení přístupu na základě role (RBAC) Intune. Ve výchozím nastavení mají všichni globální správci a správci služby Intune pro vašeho tenanta přístup k datovému skladu. Použijte role Intune k poskytnutí přístupu pro další uživatele tak, že jim udělíte přístup k prostředku **datového skladu Intune** .

Požadavky pro přístup k datovému skladu Intune (včetně rozhraní API) jsou:

- Uživatel musí být jedním z těchto uživatelů:
  - Globální správce Azure AD
  - Správce služby Intune
  - Uživatel s přístupem na základě role k prostředku **Datový sklad Intune**
  - Ověření bez účasti uživatele pomocí [ověřování pouze na úrovni aplikace](../developer/data-warehouse-app-only-auth.md) 
