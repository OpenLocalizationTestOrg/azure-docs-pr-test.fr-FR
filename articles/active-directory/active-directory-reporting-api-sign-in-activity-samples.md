---
title: "Exemples de l’API de création de rapports sur l’activité de connexion Azure Active Directory | Microsoft Docs"
description: "Prise en main de l'API de création de rapports Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="bff5f-103">Exemples de l’API de création de rapports sur l’activité de connexion Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bff5f-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="bff5f-104">Cette rubrique fait partie d’un ensemble de rubriques relatives à l’API de création de rapports Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bff5f-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="bff5f-105">La création de rapports Azure AD fournit une API qui vous permet d’accéder aux données de l’activité de connexion à l’aide de code ou d’outils associés.</span><span class="sxs-lookup"><span data-stu-id="bff5f-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="bff5f-106">Cette rubrique a pour but de vous fournir un exemple de code pour **l’API d’activité de connexion**.</span><span class="sxs-lookup"><span data-stu-id="bff5f-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="bff5f-107">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="bff5f-107">See:</span></span>

* <span data-ttu-id="bff5f-108">[Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles</span><span class="sxs-lookup"><span data-stu-id="bff5f-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="bff5f-109">[Prise en main de l’API de création de rapports Azure Active Directory](active-directory-reporting-api-getting-started.md) pour plus d’informations sur l’API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="bff5f-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bff5f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bff5f-110">Prerequisites</span></span>
<span data-ttu-id="bff5f-111">Avant de pouvoir utiliser les exemples de cette rubrique, vous devez respecter la [configuration requise pour accéder à l’API de création de rapports Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="bff5f-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="bff5f-112">Script PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff5f-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="bff5f-113">Exécution du script</span><span class="sxs-lookup"><span data-stu-id="bff5f-113">Executing the script</span></span>
<span data-ttu-id="bff5f-114">Une fois que vous avez terminé la modification du script, exécutez-le, puis vérifiez que les données attendues dans les journaux d’audit sont retournées.</span><span class="sxs-lookup"><span data-stu-id="bff5f-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="bff5f-115">Le script renvoie la sortie du rapport sur la connexion au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bff5f-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="bff5f-116">Il crée également un fichier `SigninActivities.json` avec la même sortie.</span><span class="sxs-lookup"><span data-stu-id="bff5f-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="bff5f-117">Vous pouvez expérimenter en modifiant le script pour renvoyer des données à partir d’autres rapports, et également commenter les formats de sortie dont vous n’avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="bff5f-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bff5f-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bff5f-118">Next Steps</span></span>
* <span data-ttu-id="bff5f-119">Vous souhaitez personnaliser les exemples de cette rubrique ?</span><span class="sxs-lookup"><span data-stu-id="bff5f-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="bff5f-120">Consultez la [référence d’API d’activité de connexion Azure Active Directory](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bff5f-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="bff5f-121">Si vous souhaitez obtenir une présentation complète de l’utilisation de l’API de création de rapports Azure Active Directory, consultez [Prise en main de l’API de création de rapports Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bff5f-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="bff5f-122">Si vous souhaitez en savoir plus sur la création de rapports Azure Active Directory, consultez le [Guide Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="bff5f-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

