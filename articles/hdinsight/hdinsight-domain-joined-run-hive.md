---
title: "Configuration de stratégies Hive dans HDInsight joint à un domaine - Azure | Microsoft Docs"
description: "Découvrir..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="9624b-103">Configuration de stratégies Hive dans HDInsight joint à un domaine (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="9624b-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="9624b-104">Découvrez comment configurer des stratégies Apache Ranger pour Hive.</span><span class="sxs-lookup"><span data-stu-id="9624b-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="9624b-105">Dans cet article, vous créez deux stratégies Ranger pour restreindre l’accès à hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9624b-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="9624b-106">hivesampletable dispose de clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9624b-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="9624b-107">Après avoir configuré les stratégies, vous utilisez Excel et le pilote ODBC pour vous connecter à des tables Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9624b-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9624b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9624b-108">Prerequisites</span></span>
* <span data-ttu-id="9624b-109">Un cluster HDInsight joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="9624b-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="9624b-110">Consultez [Configuration de cluster HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9624b-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="9624b-111">Une station de travail avec Office 2016, Office 2013 ProPlus, Office 365 Pro Plus, l’édition autonome d’Excel 2013 ou Office Professionnel Plus 2010.</span><span class="sxs-lookup"><span data-stu-id="9624b-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="9624b-112">Connexion à l’interface utilisateur Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="9624b-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="9624b-113">**Pour vous connecter à l’interface utilisateur Ranger**</span><span class="sxs-lookup"><span data-stu-id="9624b-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="9624b-114">Dans un navigateur, connectez-vous à l’interface utilisateur Ranger.</span><span class="sxs-lookup"><span data-stu-id="9624b-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="9624b-115">L’URL est https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="9624b-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9624b-116">Ranger utilise des informations d’identification différentes de celles du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9624b-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="9624b-117">Pour empêcher les navigateurs d’utiliser les informations d’identification Hadoop mises en cache, utilisez une nouvelle fenêtre de navigation InPrivate pour vous connecter à l’interface utilisateur administrateur Ranger.</span><span class="sxs-lookup"><span data-stu-id="9624b-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="9624b-118">Connectez-vous avec le nom d’utilisateur et le mot de passe du domaine de l’administrateur du cluster :</span><span class="sxs-lookup"><span data-stu-id="9624b-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Page d’accueil Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="9624b-120">Actuellement, Ranger fonctionne uniquement avec Yarn et Hive.</span><span class="sxs-lookup"><span data-stu-id="9624b-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="9624b-121">Création d’utilisateurs du domaine</span><span class="sxs-lookup"><span data-stu-id="9624b-121">Create Domain users</span></span>
<span data-ttu-id="9624b-122">Dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), vous avez créé hiveruser1 et hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="9624b-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="9624b-123">Vous allez utiliser les deux comptes utilisateur dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9624b-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="9624b-124">Création de stratégies Ranger</span><span class="sxs-lookup"><span data-stu-id="9624b-124">Create Ranger policies</span></span>
<span data-ttu-id="9624b-125">Dans cette section, vous allez créer deux stratégies Ranger pour accéder à hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="9624b-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="9624b-126">Vous accordez une autorisation select sur différents ensembles de colonnes.</span><span class="sxs-lookup"><span data-stu-id="9624b-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="9624b-127">Les deux utilisateurs ont été créés dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="9624b-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="9624b-128">Dans la section suivante, vous allez tester les deux stratégies dans Excel.</span><span class="sxs-lookup"><span data-stu-id="9624b-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="9624b-129">**Pour créer des stratégies Ranger**</span><span class="sxs-lookup"><span data-stu-id="9624b-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="9624b-130">Ouvrez l’interface utilisateur Ranger.</span><span class="sxs-lookup"><span data-stu-id="9624b-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="9624b-131">Consultez [Connexion à l’interface utilisateur Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="9624b-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="9624b-132">Cliquez sur **&lt;ClusterName>_hive** sous **Hive**.</span><span class="sxs-lookup"><span data-stu-id="9624b-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="9624b-133">Deux stratégies préconfigurées doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="9624b-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="9624b-134">Cliquez sur **Ajouter une nouvelle stratégie**, puis entrez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="9624b-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="9624b-135">Nom de la stratégie : read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="9624b-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="9624b-136">Base de données Hive : par défaut</span><span class="sxs-lookup"><span data-stu-id="9624b-136">Hive Database: default</span></span>
   * <span data-ttu-id="9624b-137">table : hivesampletable</span><span class="sxs-lookup"><span data-stu-id="9624b-137">table: hivesampletable</span></span>
   * <span data-ttu-id="9624b-138">Colonne Hive : *</span><span class="sxs-lookup"><span data-stu-id="9624b-138">Hive column: *</span></span>
   * <span data-ttu-id="9624b-139">Sélectionner un utilisateur : hiveuser1</span><span class="sxs-lookup"><span data-stu-id="9624b-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="9624b-140">Autorisations : select</span><span class="sxs-lookup"><span data-stu-id="9624b-140">Permissions: select</span></span>

     ![Configuration de stratégie Hive pour Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="9624b-142">.</span><span class="sxs-lookup"><span data-stu-id="9624b-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9624b-143">Si un utilisateur de domaine n’est pas renseigné dans Sélectionner un utilisateur, attendez quelques instants que Ranger se synchronise avec AAD.</span><span class="sxs-lookup"><span data-stu-id="9624b-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="9624b-144">Cliquez sur **Ajouter** pour enregistrer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="9624b-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="9624b-145">Répétez les deux dernières étapes pour créer une autre stratégie avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="9624b-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="9624b-146">Nom de la stratégie : read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="9624b-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="9624b-147">Base de données Hive : par défaut</span><span class="sxs-lookup"><span data-stu-id="9624b-147">Hive Database: default</span></span>
   * <span data-ttu-id="9624b-148">table : hivesampletable</span><span class="sxs-lookup"><span data-stu-id="9624b-148">table: hivesampletable</span></span>
   * <span data-ttu-id="9624b-149">Colonne Hive : clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="9624b-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="9624b-150">Sélectionner un utilisateur : hiveuser2</span><span class="sxs-lookup"><span data-stu-id="9624b-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="9624b-151">Autorisations : select</span><span class="sxs-lookup"><span data-stu-id="9624b-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="9624b-152">Création d’une source de données ODBC Hive</span><span class="sxs-lookup"><span data-stu-id="9624b-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="9624b-153">Vous trouverez les instructions dans [Création d’une source de données ODBC Hive](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="9624b-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="9624b-154">Propriété</span><span class="sxs-lookup"><span data-stu-id="9624b-154">Property</span></span>|<span data-ttu-id="9624b-155">Description</span><span class="sxs-lookup"><span data-stu-id="9624b-155">Description</span></span>
    ---|---
    <span data-ttu-id="9624b-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="9624b-156">Data Source Name</span></span>|<span data-ttu-id="9624b-157">Donnez un nom à votre source de données</span><span class="sxs-lookup"><span data-stu-id="9624b-157">Give a name to your data source</span></span>
    <span data-ttu-id="9624b-158">Host</span><span class="sxs-lookup"><span data-stu-id="9624b-158">Host</span></span>|<span data-ttu-id="9624b-159">Entrez &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9624b-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="9624b-160">Par exemple, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="9624b-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="9624b-161">Port</span><span class="sxs-lookup"><span data-stu-id="9624b-161">Port</span></span>|<span data-ttu-id="9624b-162">Utilisez <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="9624b-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="9624b-163">(ce port est passé de 563 à 443).</span><span class="sxs-lookup"><span data-stu-id="9624b-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="9624b-164">Base de données</span><span class="sxs-lookup"><span data-stu-id="9624b-164">Database</span></span>|<span data-ttu-id="9624b-165">Utilisez <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="9624b-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="9624b-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="9624b-166">Hive Server Type</span></span>|<span data-ttu-id="9624b-167">Sélectionnez <strong>Hive Server 2</strong>.</span><span class="sxs-lookup"><span data-stu-id="9624b-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="9624b-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="9624b-168">Mechanism</span></span>|<span data-ttu-id="9624b-169">Sélectionnez <strong>Azure HDInsight Service</strong>.</span><span class="sxs-lookup"><span data-stu-id="9624b-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="9624b-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="9624b-170">HTTP Path</span></span>|<span data-ttu-id="9624b-171">Laissez cette valeur vide.</span><span class="sxs-lookup"><span data-stu-id="9624b-171">Leave it blank.</span></span>
    <span data-ttu-id="9624b-172">User Name</span><span class="sxs-lookup"><span data-stu-id="9624b-172">User Name</span></span>|<span data-ttu-id="9624b-173">Entrez hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9624b-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="9624b-174">Mettez à jour le nom de domaine s’il est différent.</span><span class="sxs-lookup"><span data-stu-id="9624b-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="9624b-175">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="9624b-175">Password</span></span>|<span data-ttu-id="9624b-176">Entrez le mot de passe pour hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="9624b-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="9624b-177">Veillez à cliquer sur **Test** avant d’enregistrer la source de données.</span><span class="sxs-lookup"><span data-stu-id="9624b-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="9624b-178">Importation de données dans Microsoft Excel à partir de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9624b-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="9624b-179">Dans la dernière section, vous avez configuré deux stratégies.</span><span class="sxs-lookup"><span data-stu-id="9624b-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="9624b-180">hiveuser1 a l’autorisation select sur toutes les colonnes et hiveuser2 a l’autorisation select sur deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="9624b-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="9624b-181">Dans cette section, vous représentez les deux utilisateurs pour importer des données dans Excel.</span><span class="sxs-lookup"><span data-stu-id="9624b-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="9624b-182">Ouvrez un nouveau classeur ou un classeur existant dans Excel.</span><span class="sxs-lookup"><span data-stu-id="9624b-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="9624b-183">À partir de l’onglet **Données**, cliquez sur **À partir d’autres sources de données**, puis sur **Provenance : Assistant Connexion de données** pour lancer **l’Assistant Connexion de données**.</span><span class="sxs-lookup"><span data-stu-id="9624b-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="9624b-184">![Assistant Ouvrir la connexion de données][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="9624b-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="9624b-185">Sélectionnez **DSN ODBC** comme source de données, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9624b-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="9624b-186">Dans Sources de données ODBC, sélectionnez le nom de la source de données que vous avez créée à l’étape précédente, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9624b-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="9624b-187">Entrez à nouveau le mot de passe pour le cluster dans l’Assistant, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9624b-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="9624b-188">Attendez l'ouverture de la boîte de dialogue **Sélection d'une base de données et d'une table** .</span><span class="sxs-lookup"><span data-stu-id="9624b-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="9624b-189">Cette opération peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="9624b-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="9624b-190">Sélectionnez **hivesampletable**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9624b-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="9624b-191">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="9624b-191">Click **Finish**.</span></span>
8. <span data-ttu-id="9624b-192">Dans la boîte de dialogue **Importation de données** , vous pouvez modifier ou spécifier la requête.</span><span class="sxs-lookup"><span data-stu-id="9624b-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="9624b-193">Pour cela, cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9624b-193">To do so, click **Properties**.</span></span> <span data-ttu-id="9624b-194">Cette opération peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="9624b-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="9624b-195">Cliquez sur l’onglet **Définition**.</span><span class="sxs-lookup"><span data-stu-id="9624b-195">Click the **Definition** tab.</span></span> <span data-ttu-id="9624b-196">Le texte de commande est le suivant :</span><span class="sxs-lookup"><span data-stu-id="9624b-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="9624b-197">Selon les stratégies Ranger que vous avez définies, hiveuser1 a l’autorisation select sur toutes les colonnes.</span><span class="sxs-lookup"><span data-stu-id="9624b-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="9624b-198">Par conséquent, cette requête fonctionne avec les informations d’identification de hiveuser1, mais cette requête ne fonctionne pas avec les informations d’identification de hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="9624b-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="9624b-199">![Propriétés de connexion][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="9624b-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="9624b-200">Cliquez sur **OK** pour fermer la boîte de dialogue Propriétés de connexion.</span><span class="sxs-lookup"><span data-stu-id="9624b-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="9624b-201">Cliquez sur **OK** pour fermer la boîte de dialogue **Importation de données**.</span><span class="sxs-lookup"><span data-stu-id="9624b-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="9624b-202">Entrez à nouveau le mot de passe pour hiveuser1 et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9624b-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="9624b-203">Patientez quelques secondes pour que les données soient importées dans Excel.</span><span class="sxs-lookup"><span data-stu-id="9624b-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="9624b-204">Une fois terminé, 11 colonnes de données doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="9624b-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="9624b-205">Pour tester la deuxième stratégie (read-hivesampletable-devicemake) que vous avez créée dans la dernière section</span><span class="sxs-lookup"><span data-stu-id="9624b-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="9624b-206">Ajoutez une nouvelle feuille dans Excel.</span><span class="sxs-lookup"><span data-stu-id="9624b-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="9624b-207">Suivez la procédure précédente pour importer les données.</span><span class="sxs-lookup"><span data-stu-id="9624b-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="9624b-208">La seule modification à effectuer consiste à utiliser les informations d’identification de hiveuser2 au lieu de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="9624b-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="9624b-209">Cette opération échouera, car hiveuser2 n’est autorisé à afficher que deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="9624b-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="9624b-210">Vous devez obtenir l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="9624b-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="9624b-211">Suivez la même procédure pour importer les données.</span><span class="sxs-lookup"><span data-stu-id="9624b-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="9624b-212">Cette fois, utilisez les informations d’identification de hiveuser2 et modifiez également l’instruction select de :</span><span class="sxs-lookup"><span data-stu-id="9624b-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="9624b-213">to:</span><span class="sxs-lookup"><span data-stu-id="9624b-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="9624b-214">Une fois terminé, deux colonnes de données importées doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="9624b-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9624b-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9624b-215">Next steps</span></span>
* <span data-ttu-id="9624b-216">Pour configurer un cluster HDInsight joint à un domaine, consultez [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9624b-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="9624b-217">Pour gérer un cluster HDInsight joint à un domaine, consultez [Gestion de clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="9624b-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="9624b-218">Pour exécuter des requêtes Hive en utilisant SSH sur des clusters HDInsight joints au domaine, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="9624b-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="9624b-219">Pour connecter Hive à l’aide de Hive JDBC, consultez [Se connecter à Hive sur Azure HDInsight à l’aide du pilote Hive JDBC](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="9624b-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="9624b-220">Pour connecter Excel à Hadoop à l’aide de Hive ODBC, consultez [Connexion d’Excel à Hadoop à l’aide du pilote Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="9624b-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="9624b-221">Pour connecter Excel à Hadoop à l’aide de Power Query, consultez [Connexion d’Excel à Hadoop à l’aide de Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="9624b-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
