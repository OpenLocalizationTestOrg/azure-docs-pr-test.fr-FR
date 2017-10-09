---
title: aaaMonitor un Service de conteneur Azure cluster avec Sysdig | Documents Microsoft
description: Surveillez un cluster Azure Container Service avec Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Surveiller un cluster Azure Container Service avec Sysdig
Dans cet article, nous déploierez des nœuds d’agent Sysdig agents tooall hello dans votre cluster de Service de conteneur Azure. Vous avez besoin d’un compte Sysdig pour cette configuration. 

## <a name="prerequisites"></a>Composants requis
[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster configuré par Azure Container Service. Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md). Accédez trop[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset d’un compte de cloud Sysdig. 

## <a name="sysdig"></a>Sysdig
Sysdig est un service de surveillance qui vous permet de toomonitor vos conteneurs au sein de votre cluster. Sysdig est connu toohelp résolution des problèmes, mais il a également vos métriques de surveillance de base pour l’UC, la mise en réseau, mémoire et d’e/s. Sysdig rend toosee facile, utilisez les conteneurs plus difficiles ou essentiellement à l’aide de hello hello mémoire et processeur. Cette vue est dans la section « Présentation », ce qui est actuellement en version bêta de hello. 

![IU Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configurer un déploiement Sysdig avec Marathon
Ces étapes vous indiquent comment tooconfigure et de déploiement Sysdig applications tooyour cluster avec Marathon. 

Accéder à votre interface utilisateur de contrôleur de domaine/système d’exploitation via [http://localhost : 80 /](http://localhost:80/) qu’une seule fois dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello accédez toohello « Univers », qui se trouve sur hello inférieur gauche, puis recherchez « Sysdig ».

![Sysdig dans l’Univers DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

Maintenant les configuration hello toocomplete vous avez besoin d’un Sysdig cloud compte ou un compte d’évaluation gratuit. Une fois que vous êtes connecté dans le site Web du cloud toohello Sysdig, cliquez sur votre nom d’utilisateur et sur la page de hello, vous devez voir votre « clé d’accès ». 

![Clé d’API Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

Ensuite, entrez votre clé d’accès à la configuration Sysdig hello dans hello univers du contrôleur de domaine/système d’exploitation. 

![Configuration Sysdig Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring-sysdig/sysdig3.png)

Maintenant défini hello instances too10000000 afin que chaque fois qu’un nouveau nœud est ajouté le cluster toohello Sysdig déploiera automatiquement un agent toothat nouveau nœud. Il s’agit d’une solution intermédiaire de toomake assurer que sysdig se déploiera tooall nouveaux agents dans un cluster de hello. 

![Configuration Sysdig Bonjour contrôleur de domaine, le système d’exploitation univers-les instances](./media/container-service-monitoring-sysdig/sysdig4.png)

Une fois que vous avez installé le package de hello accédez arrière toohello Sysdig UI et vous pourrez tooexplore en mesure de métriques de l’utilisation de différents hello pour les conteneurs de hello dans votre cluster. 

Vous pouvez également installer des tableaux de bords spécifiques de Mesos et Marathon en utilisant [l’Assistant Nouveau tableau de bord](https://app.sysdigcloud.com/#/dashboards/new).
