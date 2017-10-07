---
title: aaaInstall et configurez PowerShell pour Azure pile quickstart | Documents Microsoft
description: "Découvrez comment installer et configurer PowerShell pour Azure Stack."
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
ms.openlocfilehash: bb0bed983a09e32dbaaa39159b1d6d8bae7ea690
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="1e43f-103">Devenez rapidement opérationnel avec PowerShell dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1e43f-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="1e43f-104">Cet article est un guide de démarrage rapide de tooinstall et configurer l’environnement de la pile d’Azure avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e43f-104">This article is a quick start tooinstall and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="1e43f-105">Ce script fourni dans cet article est étendue tooby hello **opérateur de pile de Azure** uniquement.</span><span class="sxs-lookup"><span data-stu-id="1e43f-105">This script provided in this article is scoped tooby hello **Azure Stack operator** only.</span></span>

<span data-ttu-id="1e43f-106">Cet article est une version condensée de salutation étapes de hello [installer PowerShell]( azure-stack-powershell-install.md), [télécharger les outils]( azure-stack-powershell-download.md), [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello]( azure-stack-powershell-configure-admin.md) articles.</span><span class="sxs-lookup"><span data-stu-id="1e43f-106">This article is a condensed version of hello steps described in hello [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure hello Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="1e43f-107">À l’aide de scripts de hello dans cette rubrique, vous pouvez configurer PowerShell pour les environnements Azure pile qui sont déployés avec Azure Active Directory ou Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="1e43f-107">By using hello scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="1e43f-108">Configurer PowerShell pour les déploiements basés sur AAD</span><span class="sxs-lookup"><span data-stu-id="1e43f-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="1e43f-109">Se connecter tooyour Kit de développement de pile Azure, ou un client externe basé sur Windows si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="1e43f-109">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="1e43f-110">Ouvrez une session de PowerShell ISE avec élévation de privilèges et exécutez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="1e43f-110">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="1e43f-111">Configurer PowerShell pour les déploiements basés sur AD FS</span><span class="sxs-lookup"><span data-stu-id="1e43f-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="1e43f-112">Se connecter tooyour Kit de développement de pile Azure, ou un client externe basé sur Windows si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="1e43f-112">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="1e43f-113">Ouvrez une session de PowerShell ISE avec élévation de privilèges et exécutez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="1e43f-113">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.local.azurestack.external/" `
  -EnableAdfsAuthentication:$true

$TenantID = Get-AzsDirectoryTenantId `
  -ADFS `
  -EnvironmentName "AzureStackAdmin"

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-hello-connectivity"></a><span data-ttu-id="1e43f-114">Tester la connectivité hello</span><span class="sxs-lookup"><span data-stu-id="1e43f-114">Test hello connectivity</span></span>

<span data-ttu-id="1e43f-115">Maintenant que vous avez configuré PowerShell, vous pouvez tester la configuration de hello en créant un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="1e43f-115">Now that you’ve configured PowerShell, you can test hello configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="1e43f-116">Lors de la création de groupe de ressources hello, sortie d’applet de commande hello hello Provisioning état propriété possède trop « réussi ».</span><span class="sxs-lookup"><span data-stu-id="1e43f-116">When hello resource group is created, hello cmdlet output has hello Provisioning state property set too"Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e43f-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e43f-117">Next steps</span></span>

* [<span data-ttu-id="1e43f-118">Installer et configurer l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="1e43f-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="1e43f-119">Développer des modèles</span><span class="sxs-lookup"><span data-stu-id="1e43f-119">Develop templates</span></span>](azure-stack-develop-templates.md)







