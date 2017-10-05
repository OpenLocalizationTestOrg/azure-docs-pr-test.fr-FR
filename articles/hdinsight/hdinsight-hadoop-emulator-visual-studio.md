---
title: Data Lake Tools pour Visual Studio avec Hortonworks Sandbox - Azure HDInsight | Microsoft Docs
description: "Apprenez à utiliser Data Lake Tools pour Visual Studio avec le bac à sable Hortonworks s’exécutant sur une machine virtuelle locale. Ces outils vous permettent de créer et d’exécuter des travaux Hive et Pig sur le bac à sable, ainsi que d’en afficher le résultat et l’historique."
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
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="ab6a7-104">Utiliser Azure Data Lake Tools pour Visual Studio avec le Bac à sable (sandbox) Hortonworks</span><span class="sxs-lookup"><span data-stu-id="ab6a7-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="ab6a7-105">Azure Data Lake inclut des outils permettant de travailler avec des clusters Hadoop génériques.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="ab6a7-106">Ce document décrit les étapes nécessaires pour utiliser Data Lake Tools avec le Bac à sable (sandbox) Hortonworks s’exécutant sur une machine virtuelle locale.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="ab6a7-107">Hortonworks Sandbox permet de travailler avec Hadoop localement sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="ab6a7-108">Après avoir développé une solution, lorsque vous souhaitez la déployer à grande échelle, vous pouvez passer à un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab6a7-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ab6a7-109">Prerequisites</span></span>

* <span data-ttu-id="ab6a7-110">Le Bac à sable (sandbox) Hortonworks s’exécutant sur une machine virtuelle dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="ab6a7-111">Ce document a été écrit et testé avec le bac à sable s’exécutant sur Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="ab6a7-112">Pour plus d’informations sur le paramétrage du bac à sable, consultez [Get started with the Hortonworks sandbox](hdinsight-hadoop-emulator-get-started.md) (Prise en main du bac à sable Hortonworks)</span><span class="sxs-lookup"><span data-stu-id="ab6a7-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="ab6a7-113">document.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-113">document.</span></span>

