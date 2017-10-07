---
title: "aaaUse PowerShell toocreate un tooaccess d’application Azure AD hello API Azure Media Services | Documents Microsoft"
description: "Découvrez comment toouse PowerShell toocreate une application Azure Active Directory (Azure AD) et configurez le tooaccess hello API Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Utilisez PowerShell toocreate un toouse d’application Azure AD avec hello API Azure Media Services

Découvrez comment toouse un PowerShell toocreate une application Azure Active Directory (Azure AD) et script tooaccess principal du service ressources d’Azure Media Services.  

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Un compte Media Services. Pour plus d’informations, consultez [créer un compte Azure Media Services Bonjour Azure portal](media-services-portal-create-account.md).
- Azure PowerShell version 0.8.8 ou version ultérieure. Pour plus d’informations, consultez [comment toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Applets de commande Azure Resource Manager.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Créer une application Azure AD à l’aide de PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Pour plus d’informations, consultez hello suivant des articles :

- [Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Gérer le contrôle d’accès en fonction du rôle à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Comment toomanually configurer des applications de démon à l’aide de certificats](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Étapes suivantes

Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).
