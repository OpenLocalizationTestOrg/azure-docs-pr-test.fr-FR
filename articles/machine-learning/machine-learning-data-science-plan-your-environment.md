---
title: "scénarios d’aaaIdentify et planifier votre processus analytique - Azure | Documents Microsoft"
description: "Planifiez une analyse avancée en imaginant une série de questions clés."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a><span data-ttu-id="cf2a3-103">Comment tooidentify scénarios et plan pour advanced analytique le traitement des données</span><span class="sxs-lookup"><span data-stu-id="cf2a3-103">How tooidentify scenarios and plan for advanced analytics data processing</span></span>
<span data-ttu-id="cf2a3-104">Quelles ressources vous prévoyez tooinclude lors de la configuration d’un environnement toodo avancée analytique de traitement sur un jeu de données ?</span><span class="sxs-lookup"><span data-stu-id="cf2a3-104">What resources should you plan tooinclude when setting up an environment toodo advanced analytics processing on a dataset?</span></span> <span data-ttu-id="cf2a3-105">Cet article propose une série de questions tooask qui permettra d’identifier les tâches de hello et les ressources appropriées à votre scénario.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-105">This article suggests a series of questions tooask that will help identify hello tasks and resources relevant your scenario.</span></span> <span data-ttu-id="cf2a3-106">ordre de Hello des principales étapes à suivre pour l’analytique prédictive est décrit dans [What ' s hello processus de science des données équipe (TDSP) ?](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-106">hello order of high-level steps for predictive analytics is outlined in [What is hello Team Data Science Process (TDSP)?](data-science-process-overview.md).</span></span> <span data-ttu-id="cf2a3-107">Chacune de ces étapes requiert des ressources spécifiques pour le scénario particulier de hello tâches tooyour pertinentes.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-107">Each of these steps will require specific resources for hello  tasks relevant tooyour particular scenario.</span></span> <span data-ttu-id="cf2a3-108">Bonjour questions clés tooidentify votre scénario préoccupation données logistiques, caractéristiques, hello de qualité de jeux de données hello et les outils hello et langues que vous préférez analyse de hello toodo.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-108">hello key questions tooidentify your scenario concern data logistics, characteristics, hello quality of hello datasets, and hello tools and languages you prefer toodo hello analysis.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a><span data-ttu-id="cf2a3-109">Questions logistiques : emplacements et déplacement des données</span><span class="sxs-lookup"><span data-stu-id="cf2a3-109">Logistic questions: data locations and movement</span></span>
<span data-ttu-id="cf2a3-110">les questions logistique Hello concernent emplacement hello Hello **source de données**, hello **destination cible** dans Azure et configuration requise pour le déplacement des données hello, y compris la planification de hello et des ressources impliqués.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-110">hello logistic questions concern hello location of hello **data source**, hello **target destination** in Azure, and requirements for moving hello data, including hello schedule, amount and resources involved.</span></span> <span data-ttu-id="cf2a3-111">les données de salutation peut-être toobe déplacé plusieurs fois au cours du processus d’analytique hello.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-111">hello data may need toobe moved several times during hello analytics process.</span></span> <span data-ttu-id="cf2a3-112">Un scénario courant consiste à toomove des données locales dans une forme de stockage sur Azure, puis dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-112">A common scenario is toomove local data into some form of storage on Azure and then into Machine Learning Studio.</span></span>

1. <span data-ttu-id="cf2a3-113">**Quelle est votre source de données ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-113">**What is your data source?**</span></span> <span data-ttu-id="cf2a3-114">Est-il local ou dans le cloud de hello ?</span><span class="sxs-lookup"><span data-stu-id="cf2a3-114">Is it local or in hello cloud?</span></span> <span data-ttu-id="cf2a3-115">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cf2a3-115">For example:</span></span>
   
   * <span data-ttu-id="cf2a3-116">les données de salutation sont publiquement disponibles à une adresse HTTP.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-116">hello data is publicly available at an HTTP address.</span></span>
   * <span data-ttu-id="cf2a3-117">les données de salutation se trouvent dans un emplacement de fichier/réseau local.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-117">hello data resides in a local/network file location.</span></span>
   * <span data-ttu-id="cf2a3-118">les données de salutation sont dans une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-118">hello data is in a SQL Server database.</span></span>
   * <span data-ttu-id="cf2a3-119">les données de salutation sont stockées dans un conteneur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cf2a3-119">hello data is stored in an Azure storage container</span></span>
