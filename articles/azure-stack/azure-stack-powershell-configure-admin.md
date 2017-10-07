---
title: "environnement de l’opérateur aaaConfigure hello pile d’Azure PowerShell | Documents Microsoft"
description: "Découvrez comment tooConfigure hello environnement de l’opérateur de la pile d’Azure PowerShell."
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
ms.openlocfilehash: 1a1e95b95598062f155126b9560934bba4994f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a><span data-ttu-id="a9fc2-103">Configurer l’environnement de l’opérateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9fc2-103">Configure hello Azure Stack operator's PowerShell environment</span></span>

<span data-ttu-id="a9fc2-104">En tant qu’opérateur Azure Stack, vous pouvez configurer l’environnement PowerShell de votre Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9fc2-104">As an Azure Stack operator, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="a9fc2-105">Après avoir configuré, vous pouvez utiliser de ressources Azure pile toomanage PowerShell telles que la création d’offres, les plans, les quotas, la gestion des alertes, etc.. Cette rubrique est étendue toouse avec l’opérateur de cloud hello environnements uniquement, si vous souhaitez tooset de PowerShell pour l’environnement utilisateur hello, reportez-vous trop[configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="a9fc2-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as creating offers, plans, quotas, managing alerts, etc. This topic is scoped toouse with hello cloud operator environments only, if you want tooset up PowerShell for hello user environment, refer too[Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a9fc2-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a9fc2-106">Prerequisites</span></span>

<span data-ttu-id="a9fc2-107">Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="a9fc2-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span> 

* <span data-ttu-id="a9fc2-108">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="a9fc2-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="a9fc2-109">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="a9fc2-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="a9fc2-110">Configurer l’environnement d’opérateur hello et connectez-vous à tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="a9fc2-110">Configure hello operator environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="a9fc2-111">En fonction de type hello du déploiement (Azure AD ou AD FS), exécutez une des hello suivant script tooconfigure hello Azure opérateur environnement pile avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a9fc2-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure hello Azure Stack operator environment with PowerShell:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="a9fc2-112">Déploiements basés sur Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="a9fc2-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="a9fc2-113">Déploiements basés sur Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="a9fc2-113">Active Directory Federation Services (AD FS) based deployments</span></span>
         
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="a9fc2-114">Tester la connectivité hello</span><span class="sxs-lookup"><span data-stu-id="a9fc2-114">Test hello connectivity</span></span>

<span data-ttu-id="a9fc2-115">Maintenant que nous avons tout configurer, nous allons utiliser de ressources au sein de la pile d’Azure PowerShell toocreate.</span><span class="sxs-lookup"><span data-stu-id="a9fc2-115">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="a9fc2-116">Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9fc2-116">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="a9fc2-117">Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :</span><span class="sxs-lookup"><span data-stu-id="a9fc2-117">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="a9fc2-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9fc2-118">Next steps</span></span>
* [<span data-ttu-id="a9fc2-119">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9fc2-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="a9fc2-120">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9fc2-120">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)