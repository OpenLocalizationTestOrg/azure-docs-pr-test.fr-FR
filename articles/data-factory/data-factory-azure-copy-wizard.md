---
title: aaaData Assistant copie de fabrique Azure | Documents Microsoft
description: "Découvrez comment toouse hello les données de toocopy Assistant copie de données fabrique Windows Azure à partir de toosinks des sources de données pris en charge."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Assistant Azure Data Factory Copy
Hello Assistant de copie de fabrique de données Azure facilite le processus hello de données de réception, qui est généralement une première étape dans un scénario d’intégration des données de bout en bout. Lorsque vous passez par hello Assistant de copie de fabrique de données Azure, il est inutile toounderstand toutes les définitions de JSON pour les services liés, les jeux de données et les pipelines. Hello crée automatiquement une données toocopy de pipeline à partir de destination sélectionné de toohello de source de données sélectionnée de hello. Hello Assistant copie de permet en outre, les données de salutation toovalidate étant ingérées au moment de hello de création. Cela fait gagner du temps, en particulier lorsque vous sont réception de données pour hello première fois à partir de la source de données hello. toostart hello Assistant Copier, cliquez sur hello **copier les données** vignette sur la page d’accueil hello votre fabrique de données.

![Assistant de copie](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Conception adaptée au Big Data
Cet Assistant vous permet de tooeasily déplacement des données à partir d’un large éventail de sources toodestinations en minutes. Une fois que vous parcourez l’Assistant de hello, un pipeline avec une activité de copie est automatiquement créé pour vous, ainsi que les entités de fabrique de données dépendantes (des services liés et jeux de données). Aucune étape supplémentaire n’est pipeline de hello toocreate requis.   

![Sélectionnez la source de données](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Pour obtenir des instructions toocreate exemples pipeline toocopy de données à partir d’une table de base de données SQL Azure tooan objets blob Azure, consultez hello [didacticiel de l’Assistant de copie](data-factory-copy-data-wizard-tutorial.md).
>
>

Assistant de Hello est conçu avec des données volumineuses en tenant compte du début de hello, avec prise en charge pour les types d’objets et données diverses. Vous pouvez créer des pipelines Data Factory capables de déplacer des centaines de dossiers, fichiers ou tables. Assistant de Hello prend en charge l’aperçu des données automatique, la capture du schéma et le mappage et le filtrage des données.

## <a name="automatic-data-preview"></a>Aperçu des données automatique
Vous pouvez afficher un aperçu faisant partie des données hello à partir de la source de données sélectionnée hello dans l’ordre toovalidate si les données de salutation sont ce que vous souhaitez toocopy. En outre, si la source de données hello est dans un fichier texte, hello Assistant copie d’analyse ligne hello toolearn du fichier de texte hello et de séparateurs de colonnes et de schéma automatiquement.

![Paramètres de format de fichier](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Mappage et capture de schéma
schéma Hello des données d’entrée peut correspondre pas de schéma de hello de données de sortie dans certains cas. Dans ce scénario, vous devez toomap des colonnes à partir de hello toocolumns de schéma source à partir du schéma de destination hello.

> [!TIP]
> Quand le copie de données à partir de SQL Server ou de la base de données SQL Azure dans l’entrepôt de données SQL Azure, si la table de hello n’existe pas dans la banque de destination hello, fabrique de données prennent en charge la création automatique de la table à l’aide du schéma de la source. En savoir plus à partir de [déplacer tooand de données à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).
>

Utilisez un tooselect de liste déroulante, une colonne à partir de la colonne de hello source schéma toomap tooa hello schéma de destination. Hello Assistant copie tente toounderstand votre modèle pour le mappage de colonne. Il s’applique hello même modèle toohello le reste de colonnes de hello, afin que vous n’avez pas besoin tooselect des colonnes de hello individuellement le mappage de schéma toocomplete hello. Si vous préférez, vous pouvez remplacer ces mappages à l’aide de colonnes de hello toomap hello listes déroulantes, une par une. modèle de Hello devient plus précis de mapper des colonnes. Hello Assistant copie de met continuellement à jour le modèle de hello et finalement atteint hello de modèle approprié pour la colonne hello mappage vous souhaitez tooachieve.     

![Mappage de schéma](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrage des données
Vous pouvez filtrer source données tooselect uniquement hello données nécessitant une banque de données de récepteur toohello toobe copié. Le filtrage de réduit le volume de hello de récepteur toohello copiés toobe hello de données magasin de données et par conséquent, améliore le débit de l’opération de copie hello hello. Il fournit des données toofilter moyen souple dans une base de données relationnelle à l’aide du langage de requête SQL hello ou les fichiers dans un dossier d’objets blob Azure à l’aide de [les variables et fonctions de Data Factory](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrage des données dans une base de données
Hello capture d’écran suivante montre une requête SQL à l’aide de hello `Text.Format` fonction et `WindowStart` variable.

![Valider des expressions](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrage des données dans un dossier d’objets blob Azure
Vous pouvez utiliser des variables dans les données de toocopy de chemin d’accès de dossier hello à partir d’un dossier qui est déterminé lors de l’exécution en fonction de [variables système](data-factory-functions-variables.md#data-factory-system-variables). les variables Hello pris en charge sont : **{year}**, **{mois}**, **{day}**, **{heure}**, **{minute}**, et **{personnalisé}**. Exemple : inputfolder/{year}/{month}/{day}.

Supposons que vous avez entrée dossiers Bonjour suivant le format :

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Cliquez sur hello **Parcourir** bouton **fichier ou dossier**, parcourir tooone de ces dossiers (par exemple, 2016 -> 03 -> 01 -> 02), puis cliquez sur **choisir**. Vous devez voir `2016/03/01/02` dans la zone de texte hello. À présent, remplacez **2016** avec **{year}**, **03** avec **{mois}**, **01** avec **{day}** , et **02** avec **{heure}**et appuyez sur hello **onglet** clé. Vous devez voir le format de hello tooselect de listes déroulantes pour ces quatre variables :

![Utilisation de variables système](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Comme indiqué dans hello suivant capture d’écran, vous pouvez également utiliser un **personnalisé** variable et les [pris en charge les chaînes de format](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect un dossier avec cette structure, utilisez hello **Parcourir** bouton tout d’abord. Remplacer une valeur avec **{personnalisé}**et appuyez sur hello **onglet** zone de texte hello toosee clé où vous pouvez taper la chaîne de format hello.     

![Utilisation de la variable custom](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Options de planification
Vous pouvez exécuter opération de copie hello qu’une seule fois ou selon une planification (horaire, quotidien, et ainsi de suite). Ces deux options utilisables pour la gamme de hello des connecteurs hello dans des environnements, notamment locaux et cloud copie bureau local.

Une opération de copie à usage unique permet le déplacement des données à partir d’une source de destination tooa qu’une seule fois. Il s’applique toodata de n’importe quelle taille et de n’importe quel format pris en charge. copie de Hello planifiée vous permet de toocopy données sur une périodicité prescrite. Vous pouvez utiliser les paramètres enrichis (par exemple, les nouvelles tentatives, délai d’attente et les alertes) tooconfigure hello planifiée copie.

![Propriétés de planification](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Étapes suivantes
Pour une procédure pas à pas rapide de l’utilisation de hello Assistant Copier les données fabrique toocreate un pipeline avec l’activité de copie, consultez [didacticiel : créer un pipeline à l’aide de hello Assistant copie de](data-factory-copy-data-wizard-tutorial.md).
