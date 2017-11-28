---
title: "Exécuter un travail Hadoop avec Azure Cosmos DB et HDInsight | Microsoft Docs"
description: "Découvrez comment exécuter un travail Hive, Pig ou MapReduce simple avec Azure Cosmos DB et Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="f8d19-103"><a name="Azure Cosmos DB-HDInsight"></a>Exécuter un travail Apache Hive, Pig ou Hadoop avec Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="f8d19-104">Ce didacticiel vous montre comment exécuter des travaux [Apache Hive][apache-hive], [Apache Pig][apache-pig] et [Apache Hadoop][apache-hadoop] MapReduce dans Azure HDInsight avec le connecteur Hadoop de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="f8d19-105">Le connecteur Hadoop de Cosmos DB permet à Cosmos DB d’agir en tant que source et récepteur pour les travaux Hive, Pig et MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f8d19-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="f8d19-106">Ce didacticiel utilise Cosmos DB en tant que source de données et destination pour les travaux Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f8d19-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="f8d19-107">Après avoir terminé ce didacticiel, vous serez en mesure de répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f8d19-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="f8d19-108">Comment charger des données à partir de Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="f8d19-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="f8d19-109">Comment stocker des données dans Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="f8d19-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="f8d19-110">Nous vous recommandons de commencer par visionner la vidéo suivante, où nous détaillons l’exécution d’un travail Hive avec Cosmos DB et HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="f8d19-111">Revenez ensuite à cet article pour obtenir des détails complets sur l’exécution de travaux d’analyse concernant vos données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="f8d19-112">Ce didacticiel part du principe que vous avez déjà utilisé Apache Hadoop, Hive et/ou Pig.</span><span class="sxs-lookup"><span data-stu-id="f8d19-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="f8d19-113">Si vous débutez avec Apache Hadoop, Hive et Pig, nous vous recommandons de commencer par consulter la [documentation Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="f8d19-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="f8d19-114">Ce didacticiel suppose également que vous avez déjà utilisé Cosmos DB et que vous possédez un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="f8d19-115">Si vous n’avez jamais utilisé Cosmos DB ou si vous ne possédez pas de compte Cosmos DB, consultez notre page [Prise en main][getting-started].</span><span class="sxs-lookup"><span data-stu-id="f8d19-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="f8d19-116">Vous n'avez pas le temps de suivre le didacticiel et vous souhaitez seulement obtenir des scripts PowerShell d'exemple pour Hive, Pig et MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="f8d19-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="f8d19-117">Ce n’est pas un problème. Vous pouvez les obtenir [ici][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="f8d19-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="f8d19-118">Le téléchargement contient également les fichiers hql, pig et java pour ces exemples.</span><span class="sxs-lookup"><span data-stu-id="f8d19-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="f8d19-119"><a name="NewestVersion"></a>Version la plus récente</span><span class="sxs-lookup"><span data-stu-id="f8d19-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="f8d19-120">Version du connecteur Hadoop</span><span class="sxs-lookup"><span data-stu-id="f8d19-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="f8d19-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="f8d19-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="f8d19-122">URI du script</span><span class="sxs-lookup"><span data-stu-id="f8d19-122">Script Uri</span></span></th>
        <td><span data-ttu-id="f8d19-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="f8d19-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="f8d19-124">Date de modification</span><span class="sxs-lookup"><span data-stu-id="f8d19-124">Date Modified</span></span></th>
        <td><span data-ttu-id="f8d19-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="f8d19-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="f8d19-126">Versions de HDInsight prises en charge</span><span class="sxs-lookup"><span data-stu-id="f8d19-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="f8d19-127">3.1, 3.2.</span><span class="sxs-lookup"><span data-stu-id="f8d19-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="f8d19-128">Journal des modifications</span><span class="sxs-lookup"><span data-stu-id="f8d19-128">Change Log</span></span></th>
        <td><span data-ttu-id="f8d19-129">Mise à jour du Kit de développement logiciel (SDK) Azure Cosmos DB vers la version 1.6.0</span><span class="sxs-lookup"><span data-stu-id="f8d19-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="f8d19-130">Prise en charge ajoutée pour les collections partitionnées en tant que source et récepteur</span><span class="sxs-lookup"><span data-stu-id="f8d19-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="f8d19-131"><a name="Prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f8d19-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f8d19-132">Avant de suivre les instructions de ce didacticiel, assurez-vous de disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f8d19-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="f8d19-133">Un compte Cosmos DB, une base de données et une collection de documents.</span><span class="sxs-lookup"><span data-stu-id="f8d19-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="f8d19-134">Pour plus d’informations, consultez la page [Getting Started with Cosmos DB (Prise en main de Cosmos DB)][getting-started].</span><span class="sxs-lookup"><span data-stu-id="f8d19-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="f8d19-135">Importez des exemples de données dans votre compte Cosmos DB avec [l’outil d’importation de Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="f8d19-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="f8d19-136">Débit.</span><span class="sxs-lookup"><span data-stu-id="f8d19-136">Throughput.</span></span> <span data-ttu-id="f8d19-137">Les lectures et écritures à partir de HDInsight seront comptabilisées sur vos unités de demande allouées pour vos collections.</span><span class="sxs-lookup"><span data-stu-id="f8d19-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="f8d19-138">Capacité pour une procédure stockée supplémentaire dans chaque collection de sortie.</span><span class="sxs-lookup"><span data-stu-id="f8d19-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="f8d19-139">Les procédures stockées sont utilisées pour le transfert des documents résultants.</span><span class="sxs-lookup"><span data-stu-id="f8d19-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="f8d19-140">Capacité pour les documents obtenus à partir des tâches Hive, Pig ou MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f8d19-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="f8d19-141">[*Facultatif*] Capacité pour une collection supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="f8d19-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="f8d19-142">Pour empêcher la création d'une collection au cours d'une des tâches, vous pouvez imprimer les résultats vers stdout, enregistrer la sortie dans votre conteneur WASB ou sélectionner une collection existante.</span><span class="sxs-lookup"><span data-stu-id="f8d19-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="f8d19-143">Si vous spécifiez une collection existante, des documents seront créés au sein de la collection et les documents existants ne seront affectés qu’en cas de conflit dans *ids*.</span><span class="sxs-lookup"><span data-stu-id="f8d19-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="f8d19-144">**Le connecteur écrasera automatiquement les documents existants présentant des conflits d’ID**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="f8d19-145">Vous pouvez désactiver cette fonctionnalité en réglant l'option upsert sur false.</span><span class="sxs-lookup"><span data-stu-id="f8d19-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="f8d19-146">Si l'option upsert est réglée sur false et qu'un conflit se produit, la tâche Hadoop échoue et une erreur liée à un conflit ID est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="f8d19-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="f8d19-147"><a name="ProvisionHDInsight"></a>Étape 1 : créer un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="f8d19-148">Ce didacticiel utilise une action de script à partir du portail Azure pour personnaliser votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="f8d19-149">Dans ce didacticiel, nous allons utiliser le portail Azure pour créer votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="f8d19-150">Pour connaître les instructions liées à l’utilisation des applets de commande PowerShell ou du Kit de développement logiciel (SDK) .NET HDInsight, consultez l’article [Personnaliser les clusters HDInsight à l’aide d’une action de script][hdinsight-custom-provision].</span><span class="sxs-lookup"><span data-stu-id="f8d19-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="f8d19-151">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f8d19-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="f8d19-152">Cliquez sur **+ Nouveau** dans la barre de navigation en haut à gauche, recherchez **HDInsight** dans la barre de recherche supérieure du panneau Nouveau.</span><span class="sxs-lookup"><span data-stu-id="f8d19-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="f8d19-153">**HDInsight** publié par **Microsoft** s’affiche en haut des résultats.</span><span class="sxs-lookup"><span data-stu-id="f8d19-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="f8d19-154">Cliquez dessus, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="f8d19-155">Dans le panneau de création du cluster HDInsight, saisissez le **nom du cluster** et sélectionnez **l’abonnement** de votre choix pour l’approvisionnement de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="f8d19-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="f8d19-156">Nom du cluster</span><span class="sxs-lookup"><span data-stu-id="f8d19-156">Cluster name</span></span></td><td><span data-ttu-id="f8d19-157">Nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="f8d19-157">Name the cluster.</span></span><br/>
<span data-ttu-id="f8d19-158">Le nom DNS doit commencer et finir par un caractère alphanumérique et peut contenir des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="f8d19-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="f8d19-159">Le champ doit être une chaîne comportant entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="f8d19-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="f8d19-160">Nom d'abonnement</span><span class="sxs-lookup"><span data-stu-id="f8d19-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="f8d19-161">Si vous avez plusieurs abonnements Azure, sélectionnez celui qui hébergera votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="f8d19-162">
5. Cliquez sur **Sélectionner un type de cluster** et définissez les propriétés suivantes avec les valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="f8d19-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="f8d19-163">Type de cluster</span><span class="sxs-lookup"><span data-stu-id="f8d19-163">Cluster type</span></span></td><td><span data-ttu-id="f8d19-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="f8d19-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f8d19-165">Niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="f8d19-165">Cluster tier</span></span></td><td><span data-ttu-id="f8d19-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="f8d19-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f8d19-167">Système d'exploitation</span><span class="sxs-lookup"><span data-stu-id="f8d19-167">Operating System</span></span></td><td><span data-ttu-id="f8d19-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="f8d19-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="f8d19-169">Version</span><span class="sxs-lookup"><span data-stu-id="f8d19-169">Version</span></span></td><td><span data-ttu-id="f8d19-170">version la plus récente</span><span class="sxs-lookup"><span data-stu-id="f8d19-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="f8d19-171">Maintenant, cliquez sur **SÉLECTIONNER**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-171">Now, click **SELECT**.</span></span>

    ![Fournir des détails du cluster initial Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="f8d19-173">Cliquez sur **Informations d’identification** pour configurer votre connexion et les informations d’identification d’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="f8d19-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="f8d19-174">Choisissez le **nom de connexion au cluster** et le **mot de passe de connexion au cluster**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="f8d19-175">Si vous souhaitez accéder à votre cluster à distance, sélectionnez *Oui* en bas du panneau et indiquez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f8d19-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="f8d19-176">Cliquez sur **Source de données** pour définir votre emplacement principal pour accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="f8d19-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="f8d19-177">Choisissez la **méthode de sélection** et spécifiez un compte de stockage existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="f8d19-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="f8d19-178">Dans le même panneau, spécifiez un **conteneur par défaut** et un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="f8d19-179">Et cliquez sur **SÉLECTIONNER**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f8d19-180">Pour de meilleures performances, sélectionnez un emplacement proche de la région de votre compte Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f8d19-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="f8d19-181">Cliquez sur **Tarification** pour sélectionner le nombre et le type de nœuds.</span><span class="sxs-lookup"><span data-stu-id="f8d19-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="f8d19-182">Vous pouvez conserver la configuration par défaut et augmenter le nombre de nœuds Worker ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f8d19-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="f8d19-183">Cliquez sur **Configuration facultative**, puis sur **Actions de script** dans le panneau Configuration facultative.</span><span class="sxs-lookup"><span data-stu-id="f8d19-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="f8d19-184">Dans Actions de script, tapez les informations suivantes pour personnaliser votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="f8d19-185">Propriété</span><span class="sxs-lookup"><span data-stu-id="f8d19-185">Property</span></span></th><th><span data-ttu-id="f8d19-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="f8d19-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="f8d19-187">Nom</span><span class="sxs-lookup"><span data-stu-id="f8d19-187">Name</span></span></td>
             <td><span data-ttu-id="f8d19-188">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="f8d19-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="f8d19-189">URI du script</span><span class="sxs-lookup"><span data-stu-id="f8d19-189">Script URI</span></span></td>
             <td><span data-ttu-id="f8d19-190">Spécifiez l'URI du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="f8d19-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="f8d19-191">Entrez :</span><span class="sxs-lookup"><span data-stu-id="f8d19-191">Please enter:</span></span> </br> <span data-ttu-id="f8d19-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f8d19-193">Nœud principal</span><span class="sxs-lookup"><span data-stu-id="f8d19-193">Head</span></span></td>
             <td><span data-ttu-id="f8d19-194">Cliquer sur la case à cocher pour exécuter le script PowerShell sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="f8d19-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="f8d19-195">
             <strong>Activez cette case à cocher</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f8d19-196">Worker</span><span class="sxs-lookup"><span data-stu-id="f8d19-196">Worker</span></span></td>
             <td><span data-ttu-id="f8d19-197">Cliquer sur la case à cocher pour exécuter le script PowerShell sur le nœud Worker.</span><span class="sxs-lookup"><span data-stu-id="f8d19-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="f8d19-198">
             <strong>Activez cette case à cocher</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="f8d19-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="f8d19-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="f8d19-200">Cliquer sur la case à cocher pour exécuter le script PowerShell sur le Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="f8d19-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="f8d19-201">
             <strong>Inutile</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="f8d19-202">parameters</span><span class="sxs-lookup"><span data-stu-id="f8d19-202">Parameters</span></span></td>
             <td><span data-ttu-id="f8d19-203">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="f8d19-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="f8d19-204">
             <strong>Aucun paramètre requis</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="f8d19-205">
11. Créez un **Groupe de ressources** ou utilisez un groupe de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f8d19-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="f8d19-206">12.</span><span class="sxs-lookup"><span data-stu-id="f8d19-206">12.</span></span> <span data-ttu-id="f8d19-207">À présent, activez la case à cocher **Épingler au tableau de bord** pour effectuer le suivi de son déploiement, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="f8d19-208"><a name="InstallCmdlets"></a>Étape 2 : installer et configurer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8d19-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="f8d19-209">Installez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8d19-209">Install Azure PowerShell.</span></span> <span data-ttu-id="f8d19-210">Vous trouverez des instructions [ici][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="f8d19-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="f8d19-211">Pour les requêtes Hive, vous pouvez également utiliser l'éditeur Hive en ligne de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="f8d19-212">Pour ce faire, connectez-vous au [portail Azure][azure-portal], cliquez sur **HDInsight** dans le volet gauche pour afficher la liste de vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="f8d19-213">Cliquez sur le cluster sur lequel vous souhaitez exécuter des requêtes Hive, puis sur **Console de requête**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="f8d19-214">Ouvrez l'environnement de script intégré Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f8d19-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="f8d19-215">Sur un ordinateur exécutant au moins Windows 8 ou Windows Server 2012, vous pouvez utiliser l’outil de recherche intégré.</span><span class="sxs-lookup"><span data-stu-id="f8d19-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="f8d19-216">Dans l’écran d’accueil, tapez **powershell ise**, puis cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="f8d19-217">Sur un ordinateur exécutant une version antérieure à Windows 8 ou Windows Server 2012, utilisez le menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="f8d19-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="f8d19-218">Dans la zone de recherche du menu Démarrer, tapez **Invite de commandes**, puis, dans la liste des résultats, cliquez sur **Invite de commandes**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="f8d19-219">Dans l’invite de commandes, tapez **powershell_ise**, puis cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="f8d19-220">Ajoutez votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f8d19-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="f8d19-221">Dans le volet de la console, tapez **Add-AzureAccount**, puis cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="f8d19-222">Tapez l’adresse de messagerie associée à votre abonnement Azure, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="f8d19-223">Tapez le mot de passe de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f8d19-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="f8d19-224">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f8d19-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="f8d19-225">Le schéma suivant identifie les éléments importants de votre environnement de script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8d19-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagramme d’Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="f8d19-227"><a name="RunHive"></a>Étape 3 : exécuter un travail Hive à l’aide de Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8d19-228">Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="f8d19-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="f8d19-229">Définissez les variables suivantes dans le volet Script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8d19-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="f8d19-230">Commençons à construire votre chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="f8d19-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="f8d19-231">Nous allons écrire une requête Hive qui prend les horodatages générés par le système de tous les documents (_ts) et les ID uniques (_rid) de tous les documents d’une collection Azure Cosmos DB, comptabilise tous les documents à la minute et stocke les résultats dans une nouvelle collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="f8d19-232">Commençons par créer une table Hive à partir de notre collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="f8d19-233">Ajoutez l’extrait de code suivant dans le volet Script PowerShell <strong>après</strong> l’extrait de code 1.</span><span class="sxs-lookup"><span data-stu-id="f8d19-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="f8d19-234">Veillez à inclure le paramètre DocumentDB.query facultatif pour réduire vos documents à _ts et _rid.</span><span class="sxs-lookup"><span data-stu-id="f8d19-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="f8d19-235">**L’attribution du nom DocumentDB.inputCollections n’était pas une erreur.**</span><span class="sxs-lookup"><span data-stu-id="f8d19-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="f8d19-236">Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée :</span><span class="sxs-lookup"><span data-stu-id="f8d19-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="f8d19-237">Créons maintenant une table Hive pour la collection de sortie.</span><span class="sxs-lookup"><span data-stu-id="f8d19-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="f8d19-238">Les propriétés des documents de sortie seront le mois, le jour, l'heure, les minutes et le nombre total d'occurrences.</span><span class="sxs-lookup"><span data-stu-id="f8d19-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f8d19-239">**Une fois encore, l’attribution du nom DocumentDB.outputCollections n’était pas une erreur.**</span><span class="sxs-lookup"><span data-stu-id="f8d19-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="f8d19-240">Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie :</span><span class="sxs-lookup"><span data-stu-id="f8d19-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="f8d19-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="f8d19-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="f8d19-242">Les noms de collection sont séparés sans espace, en utilisant uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="f8d19-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="f8d19-243">Les documents seront distribués en tourniquet (round robin), sur plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="f8d19-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="f8d19-244">Un lot de documents sera stocké dans une collection, puis un deuxième lot de documents sera stocké dans la collection suivante, etc.</span><span class="sxs-lookup"><span data-stu-id="f8d19-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="f8d19-245">Pour terminer, nous allons calculer les documents par mois, jour, heure et minutes et insérer les résultats dans la table Hive de sortie.</span><span class="sxs-lookup"><span data-stu-id="f8d19-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="f8d19-246">Ajoutez l'extrait de script suivant pour créer une définition de tâche Hive à partir de la requête précédente.</span><span class="sxs-lookup"><span data-stu-id="f8d19-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="f8d19-247">Vous pouvez également utiliser le commutateur -File pour spécifier un fichier de script HiveQL sur HDFS.</span><span class="sxs-lookup"><span data-stu-id="f8d19-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="f8d19-248">Ajoutez l'extrait suivant pour enregistrer l'heure de début et soumettre la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="f8d19-249">Ajoutez le script suivant pour attendre la fin de la tâche Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="f8d19-250">Ajoutez le code suivant pour imprimer la sortie standard et les heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="f8d19-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="f8d19-251">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="f8d19-251">**Run** your new script!</span></span> <span data-ttu-id="f8d19-252">**Cliquez** sur le bouton d’exécution vert.</span><span class="sxs-lookup"><span data-stu-id="f8d19-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="f8d19-253">Vérifiez les résultats.</span><span class="sxs-lookup"><span data-stu-id="f8d19-253">Check the results.</span></span> <span data-ttu-id="f8d19-254">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f8d19-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="f8d19-255">Cliquez sur <strong>Parcourir</strong> dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="f8d19-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="f8d19-256">Cliquez sur <strong>Tout</strong> en haut à droite du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="f8d19-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="f8d19-257">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="f8d19-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="f8d19-258">Recherchez ensuite votre <strong>compte Azure Cosmos DB</strong>, puis votre <strong>base de données Azure Cosmos DB</strong> et votre <strong>collection Azure Cosmos DB</strong> associées à la collection de sortie spécifiée dans votre requête Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="f8d19-259">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="f8d19-260">Vous verrez les résultats de votre requête Hive.</span><span class="sxs-lookup"><span data-stu-id="f8d19-260">You will see the results of your Hive query.</span></span>

   ![Résultats de la requête Hive][image-hive-query-results]

## <span data-ttu-id="f8d19-262"><a name="RunPig"></a>Étape 4 : exécuter un travail Pig à l’aide de Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8d19-263">Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="f8d19-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="f8d19-264">Définissez les variables suivantes dans le volet Script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8d19-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="f8d19-265">Commençons à construire votre chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="f8d19-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="f8d19-266">Nous allons écrire une requête Pig qui accepte les horodatages générés par le système de tous les documents (_ts) et des ID uniques (_rid) à partir d’une collection Azure Cosmos DB, comptabilise tous les documents à la minute, puis stocke les résultats dans une nouvelle collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="f8d19-267">Chargez d’abord des documents Cosmos DB dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="f8d19-268">Ajoutez l’extrait de code suivant dans le volet Script PowerShell <strong>après</strong> l’extrait de code 1 .</span><span class="sxs-lookup"><span data-stu-id="f8d19-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="f8d19-269">Veillez à ajouter une requête DocumentDB au paramètre de requête DocumentDB facultatif pour réduire vos documents à _ts et _rid.</span><span class="sxs-lookup"><span data-stu-id="f8d19-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="f8d19-270">Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée :</span><span class="sxs-lookup"><span data-stu-id="f8d19-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="f8d19-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="f8d19-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="f8d19-272">Les noms de collection sont séparés sans espace, en utilisant uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="f8d19-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="f8d19-273">Les documents seront distribués en tourniquet (round robin), sur plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="f8d19-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="f8d19-274">Un lot de documents sera stocké dans une collection, puis un deuxième lot de documents sera stocké dans la collection suivante, etc.</span><span class="sxs-lookup"><span data-stu-id="f8d19-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="f8d19-275">Nous allons ensuite calculer les documents par mois, jour, heure et minutes et le nombre total d'occurrences.</span><span class="sxs-lookup"><span data-stu-id="f8d19-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="f8d19-276">Pour terminer, nous allons stocker les résultats dans notre nouvelle collection de sortie.</span><span class="sxs-lookup"><span data-stu-id="f8d19-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f8d19-277">Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie :</span><span class="sxs-lookup"><span data-stu-id="f8d19-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="f8d19-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="f8d19-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="f8d19-279">Les noms de collection sont séparés sans espace, en utilisant uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="f8d19-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="f8d19-280">Les documents seront distribués en séquence, sur plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="f8d19-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="f8d19-281">Un lot de documents sera stocké dans une collection, puis un deuxième lot de documents sera stocké dans la collection suivante, etc.</span><span class="sxs-lookup"><span data-stu-id="f8d19-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="f8d19-282">Ajoutez l'extrait de script suivant pour créer une définition de tâche Pig à partir de la requête précédente.</span><span class="sxs-lookup"><span data-stu-id="f8d19-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="f8d19-283">Vous pouvez également utiliser le commutateur -File pour spécifier un fichier de script Pig sur HDFS.</span><span class="sxs-lookup"><span data-stu-id="f8d19-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="f8d19-284">Ajoutez l'extrait suivant pour enregistrer l'heure de début et soumettre la tâche Pig.</span><span class="sxs-lookup"><span data-stu-id="f8d19-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="f8d19-285">Ajoutez le script suivant pour attendre la fin de la tâche Pig.</span><span class="sxs-lookup"><span data-stu-id="f8d19-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="f8d19-286">Ajoutez le code suivant pour imprimer la sortie standard et les heures de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="f8d19-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="f8d19-287">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="f8d19-287">**Run** your new script!</span></span> <span data-ttu-id="f8d19-288">**Cliquez** sur le bouton d’exécution vert.</span><span class="sxs-lookup"><span data-stu-id="f8d19-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="f8d19-289">Vérifiez les résultats.</span><span class="sxs-lookup"><span data-stu-id="f8d19-289">Check the results.</span></span> <span data-ttu-id="f8d19-290">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f8d19-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="f8d19-291">Cliquez sur <strong>Parcourir</strong> dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="f8d19-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="f8d19-292">Cliquez sur <strong>Tout</strong> en haut à droite du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="f8d19-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="f8d19-293">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="f8d19-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="f8d19-294">Recherchez ensuite votre <strong>compte Azure Cosmos DB</strong>, puis votre <strong>base de données Azure Cosmos DB</strong> et votre <strong>collection Azure Cosmos DB</strong> associées à la collection de sortie spécifiée dans votre requête Pig.</span><span class="sxs-lookup"><span data-stu-id="f8d19-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="f8d19-295">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="f8d19-296">Vous verrez les résultats de votre requête Pig.</span><span class="sxs-lookup"><span data-stu-id="f8d19-296">You will see the results of your Pig query.</span></span>

    ![Résultats de la requête Pig][image-pig-query-results]

## <span data-ttu-id="f8d19-298"><a name="RunMapReduce"></a>Étape 5 : exécuter une tâche MapReduce à l’aide d’Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="f8d19-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="f8d19-299">Définissez les variables suivantes dans le volet Script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8d19-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="f8d19-300">Nous allons exécuter une tâche MapReduce qui compte le nombre d’occurrences de chaque propriété de document de votre collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="f8d19-301">Ajoutez cet extrait de script **après** l’extrait ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f8d19-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="f8d19-302">TallyProperties-v01.jar est fourni avec l’installation personnalisée du connecteur Hadoop Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8d19-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="f8d19-303">Ajoutez la commande suivante pour soumettre la tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f8d19-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="f8d19-304">En plus de la définition de la tâche MapReduce, fournissez également le nom du cluster HDInsight sur lequel vous souhaitez exécuter la tâche MapReduce, ainsi que les informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="f8d19-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="f8d19-305">Start-AzureHDInsightJob est un appel asynchrone.</span><span class="sxs-lookup"><span data-stu-id="f8d19-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="f8d19-306">Pour vérifier que la tâche est terminée, utilisez la cmdlet *Wait-AzureHDInsightJob* .</span><span class="sxs-lookup"><span data-stu-id="f8d19-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="f8d19-307">Ajoutez la commande suivante pour déterminer si l'exécution de la tâche MapReduce génère des erreurs.</span><span class="sxs-lookup"><span data-stu-id="f8d19-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="f8d19-308">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="f8d19-308">**Run** your new script!</span></span> <span data-ttu-id="f8d19-309">**Cliquez** sur le bouton d’exécution vert.</span><span class="sxs-lookup"><span data-stu-id="f8d19-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="f8d19-310">Vérifiez les résultats.</span><span class="sxs-lookup"><span data-stu-id="f8d19-310">Check the results.</span></span> <span data-ttu-id="f8d19-311">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f8d19-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="f8d19-312">Cliquez sur <strong>Parcourir</strong> dans le panneau gauche.</span><span class="sxs-lookup"><span data-stu-id="f8d19-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="f8d19-313">Cliquez sur <strong>Tout</strong> en haut à droite du volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="f8d19-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="f8d19-314">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="f8d19-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="f8d19-315">Recherchez ensuite votre <strong>compte Azure Cosmos DB</strong>, puis votre <strong>base de données Azure Cosmos DB</strong> et votre <strong>collection Azure Cosmos DB</strong> associés à la collection de sortie spécifiée dans votre tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f8d19-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="f8d19-316">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="f8d19-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="f8d19-317">Vous verrez les résultats de votre tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f8d19-317">You will see the results of your MapReduce job.</span></span>

      ![Résultats de la requête MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="f8d19-319"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8d19-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="f8d19-320">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f8d19-320">Congratulations!</span></span> <span data-ttu-id="f8d19-321">Vous venez d’exécuter vos premiers travaux Hive, Pig et MapReduce à l’aide d’Azure Cosmos DB et HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8d19-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="f8d19-322">Le code source de notre connecteur Hadoop est disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="f8d19-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="f8d19-323">Si vous êtes intéressé, vous pouvez apporter votre contribution sur [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="f8d19-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="f8d19-324">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f8d19-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f8d19-325">[Développement d’une application Java avec DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="f8d19-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="f8d19-326">[Développement de programmes MapReduce en Java pour Hadoop dans HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f8d19-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="f8d19-327">[Prise en main de Hadoop avec Hive dans HDInsight pour analyser l’utilisation des téléphones mobiles][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f8d19-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="f8d19-328">[Utilisation de MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f8d19-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="f8d19-329">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f8d19-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f8d19-330">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f8d19-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f8d19-331">[Personnaliser des clusters HDInsight à l'aide d'une action de script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="f8d19-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
