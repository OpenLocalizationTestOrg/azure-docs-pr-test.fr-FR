---
title: "Créer des artefacts personnalisés pour votre machine virtuelle DevTest Labs | Microsoft Docs"
description: "Découvrez comment créer vos propres artefacts pour les utiliser avec DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="36edd-103">Créer des artefacts personnalisés pour vos machines virtuelles DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="36edd-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="36edd-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="36edd-104">Overview</span></span>
<span data-ttu-id="36edd-105">**artefacts** sont utilisés pour déployer et configurer votre application après l’approvisionnement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36edd-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="36edd-106">Un artefact se compose d'un fichier de définition d'artefact et autres fichiers de script qui sont stockés dans un dossier de dépôt git.</span><span class="sxs-lookup"><span data-stu-id="36edd-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="36edd-107">Les fichiers de définition d'artefact se composent de JSON et d'expressions que vous pouvez utiliser pour spécifier ce que vous voulez installer sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36edd-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="36edd-108">Par exemple, vous pouvez définir le nom d’un artefact, une commande à exécuter et des paramètres disponibles lorsque la commande est exécutée.</span><span class="sxs-lookup"><span data-stu-id="36edd-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="36edd-109">Vous pouvez faire référence à d'autres fichiers de script dans le fichier de définition d'artefact par nom.</span><span class="sxs-lookup"><span data-stu-id="36edd-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="36edd-110">Format de fichier de définition d'artefact</span><span class="sxs-lookup"><span data-stu-id="36edd-110">Artifact definition file format</span></span>
<span data-ttu-id="36edd-111">L'exemple suivant indique les sections qui composent la structure de base d'un fichier de définition :</span><span class="sxs-lookup"><span data-stu-id="36edd-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="36edd-112">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36edd-112">Element name</span></span> | <span data-ttu-id="36edd-113">Requis ?</span><span class="sxs-lookup"><span data-stu-id="36edd-113">Required?</span></span> | <span data-ttu-id="36edd-114">Description</span><span class="sxs-lookup"><span data-stu-id="36edd-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36edd-115">$schema</span><span class="sxs-lookup"><span data-stu-id="36edd-115">$schema</span></span> |<span data-ttu-id="36edd-116">Non</span><span class="sxs-lookup"><span data-stu-id="36edd-116">No</span></span> |<span data-ttu-id="36edd-117">Emplacement du fichier de schéma JSON qui permet de tester la validité du fichier de définition.</span><span class="sxs-lookup"><span data-stu-id="36edd-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="36edd-118">title</span><span class="sxs-lookup"><span data-stu-id="36edd-118">title</span></span> |<span data-ttu-id="36edd-119">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-119">Yes</span></span> |<span data-ttu-id="36edd-120">Nom de l'artefact affiché dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="36edd-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="36edd-121">Description</span><span class="sxs-lookup"><span data-stu-id="36edd-121">description</span></span> |<span data-ttu-id="36edd-122">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-122">Yes</span></span> |<span data-ttu-id="36edd-123">Description de l'artefact affiché dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="36edd-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="36edd-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="36edd-124">iconUri</span></span> |<span data-ttu-id="36edd-125">Non</span><span class="sxs-lookup"><span data-stu-id="36edd-125">No</span></span> |<span data-ttu-id="36edd-126">URI de l'icône affichée dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="36edd-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="36edd-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="36edd-127">targetOsType</span></span> |<span data-ttu-id="36edd-128">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-128">Yes</span></span> |<span data-ttu-id="36edd-129">Système d'exploitation de la machine virtuelle où l'artefact sera installé.</span><span class="sxs-lookup"><span data-stu-id="36edd-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="36edd-130">Les options prises en charge sont : Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="36edd-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="36edd-131">parameters</span><span class="sxs-lookup"><span data-stu-id="36edd-131">parameters</span></span> |<span data-ttu-id="36edd-132">Non</span><span class="sxs-lookup"><span data-stu-id="36edd-132">No</span></span> |<span data-ttu-id="36edd-133">Les valeurs fournies lorsque la commande d'installation d'artefact est exécutée sur une machine.</span><span class="sxs-lookup"><span data-stu-id="36edd-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="36edd-134">Cela permet de personnaliser votre artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="36edd-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="36edd-135">runCommand</span></span> |<span data-ttu-id="36edd-136">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-136">Yes</span></span> |<span data-ttu-id="36edd-137">Commande d'installation d'artefact qui est exécutée sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36edd-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="36edd-138">Paramètres d'artefact</span><span class="sxs-lookup"><span data-stu-id="36edd-138">Artifact parameters</span></span>
<span data-ttu-id="36edd-139">Dans la section des paramètres du fichier de définition, vous spécifiez les valeurs qu'un utilisateur peut entrer lors de l'installation d'un artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="36edd-140">Vous pouvez faire référence à ces valeurs dans la commande d'installation d'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="36edd-141">Vous définissez des paramètres avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="36edd-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="36edd-142">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36edd-142">Element name</span></span> | <span data-ttu-id="36edd-143">Requis ?</span><span class="sxs-lookup"><span data-stu-id="36edd-143">Required?</span></span> | <span data-ttu-id="36edd-144">Description</span><span class="sxs-lookup"><span data-stu-id="36edd-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36edd-145">type</span><span class="sxs-lookup"><span data-stu-id="36edd-145">type</span></span> |<span data-ttu-id="36edd-146">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-146">Yes</span></span> |<span data-ttu-id="36edd-147">Type de la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="36edd-147">Type of parameter value.</span></span> <span data-ttu-id="36edd-148">Consultez la liste suivante des types autorisés :</span><span class="sxs-lookup"><span data-stu-id="36edd-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="36edd-149">displayName</span><span class="sxs-lookup"><span data-stu-id="36edd-149">displayName</span></span> |<span data-ttu-id="36edd-150">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-150">Yes</span></span> |<span data-ttu-id="36edd-151">Nom du paramètre qui est affiché à un utilisateur dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="36edd-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="36edd-152">Description</span><span class="sxs-lookup"><span data-stu-id="36edd-152">description</span></span> |<span data-ttu-id="36edd-153">Oui</span><span class="sxs-lookup"><span data-stu-id="36edd-153">Yes</span></span> |<span data-ttu-id="36edd-154">Description du paramètre qui est affiché dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="36edd-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="36edd-155">Les types autorisés sont :</span><span class="sxs-lookup"><span data-stu-id="36edd-155">The allowed types are:</span></span>

