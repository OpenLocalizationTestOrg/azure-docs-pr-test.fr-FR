---
title: "aaaBuild et déployer un modèle d’apprentissage automatique à l’aide de SQL Server sur une machine virtuelle Azure | Des documents Microsoft"
description: "Processus d’analyse avancé et technologie en action"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Hello processus de science des données équipe en action : à l’aide de SQL Server
Dans ce didacticiel, vous voyez hello les processus de génération et de déploiement d’un modèle d’apprentissage automatique à l’aide de SQL Server et un jeu de données disponible publiquement--hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) jeu de données. procédure de Hello suit un flux de travail de science des données standard : réception et Explorer les données hello ingénieur learning toofacilitate de fonctionnalités, puis générer et déployer un modèle.

## <a name="dataset"></a>Description du jeu de données NYC Taxi Trips
Hello les données NYC Taxi voyage est d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), qui comprend plus de 173 millions hello et des boucles tarifs payé pour chaque sortie. Chaque enregistrement de voyage comprend hello collecte et remise l’emplacement et l’heure, hack rendues anonymes (pilote) numéro de licence et nombre de medallion (id unique de taxi). les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :

1. Hello 'trip_data' CSV contient les détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage. Voici quelques exemples d’enregistrements :
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello 'trip_fare' CSV contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé. Voici quelques exemples d’enregistrements :
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composée de champs de hello : medallion, hack\_certificat et pickup\_datetime.

## <a name="mltasks"></a>Exemples de tâches de prédiction
Nous formuler les trois problèmes de prédiction selon hello *Conseil\_quantité*, à savoir :

1. Classification binaire : prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *tip\_amount* de 0 $ est un exemple négatif.
2. Classification multiclasse : plage de hello toopredict d’info-bulle payé pour le voyage de hello. Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Tâche de régression : toopredict hello d’info-bulle montant d’un voyage.  

## <a name="setup"></a>Configuration des hello Azure science environnement de données analytique avancée
Comme vous pouvez le constater hello [planifier votre environnement](machine-learning-data-science-plan-your-environment.md) guide, il existe plusieurs options toowork, avec jeu de données hello NYC Taxi allers-retours dans Azure :

* Travailler avec des données hello dans des objets BLOB Azure, puis le modèle dans Azure Machine Learning
* Charger des données dans une base de données SQL Server, puis le modèle dans Azure Machine Learning hello

Dans ce didacticiel, nous allons vous montrer importation parallèle en bloc de hello tooa de données SQL Server, exploration de données, la fonctionnalité d’ingénierie et vers le bas d’échantillonnage à l’aide de SQL Server Management Studio ainsi qu’à l’aide du bloc-notes de notebooks. Des [exemples de scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) et de [notebooks IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) sont publiquement accessibles dans GitHub. Un toowork de bloc-notes exemple IPython avec des données dans des objets BLOB Azure hello est également disponible dans hello même emplacement.

tooset votre environnement Azure pour la science des données :

