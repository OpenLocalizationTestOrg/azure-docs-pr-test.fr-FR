---
title: "aaaService solution de mappage au rythme de démonstration | Documents Microsoft"
description: "Carte de service est une solution dans Operations Management Suite (OMS) qui découvre automatiquement les composants de l’application sur Windows et les mappages et les systèmes Linux hello la communication entre les services.  Il s’agit d’une démonstration à ses personnel qui vous guide à l’aide de la carte de Service tooidentify et diagnostiquer un problème simulé dans une application web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Démonstration à votre rythme d’Operations Management Suite (OMS) - Carte de service
Il s’agit d’une démonstration à ses personnel pour vous aider à l’aide de hello [solutions de carte de Service](operations-management-suite-service-map.md) dans tooidentify d’Operations Management Suite (OMS) et de diagnostiquer un problème simulé dans une application web.  Carte de service découvre automatiquement les composants de l’application sur les systèmes Windows et Linux et mappages hello la communication entre les services.  Il regroupe également les données collectées par les autres tooassist de services OMS dans l’analyse des performances et d’identifier les problèmes.  Vous utiliserez également [connecter recherche Analytique de journal](../log-analytics/log-analytics-log-searches.md) toodrill vers le bas sur les données collectées dans l’origine du problème ordre tooidentify hello.


## <a name="scenario-description"></a>Description du scénario
Vous venez de recevoir une notification qu’application de portail du client ACME hello rencontre des problèmes de performances.  Hello seules les informations dont vous disposez sont que ces problèmes a démarré sur 4:00 am PST aujourd'hui.  Vous n’êtes pas sûre de tous les composants hello ce portail hello dépend autre qu’un ensemble de serveurs web.  

