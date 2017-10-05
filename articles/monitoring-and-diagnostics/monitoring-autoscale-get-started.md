---
title: "Bien démarrer avec la mise à l’échelle automatique dans Azure | Documents Microsoft"
description: "Découvrez comment effectuer une mise à l’échelle de votre ressource dans Azure."
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
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="21fe1-103">Bien démarrer avec la mise à l’échelle automatique dans Azure</span><span class="sxs-lookup"><span data-stu-id="21fe1-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="21fe1-104">Cet article décrit comment configurer vos paramètres de mise à l’échelle automatique pour votre ressource dans le portail Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="21fe1-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="21fe1-105">La mise à l’échelle automatique Azure Monitor s’applique uniquement aux jeux de mise à l’échelle de machines virtuelles, services cloud, plans Azure App Service et environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="21fe1-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="21fe1-106">Découvrir les paramètres de mise à l’échelle automatique dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="21fe1-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="21fe1-107">Vous pouvez découvrir toutes les ressources pour lesquelles la mise à l’échelle automatique est applicable dans Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="21fe1-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="21fe1-108">Pour une procédure pas à pas, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="21fe1-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="21fe1-109">Ouvrez le [portail Azure][1]</span><span class="sxs-lookup"><span data-stu-id="21fe1-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="21fe1-110">Cliquez sur l’icône Azure Monitor dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="21fe1-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="21fe1-111">![Ouvrez Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="21fe1-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="21fe1-112">Cliquez sur **Mise à l’échelle automatique** pour afficher toutes les ressources pour lesquelles la mise à l’échelle automatique est applicable, ainsi que leur état actuel de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="21fe1-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="21fe1-113">![Découvrir la mise à l’échelle automatique dans Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="21fe1-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="21fe1-114">Vous pouvez utiliser le volet de filtre en haut pour réduire l’étendue de la liste afin de sélectionner des ressources dans un groupe de ressources spécifique, des types de ressources spécifiques ou une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="21fe1-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="21fe1-115">Pour chaque ressource, vous trouverez le nombre d’instances en cours ainsi que son état de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="21fe1-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="21fe1-116">L’état de mise à l’échelle automatique peut être :</span><span class="sxs-lookup"><span data-stu-id="21fe1-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="21fe1-117">**Non configuré** : vous n’avez pas encore activé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="21fe1-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="21fe1-118">**Activé** : vous avez activé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="21fe1-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="21fe1-119">**Désactivé** : vous avez désactivé la mise à l’échelle automatique pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="21fe1-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="21fe1-120">Créez votre premier paramètre de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="21fe1-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="21fe1-121">Suivons maintenant une procédure simple pour créer votre premier paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="21fe1-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="21fe1-122">Ouvrez la panneau **Mise à l’échelle automatique** dans Azure Monitor et sélectionnez une ressource à mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="21fe1-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="21fe1-123">(les étapes ci-dessous utilisent un plan App Service associé à une application Web.</span><span class="sxs-lookup"><span data-stu-id="21fe1-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="21fe1-124">Vous pouvez [créer votre première application Web ASP.NET dans Azure en 5 minutes][4])</span><span class="sxs-lookup"><span data-stu-id="21fe1-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="21fe1-125">Notez que le nombre d’instances actuel est 1.</span><span class="sxs-lookup"><span data-stu-id="21fe1-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="21fe1-126">Cliquez sur **Activer la mise à l’échelle automatique**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="21fe1-127">![Paramètre d’échelle pour la nouvelle application web][5]</span><span class="sxs-lookup"><span data-stu-id="21fe1-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="21fe1-128">Fournissez un nom pour le paramètre de mise à l’échelle, puis cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="21fe1-129">Notez les options de règle de mise à l’échelle qui s’ouvrent dans un volet contextuel dans la partie droite.</span><span class="sxs-lookup"><span data-stu-id="21fe1-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="21fe1-130">Par défaut, l’option de mise à l’échelle du nombre d’instances est définie sur 1 si le pourcentage processeur de la ressource dépasse 70 %.</span><span class="sxs-lookup"><span data-stu-id="21fe1-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="21fe1-131">Laissez les valeurs par défaut et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="21fe1-132">![Créer le paramètre de mise à l’échelle pour une application web][6]</span><span class="sxs-lookup"><span data-stu-id="21fe1-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="21fe1-133">Vous avez créé votre première règle de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="21fe1-133">You've now created your first scale rule.</span></span> <span data-ttu-id="21fe1-134">Notez que l’expérience utilisateur recommande les meilleures pratiques et indique « qu’il est recommandé d’avoir au moins une règle de mise à l’échelle. »</span><span class="sxs-lookup"><span data-stu-id="21fe1-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="21fe1-135">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="21fe1-135">To do so:</span></span>
  
    <span data-ttu-id="21fe1-136">a.</span><span class="sxs-lookup"><span data-stu-id="21fe1-136">a.</span></span> <span data-ttu-id="21fe1-137">Cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="21fe1-138">b.</span><span class="sxs-lookup"><span data-stu-id="21fe1-138">b.</span></span> <span data-ttu-id="21fe1-139">Définissez **Opérateur** sur **moins de**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="21fe1-140">c.</span><span class="sxs-lookup"><span data-stu-id="21fe1-140">c.</span></span> <span data-ttu-id="21fe1-141">Définissez **Seuil** sur **20**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="21fe1-142">d.</span><span class="sxs-lookup"><span data-stu-id="21fe1-142">d.</span></span> <span data-ttu-id="21fe1-143">Définissez **Opération** sur **Diminuer le nombre par**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="21fe1-144">Vous devez maintenant avoir un paramètre de mise à l’échelle qui fait monter/diminuer en puissance en fonction de l’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="21fe1-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="21fe1-145">![Mise à l’échelle en fonction du processeur][8]</span><span class="sxs-lookup"><span data-stu-id="21fe1-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="21fe1-146">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-146">Click **Save**.</span></span>

<span data-ttu-id="21fe1-147">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="21fe1-147">Congratulations!</span></span> <span data-ttu-id="21fe1-148">Vous avez maintenant correctement créé votre premier paramètre de mise à l’échelle pour mettre à l’échelle automatiquement votre application Web en fonction de l’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="21fe1-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="21fe1-149">Les mêmes étapes sont applicables pour bien démarrer avec un jeu de mise à l’échelle de machines virtuelles ou un rôle de service cloud.</span><span class="sxs-lookup"><span data-stu-id="21fe1-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="21fe1-150">Autres points à considérer</span><span class="sxs-lookup"><span data-stu-id="21fe1-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="21fe1-151">Mise à l'échelle en fonction d’une planification</span><span class="sxs-lookup"><span data-stu-id="21fe1-151">Scale based on a schedule</span></span>
<span data-ttu-id="21fe1-152">En plus de la mise à l’échelle en fonction du processeur, vous pouvez aussi définir votre mise à l’échelle différemment pour certains jours de la semaine.</span><span class="sxs-lookup"><span data-stu-id="21fe1-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="21fe1-153">Cliquez sur **Ajouter une condition de mise à l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="21fe1-154">La définition du mode de mise à l’échelle et des règles est identique à la condition par défaut.</span><span class="sxs-lookup"><span data-stu-id="21fe1-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="21fe1-155">Sélectionnez **Répéter des jours spécifiques** pour la planification.</span><span class="sxs-lookup"><span data-stu-id="21fe1-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="21fe1-156">Sélectionnez les jours et les heures de début/fin auxquels la condition de mise à l’échelle doit être appliquée.</span><span class="sxs-lookup"><span data-stu-id="21fe1-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Condition de mise à l’échelle basée sur une planification][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="21fe1-158">Mettre à l’échelle différemment à des dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="21fe1-158">Scale differently on specific dates</span></span>
<span data-ttu-id="21fe1-159">En plus de la mise à l’échelle en fonction du processeur, vous pouvez aussi définir votre mise à l’échelle différemment pour certaines dates spécifiques.</span><span class="sxs-lookup"><span data-stu-id="21fe1-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="21fe1-160">Cliquez sur **Ajouter une condition de mise à l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="21fe1-161">La définition du mode de mise à l’échelle et des règles est identique à la condition par défaut.</span><span class="sxs-lookup"><span data-stu-id="21fe1-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="21fe1-162">Sélectionnez **Spécifier les dates de début et de fin** pour la planification.</span><span class="sxs-lookup"><span data-stu-id="21fe1-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="21fe1-163">Sélectionnez les dates et les heures de début/fin auxquelles la condition de mise à l’échelle doit être appliquée.</span><span class="sxs-lookup"><span data-stu-id="21fe1-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Condition de mise à l’échelle en fonction des dates][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="21fe1-165">Afficher l’historique de mise à l’échelle de votre ressource</span><span class="sxs-lookup"><span data-stu-id="21fe1-165">View the scale history of your resource</span></span>
<span data-ttu-id="21fe1-166">Chaque fois que votre ressource monte/diminue en puissance, un événement est enregistré dans le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="21fe1-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="21fe1-167">Vous pouvez afficher l’historique de la mise à l’échelle de votre ressource pour les dernières 24 heures en basculant vers l’onglet **Exécuter l’historique**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![Historique d’exécution][11]

<span data-ttu-id="21fe1-169">Si vous souhaitez afficher l’historique de la mise à l’échelle complet (jusqu'à 90 jours), sélectionnez **Cliquez ici pour obtenir plus de détails**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="21fe1-170">Ce journal d’activité s’ouvre, avec la mise à l’échelle automatique présélectionnée pour la ressource et la catégorie.</span><span class="sxs-lookup"><span data-stu-id="21fe1-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="21fe1-171">Afficher la définition de mise à l’échelle de votre ressource</span><span class="sxs-lookup"><span data-stu-id="21fe1-171">View the scale definition of your resource</span></span>
<span data-ttu-id="21fe1-172">La mise à l’échelle est une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21fe1-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="21fe1-173">Vous pouvez afficher la définition de la mise à l’échelle dans JSON en basculant vers l’onglet **JSON**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Définition de mise à l’échelle][12]

<span data-ttu-id="21fe1-175">Vous pouvez apporter des modifications dans le JSON directement, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="21fe1-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="21fe1-176">Ces modifications apparaîtront après que les avoir enregistrées.</span><span class="sxs-lookup"><span data-stu-id="21fe1-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="21fe1-177">Désactiver la mise à l’échelle automatique et mettre à l’échelle manuellement vos instances</span><span class="sxs-lookup"><span data-stu-id="21fe1-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="21fe1-178">Il peut arriver que vous souhaitiez désactiver vos paramètres actuels de mise à l’échelle et mettre à l’échelle manuellement votre ressource.</span><span class="sxs-lookup"><span data-stu-id="21fe1-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="21fe1-179">Cliquez sur le bouton **Désactiver la mise à l’échelle automatique** en haut.</span><span class="sxs-lookup"><span data-stu-id="21fe1-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="21fe1-180">![Désactiver la mise à l’échelle automatique][13]</span><span class="sxs-lookup"><span data-stu-id="21fe1-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="21fe1-181">Cette option désactive votre configuration.</span><span class="sxs-lookup"><span data-stu-id="21fe1-181">This option disables your configuration.</span></span> <span data-ttu-id="21fe1-182">Toutefois, vous pouvez revenir dessus une fois que vous activez à nouveau la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="21fe1-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="21fe1-183">Vous pouvez maintenant définir le nombre d’instances à mettre à l’échelle sur manuellement.</span><span class="sxs-lookup"><span data-stu-id="21fe1-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Définir l’échelle manuelle][14]

<span data-ttu-id="21fe1-185">Vous pouvez toujours revenir à la mise à l’échelle automatique en cliquant sur **Activer la mise à l’échelle automatique** puis sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21fe1-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21fe1-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21fe1-186">Next steps</span></span>
- [<span data-ttu-id="21fe1-187">Créez une alerte de journal d’activité pour surveiller toutes les opérations du moteur de mise à l’échelle automatique dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="21fe1-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="21fe1-188">Créez une alerte de journal d’activité pour surveiller tous les échecs d’opérations de diminution et d’augmentation de la taille des instances de la mise à l’échelle automatique dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="21fe1-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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

