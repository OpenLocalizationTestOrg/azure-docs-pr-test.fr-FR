---
title: Utiliser Apache Storm avec Power BI - Azure HDInsight | Documents Microsoft
description: "Créez un rapport Power BI en utilisant les données d’une topologie C# s’exécutant sur un cluster Apache Storm dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="c96ef-103">Utilisation de Power BI pour visualiser les données d'une topologie Apache Storm</span><span class="sxs-lookup"><span data-stu-id="c96ef-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="c96ef-104">Power BI vous permet d’afficher visuellement des données sous forme de rapports.</span><span class="sxs-lookup"><span data-stu-id="c96ef-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="c96ef-105">Ce document fournit un exemple d’utilisation d’Apache Storm sur HDInsight pour générer des données pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="c96ef-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="c96ef-106">Les étapes décrites dans ce document reposent sur un environnement de développement Windows avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c96ef-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="c96ef-107">Le projet compilé peut être soumis à un cluster HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="c96ef-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c96ef-108">Seuls les clusters basés sur Linux créés après le 28/10/2016 prennent en charge les topologies SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c96ef-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="c96ef-109">Pour utiliser une topologie C# avec un cluster basé sur Linux, mettez à jour le package NuGet Microsoft.SCP.Net.SDK utilisé par votre projet vers la version 0.10.0.6 ou une version supérieure.</span><span class="sxs-lookup"><span data-stu-id="c96ef-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="c96ef-110">La version du package doit également correspondre à la version principale de Storm installée sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="c96ef-111">Par exemple, Storm sur les versions 3.3 et 3.4 de HDInsight utilise Storm 0.10.x, tandis que HDInsight 3.5 utilise Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="c96ef-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="c96ef-112">Les topologies C# sur les clusters basés sur Linux doivent utiliser .NET 4.5, et utiliser Mono pour s’exécuter sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="c96ef-113">La plupart des éléments fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="c96ef-113">Most things work.</span></span> <span data-ttu-id="c96ef-114">Toutefois, vous devez consulter le document [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/) pour identifier les éventuelles incompatibilités.</span><span class="sxs-lookup"><span data-stu-id="c96ef-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="c96ef-115">Pour obtenir une version Java de ce projet, qui fonctionne avec HDInsight Linux ou Windows, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c96ef-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c96ef-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c96ef-116">Prerequisites</span></span>

