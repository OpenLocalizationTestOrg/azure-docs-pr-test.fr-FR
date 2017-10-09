---
title: "fonctionnalités et extensions de l’ordinateur aaaVirtual pour Linux | Documents Microsoft"
description: "Découvrez les extensions disponibles pour les machines virtuelles, regroupées par ce qu’ils fournissent ou améliorent."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="e2931-103">Extensions et fonctionnalités de machine virtuelle pour Linux</span><span class="sxs-lookup"><span data-stu-id="e2931-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="e2931-104">Les extensions de machine virtuelle Azure sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="e2931-105">Par exemple, si un ordinateur virtuel requiert l’installation du logiciel, de protection antivirus ou de configuration de Docker, une extension de machine virtuelle peut être utilisé toocomplete ces tâches.</span><span class="sxs-lookup"><span data-stu-id="e2931-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="e2931-106">Les extensions de machine virtuelle Azure peuvent être exécutées à l’aide de hello CLI d’Azure PowerShell, les modèles Azure Resource Manager et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="e2931-107">Les extensions peuvent être associées à un nouveau déploiement de machine virtuelle ou s’exécuter sur tout système existant.</span><span class="sxs-lookup"><span data-stu-id="e2931-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="e2931-108">Ce document fournit une vue d’ensemble des extensions de machine virtuelle, les conditions préalables pour l’utilisation des extensions de machine virtuelle Azure et de conseils toodetect, gérer et supprimer des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e2931-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="e2931-109">Ce document fournit des informations générales, car de nombreuses extensions de machine virtuelle sont disponibles, chacune présentant une configuration potentiellement unique.</span><span class="sxs-lookup"><span data-stu-id="e2931-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="e2931-110">Vous trouverez plus d’informations spécifiques à l’extension dans chaque document spécifique toohello individuels d’extension.</span><span class="sxs-lookup"><span data-stu-id="e2931-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="e2931-111">Cas d’utilisation et exemples</span><span class="sxs-lookup"><span data-stu-id="e2931-111">Use cases and samples</span></span>

<span data-ttu-id="e2931-112">Plusieurs extensions de machine virtuelle Azure sont disponibles, chacune impliquant un cas d’utilisation spécifique.</span><span class="sxs-lookup"><span data-stu-id="e2931-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="e2931-113">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="e2931-113">Some examples are:</span></span>