2. <span data-ttu-id="cf2a3-120">**Qu’est hello destination Azure ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-120">**What is hello Azure destination?**</span></span> <span data-ttu-id="cf2a3-121">Où faut-il toobe pour le traitement ou la modélisation ?</span><span class="sxs-lookup"><span data-stu-id="cf2a3-121">Where does it need toobe for processing or modeling?</span></span> <span data-ttu-id="cf2a3-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cf2a3-122">For example:</span></span>
   
   * <span data-ttu-id="cf2a3-123">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="cf2a3-123">Azure Blob Storage</span></span>
   * <span data-ttu-id="cf2a3-124">Bases de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cf2a3-124">SQL Azure databases</span></span>
   * <span data-ttu-id="cf2a3-125">SQL Server dans les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="cf2a3-125">SQL Server on Azure VM</span></span>
   * <span data-ttu-id="cf2a3-126">HDInsight (Hadoop sur Azure) ou tables Hive</span><span class="sxs-lookup"><span data-stu-id="cf2a3-126">HDInsight (Hadoop on Azure) or Hive tables</span></span>
   * <span data-ttu-id="cf2a3-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cf2a3-127">Azure Machine Learning</span></span>
   * <span data-ttu-id="cf2a3-128">Disques durs virtuels Azure montables.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-128">Mountable Azure virtual hard disks.</span></span>
3. <span data-ttu-id="cf2a3-129">**Comment allez-vous les données de salutation toomove ?**  hello procédures et les ressources disponibles tooingest ou charger des données dans un large éventail d’environnements de traitement et de stockage différents sont décrites dans les rubriques suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-129">**How are you going toomove hello data?** hello procedures and resources available tooingest or load data into a variety of different storage and processing environments are outlined in hello following topics.</span></span>
   
   * [<span data-ttu-id="cf2a3-130">Charger des données dans des environnements de stockage à des fins d’analyse</span><span class="sxs-lookup"><span data-stu-id="cf2a3-130">Load data into storage environments for analytics</span></span>](machine-learning-data-science-ingest-data.md)
   * <span data-ttu-id="cf2a3-131">[Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données](machine-learning-data-science-import-data.md)</span><span class="sxs-lookup"><span data-stu-id="cf2a3-131">[Import your training data into Azure Machine Learning Studio from various data sources](machine-learning-data-science-import-data.md).</span></span>
