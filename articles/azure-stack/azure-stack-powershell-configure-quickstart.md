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
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a>Devenez rapidement opérationnel avec PowerShell dans Azure Stack.

Cet article est un guide de démarrage rapide de tooinstall et configurer l’environnement de la pile d’Azure avec PowerShell. Ce script fourni dans cet article est étendue tooby hello **opérateur de pile de Azure** uniquement.

Cet article est une version condensée de salutation étapes de hello [installer PowerShell]( azure-stack-powershell-install.md), [télécharger les outils]( azure-stack-powershell-download.md), [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello]( azure-stack-powershell-configure-admin.md) articles. À l’aide de scripts de hello dans cette rubrique, vous pouvez configurer PowerShell pour les environnements Azure pile qui sont déployés avec Azure Active Directory ou Active Directory Federation Services.  


## <a name="set-up-powershell-for-aad-based-deployments"></a>Configurer PowerShell pour les déploiements basés sur AAD

Se connecter tooyour Kit de développement de pile Azure, ou un client externe basé sur Windows si vous êtes connecté via VPN. Ouvrez une session de PowerShell ISE avec élévation de privilèges et exécutez hello script suivant :

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

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a>Configurer PowerShell pour les déploiements basés sur AD FS 

Se connecter tooyour Kit de développement de pile Azure, ou un client externe basé sur Windows si vous êtes connecté via VPN. Ouvrez une session de PowerShell ISE avec élévation de privilèges et exécutez hello script suivant :

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

## <a name="test-hello-connectivity"></a>Tester la connectivité hello

Maintenant que vous avez configuré PowerShell, vous pouvez tester la configuration de hello en créant un groupe de ressources :

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

Lors de la création de groupe de ressources hello, sortie d’applet de commande hello hello Provisioning état propriété possède trop « réussi ».

## <a name="next-steps"></a>Étapes suivantes

* [Installer et configurer l’interface de ligne de commande](azure-stack-connect-cli.md)

* [Développer des modèles](azure-stack-develop-templates.md)







