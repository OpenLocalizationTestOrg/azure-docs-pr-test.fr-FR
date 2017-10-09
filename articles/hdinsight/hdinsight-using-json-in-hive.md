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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="e60ad-103">Traitement et analyse des documents JSON avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="e60ad-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="e60ad-104">Découvrez comment tooprocess et analyser les fichiers JSON à l’aide de la ruche dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e60ad-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="e60ad-105">Hello suivant du document JSON est utilisé dans le didacticiel de hello :</span><span class="sxs-lookup"><span data-stu-id="e60ad-105">hello following JSON document is used in hello tutorial:</span></span>

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

<span data-ttu-id="e60ad-106">Hello fichier se trouve à wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="e60ad-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="e60ad-107">Pour plus d’informations sur l’utilisation du stockage Blob Azure avec HDInsight, consultez la page [Utilisation du stockage d’objets blob Azure compatibles avec HDFS avec Hadoop dans HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e60ad-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="e60ad-108">Vous pouvez copier le conteneur de hello fichier toohello par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="e60ad-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="e60ad-109">Dans ce didacticiel, vous utilisez la console de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="e60ad-110">Pour obtenir des instructions d’ouvrir la console de ruche hello, consultez [utilisez Hive avec Hadoop dans HDInsight avec le Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="e60ad-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="e60ad-111">Aplatir des documents JSON</span><span class="sxs-lookup"><span data-stu-id="e60ad-111">Flatten JSON documents</span></span>
<span data-ttu-id="e60ad-112">les méthodes de Hello répertoriés dans la section suivante de hello requièrent document JSON de hello dans une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="e60ad-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="e60ad-113">Vous devez donc aplatir chaîne de tooa document hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e60ad-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="e60ad-114">Si votre document JSON est déjà aplati, vous pouvez ignorer cette étape et passer des droites toohello la prochaine section sur les données d’analyse de JSON.</span><span class="sxs-lookup"><span data-stu-id="e60ad-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="e60ad-115">Hello fichier JSON brut se trouve dans  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="e60ad-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="e60ad-116">Hello *StudentsRaw* table Hive pointe le document JSON brut aplati toohello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="e60ad-117">Hello *StudentsOneLine* table Hive stocke les données de hello Bonjour HDInsight système de fichiers par défaut sous hello */json/étudiants/* chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="e60ad-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="e60ad-118">instruction INSERT de Hello remplit la table de StudentOneLine de hello avec des données JSON hello aplatie.</span><span class="sxs-lookup"><span data-stu-id="e60ad-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="e60ad-119">instruction SELECT de Hello doit retourner uniquement une ligne.</span><span class="sxs-lookup"><span data-stu-id="e60ad-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="e60ad-120">Voici la sortie hello d’instruction SELECT de hello :</span><span class="sxs-lookup"><span data-stu-id="e60ad-120">Here is hello output of hello SELECT statement:</span></span>

![La mise à plat du document JSON de hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="e60ad-122">Analyser les documents JSON dans Hive</span><span class="sxs-lookup"><span data-stu-id="e60ad-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="e60ad-123">Ruche fournit trois mécanismes différents toorun requêtes sur des documents JSON :</span><span class="sxs-lookup"><span data-stu-id="e60ad-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="e60ad-124">Utilisez hello GET\_JSON\_définie par l’objet (fonction définie par l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="e60ad-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="e60ad-125">Utilisez hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="e60ad-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="e60ad-126">utilisation d’un SerDe personnalisé ;</span><span class="sxs-lookup"><span data-stu-id="e60ad-126">use custom SerDe</span></span>
* <span data-ttu-id="e60ad-127">écriture de votre propre fonction UDF à l’aide de Python ou d’autres langages.</span><span class="sxs-lookup"><span data-stu-id="e60ad-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="e60ad-128">Consultez [cet article][hdinsight-python] consacré à l’exécution de votre propre code Python avec Hive.</span><span class="sxs-lookup"><span data-stu-id="e60ad-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="e60ad-129">Hello d’utilisation GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="e60ad-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="e60ad-130">Hive intègre une fonction UDF appelée [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) qui permet d’exécuter des requêtes sur un document JSON pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e60ad-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="e60ad-131">Cette méthode prend deux arguments : le nom de la table hello et le nom de la méthode a hello aplati JSON document et hello champ JSON qui doit toobe analysée.</span><span class="sxs-lookup"><span data-stu-id="e60ad-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="e60ad-132">Examinons un toosee exemple le fonctionnement de cette UDF.</span><span class="sxs-lookup"><span data-stu-id="e60ad-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="e60ad-133">Obtenir hello prénom et le nom de chaque étudiant</span><span class="sxs-lookup"><span data-stu-id="e60ad-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="e60ad-134">Voici la configuration de sortie hello lors de l’exécution de cette requête dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="e60ad-134">Here is hello output when running this query in console window.</span></span>

![Fonction UDF get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="e60ad-136">Il existe quelques limitations de hello get-json_object UDF.</span><span class="sxs-lookup"><span data-stu-id="e60ad-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="e60ad-137">Étant donné que chaque champ de requête de hello nécessite l’analyse de requête de hello, il affecte les performances de hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="e60ad-138">OBTENIR\_JSON_OBJECT() retourne la représentation sous forme de chaîne hello d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="e60ad-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="e60ad-139">tooconvert ce tableau tooa ruche array, vous avez toouse des expressions régulières tooreplace hello crochets ' [' et ']' et également appel fractionne tableau de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="e60ad-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="e60ad-140">C’est pourquoi hello ruche wiki recommande l’utilisation de json_tuple.</span><span class="sxs-lookup"><span data-stu-id="e60ad-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="e60ad-141">Utilisez hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="e60ad-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="e60ad-142">L’autre fonction UDF fournie par Hive, intitulée [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), est plus performante que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="e60ad-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="e60ad-143">Cette méthode, qui accepte un ensemble de clés et une chaîne JSON, retourne un tuple de valeurs en utilisant une seule fonction.</span><span class="sxs-lookup"><span data-stu-id="e60ad-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="e60ad-144">Hello requête suivante renvoie étudiant hello et niveau de hello depuis un document JSON hello :</span><span class="sxs-lookup"><span data-stu-id="e60ad-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="e60ad-145">sortie Hello de ce script dans la console Hive hello :</span><span class="sxs-lookup"><span data-stu-id="e60ad-145">hello output of this script in hello Hive console:</span></span>

![Fonction UDF json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="e60ad-147">JSON\_TUPLE utilise hello [latérale vue](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntaxe dans la ruche, ce qui permet de json\_tuple toocreate une table virtuelle en appliquant la ligne de tooeach fonction hello UDT de table d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="e60ad-148">L’utilisation de JSON complexe devenir trop complexe en raison de hello répété du mode latéral.</span><span class="sxs-lookup"><span data-stu-id="e60ad-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="e60ad-149">En outre, JSON_TUPLE ne peut pas gérer les documents JSON imbriqués.</span><span class="sxs-lookup"><span data-stu-id="e60ad-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="e60ad-150">Utiliser un SerDe personnalisé</span><span class="sxs-lookup"><span data-stu-id="e60ad-150">Use custom SerDe</span></span>
<span data-ttu-id="e60ad-151">SerDe est hello meilleur choix pour l’analyse des documents JSON imbriquées, il vous permet de schéma JSON toodefine hello et utilisez hello schéma tooparse hello documents.</span><span class="sxs-lookup"><span data-stu-id="e60ad-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="e60ad-152">Dans ce didacticiel, vous utilisez une de hello plus populaire SerDe qui a été développé par [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="e60ad-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="e60ad-153">**toouse hello SerDe personnalisé :**</span><span class="sxs-lookup"><span data-stu-id="e60ad-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="e60ad-154">Installez le [JDK 1.7.0_55 du Kit de développement SE Java 7u55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="e60ad-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="e60ad-155">Choisissez la version de Windows X64 hello Hello JDK si vous vous apprêtez à l’aide du déploiement de Windows hello de HDInsight de toobe</span><span class="sxs-lookup"><span data-stu-id="e60ad-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="e60ad-156">Le JDK 1.8 ne fonctionne pas avec ce SerDe.</span><span class="sxs-lookup"><span data-stu-id="e60ad-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="e60ad-157">Après que l’installation de hello est terminée, ajoutez une variable d’environnement utilisateur :</span><span class="sxs-lookup"><span data-stu-id="e60ad-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="e60ad-158">Ouvrez **afficher les paramètres système avancés** à partir de l’écran de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="e60ad-159">Cliquez sur **Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="e60ad-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="e60ad-160">Ajouter un nouveau **JAVA_HOME** pointe trop de la variable d’environnement**C:\Program Files\Java\jdk1.7.0_55** ou partout où votre JDK est installé.</span><span class="sxs-lookup"><span data-stu-id="e60ad-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Définition de valeurs de configuration correctes pour JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="e60ad-162">Installer [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="e60ad-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="e60ad-163">Ajoutez le chemin d’accès de hello bin dossier tooyour en accédant tooControl Panneau de configuration--> modifier hello les Variables système pour les variables d’environnement de votre compte.</span><span class="sxs-lookup"><span data-stu-id="e60ad-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="e60ad-164">Hello capture d’écran suivante montre comment toodo cela.</span><span class="sxs-lookup"><span data-stu-id="e60ad-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Configuration de Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="e60ad-166">Projet à partir de clone hello [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) site github.</span><span class="sxs-lookup"><span data-stu-id="e60ad-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="e60ad-167">Pour cela, en cliquant sur le bouton de « Zip de téléchargement » hello, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="e60ad-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Projet de clonage de hello][image-hdi-hivejson-serde]

<span data-ttu-id="e60ad-169">4 : dossier de toohello go dans lequel vous avez téléchargé ce package et type « mvn package ».</span><span class="sxs-lookup"><span data-stu-id="e60ad-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="e60ad-170">Cela doit créer hello fichiers jar nécessaires que vous pouvez ensuite copier sur le cluster de toohello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="e60ad-171">5 : dossier de cible go toohello sous le dossier racine de hello où vous avez téléchargé le package de hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="e60ad-172">Télécharger le fichier json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nœud de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="e60ad-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="e60ad-173">J’ai généralement placer sous le dossier binaire de la ruche hello : C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin ou quelque chose de similaire.</span><span class="sxs-lookup"><span data-stu-id="e60ad-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="e60ad-174">6 : invite de commandes hello hive, tapez « ajouter le jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar ».</span><span class="sxs-lookup"><span data-stu-id="e60ad-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="e60ad-175">Étant donné que dans mon cas, jar de hello est dans le dossier de C:\apps\dist\hive-0.13.x\bin hello, puis-je ajouter directement jar hello avec nom hello comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="e60ad-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Ajout de fichier JAR tooyour projet][image-hdi-hivejson-addjar]

<span data-ttu-id="e60ad-177">Vous êtes maintenant prêt toouse hello SerDe toorun des requêtes par rapport au document JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="e60ad-178">Hello après l’instruction crée une table avec un schéma défini :</span><span class="sxs-lookup"><span data-stu-id="e60ad-178">hello following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="e60ad-179">toolist hello prénom et nom de hello étudiant</span><span class="sxs-lookup"><span data-stu-id="e60ad-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="e60ad-180">Voici le résultat de hello à partir de la console de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-180">Here is hello result from hello Hive console.</span></span>

![Requête SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="e60ad-182">somme de hello toocalculate de scores de document JSON de hello</span><span class="sxs-lookup"><span data-stu-id="e60ad-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="e60ad-183">Hello précédant la requête utilise [vue latéral éclater](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello tableau des scores afin qu’ils peuvent être additionnés.</span><span class="sxs-lookup"><span data-stu-id="e60ad-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="e60ad-184">Voici la sortie hello à partir de la console de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="e60ad-184">Here is hello output from hello Hive console.</span></span>

![Requête SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="e60ad-186">toofind qui soumet un étudiant donné a notées plus de 80 points :</span><span class="sxs-lookup"><span data-stu-id="e60ad-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="e60ad-187">Hello requête précédente retourne un tableau de ruche Contrairement à get\_json\_objet, qui retourne une chaîne.</span><span class="sxs-lookup"><span data-stu-id="e60ad-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Requête SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="e60ad-189">Si vous souhaitez tooskil JSON incorrect, puis, comme expliqué dans hello [page wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de cette SerDe vous pouvez effectuer cette en tapant hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e60ad-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="e60ad-190">Résumé</span><span class="sxs-lookup"><span data-stu-id="e60ad-190">Summary</span></span>
<span data-ttu-id="e60ad-191">En conclusion, hello type d’opérateur JSON dans la ruche que vous choisissez dépend de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="e60ad-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="e60ad-192">Si vous avez un document JSON simple et vous avez uniquement un champ toolook – vous pouvez choisir toouse hello UDF de la ruche get\_json\_objet.</span><span class="sxs-lookup"><span data-stu-id="e60ad-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="e60ad-193">Si vous avez plusieurs toolook clé, vous pouvez ensuite utiliser json_tuple.</span><span class="sxs-lookup"><span data-stu-id="e60ad-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="e60ad-194">Si vous avez un document imbriqué, vous devez utiliser hello SerDe de JSON.</span><span class="sxs-lookup"><span data-stu-id="e60ad-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e60ad-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e60ad-195">Next steps</span></span>

<span data-ttu-id="e60ad-196">Autres articles associés :</span><span class="sxs-lookup"><span data-stu-id="e60ad-196">For other related articles, see</span></span>

* [<span data-ttu-id="e60ad-197">Utilisez Hive et HiveQL avec Hadoop dans HDInsight tooanalyze un exemple de fichier log4j Apache</span><span class="sxs-lookup"><span data-stu-id="e60ad-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e60ad-198">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="e60ad-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="e60ad-199">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="e60ad-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="e60ad-200">Exécution d’une tâche Hadoop avec Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="e60ad-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
