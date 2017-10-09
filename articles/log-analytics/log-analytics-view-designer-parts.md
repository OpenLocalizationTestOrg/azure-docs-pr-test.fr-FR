---
title: "référence aaaPart pour le Concepteur de vue de l’Analytique des journaux OMS | Documents Microsoft"
description: "Concepteur de vue de l’Analytique de journal vous permet de toocreate personnalisé dans la console OMS hello des vues qui contiennent différentes visualisations de données dans le référentiel d’OMS hello. Cet article fournit une référence des paramètres hello pour chacun des toouse disponibles des parties de visualisation hello dans vos affichages personnalisés."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Référence des composants de visualisation du Concepteur de vues de Log Analytics
Hello Concepteur de vue de l’Analytique de journal vous permet de toocreate des vues personnalisées dans la console OMS hello qui contiennent différentes visualisations de données à partir du référentiel d’OMS hello. Cet article fournit une référence des paramètres hello pour chacun des toouse disponibles des parties de visualisation hello dans vos affichages personnalisés.

Autres articles disponibles concernant le Concepteur de vues :

* [Afficher le concepteur](log-analytics-view-designer.md) -vue d’ensemble de hello Concepteur de vues et procédures pour créer et modifier des vues personnalisées.
* [Vignette référence](log-analytics-view-designer-tiles.md) -référence des paramètres hello pour chacun des hello vignettes toouse disponible dans vos affichages personnalisés.

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), alors les requêtes dans toutes les vues doivent être écrits dans hello [nouveau langage de requête](https://go.microsoft.com/fwlink/?linkid=856078).  Toutes les vues qui ont été créés avant de l’espace de travail hello a été mis à niveau seront automatiquement converti.

Hello tableau suivant décrit hello différents types de vignettes disponibles dans hello Concepteur de vue.  les sections de Hello ci-dessous décrivent chaque type de détail et leurs propriétés.

| Type de vue | Description |
|:--- |:--- |
| [Liste de requêtes](#list-of-queries-part) |Affiche une liste des requêtes de recherche dans le journal.  Hello utilisateur peut cliquer sur chaque toodisplay requête ses résultats. |
| [Nombre et liste](#number-amp-list-part) |L’en-tête affiche une valeur indiquant le nombre d’enregistrements obtenus à partir d’une requête de recherche dans le journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps. |
| [Deux nombres et liste](#two-numbers-amp-list-part) |L’en-tête affiche deux valeurs indiquant les nombres d’enregistrements obtenus à partir de requêtes de recherche distinctes dans le journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps. |
| [Anneau et liste](#donut-amp-list-part) |L’en-tête affiche un nombre résumé à partir d’une colonne de valeur dans une requête de journal.  anneau de Hello affiche graphiquement les résultats de trois principaux hello. |
| [Deux chronologies et liste](#two-timelines-amp-list-part) |En-tête affiche hello les résultats des requêtes de journal deux au fil du temps sous forme de graphiques de colonne avec une légende affichant un nombre unique résumés à partir d’une colonne de valeur dans une requête de journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps. |
| [Informations](#information-part) |L’en-tête affiche un texte statique et un lien facultatif.  La liste affiche un ou plusieurs éléments contenant un texte statique et un titre. |
| [Graphique en courbes, légende et liste](#line-chart-callout-amp-list-part) |L’en-tête affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal dans le temps, et une légende avec une valeur de synthèse.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps. |
| [Graphique en courbes et liste](#line-chart-amp-list-part) |L’en-tête affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal dans le temps.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps. |
| [Partie de pile de graphiques de courbes](#stack-of-line-charts-part) |Affiche trois graphiques en courbes distincts avec plusieurs séries à partir d’une requête de journal dans le temps. |

## <a name="list-of-queries-part"></a>Liste de parties de requêtes
Affiche une liste des requêtes de recherche dans le journal.  Hello utilisateur peut cliquer sur chaque toodisplay requête ses résultats.  affichage de Hello inclut une seule requête par défaut, et vous pouvez cliquer sur **+ requête** tooadd des requêtes supplémentaires.

![Liste de vues de requêtes](media/log-analytics-view-designer/view-list-queries.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Intitulé |Toodisplay de texte en haut de hello de vue de hello. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Filtres présélectionnés |Virgule liste délimitée par des tooinclude de propriétés dans le volet de gauche filtre hello lorsque l’utilisateur de hello sélectionne une requête. |
| Mode d’affichage |Vue initiale affichée lors de la requête de hello est sélectionnée.  Hello utilisateur sélectionne toutes les vues disponibles après l’ouverture de requête de hello. |
| **Requêtes** | |
| Requête de recherche |Toorun de la requête. |
| Nom convivial |Nom descriptif de l’utilisateur de toohello toodisplay hello requête. |

## <a name="number--list-part"></a>Nombre et composant de liste
L’en-tête affiche une valeur indiquant le nombre d’enregistrements obtenus à partir d’une requête de recherche dans le journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps.

![Liste de vues de requêtes](media/log-analytics-view-designer/view-number-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello de vue de hello. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **Titre** | |
| Légende |Toodisplay de texte en haut de hello d’en-tête de hello. |
| Interroger |Toorun de requête pour l’en-tête de hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  Bonjour tout d’abord deux propriétés de hello dix premiers enregistrements dans les résultats de hello sont affichées.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Les barres sont automatiquement créés en fonction de la valeur relative de hello de colonne numérique de hello.<br><br>Utilisez la commande de tri de hello dans les enregistrements de hello toosort hello requête dans la liste de hello.  Hello utilisateur peut cliquer sur Afficher tous les toorun hello interroger et retourner tous les enregistrements. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Séparateur de noms et de valeurs |Séparateur de caractère si vous souhaitez que la propriété en texte hello tooparse en plusieurs valeurs.  Consultez [Paramètres communs](#name-value-separator) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="two-numbers--list-part"></a>Deux nombres et composant de liste
L’en-tête affiche deux valeurs indiquant les nombres d’enregistrements obtenus à partir de requêtes de recherche distinctes dans le journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps.

![Deux nombres et affichage de liste](media/log-analytics-view-designer/view-two-numbers-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello de vue de hello. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **Titre** | |
| Légende |Toodisplay de texte en haut de hello d’en-tête de hello. |
| Interroger |Toorun de requête pour l’en-tête de hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  Bonjour tout d’abord deux propriétés de hello dix premiers enregistrements dans les résultats de hello sont affichées.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Les barres sont automatiquement créés en fonction de la valeur relative de hello de colonne numérique de hello.<br><br>Utilisez la commande de tri de hello dans les enregistrements de hello toosort hello requête dans la liste de hello.  Hello utilisateur peut cliquer sur Afficher tous les toorun hello interroger et retourner tous les enregistrements. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Opération |Tooperform d’opération pour le graphique sparkline de hello.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Séparateur de noms et de valeurs |Séparateur de caractère si vous souhaitez que la propriété en texte hello tooparse en plusieurs valeurs.  Consultez [Paramètres communs](#name-value-separator) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="donut--list-part"></a>Anneau et composant de liste
L’en-tête affiche un nombre résumé à partir d’une colonne de valeur dans une requête de journal.  anneau de Hello affiche graphiquement les résultats de trois principaux hello.

![Anneau et affichage de liste](media/log-analytics-view-designer/view-donut-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **En-tête** | |
| Intitulé |Toodisplay de texte en haut de hello d’en-tête de hello. |
| Sous-titre |Toodisplay texte sous hello titre en haut de hello d’en-tête de hello. |
| **Anneau** | |
| Interroger |Toorun de requête pour l’anneau de hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique. |
| **Anneau** |**&gt; Centrer** |
| Texte |Toodisplay de texte sous la valeur hello à l’intérieur de hello anneau. |
| Opération |Bonjour tooperform opération hello valeur propriété toosummarize tooa seule valeur.<br><br>-Somme : Ajouter des valeurs de hello de tous les enregistrements.<br>-Pourcentage : Pourcentage hello les enregistrements retournés par les valeurs hello dans **entraîner des valeurs utilisées dans le fonctionnement du centre** toohello nombre total d’enregistrements dans la requête de hello. |
| Valeurs de résultat utilisées dans l’opération relative au centre |Si vous le souhaitez cliquer hello signe tooadd une ou plusieurs valeurs.  des résultats de requête de hello Hello sera limité toorecords avec les valeurs de propriété hello que vous spécifiez.  Si aucune valeur n’est ajouté, tous les enregistrements sont inclus dans la requête de hello. |
| **Options supplémentaires** |**&gt; Couleurs** |
| Couleur 1<br>Couleur 2<br>Couleur 3 |Sélectionnez couleur hello hello de valeurs hello affiché dans l’anneau de hello. |
| **Options supplémentaires** |**&gt; Mappage avancé des couleurs** |
| Valeur du champ |Nom du type hello d’un champ de toodisplay sous la forme d’une couleur différente si elle est incluse dans l’anneau de hello. |
| Couleur |Sélectionnez la couleur hello pour un champ unique de hello. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Opération |Tooperform d’opération pour le graphique sparkline de hello.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Séparateur de noms et de valeurs |Séparateur de caractère si vous souhaitez que la propriété en texte hello tooparse en plusieurs valeurs.  Consultez [Paramètres communs](#name-value-separator) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="two-timelines--list-part"></a>Deux chronologies et composant de liste
En-tête affiche hello les résultats des requêtes de journal deux au fil du temps sous forme de graphiques de colonne avec une légende affichant un nombre unique résumés à partir d’une colonne de valeur dans une requête de journal.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps.

![Deux chronologies et affichage de liste](media/log-analytics-view-designer/view-two-timelines-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **Premier graphique<br>Deuxième graphique** | |
| Légende |Toodisplay texte sous légende hello pour la première série de hello. |
| Couleur |Toouse de couleur pour les colonnes hello dans la série de hello. |
| Interroger |Toorun de requête pour la première série de hello.  nombre de Hello de hello enregistrements sur chaque intervalle de temps est représentée par les colonnes de graphique hello. |
| Opération |Bonjour tooperform opération sur hello valeur toosummarize tooa seule valeur de propriété de légende de hello.<br><br>-Somme : Sum valeur hello à partir de tous les enregistrements.<br>-Moyenne : Moyenne valeur hello à partir de tous les enregistrements.<br>-Dernier exemple : Valeur à partir de hello dernier intervalle inclus dans le graphique de hello.<br>-Premier exemple : Valeur à partir de l’intervalle de première hello inclus dans le graphique de hello.<br>-Count : Nombre de tous les enregistrements retournés par la requête de hello. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Opération |Tooperform d’opération pour le graphique sparkline de hello.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="information-part"></a>Partie des informations
L’en-tête affiche un texte statique et un lien facultatif.  La liste affiche un ou plusieurs éléments contenant un texte statique et un titre.

![Vue Informations](media/log-analytics-view-designer/view-information.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Couleur |Couleur d’arrière-plan pour l’en-tête de hello. |
| **En-tête** | |
| Image |Toodisplay de fichier image dans l’en-tête de hello. |
| Étiquette |Toodisplay de texte dans l’en-tête de hello. |
| **En-tête** |**&gt; Lien** |
| Étiquette |Texte du lien. |
| Url |URL du lien. |
| **Éléments d’information** | |
| Intitulé |Toodisplay de texte du titre de chaque élément. |
| Contenu |Toodisplay de texte pour chaque élément. |

## <a name="line-chart-callout--list-part"></a>Graphique en courbes, légende et composant de liste
L’en-tête affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal dans le temps, et une légende avec une valeur de synthèse.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps.

![Graphique en courbes, légende et affichage de liste](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **En-tête** | |
| Intitulé |Toodisplay de texte en haut de hello d’en-tête de hello. |
| Sous-titre |Toodisplay texte sous hello titre en haut de hello d’en-tête de hello. |
| **Graphique en courbes** | |
| Interroger |Toorun de requête pour le graphique en courbes hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé.  Si la requête de hello utilise hello **intervalle** (mot clé) puis hello axe des abscisses du graphique de hello utilisera cet intervalle de temps.  Si les requêtes hello n’incluent pas de hello **intervalle** intervalles (mot clé), puis toutes les heures sont utilisés pour hello axe des abscisses. |
| **Graphique en courbes** |**&gt; Légende** |
| Titre de la légende |Toodisplay texte au-dessus de valeur de légende hello. |
| Nom de la série |Valeur de propriété pour toouse de série hello pour la valeur de légende hello.  Si aucune série n’est fourni, tous les enregistrements à partir de la requête de hello sont utilisées. |
| Opération |Bonjour tooperform opération sur hello valeur toosummarize tooa seule valeur de propriété de légende de hello.<br><br>-Moyenne : Moyenne valeur hello à partir de tous les enregistrements.<br>-Nombre de tous les enregistrements retournés par la requête de hello.<br>-Dernier exemple : Valeur à partir de hello dernier intervalle inclus dans le graphique de hello.<br>-Max : Valeur maximale à partir des intervalles de salutation inclus dans le graphique de hello.<br>-Min : Valeur minimale à partir des intervalles de salutation inclus dans le graphique de hello.<br>-Somme : Sum valeur hello à partir de tous les enregistrements. |
| **Graphique en courbes** |**&gt; Axe des Y** |
| Utiliser l’échelle logarithmique |Sélectionnez toouse une échelle logarithmique pour hello axe des ordonnées. |
| Units |Spécifiez des unités hello pour les valeurs hello retournés par la requête de hello.  Ces informations sont utilisées toodisplay étiquettes sur graphique hello indiquant les types de valeur hello et éventuellement de convertir les valeurs de hello.  Hello Type d’unité spécifie la catégorie hello d’unité de hello et définit des valeurs de Type d’unité actuelle hello qui sont disponibles.  Si vous sélectionnez une valeur numérique Convert-toothen-Bonjour les valeurs sont converties à partir de hello unité actuelle type toohello Convert tootype. |
| Étiquette personnalisée |Toodisplay de texte pour l’étiquette suivante toohello hello axe des Y pour le type d’unité hello.  Si aucune étiquette n’est spécifié, seul le type hello unité s’affiche. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Opération |Tooperform d’opération pour le graphique sparkline de hello.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Séparateur de noms et de valeurs |Séparateur de caractère si vous souhaitez que la propriété en texte hello tooparse en plusieurs valeurs.  Consultez [Paramètres communs](#name-value-separator) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="line-chart--list-part"></a>Graphique en courbes et composant de liste
L’en-tête affiche un graphique en courbes avec plusieurs séries à partir d’une requête de journal dans le temps.  Liste affiche hello dix meilleurs résultats à partir d’une requête avec un graphique indiquant la valeur relative de hello d’une colonne numérique ou de sa modification dans le temps.

![Affichage graphique et vue liste](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| Icône Utiliser |Sélectionnez l’affichage de l’icône toohave hello. |
| **En-tête** | |
| Intitulé |Toodisplay de texte en haut de hello d’en-tête de hello. |
| Sous-titre |Toodisplay texte sous hello titre en haut de hello d’en-tête de hello. |
| **Graphique en courbes** | |
| Interroger |Toorun de requête pour le graphique en courbes hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé.  Si la requête de hello utilise hello **intervalle** (mot clé) puis hello axe des abscisses du graphique de hello utilisera cet intervalle de temps.  Si les requêtes hello n’incluent pas de hello **intervalle** intervalles (mot clé), puis toutes les heures sont utilisés pour hello axe des abscisses. |
| **Graphique en courbes** |**&gt; Axe des Y** |
| Utiliser l’échelle logarithmique |Sélectionnez toouse une échelle logarithmique pour hello axe des ordonnées. |
| Units |Spécifiez des unités hello pour les valeurs hello retournés par la requête de hello.  Ces informations sont utilisées toodisplay étiquettes sur graphique hello indiquant les types de valeur hello et éventuellement de convertir les valeurs de hello.  Hello Type d’unité spécifie la catégorie hello d’unité de hello et définit des valeurs de Type d’unité actuelle hello qui sont disponibles.  Si vous sélectionnez une valeur numérique Convert-toothen-Bonjour les valeurs sont converties à partir de hello unité actuelle type toohello Convert tootype. |
| Étiquette personnalisée |Toodisplay de texte pour l’étiquette suivante toohello hello axe des Y pour le type d’unité hello.  Si aucune étiquette n’est spécifié, seul le type hello unité s’affiche. |
| **Liste** | |
| Interroger |Toorun de requête pour la liste hello.  nombre de Hello de hello enregistrements retournés par la requête de hello s’affiche. |
| Masquer le graphique |Sélectionnez toodisable hello graphique toohello droite de la colonne numérique de hello. |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Couleur |Couleur des barres de hello ou des graphiques sparkline. |
| Opération |Tooperform d’opération pour le graphique sparkline de hello.  Consultez [Paramètres communs](#sparklines) pour plus d’informations. |
| Séparateur de noms et de valeurs |Séparateur de caractère si vous souhaitez que la propriété en texte hello tooparse en plusieurs valeurs.  Consultez [Paramètres communs](#name-value-separator) pour plus d’informations. |
| Requête de navigation |Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Consultez [Paramètres communs](#navigation-query) pour plus d’informations. |
| **Liste** |**&gt; Titres des colonnes** |
| Nom |Toodisplay de texte en haut de hello de hello première colonne de liste de hello. |
| Valeur |Toodisplay texte haut hello hello deuxième colonne de liste de hello. |
| **Liste** |**&gt; Seuils** |
| Activer les seuils |Sélectionnez tooenable seuils.  Consultez [Paramètres communs](#thresholds) pour plus d’informations. |

## <a name="stack-of-line-charts-part"></a>Partie de pile de graphiques de courbes
Affiche trois graphiques en courbes distincts avec plusieurs séries à partir d’une requête de journal dans le temps.

![Pile de graphiques en courbes](media/log-analytics-view-designer/view-stack-line-charts.png)

| Paramètre | Description |
|:--- |:--- |
| **Généralités** | |
| Titre du groupe |Toodisplay de texte en haut de hello Hello disposer en mosaïque. |
| Nouveau groupe |Sélectionnez toocreate un nouveau groupe dans l’affichage de hello en commençant à l’affichage actuel de hello. |
| Icône |Image du fichier toodisplay toohello résultat suivant dans l’en-tête de hello. |
| **Graphique 1<br>Graphique 2<br>Graphique 3** |**&gt; En-tête** |
| Intitulé |Toodisplay de texte en haut de hello du graphique de hello. |
| Sous-titre |Toodisplay texte sous hello titre en haut de hello du graphique de hello. |
| **Graphique 1<br>Graphique 2<br>Graphique 3** |**Graphique en courbes** |
| Interroger |Toorun de requête pour le graphique en courbes hello.  propriété de première Hello doit être une texte valeur hello deuxième propriété et une valeur numérique.  Il s’agit généralement d’une requête qui utilise hello **mesure** résultats toosummarize de mot clé.  Si la requête de hello utilise hello **intervalle** (mot clé) puis hello axe des abscisses du graphique de hello utilisera cet intervalle de temps.  Si les requêtes hello n’incluent pas de hello **intervalle** intervalles (mot clé), puis toutes les heures sont utilisés pour hello axe des abscisses. |
| **Graphique** |**&gt; Axe des Y** |
| Utiliser l’échelle logarithmique |Sélectionnez toouse une échelle logarithmique pour hello axe des ordonnées. |
| Units |Spécifiez des unités hello pour les valeurs hello retournés par la requête de hello.  Ces informations sont utilisées toodisplay étiquettes sur graphique hello indiquant les types de valeur hello et éventuellement de convertir les valeurs de hello.  Hello Type d’unité spécifie la catégorie hello d’unité de hello et définit des valeurs de Type d’unité actuelle hello qui sont disponibles.  Si vous sélectionnez une valeur numérique Convert-toothen-Bonjour les valeurs sont converties à partir de hello unité actuelle type toohello Convert tootype. |
| Étiquette personnalisée |Toodisplay de texte pour l’étiquette suivante toohello hello axe des Y pour le type d’unité hello.  Si aucune étiquette n’est spécifié, seul le type hello unité s’affiche. |

## <a name="common-settings"></a>Paramètres courants
Hello les sections suivantes décrire des parties de visualisation tooseveral paramètres communes.

### <a name="name-value-separator">Séparateur de noms et de valeurs</a>
Séparateur de caractère si vous souhaitez que les propriétés de texte hello tooparse à partir d’une requête de liste en plusieurs valeurs.  Si vous spécifiez un délimiteur, vous pouvez fournir des noms pour chaque champ séparé par hello même délimiteur dans la zone de nom hello.

Par exemple, imaginez une propriété appelée *Location* incluant des valeurs telles que *Redmond-Building 41* et *Bellevue-Building12*.  Vous pouvez spécifier – pour hello nom & séparateur de valeur et *City-Building* pour hello nom.  Chaque valeur est alors analysée en deux propriétés respectivement nommées *City* et *Building*.

### <a name="navigation-query">Requête de navigation</a>
Interroger toorun lors de l’utilisateur de hello sélectionne un élément dans la liste de hello.  Utilisez *{sélectionnée}* syntaxe hello tooinclude élément hello sélectionné par l’utilisateur.

Par exemple, si hello requête possède une colonne appelée *ordinateur* et requête de navigation hello est *{sélectionnée}*, une requête comme *ordinateur = « Monordinateur »* doit être exécuté lorsque l’utilisateur Hello sélectionné un ordinateur.  Si la requête de navigation hello est *Type = Event {sélectionnée}* puis des requêtes hello *Type = ordinateur de l’événement = « Monordinateur »* doit être exécuté.

### <a name="sparklines">Sparklines</a>
Un graphique sparkline est un petit graphique en courbes qui illustre hello de la valeur d’une entrée de liste au fil du temps.  Pour les parties de la visualisation avec une liste, vous pouvez sélectionner si toodisplay une barre indiquant horizontale hello valeur relative d’une colonne numérique ou un graphique sparkline indiquant sa valeur au fil du temps.

Hello tableau suivant décrit les paramètres de hello pour les graphiques sparkline.

| Paramètre | Description |
|:--- |:--- |
| Activation des sparklines |Sélectionnez le graphique sparkline de toodisplay au lieu de la barre horizontale. |
| Opération |Si les graphiques sparkline sont activés, il s’agit de tooperform d’opération hello sur chaque propriété de valeurs de hello liste toocalculate hello pour le graphique sparkline de hello.<br><br>-Dernier exemple : La dernière valeur de série de hello sur intervalle de temps hello.<br>-Max : Valeur maximale série hello sur intervalle de temps hello.<br>-Min : Valeur minimale série hello sur intervalle de temps hello.<br>-Somme : Sum des valeurs de séries hello sur intervalle de temps hello.<br>-Résumé : Utilise hello même commande mesure en tant que requête hello dans l’en-tête de hello. |

### <a name="thresholds">Seuils</a>
Seuils permettent de toodisplay un élément de tooeach suivant icône de couleur dans une liste, ce qui vous donne un indicateur visuel rapide d’éléments dépasse une valeur particulière ou est comprise dans une plage particulière.  Par exemple, vous pouvez afficher une icône verte pour les éléments avec une valeur acceptable, jaune, si la valeur de hello se trouve dans une plage qui indique un avertissement et le rouge si elle dépasse une valeur d’erreur.

Lorsque vous activez des seuils pour une partie, vous devez spécifier un ou plusieurs seuils.  Si la valeur hello d’un élément est supérieur à une valeur de seuil et inférieure à la valeur de seuil suivante hello, cette couleur est utilisée.  Si l’élément de hello est supérieure à la valeur de seuil puis la plus élevée, cette couleur est définie.   

Chaque ensemble de seuils a un seuil avec la valeur **par défaut**.  Il s’agit de couleur hello si aucune autre valeur n’est dépassé.  Vous pouvez ajouter ou supprimer des seuils en cliquant sur hello  **+**  ou **x** bouton.

Hello tableau suivant décrit les paramètres de hello pour les seuils.

| Paramètre | Description |
|:--- |:--- |
| Activer les seuils |Sélectionnez toodisplay qu'une toohello icône de couleur à gauche de chaque valeur qui indique les seuils de toospecified relatif intégrité. |
| Nom |Valeur de seuil de nom tooidentify hello. |
| Seuil |Valeur de seuil de hello.  couleur de contrôle d’intégrité Hello pour chaque élément de liste a la valeur couleur toohello hello plus élevé de valeur de seuil dépassé par la valeur de l’élément hello.  Il existe un seuil par défaut qui est la couleur de hello si aucune valeur de seuil n’est atteint. |
| Couleur |Couleur de la valeur de seuil hello. |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toosupport les requêtes de hello dans les parties de visualisation.
