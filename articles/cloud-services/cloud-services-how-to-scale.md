---
title: "Mise à l’échelle automatique d’un service cloud dans le portail Classic | Microsoft Docs"
description: "(Classic) Découvrez comment utiliser le portail Classic pour configurer des règles de mise à l’échelle automatique pour le rôle web ou de travail d’un service cloud dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="d9872-103">Configuration de la mise à l’échelle automatique d’un service cloud dans le portail Classic</span><span class="sxs-lookup"><span data-stu-id="d9872-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9872-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9872-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="d9872-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="d9872-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="d9872-106">Sur la page de mise à l’échelle du portail Azure Classic, vous pouvez configurer les paramètres de mise à l’échelle automatique pour votre rôle web ou rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="d9872-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="d9872-107">Vous pouvez également configurer une mise à l’échelle manuelle au lieu d’une mise à l’échelle automatique basée sur des règles.</span><span class="sxs-lookup"><span data-stu-id="d9872-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="d9872-108">Cet article porte essentiellement sur les rôles web et de travail d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="d9872-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="d9872-109">Lorsque vous créez directement une machine virtuelle (Classic), elle est hébergée dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="d9872-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="d9872-110">Certaines de ces informations s’appliquent à ces types de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d9872-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="d9872-111">La mise à l’échelle d’un groupe à haute disponibilité de machines virtuelles consiste simplement à les démarrer et à les arrêter selon les règles de mise à l’échelle que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="d9872-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="d9872-112">Pour plus d’informations sur les machines virtuelles et les groupes à haute disponibilité, consultez [Gérer la disponibilité des machines virtuelles](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d9872-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="d9872-113">Vous devez tenir compte des informations suivantes avant de configurer la mise à l'échelle de votre application :</span><span class="sxs-lookup"><span data-stu-id="d9872-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="d9872-114">L'utilisation des cœurs a une incidence sur la mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="d9872-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="d9872-115">Le nombre de cœurs utilisés varie en fonction de la taille des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="d9872-115">Larger role instances use more cores.</span></span> <span data-ttu-id="d9872-116">Vous pouvez mettre à l’échelle une application uniquement dans la limite des cœurs de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9872-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="d9872-117">Par exemple, si la limite de votre abonnement est de 20 cœurs.</span><span class="sxs-lookup"><span data-stu-id="d9872-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="d9872-118">Si vous exécutez une application avec deux services cloud de taille moyenne (4 cœurs au total), vous pouvez seulement faire monter en charge les autres déploiements de service cloud de votre abonnement des 16 cœurs restants.</span><span class="sxs-lookup"><span data-stu-id="d9872-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="d9872-119">Pour plus d’informations sur les tailles, consultez [Tailles de services cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="d9872-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="d9872-120">Vous devez créer une file d’attente et l’associer à un rôle avant de pouvoir mettre à l’échelle une application en fonction d’un seuil de messages.</span><span class="sxs-lookup"><span data-stu-id="d9872-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="d9872-121">Pour plus d'informations, consultez la page [Utilisation du service de stockage de file d'attente](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d9872-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="d9872-122">Vous pouvez mettre à l'échelle des ressources qui sont liées à votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d9872-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="d9872-123">Pour plus d’informations sur la liaison des ressources, consultez la rubrique [Liaison d’une ressource à un service cloud](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="d9872-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="d9872-124">Pour activer la fonction de haute disponibilité de votre application, vous devez vous assurer qu’elle est déployée avec plusieurs instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="d9872-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="d9872-125">Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="d9872-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="d9872-126">Planifier la mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="d9872-126">Schedule scaling</span></span>
<span data-ttu-id="d9872-127">Par défaut, tous les rôles ne suivent pas une planification spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9872-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="d9872-128">Par conséquent, les paramètres modifiés s’appliquent à toutes les heures et à tous les jours de l’année.</span><span class="sxs-lookup"><span data-stu-id="d9872-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="d9872-129">Si vous le souhaitez, vous pouvez configurer une mise à l’échelle manuelle ou automatique pour un des modes suivants :</span><span class="sxs-lookup"><span data-stu-id="d9872-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="d9872-130">Les jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="d9872-130">Weekdays</span></span>
* <span data-ttu-id="d9872-131">Les week-ends</span><span class="sxs-lookup"><span data-stu-id="d9872-131">Weekends</span></span>
* <span data-ttu-id="d9872-132">Les nuits de la semaine</span><span class="sxs-lookup"><span data-stu-id="d9872-132">Week nights</span></span>
* <span data-ttu-id="d9872-133">Les matinées de la semaine</span><span class="sxs-lookup"><span data-stu-id="d9872-133">Week mornings</span></span>
* <span data-ttu-id="d9872-134">Des dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="d9872-134">Specific dates</span></span>
* <span data-ttu-id="d9872-135">Des plages de dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="d9872-135">Specific date ranges</span></span>

<span data-ttu-id="d9872-136">Le paramètre de planification est configuré dans le [Portail Azure Classic](https://manage.windowsazure.com/) à la page</span><span class="sxs-lookup"><span data-stu-id="d9872-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="d9872-137">**Services cloud** > **\[Votre service cloud\]** > **Mise à l’échelle** > **\[Production ou intermédiaire\]**.</span><span class="sxs-lookup"><span data-stu-id="d9872-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="d9872-138">Cliquez sur le bouton **Configurer des heures de planification** pour chaque rôle à modifier.</span><span class="sxs-lookup"><span data-stu-id="d9872-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Mise à l’échelle automatique d’un service cloud en fonction d’une planification][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="d9872-140">Mise à l’échelle manuelle</span><span class="sxs-lookup"><span data-stu-id="d9872-140">Manual scale</span></span>
<span data-ttu-id="d9872-141">Dans la page **Mettre à l’échelle** , vous pouvez augmenter ou diminuer manuellement le nombre d’instances s’exécutant dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="d9872-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="d9872-142">Cette configuration s’applique à chaque planification que vous avez créée ou tout le temps si vous n’en avez pas créé.</span><span class="sxs-lookup"><span data-stu-id="d9872-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="d9872-143">Dans le [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Cloud Services**, puis sur le nom du service cloud pour ouvrir le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d9872-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d9872-144">Si votre service cloud n’y figure pas, vous devrez peut-être passer de **Production** à **Intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9872-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="d9872-145">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="d9872-145">Click **Scale**.</span></span>
3. <span data-ttu-id="d9872-146">Sélectionnez la planification dont vous voulez modifier les options de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d9872-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="d9872-147">La valeur par défaut est *Aucune heure planifiée* si vous n’avez pas défini de planification.</span><span class="sxs-lookup"><span data-stu-id="d9872-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="d9872-148">Recherchez la section **Mettre à l’échelle par métrique**, puis sélectionnez **AUCUN**.</span><span class="sxs-lookup"><span data-stu-id="d9872-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="d9872-149">Il s’agit du paramètre par défaut pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="d9872-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="d9872-150">Chaque rôle dans le service cloud est doté d'un curseur permettant de modifier le nombre d'instances à utiliser.</span><span class="sxs-lookup"><span data-stu-id="d9872-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Mise à l’échelle manuelle d’un rôle de service cloud][manual_scale]
   
    <span data-ttu-id="d9872-152">Si vous avez besoin d’instances supplémentaires, vous devrez peut-être modifier la [taille des machines virtuelles du service cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="d9872-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="d9872-153">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="d9872-153">Click **Save**.</span></span>  
   <span data-ttu-id="d9872-154">Les instances de rôle sont ajoutées ou supprimées en fonction de vos sélections.</span><span class="sxs-lookup"><span data-stu-id="d9872-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="d9872-155">Chaque fois que l’icône ![][tip_icon] apparaît, pointez dessus avec le curseur de la souris pour obtenir de l’aide concernant la fonction d’un paramètre spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9872-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="d9872-156">Mise à l’échelle automatique - UC</span><span class="sxs-lookup"><span data-stu-id="d9872-156">Automatic scale - CPU</span></span>
<span data-ttu-id="d9872-157">Une mise à l’échelle se produit pour ce mode si le pourcentage moyen d’utilisation de l’unité centrale est supérieur ou inférieur aux seuils spécifiés.</span><span class="sxs-lookup"><span data-stu-id="d9872-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="d9872-158">Dans ce cas, des instances de rôle sont créées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="d9872-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="d9872-159">Dans le [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Cloud Services**, puis sur le nom du service cloud pour ouvrir le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d9872-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d9872-160">Si votre service cloud n’y figure pas, vous devrez peut-être passer de **Production** à **Intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9872-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="d9872-161">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="d9872-161">Click **Scale**.</span></span>
3. <span data-ttu-id="d9872-162">Sélectionnez la planification dont vous voulez modifier les options de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d9872-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="d9872-163">La valeur par défaut est *Aucune heure planifiée* si vous n’avez pas défini de planification.</span><span class="sxs-lookup"><span data-stu-id="d9872-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="d9872-164">Recherchez la section **Mettre à l’échelle par métrique**, puis sélectionnez **UC**.</span><span class="sxs-lookup"><span data-stu-id="d9872-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="d9872-165">Vous pouvez maintenant configurer une plage minimale et maximale d’instances de rôles, l’utilisation d’unité centrale cible (pour déclencher une montée en charge) et le nombre d’instances devant faire l’objet d’une montée ou d’une descente en charge.</span><span class="sxs-lookup"><span data-stu-id="d9872-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Mise à l’échelle d’un rôle de service cloud par charge d’UC][cpu_scale]

> [!TIP]
> <span data-ttu-id="d9872-167">Chaque fois que l’icône ![][tip_icon] apparaît, pointez dessus avec le curseur de la souris pour obtenir de l’aide concernant la fonction d’un paramètre spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9872-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="d9872-168">Mise à l’échelle automatique - File d’attente</span><span class="sxs-lookup"><span data-stu-id="d9872-168">Automatic scale - Queue</span></span>
<span data-ttu-id="d9872-169">Une mise à l’échelle automatique se produit dans ce mode si le nombre de messages dans une file d’attente monte ou descend au-delà d’un seuil spécifié.</span><span class="sxs-lookup"><span data-stu-id="d9872-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="d9872-170">Dans ce cas, des instances de rôle sont créées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="d9872-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="d9872-171">Dans le [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Cloud Services**, puis sur le nom du service cloud pour ouvrir le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d9872-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d9872-172">Si votre service cloud n’y figure pas, vous devrez peut-être passer de **Production** à **Intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9872-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="d9872-173">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="d9872-173">Click **Scale**.</span></span>
3. <span data-ttu-id="d9872-174">Recherchez la section **Mettre à l’échelle par métrique**, puis sélectionnez **QUEUE**.</span><span class="sxs-lookup"><span data-stu-id="d9872-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="d9872-175">Vous pouvez maintenant configurer une plage minimale et maximale d’instances de rôles, la file d’attente et le nombre de messages de file d’attente à traiter pour chaque instance, ainsi que le nombre d’instances devant faire l’objet d’une montée ou d’une descente en charge.</span><span class="sxs-lookup"><span data-stu-id="d9872-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Mise à l’échelle d’un rôle de service cloud par une file d’attente de messages][queue_scale]

> [!TIP]
> <span data-ttu-id="d9872-177">Chaque fois que l’icône ![][tip_icon] apparaît, pointez dessus avec le curseur de la souris pour obtenir de l’aide concernant la fonction d’un paramètre spécifique.</span><span class="sxs-lookup"><span data-stu-id="d9872-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="d9872-178">Mise à l'échelle des ressources liées</span><span class="sxs-lookup"><span data-stu-id="d9872-178">Scale linked resources</span></span>
<span data-ttu-id="d9872-179">Lorsque vous mettez à l'échelle un rôle, il est souvent avantageux de mettre également à l'échelle la base de données qui est utilisée par l'application.</span><span class="sxs-lookup"><span data-stu-id="d9872-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="d9872-180">Si vous liez la base de données au service cloud, vous pouvez accéder aux paramètres de mise à l’échelle de cette ressource en cliquant sur le lien approprié.</span><span class="sxs-lookup"><span data-stu-id="d9872-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="d9872-181">Dans le [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Cloud Services**, puis sur le nom du service cloud pour ouvrir le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="d9872-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d9872-182">Si votre service cloud n’y figure pas, vous devrez peut-être passer de **Production** à **Intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9872-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="d9872-183">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="d9872-183">Click **Scale**.</span></span>
3. <span data-ttu-id="d9872-184">Recherchez la section **Ressources liées** et cliquez sur **Gérer la mise à l’échelle pour cette base de données**.</span><span class="sxs-lookup"><span data-stu-id="d9872-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d9872-185">Si vous ne voyez pas de section **Ressources liées** , c’est que vous n’avez probablement pas de ressources liées.</span><span class="sxs-lookup"><span data-stu-id="d9872-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
