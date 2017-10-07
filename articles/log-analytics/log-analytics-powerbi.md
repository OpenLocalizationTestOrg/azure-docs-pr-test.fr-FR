---
title: "tooPower de données Analytique de journal aaaExport BI | Documents Microsoft"
description: "Power BI est un service Microsoft d’analyse commerciale basé sur le cloud qui fournit de riches fonctions de visualisation et de rapport afin de faciliter l’analyse de différents jeux de données.  Analytique de journal permettre en permanence exporter des données à partir du référentiel OMS de hello dans Power BI afin de vous pouvez tirer parti de ses visualisations et les outils d’analyse.  Cet article décrit le fonctionnement des requêtes tooconfigure dans Analytique de journal qui exportent automatiquement tooPower BI à intervalles réguliers."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Exporter les données de journal Analytique tooPower BI

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis ce processus d’exportation des données de journal Analytique tooPower BI ne fonctionnera plus.  Toutes les planifications existantes que vous avez créées avant la mise à niveau sont alors désactivées. 
>
> Après la mise à niveau, les utilisations Analytique de journal Azure hello même plateforme en tant qu’Application Insights et que vous utilisez hello même processus tooexport Analytique de journal des requêtes tooPower BI en tant que [hello processus tooexport Application Insights interroge tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Vous pouvez exporter requête hello à l’aide de la console d’Analytique hello comme décrit dans cet article, ou vous pouvez sélectionner hello **Power BI** bouton haut hello écran hello dans le portail de recherche de journal hello.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) est un service Microsoft d’analyse commerciale basé sur le cloud qui fournit de riches fonctions de visualisation et de rapport afin de faciliter l’analyse de différents jeux de données.  Analytique de journal peut automatiquement exporter des données à partir du référentiel d’OMS hello dans Power BI afin de vous pouvez tirer parti de ses visualisations et les outils d’analyse.

Lorsque vous configurez Power BI avec Analytique de journal, vous créez des requêtes de journal qui exportent leurs résultats toocorresponding des groupes de données dans Power BI.  exportation et requête de hello continue tooautomatically exécuter selon une planification que vous définissez un dataset de hello tookeep des toodate avec les données les plus récentes hello collectées par Analytique de journal.

