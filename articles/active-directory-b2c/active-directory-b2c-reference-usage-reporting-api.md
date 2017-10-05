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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="09a7c-103">Accès aux rapports d’utilisation dans Azure AD B2C via l’API de création de rapports</span><span class="sxs-lookup"><span data-stu-id="09a7c-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="09a7c-104">Azure Active Directory B2C (Azure AD B2C) fournit une authentification basée sur la connexion des utilisateurs et de l’authentification multifacteur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="09a7c-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="09a7c-105">L’authentification est fournie pour les utilisateurs finals de votre famille d’applications à travers les fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="09a7c-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="09a7c-106">Quand vous connaissez le nombre d’utilisateurs inscrits dans le locataire, les fournisseurs qu’ils ont utilisés pour s’inscrire et le nombre d’authentifications par type, vous pouvez répondre à des questions comme celles-ci :</span><span class="sxs-lookup"><span data-stu-id="09a7c-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="09a7c-107">Combien d’utilisateurs de chaque type de fournisseur d’identité (par exemple un compte Microsoft ou LinkedIn) se sont inscrits au cours des 10 derniers jours ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="09a7c-108">Combien d’authentifications utilisant l’authentification multifacteur ont réussi au cours du mois dernier ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="09a7c-109">Combien d’authentifications basées sur la connexion ont été effectuées ce mois-ci ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="09a7c-110">Par jour ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-110">Per day?</span></span> <span data-ttu-id="09a7c-111">Par application ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-111">Per application?</span></span>
* <span data-ttu-id="09a7c-112">Comment puis-je estimer le coût mensuel prévu de l’activité de mon locataire Azure AD B2C ?</span><span class="sxs-lookup"><span data-stu-id="09a7c-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="09a7c-113">Cet article se concentre sur les rapports liés à l’activité de facturation, qui est basée sur le nombre d’utilisateurs, les authentifications facturables basées sur la connexion et les authentifications multifacteurs.</span><span class="sxs-lookup"><span data-stu-id="09a7c-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="09a7c-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="09a7c-114">Prerequisites</span></span>
<span data-ttu-id="09a7c-115">Avant de commencer, vous devez effectuer les étapes décrites dans [Prérequis pour accéder aux API de création de rapports d’Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="09a7c-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="09a7c-116">Créez une application, obtenez une clé secrète pour celle-ci et accordez-lui des autorisations d’accès aux rapports de votre client Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09a7c-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="09a7c-117">Des exemples *Script Bash* et *Script Python* sont également fournis ici.</span><span class="sxs-lookup"><span data-stu-id="09a7c-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="09a7c-118">Script PowerShell</span><span class="sxs-lookup"><span data-stu-id="09a7c-118">PowerShell script</span></span>
<span data-ttu-id="09a7c-119">Ce script montre la création de quatre rapports d’utilisation avec le paramètre `TimeStamp` et le filtre `ApplicationId`.</span><span class="sxs-lookup"><span data-stu-id="09a7c-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="09a7c-120">Définitions de rapport d’utilisation</span><span class="sxs-lookup"><span data-stu-id="09a7c-120">Usage report definitions</span></span>
* <span data-ttu-id="09a7c-121">**tenantUserCount** : le nombre d’utilisateurs dans le locataire par type de fournisseur d’identité, par jour, au cours des 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="09a7c-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="09a7c-122">(Facultatif : un filtre `TimeStamp` fournit le nombre d’utilisateurs à partir d’une date spécifiée jusqu’à la date du jour.)</span><span class="sxs-lookup"><span data-stu-id="09a7c-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="09a7c-123">Le rapport fournit les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="09a7c-123">The report provides:</span></span>
  * <span data-ttu-id="09a7c-124">**TotalUserCount** : nombre de tous les objets utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09a7c-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="09a7c-125">**OtherUserCount** : nombre d’utilisateurs d’Azure Active Directory (pas les utilisateurs d’Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="09a7c-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="09a7c-126">**LocalUserCount** : nombre de comptes utilisateur Azure AD B2C créés avec les informations d’identification locales du locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09a7c-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="09a7c-127">**AlternateIdUserCount** : nombre d’utilisateurs d’Azure AD B2C inscrits auprès de fournisseurs d’identité externes (par exemple Facebook, un compte Microsoft ou un autre locataire Azure Active Directory, également appelé `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="09a7c-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="09a7c-128">**b2cAuthenticationCountSummary** : récapitulatif du nombre quotidien d’authentifications facturables au cours des 30 derniers jours, par jour et par type de flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="09a7c-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="09a7c-129">**b2cAuthenticationCount** : nombre d’authentifications dans une période de temps définie.</span><span class="sxs-lookup"><span data-stu-id="09a7c-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="09a7c-130">La période par défaut est celle des 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="09a7c-130">The default is the last 30 days.</span></span>  <span data-ttu-id="09a7c-131">(Facultatif : les paramètres `TimeStamp` de début et de fin définissent une période spécifique.) La sortie inclut `StartTimeStamp` (première date d’activité de ce locataire ) et `EndTimeStamp` (dernière mise à jour).</span><span class="sxs-lookup"><span data-stu-id="09a7c-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="09a7c-132">**b2cMfaRequestCountSummary** : récapitulatif du nombre quotidien d’authentifications multifacteurs, par jour et par type (SMS ou vocales).</span><span class="sxs-lookup"><span data-stu-id="09a7c-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="09a7c-133">Limitations</span><span class="sxs-lookup"><span data-stu-id="09a7c-133">Limitations</span></span>
<span data-ttu-id="09a7c-134">Les données du décompte d’utilisateurs sont actualisées toutes les 24 à 48 heures.</span><span class="sxs-lookup"><span data-stu-id="09a7c-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="09a7c-135">Les authentifications sont mises à jour plusieurs fois par jour.</span><span class="sxs-lookup"><span data-stu-id="09a7c-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="09a7c-136">Quand vous utilisez le filtre `ApplicationId`, une réponse de rapport vide peut être due à une des conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="09a7c-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="09a7c-137">L’ID d’application n’existe pas dans le locataire.</span><span class="sxs-lookup"><span data-stu-id="09a7c-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="09a7c-138">Assurez-vous qu’il est correct.</span><span class="sxs-lookup"><span data-stu-id="09a7c-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="09a7c-139">L’ID d’application existe, mais aucune donnée n’a été trouvée dans la période du rapport.</span><span class="sxs-lookup"><span data-stu-id="09a7c-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="09a7c-140">Passez en revue vos paramètres de date/heure.</span><span class="sxs-lookup"><span data-stu-id="09a7c-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="09a7c-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09a7c-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="09a7c-142">Estimations de la facturation mensuelle pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="09a7c-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="09a7c-143">Lorsque vous utilisez également [la tarification Azure AD B2C la plus récente disponible](https://azure.microsoft.com/pricing/details/active-directory-b2c/), vous pouvez estimer la consommation Azure quotidienne, hebdomadaire et mensuelle.</span><span class="sxs-lookup"><span data-stu-id="09a7c-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="09a7c-144">Une estimation est particulièrement utile quand vous prévoyez des changements de comportement du locataire qui peuvent avoir un impact sur le coût global.</span><span class="sxs-lookup"><span data-stu-id="09a7c-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="09a7c-145">Vous pouvez examiner les coûts réels dans votre [abonnement Azure lié](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="09a7c-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="09a7c-146">Options pour les autres formats de sortie</span><span class="sxs-lookup"><span data-stu-id="09a7c-146">Options for other output formats</span></span>
<span data-ttu-id="09a7c-147">Le code suivant montre des exemples de l’envoi de la sortie vers JSON, vers une liste de valeurs de noms et vers XML :</span><span class="sxs-lookup"><span data-stu-id="09a7c-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
