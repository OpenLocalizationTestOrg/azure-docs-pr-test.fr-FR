---
title: "aaaAuthor des Modules R personnalisés dans Azure Machine Learning | Documents Microsoft"
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
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="44556-103">Création de modules R personnalisés dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="44556-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="44556-104">Cette rubrique décrit comment tooauthor et déployer un module R personnalisé dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="44556-105">Il explique ce que sont les modules R personnalisés et quels fichiers sont utilisé toodefine les.</span><span class="sxs-lookup"><span data-stu-id="44556-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="44556-106">Il illustre comment tooconstruct hello les fichiers qui définissent un module et comment tooregister hello module pour le déploiement dans un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="44556-107">Hello éléments et attributs utilisés dans la définition de hello de module personnalisé de hello sont ensuite décrits plus en détail.</span><span class="sxs-lookup"><span data-stu-id="44556-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="44556-108">Comment les fonctionnalités auxiliaire toouse et les fichiers plusieurs sorties est également présenté.</span><span class="sxs-lookup"><span data-stu-id="44556-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="44556-109">Qu’est-ce qu’un module R personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="44556-109">What is a custom R module?</span></span>
<span data-ttu-id="44556-110">A **module personnalisé** est un module défini par l’utilisateur qui peut être téléchargés tooyour espace de travail et exécutée au sein d’une expérience Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="44556-111">Un **module R personnalisé** est un module exécutant une fonction R définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44556-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="44556-112">**R** est un langage de programmation utilisé pour le traitement informatique des statistiques et les graphiques. Les chercheurs de données et les statisticiens s’en servent pour implémenter des algorithmes.</span><span class="sxs-lookup"><span data-stu-id="44556-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="44556-113">Actuellement, R est hello seule langue prise en charge dans des modules personnalisés, mais prise en charge de langues supplémentaires est planifiée pour les versions futures.</span><span class="sxs-lookup"><span data-stu-id="44556-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="44556-114">Les modules personnalisés ont **état de première classe** dans Azure Machine Learning dans les sens hello qu’elles peuvent être utilisées comme tout autre module.</span><span class="sxs-lookup"><span data-stu-id="44556-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="44556-115">Ils peuvent être exécutés avec d’autres modules, inclus dans des expériences publiées ou dans des visualisations.</span><span class="sxs-lookup"><span data-stu-id="44556-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="44556-116">Vous contrôlez algorithme hello implémenté par le module de hello, hello toobe de ports d’entrée et de sortie utilisé, hello des paramètres de modélisation et d’autres comportements d’exécution différents.</span><span class="sxs-lookup"><span data-stu-id="44556-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="44556-117">Une expérience qui contient des modules personnalisés peut également être publiée dans hello Cortana Intelligence galerie pour partager facilement.</span><span class="sxs-lookup"><span data-stu-id="44556-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="44556-118">Fichiers dans un module R personnalisé</span><span class="sxs-lookup"><span data-stu-id="44556-118">Files in a custom R module</span></span>
<span data-ttu-id="44556-119">Un module R personnalisé est défini par un fichier .zip contenant au moins deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="44556-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="44556-120">A **fichier source** qui implémente la fonction hello R exposée par le module de hello</span><span class="sxs-lookup"><span data-stu-id="44556-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="44556-121">Un **fichier de définition XML** qui décrit l’interface de module personnalisé hello</span><span class="sxs-lookup"><span data-stu-id="44556-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="44556-122">Autres fichiers auxiliaires peuvent également être inclus dans le fichier .zip hello qui fournit des fonctionnalités qui sont accessibles à partir de modules personnalisés de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="44556-123">Cette option est décrite dans hello **Arguments** dans le cadre de la section de référence hello **éléments dans le fichier de définition XML hello** hello quickstart exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="44556-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="44556-124">Exemple de démarrage rapide : définir, mettre en package et enregistrer un module R personnalisé</span><span class="sxs-lookup"><span data-stu-id="44556-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="44556-125">Cet exemple illustre comment tooconstruct hello les fichiers requis par un module R personnalisé, empaqueter dans un fichier zip et module hello de Registre dans votre espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="44556-126">Hello exemple zip package et un exemple de fichiers peuvent être téléchargés à partir de [CustomAddRows.zip de télécharger le fichier](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="44556-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="44556-127">fichier de source de Hello</span><span class="sxs-lookup"><span data-stu-id="44556-127">hello source file</span></span>
<span data-ttu-id="44556-128">Considérez exemple hello d’un **personnalisé Add Rows** module qui modifie l’implémentation standard de hello Hello **Add Rows** module utilisé tooconcatenate lignes (observations) à partir de deux jeux de données (des trames de données).</span><span class="sxs-lookup"><span data-stu-id="44556-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="44556-129">Hello standard **Add Rows** module ajoute des lignes de hello fin hello deuxième jeu de données d’entrée toohello du jeu de données d’entrée première hello à l’aide de hello `rbind` algorithme.</span><span class="sxs-lookup"><span data-stu-id="44556-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="44556-130">Hello personnalisé `CustomAddRows` fonction accepte les deux jeux de données de la même façon, mais accepte également un paramètre booléen swap comme une entrée supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="44556-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="44556-131">Si la valeur du paramètre d’échange hello est trop**FALSE**, il retourne hello même jeu de données comme hello implémentation standard.</span><span class="sxs-lookup"><span data-stu-id="44556-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="44556-132">Mais si le paramètre d’échange hello est **TRUE**, fonction hello ajoute des lignes de fin de toohello premier jeu de données d’entrée de hello le deuxième jeu de données à la place.</span><span class="sxs-lookup"><span data-stu-id="44556-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="44556-133">fichier CustomAddRows.R Hello qui contient l’implémentation de hello Hello R `CustomAddRows` fonction exposée par hello **personnalisé Add Rows** module a hello suivant le code R.</span><span class="sxs-lookup"><span data-stu-id="44556-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

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