* <span data-ttu-id="ab6a7-114">Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (toute édition).</span><span class="sxs-lookup"><span data-stu-id="ab6a7-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="ab6a7-115">Le [Kit de développement logiciel (SDK) Azure pour .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="ab6a7-116">[Azure Data Lake Tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="ab6a7-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="ab6a7-117">Configuration des mots de passe pour le bac à sable</span><span class="sxs-lookup"><span data-stu-id="ab6a7-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="ab6a7-118">Assurez-vous que le Bac à sable (sandbox) Hortonworks est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="ab6a7-119">Puis suivez les instructions décrites dans le document [Get started with the Hortonworks sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) (Prise en main du bac à sable Hortonworks).</span><span class="sxs-lookup"><span data-stu-id="ab6a7-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="ab6a7-120">Ces étapes permettent de configurer le mot de passe pour le compte SSH `root` et le compte Ambari `admin`.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="ab6a7-121">Ces mots de passe vous permettent de vous connecter au bac à sable à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="ab6a7-122">Connexion des outils au bac à sable</span><span class="sxs-lookup"><span data-stu-id="ab6a7-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="ab6a7-123">Ouvrez Visual Studio, sélectionnez **Afficher**, puis **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="ab6a7-124">Dans **l’Explorateur de serveurs**, cliquez avec le bouton droit sur l’entrée **HDInsight**, puis sélectionnez **Connexion à l’émulateur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec Se connecter à l’émulateur HDInsight en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="ab6a7-126">Dans la boîte de dialogue **Se connecter à l’émulateur HDInsight**, entrez le mot de passe que vous avez configuré pour Ambari.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="ab6a7-128">Sélectionnez **Suivant** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="ab6a7-129">Utilisez le champ **Mot de passe** pour entrer le mot de passe que vous avez configuré pour le compte `root`.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="ab6a7-130">Conservez la valeur par défaut dans les autres champs.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-130">Leave the other fields at the default value.</span></span>

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="ab6a7-132">Sélectionnez **Suivant** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="ab6a7-133">Attendez que la validation des services s’achève.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="ab6a7-134">Dans certains cas, la validation peut échouer et vous inviter à mettre à jour la configuration.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="ab6a7-135">Si la validation échoue, sélectionnez **Mettre à jour**, puis attendez la fin de la configuration et de la vérification du service.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![Capture d’écran de la boîte de dialogue avec le bouton Mettre à jour en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="ab6a7-137">Le processus de mise à jour utilise Ambari pour remplacer la configuration du Bac à sable (sandbox) Hortonworks par celle attendue par Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="ab6a7-138">Une fois la validation terminée, sélectionnez **Terminer** pour achever la configuration.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="ab6a7-139">![Capture d’écran de la boîte de dialogue avec le bouton Terminer en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="ab6a7-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="ab6a7-140">Selon la vitesse de votre environnement de développement et la quantité de mémoire allouée à la machine virtuelle, la configuration et la validation des services peuvent prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="ab6a7-141">Une fois ces étapes accomplies, une entrée **HDInsight local cluster** apparaît dans la section **HDInsight** de l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="ab6a7-142">Écriture d’une requête Hive</span><span class="sxs-lookup"><span data-stu-id="ab6a7-142">Write a Hive query</span></span>

<span data-ttu-id="ab6a7-143">Hive fournit un langage de requête de type SQL (HiveQL) pour le traitement des données structurées.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="ab6a7-144">Suivez les instructions suivantes pour apprendre à exécuter des requêtes à la demande sur le cluster local.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="ab6a7-145">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur l’entrée du cluster local que vous avez ajouté précédemment, puis sélectionnez **Écrire une requête Hive**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec Écrire une requête Hive en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="ab6a7-147">Une nouvelle fenêtre de requête s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-147">A new query window appears.</span></span> <span data-ttu-id="ab6a7-148">Vous pouvez alors rapidement rédiger et envoyer une requête vers le cluster local.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="ab6a7-149">Dans la nouvelle fenêtre de requête, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ab6a7-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="ab6a7-150">Pour exécuter la requête, sélectionnez **Envoyer** en haut de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="ab6a7-151">Laissez les autres valeurs (**lot** et nom du serveur) par défaut.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![Capture d’écran de la fenêtre de requête avec le bouton Envoyer en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="ab6a7-153">Vous pouvez également utiliser le menu déroulant en regard **d’Envoyer** pour sélectionner **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="ab6a7-154">Les options avancées vous permettent de spécifier des options supplémentaires lors de l’envoi du travail.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="ab6a7-156">Une fois la requête envoyée, l’état du travail s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="ab6a7-157">Celui-ci présente des informations sur le travail tel que Hadoop l’a traité.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="ab6a7-158">Le champ **État du travail** indique l’état du travail.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="ab6a7-159">Cet état est mis à jour régulièrement. Vous pouvez également utiliser l’icône d’actualisation pour rafraîchir l’état manuellement.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![Capture d’écran de la boîte de dialogue Vue du travail, avec État du travail en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="ab6a7-161">Quand **État du travail** passe à **Terminé**, un graphe orienté acyclique (DAG) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="ab6a7-162">Ce diagramme décrit le chemin d’exécution déterminé par Tez lors du traitement de la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="ab6a7-163">Tez est le moteur d’exécution par défaut pour Hive sur le cluster local.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab6a7-164">Tez est également le moteur par défaut lorsque vous utilisez des clusters HDInsight basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="ab6a7-165">Il n’est pas le moteur par défaut pour HDInsight basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="ab6a7-166">Pour l’utiliser dans cette configuration, vous devez ajouter la ligne `set hive.execution.engine = tez;` au début de votre requête Hive.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="ab6a7-167">Utilisez le lien **Sortie de la tâche** pour afficher la sortie.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="ab6a7-168">En l’occurrence, il s’agit de 823, soit le nombre de lignes contenues dans la table sample_08.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="ab6a7-169">Vous pouvez afficher des informations de diagnostic sur la tâche à l’aide des liens **Journal de la tâche** et **Download YARN Log (Télécharger le journal YARN)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="ab6a7-170">Vous pouvez également exécuter des travaux Hive de façon interactive en définissant le champ **Lot** sur **Interactif**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="ab6a7-171">Sélectionnez ensuite **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-171">Then select **Execute**.</span></span>

    ![Capture d’écran avec les boutons Interactif et Exécuter en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="ab6a7-173">Une requête interactive affiche le journal de sortie généré lors du traitement dans la fenêtre **HiveServer2 Output** (Sortie HiveServer2).</span><span class="sxs-lookup"><span data-stu-id="ab6a7-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab6a7-174">Ces informations sont identiques à celles accessibles via le lien **Journal du travail** une fois le travail terminé.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![Capture d’écran du journal de sortie](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="ab6a7-176">Création d’un projet Hive</span><span class="sxs-lookup"><span data-stu-id="ab6a7-176">Create a Hive project</span></span>

<span data-ttu-id="ab6a7-177">Vous pouvez également créer un projet qui contient plusieurs scripts Hive.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="ab6a7-178">Utilisez un projet lorsque vous possédez des scripts associés ou que vous souhaitez stocker des scripts dans un système de gestion de version.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="ab6a7-179">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="ab6a7-180">Dans la liste des projets, développez **Modèles**, **Azure Data Lake**, puis sélectionnez **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="ab6a7-181">Dans la liste des modèles, sélectionnez **Hive Sample (Exemple Hive)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="ab6a7-182">Entrez un nom et un emplacement, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-182">Enter a name and location, and then select **OK**.</span></span>

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, HIVE, Hive Sample (Exemple Hive) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="ab6a7-184">Le projet **Hive Sample (Exemple Hive)** contient deux scripts, **WebLogAnalysis.hql** et **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="ab6a7-185">Vous pouvez les envoyer à l’aide du même bouton **Envoyer** en haut de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="ab6a7-186">Création d’un projet Pig</span><span class="sxs-lookup"><span data-stu-id="ab6a7-186">Create a Pig project</span></span>

<span data-ttu-id="ab6a7-187">Contrairement à Hive qui offre un langage de type SQL pour travailler avec des données structurées, Pig effectue des transformations sur les données.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="ab6a7-188">Pig fournit un langage (Pig Latin) permettant de développer un pipeline des transformations.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="ab6a7-189">Pour utiliser Pig avec le cluster local, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ab6a7-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="ab6a7-190">Ouvrez Visual Studio et sélectionnez **Fichier**, **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="ab6a7-191">Dans la liste des projets, développez **Modèles**, **Azure Data Lake**, puis sélectionnez **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="ab6a7-192">Dans la liste des modèles, sélectionnez **Pig Application (Application Pig)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="ab6a7-193">Entrez un nom et un emplacement, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-193">Enter a name, location, and then select **OK**.</span></span>

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, Pig, Pig Application (Application Pig) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="ab6a7-195">Entrez le texte suivant comme contenu du fichier **script.pig** créé dans le cadre de ce projet.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="ab6a7-196">Bien que Pig n’utilise pas le même langage que Hive, le mode d’exécution des travaux via le bouton **Envoyer** est cohérent pour les deux langages.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="ab6a7-197">La sélection de la liste déroulante en regard de **Envoyer** permet d’afficher une boîte de dialogue Envoyer contenant des options avancées pour Pig.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="ab6a7-199">L’état du travail et la sortie s’affichent de la même façon que pour une requête Hive.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![Capture d’écran d’un travail Pig terminé](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="ab6a7-201">Affichage des tâches</span><span class="sxs-lookup"><span data-stu-id="ab6a7-201">View jobs</span></span>

<span data-ttu-id="ab6a7-202">Les outils Data Lake Tools permettent également d’afficher facilement les informations relatives aux travaux exécutés sur Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="ab6a7-203">Pour afficher les travaux exécutés sur le cluster local, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="ab6a7-204">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur le cluster local, puis sélectionnez **Afficher les travaux**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="ab6a7-205">Une liste des tâches qui ont été soumises au cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec Afficher les travaux en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="ab6a7-207">Dans la liste des tâches, sélectionnez-en une pour en afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-207">From the list of jobs, select one to view the job details.</span></span>

    ![Capture d’écran de l’Explorateur de travaux avec l’un des travaux en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="ab6a7-209">Les informations affichées sont similaires à celles qui s’affichent après l’exécution d’une requête Hive ou Pig. Elles incluent des liens permettant d’afficher les informations de sortie et de journal.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="ab6a7-210">Vous pouvez également modifier et soumettre à nouveau la tâche à partir d’ici.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="ab6a7-211">Affichage des bases de données Hive</span><span class="sxs-lookup"><span data-stu-id="ab6a7-211">View Hive databases</span></span>

1. <span data-ttu-id="ab6a7-212">Dans **l’Explorateur de serveurs**, développez l’entrée **cluster local HDInsight**, puis développez **Bases de données Hive**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="ab6a7-213">Les bases de données **Par défaut** et **xademo** sur le cluster local sont affichées.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="ab6a7-214">Le développement d’une base de données a pour effet d’afficher les tables que celle-ci contient.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-214">Expanding a database shows the tables within the database.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec des bases de données développées](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="ab6a7-216">Le développement d’une table affiche les colonnes qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="ab6a7-217">Pour afficher rapidement les données, cliquez avec le bouton droit sur une table, puis sélectionnez **Afficher les 100 premières lignes**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Capture d’écran de l’Explorateur de serveurs avec une table développée et l’option Afficher les 100 premières lignes sélectionnée](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="ab6a7-219">Propriétés de base de données et de table</span><span class="sxs-lookup"><span data-stu-id="ab6a7-219">Database and table properties</span></span>

<span data-ttu-id="ab6a7-220">Vous pouvez afficher les propriétés d’une base de données ou d’une table.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="ab6a7-221">La sélection de **Propriétés** affiche les détails de l’élément sélectionné dans la fenêtre Propriétés.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="ab6a7-222">Par exemple, examinez les informations affichées dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="ab6a7-222">For example, see the information shown in the following screenshot:</span></span>

![Capture d’écran de le fenêtre Propriétés](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="ab6a7-224">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="ab6a7-224">Create a table</span></span>

<span data-ttu-id="ab6a7-225">Pour créer une table, cliquez avec le bouton droit sur une base de données, puis sélectionnez **Créer une table**.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![Capture d’écran de l’Explorateur de serveurs avec Créer une table en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="ab6a7-227">Vous pouvez ensuite créer la table à l’aide d’un formulaire.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-227">You can then create the table using a form.</span></span> <span data-ttu-id="ab6a7-228">Au bas de la capture d’écran suivante, vous pouvez voir le HiveQL brut utilisé pour créer la table.</span><span class="sxs-lookup"><span data-stu-id="ab6a7-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![Capture d’écran du formulaire utilisé pour créer une table](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="ab6a7-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab6a7-230">Next steps</span></span>

* [<span data-ttu-id="ab6a7-231">Se familiariser avec Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="ab6a7-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="ab6a7-232">Didacticiel Hadoop - Prise en main de HDP</span><span class="sxs-lookup"><span data-stu-id="ab6a7-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
