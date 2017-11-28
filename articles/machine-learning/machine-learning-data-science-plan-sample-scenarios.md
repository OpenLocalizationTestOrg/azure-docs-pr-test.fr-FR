---
title: "aaaIdentify avancée des scénarios d’analytique pour Azure Machine Learning | Documents Microsoft"
description: "Sélectionnez les scénarios appropriés de hello pour cette opération avancée analytique prédictive avec hello processus de science des données de Team."
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
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="018fa-103">Scénarios d’analyses avancées dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="018fa-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="018fa-104">Cet article présente plusieurs exemples de sources de données et les scénarios de cibles qui peuvent être gérés par hello hello [processus de science des données équipe (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="018fa-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="018fa-105">Hello TDSP fournit une approche systématique pour toocollaborate équipes sur la création d’applications intelligentes.</span><span class="sxs-lookup"><span data-stu-id="018fa-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="018fa-106">les scénarios de Hello présentées ici illustrent les options disponibles dans le flux de travail de traitement des données hello qui dépendent des caractéristiques des données hello, les emplacements source et les référentiels de cible dans Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="018fa-107">Hello **arbre de décision** pour les scénarios d’exemple hello qui convient à vos données et l’objectif de sélection est présentée dans la dernière section de hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="018fa-108">Chacun des hello les sections suivantes présente un exemple de scénario.</span><span class="sxs-lookup"><span data-stu-id="018fa-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="018fa-109">Pour chaque scénario, un flux possible de science des données ou d’analyse avancée et les ressources Azure connexes sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="018fa-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="018fa-110">**Pour tous les scénarios suivants de hello, vous devez :**
> </span><span class="sxs-lookup"><span data-stu-id="018fa-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="018fa-111">[Créer un compte de stockage](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="018fa-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="018fa-112">Création d’un espace de travail Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="018fa-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="018fa-113"><a name="smalllocal"></a>Scénario \#1 : toomedium petit jeu de données tabulaires dans des fichiers locaux</span><span class="sxs-lookup"><span data-stu-id="018fa-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Fichiers locaux toomedium petit][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="018fa-115">Autres ressources Azure : aucune</span><span class="sxs-lookup"><span data-stu-id="018fa-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="018fa-116">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="018fa-117">Téléchargez un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="018fa-117">Upload a dataset.</span></span>
3. <span data-ttu-id="018fa-118">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux téléchargés.</span><span class="sxs-lookup"><span data-stu-id="018fa-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="018fa-119"><a name="smalllocalprocess"></a>Scénario \#2 : toomedium petit jeu de données de fichiers locaux qui nécessitent un traitement</span><span class="sxs-lookup"><span data-stu-id="018fa-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Petite toomedium des fichiers locaux avec le traitement][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="018fa-121">Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-122">Créez une machine virtuelle Azure exécutant IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="018fa-123">Télécharger des données tooan conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="018fa-124">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données à partir du conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="018fa-125">Transformer les données toocleaned, sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="018fa-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="018fa-126">Enregistrez les données transformées dans des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="018fa-127">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="018fa-128">Lire les données de hello d’objets BLOB Windows Azure à l’aide de hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="018fa-129">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="018fa-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="018fa-130"><a name="largelocal"></a>Scénario \#3 : jeu de données volumineux de fichiers locaux, ciblant des objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="018fa-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Fichiers locaux volumineux][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="018fa-132">Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-133">Créez une machine virtuelle Azure exécutant IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="018fa-134">Télécharger des données tooan conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="018fa-135">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="018fa-136">Transformer les données toocleaned, sous forme de tableau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="018fa-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="018fa-137">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="018fa-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="018fa-138">Extrayez un échantillon de données petit à moyen.</span><span class="sxs-lookup"><span data-stu-id="018fa-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="018fa-139">Enregistrer les données de hello échantillonnée dans des objets BLOB Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="018fa-140">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="018fa-141">Lire les données de hello d’objets BLOB Windows Azure à l’aide de hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="018fa-142">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="018fa-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="018fa-143"><a name="smalllocaltodb"></a>Scénario \#4 : petit toomedium de jeu de données de fichiers locaux, ciblant SQL Server dans une Machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="018fa-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Toomedium petits fichiers locaux tooSQL DB dans Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="018fa-145">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-146">Créez une Machine virtuelle Azure exécutant SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="018fa-147">Télécharger des données tooan conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="018fa-148">Pré-traitez et nettoyez les données dans un conteneur de stockage Azure à l’aide d’IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="018fa-149">Transformer les données toocleaned, sous forme de tableau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="018fa-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="018fa-150">Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).</span><span class="sxs-lookup"><span data-stu-id="018fa-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="018fa-151">Charger des données tooSQL serveur de base de données en cours d’exécution sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="018fa-152">Option \#1 : utilisation de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="018fa-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="018fa-153">Connexion tooSQL machine virtuelle du serveur</span><span class="sxs-lookup"><span data-stu-id="018fa-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="018fa-154">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="018fa-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="018fa-155">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="018fa-155">Create database and target tables.</span></span>
   * <span data-ttu-id="018fa-156">Utilisez une en bloc de hello importer des données de hello tooload de méthodes à partir des fichiers d’ordinateur virtuel local.</span><span class="sxs-lookup"><span data-stu-id="018fa-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="018fa-157">Option \#2 : utilisation d’IPython Notebook – déconseillé pour les jeux de données de tailles moyenne et supérieure</span><span class="sxs-lookup"><span data-stu-id="018fa-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="018fa-158">Utilisez tooaccess de chaîne de connexion ODBC SQL Server sur l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="018fa-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="018fa-159">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="018fa-159">Create database and target tables.</span></span>
   * <span data-ttu-id="018fa-160">Utilisez une en bloc de hello importer des données de hello tooload de méthodes à partir des fichiers d’ordinateur virtuel local.</span><span class="sxs-lookup"><span data-stu-id="018fa-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="018fa-161">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="018fa-161">Explore data, create features as needed.</span></span> <span data-ttu-id="018fa-162">Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="018fa-163">Uniquement Notez hello requête nécessaire toocreate les.</span><span class="sxs-lookup"><span data-stu-id="018fa-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="018fa-164">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="018fa-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="018fa-165">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="018fa-166">Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="018fa-167">Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.</span><span class="sxs-lookup"><span data-stu-id="018fa-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="018fa-168">Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.</span><span class="sxs-lookup"><span data-stu-id="018fa-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="018fa-169"><a name="largelocaltodb"></a>Scénario \#5 : jeu de données volumineux dans des fichiers locaux, ciblant SQL Server dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="018fa-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Les fichiers volumineux local tooSQL DB dans Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="018fa-171">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-172">Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="018fa-173">Télécharger des données tooan conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="018fa-174">(Facultatif) Pré-traitez et nettoyez les données.</span><span class="sxs-lookup"><span data-stu-id="018fa-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="018fa-175">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-175">a.</span></span>  <span data-ttu-id="018fa-176">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="018fa-177">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-177">b.</span></span>  <span data-ttu-id="018fa-178">Transformer les données toocleaned, sous forme de tableau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="018fa-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="018fa-179">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-179">c.</span></span>  <span data-ttu-id="018fa-180">Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).</span><span class="sxs-lookup"><span data-stu-id="018fa-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="018fa-181">Charger des données tooSQL serveur de base de données en cours d’exécution sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="018fa-182">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-182">a.</span></span>  <span data-ttu-id="018fa-183">Connexion tooSQL machine virtuelle du serveur.</span><span class="sxs-lookup"><span data-stu-id="018fa-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="018fa-184">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-184">b.</span></span>  <span data-ttu-id="018fa-185">Si les données ne sont pas déjà enregistrées, téléchargez les fichiers de données à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="018fa-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="018fa-186">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-186">c.</span></span>  <span data-ttu-id="018fa-187">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="018fa-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="018fa-188">d.</span><span class="sxs-lookup"><span data-stu-id="018fa-188">d.</span></span>  <span data-ttu-id="018fa-189">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="018fa-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="018fa-190">e.</span><span class="sxs-lookup"><span data-stu-id="018fa-190">e.</span></span>  <span data-ttu-id="018fa-191">Utilisez une en bloc de hello importer des données de hello tooload de méthodes.</span><span class="sxs-lookup"><span data-stu-id="018fa-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="018fa-192">f.</span><span class="sxs-lookup"><span data-stu-id="018fa-192">f.</span></span>  <span data-ttu-id="018fa-193">Si les jointures de table sont nécessaires, créer des jointures de tooexpedite d’index.</span><span class="sxs-lookup"><span data-stu-id="018fa-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="018fa-194">Pour un chargement plus rapide des tailles de données volumineux, il est recommandé de créer des tables partitionnées et importer en bloc hello données en parallèle.</span><span class="sxs-lookup"><span data-stu-id="018fa-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="018fa-195">Pour plus d’informations, consultez [importation parallèle des données tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="018fa-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="018fa-196">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="018fa-196">Explore data, create features as needed.</span></span> <span data-ttu-id="018fa-197">Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="018fa-198">Uniquement Notez hello requête nécessaire toocreate les.</span><span class="sxs-lookup"><span data-stu-id="018fa-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="018fa-199">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="018fa-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="018fa-200">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="018fa-201">Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="018fa-202">Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.</span><span class="sxs-lookup"><span data-stu-id="018fa-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="018fa-203">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé</span><span class="sxs-lookup"><span data-stu-id="018fa-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="018fa-204"><a name="largedbtodb"></a>Scénario \#6 : jeu de données volumineux dans une base de données SQL Server locale, ciblant SQL Server dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="018fa-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Grande base de données SQL locale tooSQL DB dans Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="018fa-206">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-207">Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="018fa-208">Utilisez une des données de salutation exporter des données de hello tooexport de méthodes à partir de fichiers toodump de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="018fa-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="018fa-209">Si vous décidez de toomove toutes les données de base de données de hello localement, une autre (plus rapide) méthode toomove hello complète de la base de données toothe instance SQL Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="018fa-210">Ignorer les données de tooexport étapes hello, créer la base de données et la base de données de chargement et d’importation données toohello cible et procédez comme autre méthode de hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="018fa-211">Téléchargez le conteneur de stockage de tooAzure de fichiers dump.</span><span class="sxs-lookup"><span data-stu-id="018fa-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="018fa-212">Charge hello données tooa de données SQL Server en cours d’exécution sur une Machine virtuelle de Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="018fa-213">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-213">a.</span></span>  <span data-ttu-id="018fa-214">Connexion toohello machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="018fa-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="018fa-215">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-215">b.</span></span>  <span data-ttu-id="018fa-216">Télécharger les fichiers de données à partir d’un dossier de stockage Azure conteneur toohello local-VM.</span><span class="sxs-lookup"><span data-stu-id="018fa-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="018fa-217">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-217">c.</span></span>  <span data-ttu-id="018fa-218">Exécutez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="018fa-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="018fa-219">d.</span><span class="sxs-lookup"><span data-stu-id="018fa-219">d.</span></span>  <span data-ttu-id="018fa-220">Créez la base de données et les tables cibles.</span><span class="sxs-lookup"><span data-stu-id="018fa-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="018fa-221">e.</span><span class="sxs-lookup"><span data-stu-id="018fa-221">e.</span></span>  <span data-ttu-id="018fa-222">Utilisez une en bloc de hello importer des données de hello tooload de méthodes.</span><span class="sxs-lookup"><span data-stu-id="018fa-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="018fa-223">f.</span><span class="sxs-lookup"><span data-stu-id="018fa-223">f.</span></span>  <span data-ttu-id="018fa-224">Si les jointures de table sont nécessaires, créer des jointures de tooexpedite d’index.</span><span class="sxs-lookup"><span data-stu-id="018fa-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="018fa-225">Pour un chargement plus rapide des tailles de données volumineux, créer des tables partitionnées et toobulk importer hello des données en parallèle.</span><span class="sxs-lookup"><span data-stu-id="018fa-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="018fa-226">Pour plus d’informations, consultez [importation parallèle des données tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="018fa-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="018fa-227">Le cas échéant, explorez des données et créez des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="018fa-227">Explore data, create features as needed.</span></span> <span data-ttu-id="018fa-228">Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="018fa-229">Uniquement Notez hello requête nécessaire toocreate les.</span><span class="sxs-lookup"><span data-stu-id="018fa-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="018fa-230">Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="018fa-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="018fa-231">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="018fa-232">Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="018fa-233">Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.</span><span class="sxs-lookup"><span data-stu-id="018fa-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="018fa-234">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.</span><span class="sxs-lookup"><span data-stu-id="018fa-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="018fa-235">Autre méthode toocopy une base de données complète à partir d’un tooAzure de SQL Server sur site de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="018fa-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Détachez la base de données locale et d’attachement tooSQL DB dans Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="018fa-237">Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="018fa-238">tooreplicate hello ensemble de données SQL Server dans votre machine virtuelle SQL Server, vous devez copier une base de données à partir d’un serveur d’emplacement tooanother, en supposant que hello peut être placée temporairement hors connexion.</span><span class="sxs-lookup"><span data-stu-id="018fa-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="018fa-239">Pour cela, dans hello Explorateur d’objets SQL Server Management Studio ou en utilisant les commandes Transact-SQL équivalentes hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="018fa-240">Détachez la base de données de hello à l’emplacement source de hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="018fa-241">Pour plus d’informations, consultez la rubrique [Détacher une base de données](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="018fa-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="018fa-242">Dans la fenêtre de l’Explorateur Windows ou l’invite de commandes Windows, hello de copie de détacher les fichiers de base de données ou fichiers et fichier journal ou emplacement cible toohello des fichiers sur hello machine virtuelle SQL Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="018fa-243">Joindre l’instance de SQL Server cible hello copié les fichiers toohello.</span><span class="sxs-lookup"><span data-stu-id="018fa-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="018fa-244">Pour plus d’informations, consultez la rubrique [Attacher une base de données](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="018fa-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="018fa-245">[Déplacer une base de données à l’aide de la méthode de détachement et d’attachement (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="018fa-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="018fa-246"><a name="largedbtohive"></a>Scénario \#7 : données volumineuses (« Big Data ») dans des fichiers locaux, ciblant une base de données Hive dans des clusters Hadoop Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="018fa-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Données volumineuses (« Big Data ») dans la base de données Hive cible locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="018fa-248">Autres ressources Azure : cluster Hadoop Azure HDInsight et machine virtuelle Azure (serveur IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="018fa-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="018fa-249">Créez une machine virtuelle Azure exécutant le serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="018fa-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="018fa-250">Créez un cluster Hadoop Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="018fa-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="018fa-251">(Facultatif) Pré-traitez et nettoyez les données.</span><span class="sxs-lookup"><span data-stu-id="018fa-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="018fa-252">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-252">a.</span></span>  <span data-ttu-id="018fa-253">Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="018fa-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="018fa-254">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-254">b.</span></span>  <span data-ttu-id="018fa-255">Transformer les données toocleaned, sous forme de tableau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="018fa-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="018fa-256">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-256">c.</span></span>  <span data-ttu-id="018fa-257">Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).</span><span class="sxs-lookup"><span data-stu-id="018fa-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="018fa-258">Téléchargez le conteneur de valeur par défaut toohello de données de cluster Hadoop de hello hello étape 2.</span><span class="sxs-lookup"><span data-stu-id="018fa-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="018fa-259">Charger la base de données tooHive de cluster Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="018fa-260">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-260">a.</span></span>  <span data-ttu-id="018fa-261">Connectez-vous à toohello le nœud principal du cluster Hadoop de hello</span><span class="sxs-lookup"><span data-stu-id="018fa-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="018fa-262">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-262">b.</span></span>  <span data-ttu-id="018fa-263">Ouvrez hello de ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="018fa-264">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-264">c.</span></span>  <span data-ttu-id="018fa-265">Entrez le répertoire racine de ruche hello par commande `cd %hive_home%\bin` depuis la ligne de commande de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="018fa-266">d.</span><span class="sxs-lookup"><span data-stu-id="018fa-266">d.</span></span>  <span data-ttu-id="018fa-267">Exécuter la base de données toocreate hello ruche de requêtes et les tables et charger des données à partir des tables de tooHive de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="018fa-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="018fa-268">Si les données de salutation sont grande, les utilisateurs peuvent créer de table de Hive hello avec des partitions.</span><span class="sxs-lookup"><span data-stu-id="018fa-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="018fa-269">Ensuite, les utilisateurs peuvent utiliser un `for` boucle Bonjour de ligne de commande Hadoop sur les données de tooload de nœud principal hello en hello ruche table est partitionnée par partition.</span><span class="sxs-lookup"><span data-stu-id="018fa-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="018fa-270">Le cas échéant, explorez des données et créez des fonctionnalités dans la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="018fa-271">Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="018fa-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="018fa-272">Uniquement Notez hello requête nécessaire toocreate les.</span><span class="sxs-lookup"><span data-stu-id="018fa-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="018fa-273">a.</span><span class="sxs-lookup"><span data-stu-id="018fa-273">a.</span></span>  <span data-ttu-id="018fa-274">Connectez-vous à toohello le nœud principal du cluster Hadoop de hello</span><span class="sxs-lookup"><span data-stu-id="018fa-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="018fa-275">b.</span><span class="sxs-lookup"><span data-stu-id="018fa-275">b.</span></span>  <span data-ttu-id="018fa-276">Ouvrez hello de ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="018fa-277">c.</span><span class="sxs-lookup"><span data-stu-id="018fa-277">c.</span></span>  <span data-ttu-id="018fa-278">Entrez le répertoire racine de ruche hello par commande `cd %hive_home%\bin` depuis la ligne de commande de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="018fa-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="018fa-279">d.</span><span class="sxs-lookup"><span data-stu-id="018fa-279">d.</span></span>  <span data-ttu-id="018fa-280">Exécuter des requêtes Hive hello en ligne de commande Hadoop sur le nœud principal de hello hello Hadoop tooexplore hello de données de cluster et créer des fonctionnalités en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="018fa-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="018fa-281">Si nécessaire, et/ou vous le souhaitez, les exemples de toofit de données hello dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="018fa-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="018fa-282">Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="018fa-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="018fa-283">Lire les données de salutation directement à partir de hello `Hive Queries` à l’aide de hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="018fa-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="018fa-284">Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.</span><span class="sxs-lookup"><span data-stu-id="018fa-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="018fa-285">Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.</span><span class="sxs-lookup"><span data-stu-id="018fa-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="018fa-286"><a name="decisiontree"></a>Arbre de décision pour le choix du scénario</span><span class="sxs-lookup"><span data-stu-id="018fa-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="018fa-287">Hello diagramme suivant résume les scénarios hello décrits ci-dessus et hello technologie et les processus d’Analytique avancée choix effectués prenant tooeach des scénarios de hello détaillé.</span><span class="sxs-lookup"><span data-stu-id="018fa-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="018fa-288">Notez que le traitement des données, l’exploration, l’ingénierie de fonctionnalité et échantillonnage peuvent prendre placer dans un ou plusieurs (méthode) à l’environnement, à la source de hello, intermédiaire, et/ou les environnements cibles – et peuvent se poursuivre de manière itérative en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="018fa-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="018fa-289">diagramme de Hello sert à obtenir une illustration de certains flux possibles uniquement et ne fournit pas une énumération exhaustive.</span><span class="sxs-lookup"><span data-stu-id="018fa-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Exemples de scénarios de procédure pas à pas pour le processus DS][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="018fa-291">Analyse avancée en action, exemples</span><span class="sxs-lookup"><span data-stu-id="018fa-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="018fa-292">De bout en bout pour Azure Machine Learning procédures pas à pas qui emploient hello technologie et les processus d’Analytique avancée à l’aide de jeux de données publics, consultez :</span><span class="sxs-lookup"><span data-stu-id="018fa-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="018fa-293">[Processus TDSP (Team Data Science Process) en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="018fa-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="018fa-294">[Processus TDSP (Team Data Science Process) en action : utilisation de clusters Hadoop HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="018fa-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
