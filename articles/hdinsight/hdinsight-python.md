---
title: aaaPython UDF avec Apache Hive et Pig - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Python utilisateur défini par les fonctions (UDF) à partir de Hive et Pig dans HDInsight, hello Hadoop technologie de pile sur Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="9bec7-103">Utiliser des fonctions définies par l’utilisateur (UDF) Python avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bec7-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="9bec7-104">Découvrez comment toouse Python défini par l’utilisateur (UDF) de fonctions avec Apache Hive et Pig dans Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9bec7-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="9bec7-105"><a name="python"></a>Python sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bec7-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="9bec7-106">Python 2.7 est installé par défaut sur HDInsight 3.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9bec7-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="9bec7-107">Apache Hive peut être utilisé avec cette version de Python pour traiter les flux de données.</span><span class="sxs-lookup"><span data-stu-id="9bec7-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="9bec7-108">Le traitement des flux de données utilise les données de toopass STDOUT et STDIN entre Hive et hello UDF.</span><span class="sxs-lookup"><span data-stu-id="9bec7-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="9bec7-109">HDInsight inclut également Jython, une implémentation de Python écrite en Java.</span><span class="sxs-lookup"><span data-stu-id="9bec7-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="9bec7-110">Jython s’exécute directement sur la Machine virtuelle Java de hello et n’utilise pas de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="9bec7-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="9bec7-111">Jython est recommandé de hello interpréteur Python lors de l’utilisation de Python avec Pig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="9bec7-112">étapes Hello dans ce document apporter hello suivant hypothèses :</span><span class="sxs-lookup"><span data-stu-id="9bec7-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="9bec7-113">Vous créez des scripts Python hello sur votre environnement de développement local.</span><span class="sxs-lookup"><span data-stu-id="9bec7-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="9bec7-114">Vous téléchargez hello tooHDInsight de scripts à l’aide soit hello `scp` commande d’une session d’interpréteur de commandes locale ou d’hello fourni de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bec7-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="9bec7-115">Si vous souhaitez toouse hello [Azure Cloud Shell (interpréteur de commandes)](https://docs.microsoft.com/azure/cloud-shell/overview) aperçu toowork avec HDInsight, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9bec7-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="9bec7-116">Créer des scripts à l’intérieur d’environnement du shell hello cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="9bec7-117">Utilisez `scp` fichiers hello tooupload hello cloud tooHDInsight d’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="9bec7-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="9bec7-118">Utilisez `ssh` hello cloud shell tooconnect tooHDInsight des exemples d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="9bec7-119"><a name="hivepython"></a>UDF Hive</span><span class="sxs-lookup"><span data-stu-id="9bec7-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="9bec7-120">Python peut être utilisé comme un fichier UDF à partir de la ruche via hello HiveQL `TRANSFORM` instruction.</span><span class="sxs-lookup"><span data-stu-id="9bec7-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="9bec7-121">Par exemple, hello suivant HiveQL appelle hello `hiveudf.py` fichier stocké dans le compte de stockage Azure hello par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="9bec7-122">**HDInsight Linux**</span><span class="sxs-lookup"><span data-stu-id="9bec7-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="9bec7-123">**HDInsight Windows**</span><span class="sxs-lookup"><span data-stu-id="9bec7-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="9bec7-124">Sur les clusters HDInsight de basés sur Windows, hello `USING` clause doit spécifier hello chemin d’accès complet toopython.exe.</span><span class="sxs-lookup"><span data-stu-id="9bec7-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="9bec7-125">Cet exemple effectue ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9bec7-125">Here's what this example does:</span></span>

1. <span data-ttu-id="9bec7-126">Hello `add file` instruction au début de hello du fichier de hello ajoute hello `hiveudf.py` fichier toohello distributed cache, afin qu’il soit accessible par tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="9bec7-127">Hello `SELECT TRANSFORM ... USING` instruction sélectionne des données à partir de hello `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="9bec7-128">Il passe également hello clientid, devicemake et devicemodel valeurs toohello `hiveudf.py` script.</span><span class="sxs-lookup"><span data-stu-id="9bec7-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="9bec7-129">Hello `AS` clause décrit les champs hello retournés à partir de `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="9bec7-130">Créer le fichier de hiveudf.py hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="9bec7-131">Sur votre environnement de développement, créez un fichier texte nommé `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="9bec7-132">Utilisez hello après le code en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="9bec7-132">Use hello following code as hello contents of hello file:</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="9bec7-133">Ce script effectue hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="9bec7-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="9bec7-134">Une ligne de données de STDIN est lue.</span><span class="sxs-lookup"><span data-stu-id="9bec7-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="9bec7-135">Hello caractère de saut de ligne de fin est supprimé à l’aide de `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="9bec7-136">Lorsque vous effectuez le traitement de flux, une seule ligne contient toutes les valeurs de hello avec un caractère de tabulation entre chaque valeur.</span><span class="sxs-lookup"><span data-stu-id="9bec7-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="9bec7-137">Par conséquent, `string.split(line, "\t")` peut être hello toosplit utilisé entrée à chaque onglet, en retournant uniquement les champs hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="9bec7-138">Lorsque le traitement est terminé, la sortie hello doit être écrite tooSTDOUT comme une ligne unique, avec un onglet entre chaque champ.</span><span class="sxs-lookup"><span data-stu-id="9bec7-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="9bec7-139">Par exemple, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="9bec7-140">Hello `while` boucle se répète jusqu'à ce que non `line` est en lecture.</span><span class="sxs-lookup"><span data-stu-id="9bec7-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="9bec7-141">sortie du script Hello est une concaténation des valeurs d’entrée de hello pour `devicemake` et `devicemodel`, et un hachage de hello la valeur concaténée.</span><span class="sxs-lookup"><span data-stu-id="9bec7-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="9bec7-142">Consultez [en cours d’exécution des exemples de hello](#running) procédure toorun cet exemple sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9bec7-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="9bec7-143"><a name="pigpython"></a>UDF Pig</span><span class="sxs-lookup"><span data-stu-id="9bec7-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="9bec7-144">Un script Python peut être utilisé comme une fonction utilisateur Pig via hello `GENERATE` instruction.</span><span class="sxs-lookup"><span data-stu-id="9bec7-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="9bec7-145">Vous pouvez exécuter le script hello utilisant Jython ou C Python.</span><span class="sxs-lookup"><span data-stu-id="9bec7-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="9bec7-146">Jython s’exécute sur hello JVM et en mode natif peut être appelée à partir de Pig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="9bec7-147">C Python étant un processus externe, données hello Pig sur hello JVM est envoyée script toohello en cours d’exécution dans un processus de Python.</span><span class="sxs-lookup"><span data-stu-id="9bec7-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="9bec7-148">sortie de Hello Hello script Python est envoyée dans Pig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="9bec7-149">interpréteur Python sous toospecify hello, utilisez `register` lors du référencement du script de Python hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="9bec7-150">Hello exemples suivants auprès des scripts Pig comme `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="9bec7-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="9bec7-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="9bec7-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="9bec7-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="9bec7-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bec7-153">Lorsque vous utilisez Jython, hello chemin d’accès toohello pig_jython fichier peut être un chemin d’accès local ou un WASB : / / chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="9bec7-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="9bec7-154">Toutefois, lorsque vous utilisez Python de C, vous devez référencer un fichier sur le système de fichiers local hello du nœud hello que vous utilisez la tâche de Pig toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="9bec7-155">Une fois après l’inscription, hello Pig Latin pour cet exemple hello même pour les deux :</span><span class="sxs-lookup"><span data-stu-id="9bec7-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="9bec7-156">Cet exemple effectue ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9bec7-156">Here's what this example does:</span></span>

1. <span data-ttu-id="9bec7-157">Hello première ligne charge le fichier de données hello exemple `sample.log` dans `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="9bec7-158">Elle définit également chaque enregistrement sous la forme d’un tableau de caractères `chararray`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="9bec7-159">ligne suivante de Hello exclut toutes les valeurs null, le stockage des résultats hello d’opération hello dans `LOG`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="9bec7-160">Ensuite, il effectue une itération sur les enregistrements de hello dans `LOG` et utilise `GENERATE` tooinvoke hello `create_structure` méthode contenu dans le script de Python/Jython hello chargée sous la forme `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="9bec7-161">`LINE`est toopass utilisé fonction toohello enregistrement en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="9bec7-162">Enfin, les sorties de hello sont tooSTDOUT enregistrée représente à l’aide de hello `DUMP` commande.</span><span class="sxs-lookup"><span data-stu-id="9bec7-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="9bec7-163">Cette commande affiche les résultats de hello lorsque hello opération sera terminée.</span><span class="sxs-lookup"><span data-stu-id="9bec7-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="9bec7-164">Créer le fichier de pigudf.py hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="9bec7-165">Sur votre environnement de développement, créez un fichier texte nommé `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="9bec7-166">Utilisez hello après le code en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="9bec7-166">Use hello following code as hello contents of hello file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="9bec7-167">Dans l’exemple de Pig Latin hello, nous avons défini hello `LINE` entrée comme un chararray, car il n’existe aucun schéma cohérent pour l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="9bec7-168">Hello script Python transforme les données de hello dans un schéma cohérent pour la sortie.</span><span class="sxs-lookup"><span data-stu-id="9bec7-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="9bec7-169">Hello `@outputSchema` instruction définit le format hello de données hello tooPig retournée.</span><span class="sxs-lookup"><span data-stu-id="9bec7-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="9bec7-170">Dans le cas présent, il s'agit d'un **data bag**, qui est un type de données Pig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="9bec7-171">conteneur de Hello contient hello suivant des champs, qui sont tous des chararray (chaînes) :</span><span class="sxs-lookup"><span data-stu-id="9bec7-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="9bec7-172">date - hello date hello entrée du journal a été créée</span><span class="sxs-lookup"><span data-stu-id="9bec7-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="9bec7-173">heure - hello entrée de journal hello a été créée.</span><span class="sxs-lookup"><span data-stu-id="9bec7-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="9bec7-174">nom de classe - entrée hello hello du nom de classe a été créé pour</span><span class="sxs-lookup"><span data-stu-id="9bec7-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="9bec7-175">niveau - niveau de journal hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-175">level - hello log level</span></span>
   * <span data-ttu-id="9bec7-176">entrée de journal détaillées pour hello détail :</span><span class="sxs-lookup"><span data-stu-id="9bec7-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="9bec7-177">Ensuite, hello `def create_structure(input)` définit fonction hello Pig passe à des éléments de ligne.</span><span class="sxs-lookup"><span data-stu-id="9bec7-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="9bec7-178">Hello d’exemple de données, `sample.log`, principalement est conforme toohello date, heure, classname, niveau et nous souhaitons tooreturn de schéma décrit en détail.</span><span class="sxs-lookup"><span data-stu-id="9bec7-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="9bec7-179">Toutefois, il contient quelques lignes qui commencent par `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="9bec7-180">Ces lignes doivent être schéma de hello toomatch modifié.</span><span class="sxs-lookup"><span data-stu-id="9bec7-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="9bec7-181">Hello `if` instruction vérifie les, puis massages hello hello toomove de données d’entrée `*java.lang.Exception*` fin toohello de chaîne, hello données en ligne avec notre schéma de sortie attendue de remise.</span><span class="sxs-lookup"><span data-stu-id="9bec7-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="9bec7-182">Ensuite, hello `split` commande est utilisée toosplit hello données hello première quatre espaces.</span><span class="sxs-lookup"><span data-stu-id="9bec7-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="9bec7-183">sortie de Hello est attribué dans `date`, `time`, `classname`, `level`, et `detail`.</span><span class="sxs-lookup"><span data-stu-id="9bec7-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="9bec7-184">Enfin, les valeurs hello sont retournés tooPig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="9bec7-185">Lorsque les données de salutation sont retournées tooPig, il a un schéma cohérent tel que défini dans hello `@outputSchema` instruction.</span><span class="sxs-lookup"><span data-stu-id="9bec7-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="9bec7-186"><a name="running"></a>Télécharger et exécuter les exemples hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bec7-187">Hello **SSH** étapes fonctionnent uniquement avec un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="9bec7-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9bec7-188">Hello **PowerShell** étapes fonctionnent avec cluster Linux ou le HDInsight de basés sur Windows, mais nécessitent un client Windows.</span><span class="sxs-lookup"><span data-stu-id="9bec7-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="9bec7-189">SSH</span><span class="sxs-lookup"><span data-stu-id="9bec7-189">SSH</span></span>

<span data-ttu-id="9bec7-190">Pour plus d’informations sur l’utilisation de SSH, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9bec7-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="9bec7-191">Utilisez `scp` le cluster HDInsight tooyour toocopy hello fichiers.</span><span class="sxs-lookup"><span data-stu-id="9bec7-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="9bec7-192">Par exemple, hello commande copies hello cluster tooa de fichiers nommé suivante **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="9bec7-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="9bec7-193">Utiliser SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="9bec7-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="9bec7-194">À partir de la session SSH hello, ajoutez hello python fichiers téléchargés précédemment stockage WASB toohello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="9bec7-195">Après avoir téléchargé les fichiers hello, utilisez hello étapes suivantes toorun hello Hive et les travaux Pig.</span><span class="sxs-lookup"><span data-stu-id="9bec7-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="9bec7-196">Utilisez hello Hive une UDF</span><span class="sxs-lookup"><span data-stu-id="9bec7-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="9bec7-197">Hello d’utilisation `hive` toostart hello ruche interface de commande.</span><span class="sxs-lookup"><span data-stu-id="9bec7-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="9bec7-198">Vous devez voir un `hive>` demander une fois que l’interpréteur de commandes hello a chargé.</span><span class="sxs-lookup"><span data-stu-id="9bec7-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="9bec7-199">Entrez hello suivant la requête à hello `hive>` invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="9bec7-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="9bec7-200">Après avoir entré la dernière ligne de hello, hello doit démarrer.</span><span class="sxs-lookup"><span data-stu-id="9bec7-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="9bec7-201">Une fois que hello est terminée, elle retourne toohello similaire de sortie l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9bec7-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="9bec7-202">Utilisez hello Pig UDF</span><span class="sxs-lookup"><span data-stu-id="9bec7-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="9bec7-203">Hello d’utilisation `pig` toostart hello interface de commande.</span><span class="sxs-lookup"><span data-stu-id="9bec7-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="9bec7-204">Vous voyez un `grunt>` demander une fois que l’interpréteur de commandes hello a chargé.</span><span class="sxs-lookup"><span data-stu-id="9bec7-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="9bec7-205">Entrez hello suivant les instructions à hello `grunt>` invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="9bec7-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="9bec7-206">Après avoir entré hello ligne suivante, hello doit démarrer.</span><span class="sxs-lookup"><span data-stu-id="9bec7-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="9bec7-207">Une fois hello est terminée, elle retourne toohello similaire de sortie données suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bec7-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="9bec7-208">Utilisez `quit` tooexit hello shell de Grunt et utilisez hello tooedit hello pigudf.py le fichier sur le système de fichiers local hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9bec7-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="9bec7-209">Une fois dans l’éditeur de hello, supprimez les commentaires hello ligne suivante en supprimant hello `#` caractère de début hello de ligne de hello :</span><span class="sxs-lookup"><span data-stu-id="9bec7-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="9bec7-210">Une fois hello a été modifié, utiliser l’éditeur de hello tooexit Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="9bec7-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="9bec7-211">Sélectionnez Y, puis modifiez toosave hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="9bec7-212">Hello d’utilisation `pig` réexécutez la commande shell de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="9bec7-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="9bec7-213">Une fois que vous vous trouvez dans hello `grunt>` invite, utilisez hello toorun hello Python script à l’aide hello C Python interpréteur suivant.</span><span class="sxs-lookup"><span data-stu-id="9bec7-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="9bec7-214">Une fois cette tâche est terminée, vous devez voir hello même sortie que lorsque vous avez déjà exécuté script hello à l’aide de Jython.</span><span class="sxs-lookup"><span data-stu-id="9bec7-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="9bec7-215">PowerShell : Télécharger les fichiers de hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="9bec7-216">Vous pouvez utiliser PowerShell tooupload hello fichiers toohello HDInsight du serveur.</span><span class="sxs-lookup"><span data-stu-id="9bec7-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="9bec7-217">Utilisez hello script tooupload hello Python fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="9bec7-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9bec7-218">étapes de Hello dans cette section utilisent Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bec7-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="9bec7-219">Pour plus d’informations sur l’utilisation d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9bec7-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> <span data-ttu-id="9bec7-220">Hello de modification `C:\path\to` toohello chemin d’accès toohello fichiers sur votre environnement de développement de valeur.</span><span class="sxs-lookup"><span data-stu-id="9bec7-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="9bec7-221">Ce script récupère les informations de votre cluster HDInsight, puis extrait le compte de hello et une clé de compte de stockage par défaut hello et téléchargements hello racine toohello des fichiers du conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="9bec7-222">Pour plus d’informations sur le téléchargement de fichiers, consultez hello [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md) document.</span><span class="sxs-lookup"><span data-stu-id="9bec7-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="9bec7-223">PowerShell : Utilisez hello Hive une UDF</span><span class="sxs-lookup"><span data-stu-id="9bec7-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="9bec7-224">PowerShell peut également être utilisé tooremotely exécuter des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="9bec7-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="9bec7-225">Hello utilisation suivant toorun de script PowerShell une requête Hive qui utilise **hiveudf.py** script :</span><span class="sxs-lookup"><span data-stu-id="9bec7-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bec7-226">Avant d’exécuter, script de hello vous invite à hello HTTPs/Admin les informations de compte pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9bec7-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="9bec7-227">Hello sortie pour hello **Hive** travail doit apparaître comme toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9bec7-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="9bec7-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="9bec7-228">Pig (Jython)</span></span>

<span data-ttu-id="9bec7-229">PowerShell peut également être utilisé toorun Pig Latin travaux.</span><span class="sxs-lookup"><span data-stu-id="9bec7-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="9bec7-230">toorun un travail Pig Latin qui utilise hello **pigudf.py** script, utilisez hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="9bec7-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="9bec7-231">Lors de l’envoi d’un travail à l’aide de PowerShell à distance, il n’est pas possible de toouse C Python comme interpréteur de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="9bec7-232">Hello sortie pour hello **Pig** travail doit apparaître similaire toohello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bec7-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="9bec7-233"><a name="troubleshooting"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9bec7-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="9bec7-234">Erreurs lors de l'exécution des travaux</span><span class="sxs-lookup"><span data-stu-id="9bec7-234">Errors when running jobs</span></span>

<span data-ttu-id="9bec7-235">Lorsque vous exécutez la tâche hive de hello, vous pouvez rencontrer un toohello similaire erreur suit texte :</span><span class="sxs-lookup"><span data-stu-id="9bec7-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="9bec7-236">Ce problème peut être dû à des fins de ligne hello dans le fichier de Python hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="9bec7-237">De nombreux éditeurs de Windows par défaut toousing CRLF comme fin de ligne hello, mais les applications Linux attendent généralement LF.</span><span class="sxs-lookup"><span data-stu-id="9bec7-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="9bec7-238">Vous pouvez utiliser hello PowerShell instructions tooremove hello CR caractères qui suivent avant de le télécharger hello fichier tooHDInsight :</span><span class="sxs-lookup"><span data-stu-id="9bec7-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="9bec7-239">Scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bec7-239">PowerShell scripts</span></span>

<span data-ttu-id="9bec7-240">À la fois de l’exemple hello scripts PowerShell utilisé les exemples de hello toorun contient une ligne de commentaire qui affiche la sortie d’erreur pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="9bec7-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="9bec7-241">Si vous ne voyez pas de sortie hello attendu pour le travail de hello, supprimez les commentaires suivants de hello ligne et de voir si des informations d’erreur hello indiquent un problème.</span><span class="sxs-lookup"><span data-stu-id="9bec7-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="9bec7-242">informations sur l’erreur (STDERR) Hello et résultat hello du travail de hello (STDOUT) sont également enregistrés tooyour HDInsight stockage.</span><span class="sxs-lookup"><span data-stu-id="9bec7-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="9bec7-243">Pour ce travail...</span><span class="sxs-lookup"><span data-stu-id="9bec7-243">For this job...</span></span> | <span data-ttu-id="9bec7-244">Examinez ces fichiers dans le conteneur d’objets blob hello</span><span class="sxs-lookup"><span data-stu-id="9bec7-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="9bec7-245">Hive</span><span class="sxs-lookup"><span data-stu-id="9bec7-245">Hive</span></span> |<span data-ttu-id="9bec7-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="9bec7-246">/HivePython/stderr</span></span><p><span data-ttu-id="9bec7-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="9bec7-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="9bec7-248">Pig</span><span class="sxs-lookup"><span data-stu-id="9bec7-248">Pig</span></span> |<span data-ttu-id="9bec7-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="9bec7-249">/PigPython/stderr</span></span><p><span data-ttu-id="9bec7-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="9bec7-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="9bec7-251"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9bec7-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="9bec7-252">Si vous avez besoin des modules Python tooload qui ne sont pas fournis par défaut, consultez [comment toodeploy un tooAzure module HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bec7-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="9bec7-253">Pour les autres façons toouse Pig, Hive et toolearn sur l’utilisation de MapReduce, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="9bec7-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="9bec7-254">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bec7-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9bec7-255">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bec7-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9bec7-256">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="9bec7-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
