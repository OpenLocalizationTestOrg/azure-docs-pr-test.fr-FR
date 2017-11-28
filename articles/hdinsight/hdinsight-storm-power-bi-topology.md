---
title: aaaUse Apache Storm avec Power BI - Azure HDInsight | Documents Microsoft
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="d16da-103">Utiliser les données de toovisualize Power BI à partir d’une topologie d’Apache Storm</span><span class="sxs-lookup"><span data-stu-id="d16da-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="d16da-104">Power BI vous permet d’afficher les données toovisually sous forme de rapports.</span><span class="sxs-lookup"><span data-stu-id="d16da-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="d16da-105">Ce document fournit un exemple de procédure toouse Apache Storm sur les données de toogenerate HDInsight pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="d16da-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="d16da-106">Hello étapes décrites dans ce document reposent sur un environnement de développement Windows avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d16da-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="d16da-107">projet compilé de Hello peut être soumis tooa HDInsight de basés sur Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="d16da-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d16da-108">Seuls les clusters basés sur Linux créés après le 28/10/2016 prennent en charge les topologies SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="d16da-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="d16da-109">toouse une topologie c# avec un cluster basé sur Linux, hello de mise à jour de package NuGet de Microsoft.SCP.Net.SDK utilisé par votre projet de tooversion 0.10.0.6 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d16da-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="d16da-110">version Hello du package de hello doit également correspondre version majeure de hello de Storm installé sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d16da-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="d16da-111">Par exemple, Storm sur les versions 3.3 et 3.4 de HDInsight utilise Storm 0.10.x, tandis que HDInsight 3.5 utilise Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="d16da-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="d16da-112">Topologies c# sur des clusters basés sur Linux doivent utiliser .NET 4.5 et utiliser toorun Mono sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="d16da-113">La plupart des éléments fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="d16da-113">Most things work.</span></span> <span data-ttu-id="d16da-114">Toutefois, vous devez vérifier hello [Mono compatibilité](http://www.mono-project.com/docs/about-mono/compatibility/) document pour identifier les éventuelles incompatibilités.</span><span class="sxs-lookup"><span data-stu-id="d16da-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="d16da-115">Pour obtenir une version Java de ce projet, qui fonctionne avec HDInsight Linux ou Windows, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d16da-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d16da-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d16da-116">Prerequisites</span></span>

