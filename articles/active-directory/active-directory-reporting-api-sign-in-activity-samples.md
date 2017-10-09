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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Exemples de l’API de création de rapports sur l’activité de connexion Azure Active Directory
Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.  
La création de rapports Azure AD vous offre une API qui vous permet de données d’activité de connexion tooaccess à l’aide de code ou les outils connexes.  
étendue de cette rubrique Hello est tooprovide vous avec l’exemple de code pour hello **connectez-vous activité API**.

Consultez l'article :

* [Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles
* [Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.


## <a name="prerequisites"></a>Composants requis
Avant de pouvoir utiliser les exemples hello dans cette rubrique, vous devez toocomplete hello [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>Script PowerShell
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




## <a name="executing-hello-script"></a>L’exécution du script de hello
Une fois vous terminez de modifier le script de hello, exécutez et de Vérifiez que hello attendu de données à partir de hello rapport de journaux d’Audit sont retournées.

script de Hello retourne une sortie à partir de l’état connexion hello au format JSON. Il crée également un `SigninActivities.json` de fichiers avec hello même sortie. Vous pouvez faire des essais en modifiant les données de tooreturn hello script à partir d’autres rapports et commentez les formats de sortie de hello que vous n’avez pas besoin.

## <a name="next-steps"></a>Étapes suivantes
* Voulez-vous que les exemples de hello toocustomize dans cette rubrique ? Extraire hello [Azure Active Directory signe-activité de référence de l’API](active-directory-reporting-api-sign-in-activity-reference.md). 
* Si vous souhaitez une vue d’ensemble complète de l’utilisation de toosee hello Azure Active Directory API de création de rapports, consultez [prise en main de hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).
* Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).  

