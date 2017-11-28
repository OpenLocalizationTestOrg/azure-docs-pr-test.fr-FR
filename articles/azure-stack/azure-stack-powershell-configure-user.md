---
title: "Configurer l’environnement PowerShell de l’utilisateur Azure Stack | Microsoft Docs"
description: "Configurer l’environnement PowerShell de l’utilisateur Azure Stack"
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
ms.openlocfilehash: dabbd83fb35397f2cf90fac5957d299f0c5d446e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-the-azure-stack-users-powershell-environment"></a><span data-ttu-id="9b671-103">Configurer l’environnement PowerShell de l’utilisateur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9b671-103">Configure the Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="9b671-104">En tant qu’utilisateur d’Azure Stack, vous pouvez configurer l’environnement PowerShell de votre Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9b671-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="9b671-105">Une fois la configuration effectuée, vous pouvez utiliser PowerShell pour gérer les ressources Azure Stack, par exemple vous abonner à des offres, créer des machines virtuelles, déployer des modèles Azure Resource Manager, et ainsi de suite. Cette rubrique concerne uniquement les environnements utilisateur. Si vous souhaitez configurer PowerShell pour l’environnement d’opérateur cloud, consultez la rubrique [Configurer l’environnement PowerShell de l’opérateur Azure Stack](azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="9b671-105">After you configure, you can use PowerShell to manage Azure Stack resources such as subscribe to offers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped to use with the user environments only, if you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9b671-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b671-106">Prerequisites</span></span> 

<span data-ttu-id="9b671-107">Effectuez les étapes prérequises suivantes à partir du [Kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou à partir d’un client externe Windows si vous êtes [connecté par le biais d’un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) :</span><span class="sxs-lookup"><span data-stu-id="9b671-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="9b671-108">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="9b671-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="9b671-109">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="9b671-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a><span data-ttu-id="9b671-110">Configurer l’environnement de l’utilisateur et se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9b671-110">Configure the user environment and sign in to Azure Stack</span></span>

<span data-ttu-id="9b671-111">En fonction du type de déploiement (Azure AD ou AD FS), exécutez l’un des scripts suivants pour configurer PowerShell pour Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="9b671-111">Based on the type of deployment (Azure AD or AD FS), run one of the following script to configure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="9b671-112">Déploiements basés sur Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="9b671-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="9b671-113">Déploiements basés sur Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="9b671-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get the Active Directory tenantId that is used to deploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="9b671-114">Inscrire des fournisseurs de ressources</span><span class="sxs-lookup"><span data-stu-id="9b671-114">Register resource providers</span></span>

<span data-ttu-id="9b671-115">Quand il s’agit d’un abonnement utilisateur nouvellement créé qui n’a aucune ressource déployée par le biais du portail, les fournisseurs de ressources ne sont pas automatiquement inscrits.</span><span class="sxs-lookup"><span data-stu-id="9b671-115">When operating on a newly created user subscription that doesn’t have any resources deployed through the portal, the resource providers aren't automatically registered.</span></span> <span data-ttu-id="9b671-116">Vous devez les inscrire explicitement à l’aide du script suivant :</span><span class="sxs-lookup"><span data-stu-id="9b671-116">You should explicitly register them by using the following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a><span data-ttu-id="9b671-117">Tester la connectivité</span><span class="sxs-lookup"><span data-stu-id="9b671-117">Test the connectivity</span></span>

<span data-ttu-id="9b671-118">Nous avons terminé l’installation. Nous allons maintenant utiliser PowerShell pour créer des ressources dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9b671-118">Now that we've got everything set up, let's use PowerShell to create resources within Azure Stack.</span></span> <span data-ttu-id="9b671-119">Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b671-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="9b671-120">Utilisez la commande suivante pour créer le groupe de ressources nommé « myResourceGroup » :</span><span class="sxs-lookup"><span data-stu-id="9b671-120">Use the following command to create a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="9b671-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b671-121">Next steps</span></span>
* [<span data-ttu-id="9b671-122">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9b671-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="9b671-123">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b671-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
