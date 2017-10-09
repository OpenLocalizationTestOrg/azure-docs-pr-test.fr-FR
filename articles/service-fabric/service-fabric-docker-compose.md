---
title: aaaAzure Service Fabric Docker composer Preview
description: "Azure Service Fabric accepte toomake de format Docker Compose il plus faciles conteneurs existants tooorchestrate à l’aide de l’infrastructure de Service. Cette prise en charge est actuellement en mode préliminaire."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="e76d1-104">Prise en charge de l’application Docker Compose dans Azure Service Fabric (préversion)</span><span class="sxs-lookup"><span data-stu-id="e76d1-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="e76d1-105">Docker utilise hello [docker-compose.yml](https://docs.docker.com/compose) fichier permettant de définir le conteneur de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="e76d1-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="e76d1-106">toomake il facile pour les clients familiarisés avec les applications existantes conteneur Docker tooorchestrate sur Azure Service Fabric, nous avons inclus prise en charge de la version préliminaire de Docker Compose en mode natif dans hello plate-forme.</span><span class="sxs-lookup"><span data-stu-id="e76d1-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="e76d1-107">Service Fabric peut accepter des fichiers `docker-compose.yml` version 3 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e76d1-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="e76d1-108">Étant donné que cette prise en charge est disponible en préversion, seul un sous-ensemble des directives de Compose est reconnu.</span><span class="sxs-lookup"><span data-stu-id="e76d1-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="e76d1-109">Par exemple, les mises à niveau d’application ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="e76d1-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="e76d1-110">Toutefois, vous pouvez toujours supprimer et déployer des applications au lieu de les mettre à niveau.</span><span class="sxs-lookup"><span data-stu-id="e76d1-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="e76d1-111">toouse cela prévisualiser, créez votre cluster avec la version 5.7 ou version ultérieure du runtime de Service Fabric hello via le portail Azure, ainsi que de hello correspondant du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="e76d1-112">Cette fonctionnalité est disponible en préversion et n’est pas prise en charge dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="e76d1-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="e76d1-113">Déployer un fichier Docker Compose sur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e76d1-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="e76d1-114">Hello commandes suivantes créent une application Service Fabric (nommé `fabric:/TestContainerApp` Bonjour précédent exemple), que vous pouvez surveiller et gérer comme toute autre application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e76d1-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="e76d1-115">Vous pouvez utiliser le nom de l’application spécifiée hello pour les requêtes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="e76d1-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="e76d1-116">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="e76d1-116">Use PowerShell</span></span>

<span data-ttu-id="e76d1-117">Créez une application de composer de l’infrastructure de Service à partir d’un fichier compose.yml de docker en exécutant hello commande dans PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="e76d1-118">`RegistryUserName`et `RegistryPassword` font référence toohello conteneur Registre username et password.</span><span class="sxs-lookup"><span data-stu-id="e76d1-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="e76d1-119">Une fois que vous avez terminé d’application hello, vous pouvez vérifier son état à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="e76d1-120">toodelete hello application composition via PowerShell, utilisez les hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="e76d1-121">Utiliser l’interface CLI Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="e76d1-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="e76d1-122">Vous pouvez également utiliser hello Service Fabric CLI commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="e76d1-123">Une fois que vous avez créé l’application hello, vous pouvez vérifier son état à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="e76d1-124">toodelete hello application du nouveau message, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e76d1-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="e76d1-125">Directives Compose prises en charge</span><span class="sxs-lookup"><span data-stu-id="e76d1-125">Supported Compose directives</span></span>

<span data-ttu-id="e76d1-126">Cette version préliminaire prend en charge un sous-ensemble des options de configuration hello depuis le format de version 3 message hello, y compris hello suivant primitives :</span><span class="sxs-lookup"><span data-stu-id="e76d1-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="e76d1-127">Services > Déploiement > Réplicas</span><span class="sxs-lookup"><span data-stu-id="e76d1-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="e76d1-128">Services > Déploiement > Placement > Contraintes</span><span class="sxs-lookup"><span data-stu-id="e76d1-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="e76d1-129">Services > Déploiement > Ressources > Limites</span><span class="sxs-lookup"><span data-stu-id="e76d1-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="e76d1-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="e76d1-130">-cpu-shares</span></span>
    * <span data-ttu-id="e76d1-131">-memory</span><span class="sxs-lookup"><span data-stu-id="e76d1-131">-memory</span></span>
    * <span data-ttu-id="e76d1-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="e76d1-132">-memory-swap</span></span>
