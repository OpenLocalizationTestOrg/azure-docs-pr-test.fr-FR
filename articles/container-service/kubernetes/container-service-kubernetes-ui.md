---
title: "aaaManage Azure Kubernetes cluster associé à l’interface utilisateur web | Documents Microsoft"
description: "À l’aide de hello Kubernetes web l’interface utilisateur dans le conteneur de Service Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>À l’aide de hello Kubernetes web l’interface utilisateur avec le Service de conteneur Azure

## <a name="prerequisites"></a>Composants requis
Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).


Il suppose également que vous avez hello Azure CLI 2.0 et `kubectl` outils sont installés.

Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :

```console
$ az --version
```

Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).

Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :

```console
$ kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Vue d'ensemble

### <a name="connect-toohello-web-ui"></a>Se connecter à l’interface utilisateur web de toohello
Vous pouvez lancer l’interface utilisateur web de Kubernetes hello en exécutant :

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Il doit s’ouvrir un proxy de tooa sécurisée web navigateur configuré tootalk se connectant à votre interface utilisateur web de Kubernetes de toohello ordinateur local.

### <a name="create-and-expose-a-service"></a>Création et exposition d’un service
1. Dans hello Kubernetes interface utilisateur web, cliquez sur **créer** bouton hello supérieur droit de la fenêtre.

    ![Interface de création Kubernetes](./media/container-service-kubernetes-ui/create.png)

    Une boîte de dialogue dans laquelle vous pouvez commencer à créer votre application s’ouvre.

2. Nommez hello `hello-nginx`. Hello d’utilisation [ `nginx` conteneur à partir de Docker](https://hub.docker.com/_/nginx/) et déployer les trois réplicas de ce service web.

    ![Boîte de dialogue de création de pods Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. Sous **Service**, sélectionnez **Externe** et saisissez le port 80.

    Ce paramètre équilibre la charge de trois réplicas de trafic toohello.

    ![Boîte de dialogue de création de service Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Cliquez sur **déployer** toodeploy ces conteneurs et les services.

    ![Déploiement de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Affichage de vos conteneurs
Après avoir cliqué sur **déployer**, hello l’interface utilisateur affiche une vue de votre service lors de son déploiement :

![État de Kubernetes](./media/container-service-kubernetes-ui/status.png)

Vous pouvez voir sous état hello de chaque objet Kubernetes dans un cercle hello sur la partie gauche de l’interface utilisateur, hello **POD**. S’il s’agit d’un cercle complet partiellement, puis les objet hello consiste toujours à déployer. Lorsqu’un objet est entièrement déployé, une coche verte s’affiche :

![Kubernetes déployé](./media/container-service-kubernetes-ui/deployed.png)

Une fois que tout est en cours d’exécution, cliquez sur un de vos modules toosee plus d’informations sur hello en cours d’exécution service web.

![Pods kubernetes](./media/container-service-kubernetes-ui/pods.png)

Bonjour **POD** vue, vous pouvez voir des informations sur les conteneurs hello dans pod de hello, ainsi que des ressources processeur et mémoire hello utilisées par les conteneurs :

![Ressources Kubernetes](./media/container-service-kubernetes-ui/resources.png)

Si vous ne voyez pas les ressources hello, vous devrez peut-être toowait quelques minutes pour hello toopropagate des données d’analyse.

journaux de hello toosee pour votre conteneur, cliquez sur **afficher les journaux**.

![Journaux Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Affichage de votre service
Dans Ajout toorunning vos conteneurs, hello Kubernetes UI a créé par un externe `Service` qui configure une charge équilibrage toobring trafic toohello les conteneurs dans votre cluster.

Dans le volet de navigation gauche hello, cliquez sur **Services** tooview tous les services (il doit être uniquement).

![Services Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

Dans cet affichage, vous devez voir un point de terminaison externe (adresse IP) qui a été alloué tooyour service.
Si vous cliquez sur cette adresse IP, vous devez voir votre conteneur Nginx en cours d’exécution derrière l’équilibrage de charge.

![Vue nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Redimensionnement de votre service
En outre tooviewing vos objets dans hello l’interface utilisateur, vous pouvez modifier et mettre à jour les objets de l’API de Kubernetes hello.

Tout d’abord, cliquez sur **déploiements** Bonjour laissé le déploiement de navigation volet toosee hello pour votre service.

Une fois que vous êtes dans cette vue, cliquez sur le jeu de réplicas hello, puis cliquez sur **modifier** dans la barre de navigation supérieur hello :

![Modification de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Modifier hello `spec.replicas` champ toobe `2`, puis cliquez sur **mise à jour**.

Cela entraîne un nombre hello de réplicas toodrop tootwo par la suppression de l’un de vos modules.

 

