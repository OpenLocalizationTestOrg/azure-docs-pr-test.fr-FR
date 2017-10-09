---
title: aaaConfigure PowerShell pour une utilisation avec la pile de Azure | Documents Microsoft
description: "Découvrez comment tooconfigure PowerShell pour Azure pile."
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
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a>Configuration PowerShell pour une utilisation avec la pile de Azure 

Cet article décrit l’instance de Kit de développement Azure pile tooan hello étapes tooconnect requis à l’aide de PowerShell. Une fois que vous vous connectez, vous pouvez accéder au portail de hello et déployer des ressources via PowerShell. Vous pouvez utiliser les étapes de hello décrits dans cet article du kit de développement hello, soit à partir d’un client externe basé sur Windows, si vous êtes connecté via VPN.

Cet article détaille tooconfigure d’instructions PowerShell pour Azure pile. Toutefois, si vous souhaitez tooquickly installer et configurez PowerShell, vous pouvez utiliser le script hello dans hello [obtenir en cours d’exécution avec PowerShell](azure-stack-powershell-configure-quickstart.md) rubrique. 

## <a name="prerequisites"></a>Composants requis
* Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).  
* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).  

## <a name="import-hello-connect-powershell-module"></a>Module d’importation hello Connect PowerShell

Après avoir téléchargé hello requis outils, accédez toohello téléchargé dossier et importer hello **Connect** module PowerShell. module de connexion hello tooimport, exécutez hello commande suivante dans une session PowerShell avec élévation de privilèges :

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a>Configurer l’environnement PowerShell de hello

tooconfigure votre environnement Azure pile, hello suivant :

1. Inscrire un environnement Azure Resource Manager qui cible votre instance de la pile d’Azure à l’aide d’une des hello suivant d’applets de commande :

   * **Environnement d’administration de cloud**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * **Environnement de l’utilisateur**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   Une fois que vous avez enregistré l’environnement d’Azure Resource Manager hello, vous pouvez utiliser toutes les applets de commande hello Azure Resource Manager dans votre environnement de la pile de Azure. Hello d’applet de commande précédente hello est affiché dans hello suivant capture d’écran :

   ![Obtenir les détails de l’environnement](media/azure-stack-powershell-configure/getenvdetails.png)

2. Définissez la valeur de GraphEndpointResourceId de hello en utilisant l’une de hello suivant d’applets de commande :
   
   * **Azure Active Directory (Azure AD)**
   
      * Pourquoi **environnement d’administration de cloud**, utilisez :
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * Pourquoi **l’environnement utilisateur**, utilisez :
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * **Active Directory Federation Services**
   
      * Pourquoi **environnement d’administration de cloud**, utilisez :
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * Pourquoi **l’environnement utilisateur**, utilisez :
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. Obtenir la valeur GUID hello du client Active Directory hello qui est utilisé toodeploy pile d’Azure. Si votre environnement Azure pile est déployé à l’aide de :  

   * **Azure Active Directory (Azure AD)**
   
      * tooaccess hello **environnement d’administration de cloud**, utilisez :
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello **l’environnement utilisateur**, utilisez :
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * **Active Directory Federation Services**
   
      * tooaccess hello **environnement d’administration de cloud**, utilisez :
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello **l’environnement utilisateur**, utilisez :
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a>Connectez-vous à tooAzure pile

La connexion toohello environnement Azure pile à l’aide d’une des hello suivant deux applets de commande :

   * toosign dans toohello **portail administratif**, utilisez :
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * toosign dans toohello **portail de l’utilisateur**, utilisez :

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a>Inscrire des fournisseurs de ressources

Après que vous être connecté dans le portail d’administrateur ou utilisateur toohello, vous pouvez émettre des opérations sur les fournisseurs de ressources hello inscrit. Par défaut, tous les fournisseurs de ressources fondamentaux hello sont inscrits dans hello abonnement du fournisseur par défaut (abonnement de l’administrateur de cloud hello).

Lorsque vous travaillez sur un abonnement de l’utilisateur nouvellement créé, qui n’a pas toutes les ressources déployées via le portail de hello, les fournisseurs de ressources hello ne sont pas enregistrés automatiquement. Vous devez explicitement inscrire des fournisseurs de ressources hello à l’aide de hello script suivant :

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a>Étapes suivantes
* [Développer des modèles pour Azure Stack](azure-stack-develop-templates.md)
* [Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)
