---
title: aaaExporting des groupes de ressources Azure qui contiennent des extensions de machine virtuelle | Documents Microsoft
description: "Exportez des modèles Resource Manager qui incluent des extensions de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="9137a-103">Exportation de groupes de ressources contenant des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9137a-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="9137a-104">Des groupes de ressources Azure peuvent être exportés dans un nouveau modèle Resource Manager qui peut alors être redéployé.</span><span class="sxs-lookup"><span data-stu-id="9137a-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="9137a-105">Hello processus d’exportation interprète les ressources existantes et crée un modèle de gestionnaire de ressources que lors du déploiement des résultats dans un groupe de ressources similaires.</span><span class="sxs-lookup"><span data-stu-id="9137a-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="9137a-106">Lorsque vous utilisez l’option d’exportation hello groupe de ressources par rapport à un groupe de ressources contenant les extensions de Machine virtuelle, toobe de besoin de plusieurs éléments considérées comme telles que de la compatibilité d’extension et protégés de paramètres.</span><span class="sxs-lookup"><span data-stu-id="9137a-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="9137a-107">Ce document décrit en détail le fonctionnement de hello processus d’exportation de groupe de ressources en ce qui concerne les extensions de machine virtuelle, notamment une liste de prise en charge les extensions, et plus d’informations sur la gestion des données sécurisées.</span><span class="sxs-lookup"><span data-stu-id="9137a-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="9137a-108">Extensions de machine virtuelle prises en charge</span><span class="sxs-lookup"><span data-stu-id="9137a-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="9137a-109">De nombreuses extensions de machine virtuelle sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="9137a-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="9137a-110">Toutes les extensions ne peuvent être exportées dans un modèle de gestionnaire de ressources à l’aide de la fonctionnalité de « Script d’automatisation » hello.</span><span class="sxs-lookup"><span data-stu-id="9137a-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="9137a-111">Si une extension de machine virtuelle n’est pas pris en charge, il doit toobe manuellement replacée dans les modèles exportés hello.</span><span class="sxs-lookup"><span data-stu-id="9137a-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="9137a-112">Hello extensions suivantes peuvent être exportées avec la fonctionnalité de script d’automation hello.</span><span class="sxs-lookup"><span data-stu-id="9137a-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="9137a-113">Extension</span><span class="sxs-lookup"><span data-stu-id="9137a-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="9137a-114">Sauvegarde Acronis</span><span class="sxs-lookup"><span data-stu-id="9137a-114">Acronis Backup</span></span> | <span data-ttu-id="9137a-115">Agent Datadog Windows</span><span class="sxs-lookup"><span data-stu-id="9137a-115">Datadog Windows Agent</span></span> | <span data-ttu-id="9137a-116">Application de correctifs au système d’exploitation pour Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-116">OS Patching For Linux</span></span> | <span data-ttu-id="9137a-117">Instantané de machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="9137a-118">Sauvegarde Acronis Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-118">Acronis Backup Linux</span></span> | <span data-ttu-id="9137a-119">Extension Docker</span><span class="sxs-lookup"><span data-stu-id="9137a-119">Docker Extension</span></span> | <span data-ttu-id="9137a-120">Agent Puppet</span><span class="sxs-lookup"><span data-stu-id="9137a-120">Puppet Agent</span></span> |
| <span data-ttu-id="9137a-121">Infos Bg</span><span class="sxs-lookup"><span data-stu-id="9137a-121">Bg Info</span></span> | <span data-ttu-id="9137a-122">Extension DSC</span><span class="sxs-lookup"><span data-stu-id="9137a-122">DSC Extension</span></span> | <span data-ttu-id="9137a-123">Aperçu Apm 24 x 7 de site</span><span class="sxs-lookup"><span data-stu-id="9137a-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="9137a-124">Agent BMC CTM Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="9137a-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-125">Dynatrace Linux</span></span> | <span data-ttu-id="9137a-126">Serveur Linux 24 x 7 de site</span><span class="sxs-lookup"><span data-stu-id="9137a-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="9137a-127">Agent BMC CTM Windows</span><span class="sxs-lookup"><span data-stu-id="9137a-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="9137a-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="9137a-128">Dynatrace Windows</span></span> | <span data-ttu-id="9137a-129">Windows Server 24 x 7 de site</span><span class="sxs-lookup"><span data-stu-id="9137a-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="9137a-130">Client Chef</span><span class="sxs-lookup"><span data-stu-id="9137a-130">Chef Client</span></span> | <span data-ttu-id="9137a-131">Application de sécurité HPE Defender</span><span class="sxs-lookup"><span data-stu-id="9137a-131">HPE Security Application Defender</span></span> | <span data-ttu-id="9137a-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="9137a-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="9137a-133">Script personnalisé</span><span class="sxs-lookup"><span data-stu-id="9137a-133">Custom Script</span></span> | <span data-ttu-id="9137a-134">Logiciel anti-programme malveillant IaaS</span><span class="sxs-lookup"><span data-stu-id="9137a-134">IaaS Antimalware</span></span> | <span data-ttu-id="9137a-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="9137a-136">Extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="9137a-136">Custom Script Extension</span></span> | <span data-ttu-id="9137a-137">Diagnostics IaaS</span><span class="sxs-lookup"><span data-stu-id="9137a-137">IaaS Diagnostics</span></span> | <span data-ttu-id="9137a-138">Accès aux machines virtuelles pour Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-138">VM Access For Linux</span></span> |
| <span data-ttu-id="9137a-139">Script personnalisé pour Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-139">Custom Script for Linux</span></span> | <span data-ttu-id="9137a-140">Client Chef Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-140">Linux Chef Client</span></span> | <span data-ttu-id="9137a-141">Accès aux machines virtuelles pour Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-141">VM Access For Linux</span></span> |
| <span data-ttu-id="9137a-142">Agent Datadog Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-142">Datadog Linux Agent</span></span> | <span data-ttu-id="9137a-143">Diagnostic Linux</span><span class="sxs-lookup"><span data-stu-id="9137a-143">Linux Diagnostic</span></span> | <span data-ttu-id="9137a-144">Instantané de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9137a-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="9137a-145">Exportation hello groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9137a-145">Export hello Resource Group</span></span>

