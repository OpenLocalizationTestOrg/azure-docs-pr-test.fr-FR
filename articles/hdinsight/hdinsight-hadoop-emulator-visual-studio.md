---
title: outils aaaData Lake pour Visual Studio avec Hortonworks Sandbox - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse hello des outils d’Azure Data Lake pour Visual Studio avec un sandbox de Hortonworks hello en cours d’exécution dans une machine virtuelle locale. Grâce à ces outils, vous pouvez créer et exécuter des tâches Hive et Pig sur sandbox de hello et de sortie de travail vue et de l’historique."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="2de8a-104">Utiliser les outils d’Azure Data Lake hello pour Visual Studio avec hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="2de8a-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="2de8a-105">Azure Data Lake inclut des outils permettant de travailler avec des clusters Hadoop génériques.</span><span class="sxs-lookup"><span data-stu-id="2de8a-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="2de8a-106">Ce document fournit la procédure de hello nécessitent toouse hello Data Lake outils hello Hortonworks Sandbox en cours d’exécution sur un ordinateur virtuel local.</span><span class="sxs-lookup"><span data-stu-id="2de8a-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="2de8a-107">À l’aide de hello bac à sable Hortonworks vous permet de toowork avec Hadoop localement sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="2de8a-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="2de8a-108">Une fois que vous avez développé une solution et que vous souhaitez toodeploy il à grande échelle, vous pouvez ensuite déplacer le cluster HDInsight de tooan.</span><span class="sxs-lookup"><span data-stu-id="2de8a-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2de8a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2de8a-109">Prerequisites</span></span>

