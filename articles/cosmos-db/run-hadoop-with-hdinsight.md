---
title: "aaaRun un Hadoop de la tâche à l’aide de la base de données Azure Cosmos et HDInsight | Documents Microsoft"
description: "Découvrez comment toorun un simple Hive, Pig et MapReduce de la tâche avec la base de données Azure Cosmos et Azure HDInsight."
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="4b9a7-103"><a name="Azure Cosmos DB-HDInsight"></a>Exécuter un travail Apache Hive, Pig ou Hadoop avec Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b9a7-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="4b9a7-104">Ce didacticiel vous montre comment toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], et [Apache Hadoop] [ apache-hadoop] Travaux MapReduce sur Azure HDInsight avec connecteur Hadoop de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="4b9a7-105">Connecteur de Hadoop COSMOS DB permet tooact Cosmos DB comme une source et le récepteur de tâches Hive, Pig et MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="4b9a7-106">Ce didacticiel utilise Cosmos DB en tant que source de données hello et de destination pour les travaux Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="4b9a7-107">À l’issue de ce didacticiel, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="4b9a7-108">Comment charger des données à partir de Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="4b9a7-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="4b9a7-109">Comment stocker des données dans Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="4b9a7-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="4b9a7-110">Nous vous recommandons de mise en route en regardant hello suivant vidéo, où nous exécuter un travail Hive à l’aide de la base de données Cosmos et HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="4b9a7-111">Revenez ensuite toothis article, où vous recevrez hello plus de détails sur l’exécution de travaux de l’analytique sur vos données de la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="4b9a7-112">Ce didacticiel part du principe que vous avez déjà utilisé Apache Hadoop, Hive et/ou Pig.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="4b9a7-113">Si vous êtes de nouveau tooApache Hadoop, Hive et Pig, nous vous recommandons de consulter hello [Apache Hadoop documentation][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="4b9a7-114">Ce didacticiel suppose également que vous avez déjà utilisé Cosmos DB et que vous possédez un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="4b9a7-115">Si vous êtes tooCosmos nouvelle base de données ou vous n’avez pas un compte de base de données Cosmos, consultez notre [mise en route] [ getting-started] page.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="4b9a7-116">N’avez pas temps toocomplete hello didacticiel et souhaitez uniquement tooget hello complète exemples PowerShell de scripts Hive, Pig et MapReduce ?</span><span class="sxs-lookup"><span data-stu-id="4b9a7-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="4b9a7-117">Ce n’est pas un problème. Vous pouvez les obtenir [ici][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="4b9a7-118">téléchargement de Hello contient également les fichiers de hql, pig et java hello pour ces exemples.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="4b9a7-119"><a name="NewestVersion"></a>Version la plus récente</span><span class="sxs-lookup"><span data-stu-id="4b9a7-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="4b9a7-120">Version du connecteur Hadoop</span><span class="sxs-lookup"><span data-stu-id="4b9a7-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="4b9a7-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="4b9a7-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="4b9a7-122">URI du script</span><span class="sxs-lookup"><span data-stu-id="4b9a7-122">Script Uri</span></span></th>
        <td><span data-ttu-id="4b9a7-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="4b9a7-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="4b9a7-124">Date de modification</span><span class="sxs-lookup"><span data-stu-id="4b9a7-124">Date Modified</span></span></th>
        <td><span data-ttu-id="4b9a7-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="4b9a7-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="4b9a7-126">Versions de HDInsight prises en charge</span><span class="sxs-lookup"><span data-stu-id="4b9a7-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="4b9a7-127">3.1, 3.2.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="4b9a7-128">Journal des modifications</span><span class="sxs-lookup"><span data-stu-id="4b9a7-128">Change Log</span></span></th>
        <td><span data-ttu-id="4b9a7-129">Mise à jour too1.6.0 de kit de développement Java Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4b9a7-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="4b9a7-130">Prise en charge ajoutée pour les collections partitionnées en tant que source et récepteur</span><span class="sxs-lookup"><span data-stu-id="4b9a7-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="4b9a7-131"><a name="Prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="4b9a7-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="4b9a7-132">Avant de suivre les instructions de hello dans ce didacticiel, assurez-vous que vous disposez des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="4b9a7-133">Un compte Cosmos DB, une base de données et une collection de documents.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="4b9a7-134">Pour plus d’informations, consultez la page [Getting Started with Cosmos DB (Prise en main de Cosmos DB)][getting-started].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="4b9a7-135">Importer des exemples de données dans votre compte de base de données Cosmos avec hello [outil d’importation de base de données Cosmos][import-data].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="4b9a7-136">Débit.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-136">Throughput.</span></span> <span data-ttu-id="4b9a7-137">Les lectures et écritures à partir de HDInsight seront comptabilisées sur vos unités de demande allouées pour vos collections.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="4b9a7-138">Capacité pour une procédure stockée supplémentaire dans chaque collection de sortie.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="4b9a7-139">les procédures stockée de Hello sont utilisées pour le transfert de documents qui en résultent.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="4b9a7-140">Capacité d’un document qui en résulte hello hello Hive, Pig, MapReduce travaux ou.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="4b9a7-141">[*Facultatif*] Capacité pour une collection supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="4b9a7-142">Dans l’ordre tooavoid hello la création d’une nouvelle collection au cours des travaux de hello, vous pouvez imprimer hello résultats toostdout, enregistrez le conteneur de hello sortie tooyour WASB ou spécifiez un regroupement existant déjà.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="4b9a7-143">Dans les cas de hello de spécification d’une collection existante, des documents seront créées à l’intérieur de la collection de hello et des documents déjà existants ne seront supprimés s’il existe un conflit dans *ID*.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="4b9a7-144">**connecteur de Hello remplace automatiquement les documents existants avec des conflits d’id**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="4b9a7-145">Vous pouvez désactiver cette fonctionnalité en définissant hello upsert option toofalse.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="4b9a7-146">Si upsert a la valeur false et si un conflit se produit, la tâche Hadoop de hello échoue ; une erreur de conflit d’id de rapport.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="4b9a7-147"><a name="ProvisionHDInsight"></a>Étape 1 : créer un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b9a7-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="4b9a7-148">Ce didacticiel utilise Action de Script à partir de toocustomize du portail Azure hello votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="4b9a7-149">Dans ce didacticiel, nous utiliserons toocreate du portail Azure hello votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="4b9a7-150">Pour obtenir des instructions sur la façon dont les applets de commande PowerShell toouse ou hello HDInsight .NET SDK, extraire les [HDInsight de personnaliser des clusters à l’aide de Script Action] [ hdinsight-custom-provision] l’article.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="4b9a7-151">Connectez-vous à toohello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="4b9a7-152">Cliquez sur **+ nouveau** sur haut hello Hello barre de navigation gauche, recherchez **HDInsight** dans la barre de recherche supérieure hello sur le nouveau panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="4b9a7-153">**HDInsight** publié par **Microsoft** s’affiche en haut de hello des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="4b9a7-154">Cliquez dessus, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="4b9a7-155">Sur le nouveau HDInsight Cluster de hello créer panneau, entrez votre **nom de Cluster** et sélectionnez hello **abonnement** vous souhaitez tooprovision cette ressource sous.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="4b9a7-156">Nom du cluster</span><span class="sxs-lookup"><span data-stu-id="4b9a7-156">Cluster name</span></span></td><td><span data-ttu-id="4b9a7-157">Cluster de nom hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="4b9a7-158">Le nom DNS doit commencer et finir par un caractère alphanumérique et peut contenir des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="4b9a7-159">champ de Hello doit être une chaîne comprise entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="4b9a7-160">Nom d'abonnement</span><span class="sxs-lookup"><span data-stu-id="4b9a7-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="4b9a7-161">Si vous avez plusieurs abonnements Azure, sélectionnez l’abonnement hello qui hébergera votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="4b9a7-162">
5.Cliquez sur **sélectionner le Type de Cluster** et hello ensemble suivant de propriétés toohello des valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="4b9a7-163">Type de cluster</span><span class="sxs-lookup"><span data-stu-id="4b9a7-163">Cluster type</span></span></td><td><span data-ttu-id="4b9a7-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="4b9a7-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="4b9a7-165">Niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="4b9a7-165">Cluster tier</span></span></td><td><span data-ttu-id="4b9a7-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="4b9a7-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="4b9a7-167">Système d'exploitation</span><span class="sxs-lookup"><span data-stu-id="4b9a7-167">Operating System</span></span></td><td><span data-ttu-id="4b9a7-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="4b9a7-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="4b9a7-169">Version</span><span class="sxs-lookup"><span data-stu-id="4b9a7-169">Version</span></span></td><td><span data-ttu-id="4b9a7-170">version la plus récente</span><span class="sxs-lookup"><span data-stu-id="4b9a7-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="4b9a7-171">Maintenant, cliquez sur **SÉLECTIONNER**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-171">Now, click **SELECT**.</span></span>

    ![Fournir des détails du cluster initial Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="4b9a7-173">Cliquez sur **informations d’identification** tooset votre connexion et les informations d’identification de l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="4b9a7-174">Choisissez le **nom de connexion au cluster** et le **mot de passe de connexion au cluster**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="4b9a7-175">Si vous souhaitez tooremote dans votre cluster, sélectionnez *Oui* bas hello du Panneau de hello et fournir un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="4b9a7-176">Cliquez sur **Source de données** tooset accéder à votre emplacement principal pour les données.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="4b9a7-177">Choisissez hello **méthode de sélection** et spécifiez un compte de stockage déjà existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="4b9a7-178">On hello même panneau, spécifiez un **conteneur par défaut** et un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="4b9a7-179">Et cliquez sur **SÉLECTIONNER**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-180">Sélectionnez une région du compte de base de données Cosmos pour de meilleures performances de tooyour fermer emplacement</span><span class="sxs-lookup"><span data-stu-id="4b9a7-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="4b9a7-181">Cliquez sur **tarification** tooselect hello nombre et le type de nœuds.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="4b9a7-182">Vous pouvez conserver configuration par défaut de hello et nombre de hello mise à l’échelle de nœuds Worker ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="4b9a7-183">Cliquez sur **Configuration facultative**, puis **Actions de Script** Bonjour facultatif Panneau de Configuration.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="4b9a7-184">Dans Actions de Script, entrez hello suivant informations toocustomize votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="4b9a7-185">Propriété</span><span class="sxs-lookup"><span data-stu-id="4b9a7-185">Property</span></span></th><th><span data-ttu-id="4b9a7-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="4b9a7-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="4b9a7-187">Nom</span><span class="sxs-lookup"><span data-stu-id="4b9a7-187">Name</span></span></td>
             <td><span data-ttu-id="4b9a7-188">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="4b9a7-189">URI du script</span><span class="sxs-lookup"><span data-stu-id="4b9a7-189">Script URI</span></span></td>
             <td><span data-ttu-id="4b9a7-190">Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="4b9a7-191">Entrez :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-191">Please enter:</span></span> </br> <span data-ttu-id="4b9a7-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="4b9a7-193">Nœud principal</span><span class="sxs-lookup"><span data-stu-id="4b9a7-193">Head</span></span></td>
             <td><span data-ttu-id="4b9a7-194">Cliquez sur toorun de case à cocher Bonjour Bonjour script PowerShell sur le nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="4b9a7-195">
             <strong>Activez cette case à cocher</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="4b9a7-196">Worker</span><span class="sxs-lookup"><span data-stu-id="4b9a7-196">Worker</span></span></td>
             <td><span data-ttu-id="4b9a7-197">Cliquez sur hello case à cocher toorun hello PowerShell script sur le nœud de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="4b9a7-198">
             <strong>Activez cette case à cocher</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="4b9a7-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="4b9a7-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="4b9a7-200">Cliquez sur le script hello case à cocher toorun hello PowerShell sur hello soigneur.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="4b9a7-201">
             <strong>Inutile</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="4b9a7-202">Paramètres</span><span class="sxs-lookup"><span data-stu-id="4b9a7-202">Parameters</span></span></td>
             <td><span data-ttu-id="4b9a7-203">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="4b9a7-204">
             <strong>Aucun paramètre requis</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="4b9a7-205">
11. Créez un **Groupe de ressources** ou utilisez un groupe de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="4b9a7-206">12.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-206">12.</span></span> <span data-ttu-id="4b9a7-207">Examinez à présent **code confidentiel toodashboard** tootrack son déploiement et un clic **créer**!</span><span class="sxs-lookup"><span data-stu-id="4b9a7-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="4b9a7-208"><a name="InstallCmdlets"></a>Étape 2 : installer et configurer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b9a7-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="4b9a7-209">Installez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-209">Install Azure PowerShell.</span></span> <span data-ttu-id="4b9a7-210">Vous trouverez des instructions [ici][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-211">Pour les requêtes Hive, vous pouvez également utiliser l'éditeur Hive en ligne de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="4b9a7-212">toodo, inscrivez-vous dans toohello [Azure Portal][azure-portal], cliquez sur **HDInsight** tooview de volet de gauche hello sur une liste de vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="4b9a7-213">Cliquez sur le cluster hello vous souhaitez que les requêtes Hive toorun sur, puis cliquez sur **Console de requête**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="4b9a7-214">Ouvrez hello environnement d’écriture de scripts intégré Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="4b9a7-215">Sur un ordinateur exécutant Windows 8 ou Windows Server 2012 ou version ultérieure, vous pouvez utiliser intégrées de hello recherche.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="4b9a7-216">À partir de l’écran d’accueil hello, tapez **powershell ise** et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="4b9a7-217">Sur un ordinateur exécutant une version antérieure à Windows 8 ou Windows Server 2012, utilisez le menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="4b9a7-218">À partir du menu Démarrer de hello, tapez **invite de commandes** dans la zone de recherche hello, puis, dans la liste hello des résultats, cliquez sur **invite de commandes**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="4b9a7-219">Bonjour invite de commandes, tapez **powershell_ise** et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="4b9a7-220">Ajoutez votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="4b9a7-221">Dans le volet de la Console de hello, tapez **Add-AzureAccount** et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="4b9a7-222">Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="4b9a7-223">Tapez un mot de passe hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="4b9a7-224">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="4b9a7-225">Hello suivant schéma identifie les parties importantes de hello de votre environnement de script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagramme d’Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="4b9a7-227"><a name="RunHive"></a>Étape 3 : exécuter un travail Hive à l’aide de Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b9a7-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4b9a7-228">Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="4b9a7-229">Hello ensemble suivant de variables dans votre volet de PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="4b9a7-230">Commençons à construire votre chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="4b9a7-231">Nous allons écrire une requête Hive qui Récupère tous les documents générés par le système horodateurs (DTS) et des identificateurs uniques (_rid) à partir d’une collection de base de données Azure Cosmos, comptabilise tous les documents par minute de hello et stocke ensuite les résultats de hello dans une nouvelle collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="4b9a7-232">Commençons par créer une table Hive à partir de notre collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="4b9a7-233">Ajouter hello suivant extrait de code toohello volet de PowerShell Script <strong>après</strong> extrait de code hello de #1.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="4b9a7-234">Veillez à qu'inclure hello facultatif DocumentDB.query paramètre t trim nos documents toojust _ts et le _rid.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-235">**L’attribution du nom DocumentDB.inputCollections n’était pas une erreur.**</span><span class="sxs-lookup"><span data-stu-id="4b9a7-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="4b9a7-236">Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="4b9a7-237">Ensuite, nous allons créer une table Hive pour la collection de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="4b9a7-238">propriétés de document de sortie Hello sera hello mois, jour, heure, minute et nombre total de hello d’occurrences.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-239">**Une fois encore, l’attribution du nom DocumentDB.outputCollections n’était pas une erreur.**</span><span class="sxs-lookup"><span data-stu-id="4b9a7-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="4b9a7-240">Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="4b9a7-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="4b9a7-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="4b9a7-242">noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="4b9a7-243">Les documents seront distribués en tourniquet (round robin), sur plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="4b9a7-244">Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="4b9a7-245">Enfin, nous allons tally hello des documents par mois, jour, heure et minute et insérer les résultats de hello en hello sortie table Hive.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="4b9a7-246">Ajoutez hello suivant extrait de code de script toocreate une définition de tâche Hive à partir de la requête précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="4b9a7-247">Vous pouvez également utiliser hello - fichier basculer toospecify un fichier de script HiveQL sur HDFS.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="4b9a7-248">Ajouter hello suivant l’heure de début d’extrait de code toosave hello et envoi de la tâche de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="4b9a7-249">Ajoutez hello suivant toowait pour hello ruche travail toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="4b9a7-250">Ajouter hello suivant tooprint hello standard sortie et hello démarrez heures et de fin.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="4b9a7-251">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="4b9a7-251">**Run** your new script!</span></span> <span data-ttu-id="4b9a7-252">**Cliquez sur** vert de hello bouton d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="4b9a7-253">Vérifier les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-253">Check hello results.</span></span> <span data-ttu-id="4b9a7-254">L’authentification à hello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="4b9a7-255">Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="4b9a7-256">Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="4b9a7-257">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="4b9a7-258">Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre requête Hive.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="4b9a7-259">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="4b9a7-260">Vous verrez des résultats de votre requête Hive hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-260">You will see hello results of your Hive query.</span></span>

   ![Résultats de la requête Hive][image-hive-query-results]

## <span data-ttu-id="4b9a7-262"><a name="RunPig"></a>Étape 4 : exécuter un travail Pig à l’aide de Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b9a7-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4b9a7-263">Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="4b9a7-264">Hello ensemble suivant de variables dans votre volet de PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="4b9a7-265">Commençons à construire votre chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="4b9a7-266">Nous allons écrire une requête Pig qui Récupère tous les documents générés par le système horodateurs (DTS) et des identificateurs uniques (_rid) à partir d’une collection de base de données Azure Cosmos, comptabilise tous les documents par minute de hello et stocke ensuite les résultats de hello dans une nouvelle collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="4b9a7-267">Chargez d’abord des documents Cosmos DB dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="4b9a7-268">Ajouter hello suivant extrait de code toohello volet de PowerShell Script <strong>après</strong> extrait de code hello de #1.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="4b9a7-269">Assurez-vous que tooadd un DocumentDB requête tootrim DocumentDB facultatif du paramètre de requête toohello nos documents toojust _ts et le _rid.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-270">Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="4b9a7-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="4b9a7-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="4b9a7-272">noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="4b9a7-273">Les documents seront distribués en tourniquet (round robin), sur plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="4b9a7-274">Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="4b9a7-275">Ensuite, nous allons calculer les documents hello en hello mois, jour, heure, minute et nombre total de hello d’occurrences.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="4b9a7-276">Enfin, nous allons stocker les résultats de hello dans notre nouvelle collection de sortie.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b9a7-277">Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="4b9a7-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="4b9a7-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="4b9a7-279">noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="4b9a7-280">Documents va être distribué de tourniquet (Round Robin) entre hello plusieurs collections.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="4b9a7-281">Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="4b9a7-282">Ajoutez hello suivant extrait de code de script toocreate une définition de tâche Pig à partir de la requête précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="4b9a7-283">Vous pouvez également utiliser hello - fichier basculer toospecify un fichier de script Pig sur HDFS.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="4b9a7-284">Ajouter hello suivant l’heure de début d’extrait de code toosave hello et envoi de la tâche de Pig hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="4b9a7-285">Ajoutez hello suivant toowait pour toocomplete de travail Pig hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="4b9a7-286">Ajouter hello suivant tooprint hello standard sortie et hello démarrez heures et de fin.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="4b9a7-287">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="4b9a7-287">**Run** your new script!</span></span> <span data-ttu-id="4b9a7-288">**Cliquez sur** vert de hello bouton d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="4b9a7-289">Vérifier les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-289">Check hello results.</span></span> <span data-ttu-id="4b9a7-290">L’authentification à hello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="4b9a7-291">Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="4b9a7-292">Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="4b9a7-293">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="4b9a7-294">Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre requête Pig.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="4b9a7-295">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="4b9a7-296">Vous verrez des résultats de votre requête Pig hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-296">You will see hello results of your Pig query.</span></span>

    ![Résultats de la requête Pig][image-pig-query-results]

## <span data-ttu-id="4b9a7-298"><a name="RunMapReduce"></a>Étape 5 : exécuter une tâche MapReduce à l’aide d’Azure Cosmos DB et HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b9a7-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="4b9a7-299">Hello ensemble suivant de variables dans votre volet de PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="4b9a7-300">Nous allons exécuter une tâche MapReduce qui comptabilise le nombre de hello d’occurrences de chaque propriété de Document à partir de votre collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="4b9a7-301">Ajoutez cet extrait de script **après** extrait de code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="4b9a7-302">TallyProperties-v01.jar est fourni avec une installation personnalisée de hello Cosmos DB Hadoop connecteur hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="4b9a7-303">Ajoutez hello suivant la tâche de commande toosubmit hello MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="4b9a7-304">En outre toohello définition de la tâche MapReduce, vous fournissez également nom du cluster HDInsight hello où vous souhaitez tâche MapReduce de hello toorun et les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="4b9a7-305">Hello Start-AzureHDInsightJob est un appel asynchrone.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="4b9a7-306">toocheck hello hello travail achevé, utilisez hello *Wait-AzureHDInsightJob* applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="4b9a7-307">Ajoutez hello suivant de commande toocheck des erreurs avec la tâche de MapReduce hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="4b9a7-308">**Exécutez** votre nouveau script !</span><span class="sxs-lookup"><span data-stu-id="4b9a7-308">**Run** your new script!</span></span> <span data-ttu-id="4b9a7-309">**Cliquez sur** vert de hello bouton d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="4b9a7-310">Vérifier les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-310">Check hello results.</span></span> <span data-ttu-id="4b9a7-311">L’authentification à hello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="4b9a7-312">Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="4b9a7-313">Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="4b9a7-314">Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="4b9a7-315">Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre tâche MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="4b9a7-316">Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="4b9a7-317">Vous verrez des résultats de votre tâche MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-317">You will see hello results of your MapReduce job.</span></span>

      ![Résultats de la requête MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="4b9a7-319"><a name="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b9a7-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="4b9a7-320">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="4b9a7-320">Congratulations!</span></span> <span data-ttu-id="4b9a7-321">Vous venez d’exécuter vos premiers travaux Hive, Pig et MapReduce à l’aide d’Azure Cosmos DB et HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="4b9a7-322">Le code source de notre connecteur Hadoop est disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="4b9a7-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="4b9a7-323">Si vous êtes intéressé, vous pouvez apporter votre contribution sur [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="4b9a7-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="4b9a7-324">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="4b9a7-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="4b9a7-325">[Développement d’une application Java avec DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="4b9a7-326">[Développement de programmes MapReduce en Java pour Hadoop dans HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="4b9a7-327">[Prise en main Hadoop avec ruche en cours d’utilisation de HDInsight tooanalyze combiné mobile][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="4b9a7-328">[Utilisation de MapReduce avec HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="4b9a7-329">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4b9a7-330">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4b9a7-331">[Personnaliser des clusters HDInsight à l'aide d'une action de script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="4b9a7-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