### <a name="hello-xml-definition-file"></a><span data-ttu-id="44556-134">fichier de définition XML Hello</span><span class="sxs-lookup"><span data-stu-id="44556-134">hello XML definition file</span></span>
<span data-ttu-id="44556-135">tooexpose cela `CustomAddRows` fonctionne comme un module d’Azure Machine Learning, un fichier de définition XML doit être créé toospecify comment hello **personnalisé Add Rows** module doit ressemblent et se comportent.</span><span class="sxs-lookup"><span data-stu-id="44556-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="44556-136">Il est critique toonote qui hello valeur Hello **id** attributs Hello **entrée** et **Arg** éléments dans le fichier XML de hello doivent correspondre aux noms de paramètre de fonction de hello Hello R le code dans le fichier de CustomAddRows.R hello exactement : (*dataset1*, *dataset2*, et *échange* dans l’exemple de hello).</span><span class="sxs-lookup"><span data-stu-id="44556-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="44556-137">De même, hello valeur Hello **entryPoint** attribut Hello **langage** élément doit correspondre exactement au nom de hello de fonction hello dans le script de hello R : (*CustomAddRows* dans l’exemple hello).</span><span class="sxs-lookup"><span data-stu-id="44556-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="44556-138">En revanche, hello **id** attribut pour hello **sortie** élément ne correspond pas tooany les variables de script de hello R.</span><span class="sxs-lookup"><span data-stu-id="44556-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="44556-139">Quand plusieurs sorties est requis, se contentent de retourner une liste à partir de la fonction hello R résultats placés *Bonjour même ordre* en tant que **sorties** sont déclarés dans le fichier XML de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="44556-140">Package et inscrire le module de hello</span><span class="sxs-lookup"><span data-stu-id="44556-140">Package and register hello module</span></span>
<span data-ttu-id="44556-141">Enregistrez ces deux fichiers comme *CustomAddRows.R* et *CustomAddRows.xml* et puis zip hello ensemble la deux fichiers dans un *CustomAddRows.zip* fichier.</span><span class="sxs-lookup"><span data-stu-id="44556-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="44556-142">tooregister dans votre espace de travail Machine Learning, espace de travail tooyour accédez hello Machine Learning Studio, cliquez sur hello **+ nouveau** bouton bas de hello **MODULE -> à partir de PACKAGE ZIP** tooupload Hello nouvelle **personnalisé Add Rows** module.</span><span class="sxs-lookup"><span data-stu-id="44556-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Charger les zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="44556-144">Hello **personnalisé Add Rows** module est désormais prêt toobe accédé par vos expériences d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="44556-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="44556-145">Éléments dans le fichier de définition XML hello</span><span class="sxs-lookup"><span data-stu-id="44556-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="44556-146">Éléments de module</span><span class="sxs-lookup"><span data-stu-id="44556-146">Module elements</span></span>
<span data-ttu-id="44556-147">Hello **Module** élément est toodefine utilisé un module personnalisé dans le fichier XML de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="44556-148">Plusieurs modules peuvent être définis dans un fichier XML à l’aide de plusieurs éléments **module** .</span><span class="sxs-lookup"><span data-stu-id="44556-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="44556-149">Chaque module de votre espace de travail doit avoir un nom unique.</span><span class="sxs-lookup"><span data-stu-id="44556-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="44556-150">Enregistrer un module personnalisé avec le même nom qu’un module personnalisé existant de hello et il remplace un module existant de hello hello nouveau.</span><span class="sxs-lookup"><span data-stu-id="44556-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="44556-151">Modules personnalisés peuvent, toutefois, être inscrit avec hello comme un module Azure Machine Learning existant du même nom.</span><span class="sxs-lookup"><span data-stu-id="44556-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="44556-152">Si elles apparaissent donc, Bonjour **personnalisé** catégorie de la palette de module hello.</span><span class="sxs-lookup"><span data-stu-id="44556-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="44556-153">Au sein de hello **Module** élément, vous pouvez spécifier deux éléments facultatifs supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="44556-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="44556-154">un **propriétaire** élément imbriqué dans le module de hello</span><span class="sxs-lookup"><span data-stu-id="44556-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="44556-155">un **Description** élément qui contient le texte qui s’affiche dans l’aide rapide pour le module de hello et lorsque vous pointez sur le module hello Bonjour l’interface utilisateur de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="44556-156">Règles pour les limites de caractères dans les éléments de Module hello :</span><span class="sxs-lookup"><span data-stu-id="44556-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="44556-157">Hello valeur Hello **nom** attribut Bonjour **Module** élément ne doit pas dépasser 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="44556-158">Hello contenu Hello **Description** élément ne doit pas dépasser 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="44556-159">Hello contenu Hello **propriétaire** élément ne doit pas dépasser 32 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="44556-160">Les résultats d’un module peuvent être déterministes ou nondeterministic.* * par défaut, tous les modules sont considérés comme toobe déterministe.</span><span class="sxs-lookup"><span data-stu-id="44556-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="44556-161">Autrement dit, étant donné un jeu qui ne changent pas de paramètres d’entrée et de données, le module de hello doit retourner hello mêmes résultats eacRAND ou un functionh de son exécution.</span><span class="sxs-lookup"><span data-stu-id="44556-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="44556-162">Étant donné ce comportement, Azure Machine Learning Studio réexécute uniquement les modules marqués comme étant déterministe si un paramètre ou les données d’entrée hello a changé.</span><span class="sxs-lookup"><span data-stu-id="44556-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="44556-163">Retour des résultats de hello mis en cache fournit également une exécution beaucoup plus rapide d’expériences.</span><span class="sxs-lookup"><span data-stu-id="44556-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="44556-164">Il existe des fonctions qui sont non déterministes, telles que RAND ou une fonction qui retourne la date ou l’heure de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="44556-165">Si votre module utilise une fonction non déterministe, vous pouvez spécifier que le module hello est non déterministe par hello de paramètre facultatif **isDeterministic** trop d’attributs**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="44556-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="44556-166">Cela garantit que le module hello est exécuté à nouveau à chaque exécution de l’expérience de hello, même si hello module Paramètres d’entrée et n’ont pas changé.</span><span class="sxs-lookup"><span data-stu-id="44556-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="44556-167">Définition de l’élément Language</span><span class="sxs-lookup"><span data-stu-id="44556-167">Language Definition</span></span>
<span data-ttu-id="44556-168">Hello **langage** élément dans votre fichier de définition XML est la langue de module personnalisé utilisé toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="44556-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="44556-169">Actuellement, R est hello uniquement prise en charge de langue.</span><span class="sxs-lookup"><span data-stu-id="44556-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="44556-170">Hello valeur Hello **sourceFile** attribut doit être le nom hello du fichier hello R contenant hello fonction toocall lors de l’exécution de module de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="44556-171">Ce fichier doit faire partie du package zip de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="44556-172">Hello valeur Hello **entryPoint** attribut est le nom hello de fonction hello appelée et doit correspondre à une fonction valide définie dans le fichier de source de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="44556-173">Ports</span><span class="sxs-lookup"><span data-stu-id="44556-173">Ports</span></span>
<span data-ttu-id="44556-174">les ports d’entrée et de sortie pour un module personnalisé Hello sont spécifiés dans les éléments enfants de hello **Ports** section hello XML du fichier de définition.</span><span class="sxs-lookup"><span data-stu-id="44556-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="44556-175">commande Hello de ces éléments détermine hello disposition expérimentée (UX) par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="44556-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="44556-176">premier enfant de Hello **d’entrée** ou **sortie** répertoriés dans hello **Ports** élément du fichier XML de hello devienne le port d’entrée de la plus à gauche hello Bonjour Machine Learning UX</span><span class="sxs-lookup"><span data-stu-id="44556-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="44556-177">Chaque d’entrée et de port de sortie peut-être avoir facultatif **Description** élément enfant qui spécifie le texte hello lorsque vous pointez la souris hello sur port hello Bonjour l’interface utilisateur de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="44556-178">**Règles relatives aux ports**:</span><span class="sxs-lookup"><span data-stu-id="44556-178">**Ports Rules**:</span></span>

