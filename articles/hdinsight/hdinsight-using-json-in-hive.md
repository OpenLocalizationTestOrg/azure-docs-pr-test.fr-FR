---
title: aaaAnalyze et processus JSON documents avec Hive dans HDInsight | Documents Microsoft
description: "Découvrez comment toouse JSON documents et les analyser à l’aide de la ruche dans HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Traitement et analyse des documents JSON avec Hive dans HDInsight

Découvrez comment tooprocess et analyser les fichiers JSON à l’aide de la ruche dans HDInsight. Hello suivant du document JSON est utilisé dans le didacticiel de hello :

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

Hello fichier se trouve à wasb://processjson@hditutorialdata.blob.core.windows.net/. Pour plus d’informations sur l’utilisation du stockage Blob Azure avec HDInsight, consultez la page [Utilisation du stockage d’objets blob Azure compatibles avec HDFS avec Hadoop dans HDInsight](hdinsight-hadoop-use-blob-storage.md). Vous pouvez copier le conteneur de hello fichier toohello par défaut de votre cluster.

Dans ce didacticiel, vous utilisez la console de ruche hello.  Pour obtenir des instructions d’ouvrir la console de ruche hello, consultez [utilisez Hive avec Hadoop dans HDInsight avec le Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Aplatir des documents JSON
les méthodes de Hello répertoriés dans la section suivante de hello requièrent document JSON de hello dans une seule ligne. Vous devez donc aplatir chaîne de tooa document hello JSON. Si votre document JSON est déjà aplati, vous pouvez ignorer cette étape et passer des droites toohello la prochaine section sur les données d’analyse de JSON.

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

Hello fichier JSON brut se trouve dans  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Hello *StudentsRaw* table Hive pointe le document JSON brut aplati toohello.

Hello *StudentsOneLine* table Hive stocke les données de hello Bonjour HDInsight système de fichiers par défaut sous hello */json/étudiants/* chemin d’accès.

instruction INSERT de Hello remplit la table de StudentOneLine de hello avec des données JSON hello aplatie.

instruction SELECT de Hello doit retourner uniquement une ligne.

Voici la sortie hello d’instruction SELECT de hello :

![La mise à plat du document JSON de hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Analyser les documents JSON dans Hive
Ruche fournit trois mécanismes différents toorun requêtes sur des documents JSON :

* Utilisez hello GET\_JSON\_définie par l’objet (fonction définie par l’utilisateur)
* Utilisez hello JSON_TUPLE UDF
* utilisation d’un SerDe personnalisé ;
* écriture de votre propre fonction UDF à l’aide de Python ou d’autres langages. Consultez [cet article][hdinsight-python] consacré à l’exécution de votre propre code Python avec Hive.

### <a name="use-hello-getjsonobject-udf"></a>Hello d’utilisation GET\_JSON_OBJECT UDF
Hive intègre une fonction UDF appelée [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) qui permet d’exécuter des requêtes sur un document JSON pendant l’exécution. Cette méthode prend deux arguments : le nom de la table hello et le nom de la méthode a hello aplati JSON document et hello champ JSON qui doit toobe analysée. Examinons un toosee exemple le fonctionnement de cette UDF.

Obtenir hello prénom et le nom de chaque étudiant

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Voici la configuration de sortie hello lors de l’exécution de cette requête dans la fenêtre de console.

![Fonction UDF get_json_object][image-hdi-hivejson-getjsonobject]

Il existe quelques limitations de hello get-json_object UDF.

* Étant donné que chaque champ de requête de hello nécessite l’analyse de requête de hello, il affecte les performances de hello.
* OBTENIR\_JSON_OBJECT() retourne la représentation sous forme de chaîne hello d’un tableau. tooconvert ce tableau tooa ruche array, vous avez toouse des expressions régulières tooreplace hello crochets ' [' et ']' et également appel fractionne tableau de hello tooget.

C’est pourquoi hello ruche wiki recommande l’utilisation de json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Utilisez hello JSON_TUPLE UDF
L’autre fonction UDF fournie par Hive, intitulée [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), est plus performante que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Cette méthode, qui accepte un ensemble de clés et une chaîne JSON, retourne un tuple de valeurs en utilisant une seule fonction. Hello requête suivante renvoie étudiant hello et niveau de hello depuis un document JSON hello :

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

sortie Hello de ce script dans la console Hive hello :

![Fonction UDF json_tuple][image-hdi-hivejson-jsontuple]

JSON\_TUPLE utilise hello [latérale vue](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntaxe dans la ruche, ce qui permet de json\_tuple toocreate une table virtuelle en appliquant la ligne de tooeach fonction hello UDT de table d’origine de hello.  L’utilisation de JSON complexe devenir trop complexe en raison de hello répété du mode latéral. En outre, JSON_TUPLE ne peut pas gérer les documents JSON imbriqués.

### <a name="use-custom-serde"></a>Utiliser un SerDe personnalisé
SerDe est hello meilleur choix pour l’analyse des documents JSON imbriquées, il vous permet de schéma JSON toodefine hello et utilisez hello schéma tooparse hello documents. Dans ce didacticiel, vous utilisez une de hello plus populaire SerDe qui a été développé par [Roberto Congiu](https://github.com/rcongiu).

**toouse hello SerDe personnalisé :**

1. Installez le [JDK 1.7.0_55 du Kit de développement SE Java 7u55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Choisissez la version de Windows X64 hello Hello JDK si vous vous apprêtez à l’aide du déploiement de Windows hello de HDInsight de toobe
   
   > [!WARNING]
   > Le JDK 1.8 ne fonctionne pas avec ce SerDe.
   > 
   > 
   
    Après que l’installation de hello est terminée, ajoutez une variable d’environnement utilisateur :
   
   1. Ouvrez **afficher les paramètres système avancés** à partir de l’écran de Windows hello.
   2. Cliquez sur **Variables d’environnement**.  
   3. Ajouter un nouveau **JAVA_HOME** pointe trop de la variable d’environnement**C:\Program Files\Java\jdk1.7.0_55** ou partout où votre JDK est installé.
      
      ![Définition de valeurs de configuration correctes pour JDK][image-hdi-hivejson-jdk]
2. Installer [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Ajoutez le chemin d’accès de hello bin dossier tooyour en accédant tooControl Panneau de configuration--> modifier hello les Variables système pour les variables d’environnement de votre compte. Hello capture d’écran suivante montre comment toodo cela.
   
    ![Configuration de Maven][image-hdi-hivejson-maven]
3. Projet à partir de clone hello [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) site github. Pour cela, en cliquant sur le bouton de « Zip de téléchargement » hello, comme indiqué dans hello suivant capture d’écran.
   
    ![Projet de clonage de hello][image-hdi-hivejson-serde]

4 : dossier de toohello go dans lequel vous avez téléchargé ce package et type « mvn package ». Cela doit créer hello fichiers jar nécessaires que vous pouvez ensuite copier sur le cluster de toohello.

5 : dossier de cible go toohello sous le dossier racine de hello où vous avez téléchargé le package de hello. Télécharger le fichier json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nœud de votre cluster. J’ai généralement placer sous le dossier binaire de la ruche hello : C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin ou quelque chose de similaire.

6 : invite de commandes hello hive, tapez « ajouter le jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar ». Étant donné que dans mon cas, jar de hello est dans le dossier de C:\apps\dist\hive-0.13.x\bin hello, puis-je ajouter directement jar hello avec nom hello comme indiqué :

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Ajout de fichier JAR tooyour projet][image-hdi-hivejson-addjar]

Vous êtes maintenant prêt toouse hello SerDe toorun des requêtes par rapport au document JSON de hello.

Hello après l’instruction crée une table avec un schéma défini :

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello prénom et nom de hello étudiant

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Voici le résultat de hello à partir de la console de ruche hello.

![Requête SerDe 1][image-hdi-hivejson-serde_query1]

somme de hello toocalculate de scores de document JSON de hello

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Hello précédant la requête utilise [vue latéral éclater](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello tableau des scores afin qu’ils peuvent être additionnés.

Voici la sortie hello à partir de la console de ruche hello.

![Requête SerDe 2][image-hdi-hivejson-serde_query2]

toofind qui soumet un étudiant donné a notées plus de 80 points :

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Hello requête précédente retourne un tableau de ruche Contrairement à get\_json\_objet, qui retourne une chaîne.

![Requête SerDe 3][image-hdi-hivejson-serde_query3]

Si vous souhaitez tooskil JSON incorrect, puis, comme expliqué dans hello [page wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de cette SerDe vous pouvez effectuer cette en tapant hello suivant de code :  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Résumé
En conclusion, hello type d’opérateur JSON dans la ruche que vous choisissez dépend de votre scénario. Si vous avez un document JSON simple et vous avez uniquement un champ toolook – vous pouvez choisir toouse hello UDF de la ruche get\_json\_objet. Si vous avez plusieurs toolook clé, vous pouvez ensuite utiliser json_tuple. Si vous avez un document imbriqué, vous devez utiliser hello SerDe de JSON.

## <a name="next-steps"></a>Étapes suivantes

Autres articles associés :

* [Utilisez Hive et HiveQL avec Hadoop dans HDInsight tooanalyze un exemple de fichier log4j Apache](hdinsight-use-hive.md)
* [Analyse des données sur les retards de vol avec Hive dans HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analyse des données Twitter avec Hive dans HDInsight](hdinsight-analyze-twitter-data.md)
* [Exécution d’une tâche Hadoop avec Azure Cosmos DB et HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
