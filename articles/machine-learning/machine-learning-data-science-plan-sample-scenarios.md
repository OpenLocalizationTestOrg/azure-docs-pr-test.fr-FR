---
title: "Identifier des scénarios d’analyses avancées pour Azure Machine Learning | Microsoft Docs"
description: "Sélectionnez les scénarios appropriés pour l’analyse prédictive avancée à l’aide du processus TDSP (Team Data Science Process)."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="5a182-103">Scénarios d’analyses avancées dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a182-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="5a182-104">Cet article présente les divers exemples de sources de données et les scénarios cibles qui peuvent être gérés par le processus [TDSP (Team Data Science Process)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a182-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="5a182-105">Le processus TDSP fournit une approche systématique permettant aux équipes de collaborer à la création d’applications intelligentes.</span><span class="sxs-lookup"><span data-stu-id="5a182-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="5a182-106">Les scénarios présentés ici illustrent les options disponibles dans le flux de travail de traitement basées sur les caractéristiques des données, les emplacements sources et les référentiels cibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="5a182-107">L’ **arbre de décision** qui permet de sélectionner les exemples de scénarios qui conviennent dans le cas de vos données et objectifs est présenté à la dernière section.</span><span class="sxs-lookup"><span data-stu-id="5a182-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="5a182-108">Les sections suivantes présentent quelques exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="5a182-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="5a182-109">Pour chaque scénario, un flux possible de science des données ou d’analyse avancée et les ressources Azure connexes sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="5a182-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="5a182-110">**Pour tous les scénarios suivants, vous devez:**
> </span><span class="sxs-lookup"><span data-stu-id="5a182-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="5a182-111">[Créer un compte de stockage](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="5a182-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="5a182-112">Création d’un espace de travail Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a182-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="5a182-113"><a name="smalllocal"></a>Scénario \#1 : jeu de données tabulaires petit à moyen dans des fichiers locaux</span><span class="sxs-lookup"><span data-stu-id="5a182-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Fichiers locaux petits à moyens][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="5a182-115">Autres ressources Azure : aucune</span><span class="sxs-lookup"><span data-stu-id="5a182-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="5a182-116">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="5a182-117">Téléchargez un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="5a182-117">Upload a dataset.</span></span>
3. <span data-ttu-id="5a182-118">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux téléchargés.</span><span class="sxs-lookup"><span data-stu-id="5a182-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="5a182-119"><a name="smalllocalprocess"></a>Scénario \#2 : jeu de données petit à moyen de fichiers locaux nécessitant un traitement</span><span class="sxs-lookup"><span data-stu-id="5a182-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Fichiers locaux petits à moyens avec traitement][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5a182-121">Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-122">Créez une machine virtuelle Azure exécutant IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="5a182-123">Téléchargez des données vers un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="5a182-124">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données à partir du conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="5a182-125">Transformez les données sous forme de tableau nettoyé.</span><span class="sxs-lookup"><span data-stu-id="5a182-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="5a182-126">Enregistrez les données transformées dans des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="5a182-127">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="5a182-128">Lisez les données des objets blob Azure à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="5a182-129">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="5a182-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5a182-130"><a name="largelocal"></a>Scénario \#3 : jeu de données volumineux de fichiers locaux, ciblant des objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Fichiers locaux volumineux][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5a182-132">Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-133">Créez une machine virtuelle Azure exécutant IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="5a182-134">Téléchargez des données vers un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="5a182-135">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="5a182-136">Le cas échéant, transformez les données sous forme de tableau nettoyé.</span><span class="sxs-lookup"><span data-stu-id="5a182-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="5a182-137">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5a182-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="5a182-138">Extrayez un échantillon de données petit à moyen.</span><span class="sxs-lookup"><span data-stu-id="5a182-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="5a182-139">Enregistrez les données échantillonnées dans des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="5a182-140">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="5a182-141">Lisez les données des objets blob Azure à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="5a182-142">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="5a182-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5a182-143"><a name="smalllocaltodb"></a>Scénario \#4 : jeu de données petit à moyen de fichiers locaux, ciblant SQL Server dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Fichiers locaux petits à moyens vers une base de données SQL dans Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5a182-145">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-146">Créez une Machine virtuelle Azure exécutant SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="5a182-147">Téléchargez des données vers un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="5a182-148">Pré-traitez et nettoyez les données dans un conteneur de stockage Azure à l’aide d’IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="5a182-149">Le cas échéant, transformez les données sous forme de tableau nettoyé.</span><span class="sxs-lookup"><span data-stu-id="5a182-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="5a182-150">Enregistrez les données dans des fichiers locaux de la machine virtuelle (IPython Notebook est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence aux lecteurs de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="5a182-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="5a182-151">Chargez des données dans la base de données SQL Server s’exécutant sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="5a182-152">Option \#1 : utilisation de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5a182-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="5a182-153">Vous connecter à la machine virtuelle SQL Server</span><span class="sxs-lookup"><span data-stu-id="5a182-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="5a182-154">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5a182-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="5a182-155">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="5a182-155">Create database and target tables.</span></span>
   * <span data-ttu-id="5a182-156">Utilisez une des méthodes d’importation en bloc pour charger les données à partir des fichiers locaux de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a182-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="5a182-157">Option \#2 : utilisation d’IPython Notebook – déconseillé pour les jeux de données de tailles moyenne et supérieure</span><span class="sxs-lookup"><span data-stu-id="5a182-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="5a182-158">Utilisez la chaîne de connexion ODBC pour accéder à SQL Server sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a182-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="5a182-159">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="5a182-159">Create database and target tables.</span></span>
   * <span data-ttu-id="5a182-160">Utilisez une des méthodes d’importation en bloc pour charger les données à partir des fichiers locaux de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a182-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="5a182-161">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5a182-161">Explore data, create features as needed.</span></span> <span data-ttu-id="5a182-162">Notez que les fonctionnalités ne doivent pas être matérialisées dans les tables de base de données.</span><span class="sxs-lookup"><span data-stu-id="5a182-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="5a182-163">Notez seulement la requête nécessaire pour les créer.</span><span class="sxs-lookup"><span data-stu-id="5a182-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="5a182-164">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="5a182-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="5a182-165">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="5a182-166">Lisez les données directement à partir de SQL Server à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="5a182-167">Collez la requête nécessaire qui extrait les champs, crée les fonctionnalités et échantillonne les données, le cas échéant, directement dans la requête [Import Data][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="5a182-168">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="5a182-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5a182-169"><a name="largelocaltodb"></a>Scénario \#5 : jeu de données volumineux dans des fichiers locaux, ciblant SQL Server dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Fichiers locaux volumineux vers une base de données SQL dans Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5a182-171">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-172">Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="5a182-173">Téléchargez des données vers un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="5a182-174">(Facultatif) Pré-traitez et nettoyez les données.</span><span class="sxs-lookup"><span data-stu-id="5a182-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="5a182-175">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-175">a.</span></span>  <span data-ttu-id="5a182-176">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="5a182-177">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-177">b.</span></span>  <span data-ttu-id="5a182-178">Le cas échéant, transformez les données sous forme de tableau nettoyé.</span><span class="sxs-lookup"><span data-stu-id="5a182-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="5a182-179">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-179">c.</span></span>  <span data-ttu-id="5a182-180">Enregistrez les données dans des fichiers locaux de la machine virtuelle (IPython Notebook est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence aux lecteurs de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="5a182-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="5a182-181">Chargez des données dans la base de données SQL Server s’exécutant sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="5a182-182">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-182">a.</span></span>  <span data-ttu-id="5a182-183">Connectez-vous à la machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a182-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="5a182-184">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-184">b.</span></span>  <span data-ttu-id="5a182-185">Si les données ne sont pas déjà enregistrées, téléchargez les fichiers de données à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="5a182-186">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-186">c.</span></span>  <span data-ttu-id="5a182-187">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5a182-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="5a182-188">d.</span><span class="sxs-lookup"><span data-stu-id="5a182-188">d.</span></span>  <span data-ttu-id="5a182-189">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="5a182-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="5a182-190">e.</span><span class="sxs-lookup"><span data-stu-id="5a182-190">e.</span></span>  <span data-ttu-id="5a182-191">Utilisez l’une des méthodes d’importation en bloc pour charger les données.</span><span class="sxs-lookup"><span data-stu-id="5a182-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="5a182-192">f.</span><span class="sxs-lookup"><span data-stu-id="5a182-192">f.</span></span>  <span data-ttu-id="5a182-193">Si les jointures de table sont nécessaires, créez des index pour accélérer les jointures.</span><span class="sxs-lookup"><span data-stu-id="5a182-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a182-194">Pour accélérer le chargement des formats de données volumineux, il est recommandé de créer des tables partitionnées et d’importer en bloc les données en parallèle.</span><span class="sxs-lookup"><span data-stu-id="5a182-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="5a182-195">Pour plus d’informations, consultez la rubrique [Importation de données en parallèle dans des tables partitionnées SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5a182-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5a182-196">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5a182-196">Explore data, create features as needed.</span></span> <span data-ttu-id="5a182-197">Notez que les fonctionnalités ne doivent pas être matérialisées dans les tables de base de données.</span><span class="sxs-lookup"><span data-stu-id="5a182-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="5a182-198">Notez seulement la requête nécessaire pour les créer.</span><span class="sxs-lookup"><span data-stu-id="5a182-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="5a182-199">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="5a182-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="5a182-200">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="5a182-201">Lisez les données directement à partir de SQL Server à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="5a182-202">Collez la requête nécessaire qui extrait les champs, crée les fonctionnalités et échantillonne les données, le cas échéant, directement dans la requête [Import Data][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="5a182-203">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé</span><span class="sxs-lookup"><span data-stu-id="5a182-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="5a182-204"><a name="largedbtodb"></a>Scénario \#6 : jeu de données volumineux dans une base de données SQL Server locale, ciblant SQL Server dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Base de données SQL volumineuse sur site vers une base de données SQL dans Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5a182-206">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-207">Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="5a182-208">Utilisez l’une des méthodes d’exportation des données pour exporter les données à partir de SQL Server vers des fichiers de vidage.</span><span class="sxs-lookup"><span data-stu-id="5a182-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a182-209">Si vous décidez de déplacer toutes les données à partir de la base de données locale, il existe une autre méthode (plus rapide) pour déplacer la base de données entière vers l’instance SQL Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="5a182-210">Ignorez les étapes d’exportation des données, de création de la base de données et de chargement/importation des données dans la base de données cible, et suivez l’autre méthode.</span><span class="sxs-lookup"><span data-stu-id="5a182-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="5a182-211">Téléchargez les fichiers de vidage vers le conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="5a182-212">Chargez les données dans une base de données SQL Server sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="5a182-213">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-213">a.</span></span>  <span data-ttu-id="5a182-214">Connectez-vous à la machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a182-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="5a182-215">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-215">b.</span></span>  <span data-ttu-id="5a182-216">Téléchargez les fichiers de données à partir d’un conteneur de stockage Azure vers le dossier de machine virtuelle local.</span><span class="sxs-lookup"><span data-stu-id="5a182-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="5a182-217">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-217">c.</span></span>  <span data-ttu-id="5a182-218">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5a182-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="5a182-219">d.</span><span class="sxs-lookup"><span data-stu-id="5a182-219">d.</span></span>  <span data-ttu-id="5a182-220">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="5a182-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="5a182-221">e.</span><span class="sxs-lookup"><span data-stu-id="5a182-221">e.</span></span>  <span data-ttu-id="5a182-222">Utilisez l’une des méthodes d’importation en bloc pour charger les données.</span><span class="sxs-lookup"><span data-stu-id="5a182-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="5a182-223">f.</span><span class="sxs-lookup"><span data-stu-id="5a182-223">f.</span></span>  <span data-ttu-id="5a182-224">Si les jointures de table sont nécessaires, créez des index pour accélérer les jointures.</span><span class="sxs-lookup"><span data-stu-id="5a182-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a182-225">Pour accélérer le chargement des formats de données volumineux, créez des tables partitionnées et importez en bloc les données en parallèle.</span><span class="sxs-lookup"><span data-stu-id="5a182-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="5a182-226">Pour plus d’informations, consultez la rubrique [Importation de données en parallèle dans des tables partitionnées SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5a182-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5a182-227">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5a182-227">Explore data, create features as needed.</span></span> <span data-ttu-id="5a182-228">Notez que les fonctionnalités ne doivent pas être matérialisées dans les tables de base de données.</span><span class="sxs-lookup"><span data-stu-id="5a182-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="5a182-229">Notez seulement la requête nécessaire pour les créer.</span><span class="sxs-lookup"><span data-stu-id="5a182-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="5a182-230">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="5a182-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="5a182-231">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="5a182-232">Lisez les données directement à partir de SQL Server à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="5a182-233">Collez la requête nécessaire qui extrait les champs, crée les fonctionnalités et échantillonne les données, le cas échéant, directement dans la requête [Import Data][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="5a182-234">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.</span><span class="sxs-lookup"><span data-stu-id="5a182-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="5a182-235">Autre méthode pour copier une base de données complète à partir d’un serveur SQL local vers une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5a182-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Détacher la base de données locale et l’attacher à la base de données SQL dans Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5a182-237">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="5a182-238">Pour répliquer l’ensemble de la base de données SQL Server dans votre machine virtuelle SQL Server, vous devez copier une base de données à partir d’un emplacement/serveur vers un autre, en supposant que la base de données puisse être mise temporairement hors connexion.</span><span class="sxs-lookup"><span data-stu-id="5a182-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="5a182-239">Pour cela, utilisez l’Explorateur d’objets SQL Server Management Studio ou les commandes Transact-SQL équivalentes.</span><span class="sxs-lookup"><span data-stu-id="5a182-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="5a182-240">Détachez la base de données à l’emplacement source.</span><span class="sxs-lookup"><span data-stu-id="5a182-240">Detach the database at the source location.</span></span> <span data-ttu-id="5a182-241">Pour plus d’informations, consultez la rubrique [Détacher une base de données](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5a182-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="5a182-242">Dans l’Explorateur Windows ou l’invite de commandes Windows, copiez les fichiers de la base de données détachée et les fichiers journaux à l’emplacement cible sur la machine virtuelle SQL Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="5a182-243">Attachez les fichiers copiés à l’instance SQL Server cible.</span><span class="sxs-lookup"><span data-stu-id="5a182-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="5a182-244">Pour plus d’informations, consultez la rubrique [Attacher une base de données](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5a182-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="5a182-245">[Déplacer une base de données à l’aide de la méthode de détachement et d’attachement (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="5a182-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="5a182-246"><a name="largedbtohive"></a>Scénario \#7 : données volumineuses (« Big Data ») dans des fichiers locaux, ciblant une base de données Hive dans des clusters Hadoop Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a182-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Données volumineuses (« Big Data ») dans la base de données Hive cible locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5a182-248">Autres ressources Azure : cluster Hadoop Azure HDInsight et machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5a182-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5a182-249">Créez une machine virtuelle Azure exécutant le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5a182-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="5a182-250">Créez un cluster Hadoop Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a182-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="5a182-251">(Facultatif) Pré-traitez et nettoyez les données.</span><span class="sxs-lookup"><span data-stu-id="5a182-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="5a182-252">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-252">a.</span></span>  <span data-ttu-id="5a182-253">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a182-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="5a182-254">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-254">b.</span></span>  <span data-ttu-id="5a182-255">Le cas échéant, transformez les données sous forme de tableau nettoyé.</span><span class="sxs-lookup"><span data-stu-id="5a182-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="5a182-256">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-256">c.</span></span>  <span data-ttu-id="5a182-257">Enregistrez les données dans des fichiers locaux de la machine virtuelle (IPython Notebook est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence aux lecteurs de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="5a182-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="5a182-258">Téléchargez des données vers le conteneur par défaut du cluster Hadoop sélectionné à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="5a182-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="5a182-259">Chargez des données dans la base de données Hive du cluster Hadoop Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a182-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="5a182-260">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-260">a.</span></span>  <span data-ttu-id="5a182-261">Connectez-vous au nœud principal du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="5a182-262">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-262">b.</span></span>  <span data-ttu-id="5a182-263">Ouvrez la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5a182-264">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-264">c.</span></span>  <span data-ttu-id="5a182-265">Entrez le répertoire racine Hive en utilisant la commande `cd %hive_home%\bin` sur la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5a182-266">d.</span><span class="sxs-lookup"><span data-stu-id="5a182-266">d.</span></span>  <span data-ttu-id="5a182-267">Exécutez les requêtes Hive pour créer la base de données et les tables, puis chargez des données depuis le stockage d’objets blob vers des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="5a182-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a182-268">Si les données sont volumineuses, les utilisateurs peuvent créer la table Hive avec des partitions.</span><span class="sxs-lookup"><span data-stu-id="5a182-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="5a182-269">Ils peuvent ensuite utiliser une boucle `for` dans la ligne de commande Hadoop sur le nœud principal pour charger les données dans la table Hive une partition à la fois.</span><span class="sxs-lookup"><span data-stu-id="5a182-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="5a182-270">Le cas échéant, explorez des données et créez des fonctionnalités dans la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="5a182-271">Notez que les fonctionnalités ne doivent pas être matérialisées dans les tables de base de données.</span><span class="sxs-lookup"><span data-stu-id="5a182-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="5a182-272">Notez seulement la requête nécessaire pour les créer.</span><span class="sxs-lookup"><span data-stu-id="5a182-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="5a182-273">a.</span><span class="sxs-lookup"><span data-stu-id="5a182-273">a.</span></span>  <span data-ttu-id="5a182-274">Connectez-vous au nœud principal du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="5a182-275">b.</span><span class="sxs-lookup"><span data-stu-id="5a182-275">b.</span></span>  <span data-ttu-id="5a182-276">Ouvrez la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5a182-277">c.</span><span class="sxs-lookup"><span data-stu-id="5a182-277">c.</span></span>  <span data-ttu-id="5a182-278">Entrez le répertoire racine Hive en utilisant la commande `cd %hive_home%\bin` sur la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5a182-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5a182-279">d.</span><span class="sxs-lookup"><span data-stu-id="5a182-279">d.</span></span>  <span data-ttu-id="5a182-280">Exécutez les requêtes Hive sur la ligne de commande Hadoop sur le nœud principal du cluster Hadoop pour explorer les données et créer des fonctionnalités en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="5a182-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="5a182-281">Si nécessaire et/ou souhaité, échantillonnez les données pour les adapter à Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a182-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="5a182-282">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5a182-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="5a182-283">Lisez les données directement à partir de `Hive Queries` à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="5a182-284">Collez la requête nécessaire qui extrait les champs, crée les fonctionnalités et échantillonne les données, le cas échéant, directement dans la requête [Import Data][import-data].</span><span class="sxs-lookup"><span data-stu-id="5a182-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="5a182-285">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.</span><span class="sxs-lookup"><span data-stu-id="5a182-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="5a182-286"><a name="decisiontree"></a>Arbre de décision pour le choix du scénario</span><span class="sxs-lookup"><span data-stu-id="5a182-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="5a182-287">Le schéma suivant résume les scénarios décrits ci-dessus et les processus de science des données ainsi que les choix technologiques effectués qui vous guident vers chacun des scénarios détaillés.</span><span class="sxs-lookup"><span data-stu-id="5a182-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="5a182-288">Notez que le traitement des données, l’exploration, la conception de fonctionnalités et l’échantillonnage peuvent survenir dans un(e) ou plusieurs méthodes/environnements (dans l’environnement source, l’environnement intermédiaire et/ou l’environnement cible) et peuvent s’effectuer de manière itérative en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="5a182-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="5a182-289">Le schéma illustre uniquement les flux possibles et ne fournit pas d’énumération exhaustive.</span><span class="sxs-lookup"><span data-stu-id="5a182-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Exemples de scénarios de procédure pas à pas pour le processus DS][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="5a182-291">Analyse avancée en action, exemples</span><span class="sxs-lookup"><span data-stu-id="5a182-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="5a182-292">Pour connaître les procédures pas à pas de bout en bout pour Azure Machine Learning qui utilisent le processus et la technologie d’analyse avancée à l’aide de jeux de données publics, consultez :</span><span class="sxs-lookup"><span data-stu-id="5a182-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="5a182-293">[Processus TDSP (Team Data Science Process) en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5a182-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="5a182-294">[Processus TDSP (Team Data Science Process) en action : utilisation de clusters Hadoop HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5a182-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
