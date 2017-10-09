---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaMonitor - gestion des opérations | Documents Microsoft"
description: Surveillez un cluster DC/OS Azure Container Service avec Microsoft Operations Management Suite.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Surveillez un cluster DC/OS Azure Container Service avec Operations Management Suite.

Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Conteneur est une solution dans Analytique de journal d’OMS, ce qui vous permet d’afficher l’inventaire hello conteneur, les performances et les journaux dans un emplacement unique. Vous pouvez auditer, résoudre des conteneurs en consultant les journaux hello dans un emplacement centralisé et trouver bruyantes consommation excessive conteneur sur un ordinateur hôte.

![](media/container-service-monitoring-oms/image1.png)

Pour plus d’informations sur les solutions de conteneur, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Configuration d’OMS à partir de l’univers du contrôleur de domaine/système d’exploitation hello


Cet article suppose que vous avez défini un contrôleur de domaine/système d’exploitation et que vous avez déployé des applications de conteneur web simple sur le cluster de hello.

### <a name="pre-requisite"></a>Conditions préalables
- [Abonnement Microsoft Azure](https://azure.microsoft.com/free/) : vous pouvez l’obtenir gratuitement.  
- Configuration de l’espace de travail Microsoft OMS : voir l’Étape 3 ci-dessous.
- [Interface CLI DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) installées.

1. Dans le tableau de bord du contrôleur de domaine/système d’exploitation hello, cliquez sur l’univers et de recherche à utiliser OMS comme indiqué ci-dessous.

![](media/container-service-monitoring-oms/image2.png)

2. Cliquez sur **Installer**. Vous découvrez un pop avec les informations de version hello OMS et un **installer le Package** ou **Installation avancé** bouton. Lorsque vous cliquez sur **Installation avancé**, qui vous guide toohello **propriétés de configuration spécifiques OMS** page.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Ici, nous vous demanderons tooenter hello `wsid` (hello ID d’espace de travail OMS) et `wskey` (hello OMS clé primaire pour l’id d’espace de travail hello). tooget les deux `wsid` et `wskey` vous devez toocreate un compte OMS à <https://mms.microsoft.com>. Veuillez suivre hello étapes toocreate un compte. Une fois que vous avez terminé la création de compte de hello, vous devez tooobtain votre `wsid` et `wskey` en cliquant sur **paramètres**, puis **Sources connectées**, puis **des serveurs Linux** , comme illustré ci-dessous.

 ![](media/container-service-monitoring-oms/image5.png)

4. Sélectionnez hello numéro vous OMS instances que vous souhaitez et cliquez sur bouton de « Examinez et installez » hello. En règle générale, vous pouvez toohave hello nombre de OMS instances toohello égale la machine virtuelle vous avez dans votre cluster de l’agent. Agent OMS pour Linux est installe en tant que conteneurs individuels sur chaque machine virtuelle qu’il souhaite toocollect des informations pour l’analyse et les informations de journalisation.

## <a name="setting-up-a-simple-oms-dashboard"></a>Configuration d’un tableau de bord OMS simple

Une fois que vous avez installé hello Agent OMS pour Linux sur les machines virtuelles de hello, étape suivante consiste à tooset de tableau de bord OMS hello. Il existe deux façons toodo cela : portail OMS ou le portail Azure.

### <a name="oms-portal"></a>Portail OMS 

Connectez-vous au portail OMS est toohello (<https://mms.microsoft.com>) et accédez toohello **galerie de solutions**.

![](media/container-service-monitoring-oms/image6.png)

Une fois que vous êtes dans hello **galerie de solutions**, sélectionnez **conteneurs**.

![](media/container-service-monitoring-oms/image7.png)

Une fois que vous avez sélectionné hello conteneur Solution, vous verrez hello vignette sur la page de vue d’ensemble du tableau de bord OMS hello. Une fois que les données de conteneur hello ingéré sont indexées, vous verrez vignette hello rempli avec les informations sur les vignettes de vue de solution.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Portail Azure 

Portail de tooAzure de connexion à l’adresse <https://portal.microsoft.com/>. Go to **Marketplace**, sélectionnez **Surveillance + gestion**, puis cliquez sur **Afficher tout**. Ensuite, saisissez `containers` dans la recherche. Vous verrez « conteneurs » dans les résultats de recherche hello. Sélectionnez **Conteneurs**, puis cliquez sur **Créer**.

![](media/container-service-monitoring-oms/image9.png)

Une fois que vous avez cliqué sur **Créer**, vous êtes invité à saisir votre espace de travail. Sélectionnez votre espace de travail. Si vous n’en avez pas, créez-en un.

![](media/container-service-monitoring-oms/image10.PNG)

Une fois la sélection effectuée, cliquez sur **Créer**.

![](media/container-service-monitoring-oms/image11.png)

Pour plus d’informations sur hello OMS conteneur Solution, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Comment tooscale l’Agent OMS avec contrôleur de domaine/système d’exploitation des services ACS 

Au cas où vous avez besoin de l’agent OMS de toohave installé au niveau du nombre de nœud réel hello ou mise à l’échelle de la mise en ajoutant plus d’ordinateurs virtuels, vous pouvez le faire par la mise à l’échelle hello `msoms` service.

Vous pouvez soit tooMarathon ou hello onglet de Services de l’interface utilisateur de contrôleur de domaine/système d’exploitation et l’échelle votre nombre de nœuds.

![](media/container-service-monitoring-oms/image12.PNG)

Cette action déploie tooother les nœuds dont vous n’ont pas encore déployé l’agent OMS de hello.

## <a name="uninstall-ms-oms"></a>Désinstaller MS OMS

toouninstall MS OMS entrez hello de commande suivante :

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Dites-le-nous !
Qu’est-ce qui fonctionne ? Quels sont les manquements ? Quoi d’autre devez-vous pour cette toobe utiles pour vous ? Faites-le nous savoir sur <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Étapes suivantes

 Maintenant que vous avez configuré OMS toomonitor vos conteneurs,[voir votre tableau de bord du conteneur](../../log-analytics/log-analytics-containers.md).
