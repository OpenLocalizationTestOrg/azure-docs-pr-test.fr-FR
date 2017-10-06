---
title: "aaaRun des scripts personnalisés sur les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Automatiser les tâches de configuration Linux VM à l’aide de hello Extension de Script personnalisé"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="29497-103">À l’aide de hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="29497-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="29497-104">Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="29497-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="29497-105">Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="29497-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="29497-106">Scripts pouvant être téléchargés à partir de stockage Azure ou un autre emplacement internet accessible, ou extension toohello moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="29497-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="29497-107">Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="29497-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="29497-108">Ce document décrit en détail comment toouse hello Extension de Script personnalisé à partir de hello CLI d’Azure et un modèle Azure Resource Manager et informations de dépannage sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="29497-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="29497-109">Configuration de l’extension</span><span class="sxs-lookup"><span data-stu-id="29497-109">Extension Configuration</span></span>
<span data-ttu-id="29497-110">configuration d’Extension de Script personnalisé Hello spécifie des éléments tels que l’emplacement du script et toobe de commande hello exécuter.</span><span class="sxs-lookup"><span data-stu-id="29497-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="29497-111">Cette configuration peut être stockée dans les fichiers de configuration spécifiées sur la ligne de commande hello, ou dans un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29497-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="29497-112">Les données sensibles peuvent être stockées dans une configuration protégée, qui est chiffrée et déchiffrée uniquement à l’intérieur de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="29497-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="29497-113">la configuration protégée Hello est utile lors de la commande d’exécution hello inclut des secrets comme un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="29497-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="29497-114">Configuration publique</span><span class="sxs-lookup"><span data-stu-id="29497-114">Public Configuration</span></span>
<span data-ttu-id="29497-115">Schéma :</span><span class="sxs-lookup"><span data-stu-id="29497-115">Schema:</span></span>

<span data-ttu-id="29497-116">**Remarque** : ces noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="29497-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="29497-117">Utiliser des noms de hello comme indiqué ci-dessous tooavoid les problèmes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="29497-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="29497-118">**commandToExecute**: (obligatoire, string) hello tooexecute de script de point d’entrée</span><span class="sxs-lookup"><span data-stu-id="29497-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="29497-119">**fileUris**: téléchargé des URL hello pour les fichiers toobe (facultatif, tableau de chaînes).</span><span class="sxs-lookup"><span data-stu-id="29497-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="29497-120">**horodatage** (entier facultatif) Utilisez cette tootrigger uniquement de champ la ré-exécution du script de hello en modifiant la valeur de ce champ.</span><span class="sxs-lookup"><span data-stu-id="29497-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="29497-121">Configuration protégée</span><span class="sxs-lookup"><span data-stu-id="29497-121">Protected Configuration</span></span>
<span data-ttu-id="29497-122">Schéma :</span><span class="sxs-lookup"><span data-stu-id="29497-122">Schema:</span></span>

<span data-ttu-id="29497-123">**Remarque** : ces noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="29497-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="29497-124">Utiliser des noms de hello comme indiqué ci-dessous tooavoid les problèmes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="29497-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="29497-125">**commandToExecute**: (facultatif, string) hello tooexecute de script de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="29497-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="29497-126">Utilisez plutôt ce champ si votre commande contient des secrets tels que des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="29497-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="29497-127">**storageAccountName**: (facultatif, string) nom hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29497-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="29497-128">Si vous spécifiez des informations d’identification de stockage, tous les fileUris doivent être des URL pour les objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="29497-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="29497-129">**storageAccountKey**: (facultatif, string) clé d’accès hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="29497-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="29497-130">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="29497-130">Azure CLI</span></span>
<span data-ttu-id="29497-131">Lorsque vous utilisez toorun hello Extension de Script personnalisé de hello CLI d’Azure, créez un fichier de configuration ou des fichiers contenant les uri de fichier minimale hello et commande d’exécution de script hello.</span><span class="sxs-lookup"><span data-stu-id="29497-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="29497-132">Vous pouvez également les paramètres de hello peuvent être spécifiés dans la commande hello sous forme de chaîne au format JSON.</span><span class="sxs-lookup"><span data-stu-id="29497-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="29497-133">Cela permet de hello toobe de configuration spécifié lors de l’exécution et sans fichier de configuration distincts.</span><span class="sxs-lookup"><span data-stu-id="29497-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="29497-134">Exemples d’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="29497-134">Azure CLI Examples</span></span>

<span data-ttu-id="29497-135">**Exemple 1** : configuration publique avec fichier de script.</span><span class="sxs-lookup"><span data-stu-id="29497-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="29497-136">Commande d’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="29497-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="29497-137">**Exemple 2** : configuration publique sans fichier de script.</span><span class="sxs-lookup"><span data-stu-id="29497-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="29497-138">Commande d’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="29497-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="29497-139">**Exemple 3** : un fichier de configuration publique est l’URI de fichier de script utilisé toospecify hello et un fichier de configuration protégée est utilisé toospecify hello commande toobe exécutée.</span><span class="sxs-lookup"><span data-stu-id="29497-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="29497-140">Fichier de configuration publique :</span><span class="sxs-lookup"><span data-stu-id="29497-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="29497-141">Fichier de configuration protégée :</span><span class="sxs-lookup"><span data-stu-id="29497-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="29497-142">Commande d’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="29497-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="29497-143">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29497-143">Resource Manager Template</span></span>
<span data-ttu-id="29497-144">Bonjour Azure Extension de Script personnalisé peut être exécuté au moment du déploiement Machine virtuelle à l’aide d’un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="29497-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="29497-145">toodo ajouter, modèle de déploiement toohello JSON au format correct.</span><span class="sxs-lookup"><span data-stu-id="29497-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="29497-146">Exemples Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29497-146">Resource Manager Examples</span></span>
<span data-ttu-id="29497-147">**Exemple 1** : configuration publique.</span><span class="sxs-lookup"><span data-stu-id="29497-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="29497-148">**Exemple 2** : commande d’exécution dans une configuration protégée.</span><span class="sxs-lookup"><span data-stu-id="29497-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="29497-149">Consultez le magasin de musique hello .net Core démonstration pour obtenir un exemple complet - [démonstration de magasin de musique](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="29497-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="29497-150">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="29497-150">Troubleshooting</span></span>
<span data-ttu-id="29497-151">Lorsque hello Extension de Script personnalisé est exécuté, hello est créé ou téléchargé dans un toohello similaire Active l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="29497-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="29497-152">sortie de la commande Hello est également enregistrée dans ce répertoire dans `stdout` et `stderr` fichier.</span><span class="sxs-lookup"><span data-stu-id="29497-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="29497-153">Hello, Extension de Script Azure génère un journal, qui se trouve ici.</span><span class="sxs-lookup"><span data-stu-id="29497-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="29497-154">l’état d’exécution Hello Hello Extension de Script personnalisé peut également être récupéré avec hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="29497-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="29497-155">sortie de Hello ressemble à hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="29497-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="29497-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29497-156">Next Steps</span></span>
<span data-ttu-id="29497-157">Pour plus d’informations sur les autres extensions de script de machine virtuelle, consultez [Vue d’ensemble de l’extension de script Azure pour Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29497-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

