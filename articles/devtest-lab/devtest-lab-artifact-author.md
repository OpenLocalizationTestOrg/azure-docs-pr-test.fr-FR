---
title: "aaaCreate des artefacts personnalisés pour votre machine de virtuelle DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooauthor vos propres artefacts pour utilisent avec DevTest Labs"
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
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="35799-103">Créer des artefacts personnalisés pour vos machines virtuelles DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="35799-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="35799-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="35799-104">Overview</span></span>
<span data-ttu-id="35799-105">**Artefacts** sont toodeploy utilisé et de configurer votre application après la configuration d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="35799-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="35799-106">Un artefact se compose d'un fichier de définition d'artefact et autres fichiers de script qui sont stockés dans un dossier de dépôt git.</span><span class="sxs-lookup"><span data-stu-id="35799-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="35799-107">Fichiers de définition d’artefact se composent de JSON et les expressions que vous pouvez utiliser toospecify ce que vous voulez tooinstall sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="35799-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="35799-108">Par exemple, vous pouvez définir nom hello d’un artefact, toorun de commande et les paramètres qui sont rendues disponibles lors de l’exécution de commande hello.</span><span class="sxs-lookup"><span data-stu-id="35799-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="35799-109">Vous pouvez faire référence à des fichiers de script tooother dans le fichier de définition d’artefact hello par nom.</span><span class="sxs-lookup"><span data-stu-id="35799-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="35799-110">Format de fichier de définition d'artefact</span><span class="sxs-lookup"><span data-stu-id="35799-110">Artifact definition file format</span></span>
<span data-ttu-id="35799-111">Hello suivant montre les sections hello qui composent la structure de base de hello d’un fichier de définition :</span><span class="sxs-lookup"><span data-stu-id="35799-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

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

