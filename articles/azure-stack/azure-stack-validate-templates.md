---
title: "modèles de toocheck aaaUse validateur de modèle pour la pile de Azure | Documents Microsoft"
description: "Vérifier les modèles de déploiement tooAzure pile"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="faa74-103">Vérifier vos modèles pour Azure Stack par le validateur de modèle</span><span class="sxs-lookup"><span data-stu-id="faa74-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="faa74-104">Vous pouvez utiliser toocheck d’outil de validation de modèle hello si votre gestionnaire de ressources Azure [modèles](azure-stack-arm-templates.md) sont prêts pour la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="faa74-104">You can use hello template validation tool toocheck if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="faa74-105">outil de validation de modèle Hello est disponible dans le cadre des outils de pile de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="faa74-105">hello template validation tool is available as a part of hello Azure Stack tools.</span></span> <span data-ttu-id="faa74-106">Télécharger les outils de pile de Azure hello à l’aide de hello étapes de hello [télécharger les outils à partir de GitHub](azure-stack-powershell-download.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="faa74-106">Download hello Azure Stack tools by using hello steps described in hello [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="faa74-107">les modèles toovalidate, vous utilisez hello suivant des modules PowerShell et hello JSON fichier situé dans **TemplateValidator** et **CloudCapabilities** dossiers :</span><span class="sxs-lookup"><span data-stu-id="faa74-107">toovalidate templates, you use hello following PowerShell modules and hello JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="faa74-108">AzureRM.CloudCapabilities.psm1 crée un fichier JSON de fonctionnalités cloud représentant les services hello et les versions dans un cloud comme Azure pile.</span><span class="sxs-lookup"><span data-stu-id="faa74-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing hello services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="faa74-109">AzureRM.TemplateValidator.psm1 utilise un modèles de tootest de fichiers JSON des capacités du cloud pour le déploiement dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="faa74-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file tootest templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="faa74-110">AzureStackCloudCapabilities_with_AddOns_20170627.json est un fichier des fonctionnalités du cloud par défaut.</span><span class="sxs-lookup"><span data-stu-id="faa74-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="faa74-111">Vous pouvez créer vos propres ou utiliser ce tooget fichier a démarré.</span><span class="sxs-lookup"><span data-stu-id="faa74-111">You can create your own, or use this file tooget started.</span></span> 

<span data-ttu-id="faa74-112">Dans cette rubrique, vous aller exécuter une validation de vos modèles, et éventuellement générer un fichier des fonctionnalités du cloud.</span><span class="sxs-lookup"><span data-stu-id="faa74-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="faa74-113">Valider des modèles</span><span class="sxs-lookup"><span data-stu-id="faa74-113">Validate templates</span></span>
<span data-ttu-id="faa74-114">Dans ces étapes, valider les modèles à l’aide du module PowerShell de AzureRM.TemplateValidator de hello.</span><span class="sxs-lookup"><span data-stu-id="faa74-114">In these steps, you validate templates by using hello AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="faa74-115">Vous pouvez utiliser vos propres modèles, ou valider hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="faa74-115">You can use your own templates, or validate hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="faa74-116">Module d’importation hello AzureRM.TemplateValidator.psm1 PowerShell :</span><span class="sxs-lookup"><span data-stu-id="faa74-116">Import hello AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="faa74-117">Validateur de modèle hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="faa74-117">Run hello template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="faa74-118">Les avertissements de validation de modèle ou les erreurs sont journalisées toohello PowerShell console et sont également consignées tooan HTML fichier dans le répertoire source hello.</span><span class="sxs-lookup"><span data-stu-id="faa74-118">Any template validation warnings or errors are logged toohello PowerShell console, and are also logged tooan HTML file in hello source directory.</span></span> <span data-ttu-id="faa74-119">Un exemple de sortie de rapport de validation hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="faa74-119">An example of hello validation report output looks like this:</span></span>