* <span data-ttu-id="d16da-117">Un utilisateur Azure Active Directory avec un accès [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="d16da-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="d16da-118">Un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d16da-118">An HDInsight cluster.</span></span> <span data-ttu-id="d16da-119">Pour plus d’informations, consultez [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d16da-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d16da-120">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="d16da-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d16da-121">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d16da-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d16da-122">(L’une des versions suivantes de hello) de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d16da-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="d16da-123">Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d16da-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="d16da-124">Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d16da-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="d16da-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d16da-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="d16da-126">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="d16da-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="d16da-127">Hello outils HDInsight pour Visual Studio : consultez [prise en main à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) pour plus d’informations sur les informations d’installation.</span><span class="sxs-lookup"><span data-stu-id="d16da-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="d16da-128">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="d16da-128">How it works</span></span>

<span data-ttu-id="d16da-129">Cet exemple contient une topologie Storm en C# qui génère de façon aléatoire les données du journal Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="d16da-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="d16da-130">Ces données sont ensuite écrites tooa base de données SQL, et à partir de là, il est utilisé toogenerate des rapports dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="d16da-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="d16da-131">Hello suivant fichiers implémentent hello principales fonctionnalités de cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d16da-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="d16da-132">**SqlAzureBolt.cs**: écrit les informations de produit dans hello Storm topologie tooSQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="d16da-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="d16da-133">**IISLogsTable.sql**: hello Transact-SQL instructions utilisées toogenerate hello base de données stockées dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d16da-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="d16da-134">Créer la table de hello dans la base de données SQL avant le début de la topologie de hello sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d16da-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="d16da-135">Télécharger l’exemple de hello</span><span class="sxs-lookup"><span data-stu-id="d16da-135">Download hello example</span></span>

<span data-ttu-id="d16da-136">Télécharger hello [exemple de HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="d16da-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="d16da-137">toodownload, une branche/clonage à l’aide de [git](http://git-scm.com/), ou utilisez hello **télécharger** toodownload de lier un fichier ZIP d’archive de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="d16da-138">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="d16da-138">Create a database</span></span>

1. <span data-ttu-id="d16da-139">toocreate une base de données, utilisez les étapes de hello Bonjour [didacticiel de base de données SQL](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="d16da-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="d16da-140">Base de données toohello de se connecter par hello suivant les étapes dans hello [connecter tooa base de données SQL avec Visual Studio](../sql-database/sql-database-connect-query.md) document.</span><span class="sxs-lookup"><span data-stu-id="d16da-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="d16da-141">Dans l’Explorateur d’objets, avec le bouton droit de la base de données hello et sélectionnez **nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="d16da-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="d16da-142">Coller le contenu de hello hello **IISLogsTable.sql** fichier inclus dans hello téléchargé le projet dans la fenêtre de requête hello, puis utilisez Ctrl + Maj + E tooexecute hello requête.</span><span class="sxs-lookup"><span data-stu-id="d16da-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="d16da-143">Vous devez recevoir un message qui hello commandes s’est terminées correctement.</span><span class="sxs-lookup"><span data-stu-id="d16da-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="d16da-144">Configurer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d16da-144">Configure hello sample</span></span>

1. <span data-ttu-id="d16da-145">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="d16da-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="d16da-146">À partir de hello **Essentials** section hello de base de données du Panneau de SQL, sélectionnez **afficher les chaînes de connexion de base de données**.</span><span class="sxs-lookup"><span data-stu-id="d16da-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="d16da-147">À partir de la liste hello qui s’affiche, copiez hello **ADO.NET (authentification SQL)** plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d16da-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="d16da-148">Ouvrez l’exemple hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d16da-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="d16da-149">À partir de **l’Explorateur de solutions**, ouvrez hello **App.config** de fichiers et recherchez hello entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="d16da-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="d16da-150">Remplacez hello **TOBEFILLED ## ##** valeur avec la chaîne de connexion de base de données hello copiée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="d16da-151">Remplacez **{votre\_nom d’utilisateur}** et **{votre\_mot de passe}** avec le nom d’utilisateur hello et le mot de passe pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="d16da-152">Enregistrez et fermez les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="d16da-153">Déployer l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d16da-153">Deploy hello sample</span></span>

1. <span data-ttu-id="d16da-154">À partir de **l’Explorateur de solutions**, avec le bouton hello **StormToSQL** de projet et sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d16da-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d16da-155">Cluster HDInsight de hello SELECT à partir de hello **Cluster Storm** boîte de dialogue de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d16da-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d16da-156">Il peut prendre quelques secondes que hello **Cluster Storm** toopopulate de liste déroulante des noms de serveur.</span><span class="sxs-lookup"><span data-stu-id="d16da-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="d16da-157">Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d16da-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="d16da-158">Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d16da-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d16da-159">Lors de la topologie de hello a été envoyée, hello __visionneuse de topologie__ s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d16da-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="d16da-160">tooview cette topologie, l’entrée de SqlAzureWriterTopology hello select à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologies de Hello, avec la topologie hello sélectionné](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="d16da-162">Vous pouvez utiliser cette toosee afficher des informations sur la topologie de hello ou double-cliquez sur un composant entrée (par exemple hello SqlAzureBolt) toosee informations tooa spécifique dans une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="d16da-163">Après avoir hello topologie a exécuté pendant quelques minutes, fenêtre de requête SQL toohello retour vous avez utilisé la base de données toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="d16da-164">Remplacez les instructions existantes hello hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="d16da-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="d16da-165">Utilisez Ctrl + Maj + requête de hello tooexecute E et vous devez réception toohello similaire de résultats données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d16da-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="d16da-166">Ces données ont été écrites à partir de la topologie de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="d16da-167">Créer un rapport</span><span class="sxs-lookup"><span data-stu-id="d16da-167">Create a report</span></span>

1. <span data-ttu-id="d16da-168">Se connecter toohello [connecteur de base de données SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="d16da-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="d16da-169">Dans **Databases** (Bases de données), sélectionnez **Get** (Obtenir).</span><span class="sxs-lookup"><span data-stu-id="d16da-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="d16da-170">Sélectionnez **Azure SQL Database** (Base de données SQL Microsoft Azure), puis sélectionnez **Connect** (Se connecter).</span><span class="sxs-lookup"><span data-stu-id="d16da-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d16da-171">Vous pouvez être invité à toodownload hello Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d16da-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="d16da-172">Dans ce cas, utilisez hello suivant les étapes tooconnect :</span><span class="sxs-lookup"><span data-stu-id="d16da-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="d16da-173">Ouvrez Power BI Desktop et sélectionnez __obtenir les données__.</span><span class="sxs-lookup"><span data-stu-id="d16da-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="d16da-174">2 - Sélectionnez __Azure__, puis sélectionnez __Base de données Azure SQL__.</span><span class="sxs-lookup"><span data-stu-id="d16da-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="d16da-175">Entrez hello informations tooconnect tooyour base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d16da-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="d16da-176">Vous pouvez trouver ces informations en visitant hello [portail Azure](https://portal.azure.com) et en sélectionnant votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="d16da-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d16da-177">Vous pouvez également définir un intervalle d’actualisation hello et des filtres personnalisés à l’aide de **activer les Options avancées** hello à partir de la boîte de dialogue connexion.</span><span class="sxs-lookup"><span data-stu-id="d16da-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="d16da-178">Une fois que vous vous êtes connecté, vous verrez un nouveau dataset avec hello que même nom en tant que base de données hello, vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="d16da-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="d16da-179">Sélectionnez toobegin de jeu de données hello conception d’un rapport.</span><span class="sxs-lookup"><span data-stu-id="d16da-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="d16da-180">À partir de **champs**, développez hello **IISLOGS** entrée.</span><span class="sxs-lookup"><span data-stu-id="d16da-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="d16da-181">toocreate provient d’un rapport que listes hello URI, cochez la case hello **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="d16da-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Création d’un rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="d16da-183">Ensuite, faites glisser **méthode** toohello rapport.</span><span class="sxs-lookup"><span data-stu-id="d16da-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="d16da-184">Bonjour rapport mises à jour toolist Bonjour découle et méthode HTTP correspondante de hello utilisé pour hello requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="d16da-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Ajout de données de la méthode hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="d16da-186">À partir de hello **visualisations** colonne, sélectionnez hello **champs** icône, puis sélectionnez hello bas ensuite trop**méthode** Bonjour **valeurs**section.</span><span class="sxs-lookup"><span data-stu-id="d16da-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="d16da-187">toodisplay a accédé au nombre de combien de fois un URI, sélectionnez **nombre**.</span><span class="sxs-lookup"><span data-stu-id="d16da-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Nombre de tooa des méthodes de modification](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="d16da-189">Ensuite, sélectionnez hello **empilé** toochange affichage des informations de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Modification tooa empilé](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="d16da-191">rapport de hello toosave, sélectionnez **enregistrer** et entrez un nom pour le rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d16da-192">Arrêter la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="d16da-192">Stop hello topology</span></span>

<span data-ttu-id="d16da-193">topologie de Hello continue toorun jusqu'à ce que vous l’arrêtez ou supprimez hello Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d16da-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="d16da-194">toostop hello topologie, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d16da-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="d16da-195">Dans Visual Studio, renvoyer la visionneuse de topologie toohello et sélectionnez hello topologie.</span><span class="sxs-lookup"><span data-stu-id="d16da-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="d16da-196">Sélectionnez hello **Kill** topologie de bouton toostop hello.</span><span class="sxs-lookup"><span data-stu-id="d16da-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill sur la topologie hello résumé bouton](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="d16da-198">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="d16da-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d16da-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d16da-199">Next steps</span></span>

<span data-ttu-id="d16da-200">Dans ce document, vous avez appris comment le toosend des données à partir d’un tooSQL de topologie tempête de base de données, puis pour visualiser les données hello à l’aide de Power BI.</span><span class="sxs-lookup"><span data-stu-id="d16da-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="d16da-201">Pour plus d’informations sur la façon de toowork avec d’autres technologies Azure à l’aide de Storm sur HDInsight, consultez hello suivant du document :</span><span class="sxs-lookup"><span data-stu-id="d16da-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="d16da-202">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d16da-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