* <span data-ttu-id="2de8a-110">Hello Hortonworks Sandbox, en cours d’exécution sur un ordinateur virtuel sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="2de8a-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="2de8a-111">Ce document a été écrit et testé avec sandbox hello en cours d’exécution dans Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="2de8a-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="2de8a-112">Pour plus d’informations sur la configuration de bac à sable hello, consultez hello [prise en main sandbox de Hortonworks hello.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2de8a-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="2de8a-113">document.</span><span class="sxs-lookup"><span data-stu-id="2de8a-113">document.</span></span>

* <span data-ttu-id="2de8a-114">Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (toute édition).</span><span class="sxs-lookup"><span data-stu-id="2de8a-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="2de8a-115">Hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2de8a-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="2de8a-116">Hello [lac de données Azure tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="2de8a-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="2de8a-117">Configurer des mots de passe pour le bac à sable hello</span><span class="sxs-lookup"><span data-stu-id="2de8a-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="2de8a-118">Vérifiez que hello que hortonworks Sandbox est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2de8a-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="2de8a-119">Puis suivez les étapes de hello Bonjour [prise en main de hello bac à sable Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span><span class="sxs-lookup"><span data-stu-id="2de8a-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="2de8a-120">Ces étapes configurent le mot de passe hello hello SSH `root` de compte et hello Ambari `admin` compte.</span><span class="sxs-lookup"><span data-stu-id="2de8a-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="2de8a-121">Ces mots de passe sont utilisés lorsque vous vous connectez le bac à sable toohello à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2de8a-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="2de8a-122">Connecter le bac à sable toohello hello outils</span><span class="sxs-lookup"><span data-stu-id="2de8a-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="2de8a-123">Ouvrez Visual Studio, sélectionnez **Afficher**, puis **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="2de8a-124">À partir de **l’Explorateur de serveurs**, avec le bouton hello **HDInsight** entrée, puis sélectionnez **connecter tooHDInsight émulateur**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec connexion tooHDInsight émulateur mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="2de8a-126">À partir de hello **connecter tooHDInsight émulateur** boîte de dialogue, entrez le mot de passe hello que vous avez configuré pour Ambari.</span><span class="sxs-lookup"><span data-stu-id="2de8a-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="2de8a-128">Sélectionnez **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2de8a-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="2de8a-129">Hello d’utilisation **mot de passe** champ tooenter hello mot de passe vous avez configuré pour hello `root` compte.</span><span class="sxs-lookup"><span data-stu-id="2de8a-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="2de8a-130">Laissez hello autres champs à la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-130">Leave hello other fields at hello default value.</span></span>

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="2de8a-132">Sélectionnez **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2de8a-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="2de8a-133">Attendez que la validation de hello services toofinish.</span><span class="sxs-lookup"><span data-stu-id="2de8a-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="2de8a-134">Dans certains cas, la validation peut-être échouer et vous demande de configuration de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2de8a-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="2de8a-135">Si la validation échoue, sélectionnez **mise à jour**et attendez que la configuration de hello et de vérification pour hello service toofinish.</span><span class="sxs-lookup"><span data-stu-id="2de8a-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Capture d’écran de la boîte de dialogue avec le bouton Mettre à jour en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="2de8a-137">processus de mise à jour Hello utilise hello toomodify de Ambari toowhat de configuration de bac à sable Hortonworks attendu par les outils de Data Lake hello pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2de8a-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="2de8a-138">Une fois la validation terminée, sélectionnez **Terminer** toocomplete configuration.</span><span class="sxs-lookup"><span data-stu-id="2de8a-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="2de8a-139">![Capture d’écran de la boîte de dialogue avec le bouton Terminer en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="2de8a-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="2de8a-140">Selon la vitesse de hello de votre environnement de développement et hello quantité de mémoire allouée toohello virtual machine, il peut prendre plusieurs minutes tooconfigure et valider des services de hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="2de8a-141">Après avoir suivi ces étapes, vous avez maintenant un **cluster local HDInsight** entrée dans l’Explorateur de serveurs sous hello **HDInsight** section.</span><span class="sxs-lookup"><span data-stu-id="2de8a-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="2de8a-142">Écriture d’une requête Hive</span><span class="sxs-lookup"><span data-stu-id="2de8a-142">Write a Hive query</span></span>

<span data-ttu-id="2de8a-143">Hive fournit un langage de requête de type SQL (HiveQL) pour le traitement des données structurées.</span><span class="sxs-lookup"><span data-stu-id="2de8a-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="2de8a-144">Utilisez hello suivant toolearn étapes fonctionnement des requêtes sur le cluster local de hello toorun à la demande.</span><span class="sxs-lookup"><span data-stu-id="2de8a-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="2de8a-145">Dans **l’Explorateur de serveurs**, cliquez sur entrée hello pour le cluster local hello que vous avez ajouté précédemment, puis sélectionnez **écrire une requête Hive**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec Écrire une requête Hive en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="2de8a-147">Une nouvelle fenêtre de requête s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2de8a-147">A new query window appears.</span></span> <span data-ttu-id="2de8a-148">Ici, vous pouvez rapidement écrire et envoyer un cluster local toohello de requête.</span><span class="sxs-lookup"><span data-stu-id="2de8a-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="2de8a-149">Dans la nouvelle fenêtre de requête hello, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2de8a-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="2de8a-150">requête de hello toorun, sélectionnez **Submit** haut hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="2de8a-151">Laissez des autres valeurs hello (**lot** et le nom du serveur) à des valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Capture d’écran de la fenêtre de requête, avec le bouton d’envoi hello mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="2de8a-153">Vous pouvez également utiliser déroulante hello ensuite trop**Submit** tooselect **avancé**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="2de8a-154">Les options avancées permettent tooprovide des options supplémentaires lors de l’envoi de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="2de8a-156">Une fois que vous envoyez la requête de hello, état de la tâche hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2de8a-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="2de8a-157">état de la tâche Hello affiche des informations sur les travaux hello s’il est traité par Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2de8a-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="2de8a-158">**État de la tâche** indique l’état du travail de hello hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="2de8a-159">état de Hello est régulièrement mis à jour, ou vous pouvez utiliser hello actualiser icône toorefresh hello l’état manuellement.</span><span class="sxs-lookup"><span data-stu-id="2de8a-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Capture d’écran de la boîte de dialogue Vue du travail, avec État du travail en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="2de8a-161">Après avoir hello **état du travail** change également**terminé**, un graphique acyclique dirigé (DAG, Switched Virtual Circuit) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2de8a-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="2de8a-162">Ce diagramme décrit le chemin d’exécution hello qui a été déterminé par Tez lors du traitement de requête de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="2de8a-163">Tez est le moteur d’exécution par défaut de hello pour la ruche du cluster local de hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2de8a-164">Tez est également hello par défaut lorsque vous utilisez des clusters HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2de8a-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2de8a-165">Il n’est pas défaut hello sur HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="2de8a-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="2de8a-166">toouse il, vous devez ajouter la ligne de hello `set hive.execution.engine = tez;` début toohello de votre requête Hive.</span><span class="sxs-lookup"><span data-stu-id="2de8a-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="2de8a-167">Hello d’utilisation **sortie des tâches** lien de sortie de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="2de8a-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="2de8a-168">Dans ce cas, il est 823, nombre de hello de lignes dans la table de sample_08 hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="2de8a-169">Vous pouvez afficher des informations de diagnostic sur la tâche de hello en utilisant hello **journal des travaux** et **télécharger un journal fils** des liens.</span><span class="sxs-lookup"><span data-stu-id="2de8a-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="2de8a-170">Vous pouvez également exécuter des travaux de la ruche interactive en modifiant hello **lot** champ trop**Interactive**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="2de8a-171">Sélectionnez ensuite **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-171">Then select **Execute**.</span></span>

    ![Capture d’écran avec les boutons Interactif et Exécuter en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="2de8a-173">Une requête interactive flux hello le journal de sortie généré pendant le traitement toohello **HiveServer2 sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2de8a-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2de8a-174">Hello informations est hello même qui est disponible à partir de hello **journal des travaux** lier une fois une tâche terminée.</span><span class="sxs-lookup"><span data-stu-id="2de8a-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Capture d’écran du journal de sortie](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="2de8a-176">Création d’un projet Hive</span><span class="sxs-lookup"><span data-stu-id="2de8a-176">Create a Hive project</span></span>

<span data-ttu-id="2de8a-177">Vous pouvez également créer un projet qui contient plusieurs scripts Hive.</span><span class="sxs-lookup"><span data-stu-id="2de8a-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="2de8a-178">Utiliser un projet lorsque vous avez des scripts associés ou les scripts toostore dans un système de contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="2de8a-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="2de8a-179">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="2de8a-180">À partir de la liste de hello de projets, développez **modèles**, développez **Azure Data Lake**, puis sélectionnez **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="2de8a-181">Dans la liste hello des modèles, sélectionnez **exemple de la ruche**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="2de8a-182">Entrez un nom et un emplacement, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-182">Enter a name and location, and then select **OK**.</span></span>

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, HIVE, Hive Sample (Exemple Hive) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="2de8a-184">Hello **exemple de la ruche** projet contient deux scripts, **WebLogAnalysis.hql** et **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="2de8a-185">Vous pouvez soumettre ces scripts à l’aide de hello même **Submit** bouton en haut de hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="2de8a-186">Création d’un projet Pig</span><span class="sxs-lookup"><span data-stu-id="2de8a-186">Create a Pig project</span></span>

<span data-ttu-id="2de8a-187">Contrairement à Hive qui offre un langage de type SQL pour travailler avec des données structurées, Pig effectue des transformations sur les données.</span><span class="sxs-lookup"><span data-stu-id="2de8a-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="2de8a-188">Pig fournit un langage (Pig Latin) qui vous permet de toodevelop un pipeline de transformations.</span><span class="sxs-lookup"><span data-stu-id="2de8a-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="2de8a-189">toouse Pig avec le cluster local de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de8a-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="2de8a-190">Ouvrez Visual Studio et sélectionnez **Fichier**, **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="2de8a-191">À partir de la liste de hello de projets, développez **modèles**, développez **Azure Data Lake**, puis sélectionnez **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="2de8a-192">Dans la liste hello des modèles, sélectionnez **Pig Application**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="2de8a-193">Entrez un nom et un emplacement, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-193">Enter a name, location, and then select **OK**.</span></span>

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, Pig, Pig Application (Application Pig) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="2de8a-195">Entrez hello après le texte en tant que contenu hello Hello **script.pig** fichier qui a été créé avec ce projet.</span><span class="sxs-lookup"><span data-stu-id="2de8a-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="2de8a-196">Alors que Pig utilise une autre langue que la ruche, mode d’exécution de travaux de hello est cohérent entre les deux langages, de par Bonjour **Submit** bouton.</span><span class="sxs-lookup"><span data-stu-id="2de8a-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="2de8a-197">Liste déroulante en regard de hello en sélectionnant **Submit** affiche une boîte de dialogue avancées d’envoi pour Pig.</span><span class="sxs-lookup"><span data-stu-id="2de8a-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="2de8a-199">état de la tâche hello et de sortie s’affiche également, même hello en tant qu’une requête Hive.</span><span class="sxs-lookup"><span data-stu-id="2de8a-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Capture d’écran d’un travail Pig terminé](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="2de8a-201">Affichage des tâches</span><span class="sxs-lookup"><span data-stu-id="2de8a-201">View jobs</span></span>

<span data-ttu-id="2de8a-202">Outils de LAC de données vous permettent également tooeasily afficher des informations sur les travaux qui ont été exécutées sur Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2de8a-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="2de8a-203">Utilisez hello suivant les étapes toosee hello travaux qui ont été exécutées sur le cluster local de hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="2de8a-204">À partir de **l’Explorateur de serveurs**, cliquez sur le cluster local de hello, puis sélectionnez **afficher les travaux**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="2de8a-205">Une liste des tâches qui ont été soumis toohello cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2de8a-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec Afficher les travaux en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="2de8a-207">Dans la liste hello des tâches, sélectionnez une tooview détails de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Capture d’écran de travail de navigateur, avec l’un des travaux hello mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="2de8a-209">les informations de Hello affichées sont similaires toowhat qu'après l’exécution d’une requête Hive ou Pig, y compris des liens tooview hello sortie et le journal.</span><span class="sxs-lookup"><span data-stu-id="2de8a-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="2de8a-210">Vous pouvez également modifier et soumettez à nouveau la tâche hello à partir d’ici.</span><span class="sxs-lookup"><span data-stu-id="2de8a-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="2de8a-211">Affichage des bases de données Hive</span><span class="sxs-lookup"><span data-stu-id="2de8a-211">View Hive databases</span></span>

1. <span data-ttu-id="2de8a-212">Dans **l’Explorateur de serveurs**, développez hello **cluster local HDInsight** entrée, puis développez **bases de données de la ruche**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="2de8a-213">Hello **par défaut** et **xademo** bases de données sur le cluster local de hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="2de8a-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="2de8a-214">Une base de données en développant les tables au sein de la base de données hello hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec des bases de données développées](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="2de8a-216">Développer un tableau affiche hello colonnes de la table.</span><span class="sxs-lookup"><span data-stu-id="2de8a-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="2de8a-217">tooquickly afficher hello de données, cliquez sur une table et sélectionnez **100 lignes du haut vue**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec une table développée et l’option Afficher les 100 premières lignes sélectionnée](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="2de8a-219">Propriétés de base de données et de table</span><span class="sxs-lookup"><span data-stu-id="2de8a-219">Database and table properties</span></span>

<span data-ttu-id="2de8a-220">Vous pouvez afficher les propriétés de hello d’une base de données ou une table.</span><span class="sxs-lookup"><span data-stu-id="2de8a-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="2de8a-221">En sélectionnant **propriétés** affiche les détails d’élément de hello sélectionné dans la fenêtre de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="2de8a-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="2de8a-222">Par exemple, consultez les informations de hello illustrées hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="2de8a-222">For example, see hello information shown in hello following screenshot:</span></span>

![Capture d’écran de le fenêtre Propriétés](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="2de8a-224">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="2de8a-224">Create a table</span></span>

<span data-ttu-id="2de8a-225">toocreate une table, cliquez sur une base de données, puis sélectionnez **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="2de8a-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Capture d’écran de l’Explorateur de serveurs avec Créer une table en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="2de8a-227">Vous pouvez ensuite créer la table hello à l’aide d’un formulaire.</span><span class="sxs-lookup"><span data-stu-id="2de8a-227">You can then create hello table using a form.</span></span> <span data-ttu-id="2de8a-228">Au bas de hello de hello suivant capture d’écran, vous pouvez voir hello HiveQL brut qui est utilisé toocreate hello table.</span><span class="sxs-lookup"><span data-stu-id="2de8a-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Capture d’écran du formulaire de hello utilisé toocreate une table](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="2de8a-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2de8a-230">Next steps</span></span>

* [<span data-ttu-id="2de8a-231">Apprentissage des câbles hello Hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="2de8a-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="2de8a-232">Didacticiel Hadoop - Prise en main de HDP</span><span class="sxs-lookup"><span data-stu-id="2de8a-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
