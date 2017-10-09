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
# <a name="configure-hello-azure-stack-users-powershell-environment"></a>Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell

En tant qu’utilisateur d’Azure Stack, vous pouvez configurer l’environnement PowerShell de votre Kit de développement Azure Stack. Après avoir configuré, vous pouvez utiliser PowerShell toomanage des ressources de pile de Azure telles que s’abonner toooffers, créer des ordinateurs virtuels, déployer des modèles Azure Resource Manager, etc.. Cette rubrique est toouse étendue avec les environnements hello utilisateur uniquement, si vous souhaitez tooset de PowerShell pour l’environnement d’opérateur hello cloud, consultez toohello [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello](azure-stack-powershell-configure-admin.md) rubrique. 

## <a name="prerequisites"></a>Composants requis 

Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).  
* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md). 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a>Configuration de l’environnement utilisateur hello et la connexion tooAzure pile

En fonction de type hello du déploiement (Azure AD ou AD FS), exécutez une des hello suivant tooconfigure de script PowerShell pour Azure pile :

### <a name="azure-active-directory-aad-based-deployments"></a>Déploiements basés sur Azure Active Directory (AAD)
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Déploiements basés sur Active Directory Federation Services (AD FS) 
          
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

## <a name="register-resource-providers"></a>Inscrire des fournisseurs de ressources

Lorsqu’il fonctionne sur un abonnement de l’utilisateur nouvellement créé qui ne contient aucune ressource déployée via le portail de hello, les fournisseurs de ressources hello ne sont pas enregistrés automatiquement. Vous devez les inscrire explicitement à l’aide de hello script suivant :

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a>Tester la connectivité hello

Maintenant que nous avons tout configurer, nous allons utiliser de ressources au sein de la pile d’Azure PowerShell toocreate. Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle. Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Étapes suivantes
* [Développer des modèles pour Azure Stack](azure-stack-develop-templates.md)
* [Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)
