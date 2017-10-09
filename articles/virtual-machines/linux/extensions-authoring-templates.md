---
title: "modèles d’aaaAuthoring avec les extensions de Linux VM | Documents Microsoft"
description: "En savoir plus sur la création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="dc1df-103">Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="dc1df-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="dc1df-104">À partir de l’interface CLI d’Azure, exécutez hello suivant de commande :</span><span class="sxs-lookup"><span data-stu-id="dc1df-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="dc1df-105">Cette commande retourne hello, nom de serveur de publication, le nom de l’extension et la version comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc1df-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="dc1df-106">Ces trois propriétés mappent trop « éditeur », « type » et « typeHandlerVersion » respectivement dans hello ci-dessus extrait de modèle.</span><span class="sxs-lookup"><span data-stu-id="dc1df-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="dc1df-107">Il est toujours recommandée toouse hello dernière extension version tooget hello plus mis à jour des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="dc1df-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="dc1df-108">Identification de schéma hello pour les paramètres de configuration d’extension hello</span><span class="sxs-lookup"><span data-stu-id="dc1df-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="dc1df-109">étape suivante de Hello par la création d’un modèle d’extension est format de hello tooidentify pour fournir des paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc1df-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="dc1df-110">Chaque extension prend en charge son propre ensemble de paramètres.</span><span class="sxs-lookup"><span data-stu-id="dc1df-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="dc1df-111">toolook à des exemples de configurations pour les extensions de Linux, cliquez sur documentation hello pour voir [Linux eExtensions exemples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc1df-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dc1df-112">Reportez-vous toohello suivant tooget un modèle entièrement terminé avec des Extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dc1df-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="dc1df-113">Extension de script personnalisé sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="dc1df-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="dc1df-114">Après la création de modèle de hello, vous pouvez déployer à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="dc1df-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

