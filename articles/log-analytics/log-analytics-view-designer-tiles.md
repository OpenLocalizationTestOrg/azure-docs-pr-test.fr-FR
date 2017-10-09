---
title: "référence aaaTile pour le Concepteur de vue de l’Analytique des journaux OMS | Documents Microsoft"
description: "Concepteur de vue de l’Analytique de journal vous permet de toocreate personnalisé dans la console OMS hello des vues qui contiennent différentes visualisations de données dans le référentiel d’OMS hello. Cet article fournit une référence des paramètres hello pour chacun des toouse disponibles de hello vignettes dans vos affichages personnalisés."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Référence de la vignette Concepteur de vues de Log Analytics
Hello Concepteur de vue de l’Analytique de journal vous permet de toocreate personnalisé dans la console OMS hello des vues qui contiennent différentes visualisations de données dans le référentiel d’OMS hello. Cet article fournit une référence des paramètres hello pour chacun des toouse disponibles de hello vignettes dans vos affichages personnalisés.

Autres articles disponibles concernant le Concepteur de vues :

* [Afficher le concepteur](log-analytics-view-designer.md) -vue d’ensemble de hello Concepteur de vues et procédures pour créer et modifier des vues personnalisées.
* [Référence de partie de visualisation](log-analytics-view-designer-parts.md) -référence des paramètres hello pour chacun des hello vignettes toouse disponible dans vos affichages personnalisés.

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), alors les requêtes dans toutes les vues doivent être écrits dans hello [nouveau langage de requête](https://go.microsoft.com/fwlink/?linkid=856078).  Toutes les vues qui ont été créés avant de l’espace de travail hello a été mis à niveau seront automatiquement converti.

Hello tableau suivant répertorie hello différents types de vignettes disponibles dans hello Concepteur de vue.  les sections de Hello ci-dessous décrivent chaque type de détail et leurs propriétés.

| Vignette | Description |
|:--- |:--- |
| [Nombre](#number-tile) |Nombre unique indiquant le décompte des enregistrements retournés par une requête. |
| [Deux nombres](#two-numbers-tile) |Deux nombres uniques indiquant le décompte des enregistrements retournés par deux requêtes distinctes. |
| [Anneau](#donut-tile) |Graphique en anneau basé sur une requête avec une valeur de synthèse dans le centre de hello. |
| [Graphique en courbes et légende](#line-chart-amp-callout-tile) |Graphique en courbes basé sur une requête, et légende avec une valeur de synthèse. |
| [Graphique en courbes](#line-chart-tile) |Graphique en courbes basé sur une requête. |
| [Deux chronologies](#two-timelines-tile) |Histogramme avec deux séries basée chacune sur une requête distincte. |

## <a name="number-tile"></a>Vignette Nombre
Hello **nombre** vignette affiche un nombre unique indiquant le nombre hello d’enregistrements à partir d’une requête de journal et d’une étiquette.

![Vignette Nombre](media/log-analytics-view-designer/tile-number.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| **Vignette** | |
| Légende |Toodisplay de texte sous la valeur hello. |
| Interroger |Toorun de la requête.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="two-numbers-tile"></a>Vignette Deux nombres
Hello **nombre deux** vignette affiche deux nombres montrant le nombre hello d’enregistrements à partir d’une étiquette et les deux requêtes de journal différent pour chacun.

![Vignette Deux nombres](media/log-analytics-view-designer/tile-two-numbers.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| **Première vignette** | |
| Légende |Toodisplay de texte sous la valeur hello. |
| Interroger |Toorun de la requête.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| **Deuxième vignette** | |
| Légende |Toodisplay de texte sous la valeur hello. |
| Interroger |Toorun de la requête.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="donut-tile"></a>Vignette Anneau
Hello **anneau** vignette affiche un nombre unique récapitulée à partir d’une colonne de valeur dans une requête de journal.  anneau de Hello affiche graphiquement les résultats de trois principaux hello.

![Vignette Anneau](media/log-analytics-view-designer/tile-donut.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| **Anneau** | |
| Interroger |Toorun de requête pour l’anneau de hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé. |
| **Anneau** |**&gt; Centrer** |
| Texte |Toodisplay de texte sous la valeur hello à l’intérieur de hello anneau. |
| Opération |Bonjour tooperform opération hello valeur propriété toosummarize tooa seule valeur.<br><br>-Somme : Ajouter des valeurs de hello de tous les enregistrements avec la valeur de la propriété hello.<br>-Pourcentage : Pourcentage de valeurs hello additionnée à partir d’enregistrements avec toohello de valeur de propriété hello additionnées des valeurs de tous les enregistrements. |
| Valeurs de résultat utilisées dans l’opération relative au centre |Si vous le souhaitez cliquer hello signe tooadd une ou plusieurs valeurs.  des résultats de requête de hello Hello sera limité toorecords avec les valeurs de propriété hello que vous spécifiez.  Si aucune valeur n’est ajouté, que tous les enregistrements sont inclus dans la requête de hello. |
| **Anneau** |**&gt; Options supplémentaires** |
| Couleurs |Bonjour toodisplay de couleur pour chacun des trois propriétés de supérieur hello.  Si vous souhaitez toospecify couleurs pour les valeurs de propriété spécifiques, puis utilisez avancé le mappage de couleur. |
| Mappage avancé des couleurs |Affiche une couleur pour des valeurs de propriété spécifiques.  Si la valeur hello spécifiée est dans hello trois supérieur, puis une couleur différente hello s’affiche au lieu de couleurs standard de hello.  Si la propriété de hello n’est pas dans hello les trois premiers, puis les couleurs hello ne sont pas affichée. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="line-chart-tile"></a>Vignette Graphique en courbes
Hello **graphique en courbes** vignette affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal au fil du temps.  

![Vignette Graphique en courbes et légende](media/log-analytics-view-designer/tile-line-chart.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| **Graphique en courbes** | |
| Interroger |Toorun de requête pour le graphique en courbes hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé.  Si la requête de hello utilise hello **intervalle** (mot clé) puis hello axe des abscisses du graphique de hello utilisera cet intervalle de temps.  Si les requêtes hello n’incluent pas de hello **intervalle** intervalles (mot clé), puis toutes les heures sont utilisés pour hello axe des abscisses. |
| **Graphique en courbes** |**&gt; Axe des Y** |
| Utiliser l’échelle logarithmique |Sélectionnez toouse une échelle logarithmique pour hello axe des ordonnées. |
| Units |Spécifiez des unités hello pour les valeurs hello retournés par la requête de hello.  Ces informations sont utilisées toodisplay étiquettes sur graphique hello indiquant les types de valeur hello et éventuellement de convertir les valeurs de hello.  Hello **Type d’unité** spécifie la catégorie hello d’unité de hello et définit hello **Type d’unité en cours** valeurs qui sont disponibles.  Si vous sélectionnez une valeur dans **convertir** puis hello numérique sont converties à partir de hello **unité actuelle** type toohello **convertir** type. |
| Étiquette personnalisée |Toodisplay de texte pour l’étiquette suivante toohello hello axe des Y pour le type d’unité hello.  Si aucune étiquette n’est spécifié, seul le type hello unité s’affiche. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="line-chart--callout-tile"></a>Vignette Graphique en courbes et légende
Hello **& légende du graphique de ligne** vignette affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal dans le temps et une légende avec une valeur de synthèse.  

![Vignette Graphique en courbes et légende](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| **Graphique en courbes** | |
| Interroger |Toorun de requête pour le graphique en courbes hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé.  Si la requête de hello utilise hello **intervalle** (mot clé) puis hello axe des abscisses du graphique de hello utilisera cet intervalle de temps.  Si les requêtes hello n’incluent pas de hello **intervalle** intervalles (mot clé), puis toutes les heures sont utilisés pour hello axe des abscisses. |
| **Graphique en courbes** |**&gt; Légende** |
| Légende |Toodisplay de texte titre au-dessus de valeur de légende hello. |
| Nom de la série |Valeur de propriété pour toouse de série hello pour la valeur de légende hello.  Si aucune série n’est fourni, tous les enregistrements à partir de la requête de hello sont utilisées. |
| Opération |Bonjour tooperform opération sur hello valeur toosummarize tooa seule valeur de propriété de légende de hello.<br>-Moyenne : Moyenne valeur hello à partir de tous les enregistrements.<br><br>-Count : Nombre de tous les enregistrements retournés par la requête de hello.<br>-Dernier exemple : Valeur à partir de hello dernier intervalle inclus dans le graphique de hello.<br>-Max : Valeur maximale à partir des intervalles de salutation inclus dans le graphique de hello.<br>-Min : Valeur minimale à partir des intervalles de salutation inclus dans le graphique de hello.<br>-Somme : Sum valeur hello à partir de tous les enregistrements. |
| **Graphique en courbes** |**&gt; Axe des Y** |
| Utiliser l’échelle logarithmique |Sélectionnez toouse une échelle logarithmique pour hello axe des ordonnées. |
| Units |Spécifiez des unités hello pour les valeurs hello retournés par la requête de hello.  Ces informations sont utilisées toodisplay étiquettes sur graphique hello indiquant les types de valeur hello et éventuellement de convertir les valeurs de hello.  Hello **Type d’unité** spécifie la catégorie hello d’unité de hello et définit hello **Type d’unité en cours** valeurs qui sont disponibles.  Si vous sélectionnez une valeur dans **convertir** puis hello numérique sont converties à partir de hello **unité actuelle** type toohello **convertir** type. |
| Étiquette personnalisée |Toodisplay de texte pour l’étiquette suivante toohello hello axe des Y pour le type d’unité hello.  Si aucune étiquette n’est spécifié, seul le type hello unité s’affiche. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="two-timelines-tile"></a>Vignette Deux chronologies
Hello **deux chronologies** vignette affiche les résultats de hello deux requêtes de journal au fil du temps sous forme de graphiques de la colonne.  Une légende est affichée pour chaque série.  

![Vignette Deux chronologies](media/log-analytics-view-designer/tile-two-timelines.png)

| Paramètre | Description |
|:--- |:--- |
| Nom |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Description |Toodisplay de texte sous le nom de la vignette hello. |
| Premier graphique | |
| Légende |Toodisplay texte sous légende hello pour la première série de hello. |
| Couleur |Toouse de couleur pour les colonnes dans la première série de hello hello. |
| Requête de graphique |Toorun de requête pour la première série de hello.  nombre de Hello de hello enregistrements sur chaque intervalle de temps est représentée par les colonnes de graphique hello. |
| Opération |Bonjour tooperform opération sur hello valeur toosummarize tooa seule valeur de propriété de légende de hello.<br><br>-Moyenne : Moyenne valeur hello à partir de tous les enregistrements.<br>-Count : Nombre de tous les enregistrements retournés par la requête de hello.<br>-Dernier exemple : Valeur à partir de hello dernier intervalle inclus dans le graphique de hello.<br>-Max : Valeur maximale à partir des intervalles de salutation inclus dans le graphique de hello. |
| **Deuxième graphique** | |
| Légende |Toodisplay texte sous légende hello pour la deuxième série de hello. |
| Couleur |Toouse de couleur pour les colonnes hello dans la deuxième série de hello. |
| Requête de graphique |Toorun de requête pour la deuxième série de hello.  nombre de Hello de hello enregistrements sur chaque intervalle de temps est représentée par les colonnes de graphique hello. |
| Opération |Bonjour tooperform opération sur hello valeur toosummarize tooa seule valeur de propriété de légende de hello.<br><br>-Moyenne : Moyenne valeur hello à partir de tous les enregistrements.<br>-Count : Nombre de tous les enregistrements retournés par la requête de hello.<br>-Dernier exemple : Valeur à partir de hello dernier intervalle inclus dans le graphique de hello.<br>-Max : Valeur maximale à partir des intervalles de salutation inclus dans le graphique de hello. |
| **Avancée** |**&gt; Vérification du flux de données** |
| Activé |Sélectionnez si la vérification du flux de données doit être activée pour la vignette de hello.  Cela fournit un autre message si les données ne soient pas disponibles pour la vignette de hello.  Il s’agit généralement utilisée tooprovide un message période hello temporaire lorsque vue de hello est installé et que les données proviennent disponibles. |
| Interroger |Requête toorun toocheck si les données sont disponibles pour l’affichage de hello.  Si la requête de hello ne retourne aucun résultat, un message s’affiche au lieu de la valeur hello à partir de la requête principale de hello. |
| Message |Message toodisplay si la requête de vérification de flux de données hello ne retourne aucune donnée.  Si vous ne fournissez aucun message, le texte *Exécution de l'évaluation* s’affiche. |


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toosupport les requêtes de hello dans les vignettes.
* Ajouter [visualisation parties](log-analytics-view-designer-parts.md) tooyour une vue personnalisée.
