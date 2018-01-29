---
title: Assistant Azure Data Factory Copy | Microsoft Docs
description: "Découvrez comment utiliser l’Assistant Azure Data Factory Copy pour copier des données à partir de sources de données prises en charge dans des récepteurs."
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
ms.date: 01/22/2018
ms.author: spelluru
robots: noindex
ms.openlocfilehash: d9f3fea0db5a08fc91d9e4dc525b48575c512634
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory-copy-wizard"></a>Assistant Azure Data Factory Copy
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). 

L’Assistant Azure Data Factory Copy facilite le processus de réception des données, qui est généralement la première étape dans un scénario d’intégration des données de bout en bout. Lorsque vous passez par l’Assistant Azure Data Factory Copy, vous n’avez pas besoin de comprendre les définitions JSON pour les services liés, les jeux de données et les pipelines. L’Assistant crée automatiquement un pipeline pour copier les données de la source de données sélectionnée vers la destination sélectionnée. En outre, l’Assistant de copie vous permet de valider les données en cours de réception au moment de la création. Cela vous permet de gagner du temps, surtout lorsque vous réceptionnez des données pour la première fois à partir de la source de données. Pour lancer l’Assistant Data Factory Copy, cliquez sur la mosaïque **Copier les données** sur la page d’accueil de votre fabrique de données.

![Assistant de copie](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Conception adaptée au Big Data
Cet Assistant vous permet de déplacer facilement et en quelques minutes des données provenant de nombreuses sources différentes vers des destinations. Une fois que vous avez utilisé l’Assistant, un pipeline avec une activité de copie est automatiquement créée, ainsi que des entités Data Factory dépendantes (services et jeux de données liés). Aucune étape supplémentaire n’est nécessaire pour créer le pipeline.   

![Sélectionnez la source de données](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Consultez le [didacticiel sur l’Assistant de copie](data-factory-copy-data-wizard-tutorial.md) pour obtenir des instructions détaillées sur la création d’un exemple de pipeline afin de copier des données d’un objet blob Azure vers une table Azure SQL Database.
>
>

La conception de l’Assistant est particulièrement adaptée au Big Data, avec la prise en charge de divers types d’objet et de données. Vous pouvez créer des pipelines Data Factory capables de déplacer des centaines de dossiers, fichiers ou tables. L’Assistant prend en charge l’aperçu des données automatique, la capture et le mappage de schéma, ainsi que le filtrage des données.

## <a name="automatic-data-preview"></a>Aperçu des données automatique
Vous pouvez afficher un aperçu d’une partie des données à partir de la source de données sélectionnée afin de vérifier si les données correspondent à ce que vous voulez copier. En outre, si les données sources sont contenues dans un fichier texte, l’Assistant de copie analyse ce fichier pour découvrir automatiquement les délimiteurs de colonnes et de lignes ainsi que le schéma.

![Paramètres de format de fichier](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Mappage et capture de schéma
Le schéma des données d’entrée peut ne pas correspondre au schéma des données de sortie dans certains cas. Le cas échéant, vous devez mapper les colonnes du schéma source aux colonnes du schéma de destination.

> [!TIP]
> Lors de la copie de données à partir de SQL Server ou d’Azure SQL Data Warehouse vers Azure SQL Data Warehouse, si la table n’existe pas dans le magasin de destination, Data Factory prend en charge la création automatique de la table à l’aide du schéma de la source. Pour en savoir plus, consultez la rubrique [Déplacer des données vers et depuis Azure SQL Data Warehouse à l’aide d’Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).
>

Utilisez une liste déroulante pour sélectionner une colonne du schéma source à mapper à une colonne du schéma de destination. L’Assistant de copie essaie de comprendre votre modèle de mappage des colonnes. Le même modèle est appliqué aux autres colonnes, ce qui vous évite de sélectionner les colonnes individuellement pour effectuer le mappage du schéma. Si vous le souhaitez, vous pouvez remplacer ces mappages en utilisant les listes déroulantes pour mapper les colonnes une par une. Le modèle devient plus précis à mesure que vous mappez des colonnes. L’Assistant de copie met continuellement à jour le modèle pour finalement obtenir le modèle adapté au mappage de colonnes que vous voulez.     

![Mappage de schéma](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrage des données
Vous pouvez filtrer les données sources pour sélectionner uniquement celles qui doivent être copiées vers le magasin de données de récepteur. Le filtrage réduit le volume des données à copier vers le magasin de données de récepteur et améliore de ce fait le débit de la copie. Il fournit un moyen souple de filtrer les données dans une base de données relationnelle à l’aide du langage de requête SQL ou les fichiers d’un dossier d’objets blob Azure à l’aide de [variables et fonctions Data Factory](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrage des données dans une base de données
La capture d’écran suivante illustre une requête SQL à l’aide de la fonction `Text.Format` et de la variable `WindowStart`.

![Valider des expressions](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrage des données dans un dossier d’objets blob Azure
Vous pouvez utiliser des variables dans le chemin du dossier pour copier des données à partir d’un dossier qui est déterminé au moment de l’exécution par les [variables système](data-factory-functions-variables.md#data-factory-system-variables). Les variables prises en charge sont les suivantes : **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}** et **{custom}**. Exemple : inputfolder/{year}/{month}/{day}.

Supposons que vos dossiers d’entrée présentent le format suivant :

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Cliquez sur le bouton **Parcourir** à côté de **Fichier ou dossier**, accédez à l’un de ces dossiers (par exemple, 2016->03->01->02), puis cliquez sur **Choisir**. Vous devez voir `2016/03/01/02` dans la zone de texte. À présent, remplacez **2016** par **{year}**, **03** par **{month}**, **01** par **{day}** et **02** par **{hour}**, puis appuyez sur la touche de **tabulation**. Vous devez maintenant voir des listes déroulantes pour sélectionner le format de ces quatre variables :

![Utilisation de variables système](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Comme la capture d’écran suivante le montre, vous pouvez également configurer une variable **custom** pour utiliser l’une des [chaînes de format prises en charge](https://msdn.microsoft.com/library/8kb3ddd4.aspx). Pour sélectionner un dossier avec cette structure, utilisez d’abord le bouton **Parcourir** . Remplacez alors une valeur par **{custom}**, puis appuyez sur la touche de **tabulation** pour afficher la zone de texte dans laquelle vous pouvez taper la chaîne de format.     

![Utilisation de la variable custom](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Options de planification
Vous pouvez effectuer l’opération de copie une seule fois ou la répéter selon une planification établie (horaire, quotidienne et ainsi de suite.). Ces deux options peuvent être définies pour l’ensemble des connecteurs entre différents environnements utilisés pour la copie locale, dans le cloud ou sur un Bureau local.

Une opération de copie unique ne permet le déplacement des données à d’une source vers une destination qu’une seule fois. Elle s’applique aux données de toute taille et de n’importe quel format pris en charge. La copie planifiée vous permet de copier des données selon une périodicité définie. Vous pouvez utiliser les paramètres avancés (nouvelle tentative, délai d’attente, alertes, etc.) pour configurer la copie planifiée.

![Propriétés de planification](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>étapes suivantes
Pour découvrir une procédure pas à pas rapide sur l’utilisation de l’Assistant Data Factory Copy afin de créer un pipeline avec une activité de copie, consultez le [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md).
