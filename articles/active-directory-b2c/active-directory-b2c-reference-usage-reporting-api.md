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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="0dfb8-103">L’accès aux rapports d’utilisation dans Azure AD B2C via hello API de création de rapports</span><span class="sxs-lookup"><span data-stu-id="0dfb8-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="0dfb8-104">Azure Active Directory B2C (Azure AD B2C) fournit une authentification basée sur la connexion des utilisateurs et de l’authentification multifacteur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="0dfb8-105">L’authentification est fournie pour les utilisateurs finals de votre famille d’applications à travers les fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="0dfb8-106">Lorsque vous connaissez le nombre de hello d’utilisateurs inscrits dans le locataire hello, fournisseurs hello ils utilisées tooregister et le nombre de hello d’authentifications par type, vous pouvez répondre aux questions telles que :</span><span class="sxs-lookup"><span data-stu-id="0dfb8-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="0dfb8-107">Nombre d’utilisateurs à partir de chaque type de fournisseur d’identité (par exemple, un compte Microsoft ou LinkedIn) ont enregistré Bonjour 10 derniers jours ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="0dfb8-108">Le nombre des authentifications à l’aide de l’authentification multifacteur ont abouti Bonjour le mois dernier ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="0dfb8-109">Combien d’authentifications basées sur la connexion ont été effectuées ce mois-ci ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="0dfb8-110">Par jour ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-110">Per day?</span></span> <span data-ttu-id="0dfb8-111">Par application ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-111">Per application?</span></span>
* <span data-ttu-id="0dfb8-112">Comment puis-je évaluer hello attendu coût mensuel de mon activité du client Azure AD B2C ?</span><span class="sxs-lookup"><span data-stu-id="0dfb8-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="0dfb8-113">Cet article se concentre sur l’activité de toobilling des rapports liés, qui est basée sur hello nombre d’utilisateurs, facturables signe dans basés sur des authentifications et d’authentifications multifacteur.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0dfb8-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0dfb8-114">Prerequisites</span></span>
<span data-ttu-id="0dfb8-115">Avant de commencer, vous devez étapes hello toocomplete [tooaccess de conditions préalables hello Azure AD reporting API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="0dfb8-116">Créer une application, obtenir une clé secrète pour elle et grant il accéder à des rapports du locataire tooyour Azure AD B2C des droits.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="0dfb8-117">Des exemples *Script Bash* et *Script Python* sont également fournis ici.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="0dfb8-118">Script PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dfb8-118">PowerShell script</span></span>
<span data-ttu-id="0dfb8-119">Ce script illustre la création de hello de quatre rapports d’utilisation à l’aide de hello `TimeStamp` paramètre et hello `ApplicationId` filtre.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

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


## <a name="usage-report-definitions"></a><span data-ttu-id="0dfb8-120">Définitions de rapport d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0dfb8-120">Usage report definitions</span></span>
* <span data-ttu-id="0dfb8-121">**tenantUserCount**: hello nombre d’utilisateurs dans le locataire hello par type de fournisseur d’identité, par jour Bonjour 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="0dfb8-122">(Le cas échéant, un `TimeStamp` filtre fournit le nombre de comptes utilisateur à partir d’une date spécifiée de toohello date actuelle).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="0dfb8-123">rapport de Hello fournit :</span><span class="sxs-lookup"><span data-stu-id="0dfb8-123">hello report provides:</span></span>
  * <span data-ttu-id="0dfb8-124">**TotalUserCount**: hello nombre de tous les objets utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="0dfb8-125">**OtherUserCount**: hello du nombre d’utilisateurs d’Azure Active Directory (pas les utilisateurs Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="0dfb8-126">**LocalUserCount**: hello du nombre de comptes d’utilisateur Azure AD B2C créé avec le client de toohello local Azure Active Directory B2C d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="0dfb8-127">**AlternateIdUserCount**: nombre de hello d’Azure AD B2C utilisateurs inscrits avec des fournisseurs d’identité externe (par exemple, Facebook, un compte Microsoft ou un autre client Azure Active Directory, également appelée tooas un `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="0dfb8-128">**b2cAuthenticationCountSummary**: résumé du nombre de quotidienne hello d’authentifications facturables sur hello 30 derniers jours, par jour et par type de flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="0dfb8-129">**b2cAuthenticationCount**: hello du nombre d’authentifications dans un laps de temps.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="0dfb8-130">valeur par défaut Hello est hello 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="0dfb8-131">(Facultatif : hello et fermants `TimeStamp` paramètres définissent une période de temps spécifique.) hello sortie inclut `StartTimeStamp` (première date de l’activité de ce client) et `EndTimeStamp` (dernière mise à jour).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="0dfb8-132">**b2cMfaRequestCountSummary**: résumé du nombre de quotidienne hello d’authentification multifacteur, par jour et par type (SMS ou vocales).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="0dfb8-133">Limites</span><span class="sxs-lookup"><span data-stu-id="0dfb8-133">Limitations</span></span>
<span data-ttu-id="0dfb8-134">Les données du compteur sont actualisées toutes les 24 heures too48.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="0dfb8-135">Les authentifications sont mises à jour plusieurs fois par jour.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="0dfb8-136">Lorsque vous utilisez hello `ApplicationId` filtre, une réponse de rapport vide peut être due tooone des conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="0dfb8-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="0dfb8-137">ID de l’application Hello n’existe pas dans le locataire de hello.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="0dfb8-138">Assurez-vous qu’il est correct.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="0dfb8-139">ID de l’application Hello existe, mais aucune donnée n’a été trouvée dans hello période de rapport.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="0dfb8-140">Passez en revue vos paramètres de date/heure.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0dfb8-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0dfb8-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="0dfb8-142">Estimations de la facturation mensuelle pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dfb8-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="0dfb8-143">Lorsque vous associez [hello plus Azure AD B2C tarification actuelle disponible](https://azure.microsoft.com/pricing/details/active-directory-b2c/), vous pouvez estimer quotidiennes, hebdomadaire et mensuelle consommation Azure.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="0dfb8-144">Une estimation est particulièrement utile quand vous prévoyez des changements de comportement du locataire qui peuvent avoir un impact sur le coût global.</span><span class="sxs-lookup"><span data-stu-id="0dfb8-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="0dfb8-145">Vous pouvez examiner les coûts réels dans votre [abonnement Azure lié](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="0dfb8-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="0dfb8-146">Options pour les autres formats de sortie</span><span class="sxs-lookup"><span data-stu-id="0dfb8-146">Options for other output formats</span></span>
<span data-ttu-id="0dfb8-147">Hello de code suivant montre des exemples d’envoi tooJSON de sortie et une liste de valeurs de nom XML :</span><span class="sxs-lookup"><span data-stu-id="0dfb8-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
