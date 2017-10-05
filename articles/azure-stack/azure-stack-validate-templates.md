---
title: "Utiliser le validateur de modèle pour vérifier des modèles pour Azure Stack | Microsoft Docs"
description: "Vérifier des modèles pour un déploiement sur Azure Stack"
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
ms.openlocfilehash: bb1d624f4c73bcd5f41dde2d0b13c57c880eca05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="72837-103">Vérifier vos modèles pour Azure Stack par le validateur de modèle</span><span class="sxs-lookup"><span data-stu-id="72837-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="72837-104">Vous pouvez utiliser l’outil de validation des modèles pour vérifier si vos [modèles](azure-stack-arm-templates.md) Azure Resource Manager sont prêts pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-104">You can use the template validation tool to check if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="72837-105">L’outil de validation des modèles fait partie des outils disponibles avec Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-105">The template validation tool is available as a part of the Azure Stack tools.</span></span> <span data-ttu-id="72837-106">Téléchargez les outils Azure Stack en utilisant la procédure décrite dans l’article [Télécharger des outils à partir de GitHub](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="72837-106">Download the Azure Stack tools by using the steps described in the [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="72837-107">Pour valider des modèles, vous utilisez les modules PowerShell suivants et le fichier JSON situé dans les dossiers **TemplateValidator** et **CloudCapabilities** :</span><span class="sxs-lookup"><span data-stu-id="72837-107">To validate templates, you use the following PowerShell modules and the JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="72837-108">AzureRM.CloudCapabilities.psm1 crée un fichier JSON des fonctionnalités du cloud représentant les services et versions présentes dans un cloud comme Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing the services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="72837-109">AzureRM.TemplateValidator.psm1 utilise un fichier JSON des fonctionnalités du cloud pour tester des modèles en vue d’un déploiement dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file to test templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="72837-110">AzureStackCloudCapabilities_with_AddOns_20170627.json est un fichier des fonctionnalités du cloud par défaut.</span><span class="sxs-lookup"><span data-stu-id="72837-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="72837-111">Vous pouvez créer votre propre fichier ou utiliser ce fichier pour commencer.</span><span class="sxs-lookup"><span data-stu-id="72837-111">You can create your own, or use this file to get started.</span></span> 