## <a name="components-and-features-used"></a>Composants et fonctionnalités utilisés
- [Solution Carte de service](operations-management-suite-service-map.md)
- [Recherches de journal Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Procédure

### <a name="1-connect-toohello-oms-experience-center"></a>1. Connexion toohello OMS expérience Center
Cette procédure pas à pas utilise hello [Operations Management Suite expérience Center](https://experience.mms.microsoft.com/) qui fournit un environnement OMS complet avec des exemples de données. Démarrez en suivant ce lien, fournissez vos informations et sélectionnez hello **Insight & Analytique** scénario.


### <a name="2-start-service-map"></a>2. Lancement de Carte de service
Démarrer la solution de carte de Service hello en cliquant sur hello **carte de Service** vignette.

![Vignette Carte de service](media/operations-management-suite-walkthrough-servicemap/tile.png)

console de Service Map Hello s’affiche.  Bonjour volet de gauche est une liste d’ordinateurs dans votre environnement avec l’agent de carte de Service hello installé.  Vous devez sélectionner l’ordinateur hello que vous souhaitez tooview dans cette liste.

![Liste des ordinateurs](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Affichage de l’ordinateur
Nous savons que les serveurs web hello sont appelées AcmeWFE001 et AcmeWFE002, cela semble être une toostart raisonnable sur place.  Cliquez sur **AcmeWFE001**.  Cela affiche la carte hello pour AcmeWFE001 et toutes ses dépendances.  Vous pouvez voir les processus qui sont en cours d’exécution sur l’ordinateur sélectionné de hello et qui ils communiquent avec des services externes.

![Serveur web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Nous sommes favoriser les performances hello de notre site web application cliquez donc sur hello **AcmeAppPool (Pool d’applications IIS)** processus.  Cela affiche les détails de hello pour ce processus et met en évidence ses dépendances.  

![Pool d’applications](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Modification de la fenêtre de temps

Nous avons reçu ce problème hello démarré à 4 h 00, nous allons donc examiner que s’est-il passé à ce moment-là. Cliquez sur **période** et modifiez hello temps too4 : 00 AM PST (conserver hello date actuelle et l’ajuster pour votre fuseau horaire local) avec une durée de 20 minutes.

![Sélecteur d’heure](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Affichage de l’alerte

Vous pouvez désormais voir ce hello **acmetomcat** dépendance est associée à une alerte s’affichera, c’est notre problème potentiel.  Cliquez sur l’icône d’alerte hello dans **acmetomcat** tooshow hello détails de l’hello alerte.  Nous pouvons constater une utilisation critique du processeur et nous pouvons développer pour obtenir plus de détails.  C’est probablement la cause de notre ralentissement des performances. 

![Alerte](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Affichage des performances

Regardons **acmetomcat** de plus près.  Cliquez sur Bonjour haut à droite de **acmetomcat** et sélectionnez **charge serveur carte** tooshow hello détail et les dépendances de cet ordinateur. Nous pouvons ensuite étudier un peu plus ces tooverify de compteurs de performances notre suspicion.  Sélectionnez hello **performances** hello de toodisplay onglet [les compteurs de performances collectées par le journal Analytique](../log-analytics/log-analytics-data-sources-performance-counters.md) sur la plage temporelle de hello.  Nous constatons que nous préparons pointes périodiques dans la mémoire et du processeur de hello.

![Performances](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Affichage du suivi des modifications
Voyons si nous pouvons trouver les causes possibles de cette utilisation intensive.  Cliquez sur hello **Résumé** onglet.  Cela fournit des informations OMS a recueilli hello comme Échec de connexions, les alertes critiques et les modifications apportées au logiciel.  Sections avec des informations récentes intéressantes doivent déjà être développées, et vous pouvez développer d’autres informations sur les sections tooinspect qu’ils contiennent.


Si **Suivi des modifications** n’est pas déjà ouvert, développez-le.  Affiche les informations collectées par hello [suivi des modifications de la solution](../log-analytics/log-analytics-change-tracking.md).  Il semblerait qu’une modification logicielle ait été effectuée dans cette fenêtre de temps.  Cliquez sur **logiciel** tooget détails.  Un processus de sauvegarde a été ajouté toohello ordinateur juste après 4:00 AM, donc cela semble coupable de hello toobe pour l’utilisation des ressources excessive hello.

![Suivi des modifications](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Affichage des détails dans Recherche dans les journaux
Nous pouvons davantage le vérifier en examinant hello des informations de performances collectées dans le référentiel d’Analytique de journal hello détaillées.  Cliquez sur hello **alertes** onglet Nouveau puis, dans un des hello **élevée du processeur** alertes.  Cliquez sur **Show in Log Search (Afficher dans Recherche dans les journaux)**.  Cela ouvre la fenêtre de recherche de journal hello où vous pouvez effectuer [recherche de journal](../log-analytics/log-analytics-log-searches.md) par rapport à toutes les données stockées dans le référentiel de hello.  Carte de service déjà renseigné un queriy pour nous alerte de hello tooretrieve nous intéresse.  

![Recherche dans les journaux](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Ouverture d’une recherche enregistrée
Voyons si nous pouvons obtenir certaines plus de détails sur la collecte des performances hello qui a généré cette alerte et vérifier notre suspecte que des problèmes de hello sont provoquées par ce processus de sauvegarde.  Modifier trop de plage de temps hello**6 heures**.  Cliquez ensuite sur **favoris** et faites défiler vers le bas recherche toohello enregistré **carte de Service**.  Il s’agit des requêtes que vous avez créées spécifiquement pour cette analyse.  Cliquez sur **Top 5 Processes by CPU for acmetomcat (5 premiers processus par processeur pour acmetomcat)**.

![Recherche enregistrée](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Cette requête retourne une liste de hello principaux 5 processus consomme du processeur sur **acmetomcat**.  Vous pouvez inspecter hello requête tooget un langage de requête introduction toohello utilisé pour les recherches de journal.  Si vous êtes intéressé par les processus hello sur d’autres ordinateurs, vous pouvez modifier ces informations hello requête tooretrieve.

Dans ce cas, nous pouvons voir que les processus de sauvegarde hello constamment consomme environ 60 % de l’UC du serveur d’application hello.  Il apparaît clairement que ce nouveau processus est responsable de notre problème de performances.  Notre solution évidemment serait tooremove ce nouveau logiciel serveur d’application hello de sauvegarde.  Nous avons réellement tirer parti de Configuration d’état souhaité (DSC) géré par Azure Automation toodefine stratégies qui garantissent que ce processus ne s’exécute jamais sur ces systèmes critiques.


## <a name="summary-points"></a>Résumé
- [Carte de service](operations-management-suite-service-map.md) vous fournit une vue de l’intégralité de votre application même si vous ne connaissez pas tous ses serveurs et dépendances.
- Carte de service met en évidence des données collectées par les autres toohelp de solutions OMS vous identifiez des problèmes avec votre application et son infrastructure sous-jacente.
- [Recherche de journal](../log-analytics/log-analytics-log-searches.md) permettent de toodrill vers le bas dans des données spécifiques recueillies dans le référentiel d’Analytique de journal hello.    

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur [Carte de service](operations-management-suite-service-map.md).
- [Déployer et configurer](operations-management-suite-service-map-configure.md) Carte de service.
- En savoir plus sur [Log Analytics](../log-analytics/log-analytics-overview.md) qui est requis pour Carte de service et conserve les données opérationnelles stockées par les agents.