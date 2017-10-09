---
title: portail de recherche de journal aaaUsing hello dans Analytique de journal Azure | Documents Microsoft
description: "Cet article inclut un didacticiel décrivant comment toocreate recherches de journal et analyser les données stockées dans votre espace de travail Analytique des journaux à l’aide du portail de recherche de journal hello.  didacticiel de Hello inclut en cours d’exécution des requêtes simples tooreturn différents types de données et analyse des résultats."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Créer des recherches de journal dans Azure Analytique de journal à l’aide du portail de recherche de journal hello

> [!NOTE]
> Cet article décrit le portail de recherche de journal hello dans Azure Analytique de journal à l’aide du nouveau langage de requête hello.  Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).  
>
> Si votre espace de travail n’a pas été mis à niveau toohello nouveau langage de requête, vous devez faire référence trop[trouver des données à l’aide de recherches de journal dans le journal Analytique](log-analytics-log-searches.md) pour plus d’informations sur la version actuelle de hello du portail de recherche de journal hello.

Cet article inclut un didacticiel décrivant comment toocreate recherches de journal et analyser les données stockées dans votre espace de travail Analytique des journaux à l’aide du portail de recherche de journal hello.  didacticiel de Hello inclut en cours d’exécution des requêtes simples tooreturn différents types de données et analyse des résultats.  Il se concentre sur les fonctionnalités dans le portail de recherche de journal hello pour modifier la requête de hello plutôt que de modifier directement.  Pour plus d’informations sur la modification directe de requête de hello, consultez hello [référence du langage de requête](https://go.microsoft.com/fwlink/?linkid=856079).

recherche toocreate dans portail d’Analytique de Advanced hello au lieu du portail de recherche de journal hello, consultez [prise en main de hello Analytique Portal](https://go.microsoft.com/fwlink/?linkid=856587).  Les deux portails utilisent hello requête même langage tooaccess hello des mêmes données dans l’espace de travail hello Analytique de journal.

## <a name="prerequisites"></a>Composants requis
Ce didacticiel suppose que vous disposez déjà d’un espace de travail Analytique de journal au moins une source connectée qui génère des données pour hello requêtes tooanalyze.  

- Si vous n’avez pas un espace de travail, vous pouvez créer un gratuitement à l’aide de la procédure hello sur [prise en main avec un espace de travail Analytique de journal](log-analytics-get-started.md).
- Se connecter au moins un [agent Windows](log-analytics-windows-agents.md) ou un [agent Linux](log-analytics-linux-agents.md) toohello espace de travail.  

## <a name="open-hello-log-search-portal"></a>Portail de recherche de journal hello ouvert
Commencez par ouvrir le portail de recherche de journal hello.  Vous pouvez y accéder dans hello portail Azure ou du portail OMS hello.

1. Ouvrez hello portail Azure.
2. Accédez tooLog Analytique et sélectionnez votre espace de travail.
3. Sélectionnez **recherche de journal** toostay Bonjour Azure portal ou lancez hello du portail OMS en sélectionnant **portail OMS** , puis sur le bouton de recherche de journal hello.

![Bouton Recherche dans les journaux](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Créer une recherche simple
tooretrieve moyen le plus rapide de Hello toowork de certaines données avec est une requête simple qui retourne tous les enregistrements dans la table.  Si vous disposez d’un espace de travail Windows ou Linux clients tooyour connecté, puis vous allez ont des données dans hello soit des événements (Windows) ou une table de Syslog (Linux).

Tapez une Bonjour suite de requêtes dans la zone de recherche hello et cliquez sur le bouton de recherche hello.  

```
Event
```
```
Syslog
```

Données sont retournées dans l’affichage de liste par défaut hello, et vous pouvez voir le nombre total d’enregistrements retournés.

![Requête simple](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Uniquement hello premier quelques propriétés de chaque enregistrement sont affichées.  Cliquez sur **afficher plus** toodisplay toutes les propriétés pour un enregistrement particulier.

![Détails des enregistrements](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Définir l’étendue de temps hello
Chaque enregistrement collecté par Analytique de journal a un **TimeGenerated** propriété contenant hello date et heure de cet enregistrement hello a été créé.  Une requête dans le portail de recherche de journal hello retourne uniquement les enregistrements avec un **TimeGenerated** étendue hello temps qui s’affiche sur hello à gauche de l’écran hello.  

Vous pouvez modifier le filtre d’heure hello en sélectionnant la liste déroulante de hello ou en modifiant le curseur de hello.  curseur de Hello affiche un graphique à barres qui affiche hello de nombre relatif des enregistrements pour chaque segment de temps au sein de la plage de hello.  Ce segment varie en fonction de la plage de hello.

étendue de temps par défaut Hello est **1 jour**.  Modifiez cette valeur trop**7 jours**, et hello le nombre total d’enregistrements doit augmenter.

![Période](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Filtrer les résultats de requête de hello
Sur hello à gauche de l’écran hello est le volet de filtre hello qui vous permet de tooadd filtrage toohello requête sans le modifier directement.  Plusieurs propriétés de hello les enregistrements retournés sont affichées avec leurs dix premières valeurs avec leur nombre d’enregistrements.

Si vous travaillez avec **événement**, sélectionnez hello case à cocher l’ensuite trop**erreur** sous **valeur EVENTLEVELNAME**.   Si vous travaillez avec **Syslog**, sélectionnez hello case à cocher l’ensuite trop**err** sous **SEVERITYLEVEL**.  Cela modifie la requête hello tooone Hello suivant toolimit hello tooerror événements des résultats.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtrer](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Volet de filtre toohello ajouter propriétés en sélectionnant **ajouter toofilters** à partir du menu de propriété hello sur l’un des enregistrements de hello.

![Toofilter menu Ajouter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Vous pouvez définir hello même filtre en sélectionnant **filtre** à partir du menu de propriété hello pour un enregistrement avec la valeur de hello souhaité toofilter.  

Il vous suffit hello **filtre** option pour les propriétés par leur nom en bleu.  Il s’agit de champs *dans lesquels une recherche peut être effectuée* et qui sont indexés pour les conditions de recherche.  Les champs en gris sont *libérer des recherches de texte* les champs qui ont uniquement des hello **afficher les références** option.  Cette option retourne les enregistrements qui ont cette valeur dans une propriété quelconque.

![Menu Filtrer](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Vous pouvez regrouper les résultats de hello sur une seule propriété en sélectionnant hello **regrouper par** option dans le menu d’enregistrement hello.  Cette opération ajoute une [résumer](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) requête tooyour opérateur qui affiche les résultats de hello dans un graphique.  Vous pouvez regrouper sur plus d’une propriété, mais vous devez alors requête de hello tooedit directement.  Sélectionnez Bonjour menu enregistrement suivant hello Bonjour **ordinateur** et sélectionnez **Group by « Computer »**.  

![Regrouper par ordinateur](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Utiliser les résultats
portail de recherche de journal Hello possède un large éventail de fonctionnalités pour l’utilisation des résultats hello d’une requête.  Vous pouvez trier, filtrer et regrouper des données de hello de tooanalyze de résultats sans modifier la requête réelle de hello.  Les résultats d’une requête ne sont pas triés par défaut.

les données de salutation tooview sous forme de table qui fournit des options supplémentaires pour le filtrage et le tri, cliquez sur **Table**.  

![Vue Table](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Cliquez sur la flèche de hello par un enregistrement tooview les détails hello pour cet enregistrement.

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Pour trier sur un champ, cliquez sur son en-tête de colonne.

![Trier les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Filtrer les résultats de hello sur une valeur spécifique dans la colonne de hello en cliquant sur le bouton Filtrer hello et en fournissant une condition de filtre.

![Filtrer les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Regrouper sur une colonne en faisant glisser en haut de toohello des en-tête de colonne des résultats de hello.  Vous pouvez regrouper plusieurs champs en faisant glisser plusieurs colonnes toohello haut.

![Regrouper les résultats](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Utiliser des données de performances
Données de performances pour les agents Windows et Linux sont stockées dans hello Analytique de journal espace de travail hello **Perf** table.  Les enregistrements de performances ressemblent aux autres enregistrements, et nous pouvons écrire une requête simple qui retourne tous les enregistrements de performances, tout comme avec les événements.

```
Perf
```

![Données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Retourner plusieurs millions d’enregistrements pour tous les objets de performances et compteurs n’est cependant pas très utile.  Vous pouvez utiliser hello mêmes méthodes que vous utilisés au-dessus de données de hello toofilter ou simplement taper hello suivante de requête directement dans la zone de recherche de journal hello.  Cela retourne uniquement les enregistrements d’utilisation des processeurs pour les ordinateurs Windows et Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilisation des processeurs](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Cela limite hello données tooa des compteurs de performance, mais il reste ne placer dans un formulaire qui est particulièrement utile.  Vous pouvez afficher les données de salutation dans un graphique en courbes, mais devez toogroup par ordinateur et TimeGenerated.  toogroup sur plusieurs champs, vous devez les requêtes de hello toomodify directement, par conséquent, de modifier toohello éléments suivants de la requête hello.  Cette méthode utilise hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) fonction hello **CounterValue** valeur moyenne de propriété toocalculate hello sur chaque heure.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Graphique de données de performances](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Maintenant que les données de salutation sont regroupées convenablement, vous pouvez l’afficher dans un graphique visual en ajoutant hello [restituer](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) opérateur.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Graphique en courbes](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur le langage de requête Analytique de journal hello à [prise en main de hello Analytique Portal](https://go.microsoft.com/fwlink/?linkid=856079).
- Suivre un didacticiel à l’aide de hello [portal d’Analytique de Advanced](https://go.microsoft.com/fwlink/?linkid=856587) qui vous permet de toorun hello même des requêtes et des accès hello des mêmes données en tant que portail de recherche de journal hello.
