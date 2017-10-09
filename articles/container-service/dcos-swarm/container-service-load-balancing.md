---
title: "conteneurs de solde aaaLoad dans un cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: "Équilibrer la charge de plusieurs conteneurs dans un cluster DC/OS Azure Container Service."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Équilibrer la charge des conteneurs dans un cluster DC/OS Azure Container Service
Dans cet article, nous explorons comment toocreate un équilibreur de charge interne dans un contrôleur de domaine/système d’exploitation géré Azure Service de conteneur à l’aide de Marathon kg. Cette configuration permet de vous tooscale vos applications horizontalement. Il vous permet également parti tootake de clusters public et privé de l’agent de hello en plaçant les équilibreurs de charge sur les clusters public hello et vos conteneurs d’applications sur les clusters privé hello. Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Configurer un équilibreur de charge Marathon
> * Déployer une application à l’aide d’équilibrage de charge hello
> * Configurer un équilibreur de charge Azure

Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel. Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Vue d’ensemble de l’équilibrage de charge

Il existe deux couches d’équilibrage de charge dans un cluster DC/OS Azure Container Service : 

**Équilibrage de charge Azure** fournit des points d’entrée publics (hello celles que les utilisateurs finaux d’accès). Un équilibrage de charge Azure est fourni automatiquement par le Service de conteneur Azure et est, par défaut, le port configuré tooexpose 80, 443 et 8080.

**Hello Marathon équilibrage de charge (marathon kg)** itinéraires entrant instances toocontainer demandes ces demandes de service. Comme nous l’échelle conteneurs hello fournissant notre service web, hello marathon kg s’adapte dynamiquement. Cet équilibrage de charge n’est pas fourni par défaut dans votre Service de conteneur, mais il est facile tooinstall.

## <a name="configure-marathon-load-balancer"></a>Configurer un équilibreur de charge Marathon

Équilibrage de charge marathon reconfigure dynamiquement elle-même en se basant sur les conteneurs hello que vous avez déployés. Il est également perte résilient toohello d’un conteneur ou un agent - si cela se produit, Apache Mesos redémarre conteneur hello ailleurs et marathon kg adapte.

Exécutez hello suivant d’équilibrage de charge de commande tooinstall hello marathon sur le cluster de l’agent hello publique.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Déployer une application à charge équilibrée

Maintenant que nous avons package kg marathon de hello, nous pouvons déployer un conteneur d’application que nous souhaitons solde de tooload. 

Tout d’abord, obtenez hello nom de domaine complet d’agents de hello exposée publiquement.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Ensuite, créez un fichier nommé *hello-web.json* et copie Bonjour suivant le contenu. Hello `HAPROXY_0_VHOST` étiquette doit toobe mis à jour avec hello nom de domaine complet d’agents de contrôleur de domaine/système d’exploitation hello. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Utilisez application de hello toorun hello CLI de contrôleur de domaine/système d’exploitation. Par défaut Marathon déploie hello hello application toohello privé de clusters. Cela signifie que hello au-dessus de déploiement est uniquement accessible via votre équilibreur de charge, qui est généralement le comportement de hello souhaité.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Une fois que l’application hello a été déployée, parcourir toohello FQDN de l’application à charge équilibrée de hello agent cluster tooview.

![Image de l’application à charge équilibrée](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Configurer Azure Load Balancer

Par défaut, Azure Load Balancer expose les ports 80, 8080 et 443. Si vous utilisez une de ces trois ports (comme nous le faisons Bonjour à l’exemple ci-dessus), alors il n’avez rien toodo. Vous devez être en mesure de toohit nom de domaine complet de l’équilibrage de charge de votre agent, et chaque fois que vous actualisez, vous devez appuyer sur un de vos serveurs trois web dans un tourniquet. 

Si vous utilisez un autre port, vous devez tooadd un tourniquet règle et une sonde d’équilibrage de charge hello pour le port hello que vous avez utilisé. Vous pouvez les spécifier cela via hello [CLI d’Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), avec les commandes hello `azure network lb rule create` et `azure network lb probe create`.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris dans ACS avec hello Marathon et charge Azure équilibrages notamment hello suit les actions d’équilibrage de charge :

> [!div class="checklist"]
> * Configurer un équilibreur de charge Marathon
> * Déployer une application à l’aide d’équilibrage de charge hello
> * Configurer un équilibreur de charge Azure

Avance toohello toolearn de didacticiel suivant sur l’intégration du stockage Azure avec contrôleur de domaine/système d’exploitation dans Azure.

> [!div class="nextstepaction"]
> [Monter un partage de fichiers Azure dans un cluster DC/OS](container-service-dcos-fileshare.md)