* <span data-ttu-id="e76d1-133">Services > Commandes</span><span class="sxs-lookup"><span data-stu-id="e76d1-133">Services > Commands</span></span>
* <span data-ttu-id="e76d1-134">Services > Environnement</span><span class="sxs-lookup"><span data-stu-id="e76d1-134">Services > Environment</span></span>
* <span data-ttu-id="e76d1-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="e76d1-135">Services > Ports</span></span>
* <span data-ttu-id="e76d1-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="e76d1-136">Services > Image</span></span>
* <span data-ttu-id="e76d1-137">Services > Isolation (uniquement pour Windows)</span><span class="sxs-lookup"><span data-stu-id="e76d1-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="e76d1-138">Services > Journalisation > Pilote</span><span class="sxs-lookup"><span data-stu-id="e76d1-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="e76d1-139">Services > Journalisation > Pilote > Options</span><span class="sxs-lookup"><span data-stu-id="e76d1-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="e76d1-140">Volume & déploiement > Volume</span><span class="sxs-lookup"><span data-stu-id="e76d1-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="e76d1-141">Configurez cluster hello pour mettre en œuvre des limites de ressources, comme décrit dans [gouvernance des ressources de Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e76d1-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="e76d1-142">Aucune des autres directives Docker Compose n’est prise en charge pour cette préversion.</span><span class="sxs-lookup"><span data-stu-id="e76d1-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="e76d1-143">Calcul de ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="e76d1-143">ServiceDnsName computation</span></span>

<span data-ttu-id="e76d1-144">Si le nom du service hello que vous spécifiez dans un fichier de message est un nom de domaine complet (autrement dit, elle contient un point [.]), le nom DNS hello enregistré par le Service Fabric est `<ServiceName>` (y compris le point de hello).</span><span class="sxs-lookup"><span data-stu-id="e76d1-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="e76d1-145">Si ce n’est pas le cas, chaque segment de chemin d’accès dans le nom de l’application hello devient un nom de domaine dans le nom DNS du service hello, avec le premier segment de chemin d’accès hello devient l’étiquette du domaine de premier niveau hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="e76d1-146">Par exemple, si hello spécifié le nom de l’application est `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` serait hello nom DNS enregistré.</span><span class="sxs-lookup"><span data-stu-id="e76d1-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="e76d1-147">Différences entre le Compose (définition d’instance) et le modèle d’application Service Fabric (définition de type)</span><span class="sxs-lookup"><span data-stu-id="e76d1-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="e76d1-148">Un fichier docker-compose.yml décrit un ensemble déployable de conteneurs, y compris leurs propriétés et leurs configurations.</span><span class="sxs-lookup"><span data-stu-id="e76d1-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="e76d1-149">Par exemple, fichier de hello peut contenir des variables d’environnement et les ports.</span><span class="sxs-lookup"><span data-stu-id="e76d1-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="e76d1-150">Vous pouvez également spécifier des paramètres de déploiement, tels que les contraintes de placement, les limites des ressources et les noms DNS dans le fichier de docker-compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="e76d1-151">Hello [modèle d’application Service Fabric](service-fabric-application-model.md) utilise des types de service et les types d’applications, où vous pouvez avoir plusieurs instances d’application du même type de hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="e76d1-152">Par exemple, vous pouvez avoir une seule instance d’application par client.</span><span class="sxs-lookup"><span data-stu-id="e76d1-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="e76d1-153">Ce modèle basé sur le type prend en charge plusieurs versions de hello même type d’application qui est inscrit avec le runtime de hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="e76d1-154">Par exemple, client A peut disposer d’une application instanciée avec type 1.0 de AppTypeA et client B peut disposer d’une autre application instanciée avec hello même type et la version.</span><span class="sxs-lookup"><span data-stu-id="e76d1-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="e76d1-155">Vous définissez des types d’application hello dans les manifestes d’application hello et que vous spécifiez les paramètres du nom et le déploiement d’application hello lorsque vous créez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="e76d1-156">Bien que ce modèle offre une grande souplesse, nous avons également l’intention toosupport un modèle de déploiement plus simple, basé sur une instance où les types sont implicites à partir du fichier de manifeste hello.</span><span class="sxs-lookup"><span data-stu-id="e76d1-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="e76d1-157">Dans ce modèle, chaque application obtient son propre manifeste indépendant.</span><span class="sxs-lookup"><span data-stu-id="e76d1-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="e76d1-158">Nous proposons cela en version préliminaire, en ajoutant la prise en charge du format docker-compose.yml, qui est un format de déploiement basé sur les instances.</span><span class="sxs-lookup"><span data-stu-id="e76d1-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e76d1-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e76d1-159">Next steps</span></span>

* <span data-ttu-id="e76d1-160">Sur hello [modèle d’application Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="e76d1-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="e76d1-161">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e76d1-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
