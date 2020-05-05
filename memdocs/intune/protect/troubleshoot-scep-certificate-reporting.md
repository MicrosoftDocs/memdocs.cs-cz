---
title: Řešení potíží s vytvářením sestav úspěšného nasazení certifikátů do zařízení při použití protokolu SCEP s Microsoft Intune | Microsoft Docs
description: Řešení potíží s vytvářením sestav pomocí NDES a konektoru pro Intune o úspěšném nasazení certifikátů, které se zřídily pomocí profilů certifikátů SCEP
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4b374d79d689e1ecad8124489fe5023378bd4f1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079072"
---
# <a name="troubleshoot-ndes-reporting-of-certificate-deployments-in-microsoft-intune"></a>Řešení potíží se sestavou nasazení certifikátů v Microsoft Intune

Pomocí následujících informací potvrďte, že NDES a Microsoft Intune Certificate Connector úspěšně hlásí Intune, že byl certifikát doručen do zařízení. Vytváření sestav do Intune je poslední fází použití profilů certifikátů SCEP ke zřízení zařízení s Windows pomocí certifikátu.

Tento článek se týká kroku 6 [komunikačního pracovního postupu SCEP](troubleshoot-scep-certificate-profiles.md).

## <a name="review-for-signs-of-successful-reporting"></a>Kontrola příznaků úspěšných sestav

Pokud bylo generování sestav úspěšné, najdete položky, které se podobají následujícím příkladům na serveru NDES:

- **Protokol IIS**:

  `fe80::f53d:89b8:c3e8:5fec%13 POST /CertificateRegistrationSvc/Certificate/Notify - 443 - fe80::f53d:89b8:c3e8:5fec%13 NDES_Plugin - 204 0 0 277 62`

- **Souboru NDESPlugin. log**:

  ```
  Calling Notifyrequest ...
  Sending request to certificate registration point.
  Exiting Notify with 0x0
  ```

- **CertificateRegistrationPoint. svclog**:

  ![Protokol Certificate Connectoru Intune](../protect/media/troubleshoot-scep-certificate-reporting/certificate-registration-point-log.png)

- **NDESConnector. svclog**:

  ![Protokol Certificate Connectoru Intune](../protect/media/troubleshoot-scep-certificate-reporting/ndesconnector-log.png)

- **CertificateRequestStatus**:

  Přejděte do složky *%ProgramFiles%\Microsoft Intune\CertificateRequestStatus* , kde se zobrazí složky **nezdařené**, **zpracovávané**a **úspěšné** , které obsahují stavové soubory žádosti o certifikát.

  Pokud je žádost o certifikát úspěšně zpracována, zobrazí se nové soubory ve složce **úspěšné** . Pomocí *programu Notepad. exe* můžete soubory otevřít a zobrazit data nahraná do služby Intune pomocí Certificate Connectoru Intune. Data, která jste nahráli, zahrnují podrobnosti jako **CertificateSerialNumber**, **UserID**, **DeviceID**a **kryptografický otisk**.

### <a name="troubleshoot-stuck-files"></a>Řešení potíží se zablokovanými soubory

Pokud nevidíte žádné nové soubory, které se vytvářejí ve složce *úspěšné* , zkontrolujte, jestli jsou ve složce pro *zpracování* zablokované nějaké soubory.

Ověřte, že na serveru NDES je spuštěná služba Intune Connector a že v Ndesconnector. svclog nejsou žádné chyby.

## <a name="next-steps"></a>Další kroky

[Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md)
