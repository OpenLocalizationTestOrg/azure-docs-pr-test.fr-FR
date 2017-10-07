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
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a>Configurer l’environnement de l’opérateur hello pile d’Azure PowerShell

En tant qu’opérateur Azure Stack, vous pouvez configurer l’environnement PowerShell de votre Kit de développement Azure Stack. Après avoir configuré, vous pouvez utiliser de ressources Azure pile toomanage PowerShell telles que la création d’offres, les plans, les quotas, la gestion des alertes, etc.. Cette rubrique est étendue toouse avec l’opérateur de cloud hello environnements uniquement, si vous souhaitez tooset de PowerShell pour l’environnement utilisateur hello, reportez-vous trop[configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md) rubrique. 

## <a name="prerequisites"></a>Composants requis

Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn): 

* Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).  
* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a>Configurer l’environnement d’opérateur hello et connectez-vous à tooAzure pile

En fonction de type hello du déploiement (Azure AD ou AD FS), exécutez une des hello suivant script tooconfigure hello Azure opérateur environnement pile avec PowerShell :

### <a name="azure-active-directory-aad-based-deployments"></a>Déploiements basés sur Azure Active Directory (AAD)
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Déploiements basés sur Active Directory Federation Services (AD FS)
         
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

## <a name="test-hello-connectivity"></a>Tester la connectivité hello

Maintenant que nous avons tout configurer, nous allons utiliser de ressources au sein de la pile d’Azure PowerShell toocreate. Par exemple, vous pouvez créer un groupe de ressources pour une application et ajouter une machine virtuelle. Hello utilisation suivant commande toocreate un groupe de ressources nommé « MyResourceGroup » :

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Étapes suivantes
* [Développer des modèles pour Azure Stack](azure-stack-develop-templates.md)
* [Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)