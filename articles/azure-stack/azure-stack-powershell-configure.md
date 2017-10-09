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
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="f82ac-103">Configuration PowerShell pour une utilisation avec la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="f82ac-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="f82ac-104">Cet article décrit l’instance de Kit de développement Azure pile tooan hello étapes tooconnect requis à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f82ac-104">This article describes hello steps required tooconnect tooan Azure Stack Development Kit instance by using PowerShell.</span></span> <span data-ttu-id="f82ac-105">Une fois que vous vous connectez, vous pouvez accéder au portail de hello et déployer des ressources via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f82ac-105">After you connect, you can access hello portal and deploy resources through PowerShell.</span></span> <span data-ttu-id="f82ac-106">Vous pouvez utiliser les étapes de hello décrits dans cet article du kit de développement hello, soit à partir d’un client externe basé sur Windows, si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="f82ac-106">You can use hello steps described in this article either from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="f82ac-107">Cet article détaille tooconfigure d’instructions PowerShell pour Azure pile.</span><span class="sxs-lookup"><span data-stu-id="f82ac-107">This article has detailed instructions tooconfigure PowerShell for Azure Stack.</span></span> <span data-ttu-id="f82ac-108">Toutefois, si vous souhaitez tooquickly installer et configurez PowerShell, vous pouvez utiliser le script hello dans hello [obtenir en cours d’exécution avec PowerShell](azure-stack-powershell-configure-quickstart.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="f82ac-108">However, if you want tooquickly install and configure PowerShell, you can use hello script provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f82ac-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f82ac-109">Prerequisites</span></span>
* <span data-ttu-id="f82ac-110">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f82ac-110">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="f82ac-111">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="f82ac-111">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="import-hello-connect-powershell-module"></a><span data-ttu-id="f82ac-112">Module d’importation hello Connect PowerShell</span><span class="sxs-lookup"><span data-stu-id="f82ac-112">Import hello Connect PowerShell module</span></span>

<span data-ttu-id="f82ac-113">Après avoir téléchargé hello requis outils, accédez toohello téléchargé dossier et importer hello **Connect** module PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f82ac-113">After you download hello required tools, navigate toohello downloaded folder and import hello **Connect** PowerShell module.</span></span> <span data-ttu-id="f82ac-114">module de connexion hello tooimport, exécutez hello commande suivante dans une session PowerShell avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="f82ac-114">tooimport hello Connect module, run hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a><span data-ttu-id="f82ac-115">Configurer l’environnement PowerShell de hello</span><span class="sxs-lookup"><span data-stu-id="f82ac-115">Configure hello PowerShell environment</span></span>

<span data-ttu-id="f82ac-116">tooconfigure votre environnement Azure pile, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f82ac-116">tooconfigure your Azure Stack environment, do hello following:</span></span>

