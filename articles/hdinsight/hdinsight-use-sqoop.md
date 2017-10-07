---
title: aaaRun Apache Sqoop travaux Azure hdinsight (Hadoop) | Documents Microsoft
description: "Découvrez comment toouse Azure PowerShell à partir d’une station de travail de toorun Sqoop importer et exporter entre un cluster Hadoop et une base de données SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="0f39f-103">Utilisation de Sqoop avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f39f-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="0f39f-104">Découvrez comment toouse Sqoop dans HDInsight tooimport et d’exportation entre le cluster HDInsight et de la base de données SQL Azure ou base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f39f-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="0f39f-105">Bien que Hadoop est un choix naturel pour le traitement des données non structurées et semi-structurées, telles que les journaux et les fichiers, il peut également être un besoin de données tooprocess structurées stockées dans les bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="0f39f-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="0f39f-106">[Sqoop] [ sqoop-user-guide-1.4.4] est un outil conçu de tootransfer des données entre les clusters Hadoop et des bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="0f39f-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="0f39f-107">Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR) telles que SQL Server, MySQL ou Oracle dans le système de fichiers DFS Hadoop hello (HDFS), transformer des données dans Hadoop MapReduce ou ruche hello et puis exporter les données hello dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="0f39f-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="0f39f-108">Dans ce didacticiel, vous allez utiliser une base de données SQL Server comme base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="0f39f-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="0f39f-109">Pour les versions de Sqoop sont pris en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight ?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="0f39f-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="0f39f-110">Comprendre le scénario de hello</span><span class="sxs-lookup"><span data-stu-id="0f39f-110">Understand hello scenario</span></span>

<span data-ttu-id="0f39f-111">Le cluster HDInsight inclut des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="0f39f-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="0f39f-112">Vous utilisez hello suivant deux exemples :</span><span class="sxs-lookup"><span data-stu-id="0f39f-112">You use hello following two samples:</span></span>

* <span data-ttu-id="0f39f-113">Un fichier journal log4j situé sous */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="0f39f-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="0f39f-114">Hello suivant les journaux est extraits à partir du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="0f39f-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="0f39f-115">Une table Hive nommée *hivesampletable*, lequel références hello le fichier de données situé à */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="0f39f-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="0f39f-116">table de Hello contient des données de l’appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="0f39f-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="0f39f-117">Champ</span><span class="sxs-lookup"><span data-stu-id="0f39f-117">Field</span></span> | <span data-ttu-id="0f39f-118">Type de données</span><span class="sxs-lookup"><span data-stu-id="0f39f-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="0f39f-119">clientid</span><span class="sxs-lookup"><span data-stu-id="0f39f-119">clientid</span></span> |<span data-ttu-id="0f39f-120">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-120">string</span></span> |
  | <span data-ttu-id="0f39f-121">querytime</span><span class="sxs-lookup"><span data-stu-id="0f39f-121">querytime</span></span> |<span data-ttu-id="0f39f-122">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-122">string</span></span> |
  | <span data-ttu-id="0f39f-123">market</span><span class="sxs-lookup"><span data-stu-id="0f39f-123">market</span></span> |<span data-ttu-id="0f39f-124">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-124">string</span></span> |
  | <span data-ttu-id="0f39f-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="0f39f-125">deviceplatform</span></span> |<span data-ttu-id="0f39f-126">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-126">string</span></span> |
  | <span data-ttu-id="0f39f-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="0f39f-127">devicemake</span></span> |<span data-ttu-id="0f39f-128">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-128">string</span></span> |
  | <span data-ttu-id="0f39f-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="0f39f-129">devicemodel</span></span> |<span data-ttu-id="0f39f-130">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-130">string</span></span> |
  | <span data-ttu-id="0f39f-131">state</span><span class="sxs-lookup"><span data-stu-id="0f39f-131">state</span></span> |<span data-ttu-id="0f39f-132">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-132">string</span></span> |
  | <span data-ttu-id="0f39f-133">country</span><span class="sxs-lookup"><span data-stu-id="0f39f-133">country</span></span> |<span data-ttu-id="0f39f-134">string</span><span class="sxs-lookup"><span data-stu-id="0f39f-134">string</span></span> |
  | <span data-ttu-id="0f39f-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="0f39f-135">querydwelltime</span></span> |<span data-ttu-id="0f39f-136">double</span><span class="sxs-lookup"><span data-stu-id="0f39f-136">double</span></span> |
  | <span data-ttu-id="0f39f-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="0f39f-137">sessionid</span></span> |<span data-ttu-id="0f39f-138">bigint</span><span class="sxs-lookup"><span data-stu-id="0f39f-138">bigint</span></span> |
  | <span data-ttu-id="0f39f-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="0f39f-139">sessionpagevieworder</span></span> |<span data-ttu-id="0f39f-140">bigint</span><span class="sxs-lookup"><span data-stu-id="0f39f-140">bigint</span></span> |

