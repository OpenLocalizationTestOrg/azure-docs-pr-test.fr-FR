---
title: "données d’aaaExplore dans SQL Server virtuels dans Azure | Documents Microsoft"
description: "Comment tooexplore les données stockées dans une machine virtuelle SQL Server sur Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Explorer les données d’une machine virtuelle SQL Server sur Azure
Ce document décrit comment les données tooexplore qui sont stockées dans une machine virtuelle SQL Server sur Azure. Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.

suivant de Hello **menu** tootopics qui décrivent comment toouse outils tooexplore des données à partir de différents environnements de stockage est liée. Cette tâche est une étape Bonjour Cortana Analytique processus (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> Hello exemples d’instructions SQL dans ce document supposent que les données sont dans SQL Server. Si elle n’est pas le cas, consultez Comment toohello cloud données science processus carte toolearn toomove votre tooSQL de données serveur.
> 
> 

## <a name="sql-dataexploration"></a>Explorer les données SQL avec des scripts SQL
Voici quelques exemples de scripts SQL qui peuvent être utilisés tooexplore des magasins de données dans SQL Server.

1. Obtenir le nombre de hello d’observations par jour
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obtenir des niveaux de hello dans une colonne catégorielle
   
    `select  distinct <column_name> from <databasename>`
3. Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obtenir distribution hello pour les colonnes numériques
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Pour obtenir un exemple pratique, vous pouvez utiliser hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) et toohello IPNB intitulée [NYC données ensuivirent à l’aide du bloc-notes de IPython et de SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) pour une procédure pas à pas de bout en bout.
> 
> 

## <a name="python"></a>Explorer les données SQL avec Python
L’utilisation de Python tooexplore données et générer des fonctionnalités lorsque hello sont de données dans SQL Server est données tooprocessing similaires dans des objets blob Azure à l’aide de Python, comme décrit dans [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md). les données de salutation doit toobe chargé à partir de la base de données hello dans une trame de données pandas et peuvent ensuite être traitées ultérieurement. Nous processus hello de connexion de base de données toohello et le chargement des données de hello en hello trame de données dans cette section de document.

Hello, suivant le format de chaîne de connexion peut être utilisé tooconnect tooa base de données SQL à partir de Python à l’aide de pyodbc (remplacez servername, dbname, nom d’utilisateur et mot de passe avec les valeurs spécifiques) :

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [bibliothèque de Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python. Hello de code suivant lit les résultats hello retourné à partir d’une base de données SQL Server dans une trame de données Pandas :

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Maintenant que vous pouvez travailler avec hello Pandas trame de données comme indiqué dans la rubrique de hello [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Exemple de processus Cortana Analytics en action
Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus Analytique de Cortana à l’aide d’un jeu de données public, consultez [hello du processus de science des données équipe en action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

