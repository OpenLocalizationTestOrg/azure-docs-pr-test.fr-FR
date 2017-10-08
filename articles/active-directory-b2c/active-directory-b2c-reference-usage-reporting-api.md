---
title: "Azure Active Directory B2C : Définitions et exemples de l’API de rapports d’utilisation | Microsoft Docs"
description: "Guide et exemples d’obtention de rapports sur les utilisateurs, les authentifications et les authentifications multifacteurs des locataires Azure AD B2C"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>L’accès aux rapports d’utilisation dans Azure AD B2C via hello API de création de rapports

Azure Active Directory B2C (Azure AD B2C) fournit une authentification basée sur la connexion des utilisateurs et de l’authentification multifacteur d’Azure. L’authentification est fournie pour les utilisateurs finals de votre famille d’applications à travers les fournisseurs d’identité. Lorsque vous connaissez le nombre de hello d’utilisateurs inscrits dans le locataire hello, fournisseurs hello ils utilisées tooregister et le nombre de hello d’authentifications par type, vous pouvez répondre aux questions telles que :
* Nombre d’utilisateurs à partir de chaque type de fournisseur d’identité (par exemple, un compte Microsoft ou LinkedIn) ont enregistré Bonjour 10 derniers jours ?
* Le nombre des authentifications à l’aide de l’authentification multifacteur ont abouti Bonjour le mois dernier ?
* Combien d’authentifications basées sur la connexion ont été effectuées ce mois-ci ? Par jour ? Par application ?
* Comment puis-je évaluer hello attendu coût mensuel de mon activité du client Azure AD B2C ?

Cet article se concentre sur l’activité de toobilling des rapports liés, qui est basée sur hello nombre d’utilisateurs, facturables signe dans basés sur des authentifications et d’authentifications multifacteur.


## <a name="prerequisites"></a>Composants requis
Avant de commencer, vous devez étapes hello toocomplete [tooaccess de conditions préalables hello Azure AD reporting API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Créer une application, obtenir une clé secrète pour elle et grant il accéder à des rapports du locataire tooyour Azure AD B2C des droits. Des exemples *Script Bash* et *Script Python* sont également fournis ici. 

## <a name="powershell-script"></a>Script PowerShell
Ce script illustre la création de hello de quatre rapports d’utilisation à l’aide de hello `TimeStamp` paramètre et hello `ApplicationId` filtre.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>Définitions de rapport d’utilisation
* **tenantUserCount**: hello nombre d’utilisateurs dans le locataire hello par type de fournisseur d’identité, par jour Bonjour 30 derniers jours. (Le cas échéant, un `TimeStamp` filtre fournit le nombre de comptes utilisateur à partir d’une date spécifiée de toohello date actuelle). rapport de Hello fournit :
  * **TotalUserCount**: hello nombre de tous les objets utilisateur.
  * **OtherUserCount**: hello du nombre d’utilisateurs d’Azure Active Directory (pas les utilisateurs Azure AD B2C).
  * **LocalUserCount**: hello du nombre de comptes d’utilisateur Azure AD B2C créé avec le client de toohello local Azure Active Directory B2C d’informations d’identification.

* **AlternateIdUserCount**: nombre de hello d’Azure AD B2C utilisateurs inscrits avec des fournisseurs d’identité externe (par exemple, Facebook, un compte Microsoft ou un autre client Azure Active Directory, également appelée tooas un `OrgId`).

* **b2cAuthenticationCountSummary**: résumé du nombre de quotidienne hello d’authentifications facturables sur hello 30 derniers jours, par jour et par type de flux d’authentification.

* **b2cAuthenticationCount**: hello du nombre d’authentifications dans un laps de temps. valeur par défaut Hello est hello 30 derniers jours.  (Facultatif : hello et fermants `TimeStamp` paramètres définissent une période de temps spécifique.) hello sortie inclut `StartTimeStamp` (première date de l’activité de ce client) et `EndTimeStamp` (dernière mise à jour).

* **b2cMfaRequestCountSummary**: résumé du nombre de quotidienne hello d’authentification multifacteur, par jour et par type (SMS ou vocales).


## <a name="limitations"></a>Limites
Les données du compteur sont actualisées toutes les 24 heures too48. Les authentifications sont mises à jour plusieurs fois par jour. Lorsque vous utilisez hello `ApplicationId` filtre, une réponse de rapport vide peut être due tooone des conditions suivantes :
  * ID de l’application Hello n’existe pas dans le locataire de hello. Assurez-vous qu’il est correct.
  * ID de l’application Hello existe, mais aucune donnée n’a été trouvée dans hello période de rapport. Passez en revue vos paramètres de date/heure.


## <a name="next-steps"></a>Étapes suivantes
### <a name="monthly-bill-estimates-for-azure-ad"></a>Estimations de la facturation mensuelle pour Azure AD
Lorsque vous associez [hello plus Azure AD B2C tarification actuelle disponible](https://azure.microsoft.com/pricing/details/active-directory-b2c/), vous pouvez estimer quotidiennes, hebdomadaire et mensuelle consommation Azure.  Une estimation est particulièrement utile quand vous prévoyez des changements de comportement du locataire qui peuvent avoir un impact sur le coût global. Vous pouvez examiner les coûts réels dans votre [abonnement Azure lié](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Options pour les autres formats de sortie
Hello de code suivant montre des exemples d’envoi tooJSON de sortie et une liste de valeurs de nom XML :
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
