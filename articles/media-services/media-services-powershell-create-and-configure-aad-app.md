---
title: "Utiliser PowerShell pour créer une application Azure AD pour accéder à l’API Azure Media Services | Microsoft Docs"
description: "Découvrez comment utiliser PowerShell pour créer une application Azure Active Directory (Azure AD) et la configurer pour accéder à l’API Azure Media Services."
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
ms.openlocfilehash: eea0f3a03dd77ce56484f32b192299bd97c05300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a><span data-ttu-id="1118a-103">Utiliser PowerShell pour créer une application Azure AD à utiliser avec l’API Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="1118a-103">Use PowerShell to create an Azure AD app to use with the Azure Media Services API</span></span>

<span data-ttu-id="1118a-104">Découvrez comment utiliser un script PowerShell pour créer une application Azure Active Directory (Azure AD) et un principal du service pour accéder aux ressources Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1118a-104">Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1118a-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1118a-105">Prerequisites</span></span>

- <span data-ttu-id="1118a-106">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1118a-106">An Azure account.</span></span> <span data-ttu-id="1118a-107">Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1118a-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="1118a-108">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="1118a-108">A Media Services account.</span></span> <span data-ttu-id="1118a-109">Pour plus d’informations, voir [Création d’un compte Azure Media Services dans le portail Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1118a-109">For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="1118a-110">Azure PowerShell version 0.8.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1118a-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="1118a-111">Pour plus d’informations, découvrez l’[utilisation d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1118a-111">For more information, see [How to use Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="1118a-112">Applets de commande Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1118a-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="1118a-113">Créer une application Azure AD à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1118a-113">Create an Azure AD app by using PowerShell</span></span>  

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
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

<span data-ttu-id="1118a-114">Pour plus d’informations, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="1118a-114">For more information, see the following articles:</span></span>

- [<span data-ttu-id="1118a-115">Créer un principal du service pour accéder aux ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1118a-115">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="1118a-116">Gérer le contrôle d’accès en fonction du rôle à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1118a-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="1118a-117">Comment configurer manuellement des applications démons à l’aide de certificats</span><span class="sxs-lookup"><span data-stu-id="1118a-117">How to manually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="1118a-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1118a-118">Next steps</span></span>

<span data-ttu-id="1118a-119">Commencez le [chargement de fichiers sur votre compte](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="1118a-119">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
