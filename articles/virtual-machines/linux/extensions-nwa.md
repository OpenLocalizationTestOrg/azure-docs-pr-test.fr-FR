---
title: "aaaAzure extension de machine virtuelle de l’Agent de l’Observateur réseau pour Linux | Documents Microsoft"
description: "Déployer hello Agent de l’Observateur réseau sur une machine virtuelle Linux à l’aide d’une extension de machine virtuelle."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="ec0f5-103">Extension de machine virtuelle Agent Network Watcher pour Linux</span><span class="sxs-lookup"><span data-stu-id="ec0f5-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="ec0f5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ec0f5-104">Overview</span></span>

<span data-ttu-id="ec0f5-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) est un service d’analyse, de diagnostic et d’analytique des performances réseau permettant de surveiller les réseaux Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="ec0f5-106">Hello, extension de machine virtuelle de l’Agent de l’Observateur réseau est obligatoire pour certaines des fonctionnalités de l’Observateur réseau hello sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="ec0f5-107">notamment la capture du trafic réseau à la demande et d’autres fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="ec0f5-108">Cette hello de détails de document pris en charge les options de déploiement et les plateformes pour hello extension de machine virtuelle de l’Agent de l’Observateur réseau pour Linux.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec0f5-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ec0f5-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="ec0f5-110">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ec0f5-110">Operating system</span></span>

<span data-ttu-id="ec0f5-111">Hello, extension de l’Agent de l’Observateur réseau peut être exécutée sur ces distributions de Linux :</span><span class="sxs-lookup"><span data-stu-id="ec0f5-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="ec0f5-112">Distribution</span><span class="sxs-lookup"><span data-stu-id="ec0f5-112">Distribution</span></span> | <span data-ttu-id="ec0f5-113">Version</span><span class="sxs-lookup"><span data-stu-id="ec0f5-113">Version</span></span> |
|---|---|
| <span data-ttu-id="ec0f5-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ec0f5-114">Ubuntu</span></span> | <span data-ttu-id="ec0f5-115">16.04 LTS, 14.04 LTS et 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ec0f5-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="ec0f5-116">Debian</span><span class="sxs-lookup"><span data-stu-id="ec0f5-116">Debian</span></span> | <span data-ttu-id="ec0f5-117">7 et 8</span><span class="sxs-lookup"><span data-stu-id="ec0f5-117">7 and 8</span></span> |
| <span data-ttu-id="ec0f5-118">Red Hat</span><span class="sxs-lookup"><span data-stu-id="ec0f5-118">RedHat</span></span> | <span data-ttu-id="ec0f5-119">6.x et 7.x</span><span class="sxs-lookup"><span data-stu-id="ec0f5-119">6.x and 7.x</span></span> |
| <span data-ttu-id="ec0f5-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="ec0f5-120">Oracle Linux</span></span> | <span data-ttu-id="ec0f5-121">7x</span><span class="sxs-lookup"><span data-stu-id="ec0f5-121">7x</span></span> |
| <span data-ttu-id="ec0f5-122">SUSE</span><span class="sxs-lookup"><span data-stu-id="ec0f5-122">Suse</span></span> | <span data-ttu-id="ec0f5-123">11 et 12</span><span class="sxs-lookup"><span data-stu-id="ec0f5-123">11 and 12</span></span> |
| <span data-ttu-id="ec0f5-124">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ec0f5-124">OpenSuse</span></span> | <span data-ttu-id="ec0f5-125">7.0</span><span class="sxs-lookup"><span data-stu-id="ec0f5-125">7.0</span></span> |
| <span data-ttu-id="ec0f5-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="ec0f5-126">CentOS</span></span> | <span data-ttu-id="ec0f5-127">7.0</span><span class="sxs-lookup"><span data-stu-id="ec0f5-127">7.0</span></span> |

<span data-ttu-id="ec0f5-128">Remarque : CoreOS n’est pas pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="ec0f5-129">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="ec0f5-129">Internet connectivity</span></span>

<span data-ttu-id="ec0f5-130">Certaines des hello fonctionnalités de l’Agent de l’Observateur réseau exige que l’ordinateur virtuel cible hello toohello connecté Internet.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="ec0f5-131">Sans les connexions sortantes hello capacité tooestablish certaines des fonctionnalités de l’Agent de l’Observateur réseau hello peuvent fonctionner correctement ou deviennent indisponibles.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="ec0f5-132">Pour plus d’informations, consultez hello [documentation de l’Observateur réseau](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="ec0f5-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="ec0f5-133">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="ec0f5-133">Extension schema</span></span>

<span data-ttu-id="ec0f5-134">Hello JSON suivant montre schéma hello pour hello extension de l’Agent de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="ec0f5-135">extension de Hello ni requiert ni prend en charge tous les paramètres fournis par l’utilisateur pour l’instant et s’appuie sur sa configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="ec0f5-136">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="ec0f5-136">Property values</span></span>

| <span data-ttu-id="ec0f5-137">Nom</span><span class="sxs-lookup"><span data-stu-id="ec0f5-137">Name</span></span> | <span data-ttu-id="ec0f5-138">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="ec0f5-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="ec0f5-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ec0f5-139">apiVersion</span></span> | <span data-ttu-id="ec0f5-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="ec0f5-140">2015-06-15</span></span> |
| <span data-ttu-id="ec0f5-141">publisher</span><span class="sxs-lookup"><span data-stu-id="ec0f5-141">publisher</span></span> | <span data-ttu-id="ec0f5-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="ec0f5-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="ec0f5-143">type</span><span class="sxs-lookup"><span data-stu-id="ec0f5-143">type</span></span> | <span data-ttu-id="ec0f5-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="ec0f5-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="ec0f5-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ec0f5-145">typeHandlerVersion</span></span> | <span data-ttu-id="ec0f5-146">1.4</span><span class="sxs-lookup"><span data-stu-id="ec0f5-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="ec0f5-147">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="ec0f5-147">Template deployment</span></span>

<span data-ttu-id="ec0f5-148">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="ec0f5-149">schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension de l’Agent de l’Observateur réseau pendant un déploiement de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="ec0f5-150">Déploiement de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ec0f5-150">Azure CLI deployment</span></span>

<span data-ttu-id="ec0f5-151">Hello CLI d’Azure peut être utilisé toodeploy hello réseau Observateur l’Agent VM extension tooan existant machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="ec0f5-152">Résolution des problèmes et support</span><span class="sxs-lookup"><span data-stu-id="ec0f5-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="ec0f5-153">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ec0f5-153">Troubleshooting</span></span>

<span data-ttu-id="ec0f5-154">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="ec0f5-155">état du déploiement hello toosee des extensions pour une machine virtuelle donnée, exécutez hello suivant à l’aide de la commande hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="ec0f5-156">Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :</span><span class="sxs-lookup"><span data-stu-id="ec0f5-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="ec0f5-157">Support</span><span class="sxs-lookup"><span data-stu-id="ec0f5-157">Support</span></span>

<span data-ttu-id="ec0f5-158">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez consultez la documentation de l’Observateur réseau toohello ou contactez hello Azure experts de hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ec0f5-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="ec0f5-159">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ec0f5-160">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="ec0f5-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="ec0f5-161">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="ec0f5-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