<span data-ttu-id="9137a-146">tooexport un groupe de ressources dans un modèle réutilisable, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="9137a-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="9137a-147">Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9137a-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="9137a-148">Sur hello Menu Hub, cliquez sur groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="9137a-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="9137a-149">Sélectionnez le groupe de ressources cible hello à partir de la liste de hello</span><span class="sxs-lookup"><span data-stu-id="9137a-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="9137a-150">Dans le panneau de groupe de ressources hello, cliquez sur le Script d’automatisation</span><span class="sxs-lookup"><span data-stu-id="9137a-150">In hello Resource Group blade, click Automation Script</span></span>

![Exportation de modèle](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="9137a-152">Hello script automatisations de Azure Resource Manager génère un modèle de gestionnaire de ressources, un fichier de paramètres et plusieurs exemples de scripts de déploiement tels que PowerShell et CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9137a-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="9137a-153">À ce stade, les modèles exportés hello peuvent être téléchargé à l’aide du bouton de téléchargement hello, ajouté en tant que nouveau modèle toohello modèle bibliothèque ou déployé à l’aide de hello bouton déployer.</span><span class="sxs-lookup"><span data-stu-id="9137a-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="9137a-154">Configurer les paramètres protégés</span><span class="sxs-lookup"><span data-stu-id="9137a-154">Configure protected settings</span></span>

<span data-ttu-id="9137a-155">Plusieurs extensions de machine virtuelle Azure incluent une configuration de paramètres protégés, qui chiffre les données sensibles telles que les informations d’identification et les chaînes de configuration.</span><span class="sxs-lookup"><span data-stu-id="9137a-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="9137a-156">Les paramètres protégés ne sont pas exportés avec script d’automatisation hello.</span><span class="sxs-lookup"><span data-stu-id="9137a-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="9137a-157">Si les paramètres nécessaires, protégés doivent toobe réinséré hello exportée basé sur un modèle.</span><span class="sxs-lookup"><span data-stu-id="9137a-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="9137a-158">Étape 1 : Supprimer un paramètre de modèle</span><span class="sxs-lookup"><span data-stu-id="9137a-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="9137a-159">Lorsque hello que groupe de ressources sont exporté, un paramètre de modèle unique est créé tooprovide un toohello valeur exporté les paramètres protégés.</span><span class="sxs-lookup"><span data-stu-id="9137a-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="9137a-160">Ce paramètre peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="9137a-160">This parameter can be removed.</span></span> <span data-ttu-id="9137a-161">tooremove hello, examinez la liste de paramètres hello et supprimer le paramètre hello qui recherche d’exemple JSON toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="9137a-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="9137a-162">Étape 2 : Obtenir les propriétés des paramètres protégés</span><span class="sxs-lookup"><span data-stu-id="9137a-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="9137a-163">Étant donné que chaque paramètre protégé a un jeu de propriétés requis, une liste de ces propriétés doivent toobe collectée.</span><span class="sxs-lookup"><span data-stu-id="9137a-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="9137a-164">Vous trouverez chaque paramètre de configuration des paramètres protégés hello Bonjour [schéma Azure Resource Manager sur GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="9137a-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="9137a-165">Ce schéma inclut uniquement les jeux de paramètres hello pour les extensions hello répertoriées dans la section vue d’ensemble de hello de ce document.</span><span class="sxs-lookup"><span data-stu-id="9137a-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="9137a-166">Dans le référentiel de schéma hello, de rechercher les extension hello que vous le souhaitez, pour cet exemple `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="9137a-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="9137a-167">Une fois hello extensions `protectedSettings` objet a été trouvé, prenez note de chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="9137a-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="9137a-168">Dans l’exemple hello Hello `IaasDiagnostic` extension, hello requièrent les paramètres sont `storageAccountName`, `storageAccountKey`, et `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="9137a-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="9137a-169">Étape 3 - créer de nouveau la configuration de hello protégé</span><span class="sxs-lookup"><span data-stu-id="9137a-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="9137a-170">On hello modèle exporté, recherchez `protectedSettings` et remplacer hello exportée protégé définition de l’objet avec une autre qui inclut des paramètres d’extension hello requis et une valeur pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="9137a-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="9137a-171">Dans l’exemple hello Hello `IaasDiagnostic` extension, nouvelle configuration de paramètre protégé hello ressemblerait hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9137a-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="9137a-172">ressource d’extension finale Hello ressemble toohello comme exemple de JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="9137a-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="9137a-173">Si vous utilisez des valeurs de propriété tooprovide modèle paramètres, ceux-ci doivent toobe créé.</span><span class="sxs-lookup"><span data-stu-id="9137a-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="9137a-174">Lorsque vous créez des paramètres de modèle pour les valeurs de paramètre de protection par, assurez-vous que toouse hello `SecureString` le type de paramètre, afin que les valeurs sensibles sont sécurisés.</span><span class="sxs-lookup"><span data-stu-id="9137a-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="9137a-175">Pour en savoir plus sur l’utilisation des paramètres, consultez [Création de modèles Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9137a-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9137a-176">Dans l’exemple hello Hello `IaasDiagnostic` extension, hello paramètres suivants est créé dans la section des paramètres de modèle de gestionnaire de ressources hello hello.</span><span class="sxs-lookup"><span data-stu-id="9137a-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="9137a-177">À ce stade, le modèle de hello peut être déployé à l’aide de n’importe quelle méthode de déploiement de modèle.</span><span class="sxs-lookup"><span data-stu-id="9137a-177">At this point, hello template can be deployed using any template deployment method.</span></span>
