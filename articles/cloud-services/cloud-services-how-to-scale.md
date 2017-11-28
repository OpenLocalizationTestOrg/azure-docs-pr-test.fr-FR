---
title: "aaaAuto faire évoluer un service cloud dans le portail classique de hello | Documents Microsoft"
description: "(classique) Découvrez comment toouse hello tooconfigure portail classique des règles de mise à l’échelle automatique pour un rôle web de service cloud ou le rôle de travail dans Azure."
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
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="b15e6-103">Comment tooconfigure mise à l’échelle d’un Service Cloud dans le portail classique de hello</span><span class="sxs-lookup"><span data-stu-id="b15e6-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b15e6-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b15e6-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="b15e6-105">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="b15e6-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="b15e6-106">Page de mise à l’échelle hello Hello portail Azure classic, vous pouvez configurer les paramètres de mise à l’échelle automatique pour votre rôle web ou d’un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="b15e6-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="b15e6-107">Vous pouvez également configurer une mise à l’échelle manuelle au lieu d’une mise à l’échelle automatique basée sur des règles.</span><span class="sxs-lookup"><span data-stu-id="b15e6-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="b15e6-108">Cet article porte essentiellement sur les rôles web et de travail d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="b15e6-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="b15e6-109">Lorsque vous créez directement une machine virtuelle (Classic), elle est hébergée dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="b15e6-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="b15e6-110">Certaines de ces informations s’applique types toothese d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="b15e6-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="b15e6-111">Mise à l’échelle d’un ensemble de disponibilité des machines virtuelles est simplement en cours d’arrêt les désactiver selon les règles de mise à l’échelle hello que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="b15e6-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="b15e6-112">Pour plus d’informations sur les ordinateurs virtuels et des groupes à haute disponibilité, consultez [gérer hello disponibilité des Machines virtuelles](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b15e6-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="b15e6-113">Vous devez envisager hello informations suivantes avant de configurer la mise à l’échelle de votre application :</span><span class="sxs-lookup"><span data-stu-id="b15e6-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="b15e6-114">L'utilisation des cœurs a une incidence sur la mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="b15e6-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="b15e6-115">Le nombre de cœurs utilisés varie en fonction de la taille des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="b15e6-115">Larger role instances use more cores.</span></span> <span data-ttu-id="b15e6-116">Vous pouvez faire évoluer une application uniquement dans la limite de hello de cœurs de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b15e6-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="b15e6-117">Par exemple, si la limite de votre abonnement est de 20 cœurs.</span><span class="sxs-lookup"><span data-stu-id="b15e6-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="b15e6-118">Si vous exécutez une application avec les deux services de cloud de taille moyenne (un total de 4 cœurs), vous pouvez uniquement l’échelle autres déploiements de service cloud dans votre abonnement en 16 cœurs restants de hello.</span><span class="sxs-lookup"><span data-stu-id="b15e6-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="b15e6-119">Pour plus d’informations sur les tailles, consultez [Tailles de services cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="b15e6-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="b15e6-120">Vous devez créer une file d’attente et l’associer à un rôle avant de pouvoir mettre à l’échelle une application en fonction d’un seuil de messages.</span><span class="sxs-lookup"><span data-stu-id="b15e6-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="b15e6-121">Pour plus d’informations, consultez [comment toouse hello Service de stockage de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b15e6-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="b15e6-122">Vous pouvez faire évoluer les ressources qui sont lié tooyour service cloud.</span><span class="sxs-lookup"><span data-stu-id="b15e6-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="b15e6-123">Pour plus d’informations sur la liaison des ressources, consultez [Comment : lier un service de cloud de ressource tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="b15e6-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="b15e6-124">tooenable haute disponibilité de votre application, vous devez vous assurer qu’il est déployé avec deux ou plusieurs instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="b15e6-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="b15e6-125">Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="b15e6-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="b15e6-126">Planifier la mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="b15e6-126">Schedule scaling</span></span>
<span data-ttu-id="b15e6-127">Par défaut, tous les rôles ne suivent pas une planification spécifique.</span><span class="sxs-lookup"><span data-stu-id="b15e6-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="b15e6-128">Par conséquent, les paramètres modifiés s’appliquent tooall fois et tous les jours pendant toute année de hello.</span><span class="sxs-lookup"><span data-stu-id="b15e6-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="b15e6-129">Si vous le souhaitez, vous pouvez configurer la mise à l’échelle manuelle ou automatique pour l’une des hello suivant modes :</span><span class="sxs-lookup"><span data-stu-id="b15e6-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="b15e6-130">Les jours de la semaine</span><span class="sxs-lookup"><span data-stu-id="b15e6-130">Weekdays</span></span>
* <span data-ttu-id="b15e6-131">Les week-ends</span><span class="sxs-lookup"><span data-stu-id="b15e6-131">Weekends</span></span>
* <span data-ttu-id="b15e6-132">Les nuits de la semaine</span><span class="sxs-lookup"><span data-stu-id="b15e6-132">Week nights</span></span>
* <span data-ttu-id="b15e6-133">Les matinées de la semaine</span><span class="sxs-lookup"><span data-stu-id="b15e6-133">Week mornings</span></span>
* <span data-ttu-id="b15e6-134">Des dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="b15e6-134">Specific dates</span></span>
* <span data-ttu-id="b15e6-135">Des plages de dates spécifiques</span><span class="sxs-lookup"><span data-stu-id="b15e6-135">Specific date ranges</span></span>

<span data-ttu-id="b15e6-136">paramètre de planification Hello est configuré dans hello [portail Azure classic](https://manage.windowsazure.com/) sur hello</span><span class="sxs-lookup"><span data-stu-id="b15e6-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="b15e6-137">**Services cloud** > **\[Votre service cloud\]** > **Mise à l’échelle** > **\[Production ou intermédiaire\]**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="b15e6-138">Cliquez sur hello **configurer des heures de planification** bouton pour chaque rôle, vous souhaitez toochange.</span><span class="sxs-lookup"><span data-stu-id="b15e6-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Mise à l’échelle automatique d’un service cloud en fonction d’une planification][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="b15e6-140">Mise à l’échelle manuelle</span><span class="sxs-lookup"><span data-stu-id="b15e6-140">Manual scale</span></span>
<span data-ttu-id="b15e6-141">Sur hello **échelle** page, vous pouvez manuellement augmenter ou réduire hello nombre d’instances en cours d’exécution dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="b15e6-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="b15e6-142">Ce paramètre est configuré pour chaque planification que vous avez créé ou tooall si vous n’avez pas créé une planification.</span><span class="sxs-lookup"><span data-stu-id="b15e6-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="b15e6-143">Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="b15e6-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b15e6-144">Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="b15e6-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="b15e6-145">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-145">Click **Scale**.</span></span>
3. <span data-ttu-id="b15e6-146">Sélectionnez l’agenda hello toochange mise à l’échelle des options pour.</span><span class="sxs-lookup"><span data-stu-id="b15e6-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="b15e6-147">*Ne moments planifiés* est par défaut de hello si vous ne disposez d’aucune planification définie.</span><span class="sxs-lookup"><span data-stu-id="b15e6-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="b15e6-148">Recherche hello **mise à l’échelle par métrique** section et sélectionnez **NONE**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="b15e6-149">Ce paramètre est par défaut de hello pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="b15e6-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="b15e6-150">Chaque rôle dans le service cloud hello dispose d’un curseur pour modifier le nombre de hello d’instances toouse.</span><span class="sxs-lookup"><span data-stu-id="b15e6-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Mise à l’échelle manuelle d’un rôle de service cloud][manual_scale]
   
    <span data-ttu-id="b15e6-152">Si vous avez besoin de plusieurs instances, vous devrez peut-être toochange hello [taille de machine virtuelle de service de cloud computing](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="b15e6-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="b15e6-153">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-153">Click **Save**.</span></span>  
   <span data-ttu-id="b15e6-154">Les instances de rôle sont ajoutées ou supprimées en fonction de vos sélections.</span><span class="sxs-lookup"><span data-stu-id="b15e6-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="b15e6-155">Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.</span><span class="sxs-lookup"><span data-stu-id="b15e6-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="b15e6-156">Mise à l’échelle automatique - UC</span><span class="sxs-lookup"><span data-stu-id="b15e6-156">Automatic scale - CPU</span></span>
<span data-ttu-id="b15e6-157">Ce mode met à l’échelle si le pourcentage moyen de hello d’utilisation du processeur passe au-dessus ou en dessous des seuils spécifiés.</span><span class="sxs-lookup"><span data-stu-id="b15e6-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="b15e6-158">Dans ce cas, des instances de rôle sont créées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="b15e6-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="b15e6-159">Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="b15e6-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b15e6-160">Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="b15e6-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="b15e6-161">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-161">Click **Scale**.</span></span>
3. <span data-ttu-id="b15e6-162">Sélectionnez l’agenda hello toochange mise à l’échelle des options pour.</span><span class="sxs-lookup"><span data-stu-id="b15e6-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="b15e6-163">*Ne moments planifiés* est par défaut de hello si vous ne disposez d’aucune planification définie.</span><span class="sxs-lookup"><span data-stu-id="b15e6-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="b15e6-164">Recherche hello **mise à l’échelle par métrique** section et sélectionnez **processeur**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="b15e6-165">Vous pouvez maintenant configurer une plage minimale et maximale des instances de rôles, hello UC cible l’utilisation de (tootrigger une montée en puissance), et nombre d’instances tooscale haut et bas par.</span><span class="sxs-lookup"><span data-stu-id="b15e6-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Mise à l’échelle d’un rôle de service cloud par charge d’UC][cpu_scale]

> [!TIP]
> <span data-ttu-id="b15e6-167">Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.</span><span class="sxs-lookup"><span data-stu-id="b15e6-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="b15e6-168">Mise à l’échelle automatique - File d’attente</span><span class="sxs-lookup"><span data-stu-id="b15e6-168">Automatic scale - Queue</span></span>
<span data-ttu-id="b15e6-169">Ce mode s’ajuste automatiquement en cas de nombre de hello de messages dans une file d’attente au-dessus ou en dessous d’un seuil spécifié.</span><span class="sxs-lookup"><span data-stu-id="b15e6-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="b15e6-170">Dans ce cas, des instances de rôle sont créées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="b15e6-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="b15e6-171">Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="b15e6-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b15e6-172">Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="b15e6-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="b15e6-173">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-173">Click **Scale**.</span></span>
3. <span data-ttu-id="b15e6-174">Recherche hello **mise à l’échelle par métrique** section et sélectionnez **file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="b15e6-175">Vous pouvez désormais configurer une plage minimale et maximale d’instances de rôles, file d’attente hello et nombre de tooprocess de messages de file d’attente pour chaque instance et combien de tooscale instances haut et bas par.</span><span class="sxs-lookup"><span data-stu-id="b15e6-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Mise à l’échelle d’un rôle de service cloud par une file d’attente de messages][queue_scale]

> [!TIP]
> <span data-ttu-id="b15e6-177">Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.</span><span class="sxs-lookup"><span data-stu-id="b15e6-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="b15e6-178">Mise à l'échelle des ressources liées</span><span class="sxs-lookup"><span data-stu-id="b15e6-178">Scale linked resources</span></span>
<span data-ttu-id="b15e6-179">Souvent, lorsque vous l’échelle d’un rôle, il est bénéfique tooscale hello base de données qui utilise également application hello.</span><span class="sxs-lookup"><span data-stu-id="b15e6-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="b15e6-180">Si vous liez le service de cloud toohello hello de base de données, vous pouvez accéder à hello mise à l’échelle des paramètres pour cette ressource en cliquant sur le lien approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="b15e6-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="b15e6-181">Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="b15e6-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b15e6-182">Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="b15e6-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="b15e6-183">Cliquez sur **Scale**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-183">Click **Scale**.</span></span>
3. <span data-ttu-id="b15e6-184">Recherche hello **de ressources liées** et cliquez sur **gérer la mise à l’échelle pour cette base de données**.</span><span class="sxs-lookup"><span data-stu-id="b15e6-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b15e6-185">Si vous ne voyez pas de section **Ressources liées** , c’est que vous n’avez probablement pas de ressources liées.</span><span class="sxs-lookup"><span data-stu-id="b15e6-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