<span data-ttu-id="72837-112">Dans cette rubrique, vous aller exécuter une validation de vos modèles, et éventuellement générer un fichier des fonctionnalités du cloud.</span><span class="sxs-lookup"><span data-stu-id="72837-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="72837-113">Valider des modèles</span><span class="sxs-lookup"><span data-stu-id="72837-113">Validate templates</span></span>
<span data-ttu-id="72837-114">Dans cette procédure, vous allez valider des modèles à l’aide du module PowerShell AzureRM.TemplateValidator.</span><span class="sxs-lookup"><span data-stu-id="72837-114">In these steps, you validate templates by using the AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="72837-115">Vous pouvez utiliser vos propres modèles, ou valider les [modèles de démarrage rapide Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="72837-115">You can use your own templates, or validate the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="72837-116">Importez le module PowerShell AzureRM.TemplateValidator.psm1 :</span><span class="sxs-lookup"><span data-stu-id="72837-116">Import the AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="72837-117">Exécutez le validateur de modèle :</span><span class="sxs-lookup"><span data-stu-id="72837-117">Run the template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path to template.json or template folder> `
    -CapabilitiesPath <path to cloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="72837-118">Les avertissements ou erreurs de validation de modèle sont journalisés sur la console PowerShell, ainsi que dans un fichier HTML situé dans le répertoire source.</span><span class="sxs-lookup"><span data-stu-id="72837-118">Any template validation warnings or errors are logged to the PowerShell console, and are also logged to an HTML file in the source directory.</span></span> <span data-ttu-id="72837-119">La sortie de rapport de validation peut se présenter ainsi :</span><span class="sxs-lookup"><span data-stu-id="72837-119">An example of the validation report output looks like this:</span></span>

![exemple de rapport de validation](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="72837-121">Paramètres</span><span class="sxs-lookup"><span data-stu-id="72837-121">Parameters</span></span>

| <span data-ttu-id="72837-122">Paramètre</span><span class="sxs-lookup"><span data-stu-id="72837-122">Parameter</span></span> | <span data-ttu-id="72837-123">Description</span><span class="sxs-lookup"><span data-stu-id="72837-123">Description</span></span> | <span data-ttu-id="72837-124">Requis</span><span class="sxs-lookup"><span data-stu-id="72837-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="72837-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="72837-125">TemplatePath</span></span> | <span data-ttu-id="72837-126">Spécifie le chemin pour rechercher des modèles Resource Manager de manière récursive</span><span class="sxs-lookup"><span data-stu-id="72837-126">Specifies the path to recursively find Resource Manager templates</span></span> | <span data-ttu-id="72837-127">Oui</span><span class="sxs-lookup"><span data-stu-id="72837-127">Yes</span></span> | 
| <span data-ttu-id="72837-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="72837-128">TemplatePattern</span></span> | <span data-ttu-id="72837-129">Spécifie le nom des fichiers de modèle à faire correspondre</span><span class="sxs-lookup"><span data-stu-id="72837-129">Specifies the name of template files to match.</span></span> | <span data-ttu-id="72837-130">Non</span><span class="sxs-lookup"><span data-stu-id="72837-130">No</span></span> |
| <span data-ttu-id="72837-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="72837-131">CapabilitiesPath</span></span> | <span data-ttu-id="72837-132">Spécifie le chemin du fichier JSON des fonctionnalités du cloud</span><span class="sxs-lookup"><span data-stu-id="72837-132">Specifies the path to cloud capabilities JSON file</span></span> | <span data-ttu-id="72837-133">Oui</span><span class="sxs-lookup"><span data-stu-id="72837-133">Yes</span></span> | 
| <span data-ttu-id="72837-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="72837-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="72837-135">Inclut l’évaluation de ressources IaaS telles que des tailles de machine virtuelle et des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="72837-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="72837-136">Non</span><span class="sxs-lookup"><span data-stu-id="72837-136">No</span></span> |
| <span data-ttu-id="72837-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="72837-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="72837-138">Inclut l’évaluation de ressources de stockage comme des types de références (SKU)</span><span class="sxs-lookup"><span data-stu-id="72837-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="72837-139">Non</span><span class="sxs-lookup"><span data-stu-id="72837-139">No</span></span> |
| <span data-ttu-id="72837-140">Rapport</span><span class="sxs-lookup"><span data-stu-id="72837-140">Report</span></span> | <span data-ttu-id="72837-141">Spécifie le nom du rapport HTML généré</span><span class="sxs-lookup"><span data-stu-id="72837-141">Specifies name of the generated HTML report</span></span> | <span data-ttu-id="72837-142">Non</span><span class="sxs-lookup"><span data-stu-id="72837-142">No</span></span> |
| <span data-ttu-id="72837-143">Détaillé</span><span class="sxs-lookup"><span data-stu-id="72837-143">Verbose</span></span> | <span data-ttu-id="72837-144">Journalise les erreurs et les avertissements dans la console</span><span class="sxs-lookup"><span data-stu-id="72837-144">Logs errors and warnings to the console</span></span> | <span data-ttu-id="72837-145">Non</span><span class="sxs-lookup"><span data-stu-id="72837-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="72837-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="72837-146">Examples</span></span>
<span data-ttu-id="72837-147">Cet exemple valide tous les [modèles de démarrage rapide Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates) téléchargés localement. Il valide également les tailles et extensions de machine virtuelle par rapport aux fonctionnalités du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-147">This example validates all the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates the VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="72837-148">Générer le fichier des fonctionnalités du cloud</span><span class="sxs-lookup"><span data-stu-id="72837-148">Build cloud capabilities file</span></span>
<span data-ttu-id="72837-149">Les fichiers téléchargés incluent un fichier *AzureStackCloudCapabilities_with_AddOns_20170627.json* par défaut, qui décrit les versions de services disponibles dans le Kit de développement Azure Stack avec les services PaaS installés.</span><span class="sxs-lookup"><span data-stu-id="72837-149">The downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes the service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="72837-150">Si vous installez des fournisseurs de ressources supplémentaires, vous pouvez utiliser le module PowerShell AzureRM.CloudCapabilities pour générer un fichier JSON incluant les nouveaux services.</span><span class="sxs-lookup"><span data-stu-id="72837-150">If you install additional Resource Providers, you can use the AzureRM.CloudCapabilities PowerShell module to build a JSON file including the new services.</span></span>  

1.  <span data-ttu-id="72837-151">Vérifiez que vous disposez d’une connectivité à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="72837-151">Make sure you have connectivity to Azure Stack.</span></span>  <span data-ttu-id="72837-152">Cette procédure peut être effectuée à partir de l’hôte de kit de développement Azure Stack, ou vous pouvez utiliser un [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) pour vous connecter à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="72837-152">These steps can be performed from the Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) to connect from your workstation.</span></span> 
2.  <span data-ttu-id="72837-153">Importez le module PowerShell AzureRM.CloudCapabilities :</span><span class="sxs-lookup"><span data-stu-id="72837-153">Import the AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="72837-154">Utilisez l’applet de commande Get-CloudCapabilities pour récupérer des versions de services et créer un fichier JSON des fonctionnalités du cloud :</span><span class="sxs-lookup"><span data-stu-id="72837-154">Use the Get-CloudCapabilities cmdlet to retrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="72837-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72837-155">Next steps</span></span>
 - [<span data-ttu-id="72837-156">Déployer des modèles sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="72837-156">Deploy templates to Azure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="72837-157">[Développer des modèles pour Azure Stack] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="72837-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

