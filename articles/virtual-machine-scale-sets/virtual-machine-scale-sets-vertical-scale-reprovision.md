---
title: "aaaVertically groupes identiques de mise à l’échelle de machine virtuelle Azure | Documents Microsoft"
description: "Comment toovertically l’échelle d’un ordinateur virtuel dans les alertes de réponse de toomonitoring avec Azure Automation"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="f2302-103">Mise à l’échelle verticale avec des jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f2302-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="f2302-104">Cet article décrit comment toovertically l’échelle Azure [machines virtuelles identiques](https://azure.microsoft.com/services/virtual-machine-scale-sets/) avec ou sans la préparation.</span><span class="sxs-lookup"><span data-stu-id="f2302-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="f2302-105">Vertical mise à l’échelle de machines virtuelles qui ne sont pas identiques, consultez trop[évolution verticale de machine virtuelle Azure avec Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2302-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f2302-106">Échelle verticale, également appelé *montée en puissance* et *à l’échelle*, moyens en augmentant ou en réduisant les tailles de machine virtuelle (VM) dans la charge de travail de réponse tooa.</span><span class="sxs-lookup"><span data-stu-id="f2302-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="f2302-107">Comparez cela avec [mise à l’échelle horizontale](virtual-machine-scale-sets-autoscale-overview.md), également appelée tooas *montée en puissance parallèle* et *l’échelle en*, où le nombre hello d’ordinateurs virtuels est modifiée en fonction de la charge de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f2302-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="f2302-108">Le terme « réapprovisionner » signifie supprimer une machine virtuelle et la remplacer par une autre.</span><span class="sxs-lookup"><span data-stu-id="f2302-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="f2302-109">Lorsque vous augmentez ou réduisez la taille des machines virtuelles sur un ensemble d’échelle de machines virtuelles de hello, dans certains cas vous souhaitez tooresize existant de machines virtuelles et conserver vos données, alors que dans d’autres cas, vous devez toodeploy nouvelles machines virtuelles de taille de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="f2302-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="f2302-110">Ce document couvre les deux cas de figure.</span><span class="sxs-lookup"><span data-stu-id="f2302-110">This document covers both cases.</span></span>

<span data-ttu-id="f2302-111">La mise à l’échelle verticale peut être utile dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="f2302-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="f2302-112">Sous-utilisation d’un service résidant sur des machines virtuelles (par exemple, le week-end).</span><span class="sxs-lookup"><span data-stu-id="f2302-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="f2302-113">La réduction de taille de machine virtuelle hello peut réduire les coûts mensuels.</span><span class="sxs-lookup"><span data-stu-id="f2302-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="f2302-114">Augmentation toocope taille de machine virtuelle avec la plus grande à la demande sans créer des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f2302-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="f2302-115">Vous pouvez configurer vertical mise à l’échelle toobe déclenchée selon des métriques alertes en fonction de votre jeu de mise à l’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2302-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="f2302-116">Alerte de hello est activé se déclenche un webhook déclenchant un runbook qui peut s’ajuster votre échelle défini vers le haut ou vers le bas.</span><span class="sxs-lookup"><span data-stu-id="f2302-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="f2302-117">La mise à l’échelle verticale peut être configurée comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2302-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="f2302-118">Créez un compte Azure Automation avec fonctionnalité d’identification.</span><span class="sxs-lookup"><span data-stu-id="f2302-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="f2302-119">Importez les runbooks de mise à l’échelle verticale Azure Automation dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2302-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="f2302-120">Ajouter un runbook de tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="f2302-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="f2302-121">Ajouter une alerte tooyour ensemble d’échelle de machine virtuelle à l’aide d’une notification de webhook.</span><span class="sxs-lookup"><span data-stu-id="f2302-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="f2302-122">La mise à l’échelle verticale ne peut s’effectuer que sur des machines virtuelles d’une certaine taille.</span><span class="sxs-lookup"><span data-stu-id="f2302-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="f2302-123">Comparer les spécifications de hello de chaque taille avant de décider de tooscale à partir d’un tooanother (nombre plus élevé n’indique pas toujours plus grande taille de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="f2302-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="f2302-124">Vous pouvez choisir tooscale entre hello suivant des paires de taille :</span><span class="sxs-lookup"><span data-stu-id="f2302-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="f2302-125">Paires de mise à l’échelle des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f2302-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="f2302-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="f2302-126">Standard_A0</span></span> |<span data-ttu-id="f2302-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="f2302-127">Standard_A11</span></span> |
> | <span data-ttu-id="f2302-128">D1 standard</span><span class="sxs-lookup"><span data-stu-id="f2302-128">Standard_D1</span></span> |<span data-ttu-id="f2302-129">D14 standard</span><span class="sxs-lookup"><span data-stu-id="f2302-129">Standard_D14</span></span> |
> | <span data-ttu-id="f2302-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="f2302-130">Standard_DS1</span></span> |<span data-ttu-id="f2302-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="f2302-131">Standard_DS14</span></span> |
> | <span data-ttu-id="f2302-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="f2302-132">Standard_D1v2</span></span> |<span data-ttu-id="f2302-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="f2302-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="f2302-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="f2302-134">Standard_G1</span></span> |<span data-ttu-id="f2302-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="f2302-135">Standard_G5</span></span> |
> | <span data-ttu-id="f2302-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="f2302-136">Standard_GS1</span></span> |<span data-ttu-id="f2302-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="f2302-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="f2302-138">Créer un compte Azure Automation avec fonctionnalité d’identification</span><span class="sxs-lookup"><span data-stu-id="f2302-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="f2302-139">Hello première chose toodo consiste à créer un compte Azure Automation qui hébergera hello procédures opérationnelles utilisé tooscale hello instances ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2302-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="f2302-140">Récemment [Azure Automation](https://azure.microsoft.com/services/automation/) a introduit la fonctionnalité « Exécuter en tant que compte » hello qui rend la hello Principal du Service pour en exécutant automatiquement les runbooks hello au nom d’un utilisateur très facile.</span><span class="sxs-lookup"><span data-stu-id="f2302-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="f2302-141">Vous pouvez en savoir plus à ce sujet dans l’article hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f2302-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="f2302-142">Authentifier des Runbooks avec un compte d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="f2302-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="f2302-143">Importer les runbooks de mise à l’échelle verticale Azure Automation dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="f2302-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="f2302-144">les runbooks Hello nécessaire échelle toovertically que vos jeux de mise à l’échelle de machine virtuelle sont déjà publiés dans hello galerie de runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f2302-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="f2302-145">les étapes tooimport dans votre abonnement suivent hello dans cet article :</span><span class="sxs-lookup"><span data-stu-id="f2302-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="f2302-146">Galeries de runbooks et de modules pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f2302-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="f2302-147">Choisissez option Parcourir la galerie de hello hello procédures opérationnelles :</span><span class="sxs-lookup"><span data-stu-id="f2302-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe runbooks importé][runbooks]

<span data-ttu-id="f2302-149">procédures opérationnelles Hello nécessitant toobe importé sont affichés.</span><span class="sxs-lookup"><span data-stu-id="f2302-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="f2302-150">Sélectionnez le runbook hello selon si vous souhaitez que verticales mise à l’échelle avec ou sans la préparation :</span><span class="sxs-lookup"><span data-stu-id="f2302-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galerie de runbooks][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="f2302-152">Ajouter un runbook de tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="f2302-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="f2302-153">Une fois que vous avez importé les runbooks hello, vous devez tooadd un runbook de toohello webhook afin qu’elle peut être déclenchée par une alerte à partir d’un ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2302-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="f2302-154">Détails de Hello de création d’un webhook pour votre Runbook sont décrites dans cet article :</span><span class="sxs-lookup"><span data-stu-id="f2302-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="f2302-155">Webhooks Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f2302-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="f2302-156">Assurez-vous que vous copiez hello webhook URI avant de fermer la boîte de dialogue hello webhook car vous en aurez besoin dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="f2302-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="f2302-157">Ajouter une alerte tooyour ensemble d’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f2302-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="f2302-158">Voici un PowerShell script qui montre comment tooadd une alerte tooa ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f2302-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="f2302-159">Consultez toohello suivant le nom de hello article tooget d’alerte de hello hello toofire métrique de : [mesures courantes de moniteur Azure échelle](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f2302-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="f2302-160">Il est recommandé de tooconfigure une fenêtre de temps raisonnable pour l’alerte hello dans tooavoid commande déclencher la mise à l’échelle verticale, et les associés interruption de service, trop souvent.</span><span class="sxs-lookup"><span data-stu-id="f2302-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="f2302-161">Envisagez une période d’au moins 20 à 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="f2302-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="f2302-162">Envisagez horizontal mise à l’échelle si vous avez besoin tooavoid toute interruption.</span><span class="sxs-lookup"><span data-stu-id="f2302-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="f2302-163">Pour plus d’informations sur comment toocreate alertes référence toohello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="f2302-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="f2302-164">Exemples de démarrage rapide Azure Monitor PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2302-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="f2302-165">Exemple de démarrage rapide de l’interface CLI multiplateforme Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f2302-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="f2302-166">Résumé</span><span class="sxs-lookup"><span data-stu-id="f2302-166">Summary</span></span>
<span data-ttu-id="f2302-167">Cet article vous a montré des exemples simples de mise à l’échelle verticale.</span><span class="sxs-lookup"><span data-stu-id="f2302-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="f2302-168">Grâce à ces éléments (compte Automation, runbooks, webhooks et alertes), vous pouvez connecter des événements très différents à un jeu d’actions personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f2302-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
