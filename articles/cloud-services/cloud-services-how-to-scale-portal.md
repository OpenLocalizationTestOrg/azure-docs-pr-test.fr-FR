---
title: "aaaAuto faire évoluer un service cloud dans le portail de hello | Documents Microsoft"
description: "Découvrez comment toouse hello tooconfigure portail règles de mise à l’échelle automatique pour un rôle web de service cloud ou le rôle de travail dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="62324-103">Comment tooconfigure mise à l’échelle d’un Service Cloud dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="62324-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62324-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="62324-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="62324-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="62324-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="62324-106">Des conditions peuvent être définies pour un rôle de travail de service cloud qui déclenchent une opération de diminution et d’augmentation de la taille des instances.</span><span class="sxs-lookup"><span data-stu-id="62324-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="62324-107">conditions de Hello pour le rôle de hello peuvent reposer sur hello processeur, disque ou de la charge réseau du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="62324-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="62324-108">Vous pouvez également définir une condition basée sur une mesure de file d’attente ou hello message d’une autre ressource Azure associé à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="62324-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="62324-109">Cet article porte essentiellement sur les rôles web et de travail d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="62324-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="62324-110">Lorsque vous créez directement une machine virtuelle (Classic), elle est hébergée dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="62324-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="62324-111">Vous pouvez mettre à l’échelle une machine virtuelle standard en l’associant à un [groupe à haute disponibilité](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) et en l’activant ou la désactivant manuellement.</span><span class="sxs-lookup"><span data-stu-id="62324-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="62324-112">Considérations</span><span class="sxs-lookup"><span data-stu-id="62324-112">Considerations</span></span>
<span data-ttu-id="62324-113">Vous devez envisager hello informations suivantes avant de configurer la mise à l’échelle de votre application :</span><span class="sxs-lookup"><span data-stu-id="62324-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="62324-114">L'utilisation des cœurs a une incidence sur la mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="62324-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="62324-115">Le nombre de cœurs utilisés varie en fonction de la taille des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="62324-115">Larger role instances use more cores.</span></span> <span data-ttu-id="62324-116">Vous pouvez faire évoluer une application uniquement dans la limite de hello de cœurs de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="62324-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="62324-117">Par exemple, si la limite de votre abonnement est de 20 cœurs.</span><span class="sxs-lookup"><span data-stu-id="62324-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="62324-118">Si vous exécutez une application avec les deux services de cloud de taille moyenne (un total de 4 cœurs), vous pouvez uniquement l’échelle autres déploiements de service cloud dans votre abonnement en 16 cœurs restants de hello.</span><span class="sxs-lookup"><span data-stu-id="62324-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="62324-119">Pour plus d’informations sur les tailles, consultez [Tailles de services cloud](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="62324-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="62324-120">Vous pouvez mettre à l’échelle en fonction d’un seuil de messages de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="62324-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="62324-121">Pour plus d’informations sur la façon toouse les files d’attente, consultez [comment toouse hello Service de stockage de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="62324-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="62324-122">Vous pouvez également mettre à l’échelle d’autres ressources associées à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="62324-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="62324-123">tooenable haute disponibilité de votre application, vous devez vous assurer qu’il est déployé avec deux ou plusieurs instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="62324-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="62324-124">Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="62324-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="62324-125">Emplacement de la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="62324-125">Where scale is located</span></span>
<span data-ttu-id="62324-126">Une fois que vous sélectionnez votre service cloud, vous devez avoir Panneau de service de cloud hello visible.</span><span class="sxs-lookup"><span data-stu-id="62324-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="62324-127">Dans Panneau de service cloud hello, sur hello **rôles et Instances** vignette, nom sélectionnez hello du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="62324-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="62324-128">**IMPORTANT**: rendre cloud de hello tooclick que service de rôle, pas hello instance de rôle qui est sous le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="62324-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="62324-129">Sélectionnez hello **échelle** vignette.</span><span class="sxs-lookup"><span data-stu-id="62324-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="62324-130">Mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="62324-130">Automatic scale</span></span>
<span data-ttu-id="62324-131">Vous pouvez configurer les paramètres de mise à l’échelle d’un rôle avec deux modes : **manuel** ou **automatique**.</span><span class="sxs-lookup"><span data-stu-id="62324-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="62324-132">Manuel est attendue, vous définissez le nombre absolu de hello d’instances.</span><span class="sxs-lookup"><span data-stu-id="62324-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="62324-133">Automatique vous permet cependant tooset règles déterminant comment et à quel beaucoup vous devant mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="62324-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="62324-134">Ensemble hello **l’échelle** option trop**les règles de performances et planification**.</span><span class="sxs-lookup"><span data-stu-id="62324-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Paramètres de mise à l’échelle de services cloud avec profil et règle](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="62324-136">Un profil existant.</span><span class="sxs-lookup"><span data-stu-id="62324-136">An existing profile.</span></span>
2. <span data-ttu-id="62324-137">Ajouter une règle pour le profil de hello parent.</span><span class="sxs-lookup"><span data-stu-id="62324-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="62324-138">Ajoutez un autre profil.</span><span class="sxs-lookup"><span data-stu-id="62324-138">Add another profile.</span></span>

<span data-ttu-id="62324-139">Sélectionnez **Ajouter un profil**.</span><span class="sxs-lookup"><span data-stu-id="62324-139">Select **Add Profile**.</span></span> <span data-ttu-id="62324-140">profil Hello détermine le mode souhaité pour la montée en puissance hello toouse : **toujours**, **périodicité**, **date fixe**.</span><span class="sxs-lookup"><span data-stu-id="62324-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="62324-141">Après avoir configuré les règles et les profils de hello, sélectionnez hello **enregistrer** icône haut hello.</span><span class="sxs-lookup"><span data-stu-id="62324-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="62324-142">Profil</span><span class="sxs-lookup"><span data-stu-id="62324-142">Profile</span></span>
<span data-ttu-id="62324-143">profil de Hello définit minimale et mettre à l’échelle d’instances maximales pour hello et également lorsque cette plage de l’échelle est active.</span><span class="sxs-lookup"><span data-stu-id="62324-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="62324-144">**Toujours**</span><span class="sxs-lookup"><span data-stu-id="62324-144">**Always**</span></span>

    <span data-ttu-id="62324-145">Toujours conserver cette plage d’instances disponible.</span><span class="sxs-lookup"><span data-stu-id="62324-145">Always keep this range of instances available.</span></span>  

    ![Service cloud toujours mis à l’échelle](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="62324-147">**Périodicité**</span><span class="sxs-lookup"><span data-stu-id="62324-147">**Recurrence**</span></span>

    <span data-ttu-id="62324-148">Choisissez un ensemble de jours de hello semaine tooscale.</span><span class="sxs-lookup"><span data-stu-id="62324-148">Choose a set of days of hello week tooscale.</span></span>

    ![Mise à l’échelle du service cloud avec une planification périodique](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="62324-150">**Date fixe**</span><span class="sxs-lookup"><span data-stu-id="62324-150">**Fixed Date**</span></span>

    <span data-ttu-id="62324-151">Un rôle de hello tooscale de plage date fixe.</span><span class="sxs-lookup"><span data-stu-id="62324-151">A fixed date range tooscale hello role.</span></span>

    ![Mise à l’échelle du service cloud avec une date fixe](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="62324-153">Une fois que vous avez configuré le profil de hello, sélectionnez hello **OK** bouton bas hello du Panneau de profil hello.</span><span class="sxs-lookup"><span data-stu-id="62324-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="62324-154">Règle</span><span class="sxs-lookup"><span data-stu-id="62324-154">Rule</span></span>
<span data-ttu-id="62324-155">Les règles sont ajoutées tooa profil et représentent une condition qui déclenche la montée en puissance hello.</span><span class="sxs-lookup"><span data-stu-id="62324-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="62324-156">déclencheur de la règle Hello est basé sur une mesure du service de cloud hello (utilisation de l’UC, l’activité du disque ou une activité de réseau) toowhich, vous pouvez ajouter une valeur conditionnelle.</span><span class="sxs-lookup"><span data-stu-id="62324-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="62324-157">En outre, vous pouvez avoir déclencheur hello basé sur une mesure de file d’attente ou hello message d’une autre ressource Azure associé à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="62324-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="62324-158">Une fois que vous avez configuré la règle de hello, sélectionnez hello **OK** bouton bas hello du Panneau de règle hello.</span><span class="sxs-lookup"><span data-stu-id="62324-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="62324-159">Mise à l’échelle toomanual précédent</span><span class="sxs-lookup"><span data-stu-id="62324-159">Back toomanual scale</span></span>
<span data-ttu-id="62324-160">Accédez toohello [paramètres d’échelle](#where-scale-is-located) et ensemble hello **l’échelle** option trop**un nombre d’instances que j’entre manuellement**.</span><span class="sxs-lookup"><span data-stu-id="62324-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Paramètres de mise à l’échelle de services cloud avec profil et règle](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="62324-162">Ce paramètre supprime la mise à l’échelle automatique du rôle de hello et vous pouvez définir le nombre d’instances hello directement.</span><span class="sxs-lookup"><span data-stu-id="62324-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="62324-163">option de mise à l’échelle (manuels ou automatisés) Hello.</span><span class="sxs-lookup"><span data-stu-id="62324-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="62324-164">Un rôle instance curseur tooset hello instances tooscale à.</span><span class="sxs-lookup"><span data-stu-id="62324-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="62324-165">Instances de tooscale de rôle hello pour.</span><span class="sxs-lookup"><span data-stu-id="62324-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="62324-166">Après avoir configuré les paramètres d’échelle hello, sélectionnez hello **enregistrer** icône haut hello.</span><span class="sxs-lookup"><span data-stu-id="62324-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
