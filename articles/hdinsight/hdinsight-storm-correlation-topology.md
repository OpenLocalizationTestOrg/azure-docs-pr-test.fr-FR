---
title: "événements aaaCorrelate au fil du temps avec Storm et HBase sur HDInsight"
description: "Découvrez comment toocorrelate les événements qui arrivent à des moments différents, à l’aide de Storm et HBase sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="19a07-103">Corrélation des événements au fil du temps avec Storm et HBase</span><span class="sxs-lookup"><span data-stu-id="19a07-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="19a07-104">En utilisant une banque de données persistante avec Apache Storm, vous pouvez associer les entrées de données qui arrivent à des moments différents.</span><span class="sxs-lookup"><span data-stu-id="19a07-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="19a07-105">Par exemple, lier des événements de connexion et de déconnexion pour un toocalculate de session utilisateur comment durée pendant laquelle les session hello a duré.</span><span class="sxs-lookup"><span data-stu-id="19a07-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="19a07-106">Dans ce document, vous apprendrez comment toocreate une topologie c# tempête de base qui effectue le suivi des événements de connexion et déconnexion des sessions de l’utilisateur et calcule la durée hello de session de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="19a07-107">topologie de Hello utilise HBase comme un magasin de données persistantes.</span><span class="sxs-lookup"><span data-stu-id="19a07-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="19a07-108">HBase vous permet également tooperform les requêtes de traitement par lots sur des informations supplémentaires du tooproduce hello les données d’historique.</span><span class="sxs-lookup"><span data-stu-id="19a07-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="19a07-109">telles que le nombre de sessions utilisateur ayant démarré ou ayant pris fin pendant une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="19a07-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19a07-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="19a07-110">Prerequisites</span></span>

