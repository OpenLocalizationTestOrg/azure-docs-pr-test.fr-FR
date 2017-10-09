---
title: "ressources aaaManage avec hello CLI d’Azure | Documents Microsoft"
description: Utilisez hello Azure Interface de ligne de commande (CLI) toomanage Azure ressources et les groupes
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="32418-103">Utilisez hello CLI d’Azure toomanage Azure ressources et groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="32418-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32418-104">Portail</span><span class="sxs-lookup"><span data-stu-id="32418-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="32418-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="32418-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="32418-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="32418-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="32418-107">API REST</span><span class="sxs-lookup"><span data-stu-id="32418-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="32418-108">Bonjour Azure Interface de ligne (Azure) est un ou plusieurs outils, vous pouvez utiliser toodeploy et gérer les ressources avec le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="32418-109">Cet article présente toomanage façons courantes Azure ressources et groupes de ressources à l’aide de hello CLI d’Azure en mode de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="32418-110">Pour plus d’informations sur l’utilisation des ressources de toodeploy hello CLI, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32418-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="32418-111">Pour plus d’informations sur le Gestionnaire de ressources et les ressources Azure, visitez hello [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32418-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="32418-112">toomanage Azure ressources avec hello CLI d’Azure, vous devez trop[installer hello CLI d’Azure](../cli-install-nodejs.md), et [connecter tooAzure](../xplat-cli-connect.md) à l’aide de hello `azure login` commande.</span><span class="sxs-lookup"><span data-stu-id="32418-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="32418-113">Vérifiez que hello est CLI est en mode de gestionnaire de ressources (exécutez `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="32418-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="32418-114">Si vous avez effectué ces opérations, vous êtes prêt toogo.</span><span class="sxs-lookup"><span data-stu-id="32418-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="32418-115">Obtenir des ressources et des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="32418-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="32418-116">Groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="32418-116">Resource groups</span></span>
<span data-ttu-id="32418-117">tooget une liste de tous les groupes de ressources dans votre abonnement et leurs emplacements, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="32418-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="32418-118">Ressources</span><span class="sxs-lookup"><span data-stu-id="32418-118">Resources</span></span>
 <span data-ttu-id="32418-119">nom de toutes les ressources dans un groupe, tel que celui avec toolist *testRG*, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="32418-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="32418-120">tooview une ressource individuelle dans le groupe de hello, par exemple un ordinateur virtuel nommé *MyUbuntuVM*, utilisez une commande semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="32418-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="32418-121">Hello d’avis **Microsoft.Compute/virtualMachines** paramètre.</span><span class="sxs-lookup"><span data-stu-id="32418-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="32418-122">Ce paramètre indique le type hello de ressource hello que vous demandent des informations.</span><span class="sxs-lookup"><span data-stu-id="32418-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="32418-123">Lorsque vous utilisez hello **ressource azure** commandes autres que hello **liste** de commande, vous devez spécifier la version hello API de ressource de hello avec hello **-o** paramètre.</span><span class="sxs-lookup"><span data-stu-id="32418-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="32418-124">Si vous ne savez pas sur la version de l’API hello, consultez le fichier de modèle hello et trouver le champ d’apiVersion hello pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="32418-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="32418-125">Pour plus d’informations sur les versions d’API dans Gestionnaire des ressources, consultez [Fournisseurs et types de ressources](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="32418-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="32418-126">Lors de l’affichage des détails sur une ressource, il est souvent utile toouse hello `--json` paramètre.</span><span class="sxs-lookup"><span data-stu-id="32418-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="32418-127">Ce paramètre rend hello de sortie plus lisible, car certaines valeurs sont des structures imbriquées ou des collections.</span><span class="sxs-lookup"><span data-stu-id="32418-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="32418-128">exemple Hello illustre le retour de résultats hello Hello **afficher** en tant que document JSON.</span><span class="sxs-lookup"><span data-stu-id="32418-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="32418-129">Si vous le souhaitez, enregistrer hello toofile de données JSON à l’aide de hello &gt; fichier tooa de caractère toodirect hello sortie.</span><span class="sxs-lookup"><span data-stu-id="32418-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="32418-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="32418-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="32418-131">Balises</span><span class="sxs-lookup"><span data-stu-id="32418-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="32418-132">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="32418-132">Manage resources</span></span>
<span data-ttu-id="32418-133">tooadd une ressource telle qu’un groupe de ressources tooa du compte de stockage, exécutez une commande semblable à :</span><span class="sxs-lookup"><span data-stu-id="32418-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="32418-134">En outre toospecifying hello version de l’API de ressource de hello avec hello **-o** paramètre, utilisez hello **-p** paramètre toopass un format JSON en chaîne tout ou des propriétés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="32418-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="32418-135">toodelete une ressource existante comme une ressource d’ordinateur virtuel, utilisez une commande semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="32418-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="32418-136">toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello **du déplacement des Ressources azure** commande.</span><span class="sxs-lookup"><span data-stu-id="32418-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="32418-137">Hello suivant montre l’exemple de comment toomove un Cache Redis tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="32418-138">Bonjour **-i** paramètre, fournir une liste séparée par des virgules de toomove d’id de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="32418-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="32418-139">Contrôle l’accès tooresources</span><span class="sxs-lookup"><span data-stu-id="32418-139">Control access tooresources</span></span>
<span data-ttu-id="32418-140">Vous pouvez utiliser hello CLI d’Azure toocreate et gérer les stratégies toocontrol accès tooAzure ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="32418-141">Pour plus d’informations sur les définitions de stratégie et d’assignation tooresources de stratégies, consultez [utiliser les ressources de la stratégie toomanage et contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="32418-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="32418-142">Par exemple, définir hello suivant stratégie toodeny toutes les demandes où emplacement n’est pas ouest des États-Unis ou Amérique du Nord et enregistrez-le policy.json de fichier de définition de stratégie toohello :</span><span class="sxs-lookup"><span data-stu-id="32418-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="32418-143">Puis exécutez hello **création d’une définition de stratégie** commande :</span><span class="sxs-lookup"><span data-stu-id="32418-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="32418-144">Cette commande montre suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="32418-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="32418-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="32418-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="32418-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="32418-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="32418-147">tooassign une stratégie au niveau de la portée de hello souhaitée, utilisez hello **PolicyDefinitionId** retourné à partir de la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="32418-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="32418-148">Dans l’exemple suivant de hello, cette étendue est abonnement de hello, mais vous pouvez définir l’étendue tooresource groupes ou des ressources individuelles :</span><span class="sxs-lookup"><span data-stu-id="32418-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="32418-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="32418-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="32418-150">Vous pouvez obtenir, modifier ou supprimer des définitions de stratégie à l’aide de hello **afficher de définition de stratégie**, **jeu de définition de stratégie**, et **supprimer de la définition de la stratégie** commandes.</span><span class="sxs-lookup"><span data-stu-id="32418-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="32418-151">De même, vous pouvez obtenir, modifier ou supprimer des attributions de stratégies à l’aide de hello **afficher d’attribution de stratégie**, **jeu d’attribution de stratégie**, et **supprimer de l’affectation de stratégie** commandes .</span><span class="sxs-lookup"><span data-stu-id="32418-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="32418-152">Exporter un groupe de ressources en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="32418-152">Export a resource group as a template</span></span>
<span data-ttu-id="32418-153">Pour un groupe de ressources existant, vous pouvez afficher le modèle de gestionnaire de ressources hello pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="32418-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="32418-154">Exportation de modèle de hello offre deux avantages :</span><span class="sxs-lookup"><span data-stu-id="32418-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="32418-155">Vous pouvez automatiser facilement les futurs déploiements de solution de hello car toute infrastructure hello est défini dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="32418-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="32418-156">Vous pouvez vous familiariser avec la syntaxe de modèle en examinant hello JSON qui représente votre solution.</span><span class="sxs-lookup"><span data-stu-id="32418-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="32418-157">À l’aide de hello CLI d’Azure, vous pouvez exporter un modèle qui représente l’état actuel de hello de votre groupe de ressources, ou téléchargez le modèle hello qui a été utilisé pour un déploiement particulier.</span><span class="sxs-lookup"><span data-stu-id="32418-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="32418-158">**Exporter le modèle hello pour un groupe de ressources** -cela est utile lorsque le groupe de ressources tooa de modifications, et que vous avez besoin de tooretrieve hello représentation JSON de son état actuel.</span><span class="sxs-lookup"><span data-stu-id="32418-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="32418-159">Toutefois, le modèle généré de hello contient uniquement un nombre minimal de paramètres et aucune variable.</span><span class="sxs-lookup"><span data-stu-id="32418-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="32418-160">La plupart des valeurs hello dans le modèle de hello est codés en dur.</span><span class="sxs-lookup"><span data-stu-id="32418-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="32418-161">Avant de déployer le modèle de hello généré, vous souhaiterez tooconvert plusieurs des valeurs de hello dans les paramètres afin que vous pouvez personnaliser le déploiement hello pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="32418-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="32418-162">modèle de hello tooexport pour un groupe tooa local répertoire des ressources, exécutez hello `azure group export` commande comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="32418-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="32418-163">(Indiquez un répertoire local adapté à l’environnement de votre système d’exploitation.)</span><span class="sxs-lookup"><span data-stu-id="32418-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="32418-164">**Télécharger le modèle hello pour un déploiement particulier** --Ceci est utile lorsque vous avez besoin de modèle réel tooview hello qui a été utilisé toodeploy ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="32418-165">modèle de Hello inclut tous les paramètres et les variables définies pour le déploiement d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="32418-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="32418-166">Toutefois, si une personne de votre organisation a le groupe de ressources toohello modifications en dehors de la définition de hello dans le modèle de hello, ce modèle ne représente pas état actuel de hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="32418-167">modèle de hello toodownload utilisé pour un répertoire tooa local de déploiement particulier, exécutez hello `azure group deployment template download` commande.</span><span class="sxs-lookup"><span data-stu-id="32418-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="32418-168">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="32418-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="32418-169">L’exportation de modèle est en version préliminaire. Elle n’est pas encore prise en charge par tous les types de ressources.</span><span class="sxs-lookup"><span data-stu-id="32418-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="32418-170">Lors de la tentative de tooexport un modèle, vous pouvez voir une erreur indiquant que certaines ressources n’ont pas été exportés.</span><span class="sxs-lookup"><span data-stu-id="32418-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="32418-171">Le cas échéant, définissez ces ressources manuellement dans votre modèle après l’avoir téléchargé.</span><span class="sxs-lookup"><span data-stu-id="32418-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="32418-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32418-172">Next steps</span></span>
* <span data-ttu-id="32418-173">tooget les détails des opérations de déploiement et de résoudre les erreurs de déploiement avec hello CLI d’Azure, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="32418-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="32418-174">Si vous souhaitez toouse hello CLI tooset d’une application ou tooaccess des ressources de script, consultez [CLI d’Azure utilisation toocreate un principal de service tooaccess ressources](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32418-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="32418-175">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="32418-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