* <span data-ttu-id="44556-179">Le nombre maximum de **ports d’entrée et de sortie** est de 8 pour chacun.</span><span class="sxs-lookup"><span data-stu-id="44556-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="44556-180">Éléments d'entrée</span><span class="sxs-lookup"><span data-stu-id="44556-180">Input elements</span></span>
<span data-ttu-id="44556-181">Ports d’entrée vous permettent d’espace de travail et la fonction tooyour R toopass données.</span><span class="sxs-lookup"><span data-stu-id="44556-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="44556-182">Hello **des types de données** qui sont pris en charge pour les ports d’entrée sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="44556-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="44556-183">**DataTable :** ce type est passé de tooyour R fonction comme un data.frame.</span><span class="sxs-lookup"><span data-stu-id="44556-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="44556-184">En fait, tous les types (par exemple, des fichiers CSV ou des fichiers ARFF) sont pris en charge par l’apprentissage automatique et qui sont compatibles avec **DataTable** sont convertis tooa data.frame automatiquement.</span><span class="sxs-lookup"><span data-stu-id="44556-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="44556-185">Hello **id** attribut associée à chaque **DataTable** port d’entrée doit avoir une valeur unique, et cette valeur doit correspondre à son paramètre dans votre fonction R nommé correspondant.</span><span class="sxs-lookup"><span data-stu-id="44556-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="44556-186">Facultatif **DataTable** ports qui ne sont pas transmis en tant qu’entrée dans une expérience ont la valeur de hello **NULL** toohello passé R fonction et les ports de zip facultatif sont ignorés si hello entrée n’est pas connectée.</span><span class="sxs-lookup"><span data-stu-id="44556-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="44556-187">Hello **isOptional** attribut est facultatif pour les deux hello **DataTable** et **Zip** les types et est *false* par défaut.</span><span class="sxs-lookup"><span data-stu-id="44556-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="44556-188">**Zip :** modules personnalisés pouvant accepter un fichier .zip en entrée.</span><span class="sxs-lookup"><span data-stu-id="44556-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="44556-189">Cette entrée est décompressée dans le répertoire de travail hello R de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="44556-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="44556-190">Pour les modules R personnalisés, hello id pour un port Zip n’est pas toomatch tous les paramètres de fonction hello R.</span><span class="sxs-lookup"><span data-stu-id="44556-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="44556-191">Il s’agit, car le fichier zip de hello est le répertoire de travail automatiquement extraits toohello R.</span><span class="sxs-lookup"><span data-stu-id="44556-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="44556-192">**Règles d'entrée :**</span><span class="sxs-lookup"><span data-stu-id="44556-192">**Input Rules:**</span></span>

