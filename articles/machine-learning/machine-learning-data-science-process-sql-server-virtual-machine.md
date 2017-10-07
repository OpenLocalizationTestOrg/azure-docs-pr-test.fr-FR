---
title: "aaaExplore des données dans une machine virtuelle de SQL Server sur Azure | Documents Microsoft"
description: "Explorer des données et générer des fonctionnalités dans une machine virtuelle SQL Server sur Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Traitement des données d’une machine virtuelle SQL Server sur Azure
Ce document décrit comment les données tooexplore et générer des fonctionnalités pour les données stockées dans une machine virtuelle SQL Server sur Azure. Cela est possible avec le retraitement des données à l'aide de SQL ou en utilisant un langage de programmation comme Python.

> [!NOTE]
> Hello exemples d’instructions SQL dans ce document supposent que les données sont dans SQL Server. Si elle n’est pas le cas, consultez Comment toohello cloud données science processus carte toolearn toomove votre tooSQL de données serveur.
> 
> 

## <a name="SQL"></a>Utilisation de SQL
Nous allons décrire hello données batailler avec des tâches de cette section à l’aide de SQL suivantes :

1. [Exploration des données](#sql-dataexploration)
2. [Génération de fonctionnalités](#sql-featuregen)

### <a name="sql-dataexploration"></a>Exploration des données
Voici quelques exemples de scripts SQL qui peuvent être utilisés tooexplore des magasins de données dans SQL Server.

> [!NOTE]
> Pour obtenir un exemple pratique, vous pouvez utiliser hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) et toohello IPNB intitulée [NYC données ensuivirent à l’aide du bloc-notes de IPython et de SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) pour une procédure pas à pas de bout en bout.
> 
> 

1. Obtenir le nombre de hello d’observations par jour
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obtenir des niveaux de hello dans une colonne catégorielle
   
    `select  distinct <column_name> from <databasename>`
3. Obtenir le nombre hello de niveaux dans la combinaison de deux colonnes catégorielles 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obtenir distribution hello pour les colonnes numériques
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Génération de fonctionnalités
Dans cette section, nous décrivons plusieurs manières de générer des fonctionnalités via SQL :  

1. [Génération de fonctionnalités utilisant des décomptes](#sql-countfeature)
2. [Génération de caractéristiques de compartimentage](#sql-binningfeature)
3. [Déploiement de fonctionnalités de hello à partir d’une seule colonne](#sql-featurerollout)

> [!NOTE]
> Une fois que vous générez des fonctionnalités supplémentaires, vous pouvez les ajouter en tant que table de colonnes toohello existante ou créer une table avec des fonctionnalités supplémentaires hello et la clé primaire, ce qui peut être jointe avec la table d’origine de hello. 
> 
> 

### <a name="sql-countfeature"></a>Génération de fonctionnalités utilisant des décomptes
Hello exemples suivants illustrent deux façons de générer des fonctionnalités de nombre. Hello première méthode utilise la somme conditionnelle et utilise deuxième hello hello clause « where ». Ils peuvent être joints avec hello d’origine (à l’aide des colonnes de clé primaire) de table toohave nombre des fonctionnalités en même temps que les données d’origine hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Génération de caractéristiques de compartimentage
Hello suivant montre comment toogenerate placées fonctionnalités par compartimentage (à l’aide de cinq emplacements), une colonne numérique qui peut être utilisée en tant que fonctionnalité à la place :

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Déploiement de fonctionnalités de hello à partir d’une seule colonne
Dans cette section, nous allons montrer comment tooroll à une seule colonne dans une table toogenerate supplémentaire des fonctionnalités. Hello exemple suppose qu’il existe une colonne de latitude ou de longitude dans la table hello à partir de laquelle vous essayez de toogenerate fonctionnalités.

Voici une brève introduction sur les données d’emplacement latitude/longitude (avec une ressource à partir de stackoverflow [comment toomeasure hello précision de latitude et longitude ?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Cela est utile toounderstand avant le champ d’emplacement featurizing hello :

* signe de Hello nous indique que nous sont Nord ou sud, est ou ouest globe de hello.
* Un chiffre des centaines différent de zéro indique que nous utilisons la longitude, et non la latitude.
* les chiffres des dizaines de Hello donne un tooabout position 1 000 kilomètres. Il nous fournit des informations utiles sur le continent ou l’océan dans lequel nous nous trouvons.
* chiffre des unités Hello (un degré décimale) donne une position de too111 kilomètres (60 milles, environ 69 miles). Il nous permet de déterminer approximativement le département de grande superficie ou le pays dans lequel nous sommes.
* première décimale Hello vaut des too11.1 km : elle peut distinguer la position hello d’une ville volumineuse à partir d’une grande ville voisinage.
* deuxième décimale Hello vaut des too1.1 km : il peut séparer un village hello ensuite.
* est intéressant too110 m: Hello troisième décimale, il peut identifier un grand champ agricole ou un campus institutionnel.
* est intéressant too11 m: Hello quatrième décimale, il peut identifier un paquet de terrain. Il est toohello comparable au niveau de précision classique d’une unité GPS corrigée avec sans interférence.
* cinquième décimale Hello vaut des too1.1 m: qu'il arborescences fait la distinction entre eux. Niveau de toothis de précision avec des unités commerciales GPS ne peut être obtenu avec une correction différentielle.
* Hello sixième décimale est intéressant m: too0.11 que vous pouvez l’utiliser pour la disposition des structures en détail, pour la conception des architectures, des routes de génération. Elle devrait se révéler amplement suffisante pour assurer le suivi des mouvements des glaciers et des rivières. L’obtention d’une telle précision sur un GPS nécessite l’emploi de mesures rigoureuses, telles qu’une correction différentielle.

informations d’emplacement Hello peuvent être caractéristiques, procédez comme suit séparation des informations sur la ville, l’emplacement et la région. Notez que vous pouvez également appeler un point de terminaison REST telles que les API Bing Maps disponible à l’adresse [de trouver un emplacement par Point](https://msdn.microsoft.com/library/ff701710.aspx) informations de région/district tooget hello.

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Ces fonctionnalités basée sur l’emplacement peuvent être davantage fonctionnalités nombre supplémentaire de toogenerate utilisés comme décrit précédemment. 

> [!TIP]
> Vous pouvez insérer par programme des enregistrements de hello à l’aide de la langue de votre choix. Vous devrez peut-être les données de salutation tooinsert dans l’efficacité de segments tooimprove écriture (pour obtenir un exemple de procédure toodo cette pyodbc, voir les [A HelloWorld exemple tooaccess SQLServer avec python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Une autre solution consiste à données tooinsert hello de base de données à l’aide de hello [utilitaire BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Connexion tooAzure Machine Learning
Hello généré récemment fonctionnalité peut être ajoutée en tant que colonne tooan existant table stockée dans une nouvelle table et jointe à la table d’origine de hello pour l’apprentissage. Fonctionnalités peuvent être générées ou accessibles si déjà créé, à l’aide de hello [importer des données] [ import-data] module dans Azure Machine Learning, comme indiqué ci-dessous :

![lecteurs azureml][1] 

## <a name="python"></a>Utilisation d’un langage de programmation tel que Python
À l’aide de données de tooexplore Python et générer des fonctionnalités lorsque hello sont de données dans SQL Server est données tooprocessing similaires dans des objets blob Azure à l’aide de Python comme documenté dans [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md). les données de salutation doit toobe chargé à partir de la base de données hello dans une trame de données pandas et peuvent ensuite être traitées ultérieurement. Nous processus hello de connexion de base de données toohello et de charger les données de hello de trame de données hello dans cette section de document.

Hello, suivant le format de chaîne de connexion peut être utilisé tooconnect tooa base de données SQL à partir de Python à l’aide de pyodbc (remplacez servername, dbname, nom d’utilisateur et mot de passe avec les valeurs spécifiques) :

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [bibliothèque de Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python. code Hello ci-dessous lit hello résultats à partir d’une base de données SQL Server dans une trame de données Pandas :

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Maintenant que vous pouvez travailler avec la trame de données hello Pandas comme indiqué dans l’article de hello [données d’objets Blob Azure de processus dans votre environnement de science des données](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Exemple de processus de science des données Azure en action
Pour obtenir un exemple de procédure pas à pas de bout en bout de hello processus de science des données Azure à l’aide d’un jeu de données public, consultez [processus de science des données Azure dans l’Action](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

