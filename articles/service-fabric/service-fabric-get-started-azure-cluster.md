---
title: "aaaSet configuration d’un cluster Azure Service Fabric | Documents Microsoft"
description: "Démarrage rapide - Créer un cluster Service Fabric Windows ou Linux sur Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="f9b9b-103">Créer votre premier cluster Service Fabric sur Azure</span><span class="sxs-lookup"><span data-stu-id="f9b9b-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="f9b9b-104">Un [cluster Service Fabric](service-fabric-deploy-anywhere.md) est un groupe de machines virtuelles ou physiques connectées au réseau, sur lequel vos microservices sont déployés et gérés.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="f9b9b-105">Ce démarrage rapide vous aide à toocreate un cluster de cinq nœuds, en cours d’exécution sur Windows ou Linux, via hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portail Azure](http://portal.azure.com) dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="f9b9b-106">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="f9b9b-107">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f9b9b-107">Use hello Azure portal</span></span>

<span data-ttu-id="f9b9b-108">Connectez-vous toohello portail Azure à l’adresse [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9b9b-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="f9b9b-109">Créer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="f9b9b-109">Create hello cluster</span></span>

1. <span data-ttu-id="f9b9b-110">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="f9b9b-111">Sélectionnez **de calcul** de hello **nouveau** panneau, puis sélectionnez **Cluster Service Fabric** de hello **de calcul** panneau.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="f9b9b-112">Remplir hello Service Fabric **notions de base** formulaire.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="f9b9b-113">Pour **système d’exploitation**, sélectionnez version hello de Windows ou Linux que vous souhaitez hello toorun des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="f9b9b-114">nom d’utilisateur Hello et le mot de passe entré ici est toolog utilisé dans la machine virtuelle de toohello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="f9b9b-115">Pour **Groupe de ressources** créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="f9b9b-116">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont créées et gérées collectivement.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="f9b9b-117">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-117">When complete, click **OK**.</span></span>

    ![Résultat de configuration du cluster][cluster-setup-basics]

4. <span data-ttu-id="f9b9b-119">Remplir hello **configuration de Cluster** formulaire.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="f9b9b-120">Dans **Nombre de type de nœud**, mettez « 1 ».</span><span class="sxs-lookup"><span data-stu-id="f9b9b-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="f9b9b-121">Sélectionnez **le type de nœud 1 (principal)** et remplissez hello **configuration du type de nœud** formulaire.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="f9b9b-122">Entrez un nom de type de nœud et définissez hello [le niveau de durabilité](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) trop « Bronze ».</span><span class="sxs-lookup"><span data-stu-id="f9b9b-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="f9b9b-123">Sélectionnez une taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-123">Select a VM size.</span></span>

    <span data-ttu-id="f9b9b-124">Taille de machine virtuelle hello, nombre d’ordinateurs virtuels, des points de terminaison personnalisés, définissent des types de nœuds et d’autres paramètres pour hello des machines virtuelles de ce type.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="f9b9b-125">Chaque type de nœud défini est configuré comme un ensemble d’échelle de machine virtuelle distincte, qui est utilisé toodeploy et les machines virtuelles gérées en tant qu’ensemble.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="f9b9b-126">Chaque type de nœud peut faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="f9b9b-127">Hello premier ou principal, type de nœud est où les services de système de l’infrastructure de Service sont hébergés et doivent avoir cinq ou plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="f9b9b-128">Pour un déploiement de production, la [planification de la capacité](service-fabric-cluster-capacity.md) est une étape importante.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="f9b9b-129">Pour ce guide de démarrage rapide, toutefois, vous n’exécutez pas d’applications. Vous pouvez donc sélectionner la taille de machine virtuelle *DS1_v2 Standard*.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="f9b9b-130">Sélectionnez « Silver » pour hello [niveau de fiabilité](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) et une échelle de machine virtuelle initiale définie la capacité de 5.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="f9b9b-131">Points de terminaison personnalisés ouvrent des ports dans l’équilibrage de charge Azure hello afin que vous pouvez vous connecter avec les applications qui s’exécutent sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="f9b9b-132">Entrez « 80, 8172 » tooopen les ports 80 et 8172.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="f9b9b-133">Ne pas vérifier hello **configurer des paramètres avancés** boîte, qui est utilisée pour la personnalisation de points de terminaison de la gestion de TCP/HTTP, plages de ports d’application, [les contraintes de placement](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), et [capacité propriétés](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f9b9b-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="f9b9b-134">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-134">Select **OK**.</span></span>

6. <span data-ttu-id="f9b9b-135">Bonjour **configuration de Cluster** écran, définissez **Diagnostics** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="f9b9b-136">Pour ce démarrage rapide, vous ne devez pas tooenter toute [définition de l’ensemble fibre optique](service-fabric-cluster-fabric-settings.md) propriétés.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="f9b9b-137">Dans **la version de Fabric**, sélectionnez **automatique** mise à niveau en mode afin que Microsoft met automatiquement à jour la version de hello du code de l’ensemble fibre optique de hello exécution hello cluster.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="f9b9b-138">Définir le mode hello trop**manuel** si vous souhaitez trop[choisir une version prise en charge](service-fabric-cluster-upgrade.md) tooupgrade à.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configuration du type de nœud][node-type-config]

    <span data-ttu-id="f9b9b-140">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-140">Select **OK**.</span></span>

7. <span data-ttu-id="f9b9b-141">Remplir hello **sécurité** formulaire.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="f9b9b-142">Pour ce guide de démarrage rapide, sélectionnez **Non sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="f9b9b-143">Il est vivement recommandé de toocreate un cluster sécurisé pour les charges de production, toutefois, étant donné que toute personne peut anonymement connecter tooan des clusters non sécurisés et effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="f9b9b-144">Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="f9b9b-145">Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="f9b9b-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="f9b9b-146">à l’aide d’Azure Active Directory ou tooset des certificats pour la sécurité de l’application, l’authentification utilisateur tooenable [créer un cluster à partir d’un modèle de gestionnaire de ressources](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f9b9b-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="f9b9b-147">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-147">Select **OK**.</span></span>

8. <span data-ttu-id="f9b9b-148">Hello de révision résumé.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-148">Review hello summary.</span></span>  <span data-ttu-id="f9b9b-149">Si vous souhaitez que toodownload un modèle de gestionnaire de ressources généré à partir des paramètres de hello que vous avez entrées, sélectionnez **télécharger le modèle et les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="f9b9b-150">Sélectionnez **créer** cluster hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="f9b9b-151">Vous pouvez voir la progression de la création de hello dans les notifications de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="f9b9b-152">(Cliquez sur l’icône de hello « cloche » près de barre d’état hello au niveau supérieur de hello à droite de votre écran.) Si vous avez cliqué sur **code confidentiel tooStartboard** lors de la création de cluster de hello, vous voyez **déploiement d’un Cluster Service Fabric** épinglé toohello **Démarrer** carte.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="f9b9b-153">Afficher l’état du cluster</span><span class="sxs-lookup"><span data-stu-id="f9b9b-153">View cluster status</span></span>
<span data-ttu-id="f9b9b-154">Une fois que votre cluster est créé, vous pouvez inspecter votre cluster Bonjour **vue d’ensemble** panneau dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="f9b9b-155">Vous pouvez maintenant voir les détails de hello de votre cluster dans le tableau de bord hello, y compris le point de terminaison public du cluster hello et un lien de tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![État du cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="f9b9b-157">Visualiser le cluster hello à l’aide de l’Explorateur de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f9b9b-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="f9b9b-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un bon outil pour visualiser votre cluster et gérer les applications.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="f9b9b-159">Service Fabric Explorer est un service qui s’exécute dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="f9b9b-160">Accéder à l’aide d’un navigateur web en cliquant sur hello **Service Fabric Explorer** lien du cluster de hello **vue d’ensemble** page hello portail.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="f9b9b-161">Vous pouvez également entrer l’adresse de hello directement dans le navigateur de hello : [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="f9b9b-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="f9b9b-162">tableau de bord Hello cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’application et d’intégrité de nœud.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="f9b9b-163">affichage du nœud Hello montre la disposition physique de hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="f9b9b-164">Vous pouvez identifier les applications ayant déployé du code sur un nœud donné.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="f9b9b-166">Connecter le cluster toohello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9b9b-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="f9b9b-167">Vérifiez que le cluster hello est en cours d’exécution en vous connectant à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="f9b9b-168">module ServiceFabric PowerShell Hello est installé avec hello [Service Fabric SDK](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9b9b-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="f9b9b-169">Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande établit un cluster de toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="f9b9b-170">Consultez [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md) pour obtenir des exemples de connexion tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="f9b9b-171">Après la connexion toohello cluster, utilisez hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay de l’applet de commande une liste de nœuds dans les informations de cluster et d’état hello pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="f9b9b-172">**HealthState** doit être à l’état *OK* pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="f9b9b-173">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="f9b9b-173">Remove hello cluster</span></span>
<span data-ttu-id="f9b9b-174">Un cluster Service Fabric est constitué d’autres ressources Windows Azure en outre toohello du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="f9b9b-175">Toocompletely supprimer un cluster Service Fabric, vous devez également toodelete que tous hello il est constitué de ressources.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="f9b9b-176">cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="f9b9b-177">Pour les autres toodelete comme un cluster ou un toodelete certaines ressources (mais pas toutes) hello dans un groupe de ressources, consultez [supprimer un cluster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="f9b9b-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="f9b9b-178">Supprimer un groupe de ressources Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="f9b9b-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="f9b9b-179">Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="f9b9b-180">Cliquez sur hello **groupe de ressources** nom sur la page d’essentials hello cluster.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="f9b9b-181">Bonjour **Essentials du groupe de ressources** , cliquez sur **supprimer le groupe de ressources** et suivez les instructions de hello sur cette page toocomplete hello la suppression du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="f9b9b-182">![Supprimer le groupe de ressources hello][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="f9b9b-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="f9b9b-183">Utiliser Azure Powershell toodeploy un cluster sécurisé</span><span class="sxs-lookup"><span data-stu-id="f9b9b-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="f9b9b-184">Télécharger hello [Azure Powershell version 4.0 ou version ultérieure du module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="f9b9b-185">Ouvrez une fenêtre Windows PowerShell, hello exécuter commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="f9b9b-186">Vous devez voir s’afficher une sortie similaire toohello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-186">You should see an output similar toohello following.</span></span>

    ![liste ps][ps-list]

3. <span data-ttu-id="f9b9b-188">Connexion tooAzure et toowhich d’abonnement hello sélectionnez vous voulez toocreate hello cluster</span><span class="sxs-lookup"><span data-stu-id="f9b9b-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="f9b9b-189">Exécution hello suivant toonow de la commande Créer un cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="f9b9b-190">N’oubliez pas de paramètres de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="f9b9b-191">commande Hello peut prendre de 10 minutes too30 minutes toocomplete, à fin hello de celle-ci, vous devez obtenir un suivante toohello similaire de sortie.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="f9b9b-192">sortie de Hello a plus d’informations sur le certificat hello, hello KeyVault où il a été téléchargé, et hello dossier local où le certificat de hello est copié.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![Résultat PS][ps-out]

5. <span data-ttu-id="f9b9b-194">Copier l’intégralité de la sortie hello tooa fichier texte et enregistrez-le comme nous devons toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="f9b9b-195">Prenez note de hello informations suivantes à partir de la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="f9b9b-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="f9b9b-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="f9b9b-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="f9b9b-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="f9b9b-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="f9b9b-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="f9b9b-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="f9b9b-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="f9b9b-200">Installer le certificat de hello sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="f9b9b-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="f9b9b-201">tooconnect toohello cluster, vous avez besoin tooinstall hello certificat dans le magasin personnel (My) de hello de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="f9b9b-202">Exécutez hello suivant PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9b9b-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="f9b9b-203">Vous êtes maintenant cluster sécurisée de tooyour tooconnect prêt.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="f9b9b-204">Connecter le cluster sécurisée de tooa</span><span class="sxs-lookup"><span data-stu-id="f9b9b-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="f9b9b-205">Exécutez hello suivant cluster sécurisée du tooa tooconnect commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="f9b9b-206">Détails du certificat Hello doivent correspondre à un certificat qui a été utilisé tooset cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="f9b9b-207">Hello suivant l’exemple affiche hello des paramètres completed :</span><span class="sxs-lookup"><span data-stu-id="f9b9b-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="f9b9b-208">Exécutez hello suivant toocheck de commande que vous êtes connecté et le cluster de hello est sain.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="f9b9b-209">Publier votre cluster de tooyour des applications à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f9b9b-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="f9b9b-210">Maintenant que vous avez configuré un cluster Azure, vous pouvez publier votre tooit d’applications à partir de Visual Studio en suivant hello [publier tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="f9b9b-211">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="f9b9b-211">Remove hello cluster</span></span>
<span data-ttu-id="f9b9b-212">Un cluster est composé d’autres ressources Windows Azure en outre toohello du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="f9b9b-213">cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="f9b9b-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="f9b9b-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9b9b-214">Next steps</span></span>
<span data-ttu-id="f9b9b-215">Maintenant que vous avez configuré un cluster de développement, essayez suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="f9b9b-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="f9b9b-216">Créer un cluster sécurisé dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="f9b9b-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="f9b9b-217">Créer un cluster à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="f9b9b-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="f9b9b-218">Déployer des applications à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9b9b-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