* <span data-ttu-id="44556-193">Hello valeur Hello **id** attribut Hello **entrée** élément doit être un nom de variable R valide.</span><span class="sxs-lookup"><span data-stu-id="44556-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="44556-194">Hello valeur Hello **id** attribut Hello **entrée** élément ne doit pas comporter plu de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="44556-195">Hello valeur Hello **nom** attribut Hello **entrée** élément ne doit pas comporter plu de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="44556-196">Hello contenu Hello **Description** élément ne doit pas comporter plu de 128 caractères</span><span class="sxs-lookup"><span data-stu-id="44556-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="44556-197">Hello valeur Hello **type** attribut Hello **entrée** l’élément doit être *Zip* ou *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="44556-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="44556-198">Hello valeur Hello **isOptional** attribut Hello **entrée** élément n’est pas obligatoire (et est *false* par défaut lorsque ne pas spécifié) ; mais s’il est spécifié, il doit être *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="44556-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="44556-199">Éléments d’entrée</span><span class="sxs-lookup"><span data-stu-id="44556-199">Output elements</span></span>
<span data-ttu-id="44556-200">**Ports de sortie standard :** ports de sortie sont des valeurs de retour toohello mappé à partir de votre fonction R, qui peut ensuite être utilisé par les modules suivants.</span><span class="sxs-lookup"><span data-stu-id="44556-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="44556-201">*DataTable* est de type de port de sortie standard uniquement hello actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="44556-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="44556-202">(Les types *Learners* et *Transformers* seront prochainement pris en charge.) Une sortie *DataTable* est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="44556-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="44556-203">Pour les sorties dans des modules R personnalisés, hello valeur Hello **id** attribut n’a pas de toocorrespond avec quoi que ce soit dans le script de hello R, mais il doit être unique.</span><span class="sxs-lookup"><span data-stu-id="44556-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="44556-204">Pour une sortie de module unique, la valeur de retour de hello à partir de la fonction hello R doit être un *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="44556-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="44556-205">Dans commande toooutput plusieurs objets d’un type de données pris en charge, ports de sortie appropriée de hello doivent toobe spécifié dans le fichier de définition XML hello et objets de hello doivent toobe retournée sous forme de liste.</span><span class="sxs-lookup"><span data-stu-id="44556-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="44556-206">objets de sortie Hello assignés toooutput ports à partir de la gauche tooright, refléter l’ordre hello dans lequel les objets de hello sont placés dans hello retourné la liste.</span><span class="sxs-lookup"><span data-stu-id="44556-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="44556-207">Par exemple, si vous souhaitez toomodify hello **personnalisé Add Rows** module toooutput hello deux jeux de données d’origine, *dataset1* et *dataset2*, en outre toohello nouveau joint jeu de données, *dataset*, (dans un ordre, de gauche tooright, en tant que : *dataset*, *dataset1*, *dataset2*), puis définissez hello la sortie des ports dans le fichier de CustomAddRows.xml hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44556-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="44556-208">Et retourne la liste hello des objets dans une liste dans l’ordre correct de hello dans 'CustomAddRows.R' :</span><span class="sxs-lookup"><span data-stu-id="44556-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="44556-209">**Sortie de visualisation :** vous pouvez également spécifier un port de sortie de type *visualisation*, qui affiche le contenu de hello à partir de la sortie de console et de périphérique graphique hello R.</span><span class="sxs-lookup"><span data-stu-id="44556-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="44556-210">Ce port ne fait pas partie de la sortie de fonction hello R et n’interfère pas avec la commande hello Hello d’autres types de port de sortie.</span><span class="sxs-lookup"><span data-stu-id="44556-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="44556-211">Ajout d’une visualisation port toohello des modules personnalisés, tooadd un **sortie** élément avec la valeur *visualisation* pour son **type** attribut :</span><span class="sxs-lookup"><span data-stu-id="44556-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="44556-212">**Règles de sortie :**</span><span class="sxs-lookup"><span data-stu-id="44556-212">**Output Rules:**</span></span>

