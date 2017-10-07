---
title: "applications Azure Service Fabric aaaManage à l’aide d’Azure Service Fabric CLI"
description: "Découvrez comment toodeploy et supprimez les applications à partir d’un Service Azure Fabric cluster à l’aide de Azure Service Fabric CLI"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="5de93-103">Gérer une application Azure Service Fabric à l’aide d’Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="5de93-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="5de93-104">Découvrez comment toocreate et supprimer des applications qui sont exécutent dans un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5de93-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5de93-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5de93-105">Prerequisites</span></span>

* <span data-ttu-id="5de93-106">Installez Service Fabric CLI.</span><span class="sxs-lookup"><span data-stu-id="5de93-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="5de93-107">Sélectionnez ensuite votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5de93-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="5de93-108">Pour plus d’informations, consultez [Prise en main de Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5de93-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="5de93-109">Avoir un toobe prêt package application Service Fabric déployé.</span><span class="sxs-lookup"><span data-stu-id="5de93-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="5de93-110">Pour plus d’informations sur la façon tooauthor et package d’une application, en savoir plus sur hello [modèle d’application Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="5de93-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="5de93-111">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5de93-111">Overview</span></span>

<span data-ttu-id="5de93-112">toodeploy une nouvelle application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5de93-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="5de93-113">Télécharger un magasin d’image application package toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5de93-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="5de93-114">Approvisionnez un type d’application.</span><span class="sxs-lookup"><span data-stu-id="5de93-114">Provision an application type.</span></span>
3. <span data-ttu-id="5de93-115">Spécifiez et créez une application.</span><span class="sxs-lookup"><span data-stu-id="5de93-115">Specify and create an application.</span></span>
4. <span data-ttu-id="5de93-116">Spécifiez et créez des services.</span><span class="sxs-lookup"><span data-stu-id="5de93-116">Specify and create services.</span></span>

<span data-ttu-id="5de93-117">tooremove une application existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5de93-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="5de93-118">Supprimer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-118">Delete hello application.</span></span>
2. <span data-ttu-id="5de93-119">Hello de la mise hors service associées de type d’application.</span><span class="sxs-lookup"><span data-stu-id="5de93-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="5de93-120">Supprimer le magasin de contenu de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="5de93-121">Déployer une nouvelle application</span><span class="sxs-lookup"><span data-stu-id="5de93-121">Deploy a new application</span></span>

<span data-ttu-id="5de93-122">toodeploy une nouvelle application hello complète tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="5de93-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="5de93-123">Télécharger un nouveau magasin d’images toohello application package</span><span class="sxs-lookup"><span data-stu-id="5de93-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="5de93-124">Avant de créer une application, téléchargez le magasin d’images hello application package toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5de93-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="5de93-125">Par exemple, si votre package d’application est Bonjour `app_package_dir` active, hello utilisation suivant active de hello tooupload de commandes :</span><span class="sxs-lookup"><span data-stu-id="5de93-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="5de93-126">Pour les packages d’application volumineux, vous pouvez spécifier hello `--show-progress` option progression de hello toodisplay du téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="5de93-127">Type d’application hello disposition</span><span class="sxs-lookup"><span data-stu-id="5de93-127">Provision hello application type</span></span>

<span data-ttu-id="5de93-128">Téléchargement de hello terminée, configurer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="5de93-129">application de hello tooprovision, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de93-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="5de93-130">Hello valeur pour `application-type-build-path` est le nom hello du répertoire hello où vous avez téléchargé le package d’application.</span><span class="sxs-lookup"><span data-stu-id="5de93-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="5de93-131">Créer une application à partir d’un type d’application</span><span class="sxs-lookup"><span data-stu-id="5de93-131">Create an application from an application type</span></span>

<span data-ttu-id="5de93-132">Une fois que vous configurez application hello, utilisez hello suivant tooname de commande et créer votre application :</span><span class="sxs-lookup"><span data-stu-id="5de93-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="5de93-133">`app-name`est le nom hello que vous souhaitez toouse pour l’instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="5de93-134">Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà approvisionné.</span><span class="sxs-lookup"><span data-stu-id="5de93-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="5de93-135">nom de l’application Hello doit commencer par le préfixe de hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="5de93-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="5de93-136">Créer des services pour la nouvelle application de hello</span><span class="sxs-lookup"><span data-stu-id="5de93-136">Create services for hello new application</span></span>

<span data-ttu-id="5de93-137">Après avoir créé une application, créer des services à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="5de93-138">Bonjour l’exemple suivant, nous créer un service sans état à partir de notre application.</span><span class="sxs-lookup"><span data-stu-id="5de93-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="5de93-139">les services de Hello que vous pouvez créer à partir d’une application sont définis dans un manifeste de service dans le package d’application déjà mis en service hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="5de93-140">Vérifier le déploiement et l’intégrité de l’application</span><span class="sxs-lookup"><span data-stu-id="5de93-140">Verify application deployment and health</span></span>

<span data-ttu-id="5de93-141">tooverify tout est sain, utilisez hello suivant les commandes de contrôle d’intégrité :</span><span class="sxs-lookup"><span data-stu-id="5de93-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="5de93-142">tooverify que le service de hello est intègre, utilisez similaire intégrité hello tooretrieve de commandes du service de hello et l’application :</span><span class="sxs-lookup"><span data-stu-id="5de93-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="5de93-143">Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.</span><span class="sxs-lookup"><span data-stu-id="5de93-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="5de93-144">Supprimer une application existante</span><span class="sxs-lookup"><span data-stu-id="5de93-144">Remove an existing application</span></span>

<span data-ttu-id="5de93-145">tooremove une application hello complète tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="5de93-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="5de93-146">Supprimer l’application hello</span><span class="sxs-lookup"><span data-stu-id="5de93-146">Delete hello application</span></span>

<span data-ttu-id="5de93-147">application de hello toodelete, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de93-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="5de93-148">Annuler l’approvisionnement du type d’application hello</span><span class="sxs-lookup"><span data-stu-id="5de93-148">Unprovision hello application type</span></span>

<span data-ttu-id="5de93-149">Après avoir supprimé application hello, vous pouvez annuler la configuration type d’application hello si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5de93-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="5de93-150">type d’application hello toounprovision, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de93-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="5de93-151">version de nom et le type de type Hello doit correspondre au nom de hello et la version dans le manifeste de l’application déjà mis en service hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="5de93-152">Supprimer le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="5de93-152">Delete hello application package</span></span>

<span data-ttu-id="5de93-153">Une fois que vous avez annulé la préparation type d’application hello, vous pouvez supprimer le package d’application hello à partir du magasin d’images hello si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5de93-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="5de93-154">La suppression des packages d’application permet de récupérer de l’espace sur le disque.</span><span class="sxs-lookup"><span data-stu-id="5de93-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="5de93-155">package d’application hello toodelete à partir du magasin d’images hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de93-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="5de93-156">`content-path`doit être nom hello du répertoire hello que vous avez téléchargé lorsque vous avez créé l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="5de93-157">Mettre à niveau l’application</span><span class="sxs-lookup"><span data-stu-id="5de93-157">Upgrade application</span></span>

<span data-ttu-id="5de93-158">Après avoir créé votre application, vous pouvez répéter hello même ensemble d’étapes tooprovision une deuxième version de votre application.</span><span class="sxs-lookup"><span data-stu-id="5de93-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="5de93-159">Ensuite, avec une mise à niveau de Service Fabric application, vous pouvez passer toorunning hello deuxième version de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5de93-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="5de93-160">Pour plus d’informations, consultez la documentation de hello sur [mises à niveau de Service Fabric application](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="5de93-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="5de93-161">tooperform une mise à niveau, la première disposition hello prochaine version d’à l’aide d’application hello hello mêmes commandes que précédemment :</span><span class="sxs-lookup"><span data-stu-id="5de93-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="5de93-162">Il est recommandé de puis tooperform une mise à niveau automatique analysé, lancer la mise à niveau hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de93-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="5de93-163">Les mises à niveau remplacent les paramètres existants par ce qui est spécifié.</span><span class="sxs-lookup"><span data-stu-id="5de93-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="5de93-164">Paramètres de l’application doivent être passés en tant que commande de mise à niveau toohello arguments, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5de93-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="5de93-165">Les paramètres de l’application doivent être codés en tant qu’objet JSON.</span><span class="sxs-lookup"><span data-stu-id="5de93-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="5de93-166">tooretrieve tous les paramètres spécifiés précédemment, vous pouvez utiliser hello `sfctl application info` commande.</span><span class="sxs-lookup"><span data-stu-id="5de93-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="5de93-167">Lorsqu’une mise à niveau de l’application est en cours, état de hello peut être récupéré à l’aide de la `sfctl application upgrade-status` commande.</span><span class="sxs-lookup"><span data-stu-id="5de93-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="5de93-168">Enfin, si une mise à niveau est en cours et doit toobe annulée, vous pouvez utiliser hello `sfctl application upgrade-rollback` tooroll précédent hello mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="5de93-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5de93-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5de93-169">Next steps</span></span>

* [<span data-ttu-id="5de93-170">Concepts de base Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="5de93-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="5de93-171">Prise en main de Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="5de93-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="5de93-172">Lancement d’une mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5de93-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
