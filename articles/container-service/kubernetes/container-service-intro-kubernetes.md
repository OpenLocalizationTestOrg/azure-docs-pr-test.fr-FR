---
title: aaaIntroduction tooAzure Service de conteneur pour Kubernetes | Documents Microsoft
description: "Service de conteneur Azure pour Kubernetes toodeploy simple et de gérer les applications basées sur le conteneur sur Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, docker, conteneurs, microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Introduction tooAzure Service de conteneur pour Kubernetes
Service de conteneur Azure pour Kubernetes rend toocreate simple, configurer et gérer un cluster d’ordinateurs virtuels qui sont des applications préconfigurés toorun placées dans des conteneurs. Ainsi vous toouse vos compétences existantes, ou appuyer sur un corps important et croissant d’expertise de la Communauté, toodeploy et gérer les applications de conteneur basé sur Microsoft Azure.

En utilisant le Service de conteneur Azure, vous pouvez tirer parti des hello entreprise fonctionnalités d’Azure, tout en conservant la portabilité des applications via Kubernetes et hello format d’image Docker.

## <a name="using-azure-container-service-for-kubernetes"></a>Utilisation d’Azure Container Service pour Kubernetes
L’objectif de Service de conteneur Azure est tooprovide un environnement d’hébergement de conteneur à l’aide d’outils open-source et les technologies adoptés par nos clients aujourd'hui. toothis fin, nous présentons les points de terminaison Kubernetes API standard hello. À l’aide de ces points de terminaison standard, vous pouvez exploiter tout logiciel qui est capable de communiquer avec tooa Kubernetes cluster. Par exemple, vous pourriez choisir [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), ou [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Création d’un cluster Kubernetes à l’aide d’Azure Container Service
toobegin à l’aide du Service de conteneur Azure, déployer un cluster de Service de conteneur Azure avec hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) ou via le portail de hello (hello de recherche Marketplace pour **Service de conteneur Azure**). Si vous êtes un utilisateur expérimenté ayant besoin de davantage de contrôle sur les modèles Azure Resource Manager hello, vous pouvez utiliser d’ouvrir la source de hello [acs-moteur](https://github.com/Azure/acs-engine) projet toobuild vos propres Kubernetes personnalisées de cluster et le déployer via hello `az` CLI.

### <a name="using-kubernetes"></a>Utilisation de Kubernetes
Kubernetes automatise le déploiement, la mise à l’échelle et la gestion des applications en conteneur. Il possède un jeu complet de fonctionnalités, notamment :
* Binpacking automatique
* Réparation spontanée
* Mise à l’échelle horizontale
* Détection de service et équilibrage de charge
* Déploiements et restaurations automatisés
* Secret et gestion de la configuration
* Orchestration de stockage
* Exécution Batch

Diagramme architectural de Kubernetes déployé via Azure Container Service :

![Service de conteneur Azure configuré toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Vidéos

Prise en charge de Kubernetes dans Azure Container Service (Azure Friday janvier 2017) :

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Outils dédiés au développement et au déploiement d’applications sur Kubernetes (Azure OpenDev juin 2017) :

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Étapes suivantes

Explorer hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin Explorer le Service de conteneur Azure aujourd'hui.