1. [Créer un compte de stockage](../storage/common/storage-create-storage-account.md)
2. [Création d’un espace de travail Microsoft Azure Machine Learning](machine-learning-create-workspace.md)
3. [Approvisionnez une machine virtuelle de science des données](machine-learning-data-science-setup-sql-server-virtual-machine.md), qui fournit un serveur SQL Server et un serveur Notebook IPython.
   
   > [!NOTE]
   > exemples de scripts Hello et IPython Notebook sera téléchargé tooyour science des données virtual machine pendant le processus d’installation de hello. Hello script post-installation de machine virtuelle est terminée, les exemples hello doivent être dans la bibliothèque de Documents de votre machine virtuelle :  
   > 
   > * Exemples de scripts : `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Exemples de notebooks IPython : `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` est le nom de connexion de votre machine virtuelle Windows. Nous appelons toohello dossiers en tant que **exemples de Scripts** et **exemple IPython Notebook**.
   > 
   > 

Selon la taille du jeu de données hello, emplacement de source de données et environnement cible Azure sélectionné de hello, ce scénario est similaire trop[scénario \#5 : jeu de données volumineux dans des fichiers locaux, ciblent SQL Server dans Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Obtenir hello données à partir de la Source publique
tooget hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset à partir de son emplacement public, vous pouvez utiliser une des méthodes hello décrites dans [tooand de déplacer les données à partir du stockage d’objets Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello données tooyour nouvel ordinateur virtuel.

données de salutation toocopy à l’aide de AzCopy :

1. Connectez-vous à tooyour virtual machine (VM)
2. Créer un nouveau répertoire de disque de données de la machine virtuelle hello (Remarque : n’utilisez pas hello disque temporaire qui est livré avec hello machine virtuelle comme disque de données).
3. Dans une fenêtre d’invite de commandes, exécutez hello suivant la ligne de commande Azcopy, en remplaçant < path_to_data_folder > avec votre dossier de données créée dans (2) :
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Lorsque hello AzCopy est terminée, un total de 24 compressé de fichiers CSV (12 pour le voyage\_données et 12 pour le voyage\_tarif) doit être dans le dossier de données hello.
4. Décompressez les fichiers hello téléchargé. Notez le dossier hello où résident les fichiers de hello non compressé. Ce dossier sera référencé tooas hello < chemin d’accès\_à\_données\_fichiers\>.

## <a name="dbload"></a>Importer en bloc les données dans une base de données SQL Server
Hello performances de chargement et de transfert de grandes quantités de base de données de données tooan SQL et les requêtes suivantes peuvent être améliorées en utilisant *Partitioned Tables et vues*. Dans cette section, nous allons suivre les instructions hello décrites dans [parallèle en bloc données à l’aide de SQL Partition Tables d’importation](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate une nouvelle base de données et charger hello les données dans des tables partitionnées en parallèle.

1. Connecté tooyour machine virtuelle, démarrez **SQL Server Management Studio**.
2. Connectez-vous à l’aide de l’authentification Windows.
   
    ![Connecter SSMS][12]
3. Si vous n’avez pas encore modifié le mode d’authentification SQL Server hello et créé un nouveau nom d’utilisateur SQL, ouvrez le fichier de script de hello nommé **modifier\_auth.sql** Bonjour **exemples de Scripts** dossier. Modifier le nom d’utilisateur par défaut hello et le mot de passe. Cliquez sur **! Exécutez** dans le script de hello toorun hello barre d’outils.
   
    ![Exécuter le script][13]
4. Vérifiez et/ou modifiez hello SQL Server par défaut de base de données et journal dossiers tooensure que les bases de données nouvellement créées est stocké dans un disque de données. image de machine virtuelle SQL Server Hello qui est optimisé pour les charges datawarehousing est préconfiguré avec des disques de données et du journal. Si votre machine virtuelle n’incluait pas d’un disque de données et que vous avez ajouté des disques durs virtuels pendant hello les processus de configuration de machine virtuelle, modifiez les dossiers par défaut hello comme suit :
   
   * Nom de SQL Server avec le bouton hello Bonjour gauche du Panneau de configuration et cliquez sur **propriétés**.
     
       ![Propriétés SQL Server][14]
   * Sélectionnez **les paramètres de base de données** de hello **sélectionner une page** toohello gauche de la liste.
   * Vérifiez et/ou modifiez hello **emplacements par défaut de base de données** toohello **disque de données** les emplacements de votre choix. Il s’agit d’emplacement des nouvelles bases de données si créé avec les paramètres d’emplacement par défaut hello.
     
       ![Valeurs par défaut de la base de données SQL][15]  
5. toocreate une base de données et un ensemble de groupes de fichiers toohold hello tables partitionnées, ouvrez l’exemple de script hello **créer\_db\_default.sql**. Hello script crée une base de données nommée **TaxiNYC** et 12 groupes de fichiers dans un emplacement de données par défaut hello. Chaque groupe de fichiers contiendra un mois de données trip\_data et trip\_fare. Modifier le nom de base de données hello, si vous le souhaitez. Cliquez sur **! Exécutez** script de hello toorun.
6. Ensuite, créez deux tables de partition, une pour le voyage de hello\_et une autre pour le voyage de hello\_tarif. Ouvrez l’exemple de script hello **créer\_partitionnée\_table.sql**, qui sera :
   
   * Créer un partition fonction toosplit hello de données par mois.
   * Créer un toomap de schéma de partition données tooa autre groupe de fichiers de chaque mois.
   * Créer le schéma de partition de deux tables partitionnées toohello mappé : **nyctaxi\_voyage** contiendra voyage de hello\_données et **nyctaxi\_tarif** contiendra voyage de hello \_prix des données.
     
     Cliquez sur **! Exécutez** toorun hello script et créer des tables partitionnée de hello.
7. Bonjour **exemples de Scripts** dossier, il existe deux exemples de scripts PowerShell fourni toodemonstrate importations en bloc parallèle tooSQL Server de tables de données.
   
   * **bcp\_parallèles\_generic.ps1** est une script générique tooparallel importation des données en bloc dans une table. Modifiez cette tooset hello cible d’entrée et de variables de script comme indiqué dans les lignes de commentaire hello dans le script de hello.
   * **bcp\_parallèles\_nyctaxi.ps1** est une version préconfigurée de script générique de hello et peut être utilisé tootooload les deux tables pour les données NYC Taxi allers-retours hello.  
8. Avec le bouton hello **bcp\_parallèles\_nyctaxi.ps1** nom de script, cliquez sur **modifier** tooopen dans PowerShell. Hello de révision variables prédéfinies et modifier le nom de base de données sélectionnée tooyour conséquente, dossier de données d’entrée, dossier de journal cible et les fichiers de format de chemins d’accès toohello exemple **nyctaxi_trip.xml** et **nyctaxi\_ fare.XML** (fourni dans hello **exemples de Scripts** dossier).
   
    ![Importer les données][16]
   
    Vous pouvez également sélectionner le mode d’authentification hello, valeur par défaut est l’authentification Windows. Cliquez sur flèche hello vert toorun de barre d’outils hello. script de Hello lancera 24 opérations d’importation en bloc dans les 12 parallèle, pour chaque table partitionnée. Vous pouvez surveiller la progression de l’importation données hello en ouvrant le dossier de données de valeur par défaut de SQL Server hello comme ci-dessus.
9. rapports de script PowerShell Hello hello de début et de fin des heures. Lorsque tous en bloc d’importation terminée, hello leur heure de fin est signalée. Vérifiez tooverify dossier de journal de cible de hello hello les importations en bloc ont réussi, autrement dit, aucune erreur n’est signalée dans le dossier de journal hello cible.
10. Votre base de données est désormais prête pour vos opérations d’exploration, de conception de fonctionnalités, etc. Étant donné que les tables de hello sont partitionnées selon toohello **collecte\_datetime** champ, les requêtes qui incluent des **collecte\_datetime** conditions Bonjour  **OÙ** clause bénéficieront de schéma de partition hello.
11. Dans **SQL Server Management Studio**, explorez l’exemple de script hello fourni **exemple\_queries.sql**. toorun un des exemples de requêtes hello, mettez en surbrillance hello lignes de la requête, puis cliquez sur **! Exécutez** dans la barre d’outils hello.
12. les données NYC Taxi allers-retours de Hello est chargé dans deux tables distinctes. tooimprove des opérations de jointure, il est recommandé de tables de hello tooindex. Hello exemple de script **créer\_partitionnée\_index.sql** crée des index partitionnés sur la clé de jointure composite hello **medallion, hack\_licence et capture\_datetime**.

## <a name="dbexplore"></a>Exploration des données et conception de fonctionnalités dans SQL Server
Dans cette section, nous allons effectuer la génération de fonctionnalité et d’exploration de données en exécutant des requêtes SQL directement dans hello **SQL Server Management Studio** à l’aide de la base de données SQL Server hello créé précédemment. Un exemple de script nommé **exemple\_queries.sql** est fourni dans hello **exemples de Scripts** dossier. Modifier le nom de base de données hello script toochange hello, si elle est différente de la valeur par défaut hello : **TaxiNYC**.

Dans cet exercice, nous allons :

* Vous connecter trop**SQL Server Management Studio** en utilisant soit l’authentification Windows ou authentification SQL et hello nom de connexion SQL et le mot de passe.
* Explorer les distributions de données de quelques champs portant sur différentes périodes.
* Analyser la qualité des données des champs de longitude et de latitude hello.
* Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.
* Générer des fonctionnalités et calculer/comparer les distances des trajets.
* Joindre hello deux tables et extraire un échantillon aléatoire qui sera utilisé toobuild modèles.

Lorsque vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez :  

1. Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning, ou
2. Conserver hello échantillonnée et données ingénieries que vous prévoyez toouse pour une base de données de création de modèles de table et utilisent la nouvelle table de hello Bonjour [importer des données] [ import-data] module dans Azure Machine Learning.

Dans cette section, nous allons enregistrer hello final interroger tooextract et exemple hello des données. méthode deuxième Hello est illustrée dans hello [l’Exploration de données et d’ingénierie de fonctionnalité notebooks bloc-notes](#ipnb) section.

Pour une vérification rapide du nombre de hello de lignes et colonnes Bonjour tables remplies précédemment à l’aide d’importation en bloc parallèle,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Exploration : distribution des courses par médaillon
Cet exemple identifie le medallion hello (numéros taxi) avec plus de 100 allers-retours pendant une période donnée. requête de Hello tireront parti d’accès à la table hello partitionnée, car il est conditionnée par le schéma de partition hello de **collecte\_datetime**. Interrogation du jeu de données complet hello rendent également utiliser de table partitionnée de hello et/ou d’analyse d’index.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploration : distribution des courses par médaillon et par licence de taxi
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Évaluation de la qualité des données : vérifier les enregistrements avec une longitude et/ou une latitude incorrectes
Cet exemple examine si un des champs de longitude et/ou latitude hello contenir une valeur non valide (les degrés en radians doivent être comprise entre -90 et 90), ou avoir (0, 0) coordonnées.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploration : distribution des courses avec et sans pourboire
Cet exemple recherche le nombre de hello d’allers-retours qui ont été déposés par rapport aux ne pourboires pas dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello). Cette distribution reflète hello étiquette binaire distribution toobe utilisée ultérieurement pour la modélisation de classification binaire.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Exploration : distribution des classes/fourchettes de pourboires
Cet exemple calcule la distribution hello des plages de Conseil dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello). Il s’agit de distribution hello des classes d’étiquette hello qui sera utilisée ultérieurement pour la modélisation de classification multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Exploration : calculer et comparer les distances des trajets
L’exemple suivant convertit la longitude de collecte et de remise hello et latitude tooSQL geography pointe, calcule la distance de voyage hello à l’aide de la différence de points SQL geography et retourne un échantillon aléatoire de résultats hello pour la comparaison. exemple de Hello limite les résultats de hello toovalid coordonne uniquement à l’aide de la requête d’évaluation de la qualité des données d’hello évoqué précédemment.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Conception de fonctionnalités dans des requêtes SQL
Hello étiquette génération geography conversion exploration des requêtes et peuvent également être utilisé toogenerate étiquettes/fonctionnalités en supprimant hello comptage partie. Exemples SQL ingénieries de fonctionnalités supplémentaires sont fournies dans hello [l’Exploration de données et d’ingénierie de fonctionnalité notebooks bloc-notes](#ipnb) section. Il est plus efficace toorun hello fonctionnalités génération de requêtes sur le jeu de données complet hello ou une grande partie de celui-ci à l’aide de requêtes SQL qui s’exécutent directement sur l’instance de base de données SQL Server hello. les requêtes Hello peuvent être exécutées dans **SQL Server Management Studio**, notebooks bloc-notes ou n’importe quel outil/environnement de développement permettant d’accéder à hello de base de données localement ou à distance.

#### <a name="preparing-data-for-model-building"></a>Préparation des données pour la création de modèles
hello de jointures de requête suivant de Hello **nyctaxi\_voyage** et **nyctaxi\_tarif** des tables, génère une étiquette de classification binaire **incliné**, un étiquette de classification multiclasse **Conseil\_classe**et extrait un échantillon aléatoire de 1 % à partir du jeu de données joint hello complète. Cette requête peut être copiée, puis collée directement dans hello [Azure Machine Learning Studio](https://studio.azureml.net) [importer des données] [ import-data] module pour l’ingestion de données directement à partir de la base de données SQL Server hello instance dans Azure. requête de Hello exclut les enregistrements avec incorrect (0, 0) coordonnées.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Exploration des données et conception de fonctionnalités dans Notebook IPython
Dans cette section, nous allons effectuer l’exploration de données et de génération de fonctionnalité à l’aide de requêtes de Python et SQL par rapport à la base de données SQL Server hello créé précédemment. Un bloc-notes de notebooks exemple nommé **machine-Learning-data-science-process-sql-story.ipynb** est fourni dans hello **exemple notebooks Ipython** dossier. Ce notebook est également disponible sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Hello séquence recommandée lors de l’utilisation des données volumineuses est suivant de hello :

* Lire dans un petit échantillon de données de salutation dans une trame de données en mémoire.
* Effectuer des visualisations et à l’aide des explorations hello données échantillonnées.
* Faites l’expérience de l’ingénierie de fonctionnalité à l’aide de hello exemples de données.
* Exploration des données plus volumineux, l’ingénierie de fonctionnalité et de manipulation de données utiliser Python tooissue des requêtes SQL directement sur la base de données SQL Server hello Bonjour Azure VM.
* Décidez toouse de taille d’échantillon hello pour la construction d’un modèle Azure Machine Learning.

Quand vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez soit :  

1. Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning. Cette méthode est illustrée dans hello [création de modèles dans Azure Machine Learning](#mlmodel) section.    
2. Conserver hello échantillonnées et données ingénieries que vous prévoyez toouse pour dans une nouvelle table de base de données de création de modèles, puis utiliser la nouvelle table de hello Bonjour [importer des données] [ import-data] module.

Hello Voici quelques exemples d’ingénierie de fonctionnalité, exploration de données et visualisation des données. Pour plus d’exemples, consultez bloc-notes de SQL notebooks exemple hello Bonjour **exemple notebooks Ipython** dossier.

#### <a name="initialize-database-credentials"></a>Initialiser les informations d’identification de la base de données
Initialiser vos paramètres de connexion de base de données Bonjour suivant variables :

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Créer une connexion à la base de données
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Afficher le nombre de lignes et de colonnes de la table nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Nombre total de lignes = 173 179 759  
* Nombre total de colonnes = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Lecture dans un échantillon de données de petite taille à partir de hello de base de données SQL Server
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Table d’exemple hello temps tooread est 6.492000 secondes  
Nombre de lignes et de colonnes récupérées = (84 952, 21)

#### <a name="descriptive-statistics"></a>Statistiques descriptives
Sont maintenant des données de hello échantillonnée de tooexplore prêt. Nous commençons avec examinant les statistiques descriptives pour hello **voyage\_distance** (ou tout autre) (s) :

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualisation : exemple de diagramme à surfaces
Examinez maintenant surfaces hello pour hello voyage distance toovisualize hello quantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagramme #1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualisation : exemple de diagramme de distribution
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagramme #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualisation : diagrammes en bâtons et linéaires
Dans cet exemple, nous bin distance de voyage hello dans cinq compartiments et visualiser hello placement des résultats.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Nous pouvons tracer hello au-dessus de distribution d’emplacement dans une barre ou de la ligne de traçage comme indiqué ci-dessous

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagramme #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagramme #4][4]

#### <a name="visualization-scatterplot-example"></a>Visualisation : exemple de diagramme de dispersion
Nous allons montrer nuage entre **voyage\_temps\_dans\_secondes** et **voyage\_distance** toosee s’il existe une corrélation

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagramme #6][6]

De même, nous pouvons vérifier relation hello entre **taux\_code** et **voyage\_distance**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagramme #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Hello de sous-échantillonnage données dans SQL
Lorsque vous préparez des données pour le modèle de génération dans [Azure Machine Learning Studio](https://studio.azureml.net), vous pouvez décider soit de hello **toouse de requête SQL directement dans le module d’importation de données hello** ou de les conserver hello conçues et échantillonnées les données dans une nouvelle table, vous pouvez utiliser dans hello [importer des données] [ import-data] module avec un simple **sélectionner * FROM < votre\_nouveau\_table\_nom >**.

Dans cette section, que nous allons créer un nouveau Bonjour de toohold table échantillonnées et conçu des données. Un exemple d’une requête SQL directe pour la génération de modèle est fourni dans hello [l’Exploration de données et d’ingénierie de fonctionnalité dans SQL Server](#dbexplore) section.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Créer un exemple de Table et la remplir avec 1 % des Tables jointes de hello. en commençant par supprimer la table si elle existe
Dans cette section, nous joindre des tables de hello **nyctaxi\_voyage** et **nyctaxi\_tarif**, extraire un échantillon aléatoire de 1 % et conserver les données de hello échantillonnée dans un nouveau nom de table  **nyctaxi\_un\_%**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Exploration des données à l’aide de requêtes SQL dans Notebook IPython
Dans cette section, nous explorons les distributions de données à l’aide des données de 1 % échantillonnée hello qui sont conservées dans hello nouvelle table créée précédemment. Notez que des explorations similaire peuvent être effectuées à l’aide de tables d’origine hello, éventuellement à l’aide de **TABLESAMPLE** toolimit exploration d’hello exemple ou en limitant hello résultats tooa étant donné la période de temps à l’aide de hello **collecte \_datetime** partitions, comme illustré dans hello [l’Exploration de données et d’ingénierie de fonctionnalité dans SQL Server](#dbexplore) section.

#### <a name="exploration-daily-distribution-of-trips"></a>Exploration : distribution quotidienne des courses
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploration : distribution des courses par médaillon
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Génération de fonctionnalités à l’aide de requêtes SQL dans Notebook IPython
Dans cette section, nous allons générer nouvelles étiquettes et fonctionnalités directement à l’aide de requêtes SQL, sur la table de 1 % exemple hello nous avons créé dans la section précédente de hello.

#### <a name="label-generation-generate-class-labels"></a>Génération d’étiquettes : générer des étiquettes de classe
Bonjour l’exemple suivant, nous générons deux ensembles de toouse étiquettes pour la modélisation :

1. Étiquettes de classe binaires **tipped** (prédisant si un pourboire va être versé)
2. Étiquettes multiclasses **Conseil\_classe** (prédiction d’emplacement de conseil hello ou plage)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Conception de fonctionnalités : fonctionnalités de décompte pour les colonnes catégorielles
Cet exemple transforme un champ de catégorie dans un champ numérique en remplaçant chaque catégorie de nombre de hello de ses occurrences dans les données de salutation.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Conception de fonctionnalités : fonctionnalités de compartimentage pour les colonnes numériques
Cet exemple transforme un champ numérique continu en plages de catégories prédéfinies ; autrement dit, il transforme un champ numérique en champ catégoriel.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Conception de fonctionnalités : extraire des fonctionnalités d’emplacement des valeurs décimales de latitude/longitude
Cet exemple décompose hello décimal à un champ de latitude et/ou longitude en plusieurs champs de la région de granularité différente, par exemple, pays, ville, ville, bloc, etc.. Notez que hello nouvelle géo-champs ne sont pas mappées tooactual emplacements. Pour plus d’informations sur le mappage des emplacements associés à un géocode, consultez l’article consacré aux [Services REST de Bing Cartes](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Vérifiez la forme finale de la table de fonctionnalités hello de hello
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Vous voilà prêt tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net). les données de salutation sont prêtes pour un des problèmes de prédiction hello identifiées précédemment, à savoir :

1. Classification binaire : toopredict ou non un Conseil a été payé un voyage.
2. Classification multiclasse : plage de hello toopredict d’info-bulle payé, en fonction de toohello classes précédemment définies.
3. Tâche de régression : toopredict hello d’info-bulle montant d’un voyage.  

## <a name="mlmodel"></a>Création de modèles dans Azure Machine Learning
toobegin hello exercice de modélisation, ouvrez une session dans l’espace de travail Azure Machine Learning tooyour. Si vous n’avez pas encore créé d’espace de travail d’apprentissage automatique, consultez l’article [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget main d’Azure Machine Learning, consultez [Nouveautés d’Azure Machine Learning Studio ?](machine-learning-what-is-ml-studio.md)
2. Connectez-vous trop[Azure Machine Learning Studio](https://studio.azureml.net).
3. page d’accueil Studio Hello fournit une mine d’informations, des vidéos, didacticiels, des liens toohello référence des Modules et autres ressources. Pour plus d’informations sur Azure Machine Learning, consultez hello [centre de Documentation Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Une expérience de formation standard se compose de suivant de hello :

1. Création d’une expérience à l’aide du bouton **+NOUVEAU** .
2. Obtenir hello données tooAzure Machine Learning.
3. Prétraiter, transformer et manipuler des données de hello en fonction des besoins.
4. Génération des fonctionnalités requises.
5. Fractionner les données de hello en jeux de données d’apprentissage/validation/test (ou avoir des jeux de données distincts pour chaque).
6. Sélectionnez un ou plusieurs algorithmes d’apprentissage en fonction de hello toosolve de problème d’apprentissage. Exemples : classification binaire, classification multiclasse, régression.
7. L’apprentissage d’un ou plusieurs modèles à l’aide du jeu de données d’apprentissage hello.
8. Un score de jeu de données de validation hello à l’aide de modèles formés de hello.
9. Évaluer hello ou les modèles toocompute hello mesures pour hello problème d’apprentissage.
10. Réglage de l’ou les modèles hello et sélectionnez hello meilleur modèle toodeploy.

Dans cet exercice, nous avons déjà exploré et conçu données hello dans SQL Server et décidé sur tooingest de taille d’échantillon hello dans Azure Machine Learning. toobuild une ou plusieurs des modèles de prévision hello que nous avons décidé :

1. Obtenir des données de hello tooAzure Machine Learning à l’aide de hello [importer des données] [ import-data] module, disponible dans hello **données d’entrée et sortie** section. Pour plus d’informations, consultez hello [importer des données] [ import-data] page de référence de module.
   
    ![Importation de données Azure Machine Learning][17]
2. Sélectionnez **base de données SQL Azure** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.
3. Entrez le nom DNS de base de données hello Bonjour **nom du serveur de base de données** champ. Format : `tcp:<your_virtual_machine_DNS_name>,1433`
4. Entrez hello **nom de la base de données** dans le champ correspondant de hello.
5. Entrez hello **nom d’utilisateur SQL** Bonjour ** aqccount nom d’utilisateur et mot de passe hello Bonjour **mot de passe utilisateur Server**.
6. Activez l’option **Accepter tout certificat de serveur** .
7. Bonjour **requête de base de données** modifier la zone de texte, collez la requête hello extrait hello nécessaire (y compris les champs calculés tels que des étiquettes de hello) des champs de base de données et le bas exemples de taille d’échantillon hello données toohello souhaité.

Un exemple d’une expérience de classification binaire la lecture des données directement à partir de la base de données SQL Server hello est figure hello ci-dessous. Vous pouvez créer des expériences similaires pour les problèmes de classification multiclasse et de régression.

![Formation Azure Machine Learning Studio][10]

> [!IMPORTANT]
> Bonjour, extraction de données de modélisation et de l’échantillonnage des exemples de requêtes fournis dans les sections précédentes, **toutes les étiquettes pour les exercices de modélisation hello trois sont inclus dans la requête de hello**. Une étape importante (obligatoire) dans chacun des exercices de modélisation de hello est trop**exclure** hello étiquettes inutiles pour hello autres deux problèmes, ainsi que tout autre **cible fuites**. Pour, par exemple, lors de l’utilisation de classification binaire, utiliser hello étiquette **incliné** et exclure les champs hello **Conseil\_classe**, **Conseil\_quantité**, et **total\_quantité**. Hello dernier paiement des fuites de cible, car elles impliquent l’info-bulle hello.
> 
> les colonnes inutiles tooexclude et/ou des fuites de cible, vous pouvez utiliser hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module ou hello [modifier les métadonnées] [ edit-metadata]. Pour plus d’informations, consultez les pages de référence [Sélectionner des colonnes dans le jeu de données][select-columns] et [Modifier les métadonnées][edit-metadata].
> 
> 

## <a name="mldeploy"></a>Déploiement de modèles dans Azure Machine Learning
Lorsque votre modèle est prêt, vous pouvez la déployer facilement en tant qu’un service web directement à partir de l’expérience de hello. Pour plus d’informations sur le déploiement de services web Azure Machine Learning, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nouveau service web, vous devez :

1. créer une expérience de notation ;
2. Déployer un service web de hello.

toocreate une expérience d’un score d’un **terminé** expérience d’apprentissage, cliquez sur **créer une expérience de score** dans la barre d’action hello inférieur.

![Notation Azure][18]

Azure Machine Learning tentera toocreate expérience de score basée sur les composants hello d’expérience de formation hello. Il va notamment :

1. Enregistrer le modèle formé de hello et supprimer des modules de formation du modèle hello.
2. Identifier un opérateur logique **port d’entrée** toorepresent hello attendue de schéma de données d’entrée.
3. Identifier un opérateur logique **port de sortie** schéma de sortie de service toorepresent hello web attendu.

Lors de la création de hello expérience de score, examiner et ajuster en fonction des besoins. Un ajustement standard est tooreplace hello jeu de données d’entrée et/ou de la requête avec l’une qui exclut les champs d’étiquette, car il ne sera pas disponibles lorsque le service de hello est appelé. Il est également qu'une taille de hello tooreduce bonnes pratiques de hello d’entrée tooa de jeu de données et/ou des requêtes peu d’enregistrements, juste assez schéma d’entrée de tooindicate hello. Pour le port de sortie hello, il est commun tooexclude entrées tous les champs et uniquement inclure hello **Scored Labels** et **des probabilités notées** Bonjour de sortie à l’aide de hello [sélectionner les colonnes dans le jeu de données ] [ select-columns] module.

Un exemple d’expérience de score est figure hello ci-dessous. Quand vous êtes prêt toodeploy, cliquez sur hello **publier le SERVICE WEB** bouton dans la barre d’action hello inférieur.

![Publication Azure Machine Learning][11]

toorecap, dans ce didacticiel de la procédure pas à pas, vous avez créé un environnement de science des données Azure, travaillé avec un jeu de données publique volumineux tous les moyen hello de toomodel d’acquisition de données d’apprentissage et de déploiement d’un service web Azure Machine Learning.

### <a name="license-information"></a>Informations de licence
Cet exemple de procédure et accompagne des scripts et des notebooks notebook(s) sont partagées par Microsoft sous licence du MIT hello. Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.

### <a name="references"></a>Références
•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)  
•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
