---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - Dynatrace | Documents Microsoft"
description: "Surveillez un cluster DC/OS Azure Container Service avec Dynatrace. Déployer hello Dynatrace OneAgent à l’aide du tableau de bord hello contrôleur de domaine/système d’exploitation."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Surveiller un cluster DC/OS Azure Container Service avec Dynatrace SaaS/Managed
Dans cet article, nous vous indiquons comment toodeploy hello [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent tous les hello des nœuds de l’agent de votre cluster de Service de conteneur Azure. Vous avez besoin d’un compte Dynatrace SaaS/Managé pour cette configuration. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managé
Dynatrace est une solution de surveillance cloud native pour environnements de clusters et de conteneurs hautement dynamiques. Il vous permet de toobetter optimiser vos déploiements de conteneur et les allocations de mémoire à l’aide des données d’utilisation en temps réel. Elle est capable d’identifier automatiquement les problèmes d’infrastructure et d’applications en fournissant une planification automatisée, une corrélation des problèmes et une détection des causes racines.

la figure suivant de Hello affiche hello Dynatrace UI :

![IU de Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Composants requis 
[Déployer](container-service-deployment.md) et [connecter](./../container-service-connect.md) cluster tooa configuré par le Service de conteneur Azure. Explorer hello [Marathon UI](container-service-mesos-marathon-ui.md). Accédez trop[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset d’un compte Dynatrace SaaS.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Configurer un déploiement Dynatrace avec Marathon
Ces étapes vous montrent comment tooconfigure et de déploiement Dynatrace applications tooyour cluster avec Marathon.

1. Accédez à l'interface utilisateur de votre contrôleur de domaine/système d’exploitation via [http://localhost:80/](http://localhost:80/). Une fois dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello, accédez toohello **univers** onglet, puis recherchez **Dynatrace**.

    ![Dynatrace dans l’Univers DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. configuration de hello toocomplete, vous devez un compte Dynatrace SaaS ou un compte d’évaluation gratuit. Une fois que vous ouvrez une session dans le tableau de bord Dynatrace hello, sélectionnez **Dynatrace de déployer**.

    ![Configurer l’intégration PaaS Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Sur la page de hello, sélectionnez **configurer l’intégration de PaaS**. 

    ![Jeton API Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Entrez votre jeton d’API dans hello configuration Dynatrace OneAgent dans hello univers du contrôleur de domaine/système d’exploitation. 

    ![Configuration de dynaTrace OneAgent Bonjour univers du contrôleur de domaine/système d’exploitation](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Définir des instances de hello toohello nombre de nœuds vous avez l’intention de toorun. Définir un nombre plus élevé d’également fonctionne, mais contrôleur de domaine/système d’exploitation renouvellement des tentatives toofind nouvelles instances jusqu'à ce que ce nombre est atteint réellement. Si vous préférez, vous pouvez également définir cette valeur tooa comme 1000000. Dans ce cas, chaque fois qu’un nouveau nœud est ajouté toohello cluster, Dynatrace déploie automatiquement un agent toothat nouveau nœud, à prix hello du contrôleur de domaine/système d’exploitation en permanence la tentative de toodeploy des instances supplémentaires.

    ![Configuration dynaTrace Bonjour contrôleur de domaine, le système d’exploitation univers-les instances](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez installé le package de hello, accédez à tableau de bord Dynatrace toohello précédent. Vous pouvez explorer des métriques d’utilisation différentes hello pour les conteneurs de hello dans votre cluster. 
