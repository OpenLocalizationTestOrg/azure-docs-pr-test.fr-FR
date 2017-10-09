---
title: solutions de gestion aaaCreating Operations Management Suite (OMS) | Documents Microsoft
description: "Solutions de gestion d’étendent les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir espace de travail OMS.  Cet article fournit des détails sur la façon dont vous pouvez créer toobe des solutions de gestion utilisé dans votre propre environnement ou apportées disponible tooyour clients."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="e1099-104">Création d’un fichier de solutions de gestion dans Operations Management Suite (OMS) (préversion)</span><span class="sxs-lookup"><span data-stu-id="e1099-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="e1099-105">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="e1099-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="e1099-106">N’importe quel schéma décrit ci-dessous est un objet toochange.</span><span class="sxs-lookup"><span data-stu-id="e1099-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="e1099-107">Les solutions de gestion dans Operations Management Suite (OMS) sont implémentées en tant que [modèles Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e1099-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="e1099-108">tâche principale Hello d’apprentissage de la façon dont les solutions de gestion tooauthor consiste à apprendre comment trop[créer un modèle](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1099-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="e1099-109">Cet article fournit des détails uniques des modèles utilisés pour les solutions et la manière dont les ressources de solution classique tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="e1099-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="e1099-110">Outils</span><span class="sxs-lookup"><span data-stu-id="e1099-110">Tools</span></span>