![exemple de rapport de validation](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="faa74-121">Paramètres</span><span class="sxs-lookup"><span data-stu-id="faa74-121">Parameters</span></span>

| <span data-ttu-id="faa74-122">Paramètre</span><span class="sxs-lookup"><span data-stu-id="faa74-122">Parameter</span></span> | <span data-ttu-id="faa74-123">Description</span><span class="sxs-lookup"><span data-stu-id="faa74-123">Description</span></span> | <span data-ttu-id="faa74-124">Requis</span><span class="sxs-lookup"><span data-stu-id="faa74-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="faa74-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="faa74-125">TemplatePath</span></span> | <span data-ttu-id="faa74-126">Spécifie toorecursively de chemin d’accès hello trouver des modèles de gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="faa74-126">Specifies hello path toorecursively find Resource Manager templates</span></span> | <span data-ttu-id="faa74-127">Oui</span><span class="sxs-lookup"><span data-stu-id="faa74-127">Yes</span></span> | 
| <span data-ttu-id="faa74-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="faa74-128">TemplatePattern</span></span> | <span data-ttu-id="faa74-129">Spécifie le nom hello de toomatch des fichiers de modèle.</span><span class="sxs-lookup"><span data-stu-id="faa74-129">Specifies hello name of template files toomatch.</span></span> | <span data-ttu-id="faa74-130">Non</span><span class="sxs-lookup"><span data-stu-id="faa74-130">No</span></span> |
| <span data-ttu-id="faa74-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="faa74-131">CapabilitiesPath</span></span> | <span data-ttu-id="faa74-132">Spécifie le fichier JSON fonctionnalités hello chemin d’accès toocloud</span><span class="sxs-lookup"><span data-stu-id="faa74-132">Specifies hello path toocloud capabilities JSON file</span></span> | <span data-ttu-id="faa74-133">Oui</span><span class="sxs-lookup"><span data-stu-id="faa74-133">Yes</span></span> | 
| <span data-ttu-id="faa74-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="faa74-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="faa74-135">Inclut l’évaluation de ressources IaaS telles que des tailles de machine virtuelle et des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="faa74-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="faa74-136">Non</span><span class="sxs-lookup"><span data-stu-id="faa74-136">No</span></span> |
| <span data-ttu-id="faa74-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="faa74-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="faa74-138">Inclut l’évaluation de ressources de stockage comme des types de références (SKU)</span><span class="sxs-lookup"><span data-stu-id="faa74-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="faa74-139">Non</span><span class="sxs-lookup"><span data-stu-id="faa74-139">No</span></span> |
| <span data-ttu-id="faa74-140">Rapport</span><span class="sxs-lookup"><span data-stu-id="faa74-140">Report</span></span> | <span data-ttu-id="faa74-141">Spécifie le nom de hello le rapport HTML généré</span><span class="sxs-lookup"><span data-stu-id="faa74-141">Specifies name of hello generated HTML report</span></span> | <span data-ttu-id="faa74-142">Non</span><span class="sxs-lookup"><span data-stu-id="faa74-142">No</span></span> |
| <span data-ttu-id="faa74-143">Détaillé</span><span class="sxs-lookup"><span data-stu-id="faa74-143">Verbose</span></span> | <span data-ttu-id="faa74-144">Console de toohello de journaux des erreurs et avertissements</span><span class="sxs-lookup"><span data-stu-id="faa74-144">Logs errors and warnings toohello console</span></span> | <span data-ttu-id="faa74-145">Non</span><span class="sxs-lookup"><span data-stu-id="faa74-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="faa74-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="faa74-146">Examples</span></span>
<span data-ttu-id="faa74-147">Cet exemple valide tous les hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates) téléchargé localement et valide également les tailles de machine virtuelle hello et des extensions par rapport aux fonctionnalités du Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="faa74-147">This example validates all hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates hello VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="faa74-148">Générer le fichier des fonctionnalités du cloud</span><span class="sxs-lookup"><span data-stu-id="faa74-148">Build cloud capabilities file</span></span>
<span data-ttu-id="faa74-149">les fichiers téléchargés Hello incluent une valeur par défaut *AzureStackCloudCapabilities_with_AddOns_20170627.json* fichier, qui décrit les versions de service hello disponibles dans le Kit de développement Azure pile avec les services PaaS.</span><span class="sxs-lookup"><span data-stu-id="faa74-149">hello downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes hello service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="faa74-150">Si vous installez des fournisseurs de ressources supplémentaires, vous pouvez utiliser un fichier JSON, y compris les nouveaux services de hello hello AzureRM.CloudCapabilities PowerShell module toobuild.</span><span class="sxs-lookup"><span data-stu-id="faa74-150">If you install additional Resource Providers, you can use hello AzureRM.CloudCapabilities PowerShell module toobuild a JSON file including hello new services.</span></span>  

1.  <span data-ttu-id="faa74-151">Assurez-vous que vous disposez de connectivité tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="faa74-151">Make sure you have connectivity tooAzure Stack.</span></span>  <span data-ttu-id="faa74-152">Ces étapes peuvent être effectuées à partir de l’hôte de kit de développement de Azure pile hello, ou vous pouvez utiliser [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="faa74-152">These steps can be performed from hello Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect from your workstation.</span></span> 
2.  <span data-ttu-id="faa74-153">Importez hello module AzureRM.CloudCapabilities PowerShell :</span><span class="sxs-lookup"><span data-stu-id="faa74-153">Import hello AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="faa74-154">Utilisez des versions de service de tooretrieve applet de commande Get-CloudCapabilities de hello et créer un fichier JSON de fonctionnalités cloud :</span><span class="sxs-lookup"><span data-stu-id="faa74-154">Use hello Get-CloudCapabilities cmdlet tooretrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="faa74-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="faa74-155">Next steps</span></span>
 - [<span data-ttu-id="faa74-156">Déployer des modèles tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="faa74-156">Deploy templates tooAzure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="faa74-157">[Développer des modèles pour Azure Stack] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="faa74-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

