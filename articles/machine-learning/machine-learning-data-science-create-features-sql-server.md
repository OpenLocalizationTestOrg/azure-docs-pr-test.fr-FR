---
title: "fonctionnalités aaaCreate pour les données dans SQL Server à l’aide de SQL et Python | Documents Microsoft"
description: "Traiter les données de SQL Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Créer des fonctionnalités pour les données dans SQL Server à l’aide de SQL et Python
Ce document montre comment les fonctionnalités toogenerate pour les données stockées dans une machine virtuelle SQL Server sur Azure qui aident à des algorithmes en savoir plus efficacement à partir des données de hello. Vous pouvez utiliser SQL ou un langage de programmation comme Python, les deux approches étant illustrées ici.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Cela **menu** lie tootopics qui décrivent comment toocreate pour les données dans différents environnements. Cette tâche est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Pour obtenir un exemple pratique, vous pouvez consulter hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) et toohello IPNB intitulée [NYC données ensuivirent à l’aide du bloc-notes de IPython et de SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) pour une procédure pas à pas de bout en bout.
> 
> 

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez :

* Créé un compte Azure Storage. Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Stocké vos données dans SQL Server. Si vous n’avez pas le cas, consultez [déplacer les données tooan base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) pour savoir comment toomove hello des données.

## <a name="sql-featuregen"></a>Génération de fonctionnalités avec SQL
Dans cette section, nous décrivons plusieurs manières de générer des fonctionnalités via SQL :  

1. [Génération de fonctionnalités utilisant des décomptes](#sql-countfeature)
2. [Génération de caractéristiques de compartimentage](#sql-binningfeature)
3. [Déploiement de fonctionnalités de hello à partir d’une seule colonne](#sql-featurerollout)

> [!NOTE]
> Une fois que vous générez des fonctionnalités supplémentaires, vous pouvez les ajouter en tant que table de colonnes toohello existante ou créer une table avec des fonctionnalités supplémentaires hello et la clé primaire, ce qui peut être jointe avec la table d’origine de hello.
> 
> 

### <a name="sql-countfeature"></a>Génération de fonctionnalités utilisant des décomptes
Ce document décrit deux manières de générer des fonctionnalités utilisant des décomptes. Hello première méthode utilise la somme conditionnelle et utilise deuxième hello hello clause « where ». Ils peuvent être joints avec hello d’origine (à l’aide des colonnes de clé primaire) de table toohave nombre des fonctionnalités en même temps que les données d’origine hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Génération de caractéristiques de compartimentage
Hello suivant montre comment toogenerate placées fonctionnalités par compartimentage (à l’aide de 5 emplacements), une colonne numérique qui peut être utilisée en tant que fonctionnalité à la place :

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Déploiement de fonctionnalités de hello à partir d’une seule colonne
Dans cette section, nous allons montrer comment tooroll montée une seule colonne dans une table toogenerate supplémentaire des fonctionnalités. Hello exemple suppose qu’il existe une colonne de latitude ou de longitude dans la table hello à partir de laquelle vous essayez de toogenerate fonctionnalités.

Voici une brève introduction relative aux données de latitude/longitude (reposant sur les informations du site stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Cela est utile toounderstand avant le champ d’emplacement featurizing hello :

* signe de Hello nous indique que nous sont Nord ou sud, est ou ouest globe de hello.
* Un chiffre des centaines différent de zéro indique que nous utilisons la longitude, et non la latitude.
* les chiffres des dizaines de Hello donne un tooabout position 1 000 kilomètres. Il nous fournit des informations utiles sur le continent ou l’océan dans lequel nous nous trouvons.
* chiffre des unités Hello (un degré décimale) donne une position de too111 kilomètres (60 milles, environ 69 miles). Il nous permet de déterminer approximativement le département de grande superficie ou le pays dans lequel nous sommes.
* première décimale Hello vaut des too11.1 km : elle peut distinguer la position hello d’une ville volumineuse à partir d’une grande ville voisinage.
* deuxième décimale Hello vaut des too1.1 km : il peut séparer un village hello ensuite.
* est intéressant too110 m: Hello troisième décimale, il peut identifier un grand champ agricole ou un campus institutionnel.
* est intéressant too11 m: Hello quatrième décimale, il peut identifier un paquet de terrain. Il est toohello comparable au niveau de précision classique d’une unité GPS corrigée avec sans interférence.
* Hello cinquième décimale est-il important des too1.1 m: caractériser arborescences. Niveau de toothis de précision avec des unités commerciales GPS ne peut être obtenu avec une correction différentielle.
* Hello sixième décimale est intéressant m: too0.11 que vous pouvez l’utiliser pour la disposition des structures en détail, pour la conception des architectures, des routes de génération. Elle devrait se révéler amplement suffisante pour assurer le suivi des mouvements des glaciers et des rivières. L’obtention d’une telle précision sur un GPS nécessite l’emploi de mesures rigoureuses, telles qu’une correction différentielle.

informations d’emplacement Hello peuvent peut être caractéristiques, procédez comme suit but région, l’emplacement et les informations de ville. Notez qu’une seule fois peut également appeler un point de terminaison REST telles que les API Bing Maps disponible à l’adresse `https://msdn.microsoft.com/library/ff701710.aspx` plus d’informations tooget hello région/district.

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

Hello emplacement en fonction des fonctionnalités peuvent être davantage ci-dessus utilise des fonctionnalités de nombre supplémentaire de toogenerate comme décrit précédemment.

> [!TIP]
> Vous pouvez insérer par programme des enregistrements de hello à l’aide de la langue de votre choix. Vous devrez peut-être les données de salutation tooinsert dans l’efficacité de segments tooimprove écriture [extraire exemple hello de toodo ce à l’aide de pyodbc ici](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Une autre solution consiste à tooinsert des données à l’aide de base de données hello [utilitaire BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Connexion tooAzure Machine Learning
Hello généré récemment fonctionnalité peut être ajoutée en tant que colonne tooan existant table stockée dans une nouvelle table et jointe à la table d’origine de hello pour l’apprentissage. Fonctionnalités peuvent être générées ou accessibles si déjà créé, à l’aide de hello [importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module dans Azure ML, comme indiqué ci-dessous :

![lecteurs azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Utilisation d’un langage de programmation tel que Python
À l’aide des fonctionnalités de toogenerate Python lorsque les données de salutation sont dans SQL Server est données tooprocessing similaires dans des objets blob Azure à l’aide de Python comme documenté dans [données d’objets Blob Azure de processus dans l’environnement pour la science des données](machine-learning-data-science-process-data-blob.md). les données de salutation doit toobe chargé à partir de la base de données hello dans une trame de données pandas et peuvent ensuite être traitées ultérieurement. Nous processus hello de connexion de base de données toohello et de charger les données de hello de trame de données hello dans cette section de document.

Hello, suivant le format de chaîne de connexion peut être utilisé tooconnect tooa base de données SQL à partir de Python à l’aide de pyodbc (remplacez servername, dbname, nom d’utilisateur et mot de passe avec les valeurs spécifiques) :

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [bibliothèque de Pandas](http://pandas.pydata.org/) dans Python fournit un ensemble complet d’outils d’analyse de données et des structures de données pour la manipulation de données pour la programmation de Python. code Hello ci-dessous lit hello résultats à partir d’une base de données SQL Server dans une trame de données Pandas :

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Maintenant que vous pouvez travailler avec la trame de données hello Pandas comme indiqué dans les rubriques [créent des fonctionnalités pour les données de stockage d’objets blob Azure à l’aide de Panda](machine-learning-data-science-create-features-blob.md).

