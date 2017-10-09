---
title: "aaaDeploy et gérer les topologies d’Apache Storm sur HDInsight | Documents Microsoft"
description: "Découvrez comment toodeploy, surveiller et gérer des topologies de Apache Storm à l’aide de hello du tableau de bord Storm sur HDInsight. Utilisez les outils Hadoop pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="2339a-104">Déploiement et gestion des topologies Apache Storm sur HDInsight Windows</span><span class="sxs-lookup"><span data-stu-id="2339a-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="2339a-105">Hello Storm le tableau de bord vous permet de tooeasily déployer et exécuter le cluster HDInsight de Apache Storm topologies tooyour à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="2339a-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="2339a-106">Vous pouvez également utiliser toomonitor du tableau de bord hello et gérer des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2339a-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="2339a-107">Si vous utilisez Visual Studio, outils de HDInsight hello pour Visual Studio fournit des fonctionnalités similaires dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2339a-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="2339a-108">Hello Storm le tableau de bord et les fonctionnalités de tempête de hello Bonjour outils HDInsight s’appuient sur hello Storm REST API, qui peut être utilisé toocreate vos propres solutions de surveillance et de gestion.</span><span class="sxs-lookup"><span data-stu-id="2339a-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2339a-109">étapes de Hello dans ce document nécessitent une tempête sur le cluster HDInsight qui utilise Windows comme système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="2339a-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="2339a-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2339a-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2339a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="2339a-112">Pour plus d’informations sur le déploiement et la gestion des topologies avec un cluster HDInsight utilisant Linux, consultez [Déploiement et gestion des topologies Apache Storm sur HDInsight Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2339a-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2339a-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2339a-113">Prerequisites</span></span>

