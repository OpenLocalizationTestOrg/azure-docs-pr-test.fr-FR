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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="76fb0-103">Utilisez PowerShell toocreate un toouse d’application Azure AD avec hello API Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="76fb0-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="76fb0-104">Découvrez comment toouse un PowerShell toocreate une application Azure Active Directory (Azure AD) et script tooaccess principal du service ressources d’Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="76fb0-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="76fb0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76fb0-105">Prerequisites</span></span>

- <span data-ttu-id="76fb0-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="76fb0-106">An Azure account.</span></span> <span data-ttu-id="76fb0-107">Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76fb0-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="76fb0-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="76fb0-108">A Media Services account.</span></span> <span data-ttu-id="76fb0-109">Pour plus d’informations, consultez [créer un compte Azure Media Services Bonjour Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="76fb0-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="76fb0-110">Azure PowerShell version 0.8.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="76fb0-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="76fb0-111">Pour plus d’informations, consultez [comment toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76fb0-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="76fb0-112">Applets de commande Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76fb0-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="76fb0-113">Créer une application Azure AD à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="76fb0-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="76fb0-114">Pour plus d’informations, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="76fb0-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="76fb0-115">Utiliser Azure PowerShell toocreate une ressources tooaccess principal du service</span><span class="sxs-lookup"><span data-stu-id="76fb0-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="76fb0-116">Gérer le contrôle d’accès en fonction du rôle à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="76fb0-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="76fb0-117">Comment toomanually configurer des applications de démon à l’aide de certificats</span><span class="sxs-lookup"><span data-stu-id="76fb0-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="76fb0-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76fb0-118">Next steps</span></span>

<span data-ttu-id="76fb0-119">Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="76fb0-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