* <span data-ttu-id="44556-213">Hello valeur Hello **id** attribut Hello **sortie** élément doit être un nom de variable R valide.</span><span class="sxs-lookup"><span data-stu-id="44556-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="44556-214">Hello valeur Hello **id** attribut Hello **sortie** élément ne doit pas comporter plu de 32 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="44556-215">Hello valeur Hello **nom** attribut Hello **sortie** élément ne doit pas comporter plu de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="44556-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="44556-216">Hello valeur Hello **type** attribut Hello **sortie** l’élément doit être *visualisation*.</span><span class="sxs-lookup"><span data-stu-id="44556-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="44556-217">Arguments</span><span class="sxs-lookup"><span data-stu-id="44556-217">Arguments</span></span>
<span data-ttu-id="44556-218">Données supplémentaires peuvent être passées toohello R fonction via les paramètres du module qui sont définies dans hello **Arguments** élément.</span><span class="sxs-lookup"><span data-stu-id="44556-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="44556-219">Ces paramètres apparaissent dans le volet de propriétés plus à droite de hello Hello l’interface utilisateur de Machine Learning lorsque le module de hello est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="44556-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="44556-220">Les arguments peuvent être des types de hello pris en charge, ou vous pouvez créer une énumération personnalisée si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="44556-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="44556-221">Similaire toohello **Ports** éléments, **Arguments** les éléments peuvent avoir facultatif **Description** élément qui spécifie le texte hello qui s’affiche lorsque vous pointez la souris de hello sur le nom du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="44556-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="44556-222">Argument tooany comme tooa d’attributs peuvent être ajoutées à des propriétés facultatives pour un module, tels que defaultValue, minValue et maxValue **propriétés** élément.</span><span class="sxs-lookup"><span data-stu-id="44556-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="44556-223">Les propriétés valides pour hello **propriétés** élément varie selon le type d’argument hello et sont décrites avec les types d’arguments hello pris en charge dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="44556-224">Arguments par hello **isOptional** propriété trop**« true »** ne nécessitent pas de hello utilisateur tooenter une valeur.</span><span class="sxs-lookup"><span data-stu-id="44556-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="44556-225">Si aucune valeur n’est pas fournie toohello argument, argument de hello n’est passé toohello fonction de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="44556-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="44556-226">Arguments de fonction de point d’entrée hello toobe besoin facultatif géré explicitement par la fonction hello, affecté par exemple, une valeur par défaut NULL dans la définition de fonction de point d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="44556-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="44556-227">Applique un argument facultatif hello autres contraintes d’argument, par exemple, min ou max, si une valeur est fournie par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="44556-228">Comme avec les entrées et sorties, il est essentiel que chacun des paramètres de hello ont des valeurs d’id unique qui s’y rapportent.</span><span class="sxs-lookup"><span data-stu-id="44556-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="44556-229">Dans notre Guide de démarrage rapide exemple hello associé le paramètre d’id a été *swap*.</span><span class="sxs-lookup"><span data-stu-id="44556-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="44556-230">Élément Arg</span><span class="sxs-lookup"><span data-stu-id="44556-230">Arg element</span></span>
<span data-ttu-id="44556-231">Un module est défini à l’aide de hello **Arg** élément enfant de hello **Arguments** section hello XML du fichier de définition.</span><span class="sxs-lookup"><span data-stu-id="44556-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="44556-232">Comme avec les éléments enfants de hello Bonjour **Ports** section, hello organisation des paramètres Bonjour **Arguments** section définit la disposition de hello rencontrée Bonjour UX.</span><span class="sxs-lookup"><span data-stu-id="44556-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="44556-233">Hello paramètres apparaissent à partir du haut vers le bas dans l’interface utilisateur de hello Bonjour ordre dans lequel ils sont définis dans le fichier XML de hello.</span><span class="sxs-lookup"><span data-stu-id="44556-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="44556-234">types de Hello pris en charge par l’apprentissage automatique pour les paramètres sont répertoriés ici.</span><span class="sxs-lookup"><span data-stu-id="44556-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="44556-235">**int** : paramètre de type entier (32 bits).</span><span class="sxs-lookup"><span data-stu-id="44556-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="44556-236">*Propriétés facultatives* : **min**, **max**, **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="44556-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="44556-237">**double** : paramètre de type double.</span><span class="sxs-lookup"><span data-stu-id="44556-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="44556-238">*Propriétés facultatives* : **min**, **max**, **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="44556-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="44556-239">**bool** : paramètre booléen représenté par une case à cocher dans l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44556-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="44556-240">*Propriétés facultatives* : **default**. False si non défini</span><span class="sxs-lookup"><span data-stu-id="44556-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="44556-241">**string**: chaîne standard</span><span class="sxs-lookup"><span data-stu-id="44556-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="44556-242">*Propriétés facultatives* : **default** et **isOptional**</span><span class="sxs-lookup"><span data-stu-id="44556-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="44556-243">**ColumnPicker**: paramètre de sélection de colonne.</span><span class="sxs-lookup"><span data-stu-id="44556-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="44556-244">Ce type de rendu Bonjour UX sous la forme d’un sélecteur de colonne.</span><span class="sxs-lookup"><span data-stu-id="44556-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="44556-245">Hello **propriété** élément est utilisé toospecify ici les id de hello du port hello à partir de laquelle les colonnes sont sélectionnées, où le type de port hello cible doit être *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="44556-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="44556-246">résultat de Hello de sélection de la colonne hello est passé toohello R fonction sous forme de liste de chaînes contenant les noms de colonne hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="44556-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="44556-247">*Propriétés requises*: **portId** -correspondances hello id d’un élément d’entrée avec le type *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="44556-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="44556-248">*Propriétés facultatives*:</span><span class="sxs-lookup"><span data-stu-id="44556-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="44556-249">**allowedTypes** -types de colonne de hello de filtres à partir de laquelle vous pouvez choisir.</span><span class="sxs-lookup"><span data-stu-id="44556-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="44556-250">Les valeurs valides incluent :</span><span class="sxs-lookup"><span data-stu-id="44556-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="44556-251">Chiffre</span><span class="sxs-lookup"><span data-stu-id="44556-251">Numeric</span></span>
    * <span data-ttu-id="44556-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="44556-252">Boolean</span></span>
    * <span data-ttu-id="44556-253">Par catégorie</span><span class="sxs-lookup"><span data-stu-id="44556-253">Categorical</span></span>
    * <span data-ttu-id="44556-254">string</span><span class="sxs-lookup"><span data-stu-id="44556-254">String</span></span>
    * <span data-ttu-id="44556-255">Étiquette</span><span class="sxs-lookup"><span data-stu-id="44556-255">Label</span></span>
    * <span data-ttu-id="44556-256">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="44556-256">Feature</span></span>
    * <span data-ttu-id="44556-257">Score</span><span class="sxs-lookup"><span data-stu-id="44556-257">Score</span></span>
    * <span data-ttu-id="44556-258">Tout</span><span class="sxs-lookup"><span data-stu-id="44556-258">All</span></span>
  * <span data-ttu-id="44556-259">**par défaut** -les sélections par défaut valide pour le sélecteur de colonne hello incluent :</span><span class="sxs-lookup"><span data-stu-id="44556-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="44556-260">Aucun</span><span class="sxs-lookup"><span data-stu-id="44556-260">None</span></span>
    * <span data-ttu-id="44556-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="44556-261">NumericFeature</span></span>
    * <span data-ttu-id="44556-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="44556-262">NumericLabel</span></span>
    * <span data-ttu-id="44556-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="44556-263">NumericScore</span></span>
    * <span data-ttu-id="44556-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="44556-264">NumericAll</span></span>
    * <span data-ttu-id="44556-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="44556-265">BooleanFeature</span></span>
    * <span data-ttu-id="44556-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="44556-266">BooleanLabel</span></span>
    * <span data-ttu-id="44556-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="44556-267">BooleanScore</span></span>
    * <span data-ttu-id="44556-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="44556-268">BooleanAll</span></span>
    * <span data-ttu-id="44556-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="44556-269">CategoricalFeature</span></span>
    * <span data-ttu-id="44556-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="44556-270">CategoricalLabel</span></span>
    * <span data-ttu-id="44556-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="44556-271">CategoricalScore</span></span>
    * <span data-ttu-id="44556-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="44556-272">CategoricalAll</span></span>
    * <span data-ttu-id="44556-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="44556-273">StringFeature</span></span>
    * <span data-ttu-id="44556-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="44556-274">StringLabel</span></span>
    * <span data-ttu-id="44556-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="44556-275">StringScore</span></span>
    * <span data-ttu-id="44556-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="44556-276">StringAll</span></span>
    * <span data-ttu-id="44556-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="44556-277">AllLabel</span></span>
    * <span data-ttu-id="44556-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="44556-278">AllFeature</span></span>
    * <span data-ttu-id="44556-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="44556-279">AllScore</span></span>
    * <span data-ttu-id="44556-280">Tout</span><span class="sxs-lookup"><span data-stu-id="44556-280">All</span></span>