* <span data-ttu-id="2339a-114">**Apache Storm sur HDInsight** : pour connaître les étapes de création d’un cluster, voir [Prise en main d’Apache Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2339a-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="2339a-115">Pourquoi **tableau de bord Storm**: un navigateur web moderne qui prend en charge de HTML5.</span><span class="sxs-lookup"><span data-stu-id="2339a-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="2339a-116">Pour **Visual Studio** -Windows Azure SDK 2.5.1 ou plus récent et hello outils HDInsight pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2339a-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="2339a-117">Consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall et configurer les outils de hello HDInsight pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2339a-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="2339a-118">Une des hello versions de Visual Studio suivantes :</span><span class="sxs-lookup"><span data-stu-id="2339a-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="2339a-119">Visual Studio 2012 avec Update 4</span><span class="sxs-lookup"><span data-stu-id="2339a-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="2339a-120">Visual Studio 2013 avec Update 4 ou Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="2339a-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="2339a-121">Visual Studio 2015 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="2339a-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="2339a-122">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="2339a-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="2339a-123">Tableau de bord Storm</span><span class="sxs-lookup"><span data-stu-id="2339a-123">Storm Dashboard</span></span>

<span data-ttu-id="2339a-124">Hello Storm le tableau de bord est une page web disponible sur votre cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="2339a-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="2339a-125">URL de Hello est **https://&lt;nom_cluster >.azurehdinsight.net/**, où **clustername** hello désigne votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2339a-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="2339a-126">À partir du haut hello Hello Storm le tableau de bord, sélectionnez **soumettre une topologie**.</span><span class="sxs-lookup"><span data-stu-id="2339a-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="2339a-127">Suivez les instructions hello sur hello page toorun un exemple de topologie ou tooupload et exécuter une topologie que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="2339a-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Hello envoyer la page de la topologie][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="2339a-129">Interface utilisateur de Storm</span><span class="sxs-lookup"><span data-stu-id="2339a-129">Storm UI</span></span>

<span data-ttu-id="2339a-130">À partir de hello Storm le tableau de bord, sélectionnez hello **Storm UI** lien.</span><span class="sxs-lookup"><span data-stu-id="2339a-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="2339a-131">Cela affiche des informations sur le cluster de hello, dans tooany Ajout en cours d’exécution topologies.</span><span class="sxs-lookup"><span data-stu-id="2339a-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![interface utilisateur de Hello storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="2339a-133">Avec certaines versions d’Internet Explorer, vous pouvez constater que hello que Storm UI n’actualise pas une fois que vous avez visités tout d’abord qu’il.</span><span class="sxs-lookup"><span data-stu-id="2339a-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="2339a-134">Par exemple, il peut ne pas affiche les topologies de nouveau hello vous avez envoyé, ou il peut afficher une topologie comme active lorsque vous l’avez désactivée précédemment.</span><span class="sxs-lookup"><span data-stu-id="2339a-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="2339a-135">Microsoft est conscient de ce problème et recherche actuellement une solution.</span><span class="sxs-lookup"><span data-stu-id="2339a-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="2339a-136">Page principale</span><span class="sxs-lookup"><span data-stu-id="2339a-136">Main page</span></span>

<span data-ttu-id="2339a-137">page principale de Hello Hello Storm UI fournit hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2339a-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="2339a-138">**Résumé du cluster**: informations de base sur le cluster de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="2339a-139">**Résumé de la topologie**: une liste des topologies en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2339a-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="2339a-140">Utilisez les liens hello tooview de cette section plus d’informations sur les topologies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2339a-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="2339a-141">**Résumé de superviseur**: plus d’informations sur le superviseur de Storm hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="2339a-142">**Configuration de Nimbus**: configuration Nimbus pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="2339a-143">Résumé de la topologie</span><span class="sxs-lookup"><span data-stu-id="2339a-143">Topology summary</span></span>

<span data-ttu-id="2339a-144">Sélection d’un lien à partir de hello **récapitulatif de la topologie** section affiche hello informations sur la topologie de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2339a-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="2339a-145">**Résumé de la topologie**: informations de base sur la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="2339a-146">**Actions de topologie**: actions de gestion que vous pouvez effectuer pour la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="2339a-147">**Activer**: reprend le traitement d’une topologie arrêtée.</span><span class="sxs-lookup"><span data-stu-id="2339a-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="2339a-148">**Désactiver**: suspend une topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2339a-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="2339a-149">**Rééquilibrer**: ajuste le parallélisme hello de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="2339a-150">Vous devez rééquilibrer les topologies en cours d’exécution une fois que vous avez modifié le nombre de hello de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="2339a-151">Cela permet hello topologie tooadjust parallélisme toocompensate pour hello augmenté ou diminué le nombre de nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="2339a-152">Pour plus d’informations, consultez [présentation parallélisme hello d’une topologie de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="2339a-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="2339a-153">**KILL**: met fin à une topologie Storm après hello spécifié le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="2339a-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="2339a-154">**Statistiques de topologie**: statistiques sur la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="2339a-155">Utilisez les liens hello hello **fenêtre** colonne tooset hello période hello écritures de page de hello restantes.</span><span class="sxs-lookup"><span data-stu-id="2339a-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="2339a-156">**Becs verseurs amovibles**: hello becs verseurs utilisés par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="2339a-157">Utilisez les liens hello tooview de cette section plus d’informations sur becs verseurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2339a-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="2339a-158">**Boulons**: hello boulons utilisés par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="2339a-159">Utilisez les liens hello tooview de cette section plus d’informations sur les boulons spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2339a-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="2339a-160">**Configuration de la topologie**: configuration hello de topologie de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2339a-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="2339a-161">Résumé relatif aux spouts et aux bolts</span><span class="sxs-lookup"><span data-stu-id="2339a-161">Spout and Bolt summary</span></span>

<span data-ttu-id="2339a-162">En sélectionnant un bec de hello **becs verseurs amovibles** ou **boulons** sections affiche hello suit les informations d’élément de hello sélectionné :</span><span class="sxs-lookup"><span data-stu-id="2339a-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="2339a-163">**Résumé des composants**: informations de base sur bec de hello ou éclair.</span><span class="sxs-lookup"><span data-stu-id="2339a-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="2339a-164">**BEC/éclair statistiques**: statistiques sur hello bec ou boulon.</span><span class="sxs-lookup"><span data-stu-id="2339a-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="2339a-165">Utilisez les liens hello hello **fenêtre** colonne tooset hello période hello écritures de page de hello restantes.</span><span class="sxs-lookup"><span data-stu-id="2339a-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="2339a-166">**D’entrée statistiques** (boulon uniquement) : flux consommées par un éclair de hello d’entrée le plus d’informations sur hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="2339a-167">**Statistiques de sortie**: plus d’informations sur les flux hello émis par ce bec ou boulon.</span><span class="sxs-lookup"><span data-stu-id="2339a-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="2339a-168">**Les exécuteurs**: informations sur les instances de hello de bec de hello ou éclair.</span><span class="sxs-lookup"><span data-stu-id="2339a-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="2339a-169">Sélectionnez hello **Port** entrée pour un tooview spécifique de l’exécuteur un journal d’informations de diagnostic généré pour cette instance.</span><span class="sxs-lookup"><span data-stu-id="2339a-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="2339a-170">**Erreurs**: les informations d’erreur pour ce spout ou ce bolt.</span><span class="sxs-lookup"><span data-stu-id="2339a-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="2339a-171">Outils HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2339a-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="2339a-172">Hello HDInsight outils peut être utilisé toosubmit c# ou hybride topologies tooyour cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="2339a-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="2339a-173">Hello suit utilisent un exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="2339a-173">hello following steps use a sample application.</span></span> <span data-ttu-id="2339a-174">Pour plus d’informations sur la création de vos propres topologies à l’aide des outils de HDInsight hello, consultez [C# développer des topologies à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2339a-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="2339a-175">Utilisez hello suivant les étapes toodeploy un tooyour exemple tempête de cluster HDInsight, puis afficher et gérer la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="2339a-176">Si vous n’avez pas déjà installé hello dernière version de hello outils HDInsight pour Visual Studio, consultez [prise en main à l’aide des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2339a-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="2339a-177">Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="2339a-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="2339a-178">Bonjour **nouveau projet** boîte de dialogue, développez **installé** > **modèles**, puis sélectionnez **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2339a-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="2339a-179">Dans la liste hello des modèles, sélectionnez **Storm exemple**.</span><span class="sxs-lookup"><span data-stu-id="2339a-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="2339a-180">Bas hello de boîte de dialogue hello, tapez un nom pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="2339a-182">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2339a-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2339a-183">Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2339a-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="2339a-184">Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2339a-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="2339a-185">Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="2339a-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="2339a-186">Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2339a-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="2339a-187">Lors de la topologie de hello a été envoyé avec succès, hello **Storm Topologies** pour le cluster de hello doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="2339a-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="2339a-188">Sélectionnez la topologie de hello dans hello liste tooview informations hello topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2339a-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![Visual Studio Monitor](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="2339a-190">Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs** en développant **Azure** > **HDInsight**, puis en cliquant avec le bouton droit sur le cluster HDInsight et en sélectionnant **Affichage des topologies Storm**.</span><span class="sxs-lookup"><span data-stu-id="2339a-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="2339a-191">Sélectionnez la forme de hello pour hello becs verseurs amovibles ou boulons tooview d’informations sur ces composants.</span><span class="sxs-lookup"><span data-stu-id="2339a-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="2339a-192">Une nouvelle fenêtre s’ouvre pour chaque élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2339a-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2339a-193">nom Hello de topologie de hello est le nom de classe hello de topologie de hello (dans ce cas, `HelloWord`,) avec un horodatage ajouté.</span><span class="sxs-lookup"><span data-stu-id="2339a-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="2339a-194">À partir de hello **récapitulatif de la topologie** afficher, sélectionnez **Kill** topologie de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="2339a-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2339a-195">Les topologies Storm poursuivre l’exécution jusqu'à ce qu’ils sont arrêtés ou cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="2339a-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="2339a-196">API REST</span><span class="sxs-lookup"><span data-stu-id="2339a-196">REST API</span></span>

<span data-ttu-id="2339a-197">Hello Storm UI repose sur hello API REST, afin de pouvoir effectuer similaires de gestion et de la fonctionnalité d’analyse à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="2339a-198">Vous pouvez utiliser des outils personnalisés hello API REST toocreate pour gérer et surveiller les topologies de Storm.</span><span class="sxs-lookup"><span data-stu-id="2339a-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="2339a-199">Pour plus d’informations, consultez la rubrique [API REST de l’interface utilisateur Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="2339a-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="2339a-200">Hello informations suivantes sont spécifiques toousing hello API REST avec Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2339a-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="2339a-201">URI de base</span><span class="sxs-lookup"><span data-stu-id="2339a-201">Base URI</span></span>

<span data-ttu-id="2339a-202">Hello est de l’URI de base pour l’API REST de hello sur les clusters HDInsight **https://&lt;nom_cluster >.azurehdinsight.net/stormui/api/v1/**, où **clustername** désigne hello votre Storm sur Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2339a-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="2339a-203">Authentification</span><span class="sxs-lookup"><span data-stu-id="2339a-203">Authentication</span></span>

<span data-ttu-id="2339a-204">Toohello demandes API REST doivent utiliser **l’authentification de base**, de sorte que vous utilisez le nom du cluster hello HDInsight administrateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2339a-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="2339a-205">Étant donné que l’authentification de base est envoyée à l’aide de texte en clair, vous devez **toujours** utiliser les communications HTTPS toosecure avec cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="2339a-206">Valeurs de retour</span><span class="sxs-lookup"><span data-stu-id="2339a-206">Return values</span></span>

<span data-ttu-id="2339a-207">Informations qui sont retournées à partir de hello API REST peuvent uniquement être utilisable à partir de cluster de hello ou ordinateurs virtuels sur hello même réseau virtuel Azure en tant que cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2339a-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="2339a-208">Par exemple, nom de domaine complet de hello (FQDN) retournée pour les serveurs soigneur ne sont pas être accessible à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="2339a-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2339a-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2339a-209">Next Steps</span></span>

<span data-ttu-id="2339a-210">Maintenant que vous avez appris comment topologies toodeploy et le moniteur à l’aide de hello Storm le tableau de bord, découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="2339a-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="2339a-211">Développer les topologies c# à l’aide des outils de hello HDInsight pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2339a-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="2339a-212">Développer des topologies basées sur Java à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="2339a-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="2339a-213">Pour accéder à une liste d’exemples supplémentaires de topologies, consultez la rubrique [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2339a-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