<span data-ttu-id="0f39f-141">Tout d’abord, vous exportez *exemple.log* et *hivesampletable* base de données SQL Azure toohello ou tooSQL Server puis table hello d’importation qui contient les données des appareils mobiles hello sauvegarder tooHDInsight à l’aide de hello chemin d’accès suivant :</span><span class="sxs-lookup"><span data-stu-id="0f39f-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="0f39f-142">Création du cluster et de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="0f39f-142">Create cluster and SQL database</span></span>
<span data-ttu-id="0f39f-143">Cette section vous montre comment toocreate un cluster, une base de données SQL et schémas de base de données SQL hello pour en cours d’exécution hello didacticiel à l’aide de hello portail Azure et un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0f39f-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="0f39f-144">modèle de Hello peut se trouver dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0f39f-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="0f39f-145">modèle de gestionnaire de ressources Hello appelle un bacpac package toodeploy hello table schémas tooSQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="0f39f-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="0f39f-146">package bacpac de Hello se trouve dans un conteneur d’objet blob public, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="0f39f-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="0f39f-147">Si vous voulez toouse un conteneur privé pour les fichiers bacpac hello, utilisez hello valeurs dans le modèle de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f39f-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="0f39f-148">Si vous préférez le cluster de hello toocreate toouse Azure PowerShell et hello de base de données SQL, consultez [annexe A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="0f39f-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="0f39f-149">Cliquez sur hello suivant image tooopen un modèle de gestionnaire de ressources Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="0f39f-150">Entrez hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f39f-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="0f39f-151">**Abonnement** : indiquez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="0f39f-152">**Groupe de ressources** : créez un groupe de ressources Azure ou sélectionnez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="0f39f-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="0f39f-153">Un groupe de ressources est destiné à la gestion.</span><span class="sxs-lookup"><span data-stu-id="0f39f-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="0f39f-154">C’est un conteneur d’objets.</span><span class="sxs-lookup"><span data-stu-id="0f39f-154">It is a container for objects.</span></span>
    - <span data-ttu-id="0f39f-155">**Emplacement** : sélectionnez une région.</span><span class="sxs-lookup"><span data-stu-id="0f39f-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="0f39f-156">**ClusterName**: entrez un nom pour le cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="0f39f-157">**Nom de connexion et mot de passe de cluster**: nom de connexion hello par défaut est Admin.</span><span class="sxs-lookup"><span data-stu-id="0f39f-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="0f39f-158">**Nom d’utilisateur et mot de passe SSH**.</span><span class="sxs-lookup"><span data-stu-id="0f39f-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="0f39f-159">**Nom et mot de passe de connexion au serveur de base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="0f39f-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="0f39f-160">**_artifacts emplacement**: utiliser la valeur par défaut de hello sauf si vous souhaitez toouse votre propre fichier à DOS dans un emplacement différent.</span><span class="sxs-lookup"><span data-stu-id="0f39f-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="0f39f-161">**_artifacts Location Sas Token** (Jeton SAP d’emplacement _artifacts) : laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="0f39f-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="0f39f-162">**Nom du fichier Bacpac**: utiliser la valeur par défaut de hello sauf si vous souhaitez toouse votre propre fichier à DOS.</span><span class="sxs-lookup"><span data-stu-id="0f39f-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="0f39f-163">Hello valeurs suivantes est codés en dur dans la section des variables hello :</span><span class="sxs-lookup"><span data-stu-id="0f39f-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="0f39f-164">Nom du compte de stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="0f39f-164">Default storage account name</span></span> | <span data-ttu-id="0f39f-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="0f39f-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="0f39f-166">Nom du serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-166">Azure SQL database server name</span></span> |<span data-ttu-id="0f39f-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="0f39f-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="0f39f-168">Nom de la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0f39f-168">Azure SQL database name</span></span> |<span data-ttu-id="0f39f-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="0f39f-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="0f39f-170">Veuillez noter ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0f39f-170">Please write down these values.</span></span>  <span data-ttu-id="0f39f-171">Vous avez besoin plus tard dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="0f39f-172">3. Cliquez sur **OK** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="0f39f-173">4. à partir de hello **les déploiement personnalisé** panneau, cliquez sur **groupe de ressources** déroulante zone, puis cliquez sur **nouveau** toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f39f-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="0f39f-174">groupe de ressources Hello est un conteneur qui regroupe le cluster de hello, compte de stockage dépendant de hello et autres ressources liées.</span><span class="sxs-lookup"><span data-stu-id="0f39f-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="0f39f-175">5.Cliquez sur **Conditions juridiques**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0f39f-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="0f39f-176">6.Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0f39f-176">6.Click **Create**.</span></span> <span data-ttu-id="0f39f-177">Une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0f39f-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="0f39f-178">Cela prend environ le cluster de hello toocreate environ 20 minutes et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0f39f-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="0f39f-179">Si vous choisissez la base de données SQL Azure toouse ou Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f39f-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="0f39f-180">**Base de données SQL Azure**: vous devez configurer une règle de pare-feu pour hello accès au tooallow du serveur de base de données SQL Azure à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="0f39f-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="0f39f-181">Pour obtenir des instructions sur la création d’une base de données SQL Azure et de configuration du pare-feu de hello, consultez [prise en main de la base de données SQL Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="0f39f-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="0f39f-182">Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels qu’Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="0f39f-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="0f39f-183">Si ce paramètre de pare-feu est désactivé, vous devez tooenable à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="0f39f-184">Pour obtenir des instructions sur la création d’une base de données SQL Azure et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d’une base de données SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="0f39f-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="0f39f-185">**SQL Server**: Si votre cluster HDInsight se trouve sur hello même réseau virtuel dans Azure en tant que SQL Server, vous pouvez utiliser les étapes de hello dans cet article tooimport et exportation de données tooa de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f39f-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0f39f-186">HDInsight prend en charge uniquement les réseaux virtuels basés sur l'emplacement et ne fonctionne pas pour le moment avec des réseaux virtuels basés sur des groupes d'affinités.</span><span class="sxs-lookup"><span data-stu-id="0f39f-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="0f39f-187">toocreate et configurer un réseau virtuel, consultez [créer un réseau virtuel à l’aide de hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="0f39f-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="0f39f-188">Lorsque vous utilisez SQL Server dans votre centre de données, vous devez configurer le réseau virtuel hello *site-à-site* ou *point-to-site*.</span><span class="sxs-lookup"><span data-stu-id="0f39f-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="0f39f-189">Pour **point-to-site** des réseaux virtuels, SQL Server doivent exécuter hello VPN client application de configuration, qui est disponible à partir de hello **tableau de bord** de votre configuration de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="0f39f-190">Lorsque vous utilisez SQL Server sur une machine virtuelle Azure, toute configuration de réseau virtuel peut être utilisée si la machine virtuelle de hello hébergeant SQL Server est un membre de hello même réseau virtuel que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f39f-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="0f39f-191">toocreate un cluster HDInsight sur un réseau virtuel, consultez [Hadoop de créer des clusters dans HDInsight à l’aide des options personnalisées](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="0f39f-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0f39f-192">SQL Server doit également autoriser l'authentification.</span><span class="sxs-lookup"><span data-stu-id="0f39f-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="0f39f-193">Vous devez utiliser un serveur SQL Server hello toocomplete de connexion les étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="0f39f-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="0f39f-194">Exécuter des tâches Sqoop</span><span class="sxs-lookup"><span data-stu-id="0f39f-194">Run Sqoop jobs</span></span>
<span data-ttu-id="0f39f-195">HDInsight peut exécuter des tâches Sqoop à l’aide de différentes méthodes.</span><span class="sxs-lookup"><span data-stu-id="0f39f-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="0f39f-196">Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="0f39f-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="0f39f-197">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="0f39f-197">**Use this** if you want...</span></span> | <span data-ttu-id="0f39f-198">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="0f39f-198">...an **interactive** shell</span></span> | <span data-ttu-id="0f39f-199">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="0f39f-199">...**batch** processing</span></span> | <span data-ttu-id="0f39f-200">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="0f39f-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="0f39f-201">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="0f39f-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="0f39f-202">SSH</span><span class="sxs-lookup"><span data-stu-id="0f39f-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="0f39f-203">✔</span><span class="sxs-lookup"><span data-stu-id="0f39f-203">✔</span></span> |<span data-ttu-id="0f39f-204">✔</span><span class="sxs-lookup"><span data-stu-id="0f39f-204">✔</span></span> |<span data-ttu-id="0f39f-205">Linux</span><span class="sxs-lookup"><span data-stu-id="0f39f-205">Linux</span></span> |<span data-ttu-id="0f39f-206">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="0f39f-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="0f39f-207">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="0f39f-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="0f39f-208">✔</span><span class="sxs-lookup"><span data-stu-id="0f39f-208">✔</span></span> |<span data-ttu-id="0f39f-209">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="0f39f-209">Linux or Windows</span></span> |<span data-ttu-id="0f39f-210">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="0f39f-210">Windows (for now)</span></span> |
| [<span data-ttu-id="0f39f-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f39f-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="0f39f-212">✔</span><span class="sxs-lookup"><span data-stu-id="0f39f-212">✔</span></span> |<span data-ttu-id="0f39f-213">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="0f39f-213">Linux or Windows</span></span> |<span data-ttu-id="0f39f-214">Windows</span><span class="sxs-lookup"><span data-stu-id="0f39f-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="0f39f-215">Limites</span><span class="sxs-lookup"><span data-stu-id="0f39f-215">Limitations</span></span>
* <span data-ttu-id="0f39f-216">L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f39f-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="0f39f-217">Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f39f-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f39f-218">Next steps</span></span>
<span data-ttu-id="0f39f-219">Maintenant que vous avez appris comment toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="0f39f-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="0f39f-220">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="0f39f-220">toolearn more, see:</span></span>

* [<span data-ttu-id="0f39f-221">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f39f-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0f39f-222">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f39f-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="0f39f-223">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie] : utilisez l’action Sqoop dans un workflow Oozie.</span><span class="sxs-lookup"><span data-stu-id="0f39f-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="0f39f-224">[Analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-data]: utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="0f39f-225">[Télécharger des données tooHDInsight][hdinsight-upload-data]: trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="0f39f-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="0f39f-226">Annexe A - Exemple PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f39f-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="0f39f-227">exemple de PowerShell Hello exécute hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f39f-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="0f39f-228">Se connecter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="0f39f-229">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-229">Create an Azure resource group.</span></span> <span data-ttu-id="0f39f-230">Pour en savoir plus, voir [Utilisation d’Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0f39f-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="0f39f-231">Création d’un serveur Base de données SQL Azure, d’une base de données SQL Azure et de deux tables.</span><span class="sxs-lookup"><span data-stu-id="0f39f-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="0f39f-232">Si vous utilisez SQL Server au lieu de cela, utilisez hello instructions toocreate hello tables suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f39f-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="0f39f-233">tables et la base de données de hello plus simple façon tooexamine hello est toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f39f-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="0f39f-234">serveur de base de données Hello et la base de données hello peuvent être examinées à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f39f-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="0f39f-235">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f39f-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="0f39f-236">cluster de hello tooexamine, vous pouvez utiliser hello portail Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f39f-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="0f39f-237">Prétraiter le fichier de données source hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="0f39f-238">Dans ce didacticiel, vous exportez un fichier de journal log4j (un fichier délimité) et une base de données SQL Azure de tooan table Hive.</span><span class="sxs-lookup"><span data-stu-id="0f39f-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="0f39f-239">Hello fichier délimité est appelé */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="0f39f-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="0f39f-240">Plus haut dans le didacticiel de hello, vous avez vu quelques exemples des journaux de log4j.</span><span class="sxs-lookup"><span data-stu-id="0f39f-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="0f39f-241">Dans le fichier journal de hello, il existe des lignes vides et certains toothese similaires de lignes :</span><span class="sxs-lookup"><span data-stu-id="0f39f-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="0f39f-242">Cela convient pour obtenir des exemples qui utilisent ces données, mais nous devons supprimer ces exceptions avant de pouvoir importer dans la base de données SQL Azure hello ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f39f-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="0f39f-243">Exportation de Sqoop échoue s’il existe une chaîne vide ou une ligne comportant moins les éléments que nombre hello des champs définis dans la table de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="0f39f-244">table de log4jlogs Hello comporte des champs de type chaîne 7.</span><span class="sxs-lookup"><span data-stu-id="0f39f-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="0f39f-245">Cette procédure crée un nouveau fichier sur le cluster de hello : tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="0f39f-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="0f39f-246">fichier de données modifiées tooexamine hello, vous pouvez utiliser hello portail Azure, un outil Explorateur de stockage Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f39f-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="0f39f-247">[Prise en main HDInsight] [ hdinsight-get-started] possède un code d’exemple pour l’utilisation d’Azure PowerShell toodownload un fichier et afficher le contenu du fichier hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="0f39f-248">Exporter une base de données SQL Azure de données fichier toohello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="0f39f-249">fichier de source de Hello est tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="0f39f-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="0f39f-250">table Hello où les données de salutation sont exporté toois appelé log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="0f39f-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0f39f-251">Autres que les informations de chaîne de connexion, les étapes hello dans cette section doivent fonctionner pour une base de données SQL Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f39f-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="0f39f-252">Ces étapes ont été testés à l’aide de hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="0f39f-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="0f39f-253">**Configuration de point-to-site de réseau virtuel Azure**: un réseau virtuel connecté hello HDInsight cluster tooa SQL Server dans un centre de données privé.</span><span class="sxs-lookup"><span data-stu-id="0f39f-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="0f39f-254">Consultez [configurer un VPN de Point-to-Site dans le portail de gestion de hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0f39f-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="0f39f-255">**Azure HDInsight 3.1**: pour plus d’informations sur la création d’un cluster sur un réseau virtuel, consultez la rubrique [Création de clusters Hadoop dans HDInsight à l’aide d’options personnalisées](hdinsight-hadoop-provision-linux-clusters.md) .</span><span class="sxs-lookup"><span data-stu-id="0f39f-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="0f39f-256">**SQL Server 2014**: configurés de manière sécurisée l’authentification tooallow et en cours d’exécution hello VPN client configuration package tooconnect toohello des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="0f39f-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="0f39f-257">Exporter une base de données SQL Azure de toohello table Hive.</span><span class="sxs-lookup"><span data-stu-id="0f39f-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="0f39f-258">Importez le cluster HDInsight toohello hello mobiledata table.</span><span class="sxs-lookup"><span data-stu-id="0f39f-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="0f39f-259">fichier de données modifiées tooexamine hello, vous pouvez utiliser hello portail Azure, un outil Explorateur de stockage Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f39f-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="0f39f-260">[Prise en main HDInsight] [ hdinsight-get-started] possède un code d’exemple sur l’utilisation d’Azure PowerShell toodownload un fichier et afficher le contenu du fichier hello.</span><span class="sxs-lookup"><span data-stu-id="0f39f-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="0f39f-261">Hello, exemple PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f39f-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
