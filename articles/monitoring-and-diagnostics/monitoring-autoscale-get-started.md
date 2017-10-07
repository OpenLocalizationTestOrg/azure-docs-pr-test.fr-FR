---
title: "aaaGet main de la mise à l’échelle dans Azure | Documents Microsoft"
description: "Découvrez comment tooscale vos ressources dans Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="bcd9e-103">Bien démarrer avec la mise à l’échelle automatique dans Azure</span><span class="sxs-lookup"><span data-stu-id="bcd9e-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="bcd9e-104">Cet article décrit comment tooset vos paramètres de mise à l’échelle pour votre ressource dans le portail de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="bcd9e-105">Azure moniteur de mise à l’échelle s’applique uniquement toovirtual machines identiques, services de cloud computing, les plans de Service d’applications Azure et les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="bcd9e-106">Découvrir les paramètres de mise à l’échelle hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="bcd9e-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="bcd9e-107">Vous pouvez découvrir toutes les ressources hello pour lesquels la mise à l’échelle est applicable dans le moniteur de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="bcd9e-108">Utilisez hello pour une procédure pas à pas comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcd9e-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="bcd9e-109">Ouvrez hello [portail Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="bcd9e-110">Cliquez sur icône du moniteur de Windows Azure hello dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="bcd9e-111">![Ouvrez Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="bcd9e-112">Cliquez sur **mise à l’échelle** tooview toutes les ressources de hello pour le mise à l’échelle n’est applicable, ainsi que leur état actuel de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="bcd9e-113">![Découvrir la mise à l’échelle automatique dans Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="bcd9e-114">Vous pouvez utiliser le volet de filtre hello à tooscope supérieur de hello vers le bas des ressources de tooselect liste hello dans un groupe de ressources spécifique, les types de ressource spécifique ou une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="bcd9e-115">Pour chaque ressource, vous trouverez du nombre d’instances actuelles hello et l’état de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="bcd9e-116">Hello état de mise à l’échelle peut être :</span><span class="sxs-lookup"><span data-stu-id="bcd9e-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="bcd9e-117">**Non configuré** : vous n’avez pas encore activé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="bcd9e-118">**Activé** : vous avez activé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="bcd9e-119">**Désactivé** : vous avez désactivé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="bcd9e-120">Créez votre premier paramètre de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="bcd9e-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="bcd9e-121">Nous allons maintenant passer par un toocreate simple de procédure pas à pas le premier paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="bcd9e-122">Ouvrez hello **mise à l’échelle** panneau dans le moniteur de Windows Azure et sélectionnez une ressource que vous souhaitez tooscale.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="bcd9e-123">(hello étapes suivantes utilisent un plan App Service associé à une application web.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="bcd9e-124">Vous pouvez [créer votre première application Web ASP.NET dans Azure en 5 minutes][4])</span><span class="sxs-lookup"><span data-stu-id="bcd9e-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="bcd9e-125">Notez que le nombre d’instances actuelles hello est 1.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="bcd9e-126">Cliquez sur **Activer la mise à l’échelle automatique**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="bcd9e-127">![Paramètre d’échelle pour la nouvelle application web][5]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="bcd9e-128">Fournissez un nom pour le paramètre d’échelle de hello, puis cliquez sur **ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="bcd9e-129">Notez que les options de règle de mise à l’échelle de hello qui s’ouvrent un volet contextuel à droite hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="bcd9e-130">Par défaut, cette opération définit tooscale d’option hello votre instance compter à 1 si hello pourcentage d’UC de ressource de hello dépasse 70 pour cent.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="bcd9e-131">Laissez les valeurs par défaut et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="bcd9e-132">![Créer le paramètre de mise à l’échelle pour une application web][6]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="bcd9e-133">Vous avez créé votre première règle de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-133">You've now created your first scale rule.</span></span> <span data-ttu-id="bcd9e-134">Notez que hello UX recommande les meilleures pratiques et qui indique « il est recommandé de toohave au moins une échelle de la règle. »</span><span class="sxs-lookup"><span data-stu-id="bcd9e-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="bcd9e-135">toodo pour :</span><span class="sxs-lookup"><span data-stu-id="bcd9e-135">toodo so:</span></span>
  
    <span data-ttu-id="bcd9e-136">a.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-136">a.</span></span> <span data-ttu-id="bcd9e-137">Cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="bcd9e-138">b.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-138">b.</span></span> <span data-ttu-id="bcd9e-139">Définissez **opérateur** trop**moins**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="bcd9e-140">c.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-140">c.</span></span> <span data-ttu-id="bcd9e-141">Définissez **seuil** trop**20**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="bcd9e-142">d.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-142">d.</span></span> <span data-ttu-id="bcd9e-143">Définissez **opération** trop**de diminuer le nombre par**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="bcd9e-144">Vous devez maintenant avoir un paramètre de mise à l’échelle qui fait monter/diminuer en puissance en fonction de l’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="bcd9e-145">![Mise à l’échelle en fonction du processeur][8]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="bcd9e-146">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-146">Click **Save**.</span></span>

