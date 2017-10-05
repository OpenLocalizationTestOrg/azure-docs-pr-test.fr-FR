---
title: "Création de modèles avec des extensions de machine virtuelle Linux | Microsoft Docs"
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
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="fb413-103">Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="fb413-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="fb413-104">Dans l’interface de ligne de commande Azure, exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fb413-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="fb413-105">Cette commande renvoie le nom de l’éditeur, le nom de l’extension et la version, comme suit :</span><span class="sxs-lookup"><span data-stu-id="fb413-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="fb413-106">Ces trois propriétés sont mappées respectivement à « publisher », « type » et « typeHandlerVersion » dans l’extrait du modèle ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fb413-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="fb413-107">Il est toujours recommandé d’utiliser la dernière version de l’extension pour obtenir les fonctionnalités les plus à jour.</span><span class="sxs-lookup"><span data-stu-id="fb413-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="fb413-108">Identification du schéma pour les paramètres de configuration de l’extension</span><span class="sxs-lookup"><span data-stu-id="fb413-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="fb413-109">L’étape suivante de la création du modèle d’extension consiste à identifier le format pour fournir les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="fb413-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="fb413-110">Chaque extension prend en charge son propre ensemble de paramètres.</span><span class="sxs-lookup"><span data-stu-id="fb413-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="fb413-111">Pour voir un exemple de configuration pour les extensions Linux, consultez les [exemples d’extensions Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb413-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fb413-112">Reportez-vous à ce qui suit pour obtenir un modèle totalement terminé avec des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb413-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="fb413-113">Extension de script personnalisé sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="fb413-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="fb413-114">Une fois le modèle créé, vous pouvez le déployer en utilisant l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="fb413-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

