---
title: "Exécuter des tâches Apache Sqoop avec Azure HDInsight (Hadoop) | Microsoft Docs"
description: "Découvrez comment utiliser Azure PowerShell à partir d'un poste de travail pour exécuter des commandes Sqoop import et export entre un cluster HDInsight et une base de données SQL Azure."
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
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="cd051-103">Utilisation de Sqoop avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd051-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="cd051-104">Découvrez comment utiliser Sqoop dans HDInsight pour effectuer des opérations d’importation et d’exportation entre un cluster HDInsight et la base de données SQL Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd051-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="cd051-105">Bien que Hadoop soit préférable pour traiter des données non structurées et semi-structurées, telles que des journaux et des fichiers, il peut être également nécessaire de traiter les données structurées stockées dans des bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="cd051-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="cd051-106">[Sqoop][sqoop-user-guide-1.4.4] est un outil conçu pour transférer des données entre les clusters Hadoop et les bases de données relationnelles.</span><span class="sxs-lookup"><span data-stu-id="cd051-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="cd051-107">Vous pouvez l’utiliser pour importer des données depuis un système de gestion de base de données relationnelle (SGBDR) tel que SQL Server, MySQL ou Oracle dans un système de fichiers distribués Hadoop (HDFS), transformer des données dans Hadoop avec MapReduce ou Hive et exporter à nouveau les données dans un SGBDR.</span><span class="sxs-lookup"><span data-stu-id="cd051-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="cd051-108">Dans ce didacticiel, vous allez utiliser une base de données SQL Server comme base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="cd051-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="cd051-109">Pour obtenir la liste des versions Sqoop prises en charge par les clusters HDInsight, consultez la rubrique [Quels sont les composants et versions Hadoop disponibles avec HDInsight ?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="cd051-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="cd051-110">Présentation du scénario</span><span class="sxs-lookup"><span data-stu-id="cd051-110">Understand the scenario</span></span>

<span data-ttu-id="cd051-111">Le cluster HDInsight inclut des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="cd051-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="cd051-112">Vous utilisez les deux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cd051-112">You use the following two samples:</span></span>

* <span data-ttu-id="cd051-113">Un fichier journal log4j situé sous */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="cd051-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="cd051-114">Ce fichier inclut les journaux suivants :</span><span class="sxs-lookup"><span data-stu-id="cd051-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="cd051-115">Une table Hive appelée *hivesampletable*, qui référence le fichier de données situé sous */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="cd051-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="cd051-116">Cette table contient des données relatives aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="cd051-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="cd051-117">Champ</span><span class="sxs-lookup"><span data-stu-id="cd051-117">Field</span></span> | <span data-ttu-id="cd051-118">Type de données</span><span class="sxs-lookup"><span data-stu-id="cd051-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="cd051-119">clientid</span><span class="sxs-lookup"><span data-stu-id="cd051-119">clientid</span></span> |<span data-ttu-id="cd051-120">string</span><span class="sxs-lookup"><span data-stu-id="cd051-120">string</span></span> |
  | <span data-ttu-id="cd051-121">querytime</span><span class="sxs-lookup"><span data-stu-id="cd051-121">querytime</span></span> |<span data-ttu-id="cd051-122">string</span><span class="sxs-lookup"><span data-stu-id="cd051-122">string</span></span> |
  | <span data-ttu-id="cd051-123">market</span><span class="sxs-lookup"><span data-stu-id="cd051-123">market</span></span> |<span data-ttu-id="cd051-124">string</span><span class="sxs-lookup"><span data-stu-id="cd051-124">string</span></span> |
  | <span data-ttu-id="cd051-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="cd051-125">deviceplatform</span></span> |<span data-ttu-id="cd051-126">string</span><span class="sxs-lookup"><span data-stu-id="cd051-126">string</span></span> |
  | <span data-ttu-id="cd051-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="cd051-127">devicemake</span></span> |<span data-ttu-id="cd051-128">string</span><span class="sxs-lookup"><span data-stu-id="cd051-128">string</span></span> |
  | <span data-ttu-id="cd051-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="cd051-129">devicemodel</span></span> |<span data-ttu-id="cd051-130">string</span><span class="sxs-lookup"><span data-stu-id="cd051-130">string</span></span> |
  | <span data-ttu-id="cd051-131">state</span><span class="sxs-lookup"><span data-stu-id="cd051-131">state</span></span> |<span data-ttu-id="cd051-132">string</span><span class="sxs-lookup"><span data-stu-id="cd051-132">string</span></span> |
  | <span data-ttu-id="cd051-133">country</span><span class="sxs-lookup"><span data-stu-id="cd051-133">country</span></span> |<span data-ttu-id="cd051-134">string</span><span class="sxs-lookup"><span data-stu-id="cd051-134">string</span></span> |
  | <span data-ttu-id="cd051-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="cd051-135">querydwelltime</span></span> |<span data-ttu-id="cd051-136">double</span><span class="sxs-lookup"><span data-stu-id="cd051-136">double</span></span> |
  | <span data-ttu-id="cd051-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="cd051-137">sessionid</span></span> |<span data-ttu-id="cd051-138">bigint</span><span class="sxs-lookup"><span data-stu-id="cd051-138">bigint</span></span> |
  | <span data-ttu-id="cd051-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="cd051-139">sessionpagevieworder</span></span> |<span data-ttu-id="cd051-140">bigint</span><span class="sxs-lookup"><span data-stu-id="cd051-140">bigint</span></span> |

<span data-ttu-id="cd051-141">Vous commencez par exporter *sample.log* et *hivesampletable* vers la base de données SQL Azure ou vers SQL Server, puis vous importez à nouveau la table contenant les données de l’appareil mobile dans HDInsight en utilisant la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="cd051-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="cd051-142">Création du cluster et de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="cd051-142">Create cluster and SQL database</span></span>
<span data-ttu-id="cd051-143">Cette section vous montre comment créer un cluster, une base de données SQL Database et les schémas de base de données SQL pour exécuter le didacticiel à l’aide du portail Azure et d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd051-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="cd051-144">Ce modèle se trouve dans les [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="cd051-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="cd051-145">Le modèle Resource Manager appelle un package bacpac pour déployer les schémas de table vers la base de données SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cd051-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="cd051-146">Le package bacpac est disponible dans un conteneur d’objets blob public : https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="cd051-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="cd051-147">Si vous souhaitez utiliser un conteneur privé pour stocker les fichiers bacpac, appliquez les valeurs suivantes au modèle :</span><span class="sxs-lookup"><span data-stu-id="cd051-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="cd051-148">Si vous préférez utiliser Azure PowerShell pour créer le cluster et la base de données SQL Database, consultez l’[Annexe A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="cd051-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="cd051-149">Cliquez sur l’image suivante pour ouvrir un modèle Resource Manager dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="cd051-150">Entrez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd051-150">Enter the following properties:</span></span>

    - <span data-ttu-id="cd051-151">**Abonnement** : indiquez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="cd051-152">**Groupe de ressources** : créez un groupe de ressources Azure ou sélectionnez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="cd051-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="cd051-153">Un groupe de ressources est destiné à la gestion.</span><span class="sxs-lookup"><span data-stu-id="cd051-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="cd051-154">C’est un conteneur d’objets.</span><span class="sxs-lookup"><span data-stu-id="cd051-154">It is a container for objects.</span></span>
    - <span data-ttu-id="cd051-155">**Emplacement** : sélectionnez une région.</span><span class="sxs-lookup"><span data-stu-id="cd051-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="cd051-156">**Nom de cluster** : saisissez le nom du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cd051-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="cd051-157">**Nom d’utilisateur et mot de passe de cluster**: le nom de connexion par défaut est admin.</span><span class="sxs-lookup"><span data-stu-id="cd051-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="cd051-158">**Nom d’utilisateur et mot de passe SSH**.</span><span class="sxs-lookup"><span data-stu-id="cd051-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="cd051-159">**Nom et mot de passe de connexion au serveur de base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="cd051-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="cd051-160">**_artifacts Location** (Emplacement _artifacts) : utilisez la valeur par défaut, sauf si vous souhaitez utiliser votre propre fichier backpac à un emplacement différent.</span><span class="sxs-lookup"><span data-stu-id="cd051-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="cd051-161">**_artifacts Location Sas Token** (Jeton SAP d’emplacement _artifacts) : laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="cd051-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="cd051-162">**Bacpac File Name** (Nom du fichier bacpac) : utilisez la valeur par défaut, sauf si vous souhaitez utiliser votre propre fichier backpac.</span><span class="sxs-lookup"><span data-stu-id="cd051-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="cd051-163">Les valeurs suivantes sont codées en dur dans la section des variables :</span><span class="sxs-lookup"><span data-stu-id="cd051-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="cd051-164">Nom du compte de stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="cd051-164">Default storage account name</span></span> | <span data-ttu-id="cd051-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="cd051-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="cd051-166">Nom du serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-166">Azure SQL database server name</span></span> |<span data-ttu-id="cd051-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="cd051-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="cd051-168">Nom de la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cd051-168">Azure SQL database name</span></span> |<span data-ttu-id="cd051-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="cd051-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="cd051-170">Veuillez noter ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd051-170">Please write down these values.</span></span>  <span data-ttu-id="cd051-171">Vous en aurez besoin plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cd051-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="cd051-172">3.Cliquez sur **OK** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="cd051-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="cd051-173">4.Dans le panneau **Déploiement personnalisé**, cliquez sur la zone de liste déroulante **Groupe de ressources**, puis cliquez sur **Nouveau** pour créer un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cd051-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="cd051-174">Le groupe de ressources est un conteneur qui regroupe le cluster, le compte de stockage dépendant et une autre ressource liée.</span><span class="sxs-lookup"><span data-stu-id="cd051-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="cd051-175">5.Cliquez sur **Conditions juridiques**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cd051-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="cd051-176">6.Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cd051-176">6.Click **Create**.</span></span> <span data-ttu-id="cd051-177">Une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cd051-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="cd051-178">La création du cluster et de la base de données SQL prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="cd051-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="cd051-179">Si vous choisissez d’utiliser une base de données SQL Azure ou Microsoft SQL Server existante</span><span class="sxs-lookup"><span data-stu-id="cd051-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="cd051-180">**Base de données SQL Azure**: vous devez configurer une règle de pare-feu pour le serveur de base de données SQL Azure afin d’autoriser l'accès depuis votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="cd051-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="cd051-181">Pour des instructions sur la création d’une base de données SQL Azure et la configuration d’un pare-feu, consultez la rubrique [Prise en main de la base de données SQL Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="cd051-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="cd051-182">Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels qu’Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="cd051-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="cd051-183">Si ce paramètre de pare-feu est désactivé, vous devez l’activer depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="cd051-184">Pour obtenir des instructions sur la création d’une base de données SQL Azure et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d’une base de données SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="cd051-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="cd051-185">**SQL Server**: si votre cluster HDInsight se trouve sur le même réseau virtuel que SQL Server dans Azure, vous pouvez utiliser les étapes décrites dans cet article pour importer et exporter des données vers une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd051-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cd051-186">HDInsight prend en charge uniquement les réseaux virtuels basés sur l'emplacement et ne fonctionne pas pour le moment avec des réseaux virtuels basés sur des groupes d'affinités.</span><span class="sxs-lookup"><span data-stu-id="cd051-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="cd051-187">Pour créer et configurer un réseau virtuel, consultez [Créer un réseau virtuel au moyen du portail Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="cd051-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="cd051-188">Lorsque vous utilisez SQL Server dans votre centre de données, vous devez configurer le réseau virtuel comme étant *de site à site* ou *de point à site*.</span><span class="sxs-lookup"><span data-stu-id="cd051-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="cd051-189">Pour les réseaux virtuels de **point à site**, SQL Server doit exécuter l’application de configuration du client VPN, qui est disponible depuis le **tableau de bord** de la configuration de votre réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="cd051-190">Lorsque vous utilisez SQL Server sur une machine virtuelle Azure, toute configuration du réseau virtuel peut être utilisée si la machine virtuelle qui héberge SQL Server est membre du même réseau virtuel que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd051-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="cd051-191">Pour créer un cluster HDInsight sur un réseau virtuel, consultez la rubrique [Création de clusters Hadoop dans HDInsight à l’aide d’options personnalisées](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="cd051-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cd051-192">SQL Server doit également autoriser l'authentification.</span><span class="sxs-lookup"><span data-stu-id="cd051-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="cd051-193">Vous devez utiliser une connexion SQL Server pour compléter les étapes décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cd051-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="cd051-194">Exécuter des tâches Sqoop</span><span class="sxs-lookup"><span data-stu-id="cd051-194">Run Sqoop jobs</span></span>
<span data-ttu-id="cd051-195">HDInsight peut exécuter des tâches Sqoop à l’aide de différentes méthodes.</span><span class="sxs-lookup"><span data-stu-id="cd051-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="cd051-196">Utilisez le tableau suivant pour découvrir la méthode qui vous convient, puis cliquez sur le lien pour obtenir une présentation détaillée.</span><span class="sxs-lookup"><span data-stu-id="cd051-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="cd051-197">**Utilisez-le** si vous souhaitez...</span><span class="sxs-lookup"><span data-stu-id="cd051-197">**Use this** if you want...</span></span> | <span data-ttu-id="cd051-198">... un interpréteur de commandes **interactif**</span><span class="sxs-lookup"><span data-stu-id="cd051-198">...an **interactive** shell</span></span> | <span data-ttu-id="cd051-199">... un traitement par **lots**</span><span class="sxs-lookup"><span data-stu-id="cd051-199">...**batch** processing</span></span> | <span data-ttu-id="cd051-200">...avec ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="cd051-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="cd051-201">...depuis ce **système d’exploitation cluster**</span><span class="sxs-lookup"><span data-stu-id="cd051-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="cd051-202">SSH</span><span class="sxs-lookup"><span data-stu-id="cd051-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="cd051-203">✔</span><span class="sxs-lookup"><span data-stu-id="cd051-203">✔</span></span> |<span data-ttu-id="cd051-204">✔</span><span class="sxs-lookup"><span data-stu-id="cd051-204">✔</span></span> |<span data-ttu-id="cd051-205">Linux</span><span class="sxs-lookup"><span data-stu-id="cd051-205">Linux</span></span> |<span data-ttu-id="cd051-206">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="cd051-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="cd051-207">Kit de développement logiciel (SDK) .NET pour Hadoop</span><span class="sxs-lookup"><span data-stu-id="cd051-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="cd051-208">✔</span><span class="sxs-lookup"><span data-stu-id="cd051-208">✔</span></span> |<span data-ttu-id="cd051-209">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="cd051-209">Linux or Windows</span></span> |<span data-ttu-id="cd051-210">Windows (pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="cd051-210">Windows (for now)</span></span> |
| [<span data-ttu-id="cd051-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd051-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="cd051-212">✔</span><span class="sxs-lookup"><span data-stu-id="cd051-212">✔</span></span> |<span data-ttu-id="cd051-213">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="cd051-213">Linux or Windows</span></span> |<span data-ttu-id="cd051-214">Windows</span><span class="sxs-lookup"><span data-stu-id="cd051-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="cd051-215">Limitations</span><span class="sxs-lookup"><span data-stu-id="cd051-215">Limitations</span></span>
* <span data-ttu-id="cd051-216">Exportation en bloc : avec HDInsight sous Linux, le connecteur Sqoop utilisé pour exporter des données vers Microsoft SQL Server ou la base de données SQL Azure ne prend pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="cd051-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="cd051-217">Traitement par lots : avec HDInsight sous Linux, lorsque vous utilisez le commutateur `-batch` pour effectuer des insertions, Sqoop effectue plusieurs insertions plutôt qu’un traitement par lots des opérations d’insertion.</span><span class="sxs-lookup"><span data-stu-id="cd051-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd051-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd051-218">Next steps</span></span>
<span data-ttu-id="cd051-219">Vous maîtrisez à présent l'utilisation de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="cd051-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="cd051-220">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd051-220">To learn more, see:</span></span>

* [<span data-ttu-id="cd051-221">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd051-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cd051-222">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd051-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="cd051-223">[Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie] : utilisez l’action Sqoop dans un workflow Oozie.</span><span class="sxs-lookup"><span data-stu-id="cd051-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="cd051-224">[Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-data] : utilisez Hive pour analyser des données sur les retards de vol, puis utilisez Sqoop pour exporter ces données vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="cd051-225">[Chargement de données vers HDInsight][hdinsight-upload-data] : découvrez d’autres méthodes pour charger des données vers HDInsight ou Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="cd051-226">Annexe A - Exemple PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd051-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="cd051-227">L’exemple PowerShell effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd051-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="cd051-228">Connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-228">Connect to Azure.</span></span>
2. <span data-ttu-id="cd051-229">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-229">Create an Azure resource group.</span></span> <span data-ttu-id="cd051-230">Pour en savoir plus, voir [Utilisation d’Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="cd051-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="cd051-231">Création d’un serveur Base de données SQL Azure, d’une base de données SQL Azure et de deux tables.</span><span class="sxs-lookup"><span data-stu-id="cd051-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="cd051-232">Si vous utilisez SQL Server à la place, utilisez les instructions suivantes pour créer les tables :</span><span class="sxs-lookup"><span data-stu-id="cd051-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
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
   
    <span data-ttu-id="cd051-233">Le moyen le plus simple d’examiner la base de données et les tables consiste à utiliser Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd051-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="cd051-234">Le serveur de base de données et la base de données peuvent être examinés à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="cd051-235">Créez un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd051-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="cd051-236">Pour examiner le cluster, vous pouvez utiliser le portail Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd051-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="cd051-237">Prétraitez le fichier de données source.</span><span class="sxs-lookup"><span data-stu-id="cd051-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="cd051-238">Ce tutoriel explique comment exporter un fichier journal log4j (fichier délimité) et une table Hive vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="cd051-239">Le fichier délimité s’appelle */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="cd051-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="cd051-240">Vous trouverez plus haut dans ce didacticiel quelques exemples de journaux log4j.</span><span class="sxs-lookup"><span data-stu-id="cd051-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="cd051-241">Certaines lignes du fichier journal sont vides et d'autres ressemblent à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="cd051-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="cd051-242">Cela convient pour d'autres exemples qui utilisent ces données, mais nous devons supprimer ces exceptions pour pouvoir importer le fichier dans la base de données SQL Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd051-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="cd051-243">Notez que la présence de lignes vides ou contenant moins d'éléments que de champs définis dans la table de la base de données SQL Azure entraîne l'échec de la commande Sqoop export.</span><span class="sxs-lookup"><span data-stu-id="cd051-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="cd051-244">La table log4jlogs contient 7 champs de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="cd051-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="cd051-245">Cette procédure crée un fichier sur le cluster : tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="cd051-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="cd051-246">Pour examiner le fichier de données modifiées, vous pouvez utiliser le portail Azure, un outil d’exploration Azure Storage, ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd051-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="cd051-247">Le didacticiel [Prise en main de HDInsight][hdinsight-get-started] inclut un exemple de code présentant l’utilisation d’Azure PowerShell pour télécharger un fichier et afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="cd051-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="cd051-248">Exportez un fichier de données vers la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="cd051-249">Le fichier source est tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="cd051-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="cd051-250">La table vers laquelle les données sont exportées est nommée log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="cd051-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cd051-251">En dehors des informations de la chaîne de connexion, les étapes décrites dans cette section doivent fonctionner pour une base de données SQL Azure ou pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd051-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="cd051-252">Elles ont été testées avec la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="cd051-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="cd051-253">**Configuration de point à site du réseau virtuel Azure**: un réseau virtuel connectant le cluster HDInsight à un serveur SQL Server dans un centre de données privé.</span><span class="sxs-lookup"><span data-stu-id="cd051-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="cd051-254">Pour plus d'informations, consultez la page [Configuration d'un réseau privé virtuel (VPN) de point à site dans le portail de gestion](../vpn-gateway/vpn-gateway-point-to-site-create.md) .</span><span class="sxs-lookup"><span data-stu-id="cd051-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="cd051-255">**Azure HDInsight 3.1**: pour plus d’informations sur la création d’un cluster sur un réseau virtuel, consultez la rubrique [Création de clusters Hadoop dans HDInsight à l’aide d’options personnalisées](hdinsight-hadoop-provision-linux-clusters.md) .</span><span class="sxs-lookup"><span data-stu-id="cd051-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="cd051-256">**SQL Server 2014**: configuré de manière à autoriser l'authentification et à exécuter le package de configuration du client VPN pour établir une connexion sécurisée au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cd051-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="cd051-257">Exportez une table Hive vers la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd051-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="cd051-258">Importez la table mobiledata dans le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd051-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="cd051-259">Pour examiner le fichier de données modifiées, vous pouvez utiliser le portail Azure, un outil d’exploration Azure Storage, ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd051-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="cd051-260">Le didacticiel [Prise en main de HDInsight][hdinsight-get-started] inclut un exemple de code présentant l’utilisation d’Azure PowerShell pour télécharger un fichier et afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="cd051-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="cd051-261">Exemple PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd051-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
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
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
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

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

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