1. <span data-ttu-id="f82ac-117">Inscrire un environnement Azure Resource Manager qui cible votre instance de la pile d’Azure à l’aide d’une des hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="f82ac-117">Register an AzureRM environment that targets your Azure Stack instance by using one of hello following cmdlets:</span></span>

   * <span data-ttu-id="f82ac-118">**Environnement d’administration de cloud**</span><span class="sxs-lookup"><span data-stu-id="f82ac-118">**Cloud administrative environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * <span data-ttu-id="f82ac-119">**Environnement de l’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="f82ac-119">**User environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   <span data-ttu-id="f82ac-120">Une fois que vous avez enregistré l’environnement d’Azure Resource Manager hello, vous pouvez utiliser toutes les applets de commande hello Azure Resource Manager dans votre environnement de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="f82ac-120">After you've registered hello AzureRM environment, you can use all hello AzureRM cmdlets in your Azure Stack environment.</span></span> <span data-ttu-id="f82ac-121">Hello d’applet de commande précédente hello est affiché dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="f82ac-121">hello output of hello previous cmdlet is shown in hello following screenshot:</span></span>

   ![Obtenir les détails de l’environnement](media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="f82ac-123">Définissez la valeur de GraphEndpointResourceId de hello en utilisant l’une de hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="f82ac-123">Set hello GraphEndpointResourceId value by using one of hello following cmdlets:</span></span>
   
   * <span data-ttu-id="f82ac-124">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="f82ac-124">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="f82ac-125">Pourquoi **environnement d’administration de cloud**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-125">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * <span data-ttu-id="f82ac-126">Pourquoi **l’environnement utilisateur**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-126">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * <span data-ttu-id="f82ac-127">**Active Directory Federation Services**</span><span class="sxs-lookup"><span data-stu-id="f82ac-127">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="f82ac-128">Pourquoi **environnement d’administration de cloud**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-128">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * <span data-ttu-id="f82ac-129">Pourquoi **l’environnement utilisateur**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-129">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. <span data-ttu-id="f82ac-130">Obtenir la valeur GUID hello du client Active Directory hello qui est utilisé toodeploy pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f82ac-130">Get hello GUID value of hello Active Directory tenant that is used toodeploy Azure Stack.</span></span> <span data-ttu-id="f82ac-131">Si votre environnement Azure pile est déployé à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="f82ac-131">If your Azure Stack environment is deployed by using:</span></span>  

   * <span data-ttu-id="f82ac-132">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="f82ac-132">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="f82ac-133">tooaccess hello **environnement d’administration de cloud**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-133">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="f82ac-134">tooaccess hello **l’environnement utilisateur**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-134">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * <span data-ttu-id="f82ac-135">**Active Directory Federation Services**</span><span class="sxs-lookup"><span data-stu-id="f82ac-135">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="f82ac-136">tooaccess hello **environnement d’administration de cloud**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-136">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="f82ac-137">tooaccess hello **l’environnement utilisateur**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-137">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a><span data-ttu-id="f82ac-138">Connectez-vous à tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="f82ac-138">Sign in tooAzure Stack</span></span>

<span data-ttu-id="f82ac-139">La connexion toohello environnement Azure pile à l’aide d’une des hello suivant deux applets de commande :</span><span class="sxs-lookup"><span data-stu-id="f82ac-139">Sign in toohello Azure Stack environment by using one of hello following two cmdlets:</span></span>

   * <span data-ttu-id="f82ac-140">toosign dans toohello **portail administratif**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-140">toosign in toohello **administrative portal**, use:</span></span>
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * <span data-ttu-id="f82ac-141">toosign dans toohello **portail de l’utilisateur**, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f82ac-141">toosign in toohello **user portal**, use:</span></span>

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a><span data-ttu-id="f82ac-142">Inscrire des fournisseurs de ressources</span><span class="sxs-lookup"><span data-stu-id="f82ac-142">Register resource providers</span></span>

<span data-ttu-id="f82ac-143">Après que vous être connecté dans le portail d’administrateur ou utilisateur toohello, vous pouvez émettre des opérations sur les fournisseurs de ressources hello inscrit.</span><span class="sxs-lookup"><span data-stu-id="f82ac-143">After you sign in toohello administrator or user portal, you can issue operations against hello registered resource providers.</span></span> <span data-ttu-id="f82ac-144">Par défaut, tous les fournisseurs de ressources fondamentaux hello sont inscrits dans hello abonnement du fournisseur par défaut (abonnement de l’administrateur de cloud hello).</span><span class="sxs-lookup"><span data-stu-id="f82ac-144">By default, all hello foundational resource providers are registered in hello Default Provider Subscription (hello cloud administrator's subscription).</span></span>

<span data-ttu-id="f82ac-145">Lorsque vous travaillez sur un abonnement de l’utilisateur nouvellement créé, qui n’a pas toutes les ressources déployées via le portail de hello, les fournisseurs de ressources hello ne sont pas enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f82ac-145">When you operate on a newly created user subscription, which doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="f82ac-146">Vous devez explicitement inscrire des fournisseurs de ressources hello à l’aide de hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="f82ac-146">You should explicitly register hello resource providers by using hello following script:</span></span>

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a><span data-ttu-id="f82ac-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f82ac-147">Next steps</span></span>
* [<span data-ttu-id="f82ac-148">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f82ac-148">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="f82ac-149">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f82ac-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
