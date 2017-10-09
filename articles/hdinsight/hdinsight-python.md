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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Utiliser des fonctions définies par l’utilisateur (UDF) Python avec Hive et Pig dans HDInsight

Découvrez comment toouse Python défini par l’utilisateur (UDF) de fonctions avec Apache Hive et Pig dans Hadoop sur Azure HDInsight.

## <a name="python"></a>Python sur HDInsight

Python 2.7 est installé par défaut sur HDInsight 3.0 et versions ultérieures. Apache Hive peut être utilisé avec cette version de Python pour traiter les flux de données. Le traitement des flux de données utilise les données de toopass STDOUT et STDIN entre Hive et hello UDF.

HDInsight inclut également Jython, une implémentation de Python écrite en Java. Jython s’exécute directement sur la Machine virtuelle Java de hello et n’utilise pas de diffusion en continu. Jython est recommandé de hello interpréteur Python lors de l’utilisation de Python avec Pig.

> [!WARNING]
> étapes Hello dans ce document apporter hello suivant hypothèses : 
>
> * Vous créez des scripts Python hello sur votre environnement de développement local.
> * Vous téléchargez hello tooHDInsight de scripts à l’aide soit hello `scp` commande d’une session d’interpréteur de commandes locale ou d’hello fourni de script PowerShell.
>
> Si vous souhaitez toouse hello [Azure Cloud Shell (interpréteur de commandes)](https://docs.microsoft.com/azure/cloud-shell/overview) aperçu toowork avec HDInsight, vous devez :
>
> * Créer des scripts à l’intérieur d’environnement du shell hello cloud hello.
> * Utilisez `scp` fichiers hello tooupload hello cloud tooHDInsight d’interpréteur de commandes.
> * Utilisez `ssh` hello cloud shell tooconnect tooHDInsight des exemples d’exécution hello.

## <a name="hivepython"></a>UDF Hive

Python peut être utilisé comme un fichier UDF à partir de la ruche via hello HiveQL `TRANSFORM` instruction. Par exemple, hello suivant HiveQL appelle hello `hiveudf.py` fichier stocké dans le compte de stockage Azure hello par défaut pour le cluster de hello.

**HDInsight Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Sur les clusters HDInsight de basés sur Windows, hello `USING` clause doit spécifier hello chemin d’accès complet toopython.exe.

Cet exemple effectue ce qui suit :

1. Hello `add file` instruction au début de hello du fichier de hello ajoute hello `hiveudf.py` fichier toohello distributed cache, afin qu’il soit accessible par tous les nœuds de cluster de hello.
2. Hello `SELECT TRANSFORM ... USING` instruction sélectionne des données à partir de hello `hivesampletable`. Il passe également hello clientid, devicemake et devicemodel valeurs toohello `hiveudf.py` script.
3. Hello `AS` clause décrit les champs hello retournés à partir de `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Créer le fichier de hiveudf.py hello


Sur votre environnement de développement, créez un fichier texte nommé `hiveudf.py`. Utilisez hello après le code en tant que contenu hello du fichier de hello :

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

Ce script effectue hello suivant des actions :

1. Une ligne de données de STDIN est lue.
2. Hello caractère de saut de ligne de fin est supprimé à l’aide de `string.strip(line, "\n ")`.
3. Lorsque vous effectuez le traitement de flux, une seule ligne contient toutes les valeurs de hello avec un caractère de tabulation entre chaque valeur. Par conséquent, `string.split(line, "\t")` peut être hello toosplit utilisé entrée à chaque onglet, en retournant uniquement les champs hello.
4. Lorsque le traitement est terminé, la sortie hello doit être écrite tooSTDOUT comme une ligne unique, avec un onglet entre chaque champ. Par exemple, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Hello `while` boucle se répète jusqu'à ce que non `line` est en lecture.

sortie du script Hello est une concaténation des valeurs d’entrée de hello pour `devicemake` et `devicemodel`, et un hachage de hello la valeur concaténée.

Consultez [en cours d’exécution des exemples de hello](#running) procédure toorun cet exemple sur votre cluster HDInsight.

## <a name="pigpython"></a>UDF Pig

Un script Python peut être utilisé comme une fonction utilisateur Pig via hello `GENERATE` instruction. Vous pouvez exécuter le script hello utilisant Jython ou C Python.

* Jython s’exécute sur hello JVM et en mode natif peut être appelée à partir de Pig.
* C Python étant un processus externe, données hello Pig sur hello JVM est envoyée script toohello en cours d’exécution dans un processus de Python. sortie de Hello Hello script Python est envoyée dans Pig.

interpréteur Python sous toospecify hello, utilisez `register` lors du référencement du script de Python hello. Hello exemples suivants auprès des scripts Pig comme `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Lorsque vous utilisez Jython, hello chemin d’accès toohello pig_jython fichier peut être un chemin d’accès local ou un WASB : / / chemin d’accès. Toutefois, lorsque vous utilisez Python de C, vous devez référencer un fichier sur le système de fichiers local hello du nœud hello que vous utilisez la tâche de Pig toosubmit hello.

Une fois après l’inscription, hello Pig Latin pour cet exemple hello même pour les deux :

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Cet exemple effectue ce qui suit :

1. Hello première ligne charge le fichier de données hello exemple `sample.log` dans `LOGS`. Elle définit également chaque enregistrement sous la forme d’un tableau de caractères `chararray`.
2. ligne suivante de Hello exclut toutes les valeurs null, le stockage des résultats hello d’opération hello dans `LOG`.
3. Ensuite, il effectue une itération sur les enregistrements de hello dans `LOG` et utilise `GENERATE` tooinvoke hello `create_structure` méthode contenu dans le script de Python/Jython hello chargée sous la forme `myfuncs`. `LINE`est toopass utilisé fonction toohello enregistrement en cours de hello.
4. Enfin, les sorties de hello sont tooSTDOUT enregistrée représente à l’aide de hello `DUMP` commande. Cette commande affiche les résultats de hello lorsque hello opération sera terminée.

### <a name="create-hello-pigudfpy-file"></a>Créer le fichier de pigudf.py hello

Sur votre environnement de développement, créez un fichier texte nommé `pigudf.py`. Utilisez hello après le code en tant que contenu hello du fichier de hello :

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

Dans l’exemple de Pig Latin hello, nous avons défini hello `LINE` entrée comme un chararray, car il n’existe aucun schéma cohérent pour l’entrée de hello. Hello script Python transforme les données de hello dans un schéma cohérent pour la sortie.

1. Hello `@outputSchema` instruction définit le format hello de données hello tooPig retournée. Dans le cas présent, il s'agit d'un **data bag**, qui est un type de données Pig. conteneur de Hello contient hello suivant des champs, qui sont tous des chararray (chaînes) :

   * date - hello date hello entrée du journal a été créée
   * heure - hello entrée de journal hello a été créée.
   * nom de classe - entrée hello hello du nom de classe a été créé pour
   * niveau - niveau de journal hello
   * entrée de journal détaillées pour hello détail :

2. Ensuite, hello `def create_structure(input)` définit fonction hello Pig passe à des éléments de ligne.

3. Hello d’exemple de données, `sample.log`, principalement est conforme toohello date, heure, classname, niveau et nous souhaitons tooreturn de schéma décrit en détail. Toutefois, il contient quelques lignes qui commencent par `*java.lang.Exception*`. Ces lignes doivent être schéma de hello toomatch modifié. Hello `if` instruction vérifie les, puis massages hello hello toomove de données d’entrée `*java.lang.Exception*` fin toohello de chaîne, hello données en ligne avec notre schéma de sortie attendue de remise.

4. Ensuite, hello `split` commande est utilisée toosplit hello données hello première quatre espaces. sortie de Hello est attribué dans `date`, `time`, `classname`, `level`, et `detail`.

5. Enfin, les valeurs hello sont retournés tooPig.

Lorsque les données de salutation sont retournées tooPig, il a un schéma cohérent tel que défini dans hello `@outputSchema` instruction.

## <a name="running"></a>Télécharger et exécuter les exemples hello

> [!IMPORTANT]
> Hello **SSH** étapes fonctionnent uniquement avec un cluster HDInsight de basés sur Linux. Hello **PowerShell** étapes fonctionnent avec cluster Linux ou le HDInsight de basés sur Windows, mais nécessitent un client Windows.

### <a name="ssh"></a>SSH

Pour plus d’informations sur l’utilisation de SSH, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Utilisez `scp` le cluster HDInsight tooyour toocopy hello fichiers. Par exemple, hello commande copies hello cluster tooa de fichiers nommé suivante **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Utiliser SSH tooconnect toohello cluster.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. À partir de la session SSH hello, ajoutez hello python fichiers téléchargés précédemment stockage WASB toohello pour le cluster de hello.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Après avoir téléchargé les fichiers hello, utilisez hello étapes suivantes toorun hello Hive et les travaux Pig.

#### <a name="use-hello-hive-udf"></a>Utilisez hello Hive une UDF

1. Hello d’utilisation `hive` toostart hello ruche interface de commande. Vous devez voir un `hive>` demander une fois que l’interpréteur de commandes hello a chargé.

2. Entrez hello suivant la requête à hello `hive>` invite de commandes :

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Après avoir entré la dernière ligne de hello, hello doit démarrer. Une fois que hello est terminée, elle retourne toohello similaire de sortie l’exemple suivant :

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Utilisez hello Pig UDF

1. Hello d’utilisation `pig` toostart hello interface de commande. Vous voyez un `grunt>` demander une fois que l’interpréteur de commandes hello a chargé.

2. Entrez hello suivant les instructions à hello `grunt>` invite de commandes :

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Après avoir entré hello ligne suivante, hello doit démarrer. Une fois hello est terminée, elle retourne toohello similaire de sortie données suivantes :

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Utilisez `quit` tooexit hello shell de Grunt et utilisez hello tooedit hello pigudf.py le fichier sur le système de fichiers local hello suivant :

    ```bash
    nano pigudf.py
    ```

5. Une fois dans l’éditeur de hello, supprimez les commentaires hello ligne suivante en supprimant hello `#` caractère de début hello de ligne de hello :

    ```bash
    #from pig_util import outputSchema
    ```

    Une fois hello a été modifié, utiliser l’éditeur de hello tooexit Ctrl + X. Sélectionnez Y, puis modifiez toosave hello.

6. Hello d’utilisation `pig` réexécutez la commande shell de hello toostart. Une fois que vous vous trouvez dans hello `grunt>` invite, utilisez hello toorun hello Python script à l’aide hello C Python interpréteur suivant.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Une fois cette tâche est terminée, vous devez voir hello même sortie que lorsque vous avez déjà exécuté script hello à l’aide de Jython.

### <a name="powershell-upload-hello-files"></a>PowerShell : Télécharger les fichiers de hello

Vous pouvez utiliser PowerShell tooupload hello fichiers toohello HDInsight du serveur. Utilisez hello script tooupload hello Python fichiers suivants :

> [!IMPORTANT] 
> étapes de Hello dans cette section utilisent Azure PowerShell. Pour plus d’informations sur l’utilisation d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

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
> Hello de modification `C:\path\to` toohello chemin d’accès toohello fichiers sur votre environnement de développement de valeur.

Ce script récupère les informations de votre cluster HDInsight, puis extrait le compte de hello et une clé de compte de stockage par défaut hello et téléchargements hello racine toohello des fichiers du conteneur de hello.

> [!NOTE]
> Pour plus d’informations sur le téléchargement de fichiers, consultez hello [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md) document.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell : Utilisez hello Hive une UDF

PowerShell peut également être utilisé tooremotely exécuter des requêtes Hive. Hello utilisation suivant toorun de script PowerShell une requête Hive qui utilise **hiveudf.py** script :

> [!IMPORTANT]
> Avant d’exécuter, script de hello vous invite à hello HTTPs/Admin les informations de compte pour votre cluster HDInsight.

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

Hello sortie pour hello **Hive** travail doit apparaître comme toohello l’exemple suivant :

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell peut également être utilisé toorun Pig Latin travaux. toorun un travail Pig Latin qui utilise hello **pigudf.py** script, utilisez hello PowerShell script suivant :

> [!NOTE]
> Lors de l’envoi d’un travail à l’aide de PowerShell à distance, il n’est pas possible de toouse C Python comme interpréteur de hello.

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

Hello sortie pour hello **Pig** travail doit apparaître similaire toohello données suivantes :

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="errors-when-running-jobs"></a>Erreurs lors de l'exécution des travaux

Lorsque vous exécutez la tâche hive de hello, vous pouvez rencontrer un toohello similaire erreur suit texte :

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Ce problème peut être dû à des fins de ligne hello dans le fichier de Python hello. De nombreux éditeurs de Windows par défaut toousing CRLF comme fin de ligne hello, mais les applications Linux attendent généralement LF.

Vous pouvez utiliser hello PowerShell instructions tooremove hello CR caractères qui suivent avant de le télécharger hello fichier tooHDInsight :

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Scripts PowerShell

À la fois de l’exemple hello scripts PowerShell utilisé les exemples de hello toorun contient une ligne de commentaire qui affiche la sortie d’erreur pour le travail de hello. Si vous ne voyez pas de sortie hello attendu pour le travail de hello, supprimez les commentaires suivants de hello ligne et de voir si des informations d’erreur hello indiquent un problème.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

informations sur l’erreur (STDERR) Hello et résultat hello du travail de hello (STDOUT) sont également enregistrés tooyour HDInsight stockage.

| Pour ce travail... | Examinez ces fichiers dans le conteneur d’objets blob hello |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>Étapes suivantes

Si vous avez besoin des modules Python tooload qui ne sont pas fournis par défaut, consultez [comment toodeploy un tooAzure module HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Pour les autres façons toouse Pig, Hive et toolearn sur l’utilisation de MapReduce, consultez hello suivant des documents :

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)
