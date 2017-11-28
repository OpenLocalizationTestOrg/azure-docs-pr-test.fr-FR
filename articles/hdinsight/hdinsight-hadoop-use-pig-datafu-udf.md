---
title: aaaUse DataFu avec Pig dans HDInsight - Azure | Documents Microsoft
description: "DataFu est une collection de bibliothèques à utiliser avec Hadoop. Découvrez comment vous pouvez utiliser DataFu avec Pig sur votre cluster HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a><span data-ttu-id="b75b2-104">Utilisation de DataFu avec Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="b75b2-104">Use DataFu with pig on HDInsight</span></span>

<span data-ttu-id="b75b2-105">Découvrez comment toouse DataFu avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b75b2-105">Learn how toouse DataFu with HDInsight.</span></span> <span data-ttu-id="b75b2-106">DataFu est un ensemble de bibliothèques Open Source à utiliser avec Pig sur Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b75b2-106">DataFu is a collection of Open Source libraries for use with Pig on Hadoop.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b75b2-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b75b2-107">Prerequisites</span></span>

* <span data-ttu-id="b75b2-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b75b2-108">An Azure subscription.</span></span>

* <span data-ttu-id="b75b2-109">Un cluster Azure HDInsight (Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="b75b2-109">An Azure HDInsight cluster (Linux or Windows based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b75b2-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="b75b2-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b75b2-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b75b2-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b75b2-112">Des connaissances élémentaire de [l'utilisation de Pig dans HDInsight](hdinsight-use-pig.md)</span><span class="sxs-lookup"><span data-stu-id="b75b2-112">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span></span>

## <a name="install-datafu-on-linux-based-hdinsight"></a><span data-ttu-id="b75b2-113">Installation de DataFu dans HDInsight basé sur Linux</span><span class="sxs-lookup"><span data-stu-id="b75b2-113">Install DataFu on Linux-based HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b75b2-114">DataFu est installé sur les clusters basés sur Linux 3.3 et versions ultérieures, ainsi que sur les clusters Windows.</span><span class="sxs-lookup"><span data-stu-id="b75b2-114">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span></span> <span data-ttu-id="b75b2-115">Il n’est pas installé sur les clusters Linux avant la version 3.3.</span><span class="sxs-lookup"><span data-stu-id="b75b2-115">It is not installed on Linux-based clusters earlier than 3.3.</span></span>
>
> <span data-ttu-id="b75b2-116">Si vous utilisez un cluster basé sur Windows ou un cluster basé sur une version Linux ultérieure à la version 3.3, ignorez cette section.</span><span class="sxs-lookup"><span data-stu-id="b75b2-116">If you are using a Windows-based cluster, or a Linux-based cluster higher than version 3.3, skip this section.</span></span>

<span data-ttu-id="b75b2-117">DataFu peut être téléchargé et installé à partir du référentiel de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="b75b2-117">DataFu can be downloaded and installed from hello Maven repository.</span></span> <span data-ttu-id="b75b2-118">Utilisez hello suivant le cluster HDInsight tooyour étapes tooadd DataFu :</span><span class="sxs-lookup"><span data-stu-id="b75b2-118">Use hello following steps tooadd DataFu tooyour HDInsight cluster:</span></span>

1. <span data-ttu-id="b75b2-119">Connecter le cluster HDInsight de basés sur Linux de tooyour à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="b75b2-119">Connect tooyour Linux-based HDInsight cluster using SSH.</span></span> <span data-ttu-id="b75b2-120">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b75b2-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b75b2-121">Utilisez hello commande toodownload hello DataFu jar le fichier suivant à l’aide d’utilitaire wget hello ou copier- coller hello lien dans le téléchargement de hello toobegin navigateur.</span><span class="sxs-lookup"><span data-stu-id="b75b2-121">Use hello following command toodownload hello DataFu jar file using hello wget utility, or copy and paste hello link into your browser toobegin hello download.</span></span>

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. <span data-ttu-id="b75b2-122">Ensuite, téléchargez un stockage hello fichiers toodefault pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b75b2-122">Next, upload hello file toodefault storage for your HDInsight cluster.</span></span> <span data-ttu-id="b75b2-123">Placer les fichiers de hello par défaut stockage rend disponible tooall nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b75b2-123">Placing hello file in default storage makes it available tooall nodes in hello cluster.</span></span>

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > <span data-ttu-id="b75b2-124">commande précédente Hello stocke jar hello dans `/example/jars` , car ce répertoire existe déjà sur le stockage de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b75b2-124">hello previous command stores hello jar in `/example/jars` since this directory already exists on hello cluster storage.</span></span> <span data-ttu-id="b75b2-125">Vous pouvez utiliser n'importe quel emplacement dans le stockage en cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b75b2-125">You can use any location you wish on HDInsight cluster storage.</span></span>

## <a name="use-datafu-with-pig"></a><span data-ttu-id="b75b2-126">Utilisation de DataFu avec Pig</span><span class="sxs-lookup"><span data-stu-id="b75b2-126">Use DataFu With Pig</span></span>

<span data-ttu-id="b75b2-127">étapes de Hello dans cette section supposent que vous êtes familiarisé avec l’utilisation de Pig dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b75b2-127">hello steps in this section assume that you are familiar with using Pig on HDInsight.</span></span> <span data-ttu-id="b75b2-128">Pour plus d'informations sur l'utilisation de Pig avec HDInsight, consultez la rubrique [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="b75b2-128">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b75b2-129">Si vous avez installé manuellement à l’aide des étapes de hello dans la section précédente de hello de DataFu, vous devez l’enregistrer avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="b75b2-129">If you manually installed DataFu using hello steps in hello previous section, you must register it before using it.</span></span>
>
> * <span data-ttu-id="b75b2-130">Si votre cluster utilise le stockage Azure, utilisez un chemin d’accès `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="b75b2-130">If your cluster uses Azure Storage, use a `wasb://` path.</span></span> <span data-ttu-id="b75b2-131">Par exemple, `register wasb:///example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="b75b2-131">For example, `register wasb:///example/jars/datafu-1.2.0.jar`.</span></span>
>
> * <span data-ttu-id="b75b2-132">Si votre cluster utilise Azure Data Lake Store, utilisez un chemin d’accès `adl://`.</span><span class="sxs-lookup"><span data-stu-id="b75b2-132">If your cluster uses Azure Data Lake Store, use an `adl://` path.</span></span> <span data-ttu-id="b75b2-133">Par exemple, `register adl://home/example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="b75b2-133">For example, `register adl://home/example/jars/datafu-1.2.0.jar`.</span></span>

<span data-ttu-id="b75b2-134">Vous définissez souvent un alias pour les fonctions DataFu.</span><span class="sxs-lookup"><span data-stu-id="b75b2-134">You often define an alias for DataFu functions.</span></span> <span data-ttu-id="b75b2-135">Hello exemple suivant définit un alias de `SHA`:</span><span class="sxs-lookup"><span data-stu-id="b75b2-135">hello following example defines an alias of `SHA`:</span></span>

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

<span data-ttu-id="b75b2-136">Vous pouvez ensuite utiliser cet alias dans un toogenerate de script Pig Latin un hachage pour les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="b75b2-136">You can then use this alias in a Pig Latin script toogenerate a hash for hello input data.</span></span> <span data-ttu-id="b75b2-137">Par exemple, hello de code suivant remplace emplacement hello dans les données d’entrée hello avec une valeur de hachage :</span><span class="sxs-lookup"><span data-stu-id="b75b2-137">For example, hello following code replaces hello location in hello input data with a hash value:</span></span>

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

<span data-ttu-id="b75b2-138">Il génère hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="b75b2-138">It generates hello following output:</span></span>

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a><span data-ttu-id="b75b2-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b75b2-139">Next steps</span></span>

<span data-ttu-id="b75b2-140">Pour plus d’informations sur les DataFu ou Pig, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="b75b2-140">For more information on DataFu or Pig, see hello following documents:</span></span>

* <span data-ttu-id="b75b2-141">[Guide Apache DataFu Pig](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span><span class="sxs-lookup"><span data-stu-id="b75b2-141">[Apache DataFu Pig Guide](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span></span>
* [<span data-ttu-id="b75b2-142">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="b75b2-142">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
