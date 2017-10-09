---
title: "aaaCreate consulte des données de tooanalyze dans Analytique des journaux OMS | Documents Microsoft"
description: "Concepteur de vue de l’Analytique de journal vous permet de toocreate personnalisé des vues qui sont affichés dans le portail d’OMS et Azure hello et contiennent différentes visualisations de données dans le référentiel d’OMS hello. Cet article contient une présentation du Concepteur de vues et des procédures de création et modification des vues personnalisées."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Utilisez des vues personnalisées du Concepteur de vue toocreate dans Analytique de journal
Hello Concepteur de vues dans [Analytique de journal](log-analytics-overview.md) vous permet de toocreate des vues personnalisées dans la console OMS hello qui contiennent différentes visualisations de données dans le référentiel d’OMS hello. Cet article contient une présentation du Concepteur de vues et des procédures de création et modification des vues personnalisées.

Autres articles disponibles concernant le Concepteur de vues :

* [Vignette référence](log-analytics-view-designer-tiles.md) -référence des paramètres hello pour chacun des hello vignettes toouse disponible dans vos affichages personnalisés.
* [Référence de partie de visualisation](log-analytics-view-designer-parts.md) -référence des paramètres hello pour chacun des hello vignettes toouse disponible dans vos affichages personnalisés.

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), alors les requêtes dans toutes les vues doivent être écrits dans hello [nouveau langage de requête](https://go.microsoft.com/fwlink/?linkid=856078).  Toutes les vues qui ont été créés avant de l’espace de travail hello a été mis à niveau seront automatiquement converti.

## <a name="concepts"></a>Concepts
Les vues créées par hello Concepteur de vue de contient des éléments de hello Bonjour tableau suivant.

| Partie | Description |
|:--- |:--- |
| Vignette |Affiche le tableau de bord de vue d’ensemble Analytique de journal principal hello.  Inclut une synthèse visual informations hello hello affichage personnalisé.  Les différents types de vignette fournissent des visualisations différentes d’enregistrements dans le référentiel d’OMS hello.  Cliquez sur hello hello tooopen de vignette vue personnalisée. |
| Vue personnalisée |Affichée lorsque l’utilisateur de hello clique sur hello vignette.  Contient un ou plusieurs composants de visualisation. |
| Composants de visualisation |Visualisation des données dans le référentiel d’OMS hello basé sur un ou plusieurs [recherche de journal](log-analytics-log-searches.md).  La plupart des composants inclut un en-tête qui fournit une visualisation de haut niveau et une liste de résultats principaux de hello.  Types de l’autre partie fournissent différentes visualisations d’enregistrements dans le référentiel d’OMS hello.  Cliquez sur les éléments dans hello partie tooperform une recherche de journal en fournissant des rapports détaillés. |

![Vue d’ensemble du concepteur](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Ajouter l’espace de travail du Concepteur de vue tooyour
Alors que le Concepteur de vue est en version préliminaire, vous devez l’ajouter tooyour espace de travail en sélectionnant **fonctionnalités en version préliminaire** Bonjour **paramètres** section du portail OMS de hello.

![Activer la version préliminaire](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Création et modification de vues
### <a name="create-a-new-view"></a>Créer une vue
Ouvrez une nouvelle vue Bonjour **Concepteur de vue** en cliquant sur hello Concepteur de vue de vignette dans le tableau de bord OMS principal hello.

![Vignette Concepteur de vues](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Modifier une vue
tooedit une vue existante dans le Concepteur de vue, vue hello ouvrir en cliquant sur sa vignette dans le tableau de bord OMS principal hello de hello.  Puis cliquez sur hello **modifier** bouton vue de hello tooopen Bonjour Concepteur de vue.

![Modifier une vue](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Cloner une vue
Lorsque vous clonez une vue, il crée une nouvelle vue et s’ouvre dans hello Concepteur de vue.  nouvelle vue de Hello aura hello comme hello d’origine avec « Copie » ajouté toohello fin du même nom.  tooclone une vue, ouvre hello vue existante en cliquant sur sa vignette dans le tableau de bord OMS principal hello.  Puis cliquez sur hello **Clone** bouton vue de hello tooopen Bonjour Concepteur de vue.

![Cloner une vue](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Supprimer une vue
toodelete une vue existante, vue hello ouvrir en cliquant sur sa vignette dans le tableau de bord OMS principal hello.  Puis cliquez sur hello **modifier** bouton vue de hello tooopen Bonjour Concepteur de vue, puis cliquez sur **supprimer l’affichage**.

![Supprimer une vue](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Exporter une vue
Vous pouvez exporter un fichier JSON de tooa de vue que vous pouvez importer dans un autre espace de travail ou l’utiliser dans un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport une vue existante, vue hello ouvrir en cliquant sur sa vignette dans le tableau de bord OMS principal hello.  Puis cliquez sur hello **exporter** bouton toocreate un fichier dans le dossier de téléchargement du navigateur hello.  Hello nom des fichiers de hello doit être nom hello de vue hello avec l’extension de hello *omsview*.

![Exporter une vue](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importer une vue
Vous pouvez importer un fichier *omsview* que vous avez exporté à partir d’un autre groupe d’administration.  tooimport un affichage existant, d’abord créer une nouvelle vue.  Puis cliquez sur hello **importation** bouton et sélectionnez hello *omsview* fichier.  configuration Hello dans le fichier de hello sera copiée dans la vue existante de hello.

![Exporter une vue](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Utilisation du Concepteur de vues
Hello Concepteur de vue comporte trois volets.  Hello **conception** volet représente une vue personnalisée hello.  Lorsque vous ajoutez des vignettes et des parties de hello **contrôle** volet toohello **conception** volet qu’ils sont ajoutés toohello vue.  Hello **propriétés** volet affiche les propriétés de hello pour les mosaïques hello ou une partie sélectionnée.

![Concepteur de vues](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Vignette Configurer la vue
Un vue personnalisée ne peut avoir qu’une seule vignette.  Sélectionnez hello **vignette** onglet Bonjour **contrôle** volet tooview hello actuel vignette ou sélectionnez-en un autre.  Hello **propriétés** volet affiche les propriétés de hello pour la mosaïque de hello en cours.  Configurer les propriétés des mosaïques hello selon toohello détails Bonjour [vignette de référence](log-analytics-view-designer-tiles.md) et cliquez sur **appliquer** toosave modifications.

### <a name="configure-visualization-parts"></a>Configurer les composants de visualisation
Une vue peut inclure une nombre quelconque de composants de visualisation.  Sélectionnez hello **vue** onglet, puis une visualisation partie tooadd toohello vue.  Hello **propriétés** volet affiche les propriétés de hello pour la partie de hello sélectionné.  Configurer l’affichage de hello propriétés selon toohello détails Bonjour [référence de partie de visualisation](log-analytics-view-designer-parts.md) et cliquez sur **appliquer** toosave modifications.

### <a name="delete-a-visualization-part"></a>Supprimer un composant de visualisation
Vous pouvez supprimer une partie de la visualisation de hello vue en cliquant sur hello **X** bouton hello coin supérieur droit de la partie de hello.

### <a name="rearrange-visualization-parts"></a>Réorganiser les composants de visualisation
Les vues ne comprennent qu’une seule ligne de composants de visualisation.  Réorganiser les articles existants dans un affichage en cliquant et en faisant glisser tooa un nouvel emplacement.

## <a name="next-steps"></a>Étapes suivantes
* Ajouter [vignettes](log-analytics-view-designer-tiles.md) tooyour une vue personnalisée.
* Ajouter [visualisation parties](log-analytics-view-designer-parts.md) tooyour une vue personnalisée.
