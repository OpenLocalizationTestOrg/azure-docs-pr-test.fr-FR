---
title: "les paramètres d’entrée aaaRunbook | Documents Microsoft"
description: "Paramètres d’entrée du Runbook augmentent la flexibilité hello des procédures opérationnelles en vous toopass données tooa runbook lorsqu’il est démarré. Cet article décrit différents cas où des paramètres d’entrée sont utilisés dans des Runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="61ef8-104">Paramètres d’entrée de Runbook</span><span class="sxs-lookup"><span data-stu-id="61ef8-104">Runbook input parameters</span></span>
<span data-ttu-id="61ef8-105">Paramètres d’entrée du Runbook augmentent la flexibilité hello des procédures opérationnelles en vous toopass données tooit lorsqu’il est démarré.</span><span class="sxs-lookup"><span data-stu-id="61ef8-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="61ef8-106">Hello autorise hello runbook actions toobe ciblé pour des environnements et des scénarios spécifiques.</span><span class="sxs-lookup"><span data-stu-id="61ef8-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="61ef8-107">Cet article vous guide dans différents scénarios où des paramètres d’entrée sont utilisés dans des Runbooks.</span><span class="sxs-lookup"><span data-stu-id="61ef8-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="61ef8-108">Configurer les paramètres d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ef8-108">Configure input parameters</span></span>
<span data-ttu-id="61ef8-109">Des paramètres d’entrée peuvent être configurés dans des Runbooks PowerShell, PowerShell Workflow et graphiques.</span><span class="sxs-lookup"><span data-stu-id="61ef8-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="61ef8-110">Un Runbook peut avoir plusieurs paramètres avec différents types de données, ou aucun paramètre.</span><span class="sxs-lookup"><span data-stu-id="61ef8-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="61ef8-111">Des paramètres d’entrée peuvent être obligatoires ou facultatifs, et vous pouvez affecter une valeur par défaut à des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="61ef8-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="61ef8-112">Vous pouvez assigner des valeurs toohello des paramètres d’entrée d’un runbook lorsque vous le démarrez via une des méthodes disponibles de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="61ef8-113">Ces méthodes incluent le démarrage d’un runbook à partir de portail de hello ou un service web.</span><span class="sxs-lookup"><span data-stu-id="61ef8-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="61ef8-114">Vous pouvez également démarrer un Runbook en tant que Runbook enfant appelé en ligne dans un autre Runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="61ef8-115">Configurer les paramètres d’entrée dans des Runbooks PowerShell et PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="61ef8-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="61ef8-116">PowerShell et [les runbooks PowerShell Workflow](automation-first-runbook-textual.md) dans Azure Automation prend en charge les paramètres d’entrée qui sont définis via hello suivant des attributs.</span><span class="sxs-lookup"><span data-stu-id="61ef8-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="61ef8-117">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="61ef8-117">**Property**</span></span> | <span data-ttu-id="61ef8-118">**Description**</span><span class="sxs-lookup"><span data-stu-id="61ef8-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="61ef8-119">Type</span><span class="sxs-lookup"><span data-stu-id="61ef8-119">Type</span></span> |<span data-ttu-id="61ef8-120">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="61ef8-120">Required.</span></span> <span data-ttu-id="61ef8-121">type de données Hello attendu pour la valeur du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="61ef8-122">Tout type .NET est valide.</span><span class="sxs-lookup"><span data-stu-id="61ef8-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="61ef8-123">Nom</span><span class="sxs-lookup"><span data-stu-id="61ef8-123">Name</span></span> |<span data-ttu-id="61ef8-124">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="61ef8-124">Required.</span></span> <span data-ttu-id="61ef8-125">nom de Hello du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-125">hello name of hello parameter.</span></span> <span data-ttu-id="61ef8-126">Cela doit être unique au sein de hello runbook et peut contenir uniquement des lettres, des chiffres ou traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="61ef8-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="61ef8-127">et doit commencer par une lettre.</span><span class="sxs-lookup"><span data-stu-id="61ef8-127">It must start with a letter.</span></span> |
| <span data-ttu-id="61ef8-128">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="61ef8-128">Mandatory</span></span> |<span data-ttu-id="61ef8-129">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-129">Optional.</span></span> <span data-ttu-id="61ef8-130">Spécifie si une valeur doit être fournie pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="61ef8-131">Si vous affectez ce trop**$true**, puis une valeur doit être fournie au démarrage hello runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="61ef8-132">Si vous affectez ce trop**$false**, puis une valeur est facultative.</span><span class="sxs-lookup"><span data-stu-id="61ef8-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="61ef8-133">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="61ef8-133">Default value</span></span> |<span data-ttu-id="61ef8-134">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-134">Optional.</span></span>  <span data-ttu-id="61ef8-135">Spécifie une valeur qui sera utilisée pour le paramètre hello si une valeur n’est pas transmise au démarrage hello runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="61ef8-136">Une valeur par défaut peut être définie pour n’importe quel paramètre et est automatiquement apportées par paramètre hello facultatif, quelle que soit le paramètre obligatoire de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="61ef8-137">Windows PowerShell prend en charge d’autres attributs de paramètres d’entrée que ceux répertoriés ici, tels que la validation, les alias et les jeux de paramètres.</span><span class="sxs-lookup"><span data-stu-id="61ef8-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="61ef8-138">Toutefois, Azure Automation prend actuellement en charge uniquement hello paramètres d’entrée répertoriées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="61ef8-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="61ef8-139">Une définition de paramètre dans les runbooks PowerShell Workflow a hello suivant la forme générale, où plusieurs paramètres sont séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="61ef8-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="61ef8-140">Lorsque vous définissez les paramètres, si vous ne spécifiez pas hello **obligatoire** d’attribut, par défaut, paramètre hello est considéré comme facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="61ef8-141">En outre, si vous définissez une valeur par défaut pour un paramètre dans les runbooks PowerShell Workflow, il est considéré par PowerShell comme paramètre facultatif, quel que soit hello **obligatoire** valeur d’attribut.</span><span class="sxs-lookup"><span data-stu-id="61ef8-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="61ef8-142">Par exemple, permet de configurer les paramètres d’entrée hello pour un runbook PowerShell Workflow qui génère plus d’informations sur les ordinateurs virtuels, une seule machine virtuelle ou sur toutes les machines virtuelles au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61ef8-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="61ef8-143">Ce runbook possède deux paramètres comme indiqué dans hello suivant capture d’écran : nom hello de machine virtuelle et le nom hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61ef8-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![PowerShell Workflow d’Automation](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="61ef8-145">Dans cette définition de paramètre, hello paramètres **$VMName** et **$resourceGroupName** sont des paramètres simples de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="61ef8-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="61ef8-146">Toutefois, les Runbooks PowerShell et PowerShell Workflow prennent en charge tous les types, simples et complexes, tels que **object** ou **PSCredential** pour les paramètres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="61ef8-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="61ef8-147">Si votre runbook possède un paramètre d’entrée de type objet, puis utiliser une table de hachage PowerShell avec (nom, valeur) paires toopass dans une valeur.</span><span class="sxs-lookup"><span data-stu-id="61ef8-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="61ef8-148">Par exemple, si vous avez hello suit le paramètre dans un runbook :</span><span class="sxs-lookup"><span data-stu-id="61ef8-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="61ef8-149">Vous pouvez passer hello suit valeur toohello paramètre :</span><span class="sxs-lookup"><span data-stu-id="61ef8-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="61ef8-150">Configurer des paramètres d’entrée dans des Runbooks graphiques</span><span class="sxs-lookup"><span data-stu-id="61ef8-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="61ef8-151">trop[configurer un runbook graphique](automation-first-runbook-graphical.md) avec des paramètres d’entrée, nous allons créer un runbook graphique qui renvoie les détails sur les machines virtuelles, soit une seule machine virtuelle ou tous les ordinateurs virtuels au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61ef8-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="61ef8-152">La configuration d'un Runbook implique deux activités principales, comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61ef8-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="61ef8-153">[**Authentifier les procédures opérationnelles compte d’identification Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="61ef8-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="61ef8-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget les propriétés de hello d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61ef8-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="61ef8-155">Vous pouvez utiliser hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) noms de hello toooutput activité des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="61ef8-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="61ef8-156">Hello activité **Get-AzureRmVm** accepte deux paramètres, hello **nom de machine virtuelle** et hello **nom de groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="61ef8-157">Étant donné que ces paramètres peut nécessiter des valeurs différentes à chaque fois que vous démarrez hello runbook, vous pouvez ajouter des paramètres d’entrée tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="61ef8-158">Voici les paramètres d’entrée de hello étapes tooadd :</span><span class="sxs-lookup"><span data-stu-id="61ef8-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="61ef8-159">Sélectionnez hello runbook graphique de hello **Runbooks** panneau, puis cliquez sur [ **modifier** ](automation-graphical-authoring-intro.md) il.</span><span class="sxs-lookup"><span data-stu-id="61ef8-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="61ef8-160">À partir de l’éditeur de runbook hello, cliquez sur **d’entrée et de sortie** tooopen hello **d’entrée et de sortie** panneau.</span><span class="sxs-lookup"><span data-stu-id="61ef8-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Runbook graphique d’Automation](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="61ef8-162">Hello **d’entrée et de sortie** panneau affiche la liste des paramètres d’entrée qui sont définis pour les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="61ef8-163">Dans ce panneau, vous pouvez ajouter un nouveau paramètre d’entrée ou modifier la configuration de hello d’un paramètre d’entrée existant.</span><span class="sxs-lookup"><span data-stu-id="61ef8-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="61ef8-164">tooadd un nouveau paramètre hello runbook, cliquez sur **Ajout de l’entrée** tooopen hello **paramètre d’entrée du Runbook** panneau.</span><span class="sxs-lookup"><span data-stu-id="61ef8-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="61ef8-165">Là, vous pouvez configurer hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="61ef8-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="61ef8-166">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="61ef8-166">**Property**</span></span> | <span data-ttu-id="61ef8-167">**Description**</span><span class="sxs-lookup"><span data-stu-id="61ef8-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="61ef8-168">Nom</span><span class="sxs-lookup"><span data-stu-id="61ef8-168">Name</span></span> |<span data-ttu-id="61ef8-169">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="61ef8-169">Required.</span></span>  <span data-ttu-id="61ef8-170">nom de Hello du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-170">hello name of hello parameter.</span></span> <span data-ttu-id="61ef8-171">Cela doit être unique au sein de hello runbook et peut contenir uniquement des lettres, des chiffres ou traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="61ef8-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="61ef8-172">et doit commencer par une lettre.</span><span class="sxs-lookup"><span data-stu-id="61ef8-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="61ef8-173">Description</span><span class="sxs-lookup"><span data-stu-id="61ef8-173">Description</span></span> |<span data-ttu-id="61ef8-174">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-174">Optional.</span></span> <span data-ttu-id="61ef8-175">Description de l’objectif de hello du paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="61ef8-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="61ef8-176">Type</span><span class="sxs-lookup"><span data-stu-id="61ef8-176">Type</span></span> |<span data-ttu-id="61ef8-177">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-177">Optional.</span></span> <span data-ttu-id="61ef8-178">type de données de Hello est attendu pour la valeur du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="61ef8-179">Les types de paramètres pris en charge sont **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** et **Object**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="61ef8-180">Si un type de données n’est pas sélectionné, la valeur par défaut trop**chaîne**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="61ef8-181">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="61ef8-181">Mandatory</span></span> |<span data-ttu-id="61ef8-182">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-182">Optional.</span></span> <span data-ttu-id="61ef8-183">Spécifie si une valeur doit être fournie pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="61ef8-184">Si vous choisissez **Oui**, puis une valeur doit être fournie au démarrage hello runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="61ef8-185">Si vous choisissez **aucune**, puis une valeur n’est pas requise lorsque hello runbook est démarré, et une valeur par défaut peut être définie.</span><span class="sxs-lookup"><span data-stu-id="61ef8-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="61ef8-186">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="61ef8-186">Default Value</span></span> |<span data-ttu-id="61ef8-187">facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-187">Optional.</span></span> <span data-ttu-id="61ef8-188">Spécifie une valeur qui sera utilisée pour le paramètre hello si une valeur n’est pas transmise au démarrage hello runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="61ef8-189">Une valeur par défaut peut être définie pour un paramètre qui n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="61ef8-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="61ef8-190">tooset une valeur par défaut, choisissez **personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="61ef8-191">Cette valeur est utilisée, sauf si une autre valeur est fournie au démarrage hello runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="61ef8-192">Choisissez **aucun** si vous ne souhaitez pas tooprovide une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="61ef8-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Ajouter une nouvelle entrée](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="61ef8-194">Créer les deux paramètres avec hello propriétés qui seront utilisées par hello suivantes **Get-AzureRmVm** activité :</span><span class="sxs-lookup"><span data-stu-id="61ef8-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="61ef8-195">**Paramètre 1 :**</span><span class="sxs-lookup"><span data-stu-id="61ef8-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="61ef8-196">Nom - VMName</span><span class="sxs-lookup"><span data-stu-id="61ef8-196">Name - VMName</span></span>
     * <span data-ttu-id="61ef8-197">Type : Chaîne</span><span class="sxs-lookup"><span data-stu-id="61ef8-197">Type - String</span></span>
     * <span data-ttu-id="61ef8-198">Obligatoire : Non</span><span class="sxs-lookup"><span data-stu-id="61ef8-198">Mandatory - No</span></span>
   * <span data-ttu-id="61ef8-199">**Paramètre 2 :**</span><span class="sxs-lookup"><span data-stu-id="61ef8-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="61ef8-200">Nom : resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="61ef8-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="61ef8-201">Type : Chaîne</span><span class="sxs-lookup"><span data-stu-id="61ef8-201">Type - String</span></span>
     * <span data-ttu-id="61ef8-202">Obligatoire : Non</span><span class="sxs-lookup"><span data-stu-id="61ef8-202">Mandatory - No</span></span>
     * <span data-ttu-id="61ef8-203">Valeur par défaut : Personnalisé</span><span class="sxs-lookup"><span data-stu-id="61ef8-203">Default value - Custom</span></span>
     * <span data-ttu-id="61ef8-204">Valeur par défaut personnalisée - \<nom hello du groupe de ressources qui contient des machines virtuelles de hello ></span><span class="sxs-lookup"><span data-stu-id="61ef8-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="61ef8-205">Une fois que vous ajoutez des paramètres de hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="61ef8-206">Vous pouvez désormais afficher Bonjour **entrée et sortie lame**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="61ef8-207">Cliquez de nouveau sur **OK**, puis sur **Enregistrer** et **Publier** pour publier votre Runbook.</span><span class="sxs-lookup"><span data-stu-id="61ef8-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="61ef8-208">Affecter des valeurs tooinput des paramètres dans les runbooks</span><span class="sxs-lookup"><span data-stu-id="61ef8-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="61ef8-209">Vous pouvez passer des valeurs tooinput paramètres dans des procédures opérationnelles dans les scénarios suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="61ef8-210">Démarrer un Runbook et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="61ef8-211">Un runbook peut être démarré de plusieurs façons : via hello portail Azure, avec un webhook, avec les applets de commande PowerShell, hello API REST ou avec le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="61ef8-212">Nous abordons ci-dessous différentes méthodes pour démarrer un Runbook et affecter des paramètres.</span><span class="sxs-lookup"><span data-stu-id="61ef8-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="61ef8-213">Démarrer un runbook publié à l’aide de hello portail Azure et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="61ef8-214">Lorsque vous [démarrer hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **démarrer le Runbook** panneau s’ouvre et vous pouvez configurer les valeurs des paramètres hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="61ef8-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Démarrer à l’aide du portail de hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="61ef8-216">Dans l’étiquette de hello sous la zone d’entrée de hello, vous pouvez voir les attributs hello qui ont été définies pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="61ef8-217">Les attributs incluent Obligatoire ou Facultatif, Type et Valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="61ef8-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="61ef8-218">Dans hello aide bulle suivant toohello nom du paramètre, vous pouvez voir toutes les informations de clé hello vous devez toomake des décisions sur les valeurs de paramètre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="61ef8-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="61ef8-219">Ces informations indiquent si un paramètre est obligatoire ou facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="61ef8-220">Il inclut également le type de hello et la valeur par défaut (le cas échéant) et autres notes utiles.</span><span class="sxs-lookup"><span data-stu-id="61ef8-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Bulle d'aide](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="61ef8-222">Les paramètres de type String prennent en charge les valeurs de chaîne **vides** .</span><span class="sxs-lookup"><span data-stu-id="61ef8-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="61ef8-223">Saisie **[EmptyString]** dans le paramètre d’entrée hello zone passe un paramètre de toohello une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="61ef8-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="61ef8-224">De même, les paramètres de type String ne prennent pas en charge la transmission de valeurs **Null** .</span><span class="sxs-lookup"><span data-stu-id="61ef8-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="61ef8-225">Si vous ne transmettez pas n’importe quel paramètre de chaîne de valeur toohello, puis PowerShell interprète la valeur null.</span><span class="sxs-lookup"><span data-stu-id="61ef8-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="61ef8-226">Démarrer un Runbook publié à l’aide d’applets de commande PowerShell et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="61ef8-227">**Applets de commande d’Azure Resource Manager :** vous pouvez démarrer un Runbook Automation créé dans un groupe de ressources à l’aide de l’applet de commande [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="61ef8-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="61ef8-228">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="61ef8-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="61ef8-229">**Applets de commande de gestion des services Azure :** vous pouvez démarrer un Runbook Automation créé dans un groupe de ressources par défaut à l’aide de l’applet de commande [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="61ef8-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="61ef8-230">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="61ef8-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="61ef8-231">Lorsque vous démarrez un runbook à l’aide des applets de commande PowerShell, un paramètre par défaut, **MicrosoftApplicationManagementStartedBy** est créée avec la valeur de hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="61ef8-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="61ef8-232">Vous pouvez afficher ce paramètre Bonjour **détails de la tâche** panneau.</span><span class="sxs-lookup"><span data-stu-id="61ef8-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="61ef8-233">Démarrer un Runbook à l’aide d’un Kit de développement logiciel (SDK) et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="61ef8-234">**Méthode de gestionnaire de ressources Azure :** vous pouvez démarrer un runbook à l’aide du Kit de développement logiciel d’un langage de programmation de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="61ef8-235">Voici un extrait de code C# permettant de démarrer un Runbook dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="61ef8-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="61ef8-236">Vous pouvez afficher tout code hello à notre [référentiel GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="61ef8-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="61ef8-237">**Méthode de gestion des services Azure :** vous pouvez démarrer un runbook à l’aide du Kit de développement logiciel d’un langage de programmation de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="61ef8-238">Voici un extrait de code C# permettant de démarrer un Runbook dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="61ef8-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="61ef8-239">Vous pouvez afficher tout code hello à notre [référentiel GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="61ef8-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="61ef8-240">toostart cette méthode, créez un Bonjour toostore de dictionnaire des paramètres de runbook, **VMName** et **resourceGroupName**et leurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="61ef8-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="61ef8-241">Ensuite, démarrez runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-241">Then start hello runbook.</span></span> <span data-ttu-id="61ef8-242">Voici hello c# extrait de code pour appeler la méthode hello définie ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="61ef8-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="61ef8-243">Démarrer un runbook à l’aide des API REST de hello et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="61ef8-244">Une tâche de runbook peut être créée et démarrée par hello les API REST Azure Automation à l’aide de hello **PUT** URI de demande de méthode avec hello suivant.</span><span class="sxs-lookup"><span data-stu-id="61ef8-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="61ef8-245">Dans l’URI de la demande hello, remplacez hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="61ef8-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="61ef8-246">**subscription-id** : ID de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="61ef8-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="61ef8-247">**nom du service de cloud :** nom hello de demande de hello toowhich hello cloud service doit être envoyé.</span><span class="sxs-lookup"><span data-stu-id="61ef8-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="61ef8-248">**Automation-account-name :** hello le nom de votre compte automation qui est hébergé dans hello spécifié service cloud.</span><span class="sxs-lookup"><span data-stu-id="61ef8-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="61ef8-249">**id de tâche :** hello GUID pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="61ef8-250">GUID dans PowerShell peut être créés à l’aide de hello **[GUID] ::NewGuid(). ToString()** commande.</span><span class="sxs-lookup"><span data-stu-id="61ef8-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="61ef8-251">Dans la tâche de runbook toohello commande toopass paramètres, utilisez le corps de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="61ef8-252">Il prend hello deux propriétés fournies au format JSON suivantes :</span><span class="sxs-lookup"><span data-stu-id="61ef8-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="61ef8-253">**Runbook Name :** obligatoire.</span><span class="sxs-lookup"><span data-stu-id="61ef8-253">**Runbook name:** Required.</span></span> <span data-ttu-id="61ef8-254">nom de Hello du runbook de hello pour hello travail toostart.</span><span class="sxs-lookup"><span data-stu-id="61ef8-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="61ef8-255">**Runbook Parameters :** facultatif.</span><span class="sxs-lookup"><span data-stu-id="61ef8-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="61ef8-256">Un dictionnaire de liste des paramètres hello (nom, valeur) format où nom doit être de type String et de valeur peut être toute valeur JSON valide.</span><span class="sxs-lookup"><span data-stu-id="61ef8-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="61ef8-257">Si vous souhaitez toostart hello **Get-AzureVMTextual** runbook qui a été créé précédemment avec **VMName** et **resourceGroupName** en tant que paramètres, utilisez hello suivant le format JSON pour le corps de demande hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="61ef8-258">Un code d’état HTTP 201 est retourné si le travail de hello est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="61ef8-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="61ef8-259">Pour plus d’informations sur les en-têtes de réponse et corps de réponse hello, reportez-vous à l’article de toohello sur la façon trop[créer une tâche de runbook à l’aide des API REST de hello.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="61ef8-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="61ef8-260">Tester un Runbook et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="61ef8-261">Lorsque vous [brouillon hello de test de votre runbook](automation-testing-runbook.md) en utilisant l’option de test hello, hello **Test** panneau s’ouvre et vous pouvez configurer les valeurs des paramètres hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="61ef8-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Tester et affecter des paramètres](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="61ef8-263">Liez un runbook tooa de planification et d’affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="61ef8-264">Vous pouvez [lier une planification](automation-schedules.md) tooyour runbook afin que runbook hello commence à une heure spécifique.</span><span class="sxs-lookup"><span data-stu-id="61ef8-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="61ef8-265">Pour affecter des paramètres d’entrée lorsque vous créez la planification de hello, et hello runbook utilise ces valeurs lorsqu’il est démarré par la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="61ef8-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="61ef8-266">Impossible d’enregistrer la planification de hello jusqu'à ce que toutes les valeurs de paramètre obligatoires sont fournies.</span><span class="sxs-lookup"><span data-stu-id="61ef8-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Planifier et affecter des paramètres](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="61ef8-268">Créer un WebHook pour un Runbook et affecter des paramètres</span><span class="sxs-lookup"><span data-stu-id="61ef8-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="61ef8-269">Vous pouvez créer un [WebHook](automation-webhooks.md) pour votre Runbook, puis configurer les paramètres d’entrée de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="61ef8-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="61ef8-270">Impossible d’enregistrer hello webhook jusqu'à ce que toutes les valeurs de paramètre obligatoires sont fournies.</span><span class="sxs-lookup"><span data-stu-id="61ef8-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Créer un WebHook et affecter des paramètres](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="61ef8-272">Lorsque vous exécutez un runbook à l’aide d’un webhook, hello prédéfinis de paramètre d’entrée  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  est envoyé, ainsi que les paramètres d’entrée hello que vous avez définie.</span><span class="sxs-lookup"><span data-stu-id="61ef8-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="61ef8-273">Vous pouvez cliquer sur tooexpand hello **WebhookData** paramètre pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="61ef8-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Paramètre WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="61ef8-275">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61ef8-275">Next steps</span></span>
* <span data-ttu-id="61ef8-276">Pour plus d’informations sur l’entrée et la sortie du Runbook, voir [Azure Automation : entrée et sortie de Runbook, et Runbook imbriqués](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)</span><span class="sxs-lookup"><span data-stu-id="61ef8-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="61ef8-277">Pour plus d’informations sur les différentes façons toostart un runbook, consultez [démarrage d’un runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="61ef8-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="61ef8-278">tooedit un runbook textuels, consultez trop[modification des procédures opérationnelles textuelle](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="61ef8-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="61ef8-279">tooedit un runbook graphique, consultez trop[de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="61ef8-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

