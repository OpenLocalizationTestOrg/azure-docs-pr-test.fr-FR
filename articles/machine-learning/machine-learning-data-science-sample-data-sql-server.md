---
title: "aaaSample données dans SQL Server sur Azure | Documents Microsoft"
description: "Échantillonner des données dans SQL Server sur Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Échantillonner des données dans SQL Server sur Azure
Ce document montre comment les données de toosample stockées dans SQL Server sur Azure à l’aide de SQL ou hello langage de programmation Python. Il montre également comment toomove les données échantillonnées dans Azure Machine Learning en l’enregistrant le fichier tooa, téléchargeant tooan objets blob Azure, puis de le lire dans Azure Machine Learning Studio.

échantillonnage de Python Hello utilise hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC bibliothèque tooconnect tooSQL Server sur Azure et hello [Pandas](http://pandas.pydata.org/) échantillonnage de bibliothèque toodo hello.

> [!NOTE]
> Hello exemple de code SQL dans ce document part du principe que hello données sont dans un serveur SQL Server sur Azure. Si elle n’est pas le cas, veuillez vous référer trop[déplacer les données tooSQL Server sur Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) rubrique pour obtenir des instructions sur la façon de toomove votre tooSQL données Server sur Azure.
> 
> 

suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Pourquoi échantillonner vos données ?**
Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille. Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités. Son rôle dans hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.

Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Utilisation de SQL
Cette section décrit plusieurs méthodes à l’aide de SQL tooperform un échantillonnage aléatoire simple par rapport aux données de hello dans la base de données hello. Choisissez une méthode en fonction de la taille de vos données et de leur distribution.

deux éléments Hello ci-dessous montrent comment newid toouse dans SQL Server tooperform hello d’échantillonnage. Hello méthode que vous choisissez dépend aléatoire hello exemple toobe (pk_id hello exemple de code ci-dessous est supposé toobe une clé primaire générée automatiquement).

1. Échantillon aléatoire moins strict
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Échantillon plus aléatoire 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Vous pouvez également utiliser l’élément TABLESAMPLE pour l’échantillonnage, comme illustré ci-dessous. Cela peut être une meilleure approche si vos données sont volumineuses (en supposant que les données sur des pages différentes ne sont pas mis en corrélation) et pour hello requête toocomplete dans un délai raisonnable.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Vous pouvez explorer et générer des fonctionnalités à partir de ces données échantillonnées en les stockant dans une nouvelle table.
> 
> 

### <a name="sql-aml"></a>Connexion tooAzure Machine Learning
Vous pouvez utiliser directement les exemples de requêtes hello ci-dessus Bonjour Azure Machine Learning [importer des données] [ import-data] données toodown-exemple hello module hello rendiez et importez-les dans une expérience Azure Machine Learning. Vous trouverez ci-dessous une capture d’écran de l’utilisation de données de hello échantillonnée tooread hello lecture du module :

![lecteur sql][1]

## <a name="python"></a>À l’aide du langage de programmation Python hello
Cette section illustre l’utilisation de hello [pyodbc bibliothèque](https://code.google.com/p/pyodbc/) tooestablish une application ODBC se connecter tooa la base de données SQL server dans Python. chaîne de connexion de base de données Hello est comme suit : (replace servername, dbname, nom d’utilisateur et mot de passe à la configuration) :

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python. code Hello ci-dessous lit un exemple de 0,1 % des données de hello à partir d’une table de base de données SQL Azure en données Pandas :

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Vous pouvez désormais travailler avec des données dans une trame de données hello Pandas hello échantillonnée. 

### <a name="python-aml"></a>Connexion tooAzure Machine Learning
Vous pouvez utiliser hello toosave le code exemple hello échantillonnées en bas des données tooa fichier suivant et téléchargez-le tooan objets blob Azure. Hello données dans l’objet blob de hello peuvent être directement lues dans une expérience d’apprentissage de Machine Azure à l’aide de hello [importer des données] [ import-data] module. étapes de Hello sont les suivantes : 

1. Écrire le fichier local tooa du frame données hello pandas
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Télécharger l’objet blob de fichier local tooAzure
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. Lire les données d’objets blob Azure à l’aide d’Azure Machine Learning [importer des données] [ import-data] module, comme indiqué dans la capture d’écran hello ci-dessous :

![objet blob de lecteur][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Hello processus de science des données équipe dans l’exemple d’Action
Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus de science des données équipe un un jeu de données public, à l’aide voir [équipe processus de science des données en Action : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
