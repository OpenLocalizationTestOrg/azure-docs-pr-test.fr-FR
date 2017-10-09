---
title: "aaaUse hello Module de stratégie de pile Azure | Documents Microsoft"
description: "Découvrez comment tooconstrain un toobehave abonnement Azure qu’un abonnement Azure pile"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a><span data-ttu-id="c0df5-103">Gérer la stratégie Azure à l’aide de hello Module de stratégie de pile Azure</span><span class="sxs-lookup"><span data-stu-id="c0df5-103">Manage Azure policy using hello Azure Stack Policy Module</span></span>
<span data-ttu-id="c0df5-104">module de stratégie de pile Azure Hello vous permet de tooconfigure un abonnement Azure avec hello disponibilité même de contrôle de version et le service en tant que pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-104">hello Azure Stack Policy module allows you tooconfigure an Azure subscription with hello same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="c0df5-105">module de Hello utilise hello **New-AzureRMPolicyAssignment** toocreate de l’applet de commande une stratégie Azure, ce qui restreint les types de ressources hello et de services disponibles dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="c0df5-105">hello module uses hello **New-AzureRMPolicyAssignment** cmdlet toocreate an Azure policy, which limits hello resource types and services available in a subscription.</span></span>  <span data-ttu-id="c0df5-106">Une fois terminé, vous pouvez utiliser vos applications de toodevelop abonnement Azure ciblées pour la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-106">Once complete, you can use your Azure subscription toodevelop apps targeted for Azure Stack.</span></span>  

## <a name="install-hello-module"></a><span data-ttu-id="c0df5-107">Installer le module de hello</span><span class="sxs-lookup"><span data-stu-id="c0df5-107">Install hello module</span></span>
1. <span data-ttu-id="c0df5-108">Installer la version requise de hello Hello module AzureRM PowerShell, comme décrit dans l’étape 1 de [installer PowerShell pour Azure pile](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="c0df5-108">Install hello required version of hello AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="c0df5-109">Télécharger les outils de pile de Azure hello à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="c0df5-109">Download hello Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. [<span data-ttu-id="c0df5-110">Configurer PowerShell pour une utilisation avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c0df5-110">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md)

4. <span data-ttu-id="c0df5-111">Module d’importation hello AzureStack.Policy.psm1 :</span><span class="sxs-lookup"><span data-stu-id="c0df5-111">Import hello AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a><span data-ttu-id="c0df5-112">Appliquer la stratégie toosubscription</span><span class="sxs-lookup"><span data-stu-id="c0df5-112">Apply policy toosubscription</span></span>
<span data-ttu-id="c0df5-113">Hello commande suivante peut être tooapply utilisé une stratégie de la pile de Azure par défaut sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-113">hello following command can be used tooapply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="c0df5-114">Avant l’exécution, remplacez *Azure Subscription Name* par le nom de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a><span data-ttu-id="c0df5-115">Appliquer la stratégie de groupe de ressources tooa</span><span class="sxs-lookup"><span data-stu-id="c0df5-115">Apply policy tooa resource group</span></span>
<span data-ttu-id="c0df5-116">Vous souhaiterez peut-être tooapply des stratégies dans une méthode plus précise.</span><span class="sxs-lookup"><span data-stu-id="c0df5-116">You may want tooapply policies in a more granular method.</span></span>  <span data-ttu-id="c0df5-117">Par exemple, vous avez peut-être des autres ressources en cours d’exécution dans hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="c0df5-117">As an example, you may have other resources running in hello same subscription.</span></span>  <span data-ttu-id="c0df5-118">Vous pouvez définir l’étendue hello stratégie application tooa groupe de ressources spécifique, ce qui vous permet de tester vos applications pour la pile de Azure à l’aide de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-118">You can scope hello policy application tooa specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="c0df5-119">Avant l’exécution, remplacez *Azure Subscription Name* par le nom de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c0df5-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="c0df5-120">Stratégie en action</span><span class="sxs-lookup"><span data-stu-id="c0df5-120">Policy in action</span></span>
<span data-ttu-id="c0df5-121">Une fois que vous avez déployé hello stratégie Azure, vous recevez une erreur lorsque vous essayez de toodeploy une ressource interdite par la stratégie.</span><span class="sxs-lookup"><span data-stu-id="c0df5-121">Once you've deployed hello Azure policy, you receive an error when you try toodeploy a resource that prohibited by policy.</span></span>  

![Échec de déploiement de ressources en raison de la contrainte de stratégie](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="c0df5-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0df5-123">Next steps</span></span>
[<span data-ttu-id="c0df5-124">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0df5-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="c0df5-125">Déployer des modèles avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c0df5-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="c0df5-126">Déployer des modèles avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0df5-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
