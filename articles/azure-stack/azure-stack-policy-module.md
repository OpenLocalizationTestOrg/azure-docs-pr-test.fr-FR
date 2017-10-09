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
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a>Gérer la stratégie Azure à l’aide de hello Module de stratégie de pile Azure
module de stratégie de pile Azure Hello vous permet de tooconfigure un abonnement Azure avec hello disponibilité même de contrôle de version et le service en tant que pile d’Azure.  module de Hello utilise hello **New-AzureRMPolicyAssignment** toocreate de l’applet de commande une stratégie Azure, ce qui restreint les types de ressources hello et de services disponibles dans un abonnement.  Une fois terminé, vous pouvez utiliser vos applications de toodevelop abonnement Azure ciblées pour la pile de Azure.  

## <a name="install-hello-module"></a>Installer le module de hello
1. Installer la version requise de hello Hello module AzureRM PowerShell, comme décrit dans l’étape 1 de [installer PowerShell pour Azure pile](azure-stack-powershell-install.md).   
2. [Télécharger les outils de pile de Azure hello à partir de GitHub](azure-stack-powershell-download.md)  
3. [Configurer PowerShell pour une utilisation avec Azure Stack](azure-stack-powershell-configure-user.md)

4. Module d’importation hello AzureStack.Policy.psm1 :

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a>Appliquer la stratégie toosubscription
Hello commande suivante peut être tooapply utilisé une stratégie de la pile de Azure par défaut sur votre abonnement Azure. Avant l’exécution, remplacez *Azure Subscription Name* par le nom de votre abonnement Azure.

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a>Appliquer la stratégie de groupe de ressources tooa
Vous souhaiterez peut-être tooapply des stratégies dans une méthode plus précise.  Par exemple, vous avez peut-être des autres ressources en cours d’exécution dans hello même abonnement.  Vous pouvez définir l’étendue hello stratégie application tooa groupe de ressources spécifique, ce qui vous permet de tester vos applications pour la pile de Azure à l’aide de ressources Azure. Avant l’exécution, remplacez *Azure Subscription Name* par le nom de votre abonnement Azure.

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a>Stratégie en action
Une fois que vous avez déployé hello stratégie Azure, vous recevez une erreur lorsque vous essayez de toodeploy une ressource interdite par la stratégie.  

![Échec de déploiement de ressources en raison de la contrainte de stratégie](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a>Étapes suivantes
[Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)

[Déployer des modèles avec l’interface de ligne de commande Azure](azure-stack-deploy-template-command-line.md)

[Déployer des modèles avec Visual Studio](azure-stack-deploy-template-visual-studio.md)