4. <span data-ttu-id="cf2a3-132">**Les données de salutation doit-elle toobe déplacé selon une planification régulière ou modifiés pendant la migration ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-132">**Does hello data need toobe moved on a regular schedule or modified during migration?**</span></span> <span data-ttu-id="cf2a3-133">Envisagez d’utiliser la fabrique de données Azure (ADF) lorsque les données besoins toobe migrés en permanence, en particulier si un scénario hybride qui accède à la fois localement et ressources de cloud est impliqué, ou lorsque hello données sont traitées ou doit toobe modifié ont une logique métier ajouté tooit cours hello en cours de migration.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-133">Consider using Azure Data Factory (ADF) when data needs toobe continually migrated, particularly if a hybrid scenario that accesses both on-premises and cloud resources is involved, or when hello data is transacted or needs toobe modified or have business logic added tooit in hello course of being migrated.</span></span> <span data-ttu-id="cf2a3-134">Pour plus d’informations, consultez [déplacer des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)</span><span class="sxs-lookup"><span data-stu-id="cf2a3-134">For further information, see [Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)</span></span>
5. <span data-ttu-id="cf2a3-135">**La quantité de données de hello est toobe déplacé tooAzure ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-135">**How much of hello data is toobe moved tooAzure?**</span></span> <span data-ttu-id="cf2a3-136">Les jeux de données très volumineux peuvent dépasser la capacité de stockage hello de certains environnements.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-136">Datasets that are very large may exceed hello storage capacity of certain environments.</span></span> <span data-ttu-id="cf2a3-137">Pour obtenir un exemple, consultez la discussion hello des limites de taille de Machine Learning Studio, dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-137">For an example, see hello discussion of size limits for Machine Learning Studio in hello next section.</span></span> <span data-ttu-id="cf2a3-138">Dans ce cas, un échantillon de données de hello peut-être être utilisé pendant l’analyse de hello.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-138">In such cases a sample of hello data may be used during hello analysis.</span></span> <span data-ttu-id="cf2a3-139">Pour savoir comment toodown-exemple un jeu de données dans différents environnements Azure, consultez [les exemples de données Bonjour processus de science des données équipe](machine-learning-data-science-sample-data.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-139">For details of how toodown-sample a dataset in various Azure environments, see [Sample data in hello Team Data Science Process](machine-learning-data-science-sample-data.md).</span></span>

## <a name="data-characteristics-questions-type-format-and-size"></a><span data-ttu-id="cf2a3-140">Questions sur les caractéristiques des données : type, format et taille</span><span class="sxs-lookup"><span data-stu-id="cf2a3-140">Data characteristics questions: type, format and size</span></span>
<span data-ttu-id="cf2a3-141">Ces questions est tooplanning clé votre stockage et de traitement des environnements, chacun d'entre eux sont toovarious approprié types de données et chacune d’elles comportent certaines restrictions.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-141">These questions are key tooplanning your storage and processing environments, each of which are appropriate toovarious types of data and each of which have certain restrictions.</span></span>

1. <span data-ttu-id="cf2a3-142">**Quels sont les types de données hello ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-142">**What are hello data types?**</span></span> <span data-ttu-id="cf2a3-143">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cf2a3-143">For Example:</span></span>
   
   * <span data-ttu-id="cf2a3-144">Numérique</span><span class="sxs-lookup"><span data-stu-id="cf2a3-144">Numerical</span></span>
   * <span data-ttu-id="cf2a3-145">Par catégorie</span><span class="sxs-lookup"><span data-stu-id="cf2a3-145">Categorical</span></span>
   * <span data-ttu-id="cf2a3-146">Chaînes</span><span class="sxs-lookup"><span data-stu-id="cf2a3-146">Strings</span></span>
   * <span data-ttu-id="cf2a3-147">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="cf2a3-147">Binary</span></span>
2. <span data-ttu-id="cf2a3-148">**Quel est le format de vos données ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-148">**How is your data formatted?**</span></span> <span data-ttu-id="cf2a3-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cf2a3-149">For Example:</span></span>
   
   * <span data-ttu-id="cf2a3-150">Fichiers plats séparés par des virgules (CSV) ou séparées par une tabulation (TSV)</span><span class="sxs-lookup"><span data-stu-id="cf2a3-150">Comma-separated (CSV) or tab-separated (TSV) flat files</span></span>
   * <span data-ttu-id="cf2a3-151">Compressés ou non</span><span class="sxs-lookup"><span data-stu-id="cf2a3-151">Compressed or uncompressed</span></span>
   * <span data-ttu-id="cf2a3-152">Objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="cf2a3-152">Azure blobs</span></span>
   * <span data-ttu-id="cf2a3-153">Tables Hadoop Hive</span><span class="sxs-lookup"><span data-stu-id="cf2a3-153">Hadoop Hive tables</span></span>
   * <span data-ttu-id="cf2a3-154">Tables SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf2a3-154">SQL Server tables</span></span>
3. <span data-ttu-id="cf2a3-155">**Quel volume vos données représentent-elles ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-155">**How large is your data?**</span></span>
   
   * <span data-ttu-id="cf2a3-156">Petit : moins de 2 Go</span><span class="sxs-lookup"><span data-stu-id="cf2a3-156">Small: Less than 2GB</span></span>
   * <span data-ttu-id="cf2a3-157">Moyen : entre 2 Go et 10 Go</span><span class="sxs-lookup"><span data-stu-id="cf2a3-157">Medium: Greater than 2GB and less than 10GB</span></span>
   * <span data-ttu-id="cf2a3-158">Grand : supérieur à 10 Go</span><span class="sxs-lookup"><span data-stu-id="cf2a3-158">Large: Greater than 10GB</span></span>

<span data-ttu-id="cf2a3-159">Prenons l’exemple environnement d’Azure Machine Learning Studio hello :</span><span class="sxs-lookup"><span data-stu-id="cf2a3-159">Take hello Azure Machine Learning Studio environment for example:</span></span>

* <span data-ttu-id="cf2a3-160">Pour obtenir la liste des formats de données hello et des types pris en charge par Azure Machine Learning Studio, consultez [des formats de données et les types de données pris en charge](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) section.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-160">For a list of hello data formats and types supported by Azure Machine Learning Studio, see [Data formats and data types supported](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) section.</span></span>
* <span data-ttu-id="cf2a3-161">Pour plus d’informations sur les limitations de données pour Azure Machine Learning Studio, consultez hello **comment grand jeu de données hello possible pour mon modules ?** section [importation et exportation de données pour l’apprentissage](machine-learning-faq.md#machine-learning-studio-questions)</span><span class="sxs-lookup"><span data-stu-id="cf2a3-161">For information on data limitations for Azure Machine Learning Studio, see hello **How large can hello data set be for my modules?** section of [Importing and exporting data for Machine Learning](machine-learning-faq.md#machine-learning-studio-questions)</span></span>

<span data-ttu-id="cf2a3-162">Pour plus d’informations sur les limitations de hello d’autres services Azure utilisés dans le processus d’analytique hello, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-162">For information on hello limitations of other Azure services used in hello analytics process, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

## <a name="data-quality-questions-exploration-and-pre-processing"></a><span data-ttu-id="cf2a3-163">Questions sur la qualité des données : exploration et prétraitement</span><span class="sxs-lookup"><span data-stu-id="cf2a3-163">Data quality questions: exploration and pre-processing</span></span>
1. <span data-ttu-id="cf2a3-164">**Que savez-vous sur vos données ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-164">**What do you know about your data?**</span></span> <span data-ttu-id="cf2a3-165">Explorer les données lorsque vous avez besoin d’une présentation de toogain ses caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-165">Explore data when you need toogain an understand its basic characteristics.</span></span> <span data-ttu-id="cf2a3-166">Par exemple les modèles ou les tendances qu’elles dévoilent, les aberrations qu’elles contiennent ou le nombre de valeurs manquantes.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-166">What patterns or trends it exhibits, what outliers is has or how many values are missing.</span></span> <span data-ttu-id="cf2a3-167">Cette étape est importante pour déterminer l’étendue de hello de pré-traitement si nécessaire, pour formuler des hypothèses qui pourrait suggérer des fonctionnalités les plus appropriées hello ou type d’analyse, de la formulation de plans de collecte de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-167">This step is important for determining hello extent of pre-processing needed, for formulating hypotheses that could suggest hello most appropriate features or type of analysis, and for formulating plans for additional data collection.</span></span> <span data-ttu-id="cf2a3-168">Le calcul des statistiques descriptives et le tracé des visualisations sont des techniques utiles pour l’inspection des données.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-168">Calculating descriptive statistics and plotting visualizations are useful techniques for data inspection.</span></span> <span data-ttu-id="cf2a3-169">Pour plus d’informations de tooexplore un jeu de données dans différents environnements Azure, voir [Explorer les données Bonjour processus de science des données équipe](machine-learning-data-science-explore-data.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-169">For details of how tooexplore a dataset in various Azure environments, see [Explore data in hello Team Data Science Process](machine-learning-data-science-explore-data.md).</span></span>
2. <span data-ttu-id="cf2a3-170">**Les données de salutation nécessite-t-il de pré-traitement ou de nettoyage ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-170">**Does hello data require pre-processing or cleaning?**</span></span>
   <span data-ttu-id="cf2a3-171">Le prétraitement et le nettoyage des données sont des tâches importantes qui doivent intervenir avant d'utiliser un jeu de données à des fins d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-171">Pre-processing and cleaning data are important tasks that typically must be conducted before dataset can be used effectively for machine learning.</span></span> <span data-ttu-id="cf2a3-172">Les données brutes sont souvent bruyantes, peu fiables et incomplètes.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-172">Raw data is often noisy and unreliable, and may be missing values.</span></span> <span data-ttu-id="cf2a3-173">Leur utilisation pour la modélisation peut générer des résultats trompeurs.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-173">Using such data for modeling can produce misleading results.</span></span> <span data-ttu-id="cf2a3-174">Pour obtenir une description, consultez [tooprepare des données pour l’apprentissage améliorée des tâches](machine-learning-data-science-prepare-data.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-174">For a description, see [Tasks tooprepare data for enhanced machine learning](machine-learning-data-science-prepare-data.md).</span></span>

## <a name="tools-and-languages-questions"></a><span data-ttu-id="cf2a3-175">Questions sur les outils et les langues</span><span class="sxs-lookup"><span data-stu-id="cf2a3-175">Tools and languages questions</span></span>
<span data-ttu-id="cf2a3-176">Il existe un grand nombre de possibilités en fonction des langues, des environnements de développement et des outils dont vous avez besoin ou avec lesquels vous êtes le plus à l’aise.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-176">There are lots of options here depending on what languages and development environments or tools you need or are most conformable using.</span></span>

1. <span data-ttu-id="cf2a3-177">**Langues comment vous préférez toouse pour l’analyse ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-177">**What languages do you prefer toouse for analysis?**</span></span>  
   
   * <span data-ttu-id="cf2a3-178">R</span><span class="sxs-lookup"><span data-stu-id="cf2a3-178">R</span></span>
   * <span data-ttu-id="cf2a3-179">Python</span><span class="sxs-lookup"><span data-stu-id="cf2a3-179">Python</span></span>
   * <span data-ttu-id="cf2a3-180">SQL</span><span class="sxs-lookup"><span data-stu-id="cf2a3-180">SQL</span></span>
2. <span data-ttu-id="cf2a3-181">**Quels outils devez-vous utiliser pour l’analyse des données ?**</span><span class="sxs-lookup"><span data-stu-id="cf2a3-181">**What tools should you use for data analysis?**</span></span>
   
   * <span data-ttu-id="cf2a3-182">[Microsoft Azure Powershell](/powershell/azure/overview) -un langage de script utilisé tooadminister vos ressources Azure dans un langage de script.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-182">[Microsoft Azure Powershell](/powershell/azure/overview) - a script language used tooadminister your Azure resources in a script language.</span></span>
   * [<span data-ttu-id="cf2a3-183">Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="cf2a3-183">Azure Machine Learning Studio</span></span>](machine-learning-what-is-ml-studio.md)
   * [<span data-ttu-id="cf2a3-184">Revolution Analytics</span><span class="sxs-lookup"><span data-stu-id="cf2a3-184">Revolution Analytics</span></span>](http://www.revolutionanalytics.com/revolution-r-open)
   * [<span data-ttu-id="cf2a3-185">RStudio</span><span class="sxs-lookup"><span data-stu-id="cf2a3-185">RStudio</span></span>](http://www.rstudio.com)
   * [<span data-ttu-id="cf2a3-186">Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf2a3-186">Python Tools for Visual Studio</span></span>](http://microsoft.github.io/PTVS/)
   * [<span data-ttu-id="cf2a3-187">Anaconda</span><span class="sxs-lookup"><span data-stu-id="cf2a3-187">Anaconda</span></span>](https://www.continuum.io/why-anaconda)
   * [<span data-ttu-id="cf2a3-188">Blocs-notes Jupyter</span><span class="sxs-lookup"><span data-stu-id="cf2a3-188">Jupyter notebooks</span></span>](http://jupyter.org/)
   * [<span data-ttu-id="cf2a3-189">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="cf2a3-189">Microsoft Power BI</span></span>](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a><span data-ttu-id="cf2a3-190">Identification de votre scénario d’analyse avancée</span><span class="sxs-lookup"><span data-stu-id="cf2a3-190">Identify your advanced analytics scenario</span></span>
<span data-ttu-id="cf2a3-191">Une fois que vous avez répondu aux questions hello dans la section précédente de hello, vous êtes prêt toodetermine celui qui correspond à votre cas.</span><span class="sxs-lookup"><span data-stu-id="cf2a3-191">Once you have answered hello questions in hello previous section, you are ready toodetermine which scenario best fits your case.</span></span> <span data-ttu-id="cf2a3-192">exemples de scénarios de Hello sont décrites dans [scénarios d’analytique avancée dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a3-192">hello sample scenarios are outlined in [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).</span></span>
