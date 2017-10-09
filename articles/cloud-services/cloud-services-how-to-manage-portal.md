---
title: "tâches de gestion de service de cloud aaaCommon | Documents Microsoft"
description: "Découvrez comment toomanage cloud services Bonjour portail Azure. Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="40046-104">Comment les Services de cloud computing tooManage</span><span class="sxs-lookup"><span data-stu-id="40046-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40046-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="40046-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="40046-106">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="40046-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="40046-107">Bonjour **Services Cloud (classiques)** zone Hello Azure portail, vous pouvez mettre à jour un rôle de service ou d’un déploiement, promouvoir une tooproduction de déploiement par étapes, service de cloud de tooyour de ressources de liaison afin que vous puissiez voir les ressources hello dépendances et l’échelle hello ensemble de ressources et supprimer un service cloud ou un déploiement.</span><span class="sxs-lookup"><span data-stu-id="40046-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="40046-108">Plus d’informations sur la façon dont tooscale votre service cloud est disponible [ici](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40046-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="40046-109">Mise à jour d’un rôle ou d’un déploiement de service cloud</span><span class="sxs-lookup"><span data-stu-id="40046-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="40046-110">Si vous avez besoin de code de l’application hello tooupdate pour votre service cloud, utilisez **mise à jour** sur le panneau de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="40046-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="40046-111">Vous pouvez mettre à jour un ou plusieurs rôles.</span><span class="sxs-lookup"><span data-stu-id="40046-111">You can update a single role or all roles.</span></span> <span data-ttu-id="40046-112">tooupdate, vous pouvez télécharger un nouveau package de service ou d’un fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="40046-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="40046-113">Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service tooupdate.</span><span class="sxs-lookup"><span data-stu-id="40046-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="40046-114">Cette étape ouvre le panneau d’instance de service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="40046-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="40046-115">Dans le panneau de hello, cliquez sur hello **mise à jour** bouton.</span><span class="sxs-lookup"><span data-stu-id="40046-115">In hello blade, click hello **Update** button.</span></span>

    ![Bouton Update](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="40046-117">Mettre à jour le déploiement de hello avec un nouveau fichier de package de service (.cspkg) et le fichier de configuration de service (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="40046-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="40046-119">**Si vous le souhaitez** mettre à jour d’étiquette de déploiement hello et compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="40046-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="40046-120">Si tous les rôles ont une seule instance de rôle, sélectionnez hello **déployer même si un ou plusieurs rôles contiennent une seule instance** tooproceed de mise à niveau tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="40046-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="40046-121">Azure ne peut garantir 99,95 % de disponibilité du service pendant la mise à jour du service cloud que si chaque rôle dispose d'au moins deux instances de rôle (machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="40046-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="40046-122">Avec deux instances de rôle, un ordinateur virtuel traite les demandes des clients pendant la mise à jour de hello autres.</span><span class="sxs-lookup"><span data-stu-id="40046-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="40046-123">Vérifiez **démarrer le déploiement** toohave hello mise à jour appliquée une fois le téléchargement hello du package de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="40046-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="40046-124">Cliquez sur **OK** toobegin hello service mises à jour.</span><span class="sxs-lookup"><span data-stu-id="40046-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="40046-125">Comment : permuter les déploiements toopromote une tooproduction de déploiement par étapes</span><span class="sxs-lookup"><span data-stu-id="40046-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="40046-126">Lorsque vous décidez de toodeploy une nouvelle version d’un service cloud, étape et testez votre nouvelle version dans votre environnement intermédiaire du service cloud.</span><span class="sxs-lookup"><span data-stu-id="40046-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="40046-127">Utilisez **échanger** tooswitch hello URL par le hello deux déploiements sont traitées et promouvoir une nouveau tooproduction de mise en production.</span><span class="sxs-lookup"><span data-stu-id="40046-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="40046-128">Vous pouvez permuter les déploiements de hello **Services de cloud computing** hello ou la page tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="40046-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="40046-129">Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service tooupdate.</span><span class="sxs-lookup"><span data-stu-id="40046-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="40046-130">Cette étape ouvre le panneau d’instance de service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="40046-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="40046-131">Dans le panneau de hello, cliquez sur hello **échanger** bouton.</span><span class="sxs-lookup"><span data-stu-id="40046-131">In hello blade, click hello **Swap** button.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="40046-133">Hello de confirmation suivant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="40046-133">hello following confirmation prompt opens.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="40046-135">Après avoir vérifié les informations relatives au déploiement hello, cliquez sur **OK** tooswap des déploiements hello.</span><span class="sxs-lookup"><span data-stu-id="40046-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="40046-136">permutation de déploiement Hello se produit rapidement, car seul hello change est hello virtuels adresses IP (VIP) pour les déploiements de hello.</span><span class="sxs-lookup"><span data-stu-id="40046-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="40046-137">toosave les coûts de calcul, vous pouvez supprimer hello déploiement intermédiaire après avoir vérifié que votre déploiement de production fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="40046-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="40046-138">Questions courantes sur l’échange de déploiements</span><span class="sxs-lookup"><span data-stu-id="40046-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="40046-139">**Quelles sont les conditions préalables de hello pour l’échange des déploiements ?**</span><span class="sxs-lookup"><span data-stu-id="40046-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="40046-140">Il existe deux conditions préalables principales pour qu’un échange de déploiements réussisse :</span><span class="sxs-lookup"><span data-stu-id="40046-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="40046-141">Si vous souhaitez que toouse une adresse IP statique pour votre emplacement de production, vous devez réserver une pour votre emplacement de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="40046-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="40046-142">Sinon, échange de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="40046-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="40046-143">Toutes les instances de vos rôles doivent exécuter avant que vous pouvez effectuer hello.</span><span class="sxs-lookup"><span data-stu-id="40046-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="40046-144">Vous pouvez vérifier l’état de hello de vos instances dans le panneau de vue d’ensemble de hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40046-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="40046-145">Vous pouvez également utiliser hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) commande dans Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40046-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="40046-146">Notez que les mises à jour du système d’exploitation invité de déploiement peut également engendrer des opérations de réparation de service échange toofail.</span><span class="sxs-lookup"><span data-stu-id="40046-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="40046-147">Pour plus d’informations, consultez [Résoudre les problèmes de déploiement de service cloud](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="40046-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="40046-148">**Un échange implique-t-il un temps d’arrêt pour mon application ? Comment dois-je le gérer ?**</span><span class="sxs-lookup"><span data-stu-id="40046-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="40046-149">Comme décrit dans la dernière section de hello, une permutation de déploiement est généralement rapide, car elle est simplement une modification de configuration de l’équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="40046-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="40046-150">Toutefois, dans certains cas, il peut prendre au moins dix secondes et entraîner des échecs de connexion temporaires.</span><span class="sxs-lookup"><span data-stu-id="40046-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="40046-151">clients de tooyour toolimit impact, envisagez d’implémenter [logique de nouvelle tentative client](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="40046-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="40046-152">Comment : lier un service de cloud de ressource tooa</span><span class="sxs-lookup"><span data-stu-id="40046-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="40046-153">Hello portail Azure ne contient pas de liens ressources ensemble comme portail classique Azure actuel hello.</span><span class="sxs-lookup"><span data-stu-id="40046-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="40046-154">Au lieu de cela, déployer des ressources supplémentaires toohello même groupe de ressources utilisé par hello Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="40046-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="40046-155">Suppression de déploiements et d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="40046-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="40046-156">Avant de pouvoir supprimer un service cloud, vous devez supprimer tous les déploiements existants.</span><span class="sxs-lookup"><span data-stu-id="40046-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="40046-157">toosave les coûts de calcul, vous pouvez supprimer hello déploiement intermédiaire après avoir vérifié que votre déploiement de production fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="40046-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="40046-158">Vous êtes facturé pour les coûts de calcul des instances de rôle déployées qui ont été arrêtées.</span><span class="sxs-lookup"><span data-stu-id="40046-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="40046-159">Utilisez hello suivant la procédure toodelete un déploiement ou votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="40046-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="40046-160">Bonjour [portail Azure][Azure portal], sélectionnez hello cloud service toodelete.</span><span class="sxs-lookup"><span data-stu-id="40046-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="40046-161">Cette étape ouvre le panneau d’instance de service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="40046-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="40046-162">Dans le panneau de hello, cliquez sur hello **supprimer** bouton.</span><span class="sxs-lookup"><span data-stu-id="40046-162">In hello blade, click hello **Delete** button.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="40046-164">Vous pouvez supprimer le service de cloud entière hello en vérifiant **le service Cloud et ses déploiements** ou choisissez soit hello **déploiement de Production** ou hello **déploiement intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="40046-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="40046-166">Cliquez sur hello **supprimer** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="40046-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="40046-167">service de cloud toodelete hello, cliquez sur **supprimer le service cloud**.</span><span class="sxs-lookup"><span data-stu-id="40046-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="40046-168">Ensuite, à l’invite de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="40046-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="40046-169">Lorsqu’un service cloud est supprimé, et la surveillance détaillée est configurée, vous devez supprimer manuellement les données de salutation à partir de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="40046-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="40046-170">Pour savoir où toofind hello tables de métriques, consultez [cela](cloud-services-how-to-monitor.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="40046-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="40046-171">Comment trouver plus d’informations sur les déploiements échoués</span><span class="sxs-lookup"><span data-stu-id="40046-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="40046-172">Hello **vue d’ensemble** panneau a une barre d’état en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="40046-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="40046-173">Lorsque vous cliquez sur la barre de hello, un nouveau panneau s’ouvre et affiche des informations sur l’erreur.</span><span class="sxs-lookup"><span data-stu-id="40046-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="40046-174">Si le déploiement de hello ne contient pas toutes les erreurs, le panneau d’informations hello est vide.</span><span class="sxs-lookup"><span data-stu-id="40046-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="40046-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40046-176">Next steps</span></span>
* <span data-ttu-id="40046-177">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40046-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="40046-178">Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40046-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="40046-179">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40046-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="40046-180">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40046-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
