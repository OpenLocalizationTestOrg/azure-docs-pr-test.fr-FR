---
title: "Importation de données dans Machine Learning Studio | Microsoft Docs"
description: "Découvrez comment importer vos données Azure Machine Learning Studio depuis différentes sources de données. Découvrez quels types de données et quels formats de données sont pris en charge."
keywords: "importer des données, format de données, types de données, sources de données, données d’apprentissage"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="618a2-105">Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="618a2-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="618a2-106">Pour utiliser vos propres données dans Machine Learning Studio afin de développer et de tester une solution d'analyse prédictive, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="618a2-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="618a2-107">télécharger par avance les données d’un **fichier local** sur votre disque dur pour créer un module de jeu de données dans votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="618a2-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="618a2-108">accéder aux données à partir d’une des nombreuses **sources de données en ligne** pendant que votre expérience s’exécute à l’aide du module [Importer des données][import-data]</span><span class="sxs-lookup"><span data-stu-id="618a2-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="618a2-109">utiliser les données d’une autre **expérience** Azure Machine Learning enregistrée en tant que jeu de données</span><span class="sxs-lookup"><span data-stu-id="618a2-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="618a2-110">utiliser les données depuis une **base de données SQL Server** locale</span><span class="sxs-lookup"><span data-stu-id="618a2-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="618a2-111">Chacune de ces options est décrite dans l’une des rubriques du menu ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="618a2-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="618a2-112">Ces rubriques montrent comment importer des données à partir de différentes sources afin de les utiliser dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="618a2-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="618a2-113">Un certain nombre d’exemples de jeux de données sont disponibles dans Machine Learning Studio et vous pouvez les utiliser comme données de formation.</span><span class="sxs-lookup"><span data-stu-id="618a2-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="618a2-114">Pour plus d’informations, consultez [Utilisation des exemples de jeux de données dans Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="618a2-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="618a2-115">Cette rubrique d’introduction traite également de la préparation des données afin de les utiliser dans Machine Learning Studio, et décrit les formats et les types de données pris en charge.</span><span class="sxs-lookup"><span data-stu-id="618a2-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="618a2-116">Préparation des données à utiliser dans Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="618a2-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="618a2-117">Machine Learning Studio est conçu pour travailler avec des données tabulaires ou rectangulaires, comme des données texte délimitées ou structurées à partir d’une base de données, bien que dans certains cas des données non rectangulaires puissent être utilisées.</span><span class="sxs-lookup"><span data-stu-id="618a2-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="618a2-118">Il est préférable que vos données soient relativement nettoyées.</span><span class="sxs-lookup"><span data-stu-id="618a2-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="618a2-119">Autrement dit, vous devez régler les problèmes tels que des chaînes sans guillemet avant de télécharger les données dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="618a2-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="618a2-120">Toutefois, des modules de Machine Learning Studio permettent d’effectuer certaines manipulations de données dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="618a2-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="618a2-121">En fonction des algorithmes d’apprentissage automatique que vous allez utiliser, vous devrez décider comment gérer les problèmes structurels des données tels que des valeurs manquantes et des données fragmentées. Certains modules existent pour vous aider à régler ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="618a2-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="618a2-122">Rechercher dans la section **Transformation des données** de la palette des modules ceux qui exécutent ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="618a2-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="618a2-123">À tout moment dans votre expérience, vous pouvez voir ou télécharger les données qui sont générées par un module en cliquant sur le port de sortie.</span><span class="sxs-lookup"><span data-stu-id="618a2-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="618a2-124">En fonction du module, différentes options de téléchargement sont disponibles. Vous pouvez également afficher les données dans votre navigateur web dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="618a2-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="618a2-125">Formats et types de données pris en charge</span><span class="sxs-lookup"><span data-stu-id="618a2-125">Data formats and data types supported</span></span>
<span data-ttu-id="618a2-126">Vous pouvez importer un certain nombre de types de données dans votre expérience, selon le mécanisme que vous utilisez pour importer les données et l’emplacement d’où elles proviennent :</span><span class="sxs-lookup"><span data-stu-id="618a2-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="618a2-127">Texte brut (.txt)</span><span class="sxs-lookup"><span data-stu-id="618a2-127">Plain text (.txt)</span></span>
* <span data-ttu-id="618a2-128">Comma-separated values (CSV) avec un en-tête (.csv) ou sans (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="618a2-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="618a2-129">Tab-separated values (TSV) avec un en-tête (.tsv) ou sans (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="618a2-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="618a2-130">Fichier Excel</span><span class="sxs-lookup"><span data-stu-id="618a2-130">Excel file</span></span>
* <span data-ttu-id="618a2-131">Table Azure</span><span class="sxs-lookup"><span data-stu-id="618a2-131">Azure table</span></span>
* <span data-ttu-id="618a2-132">Table Hive</span><span class="sxs-lookup"><span data-stu-id="618a2-132">Hive table</span></span>
* <span data-ttu-id="618a2-133">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="618a2-133">SQL database table</span></span>
* <span data-ttu-id="618a2-134">Valeurs OData</span><span class="sxs-lookup"><span data-stu-id="618a2-134">OData values</span></span>
* <span data-ttu-id="618a2-135">Données SVMLight (.svmlight) (voir la [définition SVMLight](http://svmlight.joachims.org/) pour les informations relatives au format)</span><span class="sxs-lookup"><span data-stu-id="618a2-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="618a2-136">Données Attribute Relation File Format (ARFF) (.arff) (voir la [définition ARFF](http://weka.wikispaces.com/ARFF) pour les informations relatives au format)</span><span class="sxs-lookup"><span data-stu-id="618a2-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="618a2-137">Fichier zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="618a2-137">Zip file (.zip)</span></span>
* <span data-ttu-id="618a2-138">Fichier d’espace de travail ou d’objet R (.RData)</span><span class="sxs-lookup"><span data-stu-id="618a2-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="618a2-139">Si vous importez des données dans un format tel que ARFF qui inclut des métadonnées, Machine Learning Studio utilise ces métadonnées pour définir le titre et le type de données de chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="618a2-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="618a2-140">Si vous importez des données dans des formats tels que TSV ou CSV qui n’incluent pas ces métadonnées, Machine Learning Studio déduit le type de données de chaque colonne en échantillonnant les données.</span><span class="sxs-lookup"><span data-stu-id="618a2-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="618a2-141">Si les données aussi n’ont pas non plus de titre de colonne, Machine Learning Studio fournit des noms par défaut.</span><span class="sxs-lookup"><span data-stu-id="618a2-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="618a2-142">Vous pouvez spécifier de manière explicite ou modifier les titres et les types de données pour les colonnes à l’aide de [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="618a2-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="618a2-143">Voici les **types de données** reconnus par Machine Learning Studio :</span><span class="sxs-lookup"><span data-stu-id="618a2-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="618a2-144">String</span><span class="sxs-lookup"><span data-stu-id="618a2-144">String</span></span>
* <span data-ttu-id="618a2-145">Integer</span><span class="sxs-lookup"><span data-stu-id="618a2-145">Integer</span></span>
* <span data-ttu-id="618a2-146">Double</span><span class="sxs-lookup"><span data-stu-id="618a2-146">Double</span></span>
* <span data-ttu-id="618a2-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="618a2-147">Boolean</span></span>
* <span data-ttu-id="618a2-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="618a2-148">DateTime</span></span>
* <span data-ttu-id="618a2-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="618a2-149">TimeSpan</span></span>

<span data-ttu-id="618a2-150">Machine Learning Studio utilise un type de données interne appelé ***Table de données*** pour passer des données entre les modules.</span><span class="sxs-lookup"><span data-stu-id="618a2-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="618a2-151">Vous pouvez convertir de manière explicite vos données dans un format de table de données à l’aide du module [Convertir en jeu de données][convert-to-dataset].</span><span class="sxs-lookup"><span data-stu-id="618a2-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="618a2-152">Tout module qui accepte d'autres formats que la table de données convertira silencieusement les données de la table de données avant de les passer au module suivant.</span><span class="sxs-lookup"><span data-stu-id="618a2-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="618a2-153">Au besoin, vous pouvez convertir à nouveau le format de la table de données au format CSV, TSV, ARFF ou SVMLight à l'aide d'autres modules de conversion.</span><span class="sxs-lookup"><span data-stu-id="618a2-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="618a2-154">Recherchez dans la section **Conversion des formats de données** de la palette des modules ceux qui exécutent ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="618a2-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
