---
title: "données aaaCopy facilement avec l’Assistant copie - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello les données de toocopy Assistant de copie de fabrique de données à partir de toosinks des sources de données pris en charge."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Copier ou déplacer facilement des données avec l’Assistant de copie Azure Data Factory
Hello Assistant de copie de fabrique de données Azure consiste à tooease hello de données de réception, qui est généralement une première étape dans un scénario d’intégration des données de bout en bout. Lorsque vous passez par hello Assistant de copie de fabrique de données Azure, il est inutile toounderstand toutes les définitions de JSON pour les pipelines, les datasets et les services liés. Toutefois, après avoir effectué toutes les étapes de hello dans l’Assistant de hello, Assistant de hello crée automatiquement une données toocopy de pipeline à partir de destination sélectionné de toohello de source de données sélectionnée de hello. En outre, hello copie Assistant vous aide à toovalidate les données de salutation étant ingérées au moment de hello de création, qui permet d’économiser beaucoup de temps, en particulier lorsque vous sont réception de données pour hello première fois à partir de la source de données hello. toostart hello Assistant Copier, cliquez sur hello **copier les données** vignette sur la page d’accueil hello votre fabrique de données.

![Assistant de copie](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Un Assistant intuitif pour copier des données
Cet Assistant vous permet de tooeasily déplacement des données à partir d’un large éventail de sources toodestinations en minutes. Après avoir effectué l’Assistant de hello, un pipeline avec une activité de copie est automatiquement créé pour vous, ainsi que les entités de fabrique de données dépendantes (des services liés et des groupes de données). Aucune étape supplémentaire n’est pipeline de hello toocreate requis.   

![Sélectionnez la source de données](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Consultez [didacticiel de l’Assistant copie](data-factory-copy-data-wizard-tutorial.md) article pour obtenir des instructions toocreate exemples pipeline toocopy de données à partir d’une table de base de données SQL Azure tooan objets blob Azure. 
> 
> 

Assistant de Hello est conçu avec des données volumineuses en tenant compte du début de hello. Il s’agit des pipelines de fabrique de données tooauthor simple et efficace qui déplacent des centaines de dossiers, des fichiers ou des tables à l’aide de l’Assistant de données de la copie hello. Hello Assistant prend en charge hello suivant trois fonctionnalités : aperçu des données automatique, la capture du schéma et le mappage et le filtrage des données. 

## <a name="automatic-data-preview"></a>Aperçu des données automatique
Assistant copie de Hello permet de vous tooreview partie des données de hello de hello sélectionné source de données pour vous toovalidate si les données que vous souhaitez toocopy droit hello données hello. En outre, si la source de données hello est dans un fichier texte, Assistant copie de hello analyse ligne toolearn du fichier de texte hello et de séparateurs de colonnes et de schéma automatiquement. 

![Paramètres de format de fichier](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Mappage et capture de schéma
schéma Hello des données d’entrée peut correspondre pas de schéma de hello de données de sortie dans certains cas. Dans ce scénario, vous devez toomap des colonnes à partir de hello toocolumns de schéma source à partir du schéma de destination hello. 

Assistant copie de Hello mappe automatiquement les colonnes de toocolumns de schéma source hello hello schéma de destination. Vous pouvez remplacer les mappages hello à l’aide des listes déroulantes de hello (ou) spécifiez si une colonne doit toobe ignorée lors de la copie des données de salutation.   

![Mappage de schéma](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrage des données
Assistant de Hello vous permet de toofilter source tooselect uniquement hello données nécessitant une banque de données de destination/récepteur toohello toobe copié. Le filtrage de réduit le volume de hello de récepteur toohello copiés toobe hello de données magasin de données et par conséquent, améliore le débit de l’opération de copie hello hello. Il fournit une données toofilter de manière flexible dans une base de données relationnelle à l’aide de SQL query language (ou) les fichiers dans un dossier d’objets blob Azure à l’aide de [les variables et fonctions de Data Factory](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrage des données dans une base de données
Dans l’exemple de hello, la requête SQL hello utilise hello `Text.Format` fonction et `WindowStart` variable. 

![Valider des expressions](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrage des données dans un dossier d’objets blob Azure
Vous pouvez utiliser des variables dans les données de toocopy de chemin d’accès de dossier hello à partir d’un dossier qui est déterminé lors de l’exécution en fonction de [variables système](data-factory-functions-variables.md#data-factory-system-variables). les variables Hello pris en charge sont : **{year}**, **{mois}**, **{day}**, **{heure}**, **{minute}**, et **{personnalisé}**. Exemple : inputfolder/{year}/{month}/{day}.

Supposons que vous avez entrée dossiers Bonjour suivant le format :

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Cliquez sur hello **Parcourir** bouton **fichier ou dossier**, parcourir tooone de ces dossiers (par exemple, 2016 -> 03 -> 01 -> 02), puis cliquez sur **choisir**. Vous devez voir `2016/03/01/02` dans la zone de texte hello. À présent, remplacez **2016** par **{year}**, **03** par **{month}**, **01** par **{day}** et **02** par **{hour}**, puis appuyez sur la touche de tabulation. Vous devez voir le format de hello tooselect de listes déroulantes pour ces quatre variables :

![Utilisation de variables système](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Comme indiqué dans hello suivant capture d’écran, vous pouvez également utiliser un **personnalisé** variable et les [pris en charge les chaînes de format](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect un dossier avec cette structure, utilisez hello **Parcourir** bouton tout d’abord. Remplacer une valeur avec **{personnalisé}**, puis appuyez sur la zone de texte hello toosee onglet où vous pouvez taper la chaîne de format hello.     

![Utilisation de la variable custom](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Prise en charge de divers types d’objet et de données
À l’aide d’Assistant copie de hello, vous pouvez efficacement déplacer des centaines de tables, des fichiers ou dossiers.

![Sélectionner les tables à partir de quelles données toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Options de planification
Vous pouvez exécuter opération de copie hello qu’une seule fois ou selon une planification (horaire, quotidien, et ainsi de suite). Ces deux options peuvent servir à transversales hello des connecteurs de hello sur locaux et cloud copie bureau local.

Une opération de copie à usage unique permet le déplacement des données à partir d’une source de destination tooa qu’une seule fois. Il s’applique toodata de n’importe quelle taille et de n’importe quel format pris en charge. copie de Hello planifiée vous permet de toocopy données sur une périodicité prescrite. Vous pouvez utiliser les paramètres enrichis (par exemple, les nouvelles tentatives, délai d’attente et les alertes) tooconfigure hello planifiée copie.

![Propriétés de planification](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Étapes suivantes
Pour une procédure pas à pas rapide de l’utilisation de hello Assistant Copier les données fabrique toocreate un pipeline avec l’activité de copie, consultez [didacticiel : créer un pipeline à l’aide de hello Assistant copie de](data-factory-copy-data-wizard-tutorial.md).