<span data-ttu-id="e1099-111">Vous pouvez utiliser n’importe quel toowork de l’éditeur de texte avec les fichiers de solution, mais nous vous recommandons en exploitant les fonctionnalités de hello fournies dans Visual Studio ou Visual Studio Code comme décrit dans hello suivant des articles.</span><span class="sxs-lookup"><span data-stu-id="e1099-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="e1099-112">Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1099-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="e1099-113">Utiliser des modèles Azure Resource Manager dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e1099-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="e1099-114">Structure</span><span class="sxs-lookup"><span data-stu-id="e1099-114">Structure</span></span>
<span data-ttu-id="e1099-115">structure de base Hello d’un fichier de solution de gestion est hello identique à un [modèle Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format) qui est la suivante.</span><span class="sxs-lookup"><span data-stu-id="e1099-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="e1099-116">Chacune des sections hello ci-dessous décrit les éléments de niveau supérieur hello et et leur contenu dans une solution.</span><span class="sxs-lookup"><span data-stu-id="e1099-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="e1099-117">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e1099-117">Parameters</span></span>
<span data-ttu-id="e1099-118">[Paramètres](../azure-resource-manager/resource-group-authoring-templates.md#parameters) sont des valeurs dont vous avez besoin à partir de l’utilisateur de hello lorsqu’ils installent la solution de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="e1099-119">Il existe des paramètres standard compris dans toutes les solutions, et vous pouvez ajouter des paramètres supplémentaires en fonction des besoins spécifiques de votre solution.</span><span class="sxs-lookup"><span data-stu-id="e1099-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="e1099-120">Comment les utilisateurs fournit les valeurs de paramètre lors de l’installation de votre solution dépend de paramètre particulier hello et comment hello solution est installée.</span><span class="sxs-lookup"><span data-stu-id="e1099-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="e1099-121">Lorsqu’un utilisateur installe votre solution de gestion via hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ou [modèles de démarrage rapide d’Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) qu’ils sont invités à tooselect un [OMS espace de travail et le compte Automation ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="e1099-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="e1099-122">Ceux-ci sont des valeurs de hello toopopulate utilisés de chacun des paramètres standard de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="e1099-123">utilisateur de Hello n’est pas invité toodirectly fournir des valeurs pour les paramètres standard hello, mais elles sont demandées par invite tooprovide des valeurs pour tous les paramètres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e1099-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="e1099-124">Lorsque les utilisateur hello installe votre solution [une autre méthode](operations-management-suite-solutions.md#finding-and-installing-management-solutions), ils doivent fournir une valeur pour tous les paramètres standards et tous les paramètres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e1099-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="e1099-125">Vous trouverez ci-dessous un exemple de paramètre.</span><span class="sxs-lookup"><span data-stu-id="e1099-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="e1099-126">Hello tableau suivant décrit les attributs de hello d’un paramètre.</span><span class="sxs-lookup"><span data-stu-id="e1099-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="e1099-127">Attribut</span><span class="sxs-lookup"><span data-stu-id="e1099-127">Attribute</span></span> | <span data-ttu-id="e1099-128">Description</span><span class="sxs-lookup"><span data-stu-id="e1099-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e1099-129">type</span><span class="sxs-lookup"><span data-stu-id="e1099-129">type</span></span> |<span data-ttu-id="e1099-130">Type de données pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-130">Data type for hello parameter.</span></span> <span data-ttu-id="e1099-131">contrôle d’entrée de Hello affiché à l’utilisateur de hello dépend du type de données hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="e1099-132">Valeur booléenne : zone de liste déroulante</span><span class="sxs-lookup"><span data-stu-id="e1099-132">bool - Drop down box</span></span><br><span data-ttu-id="e1099-133">Chaîne : zone de texte</span><span class="sxs-lookup"><span data-stu-id="e1099-133">string - Text box</span></span><br><span data-ttu-id="e1099-134">Entier : zone de texte</span><span class="sxs-lookup"><span data-stu-id="e1099-134">int - Text box</span></span><br><span data-ttu-id="e1099-135">securestring : champ de mot de passe</span><span class="sxs-lookup"><span data-stu-id="e1099-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="e1099-136">category</span><span class="sxs-lookup"><span data-stu-id="e1099-136">category</span></span> |<span data-ttu-id="e1099-137">Catégorie facultative pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="e1099-138">Paramètres Bonjour même catégorie sont regroupés ensemble.</span><span class="sxs-lookup"><span data-stu-id="e1099-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="e1099-139">contrôle</span><span class="sxs-lookup"><span data-stu-id="e1099-139">control</span></span> |<span data-ttu-id="e1099-140">Fonctionnalité supplémentaire pour les paramètres de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="e1099-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="e1099-141">datetime : le contrôle Datetime est affiché.</span><span class="sxs-lookup"><span data-stu-id="e1099-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="e1099-142">GUID - valeur Guid est généré automatiquement et paramètre hello n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="e1099-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="e1099-143">description</span><span class="sxs-lookup"><span data-stu-id="e1099-143">description</span></span> |<span data-ttu-id="e1099-144">Description facultative pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="e1099-145">Affiché dans un paramètre de toohello suivant informations info-bulle.</span><span class="sxs-lookup"><span data-stu-id="e1099-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="e1099-146">Paramètres standard</span><span class="sxs-lookup"><span data-stu-id="e1099-146">Standard parameters</span></span>
<span data-ttu-id="e1099-147">Hello tableau suivant répertorie les paramètres standard hello pour toutes les solutions de gestion.</span><span class="sxs-lookup"><span data-stu-id="e1099-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="e1099-148">Ces valeurs sont remplies pour utilisateur hello au lieu de demander les lorsque votre solution est installée à partir de modèles Azure Marketplace ou de démarrage rapide de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="e1099-149">utilisateur de Hello doit fournir des valeurs pour les si les solutions hello sont installée avec une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="e1099-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="e1099-150">interface utilisateur de Hello dans les modèles Azure Marketplace et Quickstart hello s’attend à des noms de paramètre hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="e1099-151">Si vous utilisez des noms de paramètres différents puis hello utilisateur sera invité pour eux, et qu’ils ne sont pas automatiquement peuplées.</span><span class="sxs-lookup"><span data-stu-id="e1099-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="e1099-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e1099-152">Parameter</span></span> | <span data-ttu-id="e1099-153">Type</span><span class="sxs-lookup"><span data-stu-id="e1099-153">Type</span></span> | <span data-ttu-id="e1099-154">Description</span><span class="sxs-lookup"><span data-stu-id="e1099-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e1099-155">accountName</span><span class="sxs-lookup"><span data-stu-id="e1099-155">accountName</span></span> |<span data-ttu-id="e1099-156">string</span><span class="sxs-lookup"><span data-stu-id="e1099-156">string</span></span> |<span data-ttu-id="e1099-157">Nom de compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e1099-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="e1099-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="e1099-158">pricingTier</span></span> |<span data-ttu-id="e1099-159">string</span><span class="sxs-lookup"><span data-stu-id="e1099-159">string</span></span> |<span data-ttu-id="e1099-160">Niveau tarifaire de l’espace de travail Log Analytics et du compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e1099-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="e1099-161">regionId</span><span class="sxs-lookup"><span data-stu-id="e1099-161">regionId</span></span> |<span data-ttu-id="e1099-162">string</span><span class="sxs-lookup"><span data-stu-id="e1099-162">string</span></span> |<span data-ttu-id="e1099-163">Région de hello compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e1099-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="e1099-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="e1099-164">solutionName</span></span> |<span data-ttu-id="e1099-165">string</span><span class="sxs-lookup"><span data-stu-id="e1099-165">string</span></span> |<span data-ttu-id="e1099-166">Nom de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-166">Name of hello solution.</span></span>  <span data-ttu-id="e1099-167">Si vous déployez votre solution via des modèles de démarrage rapide, vous devez définir solutionName en tant que paramètre permettant de définir à la place nécessitant hello utilisateur toospecify, une chaîne.</span><span class="sxs-lookup"><span data-stu-id="e1099-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="e1099-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="e1099-168">workspaceName</span></span> |<span data-ttu-id="e1099-169">string</span><span class="sxs-lookup"><span data-stu-id="e1099-169">string</span></span> |<span data-ttu-id="e1099-170">Nom de l’espace de travail Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e1099-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="e1099-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="e1099-171">workspaceRegionId</span></span> |<span data-ttu-id="e1099-172">string</span><span class="sxs-lookup"><span data-stu-id="e1099-172">string</span></span> |<span data-ttu-id="e1099-173">Région de l’espace de travail hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="e1099-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="e1099-174">Voici la structure hello des paramètres standard de hello que vous pouvez copier et coller dans votre fichier solution.</span><span class="sxs-lookup"><span data-stu-id="e1099-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="e1099-175">Vous faites référence tooparameter des valeurs dans d’autres éléments de solution hello avec la syntaxe hello **paramètres ('parameter name')**.</span><span class="sxs-lookup"><span data-stu-id="e1099-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="e1099-176">Par exemple, tooaccess hello nom de l’espace de travail, vous utiliseriez **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="e1099-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="e1099-177">variables</span><span class="sxs-lookup"><span data-stu-id="e1099-177">Variables</span></span>
<span data-ttu-id="e1099-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) sont des valeurs que vous utiliserez dans reste hello de solution de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="e1099-179">Ces valeurs ne sont pas utilisateur toohello exposé installation hello solution.</span><span class="sxs-lookup"><span data-stu-id="e1099-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="e1099-180">Ils sont auteur de hello tooprovide prévue avec un emplacement unique où ils peuvent gérer les valeurs qui peuvent être utilisés plusieurs fois dans l’ensemble des solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="e1099-181">Vous devez placer n’importe quelle solution tooyour spécifique de valeurs dans des variables comme toohard opposé les coder Bonjour **ressources** élément.</span><span class="sxs-lookup"><span data-stu-id="e1099-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="e1099-182">Cela améliore la lisibilité du code de hello et vous permet de tooeasily modifier ces valeurs dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="e1099-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="e1099-183">Voici un exemple d’élément **variables** avec des paramètres standard utilisés dans les solutions.</span><span class="sxs-lookup"><span data-stu-id="e1099-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="e1099-184">Vous faites référence à des valeurs de toovariable solution hello avec la syntaxe hello **variables (« nom de la variable')**.</span><span class="sxs-lookup"><span data-stu-id="e1099-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="e1099-185">Par exemple, tooaccess hello SolutionName variable, vous utiliseriez **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="e1099-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="e1099-186">Vous pouvez également définir des variables complexes pour plusieurs ensembles de valeurs.</span><span class="sxs-lookup"><span data-stu-id="e1099-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="e1099-187">Elles sont particulièrement utiles dans les solutions de gestion où vous définissez plusieurs propriétés pour différents types de ressources.</span><span class="sxs-lookup"><span data-stu-id="e1099-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="e1099-188">Par exemple, vous pourriez restructurer les variables de solution hello ci-dessus toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="e1099-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="e1099-189">Dans ce cas, vous faites référence à des valeurs de toovariable solution hello avec la syntaxe hello **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="e1099-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="e1099-190">Par exemple, tooaccess hello variable du nom de la Solution, vous utiliseriez **variables('Solution'). Nom**.</span><span class="sxs-lookup"><span data-stu-id="e1099-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="e1099-191">Ressources</span><span class="sxs-lookup"><span data-stu-id="e1099-191">Resources</span></span>
<span data-ttu-id="e1099-192">[Ressources](../azure-resource-manager/resource-group-authoring-templates.md#resources) définir hello différentes ressources qui installent et configurent votre solution de gestion.</span><span class="sxs-lookup"><span data-stu-id="e1099-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="e1099-193">Il s’agit de hello plus grand et plus complexe partie du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="e1099-194">Vous pouvez obtenir la structure de hello et une description complète des éléments de ressource dans [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="e1099-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="e1099-195">Différentes ressources que vous définirez généralement sont détaillées dans d’autres articles de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="e1099-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="e1099-196">Dépendances</span><span class="sxs-lookup"><span data-stu-id="e1099-196">Dependencies</span></span>
<span data-ttu-id="e1099-197">Hello **dependsOn** éléments spécifie un [dépendance](../azure-resource-manager/resource-group-define-dependencies.md) sur une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="e1099-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="e1099-198">Lors de la solution de hello est installée, une ressource n’est pas créée jusqu'à ce que toutes ses dépendances ont été créés.</span><span class="sxs-lookup"><span data-stu-id="e1099-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="e1099-199">Par exemple, votre solution peut [démarrer un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) lorsqu’il est installé à l’aide d’une [ressource de tâche](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="e1099-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="e1099-200">ressources de travail Hello dépendront hello runbook ressources toomake que ce runbook hello est créé avant que le travail de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="e1099-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="e1099-201">Espace de travail OMS et compte Automation</span><span class="sxs-lookup"><span data-stu-id="e1099-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="e1099-202">Exigent des solutions de gestion un [espace de travail OMS](../log-analytics/log-analytics-manage-access.md) toocontain vues et une [compte Automation](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks et les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e1099-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="e1099-203">Ceux-ci doivent être disponibles avant hello ressources dans hello solution sont créés et ne doivent pas être définies dans la solution hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="e1099-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="e1099-204">Hello utilisateur [spécifier un compte et un espace de travail](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quand ils déploient votre solution, mais en tant qu’auteur de hello, vous devez envisager hello les points suivants.</span><span class="sxs-lookup"><span data-stu-id="e1099-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="e1099-205">Ressource de la solution</span><span class="sxs-lookup"><span data-stu-id="e1099-205">Solution resource</span></span>
<span data-ttu-id="e1099-206">Chaque solution nécessite une entrée de ressource Bonjour **ressources** élément qui définit la solution hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="e1099-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="e1099-207">Cela aura un type de **Microsoft.OperationsManagement/solutions** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="e1099-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="e1099-208">Cela inclut les [paramètres standard](#parameters) et [variables](#variables) qui sont des propriétés de toodefine généralement utilisées de la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="e1099-209">Dépendances</span><span class="sxs-lookup"><span data-stu-id="e1099-209">Dependencies</span></span>
<span data-ttu-id="e1099-210">ressource de solution Hello doit avoir un [dépendance](../azure-resource-manager/resource-group-define-dependencies.md) sur toutes les autres ressources dans la solution hello puisqu’ils doivent tooexist avant la création de solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="e1099-211">Pour cela en ajoutant une entrée pour chaque ressource hello **dependsOn** élément.</span><span class="sxs-lookup"><span data-stu-id="e1099-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="e1099-212">Propriétés</span><span class="sxs-lookup"><span data-stu-id="e1099-212">Properties</span></span>
<span data-ttu-id="e1099-213">ressources de solution Hello possède des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="e1099-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="e1099-214">Cela inclut des ressources de hello référencé et contenus par solution hello qui définit la gestion de ressources de hello après l’installation de la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="e1099-215">Chaque ressource dans une solution de hello doit être répertorié dans soit hello **referencedResources** ou hello **containedResources** propriété.</span><span class="sxs-lookup"><span data-stu-id="e1099-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="e1099-216">Propriété</span><span class="sxs-lookup"><span data-stu-id="e1099-216">Property</span></span> | <span data-ttu-id="e1099-217">Description</span><span class="sxs-lookup"><span data-stu-id="e1099-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e1099-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="e1099-218">workspaceResourceId</span></span> |<span data-ttu-id="e1099-219">ID de l’espace de travail hello Analytique de journal sous forme de hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nom de l’espace de travail\>*.</span><span class="sxs-lookup"><span data-stu-id="e1099-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="e1099-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="e1099-220">referencedResources</span></span> |<span data-ttu-id="e1099-221">Liste des ressources dans la solution hello qui ne doit pas être supprimé lors de la solution de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="e1099-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="e1099-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="e1099-222">containedResources</span></span> |<span data-ttu-id="e1099-223">Liste des ressources dans la solution hello qui doivent être supprimés lorsque la solution de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="e1099-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="e1099-224">exemple Hello ci-dessus est une solution avec un runbook, une planification et la vue.</span><span class="sxs-lookup"><span data-stu-id="e1099-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="e1099-225">planification de Hello et runbook sont *référencé* Bonjour **propriétés** élément afin qu’ils ne sont pas supprimées lors de la solution de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="e1099-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="e1099-226">vue de Hello est *contenus* par conséquent, il est supprimé lors de la solution de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="e1099-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="e1099-227">Planification</span><span class="sxs-lookup"><span data-stu-id="e1099-227">Plan</span></span>
<span data-ttu-id="e1099-228">Hello **plan** entité de ressource de solution hello a les propriétés de hello hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="e1099-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="e1099-229">Propriété</span><span class="sxs-lookup"><span data-stu-id="e1099-229">Property</span></span> | <span data-ttu-id="e1099-230">Description</span><span class="sxs-lookup"><span data-stu-id="e1099-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e1099-231">name</span><span class="sxs-lookup"><span data-stu-id="e1099-231">name</span></span> |<span data-ttu-id="e1099-232">Nom de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-232">Name of hello solution.</span></span> |
| <span data-ttu-id="e1099-233">version</span><span class="sxs-lookup"><span data-stu-id="e1099-233">version</span></span> |<span data-ttu-id="e1099-234">Version de solution hello comme déterminé par l’auteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="e1099-235">product</span><span class="sxs-lookup"><span data-stu-id="e1099-235">product</span></span> |<span data-ttu-id="e1099-236">Solution de hello tooidentify chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="e1099-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="e1099-237">publisher</span><span class="sxs-lookup"><span data-stu-id="e1099-237">publisher</span></span> |<span data-ttu-id="e1099-238">Éditeur de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1099-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="e1099-239">Exemple</span><span class="sxs-lookup"><span data-stu-id="e1099-239">Sample</span></span>
<span data-ttu-id="e1099-240">Vous pouvez consulter des exemples de fichiers de solution avec une ressource de la solution à hello emplacements suivants.</span><span class="sxs-lookup"><span data-stu-id="e1099-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="e1099-241">Ressources Automation</span><span class="sxs-lookup"><span data-stu-id="e1099-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="e1099-242">Ressources de recherche et d’alerte</span><span class="sxs-lookup"><span data-stu-id="e1099-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="e1099-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1099-243">Next steps</span></span>
* <span data-ttu-id="e1099-244">[Ajouter des alertes et les recherches enregistrées](operations-management-suite-solutions-resources-searches-alerts.md) solution de gestion tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1099-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="e1099-245">[Ajouter des vues](operations-management-suite-solutions-resources-views.md) solution de gestion tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1099-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="e1099-246">[Ajouter des procédures opérationnelles et autres ressources Automation](operations-management-suite-solutions-resources-automation.md) solution de gestion tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1099-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="e1099-247">En savoir plus de détails hello de [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1099-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e1099-248">Dans [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates), recherchez des exemples de modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1099-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
