---
title: "aaaAuthoring modèles avec des extensions de machine virtuelle Windows | Documents Microsoft"
description: "En savoir plus sur la création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="5aa1c-103">Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="5aa1c-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="5aa1c-104">À partir de Azure PowerShell, exécutez hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="5aa1c-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="5aa1c-105">Cette applet de commande retourne la version, nom d’extension et nom de l’éditeur hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5aa1c-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="5aa1c-106">Ces trois propriétés mappent trop « éditeur », « type » et « typeHandlerVersion » respectivement dans hello ci-dessus extrait de modèle.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa1c-107">Il est toujours recommandée toouse hello dernière extension version tooget hello plus mis à jour des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="5aa1c-108">Identification de schéma hello pour les paramètres de configuration d’extension hello</span><span class="sxs-lookup"><span data-stu-id="5aa1c-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="5aa1c-109">étape suivante de Hello par la création d’un modèle d’extension est format de hello tooidentify pour fournir des paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="5aa1c-110">Chaque extension prend en charge son propre ensemble de paramètres.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="5aa1c-111">toolook à des exemples de configurations pour les extensions Windows, consultez [exemples d’extensions Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5aa1c-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5aa1c-112">Reportez-vous toohello suivant tooget un modèle entièrement terminé avec des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="5aa1c-113">Extension de script personnalisé sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="5aa1c-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="5aa1c-114">Après la création de modèle de hello, vous pouvez déployer à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5aa1c-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