* <span data-ttu-id="c96ef-117">Un utilisateur Azure Active Directory avec un accès [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="c96ef-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="c96ef-118">Un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-118">An HDInsight cluster.</span></span> <span data-ttu-id="c96ef-119">Pour plus d’informations, consultez [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c96ef-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c96ef-120">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="c96ef-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c96ef-121">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c96ef-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c96ef-122">Visual Studio (l'une des versions suivantes)</span><span class="sxs-lookup"><span data-stu-id="c96ef-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="c96ef-123">Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="c96ef-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="c96ef-124">Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="c96ef-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="c96ef-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c96ef-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="c96ef-126">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="c96ef-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="c96ef-127">Les outils HDInsight pour Visual Studio : consultez [Prise en main des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) pour plus d'informations sur l'installation.</span><span class="sxs-lookup"><span data-stu-id="c96ef-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c96ef-128">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="c96ef-128">How it works</span></span>

<span data-ttu-id="c96ef-129">Cet exemple contient une topologie Storm en C# qui génère de façon aléatoire les données du journal Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="c96ef-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="c96ef-130">Ces données sont ensuite écrites dans une base de données SQL à partir de laquelle elles sont utilisées pour générer des rapports dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="c96ef-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="c96ef-131">Les fichiers suivants implémentent la fonctionnalité principale de cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c96ef-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="c96ef-132">**SqlAzureBolt.cs**: écrit les informations produites au sein de la topologie Storm dans la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c96ef-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="c96ef-133">**IISLogsTable.sql**: instructions Transact-SQL utilisées pour générer la base de données dans laquelle les données sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c96ef-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="c96ef-134">Créez la table dans la base de données SQL avant de démarrer la topologie sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="c96ef-135">Télécharger l'exemple</span><span class="sxs-lookup"><span data-stu-id="c96ef-135">Download the example</span></span>

<span data-ttu-id="c96ef-136">Téléchargez l’ [exemple HDInsight C# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="c96ef-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="c96ef-137">Pour le télécharger, clonez-le/répliquez-le à l'aide de [git](http://git-scm.com/)ou utilisez le lien **Télécharger** pour télécharger un fichier zip de l'archive.</span><span class="sxs-lookup"><span data-stu-id="c96ef-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="c96ef-138">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="c96ef-138">Create a database</span></span>

1. <span data-ttu-id="c96ef-139">Pour créer une base de données, suivez les étapes du document [Didacticiel sur la base de données SQL](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c96ef-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="c96ef-140">Connectez-vous à la base de données en suivant les étapes décrites dans le document [Se connecter à la base de données SQL avec Visual Studio](../sql-database/sql-database-connect-query.md).</span><span class="sxs-lookup"><span data-stu-id="c96ef-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="c96ef-141">Dans l’Explorateur d’objets, cliquez avec le bouton droit sur la base de données et sélectionnez **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="c96ef-142">Collez le contenu du fichier **IISLogsTable.sql** inclus dans le projet téléchargé dans la fenêtre de requête, puis utilisez Ctrl + Maj + E pour exécuter la requête.</span><span class="sxs-lookup"><span data-stu-id="c96ef-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="c96ef-143">Vous devez recevoir un message indiquant que l’exécution des commandes s’est terminée correctement.</span><span class="sxs-lookup"><span data-stu-id="c96ef-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="c96ef-144">Configurer l'exemple</span><span class="sxs-lookup"><span data-stu-id="c96ef-144">Configure the sample</span></span>

1. <span data-ttu-id="c96ef-145">Dans le [Portail Azure](https://portal.azure.com), sélectionnez votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c96ef-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="c96ef-146">À partir de la section **Essentials** du panneau Base de données SQL, sélectionnez **Afficher les chaînes de connexion de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="c96ef-147">Dans la liste qui s’affiche, copiez les informations **ADO.NET (Authentification SQL)** .</span><span class="sxs-lookup"><span data-stu-id="c96ef-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="c96ef-148">Ouvrez l'exemple dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c96ef-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="c96ef-149">Dans **l’Explorateur de solutions**, ouvrez le fichier **App.config**, puis recherchez l’entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="c96ef-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="c96ef-150">Remplacez la valeur **TOBEFILLED ## ##** par la chaîne de connexion de base de données copiée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c96ef-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="c96ef-151">Remplacez **{your\_username}** et **{your\_password}** par le nom d’utilisateur et le mot de passe d’accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="c96ef-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="c96ef-152">Enregistrez et fermez les fichiers.</span><span class="sxs-lookup"><span data-stu-id="c96ef-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="c96ef-153">Déployer l'exemple</span><span class="sxs-lookup"><span data-stu-id="c96ef-153">Deploy the sample</span></span>

1. <span data-ttu-id="c96ef-154">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **StormToSQL** et sélectionnez **Envoyer à Storm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="c96ef-155">Sélectionnez le cluster HDInsight dans la liste déroulante **Cluster Storm** de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c96ef-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c96ef-156">L'affichage des noms de serveur dans la liste déroulante **Cluster Storm** peut prendre plusieurs secondes.</span><span class="sxs-lookup"><span data-stu-id="c96ef-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="c96ef-157">Si vous y êtes invité, entrez les informations d’identification de connexion pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c96ef-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="c96ef-158">Si vous disposez de plusieurs abonnements, connectez-vous à celui qui contient votre cluster Storm dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="c96ef-159">Une fois la topologie envoyée, la __Visionneuse de topologies__ apparaît.</span><span class="sxs-lookup"><span data-stu-id="c96ef-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="c96ef-160">Pour afficher cette topologie, sélectionnez l’entrée SqlAzureWriterTopology dans la liste.</span><span class="sxs-lookup"><span data-stu-id="c96ef-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Les topologies, avec la topologie sélectionnée](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="c96ef-162">Vous pouvez utiliser cette vue pour afficher des informations sur la topologie. Sinon, double-cliquez sur une entrée (telle que SqlAzureBolt) pour afficher des informations spécifiques à un composant dans la topologie.</span><span class="sxs-lookup"><span data-stu-id="c96ef-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="c96ef-163">Après quelques minutes d’exécution de la topologie, revenez à la fenêtre de requête SQL utilisée pour créer la base de données.</span><span class="sxs-lookup"><span data-stu-id="c96ef-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="c96ef-164">Remplacez les instructions existantes par la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="c96ef-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="c96ef-165">Utilisez Ctrl+Maj+E pour exécuter la requête. Vous devriez recevoir des résultats similaires aux données suivantes :</span><span class="sxs-lookup"><span data-stu-id="c96ef-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="c96ef-166">Ces données ont été écrites à partir de la topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="c96ef-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="c96ef-167">Créer un rapport</span><span class="sxs-lookup"><span data-stu-id="c96ef-167">Create a report</span></span>

1. <span data-ttu-id="c96ef-168">Connectez-vous au [connecteur de base de données SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="c96ef-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="c96ef-169">Dans **Databases** (Bases de données), sélectionnez **Get** (Obtenir).</span><span class="sxs-lookup"><span data-stu-id="c96ef-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="c96ef-170">Sélectionnez **Azure SQL Database** (Base de données SQL Microsoft Azure), puis sélectionnez **Connect** (Se connecter).</span><span class="sxs-lookup"><span data-stu-id="c96ef-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c96ef-171">Vous pouvez être invité à télécharger Power BI Desktop pour continuer.</span><span class="sxs-lookup"><span data-stu-id="c96ef-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="c96ef-172">Pour ce faire, procédez comme suit pour vous connecter :</span><span class="sxs-lookup"><span data-stu-id="c96ef-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="c96ef-173">Ouvrez Power BI Desktop et sélectionnez __obtenir les données__.</span><span class="sxs-lookup"><span data-stu-id="c96ef-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="c96ef-174">2 - Sélectionnez __Azure__, puis sélectionnez __Base de données Azure SQL__.</span><span class="sxs-lookup"><span data-stu-id="c96ef-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="c96ef-175">Entrez les informations pour vous connecter à votre base de données SQL Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c96ef-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="c96ef-176">Vous trouverez ces informations en accédant au [portail Azure](https://portal.azure.com) et en sélectionnant votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c96ef-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c96ef-177">Vous pouvez également définir l’intervalle d’actualisation et les filtres personnalisés à l’aide de l’option **Activer les options avancées** de la boîte de dialogue de connexion.</span><span class="sxs-lookup"><span data-stu-id="c96ef-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="c96ef-178">Une fois connecté, vous verrez un nouveau jeu de données portant le même nom que la base de données à laquelle vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="c96ef-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="c96ef-179">Sélectionnez ce jeu de données pour commencer à concevoir un rapport.</span><span class="sxs-lookup"><span data-stu-id="c96ef-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="c96ef-180">Dans **Champs**, développez l’entrée **IISLOGS**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="c96ef-181">Pour créer un rapport qui répertorie les racines URI, sélectionnez la case à cocher **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Création d’un rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="c96ef-183">Ensuite, faites glisser **METHOD** vers le rapport.</span><span class="sxs-lookup"><span data-stu-id="c96ef-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="c96ef-184">Le rapport se met à jour pour répertorier les ressources et la méthode HTTP correspondante utilisée pour la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="c96ef-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![ajout des données de la méthode](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="c96ef-186">À partir de la colonne **Visualisations**, sélectionnez l’icône **Champs**, puis sélectionnez la flèche vers le bas en regard de **METHOD** dans la section **Valeurs**.</span><span class="sxs-lookup"><span data-stu-id="c96ef-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="c96ef-187">Pour afficher un compteur pour le nombre d’accès à un URI, sélectionnez **Compteur**</span><span class="sxs-lookup"><span data-stu-id="c96ef-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Modification d’un nombre de méthodes](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="c96ef-189">Ensuite, sélectionnez **Histogramme empilé** pour modifier l’affichage des informations.</span><span class="sxs-lookup"><span data-stu-id="c96ef-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Transformation en graphique empilé](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="c96ef-191">Pour enregistrer le rapport, sélectionnez **Enregistrer** et entrez un nom pour le rapport.</span><span class="sxs-lookup"><span data-stu-id="c96ef-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="c96ef-192">Arrêt de la topologie</span><span class="sxs-lookup"><span data-stu-id="c96ef-192">Stop the topology</span></span>

<span data-ttu-id="c96ef-193">La topologie continue de s’exécuter jusqu’à ce qu’elle soit arrêtée ou supprimée du cluster Storm dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c96ef-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="c96ef-194">Pour arrêter la topologie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c96ef-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="c96ef-195">Dans Visual Studio, retournez dans la Visionneuse de topologies et sélectionnez la topologie.</span><span class="sxs-lookup"><span data-stu-id="c96ef-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="c96ef-196">Sélectionnez le bouton **Arrêter** pour arrêter la topologie.</span><span class="sxs-lookup"><span data-stu-id="c96ef-196">Select the **Kill** button to stop the topology.</span></span>

    ![Bouton Arrêter dans le résumé de la topologie](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="c96ef-198">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="c96ef-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="c96ef-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c96ef-199">Next steps</span></span>

<span data-ttu-id="c96ef-200">Dans ce document, vous avez appris à envoyer des données d’une topologie Storm vers une base de données SQL, puis à visualiser les données à l’aide de Power BI.</span><span class="sxs-lookup"><span data-stu-id="c96ef-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="c96ef-201">Pour plus d’informations sur l’utilisation des autres technologies Azure à l’aide de Storm dans HDInsight, consultez le document suivant :</span><span class="sxs-lookup"><span data-stu-id="c96ef-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="c96ef-202">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c96ef-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