* <span data-ttu-id="36edd-156">string : n'importe quelle chaîne JSON valide</span><span class="sxs-lookup"><span data-stu-id="36edd-156">string – any valid JSON string</span></span>
* <span data-ttu-id="36edd-157">int : n'importe quel entier JSON valide</span><span class="sxs-lookup"><span data-stu-id="36edd-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="36edd-158">bool : n'importe quel booléen JSON valide </span><span class="sxs-lookup"><span data-stu-id="36edd-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="36edd-159">array : n'importe quel tableau JSON valide</span><span class="sxs-lookup"><span data-stu-id="36edd-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="36edd-160">Expressions et fonctions d'artefact</span><span class="sxs-lookup"><span data-stu-id="36edd-160">Artifact expressions and functions</span></span>
<span data-ttu-id="36edd-161">Vous pouvez utiliser une expression et des fonctions pour construire la commande d'installation d'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="36edd-162">Les expressions sont placées entre crochets ([ et ]) et sont évaluées au moment où l'artefact est installé.</span><span class="sxs-lookup"><span data-stu-id="36edd-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="36edd-163">Les expressions peuvent apparaître n'importe où dans une valeur de chaîne JSON et retournent toujours une autre valeur JSON.</span><span class="sxs-lookup"><span data-stu-id="36edd-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="36edd-164">Si vous avez besoin d'utiliser une chaîne littérale qui commence par un crochet [, vous devez utiliser deux crochets [[.</span><span class="sxs-lookup"><span data-stu-id="36edd-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="36edd-165">En général, vous utilisez des expressions avec des fonctions pour construire une valeur.</span><span class="sxs-lookup"><span data-stu-id="36edd-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="36edd-166">Exactement comme dans JavaScript, les appels de fonctions sont mis en forme selon functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="36edd-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="36edd-167">La liste suivante indique les fonctions courantes :</span><span class="sxs-lookup"><span data-stu-id="36edd-167">The following list shows common functions:</span></span>