<span data-ttu-id="bcd9e-147">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="bcd9e-147">Congratulations!</span></span> <span data-ttu-id="bcd9e-148">Vous avez maintenant créé votre premier tooautoscale de paramètre de mise à l’échelle votre application web basée sur l’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="bcd9e-149">la même procédure Hello est applicable tooget démarré avec une échelle de machine virtuelle rôle du service cloud ou de jeu.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="bcd9e-150">Autres points à considérer</span><span class="sxs-lookup"><span data-stu-id="bcd9e-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="bcd9e-151">Mise à l'échelle en fonction d’une planification</span><span class="sxs-lookup"><span data-stu-id="bcd9e-151">Scale based on a schedule</span></span>
<span data-ttu-id="bcd9e-152">En outre tooscale en fonction de l’UC, vous pouvez définir votre échelle différemment pour des jours spécifiques de la semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="bcd9e-153">Cliquez sur **Ajouter une condition de mise à l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="bcd9e-154">Définition des règles de mode et hello de montée en puissance hello est même hello en tant que condition de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="bcd9e-155">Sélectionnez **répéter des jours spécifiques** de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="bcd9e-156">Sélectionnez les jours hello et l’heure de début et de fin de hello pour lorsque la condition de l’échelle hello doit être appliquée.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Condition de mise à l’échelle basée sur une planification][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="bcd9e-158">Mettre à l’échelle différemment à des dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="bcd9e-158">Scale differently on specific dates</span></span>
<span data-ttu-id="bcd9e-159">En outre tooscale en fonction de l’UC, vous pouvez définir votre échelle différemment pour des dates spécifiques.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="bcd9e-160">Cliquez sur **Ajouter une condition de mise à l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="bcd9e-161">Définition des règles de mode et hello de montée en puissance hello est même hello en tant que condition de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="bcd9e-162">Sélectionnez **spécifier les dates de début et de fin** de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="bcd9e-163">Sélectionnez les dates de début/fin hello et l’heure de début et de fin de hello pour lorsque la condition de l’échelle hello doit être appliquée.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Condition de mise à l’échelle en fonction des dates][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="bcd9e-165">Afficher l’historique de l’échelle hello de votre ressource</span><span class="sxs-lookup"><span data-stu-id="bcd9e-165">View hello scale history of your resource</span></span>
<span data-ttu-id="bcd9e-166">Chaque fois que votre ressource est mise à l’échelle vers le haut ou vers le bas, un événement est consigné dans le journal d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="bcd9e-167">Vous pouvez afficher l’historique de l’échelle hello de votre ressource pour hello dernières 24 heures en basculant toohello **l’historique d’exécution** onglet.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Historique d’exécution][11]

<span data-ttu-id="bcd9e-169">Si vous souhaitez que l’historique de l’échelle complète tooview hello (pour les jours d’activité too90), sélectionnez **cliquez ici toosee plus de détails**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="bcd9e-170">journal d’activité Hello s’ouvre, avec mise à l’échelle présélectionnée pour votre ressource et la catégorie.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="bcd9e-171">Afficher la définition de l’échelle hello de votre ressource</span><span class="sxs-lookup"><span data-stu-id="bcd9e-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="bcd9e-172">La mise à l’échelle est une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="bcd9e-173">Vous pouvez afficher la définition de l’échelle de hello dans JSON en basculant toohello **JSON** onglet.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Définition de mise à l’échelle][12]

<span data-ttu-id="bcd9e-175">Vous pouvez apporter des modifications dans le JSON directement, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="bcd9e-176">Ces modifications apparaîtront après que les avoir enregistrées.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="bcd9e-177">Désactiver la mise à l’échelle automatique et mettre à l’échelle manuellement vos instances</span><span class="sxs-lookup"><span data-stu-id="bcd9e-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="bcd9e-178">Il peut y avoir heures lorsque vous souhaitez toodisable vos paramètres actuels de la mise à l’échelle et manuellement mettre à l’échelle de votre ressource.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="bcd9e-179">Cliquez sur hello **désactiver la mise à l’échelle** bouton en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="bcd9e-180">![Désactiver la mise à l’échelle automatique][13]</span><span class="sxs-lookup"><span data-stu-id="bcd9e-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="bcd9e-181">Cette option désactive votre configuration.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-181">This option disables your configuration.</span></span> <span data-ttu-id="bcd9e-182">Toutefois, vous pouvez revenir tooit après avoir activé la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="bcd9e-183">Vous pouvez maintenant définir le nombre de hello d’instances que vous souhaitez tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Définir l’échelle manuelle][14]

<span data-ttu-id="bcd9e-185">Vous pouvez toujours revenir tooAutoscale en cliquant sur **activez** , puis **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bcd9e-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd9e-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd9e-186">Next steps</span></span>
- [<span data-ttu-id="bcd9e-187">Créer une alerte de journal activité toomonitor toutes les opérations du moteur de mise à l’échelle de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="bcd9e-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="bcd9e-188">Créer une alerte de journal activité toomonitor toutes les opérations de montée/mise à l’échelle mise à l’échelle sur votre abonnement</span><span class="sxs-lookup"><span data-stu-id="bcd9e-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

