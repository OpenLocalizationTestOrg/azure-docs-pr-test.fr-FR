---
title: "Gestion des ressources avec l’interface CLI Azure | Microsoft Docs"
description: "Utiliser l’interface de ligne de commande Azure (CLI) pour gérer les groupes et les ressources Azure"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="492fb-103">Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="492fb-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="492fb-104">Portail</span><span class="sxs-lookup"><span data-stu-id="492fb-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="492fb-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="492fb-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="492fb-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="492fb-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="492fb-107">API REST</span><span class="sxs-lookup"><span data-stu-id="492fb-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="492fb-108">L’interface de ligne de commande Azure (CLI Azure) est l’un des nombreux outils que vous pouvez utiliser pour déployer et gérer des ressources avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="492fb-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="492fb-109">Cet article présente des méthodes courantes pour gérer des ressources et groupes de ressources Azure en utilisant l’interface de ligne de commande Azure en mode Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="492fb-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="492fb-110">Pour plus d’informations sur l’utilisation de l’interface de ligne de commande afin de déployer des ressources, voir [Déployer des ressources à l’aide de modèles Resource Manager et de l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="492fb-111">Pour plus d’informations sur les ressources Azure et Resource Manager, voir [Présentation d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="492fb-112">Pour gérer les ressources Azure avec l’interface de ligne de commande Azure, vous devez [installer l’interface de ligne de commande Azure](../cli-install-nodejs.md) et vous [connecter à Azure](../xplat-cli-connect.md) en utilisant la commande `azure login`.</span><span class="sxs-lookup"><span data-stu-id="492fb-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="492fb-113">Assurez-vous que l’interface de ligne de commande est en mode Resource Manager (exécutez `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="492fb-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="492fb-114">Si ces opérations ont déjà été effectuées, vous pouvez dès à présent créer et gérer ces ressources.</span><span class="sxs-lookup"><span data-stu-id="492fb-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="492fb-115">Obtenir des ressources et des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="492fb-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="492fb-116">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="492fb-116">Resource groups</span></span>
<span data-ttu-id="492fb-117">Pour obtenir une liste de tous les groupes de ressources dans votre abonnement et leurs emplacements, exécutez cette commande.</span><span class="sxs-lookup"><span data-stu-id="492fb-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="492fb-118">Ressources</span><span class="sxs-lookup"><span data-stu-id="492fb-118">Resources</span></span>
 <span data-ttu-id="492fb-119">Pour répertorier toutes les ressources d’un groupe, par exemple une ressource ayant pour nom *testRG*, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492fb-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="492fb-120">Pour afficher une ressource individuelle dans le groupe, par exemple une machine virtuelle nommée *MyUbuntuVM*, utilisez une commande du type de celle qui suit :</span><span class="sxs-lookup"><span data-stu-id="492fb-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="492fb-121">Notez le paramètre **Microsoft.Compute/virtualMachines**.</span><span class="sxs-lookup"><span data-stu-id="492fb-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="492fb-122">Il indique le type de la ressource sur laquelle vous demandez des informations.</span><span class="sxs-lookup"><span data-stu-id="492fb-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="492fb-123">Quand vous utilisez des commandes **azure resource** autres que la commande **list**, vous devez spécifier la version de l’API de la ressource avec laquelle vous travaillez au moyen du paramètre **-o**.</span><span class="sxs-lookup"><span data-stu-id="492fb-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="492fb-124">Si vous ne connaissez pas la version de l’API à utiliser, consultez le fichier de modèle et recherchez le champ apiVersion de la ressource.</span><span class="sxs-lookup"><span data-stu-id="492fb-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="492fb-125">Pour plus d’informations sur les versions d’API dans Gestionnaire des ressources, consultez [Fournisseurs et types de ressources](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="492fb-126">Lorsque vous affichez des détails sur une ressource, il est souvent utile d'utiliser le paramètre `--json`.</span><span class="sxs-lookup"><span data-stu-id="492fb-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="492fb-127">Il rend la sortie plus lisible, car certaines valeurs sont des structures imbriquées ou des ensembles de valeurs collectées.</span><span class="sxs-lookup"><span data-stu-id="492fb-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="492fb-128">L’exemple suivant montre les résultats renvoyés par la commande **show** dans un document JSON.</span><span class="sxs-lookup"><span data-stu-id="492fb-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="492fb-129">Si vous le voulez, vous pouvez enregistrer les données JSON dans un fichier au moyen du caractère&gt; pour diriger la sortie vers un fichier.</span><span class="sxs-lookup"><span data-stu-id="492fb-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="492fb-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="492fb-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="492fb-131">Balises</span><span class="sxs-lookup"><span data-stu-id="492fb-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="492fb-132">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="492fb-132">Manage resources</span></span>
<span data-ttu-id="492fb-133">Pour ajouter une ressource telle qu’un compte de stockage à un groupe de ressources, exécutez une commande du type :</span><span class="sxs-lookup"><span data-stu-id="492fb-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="492fb-134">En plus de spécifier la version de l’API de la ressource avec le paramètre **-o**, utilisez le paramètre **-p** pour transmettre une chaîne au format JSON contenant toutes les propriétés requises ou supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="492fb-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="492fb-135">Pour supprimer une ressource existante, par exemple une ressource de machine virtuelle, utilisez une commande du type suivant :</span><span class="sxs-lookup"><span data-stu-id="492fb-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="492fb-136">Pour déplacer des ressources existantes vers un autre groupe de ressources ou un autre abonnement, exécutez la commande **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="492fb-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="492fb-137">L’exemple suivant montre comment déplacer un cache Redis vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="492fb-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="492fb-138">Dans le paramètre **-i** , spécifiez une liste séparée par des virgules des ID des ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="492fb-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="492fb-139">Contrôler l’accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="492fb-139">Control access to resources</span></span>
<span data-ttu-id="492fb-140">Vous pouvez utiliser l’interface de ligne de commande Azure pour créer et gérer des stratégies et ainsi contrôler l’accès aux ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="492fb-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="492fb-141">Pour plus d’informations sur les définitions de stratégie et l’affectation de stratégies aux ressources, voir [Utiliser la stratégie pour gérer les ressources et contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="492fb-142">Par exemple, définissez la stratégie suivante pour refuser toutes les demandes dans lesquelles l’emplacement n’est pas Ouest des États-Unis ou Amérique du Nord, puis enregistrez-la dans le fichier de définition de stratégie policy.json :</span><span class="sxs-lookup"><span data-stu-id="492fb-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="492fb-143">Exécutez ensuite la commande **policy definition create** :</span><span class="sxs-lookup"><span data-stu-id="492fb-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="492fb-144">Cette commande propose une sortie du type suivant :</span><span class="sxs-lookup"><span data-stu-id="492fb-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="492fb-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="492fb-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="492fb-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="492fb-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="492fb-147">Pour attribuer une stratégie correspondant à l’étendue souhaitée, utilisez la valeur **PolicyDefinitionId** renvoyée par la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="492fb-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="492fb-148">Dans l’exemple suivant, cette étendue est l’abonnement, mais il peut s’agir de ressources individuelles ou de groupes de ressources :</span><span class="sxs-lookup"><span data-stu-id="492fb-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="492fb-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="492fb-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="492fb-150">Vous pouvez obtenir, modifier ou supprimer des définitions de stratégie à l’aide des commandes **policy definition show**, **policy definition set** et **policy definition delete**.</span><span class="sxs-lookup"><span data-stu-id="492fb-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="492fb-151">De même, vous pouvez obtenir, modifier ou supprimer des affectations de stratégie à l’aide des commandes **policy assignment show**, **policy assignment set** et **policy assignment delete**.</span><span class="sxs-lookup"><span data-stu-id="492fb-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="492fb-152">Exporter un groupe de ressources en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="492fb-152">Export a resource group as a template</span></span>
<span data-ttu-id="492fb-153">Vous pouvez afficher le modèle Resource Manager pour un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="492fb-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="492fb-154">L’exportation du modèle offre deux avantages :</span><span class="sxs-lookup"><span data-stu-id="492fb-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="492fb-155">Vous pouvez facilement automatiser les prochains déploiements de la solution, car l’ensemble de l’infrastructure est défini dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="492fb-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="492fb-156">Vous pouvez vous familiariser avec la syntaxe de modèle en regardant dans la JSON qui représente votre solution.</span><span class="sxs-lookup"><span data-stu-id="492fb-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="492fb-157">À l’aide de l’interface de ligne de commande Azure, vous pouvez exporter un modèle qui représente l’état actuel de votre groupe de ressources ou télécharger le modèle qui a été utilisé pour un déploiement spécifique.</span><span class="sxs-lookup"><span data-stu-id="492fb-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="492fb-158">**L’exportation du modèle pour un groupe de ressources** est utile lorsque vous avez apporté des modifications à un groupe de ressources et que vous devez récupérer la représentation JSON de son état actuel.</span><span class="sxs-lookup"><span data-stu-id="492fb-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="492fb-159">Toutefois, le modèle généré contient uniquement un nombre minimal de paramètres et aucune variable.</span><span class="sxs-lookup"><span data-stu-id="492fb-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="492fb-160">La plupart des valeurs dans le modèle sont codées en dur.</span><span class="sxs-lookup"><span data-stu-id="492fb-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="492fb-161">Avant de déployer le modèle généré, vous pouvez convertir plusieurs valeurs en paramètres afin de personnaliser le déploiement pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="492fb-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="492fb-162">Pour exporter le modèle pour un groupe de ressources dans un répertoire local, exécutez la commande `azure group export` comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="492fb-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="492fb-163">(Indiquez un répertoire local adapté à l’environnement de votre système d’exploitation.)</span><span class="sxs-lookup"><span data-stu-id="492fb-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="492fb-164">**Le téléchargement du modèle pour un déploiement spécifique** est utile lorsque vous avez besoin d’afficher le modèle réel qui a été utilisé pour déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="492fb-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="492fb-165">Ce modèle comprend tous les paramètres et toutes les variables définis pour le déploiement d’origine.</span><span class="sxs-lookup"><span data-stu-id="492fb-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="492fb-166">Toutefois, si un membre de votre organisation a apporté des modifications au groupe de ressources et que celles-ci ne sont pas définies dans le modèle, ce dernier ne représente pas l’état actuel du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="492fb-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="492fb-167">Pour télécharger le modèle utilisé pour un déploiement spécifique dans un répertoire local, exécutez la commande `azure group deployment template download`.</span><span class="sxs-lookup"><span data-stu-id="492fb-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="492fb-168">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="492fb-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="492fb-169">L’exportation de modèle est en version préliminaire. Elle n’est pas encore prise en charge par tous les types de ressources.</span><span class="sxs-lookup"><span data-stu-id="492fb-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="492fb-170">Lorsque vous tentez d’exporter un modèle, une erreur indiquant que certaines ressources n’ont pas été exportées peut s’afficher.</span><span class="sxs-lookup"><span data-stu-id="492fb-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="492fb-171">Le cas échéant, définissez ces ressources manuellement dans votre modèle après l’avoir téléchargé.</span><span class="sxs-lookup"><span data-stu-id="492fb-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="492fb-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="492fb-172">Next steps</span></span>
* <span data-ttu-id="492fb-173">Pour obtenir des informations détaillées sur les opérations de déploiement et résoudre les erreurs de déploiement avec l’interface de ligne de commande Azure, voir [Afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="492fb-174">Si vous souhaitez utiliser l’interface de ligne de commande pour configurer une application ou un script afin d’accéder aux ressources, voir [Créer un principal du service pour accéder aux ressources à l’aide de l’interface de ligne de commande (CLI) Azure](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="492fb-175">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="492fb-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