* <span data-ttu-id="36edd-168">parameters(parameterName) : renvoie une valeur de paramètre fournie lors de l'exécution de la commande de l'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="36edd-169">concat(arg1,arg2,arg3,...) : combine plusieurs valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="36edd-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="36edd-170">Cette fonction peut prendre n'importe quel nombre d'arguments.</span><span class="sxs-lookup"><span data-stu-id="36edd-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="36edd-171">L'exemple suivant indique comment utiliser les fonctions et l'expression pour construire une valeur :</span><span class="sxs-lookup"><span data-stu-id="36edd-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="36edd-172">Création d'un artefact personnalisé</span><span class="sxs-lookup"><span data-stu-id="36edd-172">Create a custom artifact</span></span>
<span data-ttu-id="36edd-173">Créez votre artefact personnalisé en suivant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="36edd-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="36edd-174">Installer un éditeur JSON : vous avez besoin d'un éditeur JSON pour utiliser les fichiers de définition d'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="36edd-175">Nous vous recommandons d'utiliser [Visual Studio Code](https://code.visualstudio.com/), qui est disponible pour Windows, Linux et OS X.</span><span class="sxs-lookup"><span data-stu-id="36edd-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="36edd-176">Obtenir un exemple d'artifactfile.json : découvrez les artefacts créés par l'équipe Azure DevTest Labs dans notre [référentiel GitHub](https://github.com/Azure/azure-devtestlab) où nous avons créé une bibliothèque d'artefacts riche qui vous permet de créer vos propres artefacts.</span><span class="sxs-lookup"><span data-stu-id="36edd-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="36edd-177">Téléchargez un fichier de définition d'artefact et modifiez-le pour créer vos propres artefacts.</span><span class="sxs-lookup"><span data-stu-id="36edd-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="36edd-178">Utiliser IntelliSense : utilisez IntelliSense pour voir des éléments valides qui peuvent être utilisés pour construire un fichier de définition d'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="36edd-179">Vous pouvez également voir les différentes options pour les valeurs d'un élément.</span><span class="sxs-lookup"><span data-stu-id="36edd-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="36edd-180">Par exemple, IntelliSense vous montre les deux options de Windows ou Linux lorsque vous modifiez l'élément **targetOsType** .</span><span class="sxs-lookup"><span data-stu-id="36edd-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="36edd-181">Stockez l'artefact dans un [référentiel git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="36edd-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="36edd-182">Créez un répertoire distinct pour chaque artefact où le nom du répertoire est le même que le nom de l'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="36edd-183">Stockez le fichier de définition d'artefact (artifactfile.json) dans le répertoire que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="36edd-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="36edd-184">Stockez les scripts qui sont référencés à partir de la commande d'installation d'artefact.</span><span class="sxs-lookup"><span data-stu-id="36edd-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="36edd-185">Voici un exemple de dossier d'artefact :</span><span class="sxs-lookup"><span data-stu-id="36edd-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Exemple de dépôt git d'artefacts](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="36edd-187">Ajoutez le référentiel d’artefacts au laboratoire : reportez-vous à l’article [Ajouter un référentiel Git d’artefacts et de modèles](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="36edd-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="36edd-188">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="36edd-188">Related articles</span></span>
* [<span data-ttu-id="36edd-189">Guide pratique pour diagnostiquer les échecs d’artefact dans DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="36edd-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="36edd-190">Joindre une machine virtuelle à un domaine AD existant à l’aide d’un modèle Resource Manager dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="36edd-190">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="36edd-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36edd-191">Next steps</span></span>
* <span data-ttu-id="36edd-192">Découvrez comment [ajouter un dépôt d’artefacts Git à un laboratoire](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="36edd-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

