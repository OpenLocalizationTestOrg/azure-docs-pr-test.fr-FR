---
title: "environnement de l’utilisateur Azure pile aaaConfigure hello PowerShell | Documents Microsoft"
description: "Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: 8e7ccea24a1917d349ab06e0abe29f534b47b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-users-powershell-environment"></a><span data-ttu-id="f1008-103">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1008-103">Configure hello Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="f1008-104">En tant qu’utilisateur d’Azure Stack, vous pouvez configurer l’environnement PowerShell de votre Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f1008-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="f1008-105">Après avoir configuré, vous pouvez utiliser PowerShell toomanage des ressources de pile de Azure telles que s’abonner toooffers, créer des ordinateurs virtuels, déployer des modèles Azure Resource Manager, etc.. Cette rubrique est toouse étendue avec les environnements hello utilisateur uniquement, si vous souhaitez tooset de PowerShell pour l’environnement d’opérateur hello cloud, consultez toohello [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello](azure-stack-powershell-configure-admin.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="f1008-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as subscribe toooffers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped toouse with hello user environments only, if you want tooset up PowerShell for hello cloud operator environment, refer toohello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f1008-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1008-106">Prerequisites</span></span> 

<span data-ttu-id="f1008-107">Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="f1008-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="f1008-108">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f1008-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="f1008-109">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="f1008-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="f1008-110">Configuration de l’environnement utilisateur hello et la connexion tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="f1008-110">Configure hello user environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="f1008-111">En fonction de type hello du déploiement (Azure AD ou AD FS), exécutez une des hello suivant tooconfigure de script PowerShell pour Azure pile :</span><span class="sxs-lookup"><span data-stu-id="f1008-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="f1008-112">Déploiements basés sur Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="f1008-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="f1008-113">Déploiements basés sur Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="f1008-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="f1008-114">Inscrire des fournisseurs de ressources</span><span class="sxs-lookup"><span data-stu-id="f1008-114">Register resource providers</span></span>

<span data-ttu-id="f1008-115">Lorsqu’il fonctionne sur un abonnement de l’utilisateur nouvellement créé qui ne contient aucune ressource déployée via le portail de hello, les fournisseurs de ressources hello ne sont pas enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f1008-115">When operating on a newly created user subscription that doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="f1008-116">Vous devez les inscrire explicitement à l’aide de hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="f1008-116">You should explicitly register them by using hello following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a><span data-ttu-id="f1008-117">Tester la connectivité hello</span><span class="sxs-lookup"><span data-stu-id="f1008-117">Test hello connectivity</span></span>

<span data-ttu-id="f1008-118">Maintenant que nous avons tout configurer, nous allons utiliser de ressources au sein de la pile d’Azure PowerShell toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1008-118">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="f1008-119">Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f1008-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="f1008-120">Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :</span><span class="sxs-lookup"><span data-stu-id="f1008-120">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="f1008-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1008-121">Next steps</span></span>
* [<span data-ttu-id="f1008-122">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f1008-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="f1008-123">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1008-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
