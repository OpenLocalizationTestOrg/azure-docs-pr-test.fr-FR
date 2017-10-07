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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Gérer une application Azure Service Fabric à l’aide d’Azure Service Fabric CLI

Découvrez comment toocreate et supprimer des applications qui sont exécutent dans un cluster Azure Service Fabric.

## <a name="prerequisites"></a>Composants requis

* Installez Service Fabric CLI. Sélectionnez ensuite votre cluster Service Fabric. Pour plus d’informations, consultez [Prise en main de Service Fabric CLI](service-fabric-cli.md).

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

toodeploy une nouvelle application hello complète tâches suivantes :

### <a name="upload-a-new-application-package-toohello-image-store"></a>Télécharger un nouveau magasin d’images toohello application package

Avant de créer une application, téléchargez le magasin d’images hello application package toohello Service Fabric.

Par exemple, si votre package d’application est Bonjour `app_package_dir` active, hello utilisation suivant active de hello tooupload de commandes :

```azurecli
sfctl application upload --path ~/app_package_dir
```

Pour les packages d’application volumineux, vous pouvez spécifier hello `--show-progress` option progression de hello toodisplay du téléchargement de hello.

### <a name="provision-hello-application-type"></a>Type d’application hello disposition

Téléchargement de hello terminée, configurer l’application hello. application de hello tooprovision, hello utilisez commande suivante :

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

Hello valeur pour `application-type-build-path` est le nom hello du répertoire hello où vous avez téléchargé le package d’application.

### <a name="create-an-application-from-an-application-type"></a>Créer une application à partir d’un type d’application

Une fois que vous configurez application hello, utilisez hello suivant tooname de commande et créer votre application :

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`est le nom hello que vous souhaitez toouse pour l’instance de l’application hello. Vous pouvez obtenir des paramètres supplémentaires à partir du manifeste de l’application déjà approvisionné.

nom de l’application Hello doit commencer par le préfixe de hello `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Créer des services pour la nouvelle application de hello

Après avoir créé une application, créer des services à partir de l’application hello. Bonjour l’exemple suivant, nous créer un service sans état à partir de notre application. les services de Hello que vous pouvez créer à partir d’une application sont définis dans un manifeste de service dans le package d’application déjà mis en service hello.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Vérifier le déploiement et l’intégrité de l’application

tooverify tout est sain, utilisez hello suivant les commandes de contrôle d’intégrité :

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

tooverify que le service de hello est intègre, utilisez similaire intégrité hello tooretrieve de commandes du service de hello et l’application :

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

Les applications et services intègres ont une valeur `HealthState` égale à `Ok`.

## <a name="remove-an-existing-application"></a>Supprimer une application existante

tooremove une application hello complète tâches suivantes :

### <a name="delete-hello-application"></a>Supprimer l’application hello

application de hello toodelete, hello utilisez commande suivante :

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Annuler l’approvisionnement du type d’application hello

Après avoir supprimé application hello, vous pouvez annuler la configuration type d’application hello si elle n’est plus nécessaire. type d’application hello toounprovision, hello utilisez commande suivante :

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

version de nom et le type de type Hello doit correspondre au nom de hello et la version dans le manifeste de l’application déjà mis en service hello.

### <a name="delete-hello-application-package"></a>Supprimer le package d’application hello

Une fois que vous avez annulé la préparation type d’application hello, vous pouvez supprimer le package d’application hello à partir du magasin d’images hello si elle n’est plus nécessaire. La suppression des packages d’application permet de récupérer de l’espace sur le disque. 

package d’application hello toodelete à partir du magasin d’images hello, hello utilisez commande suivante :

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`doit être nom hello du répertoire hello que vous avez téléchargé lorsque vous avez créé l’application hello.

## <a name="upgrade-application"></a>Mettre à niveau l’application

Après avoir créé votre application, vous pouvez répéter hello même ensemble d’étapes tooprovision une deuxième version de votre application. Ensuite, avec une mise à niveau de Service Fabric application, vous pouvez passer toorunning hello deuxième version de l’application hello. Pour plus d’informations, consultez la documentation de hello sur [mises à niveau de Service Fabric application](service-fabric-application-upgrade.md).

tooperform une mise à niveau, la première disposition hello prochaine version d’à l’aide d’application hello hello mêmes commandes que précédemment :

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

Il est recommandé de puis tooperform une mise à niveau automatique analysé, lancer la mise à niveau hello en exécutant hello de commande suivante :

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

Les mises à niveau remplacent les paramètres existants par ce qui est spécifié. Paramètres de l’application doivent être passés en tant que commande de mise à niveau toohello arguments, si nécessaire. Les paramètres de l’application doivent être codés en tant qu’objet JSON.

tooretrieve tous les paramètres spécifiés précédemment, vous pouvez utiliser hello `sfctl application info` commande.

Lorsqu’une mise à niveau de l’application est en cours, état de hello peut être récupéré à l’aide de la `sfctl application upgrade-status` commande.

Enfin, si une mise à niveau est en cours et doit toobe annulée, vous pouvez utiliser hello `sfctl application upgrade-rollback` tooroll précédent hello mise à niveau.

## <a name="next-steps"></a>Étapes suivantes

* [Concepts de base Service Fabric CLI](service-fabric-cli.md)
* [Prise en main de Service Fabric sur Linux](service-fabric-get-started-linux.md)
* [Lancement d’une mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)
