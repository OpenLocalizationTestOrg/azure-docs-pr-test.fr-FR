---
title: "Connecter Excel à Hadoop à l’aide du pilote ODBC Hive - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment configurer et utiliser le pilote ODBC Microsoft Hive pour Excel afin d’interroger des données dans des clusters HDInsight à partir de Microsoft Excel."
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="af96f-104">Connecter Excel à Hadoop dans Azure HDInsight avec le pilote ODBC Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="af96f-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="af96f-105">La solution de données volumineuses de Microsoft intègre des composants BI (Business Intelligence) à des clusters Apache Hadoop qui ont été déployés par Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af96f-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="af96f-106">Un exemple de cette intégration est la possibilité de connecter Excel à l’entrepôt de données Hive d’un cluster Hadoop dans HDInsight au moyen du pilote Open Database Connectivity (ODBC) Microsoft Hive.</span><span class="sxs-lookup"><span data-stu-id="af96f-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="af96f-107">Il est également possible de connecter les données associées à un cluster HDInsight et d'autres sources de données, y compris d'autres clusters Hadoop (non HDInsight), à partir d'Excel au moyen du complément Microsoft Power Query pour Excel.</span><span class="sxs-lookup"><span data-stu-id="af96f-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="af96f-108">Pour plus d’informations sur l’installation et l’utilisation de Power Query, consultez [Connexion d’Excel à HDInsight à l’aide de Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="af96f-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="af96f-109">Même si les étapes décrites dans cet article peuvent être utilisées avec un cluster HDInsight basé sur Linux ou Windows, Windows est requis pour le poste de travail client.</span><span class="sxs-lookup"><span data-stu-id="af96f-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="af96f-110">**Conditions préalables**:</span><span class="sxs-lookup"><span data-stu-id="af96f-110">**Prerequisites**:</span></span>

