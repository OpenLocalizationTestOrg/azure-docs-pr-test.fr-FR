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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Gérer une application Azure Service Fabric à l’aide d’Azure CLI 2.0

Découvrez comment créer et supprimer des applications qui s’exécutent dans un cluster Azure Service Fabric.

## <a name="prerequisites"></a>Composants requis

* Installez Azure CLI 2.0. Sélectionnez ensuite votre cluster Service Fabric. Pour plus d’informations, consultez [Bien démarrer avec Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* Vous devez également avoir un package d’application Service Fabric prêt à être déployé. Pour plus d’informations sur la création et l’empaquetage d’une application, consultez la documentation dédiée au [modèle d’application Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Vue d'ensemble

Pour déployer une nouvelle application, suivez les étapes ci-dessous :

1. Téléchargez un package d’application dans le magasin d’images Service Fabric.
2. Approvisionnez un type d’application.
3. Spécifiez et créez une application.
4. Spécifiez et créez des services.

Pour supprimer une application existante, procédez comme suit :

1. Supprimez l’application.
2. Annulez l’approvisionnement du type d’application associé.
3. Supprimez le contenu du magasin d’images.

## <a name="deploy-a-new-application"></a>Déployer une nouvelle application

Pour déployer une nouvelle application, suivez les étapes ci-dessous.

### <a name="upload-a-new-application-package-to-the-image-store"></a>Charger un nouveau package d’application dans le magasin d’images

Avant de créer une application, vous devez charger le package d’application dans le magasin d’images Service Fabric. 

Par exemple, si votre package d’application se trouve dans le répertoire `app_package_dir`, utilisez les commandes suivantes pour charger le répertoire :

```azurecli
az sf application upload --path ~/app_package_dir
```

Pour les packages d’application volumineux, vous pouvez spécifier l’option `--show-progress` pour afficher la progression du chargement.

### <a name="provision-the-application-type"></a>Approvisionner le type d’application

Lorsque le chargement est terminé, approvisionnez l’application. Pour approvisionner l’application, utilisez la commande suivante :

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

La valeur de `application-type-build-path` est le nom du répertoire où vous avez chargé le package d’application.

### <a name="create-an-application-from-an-application-type"></a>Créer une application à partir d’un type d’application

Une fois que vous avez approvisionné l’application, utilisez la commande suivante pour nommer et créer votre application :

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name` est le nom que vous souhaitez utiliser pour l’instance de l’application. Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà approvisionné.

Le nom de l’application doit commencer par le préfixe `fabric:/`.

### <a name="create-services-for-the-new-application"></a>Créer des services pour la nouvelle application

Après avoir créé une application, créez des services à partir de l’application. Dans l’exemple suivant, nous créons un service sans état à partir de notre application. Les services que vous pouvez créer à partir d’une application sont définis dans un manifeste de service placé dans le package d’application déjà approvisionné.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Vérifier le déploiement et l’intégrité de l’application

Pour vous assurer qu’une application et un service ont été déployés, vérifiez que l’application et le service sont répertoriés :

```azurecli
az sf application list
az sf service list --application-list TestApp
```

Pour vérifier l’intégrité du service, utilisez des commandes similaires afin de récupérer des informations sur l’intégrité du service et de l’application :

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.

## <a name="remove-an-existing-application"></a>Supprimer une application existante

Pour supprimer une application, suivez les étapes ci-dessous.

### <a name="delete-the-application"></a>Supprimer l’application

Pour supprimer l’application, utilisez la commande suivante :

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a>Annuler l’approvisionnement de l’application

Après avoir supprimé l’application, vous pouvez annuler l’approvisionnement du type d’application s’il n’est plus nécessaire. Pour annuler l’approvisionnement du type d’application, utilisez la commande suivante :

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Le nom et la version du type doivent correspondre au nom et à la version du manifeste de l’application précédemment approvisionné.

### <a name="delete-the-application-package"></a>Supprimer le package d’application

Une fois l’approvisionnement du type d’application annulé, vous pouvez supprimer le package d’application du magasin d’images si vous n’en avez plus besoin. La suppression des packages d’application permet de récupérer de l’espace sur le disque. 

Pour supprimer le package d’application du magasin d’images, utilisez la commande suivante :

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path` doit être le nom du répertoire que vous avez chargé lors de la création de l’application.

## <a name="related-articles"></a>Articles connexes

* [Prise en main de Service Fabric et d’Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Prise en main de l’interface de ligne de commande Service Fabric XPlat](service-fabric-azure-cli.md)
