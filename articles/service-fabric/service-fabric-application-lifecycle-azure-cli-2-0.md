---
title: "Gérer les applications Azure Service Fabric à l’aide d’Azure CLI 2.0"
description: "Découvrez comment déployer et supprimer des applications à partir d’un cluster Azure Service Fabric à l’aide d’Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="68f6a-103">Gérer une application Azure Service Fabric à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68f6a-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="68f6a-104">Découvrez comment créer et supprimer des applications qui s’exécutent dans un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68f6a-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68f6a-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="68f6a-105">Prerequisites</span></span>

* <span data-ttu-id="68f6a-106">Installez Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="68f6a-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="68f6a-107">Sélectionnez ensuite votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68f6a-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="68f6a-108">Pour plus d’informations, consultez [Bien démarrer avec Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="68f6a-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="68f6a-109">Vous devez également avoir un package d’application Service Fabric prêt à être déployé.</span><span class="sxs-lookup"><span data-stu-id="68f6a-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="68f6a-110">Pour plus d’informations sur la création et l’empaquetage d’une application, consultez la documentation dédiée au [modèle d’application Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="68f6a-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="68f6a-111">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="68f6a-111">Overview</span></span>

<span data-ttu-id="68f6a-112">Pour déployer une nouvelle application, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="68f6a-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="68f6a-113">Téléchargez un package d’application dans le magasin d’images Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68f6a-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="68f6a-114">Approvisionnez un type d’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-114">Provision an application type.</span></span>
3. <span data-ttu-id="68f6a-115">Spécifiez et créez une application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-115">Specify and create an application.</span></span>
4. <span data-ttu-id="68f6a-116">Spécifiez et créez des services.</span><span class="sxs-lookup"><span data-stu-id="68f6a-116">Specify and create services.</span></span>

<span data-ttu-id="68f6a-117">Pour supprimer une application existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68f6a-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="68f6a-118">Supprimez l’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-118">Delete the application.</span></span>
2. <span data-ttu-id="68f6a-119">Annulez l’approvisionnement du type d’application associé.</span><span class="sxs-lookup"><span data-stu-id="68f6a-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="68f6a-120">Supprimez le contenu du magasin d’images.</span><span class="sxs-lookup"><span data-stu-id="68f6a-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="68f6a-121">Déployer une nouvelle application</span><span class="sxs-lookup"><span data-stu-id="68f6a-121">Deploy a new application</span></span>

<span data-ttu-id="68f6a-122">Pour déployer une nouvelle application, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="68f6a-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="68f6a-123">Charger un nouveau package d’application dans le magasin d’images</span><span class="sxs-lookup"><span data-stu-id="68f6a-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="68f6a-124">Avant de créer une application, vous devez charger le package d’application dans le magasin d’images Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68f6a-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="68f6a-125">Par exemple, si votre package d’application se trouve dans le répertoire `app_package_dir`, utilisez les commandes suivantes pour charger le répertoire :</span><span class="sxs-lookup"><span data-stu-id="68f6a-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="68f6a-126">Pour les packages d’application volumineux, vous pouvez spécifier l’option `--show-progress` pour afficher la progression du chargement.</span><span class="sxs-lookup"><span data-stu-id="68f6a-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="68f6a-127">Approvisionner le type d’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-127">Provision the application type</span></span>

<span data-ttu-id="68f6a-128">Lorsque le chargement est terminé, approvisionnez l’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="68f6a-129">Pour approvisionner l’application, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68f6a-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="68f6a-130">La valeur de `application-type-build-path` est le nom du répertoire où vous avez chargé le package d’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="68f6a-131">Créer une application à partir d’un type d’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-131">Create an application from an application type</span></span>

<span data-ttu-id="68f6a-132">Une fois que vous avez approvisionné l’application, utilisez la commande suivante pour nommer et créer votre application :</span><span class="sxs-lookup"><span data-stu-id="68f6a-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="68f6a-133">`app-name` est le nom que vous souhaitez utiliser pour l’instance de l’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="68f6a-134">Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà approvisionné.</span><span class="sxs-lookup"><span data-stu-id="68f6a-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="68f6a-135">Le nom de l’application doit commencer par le préfixe `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="68f6a-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="68f6a-136">Créer des services pour la nouvelle application</span><span class="sxs-lookup"><span data-stu-id="68f6a-136">Create services for the new application</span></span>

<span data-ttu-id="68f6a-137">Après avoir créé une application, créez des services à partir de l’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="68f6a-138">Dans l’exemple suivant, nous créons un service sans état à partir de notre application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="68f6a-139">Les services que vous pouvez créer à partir d’une application sont définis dans un manifeste de service placé dans le package d’application déjà approvisionné.</span><span class="sxs-lookup"><span data-stu-id="68f6a-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="68f6a-140">Vérifier le déploiement et l’intégrité de l’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-140">Verify application deployment and health</span></span>

<span data-ttu-id="68f6a-141">Pour vous assurer qu’une application et un service ont été déployés, vérifiez que l’application et le service sont répertoriés :</span><span class="sxs-lookup"><span data-stu-id="68f6a-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="68f6a-142">Pour vérifier l’intégrité du service, utilisez des commandes similaires afin de récupérer des informations sur l’intégrité du service et de l’application :</span><span class="sxs-lookup"><span data-stu-id="68f6a-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="68f6a-143">Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.</span><span class="sxs-lookup"><span data-stu-id="68f6a-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="68f6a-144">Supprimer une application existante</span><span class="sxs-lookup"><span data-stu-id="68f6a-144">Remove an existing application</span></span>

<span data-ttu-id="68f6a-145">Pour supprimer une application, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="68f6a-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="68f6a-146">Supprimer l’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-146">Delete the application</span></span>

<span data-ttu-id="68f6a-147">Pour supprimer l’application, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68f6a-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="68f6a-148">Annuler l’approvisionnement de l’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-148">Unprovision the application type</span></span>

<span data-ttu-id="68f6a-149">Après avoir supprimé l’application, vous pouvez annuler l’approvisionnement du type d’application s’il n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="68f6a-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="68f6a-150">Pour annuler l’approvisionnement du type d’application, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68f6a-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="68f6a-151">Le nom et la version du type doivent correspondre au nom et à la version du manifeste de l’application précédemment approvisionné.</span><span class="sxs-lookup"><span data-stu-id="68f6a-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="68f6a-152">Supprimer le package d’application</span><span class="sxs-lookup"><span data-stu-id="68f6a-152">Delete the application package</span></span>

<span data-ttu-id="68f6a-153">Une fois l’approvisionnement du type d’application annulé, vous pouvez supprimer le package d’application du magasin d’images si vous n’en avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="68f6a-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="68f6a-154">La suppression des packages d’application permet de récupérer de l’espace sur le disque.</span><span class="sxs-lookup"><span data-stu-id="68f6a-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="68f6a-155">Pour supprimer le package d’application du magasin d’images, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68f6a-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="68f6a-156">`content-path` doit être le nom du répertoire que vous avez chargé lors de la création de l’application.</span><span class="sxs-lookup"><span data-stu-id="68f6a-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="68f6a-157">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="68f6a-157">Related articles</span></span>

* [<span data-ttu-id="68f6a-158">Prise en main de Service Fabric et d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68f6a-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="68f6a-159">Prise en main de l’interface de ligne de commande Service Fabric XPlat</span><span class="sxs-lookup"><span data-stu-id="68f6a-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
