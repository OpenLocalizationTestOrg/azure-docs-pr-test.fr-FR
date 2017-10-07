---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - Datadog | Documents Microsoft"
description: Surveillez un cluster Azure Container Service avec Datadog. Utilisez hello DC/OS web UI toodeploy hello Datadog agents tooyour cluster.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Conteneurs, contrôleur de domaine/système d’exploitation, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Surveiller un cluster DC/OS Azure Container Service avec Datadog
Dans cet article, nous déploierez des nœuds d’agent Datadog agents tooall hello dans votre cluster de Service de conteneur Azure. Vous aurez besoin d’un compte Datadog pour cette configuration. 

## <a name="prerequisites"></a>Composants requis
[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster configuré par Azure Container Service. Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md). Accédez trop[http://datadoghq.com](http://datadoghq.com) tooset d’un compte Datadog. 

## <a name="datadog"></a>Datadog
Datadog est un service de surveillance qui regroupe les données de surveillance provenant de vos conteneurs dans votre cluster Azure Container Service. Datadog intègre un tableau de bord Docker Integration qui affiche des mesures spécifiques dans vos conteneurs. Les mesures recueillies à partir de vos conteneurs sont classées par processeur, mémoire, réseau et E/S. Datadog fractionne les mesures en conteneurs et images. Un exemple de quel hello l’interface utilisateur semble de l’UC, l’utilisation est inférieur.

![Interface utilisateur Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Configurer un déploiement Datadog avec Marathon
Ces étapes vous indiquent comment tooconfigure et de déploiement Datadog applications tooyour cluster avec Marathon. 

Accédez à l'interface utilisateur de votre contrôleur de domaine/système d’exploitation via [http://localhost:80/](http://localhost:80/). Une fois Bonjour accédez de l’interface utilisateur du contrôleur de domaine/système d’exploitation toohello « Univers », qui se trouve sur hello inférieur gauche et recherchez « Datadog » puis cliquez sur « Installer ».

![Package Datadog dans hello univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring/datadog1.png)

Maintenant toocomplete hello configuration avoir un compte Datadog ou un compte d’évaluation gratuit. Une fois que vous êtes connecté dans le site Web de Datadog toohello rechercher toohello gauche et accédez tooIntegrations -> puis [API](https://app.datadoghq.com/account/settings#api). 

![Clé d’API Datadog](./media/container-service-monitoring/datadog2.png)

Ensuite, entrez votre clé API à la configuration Datadog hello dans hello univers du contrôleur de domaine/système d’exploitation. 

![Configuration Datadog Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring/datadog3.png) 

Bonjour au-dessus de configuration instances sont définies too10000000 donc chaque fois qu’un nouveau nœud est ajouté le cluster toohello Datadog déploiera automatiquement un nœud toothat d’agent. Il s’agit d’une solution temporaire. Une fois que vous avez installé le package de hello vous devez naviguer dans site Web de Datadog toohello précédent et rechercher «[tableaux de bord](https://app.datadoghq.com/dash/list). » Vous y verrez des tableaux de bord personnalisés (Custom) et d'intégration (Integration). Hello [tableau de bord Docker](https://app.datadoghq.com/screen/integration/docker) auront toutes les métriques de conteneur hello vous avez besoin pour l’analyse de votre cluster. 

