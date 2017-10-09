---
title: "aaaVisualizing votre cluster à l’aide du Service Fabric Explorer | Documents Microsoft"
description: "Service Fabric Explorer est un outil web dédié à l’inspection et à la gestion des applications cloud et des nœuds dans un cluster Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="e7441-103">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e7441-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="e7441-104">Service Fabric Explorer est un outil web dédié à l’inspection et à la gestion d’applications et de nœuds dans un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e7441-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e7441-105">Service Fabric Explorer est hébergé directement dans le cluster de hello, elle est toujours disponible, quel que soit l’où votre cluster est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e7441-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="e7441-106">Didacticiel vidéo</span><span class="sxs-lookup"><span data-stu-id="e7441-106">Video tutorial</span></span>

<span data-ttu-id="e7441-107">toolearn comment toouse Service Fabric Explorer, regardez hello suivant vidéo de Microsoft Virtual Academy :</span><span class="sxs-lookup"><span data-stu-id="e7441-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="e7441-108">Se connecter tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e7441-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="e7441-109">Si vous avez suivi les instructions hello trop[préparer votre environnement de développement](service-fabric-get-started.md), vous pouvez lancer le Service Fabric Explorer votre cluster local en naviguant toohttp://localhost:19080 / Explorer.</span><span class="sxs-lookup"><span data-stu-id="e7441-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="e7441-110">Comprendre la mise en page du Service Fabric Explorer hello</span><span class="sxs-lookup"><span data-stu-id="e7441-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="e7441-111">Vous pouvez naviguer dans le Service Fabric Explorer à l’aide d’arborescence de hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="e7441-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="e7441-112">À la racine de hello d’arborescence de hello, tableau de bord hello cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’application et d’intégrité de nœud.</span><span class="sxs-lookup"><span data-stu-id="e7441-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Tableau de bord de cluster de Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="e7441-114">Afficher la mise en page du cluster hello</span><span class="sxs-lookup"><span data-stu-id="e7441-114">View hello cluster's layout</span></span>
<span data-ttu-id="e7441-115">Les nœuds dans un cluster Service Fabric sont répartis dans une grille à deux dimensions composée de domaines d’erreur et de domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="e7441-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="e7441-116">Ce positionnement garantit que vos applications restent disponibles en présence de hello de mises à niveau de l’application et des défaillances matérielles.</span><span class="sxs-lookup"><span data-stu-id="e7441-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="e7441-117">Vous pouvez afficher la façon dont le cluster actuel hello est disposé à l’aide de carte de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Mappage de cluster de Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="e7441-119">Afficher les applications et les services</span><span class="sxs-lookup"><span data-stu-id="e7441-119">View applications and services</span></span>
<span data-ttu-id="e7441-120">cluster de Hello contient deux sous-arborescences : une pour les applications et un autre pour les nœuds.</span><span class="sxs-lookup"><span data-stu-id="e7441-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="e7441-121">Vous pouvez utiliser hello application vue toonavigate via la hiérarchie logique de l’architecture de Service : applications, services, partitions et réplicas.</span><span class="sxs-lookup"><span data-stu-id="e7441-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="e7441-122">Dans l’exemple hello ci-dessous, hello application **MyApp** se compose de deux services, **MyStatefulService** et **WebService**.</span><span class="sxs-lookup"><span data-stu-id="e7441-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="e7441-123">Étant donné que **MyStatefulService** est une application avec état, elle inclut une partition avec un réplica principal et deux réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="e7441-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="e7441-124">En revanche, WebSvcService est une application sans état qui ne contient qu’une seule instance.</span><span class="sxs-lookup"><span data-stu-id="e7441-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Affichage des applications de Service Fabric Explorer][sfx-application-tree]

<span data-ttu-id="e7441-126">À chaque niveau de l’arborescence de hello, volet principal de hello affiche des informations pertinentes sur l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="e7441-127">Par exemple, vous pouvez voir l’état d’intégrité hello et version pour un service particulier.</span><span class="sxs-lookup"><span data-stu-id="e7441-127">For example, you can see hello health status and version for a particular service.</span></span>