<span data-ttu-id="44556-281">**DropDown**: liste (déroulante) énumérée spécifiée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44556-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="44556-282">les éléments de liste déroulante Hello sont spécifiés dans hello **propriétés** à l’aide de l’élément une **élément** élément.</span><span class="sxs-lookup"><span data-stu-id="44556-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="44556-283">Hello **id** pour chaque **élément** doit être unique et une variable R valide.</span><span class="sxs-lookup"><span data-stu-id="44556-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="44556-284">Hello valeur Hello **nom** d’un **élément** sert de texte hello que vous voyez et valeur hello toohello R fonction passée.</span><span class="sxs-lookup"><span data-stu-id="44556-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="44556-285">*Propriétés facultatives*:</span><span class="sxs-lookup"><span data-stu-id="44556-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="44556-286">**par défaut** hello - valeur de propriété par défaut de hello doit correspondre à une valeur d’id de l’une des hello **élément** éléments.</span><span class="sxs-lookup"><span data-stu-id="44556-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="44556-287">Fichiers auxiliaires</span><span class="sxs-lookup"><span data-stu-id="44556-287">Auxiliary Files</span></span>
<span data-ttu-id="44556-288">N’importe quel fichier qui est placé dans votre fichier ZIP de module personnalisé est toobe cours disponible pour une utilisation pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="44556-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="44556-289">Toutes les structures de répertoire présentes sont conservées.</span><span class="sxs-lookup"><span data-stu-id="44556-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="44556-290">Cela signifie que works d’approvisionnement fichier hello même localement et dans l’exécution d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44556-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="44556-291">Notez que tous les fichiers sont extraits too'src' directory pour tous les chemins doivent avoir ' src /' préfixe.</span><span class="sxs-lookup"><span data-stu-id="44556-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="44556-292">Par exemple, supposons que vous souhaitez tooremove les lignes avec NAs hello dataset, également supprimez toutes les lignes en double, avant de sortir dans CustomAddRows et que vous avez déjà écrit une fonction R qui fait que dans un fichier RemoveDupNARows.R :</span><span class="sxs-lookup"><span data-stu-id="44556-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="44556-293">Vous pouvez de source de fichier auxiliaire hello RemoveDupNARows.R Bonjour CustomAddRows fonction :</span><span class="sxs-lookup"><span data-stu-id="44556-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

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