| <span data-ttu-id="35799-112">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="35799-112">Element name</span></span> | <span data-ttu-id="35799-113">Requis ?</span><span class="sxs-lookup"><span data-stu-id="35799-113">Required?</span></span> | <span data-ttu-id="35799-114">Description</span><span class="sxs-lookup"><span data-stu-id="35799-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35799-115">$schema</span><span class="sxs-lookup"><span data-stu-id="35799-115">$schema</span></span> |<span data-ttu-id="35799-116">Non</span><span class="sxs-lookup"><span data-stu-id="35799-116">No</span></span> |<span data-ttu-id="35799-117">Emplacement du fichier de schéma JSON hello qui vous aide à tester la validité hello hello du fichier de définition.</span><span class="sxs-lookup"><span data-stu-id="35799-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="35799-118">title</span><span class="sxs-lookup"><span data-stu-id="35799-118">title</span></span> |<span data-ttu-id="35799-119">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-119">Yes</span></span> |<span data-ttu-id="35799-120">Nom de l’artefact de hello affiché dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="35799-121">description</span><span class="sxs-lookup"><span data-stu-id="35799-121">description</span></span> |<span data-ttu-id="35799-122">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-122">Yes</span></span> |<span data-ttu-id="35799-123">Description de l’artefact de hello affiché dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="35799-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="35799-124">iconUri</span></span> |<span data-ttu-id="35799-125">Non</span><span class="sxs-lookup"><span data-stu-id="35799-125">No</span></span> |<span data-ttu-id="35799-126">URI de l’icône de hello affichée dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="35799-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="35799-127">targetOsType</span></span> |<span data-ttu-id="35799-128">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-128">Yes</span></span> |<span data-ttu-id="35799-129">Système d’exploitation de hello où artefact est installée.</span><span class="sxs-lookup"><span data-stu-id="35799-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="35799-130">Les options prises en charge sont : Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="35799-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="35799-131">parameters</span><span class="sxs-lookup"><span data-stu-id="35799-131">parameters</span></span> |<span data-ttu-id="35799-132">Non</span><span class="sxs-lookup"><span data-stu-id="35799-132">No</span></span> |<span data-ttu-id="35799-133">Les valeurs fournies lorsque la commande d'installation d'artefact est exécutée sur une machine.</span><span class="sxs-lookup"><span data-stu-id="35799-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="35799-134">Cela permet de personnaliser votre artefact.</span><span class="sxs-lookup"><span data-stu-id="35799-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="35799-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="35799-135">runCommand</span></span> |<span data-ttu-id="35799-136">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-136">Yes</span></span> |<span data-ttu-id="35799-137">Commande d'installation d'artefact qui est exécutée sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="35799-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="35799-138">Paramètres d'artefact</span><span class="sxs-lookup"><span data-stu-id="35799-138">Artifact parameters</span></span>
<span data-ttu-id="35799-139">Dans la section Paramètres de hello hello du fichier de définition, vous spécifiez les valeurs d’un utilisateur peut entrer lors de l’installation d’un artefact.</span><span class="sxs-lookup"><span data-stu-id="35799-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="35799-140">Vous pouvez consulter les valeurs de toothese dans la commande d’installation artefact hello.</span><span class="sxs-lookup"><span data-stu-id="35799-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="35799-141">Vous définissez des paramètres par hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="35799-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="35799-142">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="35799-142">Element name</span></span> | <span data-ttu-id="35799-143">Requis ?</span><span class="sxs-lookup"><span data-stu-id="35799-143">Required?</span></span> | <span data-ttu-id="35799-144">Description</span><span class="sxs-lookup"><span data-stu-id="35799-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35799-145">type</span><span class="sxs-lookup"><span data-stu-id="35799-145">type</span></span> |<span data-ttu-id="35799-146">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-146">Yes</span></span> |<span data-ttu-id="35799-147">Type de la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="35799-147">Type of parameter value.</span></span> <span data-ttu-id="35799-148">Consultez hello suivant liste pour hello types autorisé :</span><span class="sxs-lookup"><span data-stu-id="35799-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="35799-149">displayName</span><span class="sxs-lookup"><span data-stu-id="35799-149">displayName</span></span> |<span data-ttu-id="35799-150">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-150">Yes</span></span> |<span data-ttu-id="35799-151">Nom du paramètre hello utilisateur tooa affichées dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="35799-152">description</span><span class="sxs-lookup"><span data-stu-id="35799-152">description</span></span> |<span data-ttu-id="35799-153">Oui</span><span class="sxs-lookup"><span data-stu-id="35799-153">Yes</span></span> |<span data-ttu-id="35799-154">Description du paramètre hello qui s’affiche dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="35799-155">Hello types autorisés sont :</span><span class="sxs-lookup"><span data-stu-id="35799-155">hello allowed types are:</span></span>