<span data-ttu-id="af96f-111">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="af96f-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="af96f-112">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="af96f-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="af96f-113">Pour en créer un, consultez [Prise en main d’Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="af96f-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="af96f-114">**Une station de travail** avec Office Professionnel Plus 2013, Office 365 ProPlus, l'édition autonome d'Excel 2013 ou Office Professionnel Plus 2010.</span><span class="sxs-lookup"><span data-stu-id="af96f-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="af96f-115">Installation du pilote ODBC Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="af96f-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="af96f-116">Téléchargez et installez le pilote ODBC Microsoft Hive à partir du [Centre de téléchargement][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="af96f-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="af96f-117">Ce pilote peut être installé sur les versions 32 bits ou 64 bits de Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 et Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="af96f-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="af96f-118">Le pilote autorise la connexion à Azure HDInsight (versions 1.6 et ultérieures) et à Azure HDInsight Emulator (v.1.0.0.0 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="af96f-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="af96f-119">Vous allez installer la version correspondant à celle de l’application dans laquelle vous utilisez le pilote ODBC.</span><span class="sxs-lookup"><span data-stu-id="af96f-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="af96f-120">Pour les besoins de ce didacticiel, le pilote utilisé est celui d’Office Excel.</span><span class="sxs-lookup"><span data-stu-id="af96f-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="af96f-121">Création d’une source de données ODBC Hive</span><span class="sxs-lookup"><span data-stu-id="af96f-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="af96f-122">La procédure suivante explique comment créer une source de données ODBC Hive.</span><span class="sxs-lookup"><span data-stu-id="af96f-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="af96f-123">Sur Windows 8 ou Windows 10, appuyez sur la touche Windows pour ouvrir l’écran d’accueil, puis tapez **sources de données**.</span><span class="sxs-lookup"><span data-stu-id="af96f-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="af96f-124">Cliquez sur **Configurer les sources de données ODBC (32 bits)** ou **Configurer les sources de données ODBC (64 bits)** selon votre version d'Office.</span><span class="sxs-lookup"><span data-stu-id="af96f-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="af96f-125">Si vous utilisez Windows 7, choisissez **Sources de données ODBC (32 bits)** ou **Sources de données ODBC (64 bits)** dans **Outils d'administration**.</span><span class="sxs-lookup"><span data-stu-id="af96f-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="af96f-126">La boîte de dialogue **Administrateur de sources de données ODBC** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="af96f-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="af96f-127">![Administrateur de sources de données ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurer un DSN à l’aide de l’Administrateur de sources de données ODBC")</span><span class="sxs-lookup"><span data-stu-id="af96f-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="af96f-128">Dans DNS Utilisateur, cliquez sur **Ajouter** pour ouvrir l'Assistant **Créer une nouvelle source de données**.</span><span class="sxs-lookup"><span data-stu-id="af96f-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="af96f-129">Sélectionnez **Microsoft Hive ODBC Driver**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="af96f-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="af96f-130">La boîte de dialogue de **configuration de DNS de pilote ODBC Microsoft Hive** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="af96f-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="af96f-131">Tapez ou sélectionnez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="af96f-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="af96f-132">Propriété</span><span class="sxs-lookup"><span data-stu-id="af96f-132">Property</span></span> | <span data-ttu-id="af96f-133">Description</span><span class="sxs-lookup"><span data-stu-id="af96f-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="af96f-134">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="af96f-134">Data Source Name</span></span> |<span data-ttu-id="af96f-135">Donnez un nom à votre source de données</span><span class="sxs-lookup"><span data-stu-id="af96f-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="af96f-136">Host</span><span class="sxs-lookup"><span data-stu-id="af96f-136">Host</span></span> |<span data-ttu-id="af96f-137">Entrez &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="af96f-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="af96f-138">Par exemple, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="af96f-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="af96f-139">Port</span><span class="sxs-lookup"><span data-stu-id="af96f-139">Port</span></span> |<span data-ttu-id="af96f-140">Utilisez <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="af96f-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="af96f-141">(ce port est passé de 563 à 443).</span><span class="sxs-lookup"><span data-stu-id="af96f-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="af96f-142">Base de données</span><span class="sxs-lookup"><span data-stu-id="af96f-142">Database</span></span> |<span data-ttu-id="af96f-143">Utilisez <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="af96f-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="af96f-144">Mechanism</span><span class="sxs-lookup"><span data-stu-id="af96f-144">Mechanism</span></span> |<span data-ttu-id="af96f-145">Sélectionnez <strong>Azure HDInsight Service</strong>.</span><span class="sxs-lookup"><span data-stu-id="af96f-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="af96f-146">User Name</span><span class="sxs-lookup"><span data-stu-id="af96f-146">User Name</span></span> |<span data-ttu-id="af96f-147">Entrez le nom de l’utilisateur HTTP du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af96f-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="af96f-148">Le nom d’utilisateur par défaut est <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="af96f-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="af96f-149">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="af96f-149">Password</span></span> |<span data-ttu-id="af96f-150">Entrez le mot de passe du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af96f-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="af96f-151">Certains paramètres importants sont à prendre en compte lorsque vous cliquez sur **Options avancées**:</span><span class="sxs-lookup"><span data-stu-id="af96f-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="af96f-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="af96f-152">Parameter</span></span> | <span data-ttu-id="af96f-153">Description</span><span class="sxs-lookup"><span data-stu-id="af96f-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="af96f-154">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="af96f-154">Use Native Query</span></span> |<span data-ttu-id="af96f-155">Une fois sélectionné, le pilote ODBC ne tente PAS de convertir TSQL en HiveQL.</span><span class="sxs-lookup"><span data-stu-id="af96f-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="af96f-156">À utiliser uniquement si vous êtes sûr à 100 % que vous envoyez des instructions HiveQL pures.</span><span class="sxs-lookup"><span data-stu-id="af96f-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="af96f-157">Si vous effectuez une connexion à SQL Server ou Base de données SQL Azure, ne sélectionnez pas cette option.</span><span class="sxs-lookup"><span data-stu-id="af96f-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="af96f-158">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="af96f-158">Rows fetched per block</span></span> |<span data-ttu-id="af96f-159">Lors de l’extraction d’un grand nombre d’enregistrements, la définition de ce paramètre peut être nécessaire pour garantir des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="af96f-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="af96f-160">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="af96f-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="af96f-161">Les précisions et longueurs des types de données peuvent affecter la façon dont les données sont renvoyées.</span><span class="sxs-lookup"><span data-stu-id="af96f-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="af96f-162">Elles entraînent le renvoi d’informations incorrectes en raison d’une perte de précision et/ou de troncations.</span><span class="sxs-lookup"><span data-stu-id="af96f-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="af96f-163">![Options avancées](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Options avancées de configuration de DSN")</span><span class="sxs-lookup"><span data-stu-id="af96f-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="af96f-164">Cliquez sur **Tester** pour tester la source de données.</span><span class="sxs-lookup"><span data-stu-id="af96f-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="af96f-165">Une fois que la source de données est configurée correctement, le message suivant apparaît *TESTS COMPLETED SUCCESSFULLY!*.</span><span class="sxs-lookup"><span data-stu-id="af96f-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="af96f-166">Cliquez sur **OK** pour fermer la boîte de dialogue de test.</span><span class="sxs-lookup"><span data-stu-id="af96f-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="af96f-167">La nouvelle source de données doit apparaitre dans **l’administrateur des sources de données ODBC**.</span><span class="sxs-lookup"><span data-stu-id="af96f-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="af96f-168">Cliquez sur **OK** pour quitter l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="af96f-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="af96f-169">Importation de données dans Microsoft Excel à partir de HDInsight</span><span class="sxs-lookup"><span data-stu-id="af96f-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="af96f-170">Les étapes ci-dessous décrivent comment importer des données d’une table Hive dans un classeur Excel à l’aide de la source de données ODBC que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="af96f-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="af96f-171">Ouvrez un nouveau classeur ou un classeur existant dans Excel.</span><span class="sxs-lookup"><span data-stu-id="af96f-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="af96f-172">À partir de l’onglet **Données**, cliquez sur **Obtenir des données**, sur **Depuis d’autres sources** puis sur **Depuis ODBC** pour lancer **l’Assistant Connexion de données**.</span><span class="sxs-lookup"><span data-stu-id="af96f-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="af96f-173">![Assistant Ouvrir la connexion de données](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Assistant Ouvrir la connexion de données")</span><span class="sxs-lookup"><span data-stu-id="af96f-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="af96f-174">Sélectionnez le nom de la source de données que vous avez créé dans la dernière section, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af96f-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="af96f-175">Entrez le nom d’utilisateur Hadoop (le nom par défaut est admin) et le mot de passe, puis cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="af96f-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="af96f-176">Dans le navigateur, développez **HIVE**, développez **par défaut**, cliquez sur **hivesampletable**, puis cliquez sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="af96f-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="af96f-177">Patientez quelques secondes pour que les données soient importées dans Excel.</span><span class="sxs-lookup"><span data-stu-id="af96f-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="af96f-178">![Navigateur ODBC HDInsight Hive](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Assistant Ouvrir la connexion de données")</span><span class="sxs-lookup"><span data-stu-id="af96f-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="af96f-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af96f-179">Next steps</span></span>
<span data-ttu-id="af96f-180">Dans cet article, vous avez appris à utiliser le pilote ODBC Microsoft Hive pour extraire des données du service HDInsight dans Excel.</span><span class="sxs-lookup"><span data-stu-id="af96f-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="af96f-181">De la même façon, vous pouvez extraire les données du service HDInsight dans la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="af96f-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="af96f-182">Il est également possible de télécharger des données dans un service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af96f-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="af96f-183">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="af96f-183">To learn more, see:</span></span>

* <span data-ttu-id="af96f-184">[Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="af96f-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="af96f-185">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="af96f-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="af96f-186">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="af96f-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


