---
title: aaaOMS extension de machine virtuelle Azure pour Linux | Documents Microsoft
description: "Déployer l’agent OMS de hello sur une machine virtuelle Linux à l’aide d’une extension de machine virtuelle."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="ace92-103">Extension de machine virtuelle OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="ace92-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="ace92-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ace92-104">Overview</span></span>

<span data-ttu-id="ace92-105">Operations Management Suite (OMS) fournit des fonctionnalités de surveillance, d’alerte et de correction des alertes sur le ressources cloud et locales.</span><span class="sxs-lookup"><span data-stu-id="ace92-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="ace92-106">Hello, extension de machine virtuelle de l’Agent OMS pour Linux est publié et pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ace92-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="ace92-107">extension de Hello installe l’agent OMS de hello sur des machines virtuelles et inscrit les machines virtuelles dans un espace de travail OMS existant.</span><span class="sxs-lookup"><span data-stu-id="ace92-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="ace92-108">Cette hello de détails du document prennent en charge les plateformes, les configurations et les options de déploiement pour hello extension de machine virtuelle OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="ace92-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ace92-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ace92-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="ace92-110">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ace92-110">Operating system</span></span>

<span data-ttu-id="ace92-111">Hello extension OMS Agent peut être exécutée sur ces distributions de Linux.</span><span class="sxs-lookup"><span data-stu-id="ace92-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="ace92-112">Distribution</span><span class="sxs-lookup"><span data-stu-id="ace92-112">Distribution</span></span> | <span data-ttu-id="ace92-113">Version</span><span class="sxs-lookup"><span data-stu-id="ace92-113">Version</span></span> |
|---|---|
| <span data-ttu-id="ace92-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="ace92-114">CentOS Linux</span></span> | <span data-ttu-id="ace92-115">5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="ace92-115">5, 6, and 7</span></span> |
| <span data-ttu-id="ace92-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="ace92-116">Oracle Linux</span></span> | <span data-ttu-id="ace92-117">5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="ace92-117">5, 6, and 7</span></span> |
| <span data-ttu-id="ace92-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="ace92-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="ace92-119">5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="ace92-119">5, 6 and 7</span></span> |
| <span data-ttu-id="ace92-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="ace92-120">Debian GNU/Linux</span></span> | <span data-ttu-id="ace92-121">6, 7 et 8</span><span class="sxs-lookup"><span data-stu-id="ace92-121">6, 7, and 8</span></span> |
| <span data-ttu-id="ace92-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ace92-122">Ubuntu</span></span> | <span data-ttu-id="ace92-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ace92-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="ace92-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="ace92-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="ace92-125">11 et 12</span><span class="sxs-lookup"><span data-stu-id="ace92-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="ace92-126">Connectivité Internet</span><span class="sxs-lookup"><span data-stu-id="ace92-126">Internet connectivity</span></span>

<span data-ttu-id="ace92-127">Hello, extension de l’Agent OMS pour Linux nécessite que l’ordinateur virtuel cible hello est connecté toohello internet.</span><span class="sxs-lookup"><span data-stu-id="ace92-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="ace92-128">Schéma d’extensions</span><span class="sxs-lookup"><span data-stu-id="ace92-128">Extension schema</span></span>

<span data-ttu-id="ace92-129">Hello JSON suivant montre schéma hello pour hello extension OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="ace92-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="ace92-130">extension de Hello requiert hello espace de travail et ID de clé à partir de l’espace de travail OMS de cible hello. Vous trouverez ces valeurs dans le portail OMS est hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="ace92-131">Étant donné que la clé d’espace de travail hello doit être traité comme des données sensibles, il doit être stocké dans une configuration protégée.</span><span class="sxs-lookup"><span data-stu-id="ace92-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="ace92-132">Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="ace92-133">Notez que **workspaceId** et **workspaceKey** respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="ace92-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="ace92-134">Valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="ace92-134">Property values</span></span>

| <span data-ttu-id="ace92-135">Nom</span><span class="sxs-lookup"><span data-stu-id="ace92-135">Name</span></span> | <span data-ttu-id="ace92-136">Valeur/Exemple</span><span class="sxs-lookup"><span data-stu-id="ace92-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="ace92-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ace92-137">apiVersion</span></span> | <span data-ttu-id="ace92-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="ace92-138">2015-06-15</span></span> |
| <span data-ttu-id="ace92-139">publisher</span><span class="sxs-lookup"><span data-stu-id="ace92-139">publisher</span></span> | <span data-ttu-id="ace92-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="ace92-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="ace92-141">type</span><span class="sxs-lookup"><span data-stu-id="ace92-141">type</span></span> | <span data-ttu-id="ace92-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="ace92-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="ace92-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="ace92-143">typeHandlerVersion</span></span> | <span data-ttu-id="ace92-144">1.4</span><span class="sxs-lookup"><span data-stu-id="ace92-144">1.4</span></span> |
| <span data-ttu-id="ace92-145">workspaceId (par exemple)</span><span class="sxs-lookup"><span data-stu-id="ace92-145">workspaceId (e.g)</span></span> | <span data-ttu-id="ace92-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="ace92-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="ace92-147">workspaceKey (par exemple)</span><span class="sxs-lookup"><span data-stu-id="ace92-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="ace92-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="ace92-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="ace92-149">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="ace92-149">Template deployment</span></span>