- <span data-ttu-id="e2931-114">Appliquer l’état souhaité de PowerShell configurations tooa machine virtuelle hello extension DSC pour Linux.</span><span class="sxs-lookup"><span data-stu-id="e2931-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="e2931-115">Pour plus d’informations sur l’extension DSC Azure, consultez [cette page](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="e2931-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="e2931-116">Configurer la surveillance d’un ordinateur virtuel avec hello extension de machine virtuelle l’Agent de surveillance de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e2931-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="e2931-117">Pour plus d’informations, consultez [comment toomonitor un VM Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="e2931-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="e2931-118">Configurer la surveillance de votre infrastructure d’Azure avec hello Datadog extension.</span><span class="sxs-lookup"><span data-stu-id="e2931-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="e2931-119">Pour plus d’informations, consultez hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="e2931-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="e2931-120">Configurer un hôte Docker sur une machine virtuelle Azure à l’aide d’extension de machine virtuelle de Docker hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="e2931-121">Pour plus d’informations sur l’extension de machine virtuelle Docker, consultez [cet article](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="e2931-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="e2931-122">En outre extensions tooprocess spécifiques, une extension de Script personnalisé est disponible pour les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="e2931-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="e2931-123">Hello, extension de Script personnalisé pour Linux permet de n’importe quel toobe de script d’interpréteur de commandes s’exécutent sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e2931-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="e2931-124">Les scripts personnalisés s’avèrent utile pour concevoir des déploiements Azure qui nécessitent une configuration plus avancée que celle fournie par les outils Azure natifs.</span><span class="sxs-lookup"><span data-stu-id="e2931-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="e2931-125">Pour plus d’informations sur l’extension de script personnalisé pour les machines virtuelles Linux, consultez [cet article](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e2931-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e2931-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2931-126">Prerequisites</span></span>

<span data-ttu-id="e2931-127">Chaque extension de machine virtuelle peut présenter son propre ensemble de composants requis.</span><span class="sxs-lookup"><span data-stu-id="e2931-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="e2931-128">Par exemple, hello extension de machine virtuelle de Docker a une condition préalable d’une distribution Linux pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e2931-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="e2931-129">Configuration requise des extensions individuelles est détaillées dans la documentation spécifique à l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="e2931-130">Agent de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-130">Azure VM agent</span></span>

<span data-ttu-id="e2931-131">agent de machine virtuelle Azure Hello gère les interactions entre une machine virtuelle Azure et le contrôleur de structure Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="e2931-132">agent de machine virtuelle Hello est chargé de nombreux aspects fonctionnels de déploiement et la gestion des machines virtuelles Azure, y compris les extensions de machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e2931-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="e2931-133">l’agent de machine virtuelle Azure Hello est préinstallé sur les images Azure Marketplace et peut être installé manuellement sur les systèmes d’exploitation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e2931-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="e2931-134">Pour plus d’informations sur les systèmes d’exploitation pris en charge et sur la procédure d’installation, consultez l’article [Agent de machine virtuelle et extensions Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="e2931-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="e2931-135">Détecter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e2931-135">Discover VM extensions</span></span>

<span data-ttu-id="e2931-136">De nombreuses extensions de machine virtuelle différentes peuvent être utilisées avec les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="e2931-137">toosee une liste complète, exécutez hello suivant de commande avec hello CLI d’Azure, le remplacement d’emplacement d’exemple hello avec emplacement hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e2931-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="e2931-138">Exécuter les extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e2931-138">Run VM extensions</span></span>

<span data-ttu-id="e2931-139">Extensions de machine virtuelle Azure peuvent être exécutées sur des machines virtuelles existantes, qui sont utiles lorsque vous avez besoin de modifications de configuration toomake ou restaurer la connectivité sur une machine virtuelle déjà déployée.</span><span class="sxs-lookup"><span data-stu-id="e2931-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="e2931-140">Les extensions de machines virtuelles peuvent également être intégrées dans des déploiements de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2931-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="e2931-141">L’utilisation d’extensions avec des modèles Resource Manager permet de déployer et de configurer des machines virtuelles Azure sans avoir à intervenir après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="e2931-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="e2931-142">Hello méthodes suivantes peut être utilisée toorun une extension sur un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e2931-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="e2931-143">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-143">Azure CLI</span></span>

<span data-ttu-id="e2931-144">Extensions de machine virtuelle Azure peuvent être exécutées sur un ordinateur virtuel existant à l’aide de hello `az vm extension set` commande.</span><span class="sxs-lookup"><span data-stu-id="e2931-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="e2931-145">Cet exemple exécute une extension de script personnalisé hello contre un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e2931-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="e2931-146">Hello script produit la sortie similaire toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="e2931-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="e2931-147">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-147">Azure portal</span></span>

<span data-ttu-id="e2931-148">Extensions de machine virtuelle peuvent être appliqué tooan une machine virtuelle existante via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="e2931-149">toodo par conséquent, activez la machine virtuelle de hello, choisissez **Extensions**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e2931-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="e2931-150">Sélectionnez l’extension hello souhaité à partir de la liste de hello d’extensions disponibles et suivez les instructions hello dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="e2931-151">Hello image suivante montre installation hello Hello extension de Script personnalisé de Linux à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Installer l’extension de script personnalisé](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e2931-153">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2931-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="e2931-154">Extensions de machine virtuelle peuvent être ajoutée tooan Azure Resource Manager modèle et exécutée avec un déploiement hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="e2931-155">Lorsque vous déployez une extension avec un modèle, vous pouvez créer des déploiements Azure entièrement configurés.</span><span class="sxs-lookup"><span data-stu-id="e2931-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="e2931-156">Par exemple, hello que JSON suivant est tiré d’un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="e2931-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="e2931-157">modèle de Hello déploie un ensemble de l’équilibrage de la charge des machines virtuelles et d’une base de données SQL Azure et installe une application .NET Core sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e2931-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="e2931-158">prend en charge de l’installation du logiciel hello Hello extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e2931-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="e2931-159">Pour plus d’informations, consultez hello complète [modèle Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="e2931-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="e2931-160">Pour plus d’informations, consultez [Création de modèles Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="e2931-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="e2931-161">Sécuriser les données des extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e2931-161">Secure VM extension data</span></span>

<span data-ttu-id="e2931-162">Lorsque vous exécutez une extension de machine virtuelle, il peut être nécessaire de tooinclude des informations sensibles telles que les informations d’identification, les noms de compte de stockage et les clés d’accès de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e2931-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="e2931-163">Plusieurs extensions de machine virtuelle incluent une configuration protégée qui chiffre les données et la déchiffre uniquement à l’intérieur de la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="e2931-164">Chaque extension possède un schéma spécifique de configuration protégée, présenté en détail dans la documentation consacrée à l’extension.</span><span class="sxs-lookup"><span data-stu-id="e2931-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e2931-165">Bonjour à l’exemple suivant montre une instance de hello extension de Script personnalisé pour Linux.</span><span class="sxs-lookup"><span data-stu-id="e2931-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="e2931-166">Notez que tooexecute de commande hello comprend un ensemble d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e2931-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="e2931-167">Dans cet exemple, hello commande tooexecute n’est pas chiffrée.</span><span class="sxs-lookup"><span data-stu-id="e2931-167">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="e2931-168">Déplacement hello **commande tooexecute** propriété toohello **protégé** configuration sécurise la chaîne de l’exécution de hello.</span><span class="sxs-lookup"><span data-stu-id="e2931-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="e2931-169">Résoudre les problèmes liés aux extensions de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e2931-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="e2931-170">Chaque extension de machine virtuelle peut avoir l’extension de toohello spécifique d’étapes de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e2931-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="e2931-171">Par exemple, lorsque vous utilisez l’extension de Script personnalisé hello, détails de l’exécution de script sont accessibles localement sur l’ordinateur virtuel de hello sur lequel l’extension de hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="e2931-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="e2931-172">La procédure de résolution des problèmes spécifique d’une extension est présentée en détail dans la documentation de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="e2931-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e2931-173">Hello suivant les étapes de dépannage s’appliquent à des extensions de machine virtuelle tooall.</span><span class="sxs-lookup"><span data-stu-id="e2931-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="e2931-174">Afficher l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="e2931-174">View extension status</span></span>

<span data-ttu-id="e2931-175">Une fois une extension de machine virtuelle a été exécutée sur un ordinateur virtuel, utilisez hello suivant l’état de l’extension tooreturn commande CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="e2931-176">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e2931-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="e2931-177">sortie de Hello ressemble à hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="e2931-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="e2931-178">État d’exécution de l’extension peut également trouver dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="e2931-179">état de hello tooview d’extension, sélectionnez hello virtual machine, choisissez **Extensions**, et sélectionnez hello extension souhaitée.</span><span class="sxs-lookup"><span data-stu-id="e2931-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="e2931-180">Réexécuter une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e2931-180">Rerun a VM extension</span></span>

<span data-ttu-id="e2931-181">Il peut y avoir des cas dans lesquels une extension de machine virtuelle doit toobe exécuter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e2931-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="e2931-182">Vous pouvez réexécuter une extension en le supprimant, puis en réexécutant les extension hello avec une méthode d’exécution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e2931-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="e2931-183">tooremove une extension, exécutez hello suivant de commande avec hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e2931-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="e2931-184">Remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e2931-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="e2931-185">Vous pouvez supprimer une extension à l’aide de hello Bonjour portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2931-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="e2931-186">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e2931-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="e2931-187">Choisissez **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="e2931-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="e2931-188">Sélectionnez l’extension hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="e2931-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="e2931-189">Choisissez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="e2931-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="e2931-190">Informations de référence sur les extensions de machine virtuelle courantes</span><span class="sxs-lookup"><span data-stu-id="e2931-190">Common VM extension reference</span></span>
| <span data-ttu-id="e2931-191">Nom de l’extension</span><span class="sxs-lookup"><span data-stu-id="e2931-191">Extension name</span></span> | <span data-ttu-id="e2931-192">Description</span><span class="sxs-lookup"><span data-stu-id="e2931-192">Description</span></span> | <span data-ttu-id="e2931-193">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="e2931-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2931-194">Extension de script personnalisé pour Linux</span><span class="sxs-lookup"><span data-stu-id="e2931-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="e2931-195">Exécuter des scripts sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="e2931-196">Extension de script personnalisé pour Linux</span><span class="sxs-lookup"><span data-stu-id="e2931-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e2931-197">Extension Docker</span><span class="sxs-lookup"><span data-stu-id="e2931-197">Docker extension</span></span> |<span data-ttu-id="e2931-198">Installez hello Docker démon toosupport à distance les commandes Docker.</span><span class="sxs-lookup"><span data-stu-id="e2931-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="e2931-199">Extension de machine virtuelle Docker</span><span class="sxs-lookup"><span data-stu-id="e2931-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="e2931-200">Extension d’accès aux machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e2931-200">VM Access extension</span></span> |<span data-ttu-id="e2931-201">Récupérer l’accès tooan machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="e2931-202">Extension d’accès aux machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e2931-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="e2931-203">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="e2931-204">Gérer les diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="e2931-205">Extension Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="e2931-206">Extension d’accès aux machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e2931-206">Azure VM Access extension</span></span> |<span data-ttu-id="e2931-207">Gérer les utilisateurs et les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="e2931-207">Manage users and credentials</span></span> |[<span data-ttu-id="e2931-208">Extension d’accès aux machines virtuelles pour Linux</span><span class="sxs-lookup"><span data-stu-id="e2931-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
