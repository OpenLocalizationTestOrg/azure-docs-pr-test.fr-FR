---
title: "stratégies de ruche aaaConfigure dans HDInsight appartenant au domaine - Azure | Documents Microsoft"
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
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="e6589-103">Configuration de stratégies Hive dans HDInsight joint à un domaine (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="e6589-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="e6589-104">Découvrez comment les stratégies d’Apache Ranger tooconfigure pour la ruche.</span><span class="sxs-lookup"><span data-stu-id="e6589-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="e6589-105">Dans cet article, vous créez deux Ranger stratégies toorestrict accès toohello hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="e6589-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="e6589-106">Hello hivesampletable est fourni avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6589-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="e6589-107">Une fois que vous avez configuré des stratégies de hello, vous utilisez Excel et ODBC driver tooconnect tooHive les tables dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6589-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6589-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e6589-108">Prerequisites</span></span>
* <span data-ttu-id="e6589-109">Un cluster HDInsight joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="e6589-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="e6589-110">Consultez [Configuration de cluster HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e6589-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="e6589-111">Une station de travail avec Office 2016, Office 2013 ProPlus, Office 365 Pro Plus, l’édition autonome d’Excel 2013 ou Office Professionnel Plus 2010.</span><span class="sxs-lookup"><span data-stu-id="e6589-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="e6589-112">Se connecter tooApache Ranger l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="e6589-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="e6589-113">**tooconnect tooRanger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="e6589-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="e6589-114">À partir d’un navigateur, connectez-vous tooRanger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="e6589-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="e6589-115">URL de Hello est https://&lt;nom_cluster >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="e6589-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6589-116">Ranger utilise des informations d’identification différentes de celles du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e6589-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="e6589-117">navigateurs tooprevent à l’aide de la mise en cache des informations d’identification Hadoop, utiliser le nouveau navigateur inprivate fenêtre tooconnect toohello Ranger l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6589-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="e6589-118">Connectez-vous à l’aide du mot de passe et le nom d’utilisateur domaine hello cluster administrateur :</span><span class="sxs-lookup"><span data-stu-id="e6589-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Page d’accueil Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="e6589-120">Actuellement, Ranger fonctionne uniquement avec Yarn et Hive.</span><span class="sxs-lookup"><span data-stu-id="e6589-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="e6589-121">Création d’utilisateurs du domaine</span><span class="sxs-lookup"><span data-stu-id="e6589-121">Create Domain users</span></span>
<span data-ttu-id="e6589-122">Dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), vous avez créé hiveruser1 et hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="e6589-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="e6589-123">Vous allez utiliser le compte d’utilisateur en deux hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e6589-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="e6589-124">Création de stratégies Ranger</span><span class="sxs-lookup"><span data-stu-id="e6589-124">Create Ranger policies</span></span>
<span data-ttu-id="e6589-125">Dans cette section, vous allez créer deux stratégies Ranger pour accéder à hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="e6589-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="e6589-126">Vous accordez une autorisation select sur différents ensembles de colonnes.</span><span class="sxs-lookup"><span data-stu-id="e6589-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="e6589-127">Les deux utilisateurs ont été créés dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="e6589-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="e6589-128">Dans la section suivante de hello, vous allez tester les deux stratégies de hello dans Excel.</span><span class="sxs-lookup"><span data-stu-id="e6589-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="e6589-129">**stratégies de Ranger toocreate**</span><span class="sxs-lookup"><span data-stu-id="e6589-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="e6589-130">Ouvrez l’interface utilisateur Ranger.</span><span class="sxs-lookup"><span data-stu-id="e6589-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="e6589-131">Consultez [tooApache Ranger l’interface utilisateur de connexion](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="e6589-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="e6589-132">Cliquez sur **&lt;ClusterName>_hive** sous **Hive**.</span><span class="sxs-lookup"><span data-stu-id="e6589-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="e6589-133">Deux stratégies préconfigurées doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="e6589-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="e6589-134">Cliquez sur **ajouter une nouvelle stratégie**, puis entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6589-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="e6589-135">Nom de la stratégie : read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="e6589-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="e6589-136">Base de données Hive : par défaut</span><span class="sxs-lookup"><span data-stu-id="e6589-136">Hive Database: default</span></span>
   * <span data-ttu-id="e6589-137">table : hivesampletable</span><span class="sxs-lookup"><span data-stu-id="e6589-137">table: hivesampletable</span></span>
   * <span data-ttu-id="e6589-138">Colonne Hive : *</span><span class="sxs-lookup"><span data-stu-id="e6589-138">Hive column: *</span></span>
   * <span data-ttu-id="e6589-139">Sélectionner un utilisateur : hiveuser1</span><span class="sxs-lookup"><span data-stu-id="e6589-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="e6589-140">Autorisations : select</span><span class="sxs-lookup"><span data-stu-id="e6589-140">Permissions: select</span></span>

     ![Configuration de stratégie Hive pour Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="e6589-142">.</span><span class="sxs-lookup"><span data-stu-id="e6589-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e6589-143">Si un utilisateur de domaine n’est pas rempli dans Sélectionner un utilisateur, attendez quelques instants pour Ranger les toosync avec AAD.</span><span class="sxs-lookup"><span data-stu-id="e6589-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="e6589-144">Cliquez sur **ajouter** stratégie de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e6589-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="e6589-145">Répétez hello deux dernières étapes toocreate une autre stratégie avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6589-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="e6589-146">Nom de la stratégie : read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="e6589-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="e6589-147">Base de données Hive : par défaut</span><span class="sxs-lookup"><span data-stu-id="e6589-147">Hive Database: default</span></span>
   * <span data-ttu-id="e6589-148">table : hivesampletable</span><span class="sxs-lookup"><span data-stu-id="e6589-148">table: hivesampletable</span></span>
   * <span data-ttu-id="e6589-149">Colonne Hive : clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="e6589-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="e6589-150">Sélectionner un utilisateur : hiveuser2</span><span class="sxs-lookup"><span data-stu-id="e6589-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="e6589-151">Autorisations : select</span><span class="sxs-lookup"><span data-stu-id="e6589-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="e6589-152">Création d’une source de données ODBC Hive</span><span class="sxs-lookup"><span data-stu-id="e6589-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="e6589-153">Vous trouverez des instructions Hello dans [source de données ODBC de la ruche créer](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="e6589-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="e6589-154">Propriété</span><span class="sxs-lookup"><span data-stu-id="e6589-154">Property</span></span>|<span data-ttu-id="e6589-155">Description</span><span class="sxs-lookup"><span data-stu-id="e6589-155">Description</span></span>
    ---|---
    <span data-ttu-id="e6589-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="e6589-156">Data Source Name</span></span>|<span data-ttu-id="e6589-157">Donner à une source de données tooyour nom</span><span class="sxs-lookup"><span data-stu-id="e6589-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="e6589-158">Host</span><span class="sxs-lookup"><span data-stu-id="e6589-158">Host</span></span>|<span data-ttu-id="e6589-159">Entrez &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e6589-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="e6589-160">Par exemple, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="e6589-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="e6589-161">Port</span><span class="sxs-lookup"><span data-stu-id="e6589-161">Port</span></span>|<span data-ttu-id="e6589-162">Utilisez <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="e6589-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="e6589-163">(Ce port a été modifié à partir de too443 563.)</span><span class="sxs-lookup"><span data-stu-id="e6589-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="e6589-164">Base de données</span><span class="sxs-lookup"><span data-stu-id="e6589-164">Database</span></span>|<span data-ttu-id="e6589-165">Utilisez <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="e6589-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="e6589-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="e6589-166">Hive Server Type</span></span>|<span data-ttu-id="e6589-167">Sélectionnez <strong>Hive Server 2</strong>.</span><span class="sxs-lookup"><span data-stu-id="e6589-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="e6589-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="e6589-168">Mechanism</span></span>|<span data-ttu-id="e6589-169">Sélectionnez <strong>Azure HDInsight Service</strong>.</span><span class="sxs-lookup"><span data-stu-id="e6589-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="e6589-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="e6589-170">HTTP Path</span></span>|<span data-ttu-id="e6589-171">Laissez cette valeur vide.</span><span class="sxs-lookup"><span data-stu-id="e6589-171">Leave it blank.</span></span>
    <span data-ttu-id="e6589-172">User Name</span><span class="sxs-lookup"><span data-stu-id="e6589-172">User Name</span></span>|<span data-ttu-id="e6589-173">Entrez hiveuser1@contoso158.onmicrosoft.com. Mettre à jour de nom de domaine hello s’il est différent.</span><span class="sxs-lookup"><span data-stu-id="e6589-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="e6589-174">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="e6589-174">Password</span></span>|<span data-ttu-id="e6589-175">Entrez le mot de passe hello pour hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="e6589-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="e6589-176">Assurez-vous que tooclick **Test** avant d’enregistrer la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="e6589-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="e6589-177">Importation de données dans Microsoft Excel à partir de HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6589-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="e6589-178">Dans la dernière section de hello, vous avez configuré deux stratégies.</span><span class="sxs-lookup"><span data-stu-id="e6589-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="e6589-179">hiveuser1 a hello l’autorisation select sur toutes les colonnes hello et hiveuser2 a hello l’autorisation select sur deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="e6589-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="e6589-180">Dans cette section, vous empruntez l’identité hello deux utilisateurs tooimport des données dans Excel.</span><span class="sxs-lookup"><span data-stu-id="e6589-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="e6589-181">Ouvrez un nouveau classeur ou un classeur existant dans Excel.</span><span class="sxs-lookup"><span data-stu-id="e6589-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="e6589-182">À partir de hello **données** , cliquez sur **d’autres Sources de données**, puis cliquez sur **à partir de l’Assistant de connexion données** toolaunch hello **Assistant de connexion de données**.</span><span class="sxs-lookup"><span data-stu-id="e6589-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="e6589-183">![Assistant Ouvrir la connexion de données][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="e6589-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="e6589-184">Sélectionnez **DSN ODBC** comme source de données hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e6589-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="e6589-185">À partir de sources de données ODBC, sélectionnez hello source de données nom que vous avez créé à l’étape précédente de hello et puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e6589-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="e6589-186">Nouveau mot de passe hello pour cluster hello dans l’Assistant de hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6589-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="e6589-187">Attendez que hello **sélectionner une base de données et de Table** tooopen de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e6589-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="e6589-188">Cette opération peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e6589-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="e6589-189">Sélectionnez **hivesampletable**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e6589-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="e6589-190">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e6589-190">Click **Finish**.</span></span>
8. <span data-ttu-id="e6589-191">Bonjour **importer des données** boîte de dialogue, vous pouvez modifier ou spécifier la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="e6589-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="e6589-192">toodo, cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="e6589-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="e6589-193">Cette opération peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e6589-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="e6589-194">Cliquez sur hello **définition** est du texte de la commande hello onglet :</span><span class="sxs-lookup"><span data-stu-id="e6589-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="e6589-195">Par des stratégies de Ranger hello que vous définies, hiveuser1 a l’autorisation select sur toutes les colonnes hello.</span><span class="sxs-lookup"><span data-stu-id="e6589-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="e6589-196">Par conséquent, cette requête fonctionne avec les informations d’identification de hiveuser1, mais cette requête ne fonctionne pas avec les informations d’identification de hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="e6589-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="e6589-197">![Propriétés de connexion][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="e6589-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="e6589-198">Cliquez sur **OK** boîte de dialogue Propriétés de connexion tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="e6589-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="e6589-199">Cliquez sur **OK** tooclose hello **importer des données** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e6589-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="e6589-200">Entrez à nouveau le mot de passe hello hiveuser1, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6589-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="e6589-201">Il prend quelques secondes avant de données obtient tooExcel importé.</span><span class="sxs-lookup"><span data-stu-id="e6589-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="e6589-202">Une fois terminé, 11 colonnes de données doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="e6589-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="e6589-203">stratégie de deuxième tootest hello (en lecture-hivesampletable-devicemake) que vous avez créé dans la dernière section de hello</span><span class="sxs-lookup"><span data-stu-id="e6589-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="e6589-204">Ajoutez une nouvelle feuille dans Excel.</span><span class="sxs-lookup"><span data-stu-id="e6589-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="e6589-205">Suivez la dernière procédure tooimport hello les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="e6589-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="e6589-206">Hello seul changement que vous prendrez est informations d’identification de toouse hiveuser2 au lieu de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="e6589-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="e6589-207">Cela échoue car hiveuser2 a seulement deux colonnes de toosee d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e6589-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="e6589-208">Vous obtiendra hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="e6589-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="e6589-209">Suivez hello même données tooimport de procédure.</span><span class="sxs-lookup"><span data-stu-id="e6589-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="e6589-210">Cette fois-ci, utilisez les informations d’identification de hiveuser2 et également modifier instruction select de hello from :</span><span class="sxs-lookup"><span data-stu-id="e6589-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="e6589-211">to:</span><span class="sxs-lookup"><span data-stu-id="e6589-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="e6589-212">Une fois terminé, deux colonnes de données importées doivent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="e6589-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6589-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6589-213">Next steps</span></span>
* <span data-ttu-id="e6589-214">Pour configurer un cluster HDInsight joint à un domaine, consultez [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e6589-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="e6589-215">Pour gérer un cluster HDInsight joint à un domaine, consultez [Gestion de clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e6589-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="e6589-216">Pour exécuter des requêtes Hive en utilisant SSH sur des clusters HDInsight joints au domaine, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="e6589-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="e6589-217">Pour la connexion de la ruche à l’aide de la ruche de JDBC, consultez [connecter tooHive sur Azure HDInsight à l’aide du pilote JDBC de la ruche de hello](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="e6589-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="e6589-218">Pour la connexion tooHadoop Excel à l’aide de la ruche de ODBC, consultez [tooHadoop connexion Excel avec hello pilote ODBC de la ruche de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="e6589-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="e6589-219">Pour la connexion tooHadoop Excel à l’aide de Power Query, consultez [tooHadoop Excel de se connecter à l’aide de Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="e6589-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
