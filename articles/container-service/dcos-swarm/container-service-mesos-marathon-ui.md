---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaManage avec une interface utilisateur Marathon | Documents Microsoft"
description: "Déployer le service de cluster du Service de conteneur Azure conteneurs tooan à l’aide de l’interface utilisateur web de Marathon hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Gérer un cluster Azure conteneur Service contrôleur de domaine/système d’exploitation via l’interface utilisateur web de Marathon hello
Contrôleur de domaine/système d’exploitation fournit un environnement de déploiement et de mise à l’échelle de charges de travail en cluster, tout en faisant abstraction du matériel sous-jacent de hello. DC/OS sous-tend un framework qui gère la planification et l’exécution des charges de travail de calcul.

Alors que les infrastructures sont disponibles pour nombreuses charges de travail courantes, ce document décrit comment tooget démarrer le déploiement de conteneurs avec Marathon. 


## <a name="prerequisites"></a>Composants requis
Avant d’étudier ces exemples, vous devez avoir un cluster DC/OS configuré dans Azure Container Service. Vous devez également le cluster de toothis toohave la connectivité à distance. Pour plus d’informations sur ces éléments, consultez hello suivant des articles :

* [Déploiement d’un cluster Azure Container Service](container-service-deployment.md)
* [Connecter le cluster du Service de conteneur Azure tooan](../container-service-connect.md)

> [!NOTE]
> Cet article suppose que vous créez un tunnel cluster du contrôleur de domaine/système d’exploitation toohello via les ports locaux 80.
>

## <a name="explore-hello-dcos-ui"></a>Explorer hello l’interface utilisateur du contrôleur de domaine/système d’exploitation
Avec un tunnel SSH (Secure Shell) [établie](../container-service-connect.md), parcourir toohttp://localhost/. Cela charge l’interface utilisateur web de contrôleur de domaine/système d’exploitation hello et affiche des informations sur le cluster hello, telles que les ressources utilisées, les agents actifs et les services en cours d’exécution.

![IU DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Explorer hello Marathon UI
toosee hello Marathon UI, accédez à toohttp://localhost/marathon. À partir de cet écran, vous pouvez démarrer un nouveau conteneur ou une autre application sur le cluster du Service de conteneur Azure DC/OS hello. Vous pouvez également voir des informations sur les conteneurs et les applications en cours d’exécution.  

![IU Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Déployer un conteneur au format Docker
toodeploy un nouveau conteneur à l’aide de Marathon, cliquez sur **créer une Application**, puis entrez hello informations suivantes dans les onglets de formulaire hello :

| Champ | Valeur |
| --- | --- |
| ID |nginx |
| Mémoire | 32 |
| Image |nginx |
| Réseau |Relié par un pont |
| Port de l’hôte |80 |
| Protocole |TCP |

![Nouvelle interface utilisateur d’application : général](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nouvelle interface utilisateur d’application : conteneur Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nouvelle interface utilisateur d’application : détection de service et de ports](./media/container-service-mesos-marathon-ui/dcos6.png)

Si vous souhaitez toostatically mappe hello port du conteneur tooa le port sur l’agent de hello, vous devez toouse en Mode de JSON. toodo basculer, Assistant de nouvelle Application hello trop**JSON Mode** à l’aide de bascule de hello. Puis entrez hello suivant paramètre sous hello `portMappings` section hello de définition d’application. Cet exemple lie le port 80 de hello conteneur tooport 80 de l’agent du contrôleur de domaine/système d’exploitation hello. Vous pouvez basculer l’Assistant hors du mode JSON après avoir apporté cette modification.

```none
"hostPort": 80,
```

![Nouvelle interface utilisateur d’application : exemple de port 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Si vous souhaitez que les contrôles d’intégrité de tooenable, définir un chemin d’accès sur hello **contrôles d’intégrité** onglet.

![Interface utilisateur de nouvelle application -- contrôles d’intégrité](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

cluster de contrôleur de domaine/système d’exploitation Hello est déployé avec un ensemble d’agents privés et publics. Pour hello cluster toobe tooaccess en mesure d’applications des hello Internet, vous avez besoin d’un agent public de toodeploy hello applications tooa. toodo, sélectionnez hello **facultatif** onglet de l’Assistant de nouvelle Application hello et entrez **slave_public** pour hello **accepté les rôles de ressources**.

Cliquez ensuite sur **Créer une application**.

![Nouvelle interface utilisateur d’application : paramètre de l’agent public](./media/container-service-mesos-marathon-ui/dcos14.png)

Sur la page principale de Marathon hello, vous pouvez voir l’état du déploiement hello pour le conteneur de hello. Initialement, vous voyez l’état **Déploiement**. Après un déploiement réussi, hello les changements d’état trop**en cours d’exécution**.

![Interface utilisateur de la page principale de Marathon : état du déploiement du conteneur](./media/container-service-mesos-marathon-ui/dcos7.png)

Lorsque vous basculez web de contrôleur de domaine/système d’exploitation précédent toohello UI (http://localhost/), vous consultez qu’une tâche (dans ce cas, un conteneur au format Docker) s’exécute sur le cluster de contrôleur de domaine/système d’exploitation hello.

![Contrôleur de domaine/système d’exploitation l’interface utilisateur web--tâche en cours d’exécution sur le cluster de hello](./media/container-service-mesos-marathon-ui/dcos8.png)

nœud de cluster toosee hello hello tâche est en cours d’exécution, cliquez sur hello **nœuds** onglet.

![IU web DC/OS : nœud du cluster de tâche](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Atteindre le conteneur de hello

Dans cet exemple, application hello est en cours d’exécution sur un nœud de l’agent public. Vous atteignez application hello hello internet en parcourant toohello agent nom de domaine complet du cluster de hello : `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, où :

* **DNSPREFIX** est le préfixe du DNS hello que vous avez fourni lors du déploiement de cluster de hello.
* **RÉGION** est la région de hello dans lequel se trouve votre groupe de ressources.

    ![Nginx à partir d’Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Étapes suivantes
* [Travailler avec le contrôleur de domaine/système d’exploitation et hello Marathon API](container-service-mesos-marathon-rest.md)

* Présentation approfondie sur hello Service de conteneur Azure avec Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
