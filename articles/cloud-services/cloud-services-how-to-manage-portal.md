---
title: "Tâches courantes de gestion de service cloud | Microsoft Docs"
description: "Découvrez comment gérer des services cloud dans le portail Azure. Ces exemples utilisent le portail Azure."
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="37f24-104">Gestion des services cloud</span><span class="sxs-lookup"><span data-stu-id="37f24-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37f24-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="37f24-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="37f24-106">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="37f24-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="37f24-107">Dans la zone **Services cloud (classique)** du portail Azure, vous pouvez mettre à jour un rôle de service ou un déploiement, promouvoir un déploiement intermédiaire en déploiement de production, lier des ressources à votre service cloud afin de voir les dépendances de ressources et d’étendre les ressources en même temps, mais aussi supprimer un service cloud ou un déploiement.</span><span class="sxs-lookup"><span data-stu-id="37f24-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="37f24-108">Vous trouverez plus d’informations sur la mise à l’échelle de votre service cloud [ici](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="37f24-109">Mise à jour d’un rôle ou d’un déploiement de service cloud</span><span class="sxs-lookup"><span data-stu-id="37f24-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="37f24-110">Si vous devez mettre à jour le code de l'application pour votre service cloud, utilisez **Update** dans le panneau de service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="37f24-111">Vous pouvez mettre à jour un ou plusieurs rôles.</span><span class="sxs-lookup"><span data-stu-id="37f24-111">You can update a single role or all roles.</span></span> <span data-ttu-id="37f24-112">Pour effectuer la mise à jour, vous pouvez charger un nouveau package de service ou un nouveau fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="37f24-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="37f24-113">Dans le [portail Azure][Azure portal], sélectionnez le service cloud à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="37f24-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="37f24-114">Cette étape ouvre le panneau d'instance de service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="37f24-115">Dans le panneau, cliquez sur le bouton **Update** .</span><span class="sxs-lookup"><span data-stu-id="37f24-115">In the blade, click the **Update** button.</span></span>

    ![Bouton Update](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="37f24-117">Mettez à jour le déploiement avec un nouveau fichier de package de service (.cspkg) et un fichier de configuration de service (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="37f24-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="37f24-119">**éventuellement** à jour l'étiquette de déploiement et le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="37f24-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="37f24-120">Si l’un des rôles ne comporte qu’une seule instance, sélectionnez **Déployer même si un ou plusieurs rôles contiennent une seule instance** afin de permettre à la mise à niveau de continuer.</span><span class="sxs-lookup"><span data-stu-id="37f24-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="37f24-121">Azure ne peut garantir 99,95 % de disponibilité du service pendant la mise à jour du service cloud que si chaque rôle dispose d'au moins deux instances de rôle (machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="37f24-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="37f24-122">Avec deux instances de rôle, une machine virtuelle traite les demandes du client pendant que l'autre est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="37f24-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="37f24-123">Cochez la case **Démarrer le déploiement** pour appliquer la mise à jour après le téléchargement du package.</span><span class="sxs-lookup"><span data-stu-id="37f24-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="37f24-124">Cliquez sur **OK** pour démarrer la mise à jour du service.</span><span class="sxs-lookup"><span data-stu-id="37f24-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="37f24-125">Inversion de déploiements pour faire passer un déploiement intermédiaire en production</span><span class="sxs-lookup"><span data-stu-id="37f24-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="37f24-126">Lorsque vous décidez de déployer une nouvelle version d'un service cloud, créez un déploiement intermédiaire et testez la nouvelle version dans l'environnement intermédiaire de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="37f24-127">Utilisez **Swap** pour inverser les URL qui permettent d'accéder aux deux déploiements et de faire passer une nouvelle version en production.</span><span class="sxs-lookup"><span data-stu-id="37f24-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="37f24-128">Vous pouvez inverser les déploiements à partir de la page **Cloud Services** ou du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="37f24-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="37f24-129">Dans le [portail Azure][Azure portal], sélectionnez le service cloud à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="37f24-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="37f24-130">Cette étape ouvre le panneau d'instance de service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="37f24-131">Dans le panneau, cliquez sur le bouton **Swap** .</span><span class="sxs-lookup"><span data-stu-id="37f24-131">In the blade, click the **Swap** button.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="37f24-133">L'invite de confirmation suivante s'affiche.</span><span class="sxs-lookup"><span data-stu-id="37f24-133">The following confirmation prompt opens.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="37f24-135">Une fois les informations de déploiement vérifiées, cliquez sur **OK** pour inverser les déploiements.</span><span class="sxs-lookup"><span data-stu-id="37f24-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="37f24-136">L'inversion des déploiements se fait rapidement, car la seule chose qui change est l'adresse IP virtuelle (VIP) des déploiements.</span><span class="sxs-lookup"><span data-stu-id="37f24-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="37f24-137">Afin de réduire les coûts liés au calcul, vous pouvez supprimer le déploiement intermédiaire une fois que vous êtes certain que votre déploiement de production se comporte comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="37f24-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="37f24-138">Questions courantes sur l’échange de déploiements</span><span class="sxs-lookup"><span data-stu-id="37f24-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="37f24-139">**Quelles sont les conditions préalables à l’échange des déploiements ?**</span><span class="sxs-lookup"><span data-stu-id="37f24-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="37f24-140">Il existe deux conditions préalables principales pour qu’un échange de déploiements réussisse :</span><span class="sxs-lookup"><span data-stu-id="37f24-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="37f24-141">Si vous souhaitez utiliser une adresse IP statique pour votre emplacement de production, vous devez en réserver une pour votre emplacement intermédiaire également.</span><span class="sxs-lookup"><span data-stu-id="37f24-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="37f24-142">Sinon, l’échange échoue.</span><span class="sxs-lookup"><span data-stu-id="37f24-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="37f24-143">Toutes les instances de vos rôles doivent être en cours d’exécution pour que vous puissiez effectuer l’échange.</span><span class="sxs-lookup"><span data-stu-id="37f24-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="37f24-144">Vous pouvez vérifier l’état de vos instances dans le volet d’aperçu du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37f24-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="37f24-145">Vous pouvez également utiliser la commande [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) dans Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37f24-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="37f24-146">Notez que les mises à jour du système d’exploitation invité et les opérations de réparation de service peuvent entraîner l’échec du déploiement.</span><span class="sxs-lookup"><span data-stu-id="37f24-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="37f24-147">Pour plus d’informations, consultez [Résoudre les problèmes de déploiement de service cloud](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="37f24-148">**Un échange implique-t-il un temps d’arrêt pour mon application ? Comment dois-je le gérer ?**</span><span class="sxs-lookup"><span data-stu-id="37f24-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="37f24-149">Comme décrit dans la dernière section, un échange de déploiements est généralement rapide puisqu’il s’agit simplement d’une modification de configuration d’Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="37f24-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="37f24-150">Toutefois, dans certains cas, il peut prendre au moins dix secondes et entraîner des échecs de connexion temporaires.</span><span class="sxs-lookup"><span data-stu-id="37f24-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="37f24-151">Pour limiter l’impact sur vos clients, envisagez d’implémenter la [logique de nouvelle tentative client](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="37f24-152">Liaison d’une ressource à un service cloud</span><span class="sxs-lookup"><span data-stu-id="37f24-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="37f24-153">Le portail Azure ne lie pas les ressources comme le fait le portail Azure Classic actuel.</span><span class="sxs-lookup"><span data-stu-id="37f24-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="37f24-154">Déployez plutôt des ressources supplémentaires vers le même groupe de ressources que celui utilisé par le service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="37f24-155">Suppression de déploiements et d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="37f24-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="37f24-156">Avant de pouvoir supprimer un service cloud, vous devez supprimer tous les déploiements existants.</span><span class="sxs-lookup"><span data-stu-id="37f24-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="37f24-157">Afin de réduire les coûts liés au calcul, vous pouvez supprimer le déploiement intermédiaire une fois que vous êtes certain que votre déploiement de production se comporte comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="37f24-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="37f24-158">Vous êtes facturé pour les coûts de calcul des instances de rôle déployées qui ont été arrêtées.</span><span class="sxs-lookup"><span data-stu-id="37f24-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="37f24-159">Utiliser la procédure suivante pour supprimer un déploiement ou un service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="37f24-160">Dans le [portail Azure][Azure portal], sélectionnez le service cloud à supprimer.</span><span class="sxs-lookup"><span data-stu-id="37f24-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="37f24-161">Cette étape ouvre le panneau d'instance de service cloud.</span><span class="sxs-lookup"><span data-stu-id="37f24-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="37f24-162">Dans le panneau, cliquez sur le bouton **Delete** .</span><span class="sxs-lookup"><span data-stu-id="37f24-162">In the blade, click the **Delete** button.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="37f24-164">Vous pouvez supprimer tout le service cloud en cochant **Service cloud et ses déploiements**, ou bien choisir le **déploiement de production** ou le **déploiement intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="37f24-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="37f24-166">Cliquez sur le bouton **Delete** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="37f24-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="37f24-167">Pour supprimer le service cloud, cliquez sur **Delete cloud service**.</span><span class="sxs-lookup"><span data-stu-id="37f24-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="37f24-168">Ensuite, à l'invite de confirmation, cliquez sur **Yes**.</span><span class="sxs-lookup"><span data-stu-id="37f24-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="37f24-169">Lorsqu’un service cloud est supprimé et que la surveillance détaillée est configurée, vous devez supprimer manuellement les données de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="37f24-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="37f24-170">Pour plus d'informations sur les tables de mesures, consultez [cet](cloud-services-how-to-monitor.md) article.</span><span class="sxs-lookup"><span data-stu-id="37f24-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="37f24-171">Comment trouver plus d’informations sur les déploiements échoués</span><span class="sxs-lookup"><span data-stu-id="37f24-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="37f24-172">Le panneau **d’aperçu** possède une barre d’état en haut.</span><span class="sxs-lookup"><span data-stu-id="37f24-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="37f24-173">Lorsque vous cliquez sur la barre, un nouveau panneau s’ouvre et affiche toutes les informations d’erreur.</span><span class="sxs-lookup"><span data-stu-id="37f24-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="37f24-174">Si le déploiement ne contient pas d’erreurs, le panneau informations est vide.</span><span class="sxs-lookup"><span data-stu-id="37f24-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Inverser les services cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="37f24-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37f24-176">Next steps</span></span>
* <span data-ttu-id="37f24-177">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="37f24-178">Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="37f24-179">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="37f24-180">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37f24-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
