---
title: "applications Azure Service Fabric aaaManage à l’aide d’Azure CLI 2.0"
description: "Découvrez comment toodeploy et supprimez les applications à partir d’un Service Azure Fabric cluster à l’aide de Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="6526f-103">Gérer une application Azure Service Fabric à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6526f-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="6526f-104">Découvrez comment toocreate et supprimer des applications qui sont exécutent dans un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6526f-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6526f-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6526f-105">Prerequisites</span></span>

* <span data-ttu-id="6526f-106">Installez Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="6526f-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="6526f-107">Sélectionnez ensuite votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6526f-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="6526f-108">Pour plus d’informations, consultez [Bien démarrer avec Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="6526f-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="6526f-109">Avoir un toobe prêt package application Service Fabric déployé.</span><span class="sxs-lookup"><span data-stu-id="6526f-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="6526f-110">Pour plus d’informations sur la façon tooauthor et package d’une application, en savoir plus sur hello [modèle d’application Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="6526f-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="6526f-111">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6526f-111">Overview</span></span>

<span data-ttu-id="6526f-112">toodeploy une nouvelle application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6526f-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="6526f-113">Télécharger un magasin d’image application package toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6526f-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="6526f-114">Approvisionnez un type d’application.</span><span class="sxs-lookup"><span data-stu-id="6526f-114">Provision an application type.</span></span>
3. <span data-ttu-id="6526f-115">Spécifiez et créez une application.</span><span class="sxs-lookup"><span data-stu-id="6526f-115">Specify and create an application.</span></span>
4. <span data-ttu-id="6526f-116">Spécifiez et créez des services.</span><span class="sxs-lookup"><span data-stu-id="6526f-116">Specify and create services.</span></span>

<span data-ttu-id="6526f-117">tooremove une application existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6526f-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="6526f-118">Supprimer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-118">Delete hello application.</span></span>
2. <span data-ttu-id="6526f-119">Hello de la mise hors service associées de type d’application.</span><span class="sxs-lookup"><span data-stu-id="6526f-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="6526f-120">Supprimer le magasin de contenu de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="6526f-121">Déployer une nouvelle application</span><span class="sxs-lookup"><span data-stu-id="6526f-121">Deploy a new application</span></span>

<span data-ttu-id="6526f-122">toodeploy une nouvelle application hello complète tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="6526f-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="6526f-123">Télécharger un nouveau magasin d’images toohello application package</span><span class="sxs-lookup"><span data-stu-id="6526f-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="6526f-124">Avant de créer une application, téléchargez le magasin d’images hello application package toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6526f-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="6526f-125">Par exemple, si votre package d’application est Bonjour `app_package_dir` active, hello utilisation suivant active de hello tooupload de commandes :</span><span class="sxs-lookup"><span data-stu-id="6526f-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="6526f-126">Pour les packages d’application volumineux, vous pouvez spécifier hello `--show-progress` option progression de hello toodisplay du téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="6526f-127">Type d’application hello disposition</span><span class="sxs-lookup"><span data-stu-id="6526f-127">Provision hello application type</span></span>

<span data-ttu-id="6526f-128">Téléchargement de hello terminée, configurer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="6526f-129">application de hello tooprovision, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6526f-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="6526f-130">Hello valeur pour `application-type-build-path` est le nom hello du répertoire hello où vous avez téléchargé le package d’application.</span><span class="sxs-lookup"><span data-stu-id="6526f-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="6526f-131">Créer une application à partir d’un type d’application</span><span class="sxs-lookup"><span data-stu-id="6526f-131">Create an application from an application type</span></span>

<span data-ttu-id="6526f-132">Une fois que vous configurez application hello, utilisez hello suivant tooname de commande et créer votre application :</span><span class="sxs-lookup"><span data-stu-id="6526f-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="6526f-133">`app-name`est le nom hello que vous souhaitez toouse pour l’instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="6526f-134">Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà mis en service hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="6526f-135">nom de l’application Hello doit commencer par le préfixe de hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="6526f-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="6526f-136">Créer des services pour la nouvelle application de hello</span><span class="sxs-lookup"><span data-stu-id="6526f-136">Create services for hello new application</span></span>

<span data-ttu-id="6526f-137">Après avoir créé une application, créer des services à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="6526f-138">Bonjour l’exemple suivant, nous créer un service sans état à partir de notre application.</span><span class="sxs-lookup"><span data-stu-id="6526f-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="6526f-139">les services de Hello que vous pouvez créer à partir d’une application sont définis dans un manifeste de service dans le package d’application déjà mis en service hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="6526f-140">Vérifier le déploiement et l’intégrité de l’application</span><span class="sxs-lookup"><span data-stu-id="6526f-140">Verify application deployment and health</span></span>

<span data-ttu-id="6526f-141">tooverify qu’une application et le service ont été déployés, vérifiez que le service et application hello sont répertoriés :</span><span class="sxs-lookup"><span data-stu-id="6526f-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="6526f-142">tooverify que le service de hello est intègre, utilisez similaire commandes tooretrieve hello intégrité à la fois hello service et application hello :</span><span class="sxs-lookup"><span data-stu-id="6526f-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="6526f-143">Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.</span><span class="sxs-lookup"><span data-stu-id="6526f-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="6526f-144">Supprimer une application existante</span><span class="sxs-lookup"><span data-stu-id="6526f-144">Remove an existing application</span></span>

<span data-ttu-id="6526f-145">tooremove une application hello complète tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="6526f-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="6526f-146">Supprimer l’application hello</span><span class="sxs-lookup"><span data-stu-id="6526f-146">Delete hello application</span></span>

<span data-ttu-id="6526f-147">application de hello toodelete, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6526f-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="6526f-148">Annuler l’approvisionnement du type d’application hello</span><span class="sxs-lookup"><span data-stu-id="6526f-148">Unprovision hello application type</span></span>

<span data-ttu-id="6526f-149">Après avoir supprimé application hello, vous pouvez annuler la configuration type d’application hello si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6526f-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="6526f-150">type d’application hello toounprovision, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6526f-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="6526f-151">version de nom et le type de type Hello doit correspondre au nom de hello et la version dans le manifeste de l’application déjà mis en service hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="6526f-152">Supprimer le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="6526f-152">Delete hello application package</span></span>

<span data-ttu-id="6526f-153">Une fois que vous avez annulé la préparation type d’application hello, vous pouvez supprimer le package d’application hello à partir du magasin d’images hello si elle n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6526f-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="6526f-154">La suppression des packages d’application permet de récupérer de l’espace sur le disque.</span><span class="sxs-lookup"><span data-stu-id="6526f-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="6526f-155">package d’application hello toodelete à partir du magasin d’images hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6526f-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="6526f-156">`content-path`doit être nom hello du répertoire hello que vous avez téléchargé lorsque vous avez créé l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6526f-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6526f-157">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="6526f-157">Related articles</span></span>

* [<span data-ttu-id="6526f-158">Prise en main de Service Fabric et d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6526f-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="6526f-159">Prise en main de l’interface de ligne de commande Service Fabric XPlat</span><span class="sxs-lookup"><span data-stu-id="6526f-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