* <span data-ttu-id="35799-156">string : n'importe quelle chaîne JSON valide</span><span class="sxs-lookup"><span data-stu-id="35799-156">string – any valid JSON string</span></span>
* <span data-ttu-id="35799-157">int : n'importe quel entier JSON valide</span><span class="sxs-lookup"><span data-stu-id="35799-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="35799-158">bool : n'importe quel booléen JSON valide </span><span class="sxs-lookup"><span data-stu-id="35799-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="35799-159">array : n'importe quel tableau JSON valide</span><span class="sxs-lookup"><span data-stu-id="35799-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="35799-160">Expressions et fonctions d'artefact</span><span class="sxs-lookup"><span data-stu-id="35799-160">Artifact expressions and functions</span></span>
<span data-ttu-id="35799-161">Vous pouvez utiliser expression et d’artefact de fonctions tooconstruct hello la commande d’installation.</span><span class="sxs-lookup"><span data-stu-id="35799-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="35799-162">Les expressions sont placées entre crochets ([et]) et sont évaluées lors de l’artefact de hello est installé.</span><span class="sxs-lookup"><span data-stu-id="35799-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="35799-163">Les expressions peuvent apparaître n'importe où dans une valeur de chaîne JSON et retournent toujours une autre valeur JSON.</span><span class="sxs-lookup"><span data-stu-id="35799-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="35799-164">Si vous avez besoin d’une chaîne littérale qui commence par un crochet de toouse [, vous devez utiliser deux crochets [[.</span><span class="sxs-lookup"><span data-stu-id="35799-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="35799-165">En règle générale, vous utilisez des expressions avec les fonctions tooconstruct une valeur.</span><span class="sxs-lookup"><span data-stu-id="35799-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="35799-166">Exactement comme dans JavaScript, les appels de fonctions sont mis en forme selon functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="35799-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="35799-167">Hello liste suivante présente les fonctions courantes :</span><span class="sxs-lookup"><span data-stu-id="35799-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="35799-168">Parameters(parameterName) - renvoie une valeur de paramètre qui est fournie lors de l’exécution de commande d’artefact hello.</span><span class="sxs-lookup"><span data-stu-id="35799-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="35799-169">concat(arg1,arg2,arg3,...) : combine plusieurs valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="35799-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="35799-170">Cette fonction peut prendre n'importe quel nombre d'arguments.</span><span class="sxs-lookup"><span data-stu-id="35799-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="35799-171">Hello suivant montre l’exemple de comment toouse expression et fonctions tooconstruct une valeur :</span><span class="sxs-lookup"><span data-stu-id="35799-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="35799-172">Création d'un artefact personnalisé</span><span class="sxs-lookup"><span data-stu-id="35799-172">Create a custom artifact</span></span>
<span data-ttu-id="35799-173">Créez votre artefact personnalisé en suivant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="35799-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="35799-174">Installer un éditeur JSON, vous avez besoin d’un toowork de l’éditeur JSON avec les fichiers de définition d’artefact.</span><span class="sxs-lookup"><span data-stu-id="35799-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="35799-175">Nous vous recommandons d'utiliser [Visual Studio Code](https://code.visualstudio.com/), qui est disponible pour Windows, Linux et OS X.</span><span class="sxs-lookup"><span data-stu-id="35799-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="35799-176">Get un artifactfile.json exemple : extraction des artefacts de hello créé par l’équipe Azure DevTest Labs notre [référentiel GitHub](https://github.com/Azure/azure-devtestlab), où nous avons créé une bibliothèque riche d’artefacts qui vous aident à créent vos propres artefacts.</span><span class="sxs-lookup"><span data-stu-id="35799-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="35799-177">Télécharger un fichier de définition d’artefact et apporter des modifications tooit toocreate vos propres artefacts.</span><span class="sxs-lookup"><span data-stu-id="35799-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="35799-178">Assurez-vous d’utiliser IntelliSense - éléments valides IntelliSense de tirer parti de la toosee qui peuvent être tooconstruct utilisé un fichier de définition d’artefact.</span><span class="sxs-lookup"><span data-stu-id="35799-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="35799-179">Vous pouvez également voir hello différentes options pour les valeurs d’un élément.</span><span class="sxs-lookup"><span data-stu-id="35799-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="35799-180">Par exemple, les afficher IntelliSense vous hello deux choix de Windows ou Linux lors de la modification hello **targetOsType** élément.</span><span class="sxs-lookup"><span data-stu-id="35799-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="35799-181">Artefact de hello magasin dans un [référentiel git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="35799-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="35799-182">Créer un répertoire différent pour chaque artefact où nom de répertoire hello est même hello en tant que nom d’artefact hello.</span><span class="sxs-lookup"><span data-stu-id="35799-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="35799-183">Stocker le fichier de définition d’artefact hello (artifactfile.json) dans le répertoire hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="35799-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="35799-184">Commande d’installation scripts hello magasin qui sont référencés à partir de l’artefact de hello.</span><span class="sxs-lookup"><span data-stu-id="35799-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="35799-185">Voici un exemple de dossier d'artefact :</span><span class="sxs-lookup"><span data-stu-id="35799-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Exemple de dépôt git d'artefacts](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="35799-187">Ajouter un laboratoire de hello artefacts référentiel toohello - consultez l’article toohello, [ajouter un référentiel Git des artefacts et des modèles](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="35799-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="35799-188">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="35799-188">Related articles</span></span>
* [<span data-ttu-id="35799-189">Comment les échecs d’artefact toodiagnose dans DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="35799-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="35799-190">Joindre un domaine Active Directory à l’aide d’un modèle de gestionnaire de ressources dans Azure DevTest Labs de tooexisting machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="35799-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="35799-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35799-191">Next steps</span></span>
* <span data-ttu-id="35799-192">Découvrez comment trop[ajouter un laboratoire de tooa référentiel Git artefact](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="35799-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