<span data-ttu-id="44556-294">Ensuite, chargez un fichier .zip contenant les éléments « CustomAddRows.R », « CustomAddRows.xml » et « RemoveDupNARows.R » en tant que module R personnalisé.</span><span class="sxs-lookup"><span data-stu-id="44556-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="44556-295">Environnement d’exécution</span><span class="sxs-lookup"><span data-stu-id="44556-295">Execution Environment</span></span>
<span data-ttu-id="44556-296">environnement d’exécution Hello pour le script de hello R utilise hello même version de R que hello **Execute R Script** module et vous pouvez utiliser hello même par défaut des packages.</span><span class="sxs-lookup"><span data-stu-id="44556-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="44556-297">Vous pouvez également ajouter supplémentaire module personnalisé R packages tooyour en les incluant dans le package zip de module personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="44556-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="44556-298">Chargez-les simplement dans votre script R comme vous le feriez dans votre propre environnement R.</span><span class="sxs-lookup"><span data-stu-id="44556-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="44556-299">**Limitations de l’environnement d’exécution hello** incluent :</span><span class="sxs-lookup"><span data-stu-id="44556-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="44556-300">Système de fichiers non persistants : fichiers écrits lors de l’exécution de module personnalisé de hello ne sont pas conservés entre les différentes exécutions de hello même module.</span><span class="sxs-lookup"><span data-stu-id="44556-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="44556-301">Pas d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="44556-301">No network access</span></span>

