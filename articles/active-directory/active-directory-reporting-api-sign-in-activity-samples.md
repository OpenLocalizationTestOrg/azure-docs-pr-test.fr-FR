---
title: "exemples de rapports API activité aaaAzure connexion dans Active Directory | Documents Microsoft"
description: "Comment tooget démarrer avec hello API Azure Active Directory Reporting"
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
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="2614f-103">Exemples de l’API de création de rapports sur l’activité de connexion Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2614f-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="2614f-104">Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="2614f-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="2614f-105">La création de rapports Azure AD vous offre une API qui vous permet de données d’activité de connexion tooaccess à l’aide de code ou les outils connexes.</span><span class="sxs-lookup"><span data-stu-id="2614f-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="2614f-106">étendue de cette rubrique Hello est tooprovide vous avec l’exemple de code pour hello **connectez-vous activité API**.</span><span class="sxs-lookup"><span data-stu-id="2614f-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="2614f-107">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="2614f-107">See:</span></span>

* <span data-ttu-id="2614f-108">[Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles</span><span class="sxs-lookup"><span data-stu-id="2614f-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="2614f-109">[Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.</span><span class="sxs-lookup"><span data-stu-id="2614f-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2614f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2614f-110">Prerequisites</span></span>
<span data-ttu-id="2614f-111">Avant de pouvoir utiliser les exemples hello dans cette rubrique, vous devez toocomplete hello [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="2614f-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="2614f-112">Script PowerShell</span><span class="sxs-lookup"><span data-stu-id="2614f-112">PowerShell script</span></span>
    # This script will require hello Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a><span data-ttu-id="2614f-113">L’exécution du script de hello</span><span class="sxs-lookup"><span data-stu-id="2614f-113">Executing hello script</span></span>
<span data-ttu-id="2614f-114">Une fois vous terminez de modifier le script de hello, exécutez et de Vérifiez que hello attendu de données à partir de hello rapport de journaux d’Audit sont retournées.</span><span class="sxs-lookup"><span data-stu-id="2614f-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="2614f-115">script de Hello retourne une sortie à partir de l’état connexion hello au format JSON.</span><span class="sxs-lookup"><span data-stu-id="2614f-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="2614f-116">Il crée également un `SigninActivities.json` de fichiers avec hello même sortie.</span><span class="sxs-lookup"><span data-stu-id="2614f-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="2614f-117">Vous pouvez faire des essais en modifiant les données de tooreturn hello script à partir d’autres rapports et commentez les formats de sortie de hello que vous n’avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="2614f-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2614f-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2614f-118">Next Steps</span></span>
* <span data-ttu-id="2614f-119">Voulez-vous que les exemples de hello toocustomize dans cette rubrique ?</span><span class="sxs-lookup"><span data-stu-id="2614f-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="2614f-120">Extraire hello [Azure Active Directory signe-activité de référence de l’API](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2614f-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="2614f-121">Si vous souhaitez une vue d’ensemble complète de l’utilisation de toosee hello Azure Active Directory API de création de rapports, consultez [prise en main de hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2614f-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="2614f-122">Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2614f-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

