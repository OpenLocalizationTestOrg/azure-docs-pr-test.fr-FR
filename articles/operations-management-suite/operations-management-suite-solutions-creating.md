---
title: aaaBuild une solution de gestion dans OMS | Documents Microsoft
description: "Solutions de gestion d’étendent les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir espace de travail OMS.  Cet article fournit des détails sur la façon dont vous pouvez créer toobe des solutions de gestion utilisé dans votre propre environnement ou apportées disponible tooyour clients."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Concevoir et générer une solution de gestion dans Operations Management Suite (OMS) (préversion)
> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.

[Solutions de gestion](operations-management-suite-solutions.md) étendre les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir espace de travail OMS.  Cet article présente un processus de base de toodesign et créer une solution de gestion qui est adaptée aux besoins courants.  Si vous êtes toobuilding de nouvelles solutions de gestion vous pouvez utiliser ce processus comme point de départ et exploitez les concepts hello pour les solutions plus complexes que vos besoins évoluent.

## <a name="what-is-a-management-solution"></a>Qu’est-ce qu’une solution de gestion ?

Solutions de gestion contiennent OMS et des ressources Azure qui coopèrent tooachieve un scénario d’analyse spécifique.  Ils sont implémentés en tant que [les modèles de gestion des ressources](../azure-resource-manager/resource-manager-template-walkthrough.md) qui contiennent des détails de la façon tooinstall et configurer leurs ressources de contenu lors de la solution de hello est installée.

stratégie de base de Hello est toostart votre solution de gestion en créant des composants individuels hello dans votre environnement Windows Azure.  Une fois que vous disposez des fonctionnalités hello fonctionne correctement, vous pouvez ensuite démarrer les compresser dans un [fichier de solution de gestion](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Conception de votre solution
modèle le plus courant pour une solution de gestion Hello est illustrée dans hello suivant schéma.  Hello différents composants dans ce modèle sont abordées dans hello ci-dessous.

![Vue d’ensemble de la solution OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Sources de données
Hello première étape de conception d’une solution consiste à déterminer les données de salutation dont vous avez besoin à partir du référentiel d’Analytique de journal hello.  Ces données peuvent être collectées par une [source de données](../log-analytics/log-analytics-data-sources.md) ou [une autre solution](operations-management-suite-solutions.md), votre solution devrez tooprovide hello processus toocollect il.

Il existe plusieurs façons les sources de données qui peuvent être collectées dans le référentiel d’Analytique de journal hello comme décrit dans [des sources de données dans le journal Analytique](../log-analytics/log-analytics-data-sources.md).  Cela inclut les événements Bonjour journal des événements Windows ou généré par Syslog en outre tooperformance compteurs pour les clients Windows et Linux.  Vous pouvez également collecter des données à partir des ressources Azure collectées par Azure Monitor.  

Si vous avez besoin des données qui ne sont pas accessibles par le biais de sources de données disponibles hello, vous pouvez ensuite utiliser hello [API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md) qui vous permet de référentiel de toowrite données toohello Analytique de journal à partir de n’importe quel client qui peut appeler un reste. API.  Bonjour approche la plus courante de collecte de données personnalisé dans une solution de gestion est toocreate un [runbook dans Azure Automation](../automation/automation-runbook-types.md) qui collecte les données de hello requis à partir des ressources Azure ou externes et utilise hello toowrite de l’API de collecteur de données référentiel de toohello.  

### <a name="log-searches"></a>Recherches dans les journaux
[Recherche de journal](../log-analytics/log-analytics-log-searches.md) sont tooextract utilisé et analyser les données dans le référentiel d’Analytique de journal hello.  Ils sont utilisés par les vues et les alertes dans Ajout tooallowing hello utilisateur tooperform analyse ad hoc des données dans le référentiel de hello.  

Vous devez définir toutes les requêtes que vous considérez utiles toohello utilisateur même s’ils ne sont pas utilisés par toutes les vues ou les alertes.  Ils vous seront toothem disponible en tant que recherches enregistrées dans le portail de hello, et vous pouvez également les inclure dans un [partie de visualisation de liste de requêtes](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) dans votre affichage personnalisé.

### <a name="alerts"></a>Alertes
[Les alertes dans le journal Analytique](../log-analytics/log-analytics-alerts.md) identifier les problèmes via [recherche de journal](#log-searches) par rapport aux données hello dans le référentiel de hello.  Ils notifier hello utilisateur ou exécutent automatiquement une action en réponse. Vous devez identifier différentes conditions d’alerte pour votre application et inclure des règles d’alerte correspondantes dans votre fichier solution.

Si le problème de hello peut potentiellement être corrigée par un processus automatisé, vous allez généralement créer un runbook dans Azure Automation tooperform cette mise à jour.  Services Azure plus peuvent être gérés avec [applets de commande](/powershell/azure/overview) le runbook hello pourrait exploiter tooperform ces fonctionnalités.

Si votre solution nécessite une fonctionnalité externe dans l’alerte tooan de réponse, vous pouvez ensuite utiliser un [webhook réponse](../log-analytics/log-analytics-alerts-actions.md).  Ainsi, vous toocall un service web externe envoie des informations à partir de l’alerte de hello.

### <a name="views"></a>Views
Vues d’Analytique de journal sont données toovisualize utilisé à partir du référentiel d’Analytique de journal hello.  Chaque solution contient généralement une seule vue avec un [vignette](../log-analytics/log-analytics-view-designer-tiles.md) qui s’affiche sur le tableau de bord principal de l’utilisateur hello.  affichage de Hello peut contenir un nombre quelconque de [des parties de visualisation](../log-analytics/log-analytics-view-designer-parts.md) tooprovide différentes visualisations d’utilisateur de toohello hello les données collectées.

Vous [créer des vues personnalisées à l’aide de hello Concepteur de vue](../log-analytics/log-analytics-view-designer.md) que vous pouvez ultérieurement exporter pour l’inclure dans votre fichier de solution.  


## <a name="create-solution-file"></a>Créer le fichier solution
Une fois que vous avez configuré et testé des composants hello qui feront partie de votre solution, vous pouvez [créer votre fichier solution](operations-management-suite-solutions-solution-file.md).  Vous allez implémenter des composants de la solution hello dans un [modèle Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) qui inclut un [ressources solution](operations-management-suite-solutions-solution-file.md#solution-resource) toohello des relations avec les autres ressources hello fichier.  


## <a name="test-your-solution"></a>Tester votre solution
Pendant le développement de votre solution, vous devez tooinstall et testez-le dans votre espace de travail.  Cela à l’aide d’une des méthodes disponibles de hello trop[de test et d’installer le Gestionnaire de ressources modèles](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publier votre solution
Une fois que vous avez terminé et testé votre solution, vous pouvez rendre toocustomers disponible via soit hello sources suivantes.

- **Modèles de démarrage rapide Azure**.  [Les modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/) est un ensemble de modèles de gestionnaire de ressources fournis par la Communauté hello via GitHub.  Vous pouvez rendre votre solution disponibles en les informations suivantes dans hello [guide de contribution au](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Place de marché Azure**.  Hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) vous permet de toodistribute et vendre votre solution tooother développeurs, éditeurs de logiciels indépendants et les professionnels de l’informatique.  Vous pouvez apprendre comment toopublish votre tooAzure solution Marketplace à [comment toopublish et gérer une offre Bonjour Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[créer un fichier de solution](operations-management-suite-solutions-solution-file.md) pour votre solution de gestion.
* En savoir plus de détails hello de [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Dans [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates), recherchez des exemples de modèles Resource Manager.