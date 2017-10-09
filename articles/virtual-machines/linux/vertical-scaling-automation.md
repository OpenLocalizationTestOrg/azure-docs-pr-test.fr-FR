---
title: "montée en puissance aaaVertically machine virtuelle Azure avec Azure Automation | Documents Microsoft"
description: "Comment toovertically l’échelle d’une Machine virtuelle Linux dans les alertes de réponse de toomonitoring avec Azure Automation"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="dec1e-103">Évolution verticale des machines virtuelles Linux Azure avec Azure Automation</span><span class="sxs-lookup"><span data-stu-id="dec1e-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="dec1e-104">Mise à l’échelle verticale consiste hello croissantes ou décroissantes ressources hello d’un ordinateur dans la charge de travail de réponse toohello.</span><span class="sxs-lookup"><span data-stu-id="dec1e-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="dec1e-105">Dans Azure, cela peut être accompli en modifiant la taille de hello Hello Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dec1e-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="dec1e-106">Cela peut vous aider dans les scénarios suivants de hello</span><span class="sxs-lookup"><span data-stu-id="dec1e-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="dec1e-107">Si hello Machine virtuelle n’est pas utilisé fréquemment, vous pouvez la redimensionner vers le bas tooa plus petite taille tooreduce vos coûts mensuels</span><span class="sxs-lookup"><span data-stu-id="dec1e-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="dec1e-108">Si hello Machine virtuelle voit une charge de pointe, il peut être redimensionné tooa plus grande taille tooincrease sa capacité maximale</span><span class="sxs-lookup"><span data-stu-id="dec1e-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="dec1e-109">plan Hello pour tooaccomplish d’étapes hello il s’agit en tant que ci-dessous</span><span class="sxs-lookup"><span data-stu-id="dec1e-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="dec1e-110">Le programme d’installation Azure Automation tooaccess vos Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dec1e-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="dec1e-111">Importer des procédures opérationnelles de l’échelle verticale de Azure Automation hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="dec1e-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="dec1e-112">Ajouter un runbook de tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="dec1e-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="dec1e-113">Ajouter une alerte tooyour Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dec1e-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="dec1e-114">En raison de la taille de hello Hello première Machine virtuelle, tailles hello à l’échelle, peut être limitée en raison de la disponibilité toohello Hello autres tailles de cluster de hello actuel ordinateur virtuel est déployé dans.</span><span class="sxs-lookup"><span data-stu-id="dec1e-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="dec1e-115">Bonjour publiées de runbook automation utilisés dans cet article nous prendre en charge ce cas et uniquement l’échelle dans hello ci-dessous paires de taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dec1e-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="dec1e-116">Cela signifie qu’un ordinateur virtuel de Standard_D1v2 ne sera pas soudainement mis à l’échelle tooStandard_G5 ou la descente tooBasic_A0.</span><span class="sxs-lookup"><span data-stu-id="dec1e-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="dec1e-117">Paires de mise à l’échelle des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dec1e-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="dec1e-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="dec1e-118">Basic_A0</span></span> |<span data-ttu-id="dec1e-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="dec1e-119">Basic_A4</span></span> |
> | <span data-ttu-id="dec1e-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="dec1e-120">Standard_A0</span></span> |<span data-ttu-id="dec1e-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="dec1e-121">Standard_A4</span></span> |
> | <span data-ttu-id="dec1e-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="dec1e-122">Standard_A5</span></span> |<span data-ttu-id="dec1e-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="dec1e-123">Standard_A7</span></span> |
> | <span data-ttu-id="dec1e-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="dec1e-124">Standard_A8</span></span> |<span data-ttu-id="dec1e-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="dec1e-125">Standard_A9</span></span> |
> | <span data-ttu-id="dec1e-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="dec1e-126">Standard_A10</span></span> |<span data-ttu-id="dec1e-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="dec1e-127">Standard_A11</span></span> |
> | <span data-ttu-id="dec1e-128">D1 standard</span><span class="sxs-lookup"><span data-stu-id="dec1e-128">Standard_D1</span></span> |<span data-ttu-id="dec1e-129">D4 standard</span><span class="sxs-lookup"><span data-stu-id="dec1e-129">Standard_D4</span></span> |
> | <span data-ttu-id="dec1e-130">D11 standard</span><span class="sxs-lookup"><span data-stu-id="dec1e-130">Standard_D11</span></span> |<span data-ttu-id="dec1e-131">D14 standard</span><span class="sxs-lookup"><span data-stu-id="dec1e-131">Standard_D14</span></span> |
> | <span data-ttu-id="dec1e-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="dec1e-132">Standard_DS1</span></span> |<span data-ttu-id="dec1e-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="dec1e-133">Standard_DS4</span></span> |
> | <span data-ttu-id="dec1e-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="dec1e-134">Standard_DS11</span></span> |<span data-ttu-id="dec1e-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="dec1e-135">Standard_DS14</span></span> |
> | <span data-ttu-id="dec1e-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="dec1e-136">Standard_D1v2</span></span> |<span data-ttu-id="dec1e-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="dec1e-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="dec1e-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="dec1e-138">Standard_D11v2</span></span> |<span data-ttu-id="dec1e-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="dec1e-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="dec1e-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="dec1e-140">Standard_G1</span></span> |<span data-ttu-id="dec1e-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="dec1e-141">Standard_G5</span></span> |
> | <span data-ttu-id="dec1e-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="dec1e-142">Standard_GS1</span></span> |<span data-ttu-id="dec1e-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="dec1e-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="dec1e-144">Le programme d’installation Azure Automation tooaccess vos Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dec1e-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="dec1e-145">Hello première chose toodo consiste à créer un compte Azure Automation qui hébergera hello procédures opérationnelles utilisé tooscale hello instances ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dec1e-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="dec1e-146">Récemment service d’automatisation hello introduit la fonctionnalité « Exécuter en tant que compte » hello qui rend la hello Principal du Service pour l’exécution automatique des procédures opérationnelles de hello sur hello utilisateur très facile.</span><span class="sxs-lookup"><span data-stu-id="dec1e-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="dec1e-147">Vous pouvez en savoir plus à ce sujet dans l’article hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dec1e-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="dec1e-148">Authentifier des Runbooks avec un compte d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="dec1e-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="dec1e-149">Importer des procédures opérationnelles de l’échelle verticale de Azure Automation hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="dec1e-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="dec1e-150">Hello procédures opérationnelles qui sont nécessaires pour la mise à l’échelle verticalement votre Machine virtuelle sont déjà publiés dans hello galerie de runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dec1e-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="dec1e-151">Vous devez tooimport dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="dec1e-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="dec1e-152">Vous pouvez apprendre comment runbooks tooimport en lisant hello article suivant.</span><span class="sxs-lookup"><span data-stu-id="dec1e-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="dec1e-153">Galeries de runbooks et de modules pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="dec1e-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="dec1e-154">procédures opérationnelles Hello nécessitant toobe importé sont affichés dans image hello ci-dessous</span><span class="sxs-lookup"><span data-stu-id="dec1e-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importer des runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="dec1e-156">Ajouter un runbook de tooyour webhook</span><span class="sxs-lookup"><span data-stu-id="dec1e-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="dec1e-157">Une fois que vous avez importé les runbooks hello, vous devez tooadd un runbook de toohello webhook afin qu’elle peut être déclenchée par une alerte à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="dec1e-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="dec1e-158">Détails de Hello de création d’un webhook pour votre Runbook peuvent être lu ici</span><span class="sxs-lookup"><span data-stu-id="dec1e-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="dec1e-159">Webhooks Azure Automation</span><span class="sxs-lookup"><span data-stu-id="dec1e-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="dec1e-160">Assurez-vous que vous copiez hello webhook avant de fermer la boîte de dialogue hello webhook car vous en aurez besoin dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="dec1e-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="dec1e-161">Ajouter une alerte tooyour Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dec1e-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="dec1e-162">Sélectionnez les paramètres des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dec1e-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="dec1e-163">Sélectionnez Règles d’alerte</span><span class="sxs-lookup"><span data-stu-id="dec1e-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="dec1e-164">Sélectionnez Ajouter une alerte</span><span class="sxs-lookup"><span data-stu-id="dec1e-164">Select "Add alert"</span></span>
4. <span data-ttu-id="dec1e-165">Sélectionnez une alerte de hello métrique toofire sur</span><span class="sxs-lookup"><span data-stu-id="dec1e-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="dec1e-166">Sélectionnez une condition, où remplies va entraîner toofire d’alerte hello</span><span class="sxs-lookup"><span data-stu-id="dec1e-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="dec1e-167">Sélectionnez un seuil pour la condition de hello à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="dec1e-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="dec1e-168">toobe remplie</span><span class="sxs-lookup"><span data-stu-id="dec1e-168">toobe fulfilled</span></span>
7. <span data-ttu-id="dec1e-169">Sélectionnez une période sur quel hello service d’analyse vérifie pour la condition de hello et le seuil dans les étapes 5 et 6</span><span class="sxs-lookup"><span data-stu-id="dec1e-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="dec1e-170">Collez webhook hello copié à partir de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="dec1e-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Ajouter des alerte tooVirtual Machine 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Ajouter des alerte tooVirtual ordinateur 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