* <span data-ttu-id="19a07-111">Visual Studio et hello HDInsight tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19a07-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="19a07-112">Pour plus d’informations, consultez [prise en main à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="19a07-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="19a07-113">Apache Storm sur un cluster HDInsight (Windows).</span><span class="sxs-lookup"><span data-stu-id="19a07-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="19a07-114">Ne SCP.NET topologies sont pris en charge sur des clusters basés sur Linux une tempête créés après le 28/10/2016, hello HBase SDK pour le package .NET disponible à partir du 28/10/2016 ne fonctionne pas correctement sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="19a07-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="19a07-115">Un cluster Apache HBase sur HDInsight (Linux ou Windows).</span><span class="sxs-lookup"><span data-stu-id="19a07-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="19a07-116">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="19a07-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19a07-117">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="19a07-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="19a07-118">[Java](https://java.com) 1.7 ou version ultérieure sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="19a07-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="19a07-119">Java est utilisé toopackage hello topologie lorsqu’il est soumis toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="19a07-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="19a07-120">Hello **JAVA_HOME** environnement variable doit toohello de point de répertoire qui contient Java.</span><span class="sxs-lookup"><span data-stu-id="19a07-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="19a07-121">Hello **%JAVA_HOME%/bin** répertoire doit être dans le chemin d’accès de hello</span><span class="sxs-lookup"><span data-stu-id="19a07-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="19a07-122">Architecture</span><span class="sxs-lookup"><span data-stu-id="19a07-122">Architecture</span></span>

![Diagramme du flux de données hello via la topologie de hello](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="19a07-124">Corrélation des événements requiert l’un identificateur commun pour la source d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="19a07-125">Par exemple, un ID d’utilisateur, ID de session ou autre élément de données qui est un) unique et (b) inclus dans toutes les données envoyées tooStorm.</span><span class="sxs-lookup"><span data-stu-id="19a07-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="19a07-126">Cet exemple utilise un toorepresent de valeur GUID d’un ID de session.</span><span class="sxs-lookup"><span data-stu-id="19a07-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="19a07-127">Cet exemple se compose de deux clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="19a07-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="19a07-128">HBase : magasin de données persistant pour les données d’historique</span><span class="sxs-lookup"><span data-stu-id="19a07-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="19a07-129">Storm : utilisé tooingest les données entrantes</span><span class="sxs-lookup"><span data-stu-id="19a07-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="19a07-130">les données de salutation sont générées aléatoirement par topologie de Storm hello et comprend hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="19a07-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="19a07-131">Session ID : GUID qui identifie de façon unique chaque session</span><span class="sxs-lookup"><span data-stu-id="19a07-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="19a07-132">Event : événement START ou END</span><span class="sxs-lookup"><span data-stu-id="19a07-132">Event: a START or END event.</span></span> <span data-ttu-id="19a07-133">Pour cet exemple, START se produit toujours avant END</span><span class="sxs-lookup"><span data-stu-id="19a07-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="19a07-134">: Hello heure de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="19a07-135">Ces données sont traitées et stockées dans HBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="19a07-136">Topologie Storm</span><span class="sxs-lookup"><span data-stu-id="19a07-136">Storm topology</span></span>

<span data-ttu-id="19a07-137">Lorsqu’une session démarre, une **Démarrer** événement est reçu par la topologie de hello et connecté tooHBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="19a07-138">Lorsqu’un **fin** événement est reçu, la topologie de hello récupère hello **Démarrer** événement et calcule la durée hello entre hello deux.</span><span class="sxs-lookup"><span data-stu-id="19a07-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="19a07-139">Cela **durée** valeur est ensuite stockée dans HBase avec hello **fin** informations sur les événements.</span><span class="sxs-lookup"><span data-stu-id="19a07-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19a07-140">Alors que cette topologie illustre un modèle de base hello, une solution de production devez tootake conception pourquoi les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="19a07-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="19a07-141">Événements se produisant dans le désordre</span><span class="sxs-lookup"><span data-stu-id="19a07-141">Events arriving out of order</span></span>
> * <span data-ttu-id="19a07-142">Événements en double</span><span class="sxs-lookup"><span data-stu-id="19a07-142">Duplicate events</span></span>
> * <span data-ttu-id="19a07-143">Événements supprimés</span><span class="sxs-lookup"><span data-stu-id="19a07-143">Dropped events</span></span>

<span data-ttu-id="19a07-144">exemple de topologie Hello est composée de hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="19a07-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="19a07-145">Session.cs : simule une session utilisateur en créant un ID de session aléatoire, dure de session hello heure et la durée pendant laquelle démarrer.</span><span class="sxs-lookup"><span data-stu-id="19a07-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="19a07-146">Spout.cs : crée 100 sessions, émet un événement de début, attend un délai aléatoire de hello pour chaque session, puis émet un événement de fin.</span><span class="sxs-lookup"><span data-stu-id="19a07-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="19a07-147">Recycle terminé sessions toogenerate nouveaux.</span><span class="sxs-lookup"><span data-stu-id="19a07-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="19a07-148">HBaseLookupBolt.cs : utilise hello session ID toolook des informations de session dans HBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="19a07-149">Lorsqu’un événement de fin est traité, il recherche les événements de début correspondante hello et calcule la durée hello de session de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="19a07-150">HBaseBolt.cs : stocke les informations dans HBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="19a07-151">TypeHelper.cs : Aide à la conversion de type lors de la lecture / écriture tooHBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="19a07-152">Schéma HBase</span><span class="sxs-lookup"><span data-stu-id="19a07-152">HBase schema</span></span>

<span data-ttu-id="19a07-153">Dans HBase, les données de salutation sont stockées dans une table avec hello suivant/paramètres du schéma :</span><span class="sxs-lookup"><span data-stu-id="19a07-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="19a07-154">Clé de ligne : hello ID de session est utilisé en tant que clé hello pour les lignes de cette table.</span><span class="sxs-lookup"><span data-stu-id="19a07-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="19a07-155">Famille de colonne : nom de famille hello est 'cf'.</span><span class="sxs-lookup"><span data-stu-id="19a07-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="19a07-156">Les colonnes stockées dans cette famille sont :</span><span class="sxs-lookup"><span data-stu-id="19a07-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="19a07-157">event : START ou END.</span><span class="sxs-lookup"><span data-stu-id="19a07-157">event: START or END.</span></span>

  * <span data-ttu-id="19a07-158">Durée : durée hello en millisecondes hello événement s’est produite.</span><span class="sxs-lookup"><span data-stu-id="19a07-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="19a07-159">Durée : hello longueur entre l’événement de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="19a07-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="19a07-160">VERSIONS : famille de 'cf' hello a pour valeur tooretain 5 des versions de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="19a07-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="19a07-161">Les versions sont un journal des valeurs précédentes stockées pour une clé de ligne spécifique.</span><span class="sxs-lookup"><span data-stu-id="19a07-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="19a07-162">Par défaut, HBase retourne uniquement la valeur hello pour la version la plus récente d’une ligne hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="19a07-163">Dans ce cas, hello même ligne est utilisé pour tous les événements (début, fin.) pour que chaque version d’une ligne est identifiée par la valeur d’horodateur hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="19a07-164">Les versions fournissent une vue historique des événements consignés pour un ID spécifique.</span><span class="sxs-lookup"><span data-stu-id="19a07-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="19a07-165">Télécharger le projet de hello</span><span class="sxs-lookup"><span data-stu-id="19a07-165">Download hello project</span></span>

<span data-ttu-id="19a07-166">exemple de projet Hello peut être téléchargé à partir de [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="19a07-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="19a07-167">Ce téléchargement contient hello suivant les projets c# :</span><span class="sxs-lookup"><span data-stu-id="19a07-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="19a07-168">CorrelationTopology : topologie Storm C# qui émet de manière aléatoire des événements start et end pour les sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19a07-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="19a07-169">Chaque session dure entre 1 et 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="19a07-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="19a07-170">SessionInfo : Application console c# qui crée la table HBase à hello et fournit des exemples de requêtes tooreturn d’informations sur les données de session stockée.</span><span class="sxs-lookup"><span data-stu-id="19a07-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="19a07-171">Créer la table de hello</span><span class="sxs-lookup"><span data-stu-id="19a07-171">Create hello table</span></span>

1. <span data-ttu-id="19a07-172">Ouvrez hello **SessionInfo** projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19a07-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="19a07-173">Dans **l’Explorateur de solutions**, avec le bouton hello **SessionInfo** de projet et sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="19a07-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Capture d’écran de menu avec les propriétés sélectionnées](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="19a07-175">Sélectionnez **paramètres**, puis hello de l’ensemble des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="19a07-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="19a07-176">HBaseClusterURL : cluster de HBase tooyour hello URL.</span><span class="sxs-lookup"><span data-stu-id="19a07-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="19a07-177">Par exemple, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="19a07-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="19a07-178">HBaseClusterUserName : compte d’utilisateur admin/HTTP hello pour votre cluster</span><span class="sxs-lookup"><span data-stu-id="19a07-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="19a07-179">HBaseClusterPassword : mot de passe hello pour le compte d’utilisateur admin/HTTP hello</span><span class="sxs-lookup"><span data-stu-id="19a07-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="19a07-180">HBaseTableName : nom de hello de toouse de table hello avec cet exemple</span><span class="sxs-lookup"><span data-stu-id="19a07-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="19a07-181">HBaseTableColumnFamily : nom de famille de colonne hello</span><span class="sxs-lookup"><span data-stu-id="19a07-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Image de la boîte de dialogue Paramètres](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="19a07-183">Exécutez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-183">Run hello solution.</span></span> <span data-ttu-id="19a07-184">Lorsque vous y êtes invité, sélectionnez table de hello toocreate clé hello « c » sur votre cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="19a07-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="19a07-185">Générer et déployer la topologie de Storm hello</span><span class="sxs-lookup"><span data-stu-id="19a07-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="19a07-186">Ouvrez hello **CorrelationTopology** solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19a07-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="19a07-187">Dans **l’Explorateur de solutions**, avec le bouton hello **CorrelationTopology** de projet et sélectionnez Propriétés.</span><span class="sxs-lookup"><span data-stu-id="19a07-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="19a07-188">Dans la fenêtre de propriétés hello, sélectionnez **paramètres** et entrez les valeurs de configuration hello pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="19a07-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="19a07-189">5 premiers Hello sont hello les mêmes valeurs utilisées par hello **SessionInfo** projet :</span><span class="sxs-lookup"><span data-stu-id="19a07-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="19a07-190">HBaseClusterURL : cluster de HBase tooyour hello URL.</span><span class="sxs-lookup"><span data-stu-id="19a07-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="19a07-191">Par exemple, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="19a07-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="19a07-192">HBaseClusterUserName : compte d’utilisateur admin/HTTP hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="19a07-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="19a07-193">HBaseClusterPassword : hello mot de passe de compte d’utilisateur admin/HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="19a07-194">HBaseTableName : nom de hello de toouse de table hello avec cet exemple.</span><span class="sxs-lookup"><span data-stu-id="19a07-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="19a07-195">Cette valeur est hello même nom de la table utilisée dans le projet de SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="19a07-196">HBaseTableColumnFamily : nom de famille colonne hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="19a07-197">Cette valeur est hello même nom de famille de colonne utilisée dans le projet de SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="19a07-198">Ne modifiez pas hello HBaseTableColumnNames, comme valeurs par défaut de la hello sont utilisées par des noms de hello **SessionInfo** tooretrieve données.</span><span class="sxs-lookup"><span data-stu-id="19a07-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="19a07-199">Enregistrer les propriétés de hello, puis générez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="19a07-200">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="19a07-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="19a07-201">Si vous y êtes invité, entrez les informations d’identification de l’hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="19a07-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Image de hello envoyer l’élément de menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="19a07-203">Bonjour **soumettre une topologie** boîte de dialogue, cluster Storm de hello sélectionnez vous que toodeploy cette topologie.</span><span class="sxs-lookup"><span data-stu-id="19a07-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19a07-204">Hello première fois que vous envoyez une topologie, il peut prendre quelques secondes nom de hello tooretrieve vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19a07-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="19a07-205">Une fois que la topologie de hello, a été téléchargé et soumis toohello cluster hello **affichage de la topologie Storm** s’ouvre et affiche hello topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="19a07-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="19a07-206">les données de salutation toorefresh, sélectionnez hello **CorrelationTopology** et utiliser le bouton d’actualisation hello en hello haut à droite de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Image de l’affichage de la topologie hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="19a07-208">Lors de la topologie de hello commence à générer des données, hello valeur Bonjour **EMISE** par incréments de colonne.</span><span class="sxs-lookup"><span data-stu-id="19a07-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19a07-209">Si hello **affichage de la topologie Storm** ne pas ouvrir automatiquement, utilisez hello suivant les étapes tooopen il :</span><span class="sxs-lookup"><span data-stu-id="19a07-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="19a07-210">Dans l’**Explorateur de solutions**, développez **Azure**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="19a07-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="19a07-211">Cluster avec le bouton hello Storm hello topologie est en cours d’exécution, puis sélectionnez **vue Storm Topologies**</span><span class="sxs-lookup"><span data-stu-id="19a07-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="19a07-212">Interroger des données hello</span><span class="sxs-lookup"><span data-stu-id="19a07-212">Query hello data</span></span>

<span data-ttu-id="19a07-213">Une fois que les données a été émises, utilisez hello étapes tooquery hello données suivantes.</span><span class="sxs-lookup"><span data-stu-id="19a07-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="19a07-214">Retourner toohello **SessionInfo** projet.</span><span class="sxs-lookup"><span data-stu-id="19a07-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="19a07-215">S’il n’est pas en cours d’exécution, démarrez une nouvelle instance du projet.</span><span class="sxs-lookup"><span data-stu-id="19a07-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="19a07-216">Lorsque vous y êtes invité, sélectionnez **s** toosearch pour l’événement de début.</span><span class="sxs-lookup"><span data-stu-id="19a07-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="19a07-217">Vous sont demandée tooenter de début et de fin de temps toodefine une plage de temps - seuls les événements entre ces deux heures sont retournés.</span><span class="sxs-lookup"><span data-stu-id="19a07-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="19a07-218">Suivant de hello utilisez mettre en forme lors de l’entrée de démarrage de hello et heure de fin : hh : mm et « am » ou « pm ».</span><span class="sxs-lookup"><span data-stu-id="19a07-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="19a07-219">Par exemple, 11:20.</span><span class="sxs-lookup"><span data-stu-id="19a07-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="19a07-220">tooreturn connecté, événements, utilisez une heure de début avant hello Storm topologie a été déployée à partir d’et une heure de fin de maintenant.</span><span class="sxs-lookup"><span data-stu-id="19a07-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="19a07-221">les données de retour Hello contient toohello similaire d’entrées après le texte :</span><span class="sxs-lookup"><span data-stu-id="19a07-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="19a07-222">Recherche de hello de fin événements fonctionne même en tant qu’événements de début.</span><span class="sxs-lookup"><span data-stu-id="19a07-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="19a07-223">Toutefois, les événements de fin sont générés au hasard entre 1 et 5 minutes après l’événement de début hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="19a07-224">Vous avez peut-être tootry quelques événements de fin de hello de toofind de plages de temps.</span><span class="sxs-lookup"><span data-stu-id="19a07-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="19a07-225">Événements de fin contiennent également durée hello de session hello - différence hello entre l’heure de l’événement START hello et événements de fin.</span><span class="sxs-lookup"><span data-stu-id="19a07-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="19a07-226">Voici un exemple de données pour les événements END :</span><span class="sxs-lookup"><span data-stu-id="19a07-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="19a07-227">Alors que les valeurs de durée hello que vous entrez sont en heure locale, temps hello renvoyés par la requête de hello est au format UTC.</span><span class="sxs-lookup"><span data-stu-id="19a07-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="19a07-228">Arrêter la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="19a07-228">Stop hello topology</span></span>

<span data-ttu-id="19a07-229">Lorsque vous êtes topologie de hello toostop prêt, retourner toohello **CorrelationTopology** projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19a07-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="19a07-230">Bonjour **affichage de la topologie Storm**, sélectionnez la topologie de hello et l’utiliser hello **Kill** bouton en haut de hello d’affichage de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="19a07-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="19a07-231">Supprimer votre cluster</span><span class="sxs-lookup"><span data-stu-id="19a07-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="19a07-232">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19a07-232">Next steps</span></span>

<span data-ttu-id="19a07-233">Pour plus d’exemples Storm, consultez la page [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="19a07-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
