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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Gérer une application Azure Service Fabric à l’aide d’Azure CLI 2.0

Découvrez comment toocreate et supprimer des applications qui sont exécutent dans un cluster Azure Service Fabric.

## <a name="prerequisites"></a>Composants requis

* Installez Azure CLI 2.0. Sélectionnez ensuite votre cluster Service Fabric. Pour plus d’informations, consultez [Bien démarrer avec Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* Avoir un toobe prêt package application Service Fabric déployé. Pour plus d’informations sur la façon tooauthor et package d’une application, en savoir plus sur hello [modèle d’application Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Vue d'ensemble

toodeploy une nouvelle application, procédez comme suit :

1. Télécharger un magasin d’image application package toohello Service Fabric.
2. Approvisionnez un type d’application.
3. Spécifiez et créez une application.
4. Spécifiez et créez des services.

tooremove une application existante, procédez comme suit :

1. Supprimer l’application hello.
2. Hello de la mise hors service associées de type d’application.
3. Supprimer le magasin de contenu de l’image hello.

## <a name="deploy-a-new-application"></a>Déployer une nouvelle application

toodeploy une nouvelle application hello complète tâches suivantes.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Télécharger un nouveau magasin d’images toohello application package

Avant de créer une application, téléchargez le magasin d’images hello application package toohello Service Fabric. 

Par exemple, si votre package d’application est Bonjour `app_package_dir` active, hello utilisation suivant active de hello tooupload de commandes :

```azurecli
az sf application upload --path ~/app_package_dir
```

Pour les packages d’application volumineux, vous pouvez spécifier hello `--show-progress` option progression de hello toodisplay du téléchargement de hello.

### <a name="provision-hello-application-type"></a>Type d’application hello disposition

Téléchargement de hello terminée, configurer l’application hello. application de hello tooprovision, hello utilisez commande suivante :

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Hello valeur pour `application-type-build-path` est le nom hello du répertoire hello où vous avez téléchargé le package d’application.

### <a name="create-an-application-from-an-application-type"></a>Créer une application à partir d’un type d’application

Une fois que vous configurez application hello, utilisez hello suivant tooname de commande et créer votre application :

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`est le nom hello que vous souhaitez toouse pour l’instance de l’application hello. Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà mis en service hello.

nom de l’application Hello doit commencer par le préfixe de hello `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Créer des services pour la nouvelle application de hello

Après avoir créé une application, créer des services à partir de l’application hello. Bonjour l’exemple suivant, nous créer un service sans état à partir de notre application. les services de Hello que vous pouvez créer à partir d’une application sont définis dans un manifeste de service dans le package d’application déjà mis en service hello.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Vérifier le déploiement et l’intégrité de l’application

tooverify qu’une application et le service ont été déployés, vérifiez que le service et application hello sont répertoriés :

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify que le service de hello est intègre, utilisez similaire commandes tooretrieve hello intégrité à la fois hello service et application hello :

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.

## <a name="remove-an-existing-application"></a>Supprimer une application existante

tooremove une application hello complète tâches suivantes.

### <a name="delete-hello-application"></a>Supprimer l’application hello

application de hello toodelete, hello utilisez commande suivante :

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Annuler l’approvisionnement du type d’application hello

Après avoir supprimé application hello, vous pouvez annuler la configuration type d’application hello si elle n’est plus nécessaire. type d’application hello toounprovision, hello utilisez commande suivante :

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

version de nom et le type de type Hello doit correspondre au nom de hello et la version dans le manifeste de l’application déjà mis en service hello.

### <a name="delete-hello-application-package"></a>Supprimer le package d’application hello

Une fois que vous avez annulé la préparation type d’application hello, vous pouvez supprimer le package d’application hello à partir du magasin d’images hello si elle n’est plus nécessaire. La suppression des packages d’application permet de récupérer de l’espace sur le disque. 

package d’application hello toodelete à partir du magasin d’images hello, hello utilisez commande suivante :

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`doit être nom hello du répertoire hello que vous avez téléchargé lorsque vous avez créé l’application hello.

## <a name="related-articles"></a>Articles connexes

* [Prise en main de Service Fabric et d’Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Prise en main de l’interface de ligne de commande Service Fabric XPlat](service-fabric-azure-cli.md)