<span data-ttu-id="ace92-150">Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ace92-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="ace92-151">Les modèles sont idéaux lors du déploiement d’un ou plusieurs ordinateurs virtuels qui nécessitent le déploiement après la configuration tels que l’intégration tooOMS.</span><span class="sxs-lookup"><span data-stu-id="ace92-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="ace92-152">Vous trouverez un exemple de modèle de gestionnaire de ressources qui inclut l’extension de machine virtuelle de l’Agent OMS hello sur hello [galerie de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="ace92-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="ace92-153">configuration de JSON Hello pour une extension de machine virtuelle peut être imbriquée dans une ressource d’ordinateur virtuel hello ou placée au niveau racine de hello ou un niveau supérieur d’un modèle de gestionnaire de ressources JSON.</span><span class="sxs-lookup"><span data-stu-id="ace92-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="ace92-154">la sélection élective Hello de configuration JSON de hello affecte la valeur hello du nom de la ressource hello et type.</span><span class="sxs-lookup"><span data-stu-id="ace92-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="ace92-155">Pour plus d’informations, consultez [Définition du nom et du type des ressources enfants](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ace92-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="ace92-156">Hello suppose extension d’OMS hello est imbriquée dans la ressource d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="ace92-157">Lors de l’imbrication des ressources d’extension de hello, hello JSON est placée dans hello `"resources": []` objet de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="ace92-158">Lorsque vous placez l’extension hello JSON au niveau racine hello du modèle de hello, nom de la ressource hello inclut un ordinateur virtuel de référence toohello parent, et type de hello reflète configuration imbriqués de hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="ace92-159">Déploiement de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ace92-159">Azure CLI deployment</span></span>

<span data-ttu-id="ace92-160">Hello CLI d’Azure peut être utilisé toodeploy hello OMS Agent VM extension tooan existant machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ace92-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="ace92-161">Remplacez la clé d’OMS hello et ID d’OMS avec ceux de votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="ace92-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="ace92-162">Dépannage et support technique</span><span class="sxs-lookup"><span data-stu-id="ace92-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="ace92-163">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ace92-163">Troubleshoot</span></span>

<span data-ttu-id="ace92-164">Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ace92-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="ace92-165">état du déploiement hello toosee des extensions pour une machine virtuelle donnée, exécutez hello suivant à l’aide de la commande hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ace92-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="ace92-166">Exécution de l’extension de sortie est journalisée toohello le fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="ace92-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="ace92-167">Codes d’erreur et signification</span><span class="sxs-lookup"><span data-stu-id="ace92-167">Error codes and their meanings</span></span>

| <span data-ttu-id="ace92-168">Code d'erreur</span><span class="sxs-lookup"><span data-stu-id="ace92-168">Error Code</span></span> | <span data-ttu-id="ace92-169">Signification</span><span class="sxs-lookup"><span data-stu-id="ace92-169">Meaning</span></span> | <span data-ttu-id="ace92-170">Action possible</span><span class="sxs-lookup"><span data-stu-id="ace92-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="ace92-171">10</span><span class="sxs-lookup"><span data-stu-id="ace92-171">10</span></span> | <span data-ttu-id="ace92-172">Machine virtuelle est déjà connecté tooan espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="ace92-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="ace92-173">tooconnect hello VM toohello espace de travail spécifiée dans le schéma d’extension hello, définir stopOnMultipleConnections toofalse dans les paramètres publics ou supprimez cette propriété.</span><span class="sxs-lookup"><span data-stu-id="ace92-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="ace92-174">Cette machine virtuelle est facturée une fois pour chaque espace de travail auquel elle est connectée.</span><span class="sxs-lookup"><span data-stu-id="ace92-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="ace92-175">11</span><span class="sxs-lookup"><span data-stu-id="ace92-175">11</span></span> | <span data-ttu-id="ace92-176">Configuration non valide fournie toohello extension</span><span class="sxs-lookup"><span data-stu-id="ace92-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="ace92-177">Suivez hello précédents exemples tooset toutes les valeurs de propriété pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="ace92-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="ace92-178">12</span><span class="sxs-lookup"><span data-stu-id="ace92-178">12</span></span> | <span data-ttu-id="ace92-179">Gestionnaire de package de dpkg Hello est verrouillé.</span><span class="sxs-lookup"><span data-stu-id="ace92-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="ace92-180">Assurez-vous que toutes les opérations de mise à jour dpkg sur l’ordinateur de hello terminés, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="ace92-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="ace92-181">20</span><span class="sxs-lookup"><span data-stu-id="ace92-181">20</span></span> | <span data-ttu-id="ace92-182">Activation appelée prématurément</span><span class="sxs-lookup"><span data-stu-id="ace92-182">Enable called prematurely</span></span> | <span data-ttu-id="ace92-183">[Hello de mise à jour le Linux Agent Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="ace92-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="ace92-184">51</span><span class="sxs-lookup"><span data-stu-id="ace92-184">51</span></span> | <span data-ttu-id="ace92-185">Cette extension n’est pas pris en charge sur le système d’exploitation de la machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="ace92-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="ace92-186">55</span><span class="sxs-lookup"><span data-stu-id="ace92-186">55</span></span> | <span data-ttu-id="ace92-187">Impossible de connecter le service de Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="ace92-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="ace92-188">Vérifiez que hello système dispose d’un accès à Internet ou qu’un proxy HTTP valide a été fourni.</span><span class="sxs-lookup"><span data-stu-id="ace92-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="ace92-189">En outre, vérifier exactitude hello d’ID d’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="ace92-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="ace92-190">Vous trouverez des informations de dépannage supplémentaires sur hello [Guide de dépannage de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="ace92-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="ace92-191">Support</span><span class="sxs-lookup"><span data-stu-id="ace92-191">Support</span></span>

<span data-ttu-id="ace92-192">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ace92-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="ace92-193">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="ace92-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="ace92-194">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get.</span><span class="sxs-lookup"><span data-stu-id="ace92-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="ace92-195">Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="ace92-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