![Journal Analytique tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Planifications Power BI
A *Power BI planification* inclut une recherche de journal qui exporte un jeu de données à partir de hello OMS référentiel tooa jeu de données correspondant dans Power BI et une planification qui définit la fréquence à laquelle cette recherche est exécutée dataset de hello tookeep actuel.

champs Hello hello dataset correspondront propriétés hello d’enregistrements de hello renvoyés par la recherche de journal hello.  Si la recherche de hello retourne des enregistrements de différents types hello dataset inclut toutes les propriétés de hello de chacun des hello incluses types d’enregistrements.  

> [!NOTE]
> Il s’agit d’une meilleure toouse de pratique une requête de recherche de journal qui retourne des données brutes en opposition tooperforming une consolidation à l’aide des commandes telles que [mesure](log-analytics-search-reference.md#measure).  Vous pouvez effectuer n’importe quel regroupement et les calculs dans Power BI à partir des données brutes de hello.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Connexion tooPower d’espace de travail OMS BI
Avant de pouvoir exporter à partir de l’Analytique de journal tooPower BI, vous devez vous connecter à votre espace de travail tooyour Power BI de compte OMS à l’aide de la procédure de hello.  

1. Dans la console OMS hello, cliquez sur hello **paramètres** vignette.
2. Sélectionnez **Comptes**.
3. Bonjour **informations de l’espace de travail** cliquez sur la section **connecter tooPower compte BI**.
4. Entrez des informations d’identification de hello pour votre compte Power BI.

## <a name="create-a-power-bi-schedule"></a>Création d’une planification Power BI
Créer une planification de BI de puissance pour chaque jeu de données à l’aide de la procédure de hello.

1. Dans la console OMS hello, cliquez sur hello **recherche de journal** vignette.
2. Tapez une nouvelle requête ou sélectionnez une recherche enregistrée que retourne hello des données que vous souhaitez trop tooexport**Power BI**.  
3. Cliquez sur hello **Power BI** bouton haut hello hello de hello page tooopen **Power BI** boîte de dialogue.
4. Fournir des informations de hello Bonjour suivante, la table et cliquez sur **enregistrer**.

| Propriété | Description |
|:--- |:--- |
| Nom |Planification de la hello de tooidentify nom lorsque vous affichez la liste hello des planifications de Power BI. |
| Recherche enregistrée |toorun de recherche de journal Hello.  Vous pouvez sélectionner la requête en cours hello ou sélectionnez une recherche enregistrée à partir de la zone de liste déroulante hello. |
| Planification |La fréquence à laquelle hello toorun enregistré recherche et d’exportation de jeu de données toohello Power BI.  Hello doit être comprise entre 15 minutes et 24 heures. |
| Nom du jeu de données |nom Hello du jeu de données hello dans Power BI.  Ce nom sera créé s’il n’existe pas ; dans le cas contraire, il sera mis à jour. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Affichage et suppression de planifications Power BI
Afficher la liste hello des planifications de BI Power existantes avec hello suivant la procédure.

1. Dans la console OMS hello, cliquez sur hello **paramètres** vignette.
2. Sélectionnez **Power BI**.

De plus de planifier des détails toohello Hello, nombre hello de hello planification s’est exécutée hello semaine dernière et état de hello de hello dernière synchronisation sont affichés.  Si la synchronisation de hello a rencontré des erreurs, vous pouvez cliquer sur hello lien toorun une recherche de journal pour les enregistrements avec les détails de l’erreur de hello.

Vous pouvez supprimer une planification en cliquant sur hello **X** Bonjour **Supprimer colonne**.  Pour désactiver une planification, sélectionnez **Désactivé**.  toomodify une planification, vous devez le supprimer et recréer avec les nouveaux paramètres de hello.

![Planifications Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Exemple de procédure pas à pas
Hello suivante section décrit un exemple de création d’une planification de BI Power et à l’aide de son toocreate dataset un rapport simple.  Dans cet exemple, toutes les données de performances pour un ensemble d’ordinateurs est exporté tooPower BI et un graphique linéaire est créé toodisplay d’utilisation du processeur.

### <a name="create-log-search"></a>Création de la recherche de journal
Nous commençons par créer une recherche de journal pour les données hello que nous souhaitons toosend toohello dataset.  Dans cet exemple, nous allons utiliser une requête qui retourne toutes les données de performances des ordinateurs dont le nom commence par *srv*.  

![Planifications Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Création d’une recherche Power BI
Cliquez sur hello **Power BI** bouton boîte de dialogue tooopen hello Power BI et fournissent des informations de hello requis.  Cette toorun recherche une fois par heure et nous créer un dataset nommé *Contoso Perf*.  Étant donné que nous avons déjà ouvrir recherche hello qui crée les données de hello nous souhaitons, nous conservons hello comme valeur par défaut *utiliser la requête de recherche en cours* pour **recherche enregistrée**.

![Recherche Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Vérification de la recherche Power BI
tooverify que nous avons créé la planification de hello correctement, nous permet d’afficher hello liste de Power BI recherche sous hello **paramètres** vignette dans le tableau de bord OMS hello.  Nous Patientez quelques minutes et actualiser cette vue jusqu'à ce qu’il signale que la synchronisation de hello a été exécutée.

![Recherche Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Vérifiez que le dataset hello dans Power BI
Nous allons nous connecter à notre compte [powerbi.microsoft.com](http://powerbi.microsoft.com/) et faites défiler trop**Datasets** bas hello du volet de gauche hello.  Nous pouvons voir que hello *Contoso Perf* jeu de données est répertorié, indiquant que notre exportation a été exécutée avec succès.

![Jeu de données Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Création d’un rapport dérivé du jeu de données
Nous allons sélectionner hello **Contoso Perf** jeu de données, puis cliquez sur **résultats** Bonjour **champs** volet sur des champs hello hello tooview droit qui font partie de ce jeu de données.  toocreate ligne graphique montrant l’utilisation de processeur pour chaque ordinateur, nous effectuons hello suivant des actions.

1. Sélectionnez la visualisation de graphique de ligne hello.
2. Faites glisser **ObjectName** trop**filtre de rapport** et **processeur**.
3. Faites glisser **CounterName** trop**filtre de rapport** et **% temps processeur**.
4. Faites glisser **CounterValue** trop**valeurs**.
5. Faites glisser **ordinateur** trop**légende**.
6. Faites glisser **TimeGenerated** trop**axe**.

Nous pouvons voir que hello résultant ligne ce graphique est affiché avec les données de hello à partir de notre jeu de données.

![Graphique en courbes Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Enregistrer le rapport de hello
Nous enregistrer le rapport hello en cliquant sur hello bouton haut hello écran hello enregistrer et valider qu’il est maintenant répertorié dans la section rapports de hello dans le volet gauche de hello.

![Rapports Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toobuild les requêtes qui peuvent être exportées tooPower BI.
* En savoir plus sur [Power BI](http://powerbi.microsoft.com) toobuild visualisations selon les exportations Analytique de journal.
