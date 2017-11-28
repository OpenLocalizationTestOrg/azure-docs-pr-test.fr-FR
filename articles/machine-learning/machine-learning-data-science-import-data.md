---
title: "données aaaImport dans Machine Learning Studio | Documents Microsoft"
description: "Comment tooimport vos données dans Azure Machine Learning Studio à partir de diverses sources de données. Découvrez quels types de données et quels formats de données sont pris en charge."
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
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="92620-105">Importation de vos données d’apprentissage Azure Machine Learning Studio depuis différentes sources de données</span><span class="sxs-lookup"><span data-stu-id="92620-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="92620-106">toouse vos propres données dans Machine Learning Studio toodevelop et effectuer l’apprentissage d’une solution prédictive analytique, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="92620-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="92620-107">Télécharger les données d’une **fichier local** avance par rapport de temps à partir de votre disque dur de toocreate un module de jeu de données dans votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="92620-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="92620-108">accéder aux données à partir d’un des nombreux **des sources de données en ligne** pendant que votre expérience est en cours d’exécution à l’aide de hello [importer des données] [ import-data] module</span><span class="sxs-lookup"><span data-stu-id="92620-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="92620-109">utiliser les données d’une autre **expérience** Azure Machine Learning enregistrée en tant que jeu de données</span><span class="sxs-lookup"><span data-stu-id="92620-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="92620-110">utiliser les données depuis une **base de données SQL Server** locale</span><span class="sxs-lookup"><span data-stu-id="92620-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="92620-111">Chacune de ces options est décrite dans une des rubriques de hello dans menu hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92620-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="92620-112">Les rubriques suivantes vous montrent comment tooimport des données à partir de ces données de diverses sources toouse dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="92620-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="92620-113">Un certain nombre d’exemples de jeux de données sont disponibles dans Machine Learning Studio et vous pouvez les utiliser comme données de formation.</span><span class="sxs-lookup"><span data-stu-id="92620-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="92620-114">Pour plus d’informations sur ces, consultez [utiliser des jeux de données exemple hello dans Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="92620-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="92620-115">Cette rubrique d’introduction explique comment utilisent des données tooget prêtes pour dans Machine Learning Studio également et décrit les formats de données et les types de données sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="92620-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="92620-116">Préparation des données à utiliser dans Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="92620-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="92620-117">Machine Learning Studio est toowork conçue avec des données rectangulaires ou tabulaires, telles que les données de texte délimité ou structuré de données à partir d’une base de données, bien que dans certains cas les données non rectangulaires peuvent être utilisées.</span><span class="sxs-lookup"><span data-stu-id="92620-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="92620-118">Il est préférable que vos données soient relativement nettoyées.</span><span class="sxs-lookup"><span data-stu-id="92620-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="92620-119">Autrement dit, vous souhaiterez tootake administration problèmes tels que des chaînes non délimitées avant de télécharger les données de salutation dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="92620-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="92620-120">Toutefois, des modules de Machine Learning Studio permettent d’effectuer certaines manipulations de données dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="92620-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="92620-121">En fonction des algorithmes d’apprentissage automatique hello vous allez utiliser, vous devrez peut-être toodecide vous allez gérer les problèmes structurels des données telles que des valeurs manquantes ou éparses et les modules qui peut aider.</span><span class="sxs-lookup"><span data-stu-id="92620-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="92620-122">Regarder dans hello **Transformation des données** section de la palette de module hello pour les modules qui exécutent ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="92620-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="92620-123">À tout moment dans votre expérience, vous pouvez afficher ou télécharger des données hello qui sont générées par un module en cliquant sur le port de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="92620-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="92620-124">En fonction du module de hello, options de téléchargement différentes peuvent être disponibles, ou vous pouvez être en mesure de toovisualize les données de salutation dans votre navigateur web dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="92620-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="92620-125">Formats et types de données pris en charge</span><span class="sxs-lookup"><span data-stu-id="92620-125">Data formats and data types supported</span></span>
<span data-ttu-id="92620-126">Vous pouvez importer un nombre de types de données dans votre expérience, selon le mécanisme que vous utilisez les données tooimport et où il sera disponible à partir de :</span><span class="sxs-lookup"><span data-stu-id="92620-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="92620-127">Texte brut (.txt)</span><span class="sxs-lookup"><span data-stu-id="92620-127">Plain text (.txt)</span></span>
* <span data-ttu-id="92620-128">Comma-separated values (CSV) avec un en-tête (.csv) ou sans (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="92620-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="92620-129">Tab-separated values (TSV) avec un en-tête (.tsv) ou sans (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="92620-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="92620-130">Fichier Excel</span><span class="sxs-lookup"><span data-stu-id="92620-130">Excel file</span></span>
* <span data-ttu-id="92620-131">Table Azure</span><span class="sxs-lookup"><span data-stu-id="92620-131">Azure table</span></span>
* <span data-ttu-id="92620-132">Table Hive</span><span class="sxs-lookup"><span data-stu-id="92620-132">Hive table</span></span>
* <span data-ttu-id="92620-133">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="92620-133">SQL database table</span></span>
* <span data-ttu-id="92620-134">Valeurs OData</span><span class="sxs-lookup"><span data-stu-id="92620-134">OData values</span></span>
* <span data-ttu-id="92620-135">Données de SVMLight (.svmlight) (voir hello [SVMLight définition](http://svmlight.joachims.org/) des informations de format)</span><span class="sxs-lookup"><span data-stu-id="92620-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="92620-136">Attribut de données de Format de fichier de Relation (ARFF) (.arff) (voir hello [définition de ARFF](http://weka.wikispaces.com/ARFF) pour des informations de format)</span><span class="sxs-lookup"><span data-stu-id="92620-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="92620-137">Fichier zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="92620-137">Zip file (.zip)</span></span>
* <span data-ttu-id="92620-138">Fichier d’espace de travail ou d’objet R (.RData)</span><span class="sxs-lookup"><span data-stu-id="92620-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="92620-139">Si vous importez des données dans un format tel que ARFF qui inclut des métadonnées, Machine Learning Studio utilise cet en-tête de métadonnées toodefine hello et le type de données de chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="92620-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="92620-140">Si vous importez des données comme format TSV ou volume partagé de cluster qui n’inclut pas ces métadonnées, Machine Learning Studio déduit le type de données de hello pour chaque colonne en échantillonnant les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="92620-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="92620-141">Si les données de salutation n’ont également des en-têtes de colonnes, Machine Learning Studio fournit les noms par défaut.</span><span class="sxs-lookup"><span data-stu-id="92620-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="92620-142">Vous pouvez explicitement spécifier ou modifier hello des en-têtes et types de données pour les colonnes à l’aide de hello [modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="92620-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="92620-143">suivant de Hello **des types de données** sont reconnus par Machine Learning Studio :</span><span class="sxs-lookup"><span data-stu-id="92620-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="92620-144">String</span><span class="sxs-lookup"><span data-stu-id="92620-144">String</span></span>
* <span data-ttu-id="92620-145">Integer</span><span class="sxs-lookup"><span data-stu-id="92620-145">Integer</span></span>
* <span data-ttu-id="92620-146">Double</span><span class="sxs-lookup"><span data-stu-id="92620-146">Double</span></span>
* <span data-ttu-id="92620-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="92620-147">Boolean</span></span>
* <span data-ttu-id="92620-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="92620-148">DateTime</span></span>
* <span data-ttu-id="92620-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="92620-149">TimeSpan</span></span>

<span data-ttu-id="92620-150">Machine Learning Studio utilise un type de données interne appelé ***Table de données*** toopass des données entre les modules.</span><span class="sxs-lookup"><span data-stu-id="92620-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="92620-151">Vous pouvez explicitement convertir vos données dans un format de Table de données à l’aide de hello [convertir tooDataset] [ convert-to-dataset] module.</span><span class="sxs-lookup"><span data-stu-id="92620-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="92620-152">N’importe quel module qui accepte les formats de données Table convertira en mode silencieux hello données tooData Table avant de le transmettre toohello prochain module.</span><span class="sxs-lookup"><span data-stu-id="92620-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="92620-153">Au besoin, vous pouvez convertir à nouveau le format de la table de données au format CSV, TSV, ARFF ou SVMLight à l'aide d'autres modules de conversion.</span><span class="sxs-lookup"><span data-stu-id="92620-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="92620-154">Regarder dans hello **les Conversions de Format de données** section de la palette de module hello pour les modules qui exécutent ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="92620-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