![Volet des éléments essentiels de Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="e7441-129">Afficher les nœuds du cluster hello</span><span class="sxs-lookup"><span data-stu-id="e7441-129">View hello cluster's nodes</span></span>
<span data-ttu-id="e7441-130">affichage du nœud Hello montre la disposition physique de hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="e7441-131">Vous pouvez identifier les applications ayant déployé du code sur un nœud donné.</span><span class="sxs-lookup"><span data-stu-id="e7441-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="e7441-132">Plus particulièrement, vous pouvez voir les réplicas en cours d’exécution sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="e7441-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="e7441-133">Actions</span><span class="sxs-lookup"><span data-stu-id="e7441-133">Actions</span></span>
<span data-ttu-id="e7441-134">Service Fabric Explorer offre un moyen rapide de tooinvoke actions sur les nœuds, les applications et services au sein de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="e7441-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="e7441-135">Par exemple, toodelete une instance d’application, choisissez application hello à partir de l’arborescence hello sur hello gauche, puis **Actions** > **supprimer l’Application**.</span><span class="sxs-lookup"><span data-stu-id="e7441-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Suppression d’une application dans Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="e7441-137">Vous pouvez effectuer hello les mêmes actions en cliquant sur élément tooeach suivant de hello points de suspension.</span><span class="sxs-lookup"><span data-stu-id="e7441-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="e7441-138">Hello tableau suivant répertorie les actions de hello disponibles pour chaque entité :</span><span class="sxs-lookup"><span data-stu-id="e7441-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="e7441-139">**Entité**</span><span class="sxs-lookup"><span data-stu-id="e7441-139">**Entity**</span></span> | <span data-ttu-id="e7441-140">**Action**</span><span class="sxs-lookup"><span data-stu-id="e7441-140">**Action**</span></span> | <span data-ttu-id="e7441-141">**Description**</span><span class="sxs-lookup"><span data-stu-id="e7441-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7441-142">Type d’application</span><span class="sxs-lookup"><span data-stu-id="e7441-142">Application type</span></span> |<span data-ttu-id="e7441-143">Type de mise hors service</span><span class="sxs-lookup"><span data-stu-id="e7441-143">Unprovision type</span></span> |<span data-ttu-id="e7441-144">Supprime le package d’application hello à partir du magasin d’images du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="e7441-145">Nécessite toutes les applications de ce toobe type supprimé en premier.</span><span class="sxs-lookup"><span data-stu-id="e7441-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="e7441-146">Application</span><span class="sxs-lookup"><span data-stu-id="e7441-146">Application</span></span> |<span data-ttu-id="e7441-147">Supprimer l’application</span><span class="sxs-lookup"><span data-stu-id="e7441-147">Delete Application</span></span> |<span data-ttu-id="e7441-148">Supprimer l’application hello, y compris tous ses services et leur état (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="e7441-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="e7441-149">Service</span><span class="sxs-lookup"><span data-stu-id="e7441-149">Service</span></span> |<span data-ttu-id="e7441-150">Supprimer le service</span><span class="sxs-lookup"><span data-stu-id="e7441-150">Delete Service</span></span> |<span data-ttu-id="e7441-151">Supprimer le service de hello et son état (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="e7441-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="e7441-152">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-152">Node</span></span> |<span data-ttu-id="e7441-153">Activer</span><span class="sxs-lookup"><span data-stu-id="e7441-153">Activate</span></span> |<span data-ttu-id="e7441-154">Activer le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-154">Activate hello node.</span></span> |
| <span data-ttu-id="e7441-155">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-155">Node</span></span> | <span data-ttu-id="e7441-156">Désactiver (pause)</span><span class="sxs-lookup"><span data-stu-id="e7441-156">Deactivate (pause)</span></span> | <span data-ttu-id="e7441-157">Suspendre le nœud hello dans son état actuel.</span><span class="sxs-lookup"><span data-stu-id="e7441-157">Pause hello node in its current state.</span></span> <span data-ttu-id="e7441-158">Services continuent toorun mais Service Fabric ne déplace pas les proactive quoi que ce soit sur ou déconnecter, sauf si elle est requise tooprevent une panne ou une incohérence des données.</span><span class="sxs-lookup"><span data-stu-id="e7441-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="e7441-159">Cette action est généralement utilisé tooenable tooensure un nœud spécifique qui elles ne déplacent pas lors de l’inspection, les services de débogage.</span><span class="sxs-lookup"><span data-stu-id="e7441-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="e7441-160">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-160">Node</span></span> | <span data-ttu-id="e7441-161">Désactiver (redémarrage)</span><span class="sxs-lookup"><span data-stu-id="e7441-161">Deactivate (restart)</span></span> | <span data-ttu-id="e7441-162">Déplace en toute sécurité tous les services en mémoire d’un nœud et ferme les services persistants.</span><span class="sxs-lookup"><span data-stu-id="e7441-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="e7441-163">Généralement utilisé lorsque le processus hôte de hello ou ordinateur besoin toobe redémarré.</span><span class="sxs-lookup"><span data-stu-id="e7441-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="e7441-164">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-164">Node</span></span> | <span data-ttu-id="e7441-165">Désactiver (suppression de données)</span><span class="sxs-lookup"><span data-stu-id="e7441-165">Deactivate (remove data)</span></span> | <span data-ttu-id="e7441-166">En toute sécurité, fermez tous les services en cours d’exécution sur le nœud de hello après la génération de réplicas de rechange suffisantes.</span><span class="sxs-lookup"><span data-stu-id="e7441-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="e7441-167">Généralement utilisé quand un nœud (ou au moins son stockage) est définitivement mis hors service.</span><span class="sxs-lookup"><span data-stu-id="e7441-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="e7441-168">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-168">Node</span></span> | <span data-ttu-id="e7441-169">Supprimer l’état du nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-169">Remove node state</span></span> | <span data-ttu-id="e7441-170">Supprimer les connaissances de réplicas d’un nœud du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="e7441-171">Généralement utilisé quand un nœud déjà défaillant est considéré comme irrécupérable.</span><span class="sxs-lookup"><span data-stu-id="e7441-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="e7441-172">Nœud</span><span class="sxs-lookup"><span data-stu-id="e7441-172">Node</span></span> | <span data-ttu-id="e7441-173">Redémarrer</span><span class="sxs-lookup"><span data-stu-id="e7441-173">Restart</span></span> | <span data-ttu-id="e7441-174">Simuler un échec de nœud en redémarrant le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="e7441-175">Plus d’informations [ici](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="e7441-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="e7441-176">Étant donné que de nombreuses actions sont destructeurs, vous pouvez être invité tooconfirm votre intention avant hello action est terminée.</span><span class="sxs-lookup"><span data-stu-id="e7441-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="e7441-177">Toutes les actions qui peuvent être effectuées via l’Explorateur de l’infrastructure de Service peuvent également être effectuée via PowerShell ou une API REST, tooenable automation.</span><span class="sxs-lookup"><span data-stu-id="e7441-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="e7441-178">Vous pouvez également utiliser des instances de l’application Service Fabric Explorer toocreate pour un type d’application donné et une version.</span><span class="sxs-lookup"><span data-stu-id="e7441-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="e7441-179">Choisissez le type d’application hello dans l’arborescence de hello, puis cliquez sur hello **créer une instance application** version toohello suivante de liaison souhaité dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Création d’une instance application dans Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="e7441-181">Les instances d’application créées via le Service Fabric Explorer ne peuvent actuellement pas être paramétrées.</span><span class="sxs-lookup"><span data-stu-id="e7441-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="e7441-182">Elles sont créées à l’aide des valeurs de paramètre par défaut.</span><span class="sxs-lookup"><span data-stu-id="e7441-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="e7441-183">Se connecter à distance des clusters Service Fabric tooa</span><span class="sxs-lookup"><span data-stu-id="e7441-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="e7441-184">Si vous connaissez le point de terminaison du cluster hello et que vous disposez des autorisations suffisantes, vous pouvez accéder Service Fabric Explorer à partir de n’importe quel navigateur.</span><span class="sxs-lookup"><span data-stu-id="e7441-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="e7441-185">Il s’agit, car le Service Fabric Explorer est simplement un autre service qui s’exécute dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="e7441-186">Découvrir le point de terminaison de Service Fabric Explorer hello pour un cluster à distance</span><span class="sxs-lookup"><span data-stu-id="e7441-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="e7441-187">tooreach Service Fabric Explorer pour un cluster donné, pointez votre navigateur sur :</span><span class="sxs-lookup"><span data-stu-id="e7441-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="e7441-188">http://&lt;point-de-terminaison-de-votre-cluster&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="e7441-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="e7441-189">Pour les clusters Azure, une URL complète hello est également disponible dans hello cluster essentials volet Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e7441-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="e7441-190">Connecter le cluster sécurisée de tooa</span><span class="sxs-lookup"><span data-stu-id="e7441-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="e7441-191">Vous pouvez contrôler le cluster Service Fabric tooyour client d’accès avec des certificats ou à l’aide d’Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="e7441-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="e7441-192">Si vous essayez de tooconnect tooService Fabric Explorer sur un cluster sécurisé, puis en fonction de la configuration du cluster hello vous envisagez toopresent requis un certificat client ou connectez-vous à l’aide d’AAD.</span><span class="sxs-lookup"><span data-stu-id="e7441-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7441-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7441-193">Next steps</span></span>
* [<span data-ttu-id="e7441-194">Vue d’ensemble de la testabilité</span><span class="sxs-lookup"><span data-stu-id="e7441-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="e7441-195">Gestion de vos applications Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7441-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="e7441-196">Déploiement d’application Service Fabrix à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7441-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
