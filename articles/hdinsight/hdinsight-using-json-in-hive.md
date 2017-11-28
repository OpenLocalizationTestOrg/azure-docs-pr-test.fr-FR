---
title: Analyser et traiter des documents JSON avec Hive dans HDInsight | Microsoft Docs
description: "Découvrez comment utiliser des documents JSON et les analyser avec Hive dans HDInsight."
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
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="c361d-103">Traitement et analyse des documents JSON avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c361d-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="c361d-104">Apprenez à traiter et analyser les fichiers JSON à l’aide de Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c361d-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="c361d-105">Le document JSON suivant sera utilisé dans le tutoriel :</span><span class="sxs-lookup"><span data-stu-id="c361d-105">The following JSON document is used in the tutorial:</span></span>

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

<span data-ttu-id="c361d-106">Le fichier se trouve à l’emplacement suivant : wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="c361d-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="c361d-107">Pour plus d’informations sur l’utilisation du stockage Blob Azure avec HDInsight, consultez la page [Utilisation du stockage d’objets blob Azure compatibles avec HDFS avec Hadoop dans HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c361d-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="c361d-108">Vous pouvez copier le fichier dans le conteneur par défaut de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c361d-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="c361d-109">Dans ce tutoriel, vous allez utiliser la console Hive.</span><span class="sxs-lookup"><span data-stu-id="c361d-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="c361d-110">Pour obtenir des instructions sur l’ouverture de la console Hive, consultez la page [Utilisation de Hive avec Hadoop sur HDInsight avec le Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="c361d-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="c361d-111">Aplatir des documents JSON</span><span class="sxs-lookup"><span data-stu-id="c361d-111">Flatten JSON documents</span></span>
<span data-ttu-id="c361d-112">Les méthodes répertoriées dans la section suivante nécessitent que le document JSON n’occupe qu’une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="c361d-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="c361d-113">Par conséquent, vous devez aplatir le document JSON en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="c361d-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="c361d-114">Si votre document JSON est déjà aplati et que l’ensemble du document tient sur une ligne, vous pouvez ignorer cette étape et passer directement à la section suivante sur l’analyse des données JSON.</span><span class="sxs-lookup"><span data-stu-id="c361d-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="c361d-115">Le fichier JSON brut se trouve à l’emplacement suivant : **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="c361d-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="c361d-116">La table Hive *StudentsRaw* pointe vers le document JSON brut non aplati.</span><span class="sxs-lookup"><span data-stu-id="c361d-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="c361d-117">La table Hive *StudentsOneLine* stocke les données dans le système de fichiers HDInsight par défaut sous le chemin d’accès */json/students/*.</span><span class="sxs-lookup"><span data-stu-id="c361d-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="c361d-118">L’instruction INSERT remplit la table StudentOneLine avec les données JSON aplaties.</span><span class="sxs-lookup"><span data-stu-id="c361d-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="c361d-119">L’instruction SELECT retourne seulement 1 ligne.</span><span class="sxs-lookup"><span data-stu-id="c361d-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="c361d-120">Voici la sortie de l’instruction SELECT :</span><span class="sxs-lookup"><span data-stu-id="c361d-120">Here is the output of the SELECT statement:</span></span>

![Aplatissage du document JSON][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="c361d-122">Analyser les documents JSON dans Hive</span><span class="sxs-lookup"><span data-stu-id="c361d-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="c361d-123">Hive propose trois mécanismes différents pour exécuter des requêtes sur des documents JSON :</span><span class="sxs-lookup"><span data-stu-id="c361d-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="c361d-124">utilisation de la fonction définie par l’utilisateur GET\_JSON\_OBJECT ;</span><span class="sxs-lookup"><span data-stu-id="c361d-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="c361d-125">utilisation de la fonction UDF JSON_TUPLE ;</span><span class="sxs-lookup"><span data-stu-id="c361d-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="c361d-126">utilisation d’un SerDe personnalisé ;</span><span class="sxs-lookup"><span data-stu-id="c361d-126">use custom SerDe</span></span>
* <span data-ttu-id="c361d-127">écriture de votre propre fonction UDF à l’aide de Python ou d’autres langages.</span><span class="sxs-lookup"><span data-stu-id="c361d-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="c361d-128">Consultez [cet article][hdinsight-python] consacré à l’exécution de votre propre code Python avec Hive.</span><span class="sxs-lookup"><span data-stu-id="c361d-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="c361d-129">Utiliser la fonction UDF GET\_JSON_OBJECT</span><span class="sxs-lookup"><span data-stu-id="c361d-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="c361d-130">Hive intègre une fonction UDF appelée [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) qui permet d’exécuter des requêtes sur un document JSON pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="c361d-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="c361d-131">Cette méthode accepte deux arguments : d’une part, le nom de la table et le nom de la méthode contenant le document JSON aplati et, d’autre part, le champ JSON à analyser.</span><span class="sxs-lookup"><span data-stu-id="c361d-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="c361d-132">Prenons un exemple pour examiner de plus près cette fonction UDF.</span><span class="sxs-lookup"><span data-stu-id="c361d-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="c361d-133">Obtenir le prénom et le nom de chaque élève</span><span class="sxs-lookup"><span data-stu-id="c361d-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="c361d-134">Voici la sortie de cette requête dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="c361d-134">Here is the output when running this query in console window.</span></span>

![Fonction UDF get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="c361d-136">La fonction UDF get-json_object présente quelques limitations.</span><span class="sxs-lookup"><span data-stu-id="c361d-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="c361d-137">Étant donné que chaque champ de la requête requiert une nouvelle analyse de la requête, cela influe sur les performances.</span><span class="sxs-lookup"><span data-stu-id="c361d-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="c361d-138">GET\_JSON_OBJECT() retourne une représentation sous forme de chaîne d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="c361d-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="c361d-139">Pour convertir cette dernière en tableau Hive, vous devez utiliser des expressions régulières pour remplacer les crochets « [ » et « ] », puis appeler split pour obtenir le tableau.</span><span class="sxs-lookup"><span data-stu-id="c361d-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="c361d-140">C’est pourquoi le wiki Hive recommande l’utilisation de json_tuple.</span><span class="sxs-lookup"><span data-stu-id="c361d-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="c361d-141">Utiliser la fonction UDF JSON_TUPLE</span><span class="sxs-lookup"><span data-stu-id="c361d-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="c361d-142">L’autre fonction UDF fournie par Hive, intitulée [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), est plus performante que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="c361d-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="c361d-143">Cette méthode, qui accepte un ensemble de clés et une chaîne JSON, retourne un tuple de valeurs en utilisant une seule fonction.</span><span class="sxs-lookup"><span data-stu-id="c361d-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="c361d-144">La requête suivante renvoie l’ID de l'étudiant et la qualité du document JSON :</span><span class="sxs-lookup"><span data-stu-id="c361d-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="c361d-145">Sortie de ce script dans la console Hive :</span><span class="sxs-lookup"><span data-stu-id="c361d-145">The output of this script in the Hive console:</span></span>

![Fonction UDF json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="c361d-147">JSON\_TUPLE utilise la syntaxe [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) dans Hive, ce qui permet à json\_tuple de créer une table virtuelle en appliquant la fonction UDT à chaque ligne de la table d’origine.</span><span class="sxs-lookup"><span data-stu-id="c361d-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="c361d-148">Les documents JSON deviennent trop complexes en raison de l’utilisation répétée de LATERAL VIEW.</span><span class="sxs-lookup"><span data-stu-id="c361d-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="c361d-149">En outre, JSON_TUPLE ne peut pas gérer les documents JSON imbriqués.</span><span class="sxs-lookup"><span data-stu-id="c361d-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="c361d-150">Utiliser un SerDe personnalisé</span><span class="sxs-lookup"><span data-stu-id="c361d-150">Use custom SerDe</span></span>
<span data-ttu-id="c361d-151">SerDe est le meilleur choix pour l’analyse des documents JSON imbriqués ; il vous permet de définir le schéma JSON et de l’utiliser pour analyser les documents.</span><span class="sxs-lookup"><span data-stu-id="c361d-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="c361d-152">Dans ce tutoriel, vous allez utiliser l’un des SerDe les plus populaires développés par [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="c361d-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="c361d-153">**Pour utiliser le SerDe personnalisé :**</span><span class="sxs-lookup"><span data-stu-id="c361d-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="c361d-154">Installez le [JDK 1.7.0_55 du Kit de développement SE Java 7u55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="c361d-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="c361d-155">Si vous envisagez d’utiliser le déploiement Windows de HDInsight, choisissez la version Windows X64 du JDK.</span><span class="sxs-lookup"><span data-stu-id="c361d-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="c361d-156">Le JDK 1.8 ne fonctionne pas avec ce SerDe.</span><span class="sxs-lookup"><span data-stu-id="c361d-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="c361d-157">Une fois l'installation terminée, ajoutez une nouvelle variable d’environnement utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c361d-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="c361d-158">Ouvrez **Afficher les paramètres système avancés** à partir de l’écran de Windows.</span><span class="sxs-lookup"><span data-stu-id="c361d-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="c361d-159">Cliquez sur **Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="c361d-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="c361d-160">Ajoutez une nouvelle variable d’environnement **JAVA_HOME** pointant vers **C:\Program Files\Java\jdk1.7.0_55** ou vers l’emplacement où est installé votre JDK.</span><span class="sxs-lookup"><span data-stu-id="c361d-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Définition de valeurs de configuration correctes pour JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="c361d-162">Installer [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="c361d-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="c361d-163">Ajoutez le dossier bin à votre chemin d’accès. Pour cela, accédez à Panneau de configuration --> Modifier les variables d’environnement système --> Variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="c361d-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="c361d-164">La capture d’écran ci-dessous montre comment effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="c361d-164">The following screenshot shows you how to do this.</span></span>
   
    ![Configuration de Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="c361d-166">Clonez le projet à partir du site github [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) .</span><span class="sxs-lookup"><span data-stu-id="c361d-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="c361d-167">Pour cela, cliquez sur le bouton « Download Zip » illustré dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c361d-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![Clonage du projet][image-hdi-hivejson-serde]

<span data-ttu-id="c361d-169">4: Accédez au dossier dans lequel vous avez téléchargé ce package, puis tapez « mvn package ».</span><span class="sxs-lookup"><span data-stu-id="c361d-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="c361d-170">Cette action doit créer les fichiers jar nécessaires que vous pouvez ensuite copier dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="c361d-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="c361d-171">5: Accédez au dossier cible sous le dossier racine dans lequel vous avez téléchargé le package.</span><span class="sxs-lookup"><span data-stu-id="c361d-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="c361d-172">Téléchargez le fichier json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar dans le nœud principal de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c361d-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="c361d-173">En général, je le mets dans le dossier binaire Hive (C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin) ou un dossier semblable.</span><span class="sxs-lookup"><span data-stu-id="c361d-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="c361d-174">6: À l’invite Hive, tapez «add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.ja».</span><span class="sxs-lookup"><span data-stu-id="c361d-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="c361d-175">Étant donné que dans le cas présent, le fichier jar se trouve dans le dossier C:\apps\dist\hive-0.13.x\bin, je peux ajouter le jar directement avec le nom comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="c361d-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Ajout de JAR à votre projet][image-hdi-hivejson-addjar]

<span data-ttu-id="c361d-177">Vous pouvez dorénavant utiliser le SerDe pour exécuter des requêtes sur le document JSON.</span><span class="sxs-lookup"><span data-stu-id="c361d-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="c361d-178">L’instruction suivante crée une table avec un schéma défini :</span><span class="sxs-lookup"><span data-stu-id="c361d-178">The following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="c361d-179">Pour répertorier le prénom et le nom de l’élève</span><span class="sxs-lookup"><span data-stu-id="c361d-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="c361d-180">Voici le résultat de la console Hive.</span><span class="sxs-lookup"><span data-stu-id="c361d-180">Here is the result from the Hive console.</span></span>

![Requête SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="c361d-182">Pour calculer la somme des scores du document JSON</span><span class="sxs-lookup"><span data-stu-id="c361d-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="c361d-183">La requête ci-dessus utilise la fonction définie par l’utilisateur [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) pour développer le tableau des scores afin qu’ils puissent être additionnés.</span><span class="sxs-lookup"><span data-stu-id="c361d-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="c361d-184">Voici la sortie de la console Hive.</span><span class="sxs-lookup"><span data-stu-id="c361d-184">Here is the output from the Hive console.</span></span>

![Requête SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="c361d-186">Pour trouver les sujets sur lesquels un étudiant donné a obtenu plus de 80 points :</span><span class="sxs-lookup"><span data-stu-id="c361d-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="c361d-187">Contrairement à get\_json\_object qui retourne une chaîne, la requête ci-dessus retourne un tableau Hive.</span><span class="sxs-lookup"><span data-stu-id="c361d-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Requête SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="c361d-189">Si vous souhaitez ignorer le code JSON mal formé, comme l’explique la [page wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de ce SerDe, vous pouvez taper le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c361d-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="c361d-190">Résumé</span><span class="sxs-lookup"><span data-stu-id="c361d-190">Summary</span></span>
<span data-ttu-id="c361d-191">En conclusion, le type d'opérateur JSON que vous choisissez dans Hive dépend de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="c361d-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="c361d-192">Si vous possédez un document JSON simple et que votre recherche ne porte que sur un seul champ, vous pouvez utiliser la fonction UDF Hive get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="c361d-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="c361d-193">Si la recherche porte sur plusieurs clés, vous pouvez utiliser json_tuple.</span><span class="sxs-lookup"><span data-stu-id="c361d-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="c361d-194">Enfin, si vous disposez d'un document imbriqué, il est recommandé d'utiliser le SerDe JSON.</span><span class="sxs-lookup"><span data-stu-id="c361d-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c361d-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c361d-195">Next steps</span></span>

<span data-ttu-id="c361d-196">Autres articles associés :</span><span class="sxs-lookup"><span data-stu-id="c361d-196">For other related articles, see</span></span>

* [<span data-ttu-id="c361d-197">Utilisation de Hive et HiveQL avec Hadoop dans HDInsight pour l’analyse d’un exemple de fichier Apache log4j</span><span class="sxs-lookup"><span data-stu-id="c361d-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c361d-198">Analyse des données sur les retards de vol avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c361d-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="c361d-199">Analyse des données Twitter avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c361d-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="c361d-200">Exécution d’une tâche Hadoop avec Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="c361d-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
