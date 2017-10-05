---
title: "Création de modules R personnalisés dans Azure Machine Learning | Microsoft Docs"
description: "Démarrage rapide pour la création de modules R personnalisés dans Microsoft Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="517ed-103">Création de modules R personnalisés dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="517ed-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="517ed-104">Cette rubrique explique comment créer et déployer un module R personnalisé dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="517ed-105">Elle explique ce qu’est un module R personnalisé, en détaillant les fichiers utilisés pour le définir.</span><span class="sxs-lookup"><span data-stu-id="517ed-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="517ed-106">Par ailleurs, elle illustre la construction de ces fichiers et l’inscription du module à des fins de déploiement dans un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="517ed-107">Les éléments et attributs utilisés dans la définition du module personnalisé sont ensuite décrits plus en détail.</span><span class="sxs-lookup"><span data-stu-id="517ed-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="517ed-108">Par ailleurs, nous allons découvrir comment utiliser les fichiers et la fonctionnalité auxiliaires, ainsi que les sorties multiples.</span><span class="sxs-lookup"><span data-stu-id="517ed-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="517ed-109">Qu’est-ce qu’un module R personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="517ed-109">What is a custom R module?</span></span>
<span data-ttu-id="517ed-110">Un **module personnalisé** est un module défini par l’utilisateur, qui peut être chargé dans votre espace de travail et exécuté dans le cadre d’une expérience Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="517ed-111">Un **module R personnalisé** est un module exécutant une fonction R définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="517ed-112">**R** est un langage de programmation utilisé pour le traitement informatique des statistiques et les graphiques. Les chercheurs de données et les statisticiens s’en servent pour implémenter des algorithmes.</span><span class="sxs-lookup"><span data-stu-id="517ed-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="517ed-113">Actuellement, R est le seul langage pris en charge dans les modules personnalisés, mais la prise en charge de langages supplémentaires est prévue pour les versions à venir.</span><span class="sxs-lookup"><span data-stu-id="517ed-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="517ed-114">Les modules personnalisés présentent un **état de première classe** dans Azure Machine Learning, en ce sens qu’ils peuvent être utilisés comme n’importe quel module classique.</span><span class="sxs-lookup"><span data-stu-id="517ed-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="517ed-115">Ils peuvent être exécutés avec d’autres modules, inclus dans des expériences publiées ou dans des visualisations.</span><span class="sxs-lookup"><span data-stu-id="517ed-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="517ed-116">Vous contrôlez l’algorithme implémenté par le module, les ports d’entrée et de sortie à utiliser, les paramètres de modélisation et divers autres comportements d’exécution.</span><span class="sxs-lookup"><span data-stu-id="517ed-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="517ed-117">Une expérience qui contient des modules personnalisés peut également être publiée dans la galerie Cortana Intelligence pour faciliter le partage.</span><span class="sxs-lookup"><span data-stu-id="517ed-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="517ed-118">Fichiers dans un module R personnalisé</span><span class="sxs-lookup"><span data-stu-id="517ed-118">Files in a custom R module</span></span>
<span data-ttu-id="517ed-119">Un module R personnalisé est défini par un fichier .zip contenant au moins deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="517ed-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="517ed-120">un **fichier source** qui implémente la fonction R exposée par le module ;</span><span class="sxs-lookup"><span data-stu-id="517ed-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="517ed-121">un **fichier de définition XML** qui décrit l’interface du module personnalisé.</span><span class="sxs-lookup"><span data-stu-id="517ed-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="517ed-122">Des fichiers auxiliaires supplémentaires peuvent également être inclus dans le fichier .zip, qui fournit des fonctionnalités accessibles à partir du module personnalisé.</span><span class="sxs-lookup"><span data-stu-id="517ed-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="517ed-123">Cette option est décrite dans la partie **Arguments** de la section de référence **Éléments dans le fichier de définition XML** suivant l’exemple de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="517ed-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="517ed-124">Exemple de démarrage rapide : définir, mettre en package et enregistrer un module R personnalisé</span><span class="sxs-lookup"><span data-stu-id="517ed-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="517ed-125">Cet exemple explique comment créer les fichiers requis par un module R personnalisé, les empaqueter dans un fichier .zip, puis enregistrer le module dans l’espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="517ed-126">Les exemples de fichiers et de package zip sont disponibles en téléchargement depuis le [fichier CustomAddRows.zip](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="517ed-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="517ed-127">Le fichier source</span><span class="sxs-lookup"><span data-stu-id="517ed-127">The source file</span></span>
<span data-ttu-id="517ed-128">Prenons l’exemple d’un module **Custom Add Rows**, qui modifie l’implémentation standard du module **Add Rows** utilisé pour concaténer des lignes (observations) à partir de deux jeux de données (trames de données).</span><span class="sxs-lookup"><span data-stu-id="517ed-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="517ed-129">Le module **Add Rows** standard ajoute les lignes du deuxième jeu de données d’entrée à la fin du premier, au moyen de l’algorithme `rbind`.</span><span class="sxs-lookup"><span data-stu-id="517ed-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="517ed-130">De la même manière, la fonction `CustomAddRows` personnalisée accepte deux jeux de données, mais également un paramètre d’échange booléen en entrée supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="517ed-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="517ed-131">Si le paramètre d’échange a la valeur **FALSE**, il renvoie le même jeu de données que l’implémentation standard.</span><span class="sxs-lookup"><span data-stu-id="517ed-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="517ed-132">Par contre, s’il a la valeur **TRUE**, la fonction ajoute des lignes du premier jeu de données d’entrée à la fin du deuxième jeu de données.</span><span class="sxs-lookup"><span data-stu-id="517ed-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="517ed-133">Le fichier CustomAddRows.R qui contient l’implémentation de la fonction R `CustomAddRows` exposée par le module **Custom Add Rows** contient le code R suivant.</span><span class="sxs-lookup"><span data-stu-id="517ed-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="the-xml-definition-file"></a><span data-ttu-id="517ed-134">Le fichier de définition XML</span><span class="sxs-lookup"><span data-stu-id="517ed-134">The XML definition file</span></span>
<span data-ttu-id="517ed-135">Pour exposer la fonction `CustomAddRows` en tant que module Azure Machine Learning, vous devez créer un fichier de définition XML, afin de définir l’apparence du module **Custom Add Rows** et son comportement.</span><span class="sxs-lookup"><span data-stu-id="517ed-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="517ed-136">Il est essentiel de noter que la valeur des attributs **id** des éléments **Input** et **Arg** dans le fichier XML doit correspondre aux noms des paramètres de la fonction du code R dans le fichier CustomAddRows.R À L’EXACT (*dataset1*, *dataset2* et *swap* dans l’exemple).</span><span class="sxs-lookup"><span data-stu-id="517ed-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="517ed-137">De même, la valeur de l’attribut **entryPoint** de l’élément **Language** doit correspondre au nom de la fonction dans le script R À L’EXACT (*CustomAddRows* dans l’exemple).</span><span class="sxs-lookup"><span data-stu-id="517ed-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="517ed-138">En revanche, l’attribut **id** de l’élément **Output** ne correspond à aucune variable du script R.</span><span class="sxs-lookup"><span data-stu-id="517ed-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="517ed-139">Lorsque plusieurs sorties sont requises, il suffit de renvoyer une liste à partir de la fonction R avec les résultats placés *dans le même ordre* que celui dans lequel les éléments **Sorties** sont déclarés dans le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="517ed-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="517ed-140">Empaqueter et inscrire le module</span><span class="sxs-lookup"><span data-stu-id="517ed-140">Package and register the module</span></span>
<span data-ttu-id="517ed-141">Enregistrez ces deux fichiers sous *CustomAddRows.R* et *CustomAddRows.xml*, puis compressez les deux fichiers ensemble dans un fichier *CustomAddRows.zip*.</span><span class="sxs-lookup"><span data-stu-id="517ed-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="517ed-142">Pour les enregistrer dans votre espace de travail Machine Learning, accédez à votre espace de travail dans Machine Learning Studio, cliquez sur le bouton **+NOUVEAU** situé dans la partie inférieure de la fenêtre et choisissez **MODULE -> À PARTIR DU PACKAGE ZIP** pour charger le nouveau module **Custom Add Rows**.</span><span class="sxs-lookup"><span data-stu-id="517ed-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Charger les zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="517ed-144">Le module **Custom Add Rows** peut désormais être ouvert par vos expériences Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="517ed-145">Éléments dans le fichier de définition XML</span><span class="sxs-lookup"><span data-stu-id="517ed-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="517ed-146">Éléments de module</span><span class="sxs-lookup"><span data-stu-id="517ed-146">Module elements</span></span>
<span data-ttu-id="517ed-147">L’élément **Module** est utilisé pour définir un module personnalisé dans le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="517ed-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="517ed-148">Plusieurs modules peuvent être définis dans un fichier XML à l’aide de plusieurs éléments **module** .</span><span class="sxs-lookup"><span data-stu-id="517ed-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="517ed-149">Chaque module de votre espace de travail doit avoir un nom unique.</span><span class="sxs-lookup"><span data-stu-id="517ed-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="517ed-150">Si vous enregistrez un module personnalisé avec le même nom qu’un module personnalisé existant, le module existant est remplacé par le nouveau module.</span><span class="sxs-lookup"><span data-stu-id="517ed-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="517ed-151">Les modules personnalisés peuvent, toutefois, être inscrits avec le même nom qu’un module Azure Machine Learning existant.</span><span class="sxs-lookup"><span data-stu-id="517ed-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="517ed-152">Dans ce cas, ils apparaissent dans la catégorie **Personnalisé** de la palette de modules.</span><span class="sxs-lookup"><span data-stu-id="517ed-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="517ed-153">Dans l’élément **Module** , vous pouvez spécifier deux éléments facultatifs supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="517ed-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="517ed-154">un élément **Propriétaire** qui est incorporé dans le module</span><span class="sxs-lookup"><span data-stu-id="517ed-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="517ed-155">un élément **Description** qui contient le texte affiché dans l’aide rapide du module et lorsque vous passez la souris sur le module dans l’interface utilisateur Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="517ed-156">Règles relatives aux limites de caractères dans les éléments Module :</span><span class="sxs-lookup"><span data-stu-id="517ed-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="517ed-157">La valeur de l’attribut **name** dans l’élément **Module** ne doit pas dépasser 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="517ed-158">Le contenu de l’élément **Description** ne doit pas dépasser 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="517ed-159">Le contenu de l’élément **Owner** ne doit pas dépasser 32 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="517ed-160">Les résultats d’un module peuvent être déterministes ou non déterministes.** Par défaut, tous les modules sont considérés comme déterministes.</span><span class="sxs-lookup"><span data-stu-id="517ed-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="517ed-161">Autrement dit, en présence d’un jeu de données et de paramètres d’entrée qui ne change pas, le module doit retourner les mêmes résultats chaque fois qu’il est exécuté.</span><span class="sxs-lookup"><span data-stu-id="517ed-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="517ed-162">Étant donné ce comportement, Azure Machine Learning Studio ne réexécute les modules marqués comme étant déterministes que si un paramètre ou les données d’entrée ont été modifiés.</span><span class="sxs-lookup"><span data-stu-id="517ed-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="517ed-163">Le renvoi des résultats mis en cache assure également une exécution bien plus rapide des expériences.</span><span class="sxs-lookup"><span data-stu-id="517ed-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="517ed-164">Il existe des fonctions non déterministes, notamment RAND ou une fonction qui retourne la date ou l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="517ed-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="517ed-165">Si votre module utilise une fonction non déterministe, vous pouvez spécifier que le module n’est pas déterministe en définissant l’attribut facultatif **isDeterministic** sur **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="517ed-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="517ed-166">Cela permet de s’assurer que le module est réexécuté à chaque exécution de l’expérience, même si le module d’entrée et les paramètres n’ont pas changé.</span><span class="sxs-lookup"><span data-stu-id="517ed-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="517ed-167">Définition de l’élément Language</span><span class="sxs-lookup"><span data-stu-id="517ed-167">Language Definition</span></span>
<span data-ttu-id="517ed-168">L’élément **Language** dans votre fichier de définition XML est utilisé pour spécifier la langue du module personnalisé.</span><span class="sxs-lookup"><span data-stu-id="517ed-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="517ed-169">Actuellement, R est le seul langage pris en charge.</span><span class="sxs-lookup"><span data-stu-id="517ed-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="517ed-170">La valeur de l’attribut **sourceFile** doit être le nom du fichier R qui contient la fonction à appeler lorsque le module est exécuté.</span><span class="sxs-lookup"><span data-stu-id="517ed-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="517ed-171">Ce fichier doit faire partie du package zip.</span><span class="sxs-lookup"><span data-stu-id="517ed-171">This file must be part of the zip package.</span></span> <span data-ttu-id="517ed-172">La valeur de l’attribut **entryPoint** est le nom de la fonction appelée et doit correspondre à une fonction valide définie dans le fichier source.</span><span class="sxs-lookup"><span data-stu-id="517ed-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="517ed-173">Ports</span><span class="sxs-lookup"><span data-stu-id="517ed-173">Ports</span></span>
<span data-ttu-id="517ed-174">Les ports d’entrée et de sortie d’un module personnalisé sont spécifiés dans les éléments enfants de la section **Ports** du fichier de définition XML.</span><span class="sxs-lookup"><span data-stu-id="517ed-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="517ed-175">L’ordre de ces éléments détermine la disposition rencontrée par les utilisateurs (expérience utilisateur).</span><span class="sxs-lookup"><span data-stu-id="517ed-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="517ed-176">Le premier enfant **input** ou **output** répertorié dans l’élément **Ports** du fichier XML devient le port d’entrée le plus à gauche dans l’expérience utilisateur Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="517ed-177">Chaque port d’entrée et de sortie peut avoir un élément enfant **Description** facultatif qui spécifie le texte affiché lorsque vous passez le curseur de la souris sur le port dans l’interface utilisateur de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="517ed-178">**Règles relatives aux ports**:</span><span class="sxs-lookup"><span data-stu-id="517ed-178">**Ports Rules**:</span></span>

* <span data-ttu-id="517ed-179">Le nombre maximum de **ports d’entrée et de sortie** est de 8 pour chacun.</span><span class="sxs-lookup"><span data-stu-id="517ed-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="517ed-180">Éléments d'entrée</span><span class="sxs-lookup"><span data-stu-id="517ed-180">Input elements</span></span>
<span data-ttu-id="517ed-181">Les ports d’entrée vous permettent de transmettre des données à votre fonction R et à votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="517ed-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="517ed-182">Les **types de données** pris en charge pour les ports d’entrée sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="517ed-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="517ed-183">**DataTable :** ce type est transmis à votre fonction R sous la forme suivante : data.frame.</span><span class="sxs-lookup"><span data-stu-id="517ed-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="517ed-184">En réalité, tous les types (par exemple, des fichiers CSV ou des fichiers ARFF) pris en charge par Machine Learning et compatibles avec **DataTable** sont automatiquement convertis en data.frame.</span><span class="sxs-lookup"><span data-stu-id="517ed-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="517ed-185">L’attribut **id** associé à chaque port d’entrée **DataTable** doit avoir une valeur unique qui doit correspondre au paramètre nommé correspondant dans votre fonction R.</span><span class="sxs-lookup"><span data-stu-id="517ed-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="517ed-186">Pour les ports **DataTable** facultatifs qui ne sont pas transmis comme entrée d’une expérience, la valeur **NULL** est transmise à la fonction R et les ports zip facultatifs sont ignorés si l’entrée n’est pas connectée.</span><span class="sxs-lookup"><span data-stu-id="517ed-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="517ed-187">L’attribut **isOptional** est facultatif pour les types **DataTable** et **Zip** ; il a la valeur *false* par défaut.</span><span class="sxs-lookup"><span data-stu-id="517ed-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="517ed-188">**Zip :** modules personnalisés pouvant accepter un fichier .zip en entrée.</span><span class="sxs-lookup"><span data-stu-id="517ed-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="517ed-189">Cette entrée est décompactée et placée dans le répertoire de travail R de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="517ed-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="517ed-190">Pour les modules R personnalisés, l’id d’un port Zip ne doit pas nécessairement correspondre aux paramètres de la fonction R.</span><span class="sxs-lookup"><span data-stu-id="517ed-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="517ed-191">En effet, le fichier zip est automatiquement extrait dans le répertoire de travail R.</span><span class="sxs-lookup"><span data-stu-id="517ed-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="517ed-192">**Règles d'entrée :**</span><span class="sxs-lookup"><span data-stu-id="517ed-192">**Input Rules:**</span></span>

* <span data-ttu-id="517ed-193">La valeur de l’attribut **id** de l’élément **Input** doit être un nom de variable R valide.</span><span class="sxs-lookup"><span data-stu-id="517ed-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="517ed-194">La valeur de l’attribut **id** de l’élément **Input** ne doit pas dépasser 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="517ed-195">La valeur de l’attribut **name** de l’élément **Input** ne doit pas dépasser 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="517ed-196">Le contenu de l’élément **Description** ne doit pas contenir plus de 128 caractères</span><span class="sxs-lookup"><span data-stu-id="517ed-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="517ed-197">La valeur de l’attribut **type** de l’élément **Input** doit être *Zip* ou *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="517ed-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="517ed-198">La valeur de l’attribut **isOptional** de l’élément **Input** n’est pas obligatoire (et est définie sur *false* par défaut lorsqu’il n’est pas spécifié) ; mais s’il est spécifié, la valeur doit être *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="517ed-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="517ed-199">Éléments d’entrée</span><span class="sxs-lookup"><span data-stu-id="517ed-199">Output elements</span></span>
<span data-ttu-id="517ed-200">**Ports de sortie standard :** les ports de sortie sont mappés aux valeurs de retour à partir de votre fonction R, qui peut ensuite être utilisée par les modules suivants.</span><span class="sxs-lookup"><span data-stu-id="517ed-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="517ed-201">*DataTable* est le seul type de port de sortie standard pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="517ed-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="517ed-202">(Les types *Learners* et *Transformers* seront prochainement pris en charge.) Une sortie *DataTable* est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="517ed-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="517ed-203">Pour les sorties dans des modules personnalisés R, la valeur de l’attribut **id** ne doit pas forcément correspondre à un élément du script R, mais elle doit être unique.</span><span class="sxs-lookup"><span data-stu-id="517ed-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="517ed-204">Pour une sortie de module unique, la valeur de retour de la fonction R doit être un *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="517ed-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="517ed-205">Pour créer une sortie portant sur plusieurs objets qui présentent un type de données pris en charge, vous devez spécifier les ports de sortie appropriés dans le fichier de définition XML et les objets doivent être renvoyés dans une liste.</span><span class="sxs-lookup"><span data-stu-id="517ed-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="517ed-206">Les objets de la sortie sont affectés à des ports de sortie, de gauche à droite, selon l’ordre dans lequel les objets sont placés dans la liste renvoyée.</span><span class="sxs-lookup"><span data-stu-id="517ed-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="517ed-207">Par exemple, si vous souhaitez modifier le module **Custom Add Rows** pour sortir les deux jeux de données d’origine, *dataset1* et *dataset2*, en plus du nouveau jeu de données joint dataset, *dataset* (dans l’ordre suivant, de gauche à droite : *dataset*, *dataset1*, *dataset2*), vous devez définir les ports de sortie dans le fichier CustomAddRows.xml comme suit :</span><span class="sxs-lookup"><span data-stu-id="517ed-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="517ed-208">Ensuite, renvoyez la liste des objets dans une liste respectant l’ordre adéquat dans « myAddRows.R » :</span><span class="sxs-lookup"><span data-stu-id="517ed-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="517ed-209">**Sortie de visualisation :** vous pouvez également spécifier un port de sortie de type *Visualization*, qui affiche la sortie de la console et de l’appareil graphique R.</span><span class="sxs-lookup"><span data-stu-id="517ed-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="517ed-210">Ce port ne fait pas partie de la sortie de la fonction R et n’interfère pas avec l’ordre des autres types de ports de sortie.</span><span class="sxs-lookup"><span data-stu-id="517ed-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="517ed-211">Pour ajouter un port de visualisation pour les modules personnalisés, ajoutez un élément **Output** avec la valeur *Visualization* pour son attribut **type** :</span><span class="sxs-lookup"><span data-stu-id="517ed-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="517ed-212">**Règles de sortie :**</span><span class="sxs-lookup"><span data-stu-id="517ed-212">**Output Rules:**</span></span>

* <span data-ttu-id="517ed-213">La valeur de l’attribut **id** de l’élément **Output** doit être un nom de variable R valide.</span><span class="sxs-lookup"><span data-stu-id="517ed-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="517ed-214">La valeur de l’attribut **id** de l’élément **Output** ne doit pas dépasser 32 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="517ed-215">La valeur de l’attribut **name** de l’élément **Output** ne doit pas dépasser 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="517ed-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="517ed-216">La valeur de l’attribut **type** de l’élément **Output** doit être *Visualization*.</span><span class="sxs-lookup"><span data-stu-id="517ed-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="517ed-217">Arguments</span><span class="sxs-lookup"><span data-stu-id="517ed-217">Arguments</span></span>
<span data-ttu-id="517ed-218">Des données supplémentaires peuvent être transmises à la fonction R via les paramètres de module qui sont définis dans l’élément **Arguments** .</span><span class="sxs-lookup"><span data-stu-id="517ed-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="517ed-219">Ces paramètres apparaissent dans le volet des propriétés de l’interface utilisateur de Machine Learning le plus à droite lorsque le module est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="517ed-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="517ed-220">Les arguments peuvent être de n’importe quel type pris en charge, ou vous pouvez créer une énumération personnalisée lorsque cela s’avère nécessaire.</span><span class="sxs-lookup"><span data-stu-id="517ed-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="517ed-221">Comme pour les éléments **Ports**, les éléments **Arguments** peuvent avoir un élément **Description** facultatif spécifiant le texte qui apparaît lorsque vous passez la souris sur le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="517ed-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="517ed-222">Les propriétés facultatives pour un module, telles que defaultValue, minValue et maxValue, peuvent être ajoutées à n’importe quel argument en tant qu’attributs d’un élément **Properties** .</span><span class="sxs-lookup"><span data-stu-id="517ed-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="517ed-223">Les propriétés valides pour l’élément **Properties** dépendent du type d’argument et sont décrites avec les types d’arguments pris en charge dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="517ed-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="517ed-224">Pour les arguments dont la propriété **isOptional** est définie sur **« true »**, l’utilisateur n’a pas à entrer de valeur.</span><span class="sxs-lookup"><span data-stu-id="517ed-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="517ed-225">Si aucune valeur n’est fournie à l’argument, celui-ci n’est pas transmis à la fonction de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="517ed-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="517ed-226">Les arguments de la fonction de point d’entrée qui sont facultatifs doivent être gérés explicitement par la fonction, par exemple se voir attribuer la valeur NULL par défaut dans la définition de fonction de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="517ed-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="517ed-227">Un argument facultatif applique uniquement les autres contraintes d’argument, par exemple min ou max, si une valeur est fournie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="517ed-228">Comme dans le cas des entrées et sorties, il est essentiel que chaque paramètre soit associé à une valeur d’ID unique.</span><span class="sxs-lookup"><span data-stu-id="517ed-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="517ed-229">Dans notre exemple de démarrage rapide, l’ID/paramètre associé était *swap*.</span><span class="sxs-lookup"><span data-stu-id="517ed-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="517ed-230">Élément Arg</span><span class="sxs-lookup"><span data-stu-id="517ed-230">Arg element</span></span>
<span data-ttu-id="517ed-231">Un paramètre de module est défini à l’aide de l’élément enfant **Arg** de la section **Arguments** du fichier de définition XML.</span><span class="sxs-lookup"><span data-stu-id="517ed-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="517ed-232">Comme dans le cas des éléments enfants de la section **Ports**, l’ordre des paramètres de la section **Arguments** définit la disposition rencontrée dans l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="517ed-233">Les paramètres apparaissent de haut en bas dans l’interface utilisateur dans le même ordre que celui dans lequel ils sont définis dans le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="517ed-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="517ed-234">Les types pris en charge par Machine Learning pour les paramètres sont répertoriés ici.</span><span class="sxs-lookup"><span data-stu-id="517ed-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="517ed-235">**int** : paramètre de type entier (32 bits).</span><span class="sxs-lookup"><span data-stu-id="517ed-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="517ed-236">*Propriétés facultatives* : **min**, **max**, **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="517ed-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="517ed-237">**double** : paramètre de type double.</span><span class="sxs-lookup"><span data-stu-id="517ed-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="517ed-238">*Propriétés facultatives* : **min**, **max**, **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="517ed-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="517ed-239">**bool** : paramètre booléen représenté par une case à cocher dans l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="517ed-240">*Propriétés facultatives* : **default**. False si non défini</span><span class="sxs-lookup"><span data-stu-id="517ed-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="517ed-241">**string**: chaîne standard</span><span class="sxs-lookup"><span data-stu-id="517ed-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="517ed-242">*Propriétés facultatives* : **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="517ed-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="517ed-243">**ColumnPicker**: paramètre de sélection de colonne.</span><span class="sxs-lookup"><span data-stu-id="517ed-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="517ed-244">Ce type est représenté sous la forme d’un sélecteur de colonne dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="517ed-245">L’élément **Property** est utilisé ici pour spécifier l’ID du port à partir duquel les colonnes sont sélectionnées, où le type de port cible doit être *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="517ed-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="517ed-246">Le résultat de la sélection des colonnes est transmis à la fonction R sous forme d’une liste de chaînes contenant les noms des colonnes sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="517ed-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="517ed-247">*Propriétés obligatoires* : **portId**. Correspond à l’ID d’un élément Input de type *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="517ed-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="517ed-248">*Propriétés facultatives*:</span><span class="sxs-lookup"><span data-stu-id="517ed-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="517ed-249">**allowedTypes**. Filtre les types de colonnes que vous pouvez choisir.</span><span class="sxs-lookup"><span data-stu-id="517ed-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="517ed-250">Les valeurs valides incluent :</span><span class="sxs-lookup"><span data-stu-id="517ed-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="517ed-251">Chiffre</span><span class="sxs-lookup"><span data-stu-id="517ed-251">Numeric</span></span>
    * <span data-ttu-id="517ed-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="517ed-252">Boolean</span></span>
    * <span data-ttu-id="517ed-253">Par catégorie</span><span class="sxs-lookup"><span data-stu-id="517ed-253">Categorical</span></span>
    * <span data-ttu-id="517ed-254">string</span><span class="sxs-lookup"><span data-stu-id="517ed-254">String</span></span>
    * <span data-ttu-id="517ed-255">Étiquette</span><span class="sxs-lookup"><span data-stu-id="517ed-255">Label</span></span>
    * <span data-ttu-id="517ed-256">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="517ed-256">Feature</span></span>
    * <span data-ttu-id="517ed-257">Score</span><span class="sxs-lookup"><span data-stu-id="517ed-257">Score</span></span>
    * <span data-ttu-id="517ed-258">Tout</span><span class="sxs-lookup"><span data-stu-id="517ed-258">All</span></span>
  * <span data-ttu-id="517ed-259">**default** : les sélections par défaut valides pour le sélecteur de colonne sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="517ed-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="517ed-260">Aucun</span><span class="sxs-lookup"><span data-stu-id="517ed-260">None</span></span>
    * <span data-ttu-id="517ed-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="517ed-261">NumericFeature</span></span>
    * <span data-ttu-id="517ed-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="517ed-262">NumericLabel</span></span>
    * <span data-ttu-id="517ed-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="517ed-263">NumericScore</span></span>
    * <span data-ttu-id="517ed-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="517ed-264">NumericAll</span></span>
    * <span data-ttu-id="517ed-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="517ed-265">BooleanFeature</span></span>
    * <span data-ttu-id="517ed-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="517ed-266">BooleanLabel</span></span>
    * <span data-ttu-id="517ed-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="517ed-267">BooleanScore</span></span>
    * <span data-ttu-id="517ed-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="517ed-268">BooleanAll</span></span>
    * <span data-ttu-id="517ed-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="517ed-269">CategoricalFeature</span></span>
    * <span data-ttu-id="517ed-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="517ed-270">CategoricalLabel</span></span>
    * <span data-ttu-id="517ed-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="517ed-271">CategoricalScore</span></span>
    * <span data-ttu-id="517ed-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="517ed-272">CategoricalAll</span></span>
    * <span data-ttu-id="517ed-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="517ed-273">StringFeature</span></span>
    * <span data-ttu-id="517ed-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="517ed-274">StringLabel</span></span>
    * <span data-ttu-id="517ed-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="517ed-275">StringScore</span></span>
    * <span data-ttu-id="517ed-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="517ed-276">StringAll</span></span>
    * <span data-ttu-id="517ed-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="517ed-277">AllLabel</span></span>
    * <span data-ttu-id="517ed-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="517ed-278">AllFeature</span></span>
    * <span data-ttu-id="517ed-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="517ed-279">AllScore</span></span>
    * <span data-ttu-id="517ed-280">Tout</span><span class="sxs-lookup"><span data-stu-id="517ed-280">All</span></span>

<span data-ttu-id="517ed-281">**DropDown**: liste (déroulante) énumérée spécifiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="517ed-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="517ed-282">Les éléments de liste déroulante sont spécifiés dans l’élément **Properties** à l’aide de l’élément **Item**.</span><span class="sxs-lookup"><span data-stu-id="517ed-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="517ed-283">L’**id** de chaque **Item** doit être unique et être une variable R valide.</span><span class="sxs-lookup"><span data-stu-id="517ed-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="517ed-284">La valeur **name** d’un **Item** est à la fois le texte affiché et la valeur transmise à la fonction R.</span><span class="sxs-lookup"><span data-stu-id="517ed-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="517ed-285">*Propriétés facultatives*:</span><span class="sxs-lookup"><span data-stu-id="517ed-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="517ed-286">**default** : la valeur de la propriété par défaut doit correspondre à une valeur d’ID de l’un des éléments **Item**.</span><span class="sxs-lookup"><span data-stu-id="517ed-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="517ed-287">Fichiers auxiliaires</span><span class="sxs-lookup"><span data-stu-id="517ed-287">Auxiliary Files</span></span>
<span data-ttu-id="517ed-288">Tout fichier placé dans le fichier ZIP de votre module personnalisé sera disponible pour une utilisation au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="517ed-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="517ed-289">Toutes les structures de répertoire présentes sont conservées.</span><span class="sxs-lookup"><span data-stu-id="517ed-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="517ed-290">Cela signifie que l’approvisionnement du fichier fonctionne de la même façon en local et lors de l’exécution d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="517ed-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="517ed-291">Notez que tous les fichiers sont extraits vers le répertoire « src ». Tous les chemins d’accès doivent donc comporter un préfixe « src/ ».</span><span class="sxs-lookup"><span data-stu-id="517ed-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="517ed-292">Supposons que vous souhaitiez supprimer toutes les lignes présentant la mention « NA » et toutes les lignes en double dans le jeu de données avant de créer une sortie dans myAddRows, et que vous avez déjà créé une fonction R qui effectue cette opération dans un fichier, removeDupNARows.R :</span><span class="sxs-lookup"><span data-stu-id="517ed-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="517ed-293">Vous pouvez approvisionner le fichier auxiliaire RemoveDupNARows.R dans la fonction myAddRows :</span><span class="sxs-lookup"><span data-stu-id="517ed-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="517ed-294">Ensuite, chargez un fichier .zip contenant les éléments « CustomAddRows.R », « CustomAddRows.xml » et « RemoveDupNARows.R » en tant que module R personnalisé.</span><span class="sxs-lookup"><span data-stu-id="517ed-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="517ed-295">Environnement d’exécution</span><span class="sxs-lookup"><span data-stu-id="517ed-295">Execution Environment</span></span>
<span data-ttu-id="517ed-296">L’environnement d’exécution du script R utilise la même version de R que le module **Exécuter le script R** et vous pouvez utiliser les mêmes packages par défaut.</span><span class="sxs-lookup"><span data-stu-id="517ed-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="517ed-297">Vous pouvez également ajouter des packages R supplémentaires à votre module personnalisé en les incluant dans le package zip du module personnalisé.</span><span class="sxs-lookup"><span data-stu-id="517ed-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="517ed-298">Chargez-les simplement dans votre script R comme vous le feriez dans votre propre environnement R.</span><span class="sxs-lookup"><span data-stu-id="517ed-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="517ed-299">**limitations de l’environnement d’exécution** sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="517ed-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="517ed-300">Système de fichiers non persistant : les fichiers écrits lorsque le module personnalisé est exécuté ne sont pas persistants sur plusieurs exécutions du même module.</span><span class="sxs-lookup"><span data-stu-id="517ed-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="517ed-301">Pas d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="517ed-301">No network access</span></span>

