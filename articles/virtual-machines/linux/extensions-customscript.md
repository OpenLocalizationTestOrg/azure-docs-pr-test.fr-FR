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
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>À l’aide de hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux
Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles. Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion. Scripts pouvant être téléchargés à partir de stockage Azure ou un autre emplacement internet accessible, ou extension toohello moment de l’exécution. Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.

Ce document décrit en détail comment toouse hello Extension de Script personnalisé à partir de hello CLI d’Azure et un modèle Azure Resource Manager et informations de dépannage sur les systèmes Linux.

## <a name="extension-configuration"></a>Configuration de l’extension
configuration d’Extension de Script personnalisé Hello spécifie des éléments tels que l’emplacement du script et toobe de commande hello exécuter. Cette configuration peut être stockée dans les fichiers de configuration spécifiées sur la ligne de commande hello, ou dans un modèle Azure Resource Manager. Les données sensibles peuvent être stockées dans une configuration protégée, qui est chiffrée et déchiffrée uniquement à l’intérieur de machine virtuelle de hello. la configuration protégée Hello est utile lors de la commande d’exécution hello inclut des secrets comme un mot de passe.

### <a name="public-configuration"></a>Configuration publique
Schéma :

**Remarque** : ces noms de propriété respectent la casse. Utiliser des noms de hello comme indiqué ci-dessous tooavoid les problèmes de déploiement.

* **commandToExecute**: (obligatoire, string) hello tooexecute de script de point d’entrée
* **fileUris**: téléchargé des URL hello pour les fichiers toobe (facultatif, tableau de chaînes).
* **horodatage** (entier facultatif) Utilisez cette tootrigger uniquement de champ la ré-exécution du script de hello en modifiant la valeur de ce champ.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Configuration protégée
Schéma :

**Remarque** : ces noms de propriété respectent la casse. Utiliser des noms de hello comme indiqué ci-dessous tooavoid les problèmes de déploiement.

* **commandToExecute**: (facultatif, string) hello tooexecute de script de point d’entrée. Utilisez plutôt ce champ si votre commande contient des secrets tels que des mots de passe.
* **storageAccountName**: (facultatif, string) nom hello du compte de stockage. Si vous spécifiez des informations d’identification de stockage, tous les fileUris doivent être des URL pour les objets blob Azure.
* **storageAccountKey**: (facultatif, string) clé d’accès hello du compte de stockage.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Interface de ligne de commande Azure
Lorsque vous utilisez toorun hello Extension de Script personnalisé de hello CLI d’Azure, créez un fichier de configuration ou des fichiers contenant les uri de fichier minimale hello et commande d’exécution de script hello.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Vous pouvez également les paramètres de hello peuvent être spécifiés dans la commande hello sous forme de chaîne au format JSON. Cela permet de hello toobe de configuration spécifié lors de l’exécution et sans fichier de configuration distincts.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Exemples d’interface de ligne de commande Azure

**Exemple 1** : configuration publique avec fichier de script.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Commande d’interface de ligne de commande Azure :

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Exemple 2** : configuration publique sans fichier de script.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Commande d’interface de ligne de commande Azure :

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Exemple 3** : un fichier de configuration publique est l’URI de fichier de script utilisé toospecify hello et un fichier de configuration protégée est utilisé toospecify hello commande toobe exécutée.

Fichier de configuration publique :

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Fichier de configuration protégée :  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Commande d’interface de ligne de commande Azure :

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Modèle Resource Manager
Bonjour Azure Extension de Script personnalisé peut être exécuté au moment du déploiement Machine virtuelle à l’aide d’un modèle de gestionnaire de ressources. toodo ajouter, modèle de déploiement toohello JSON au format correct.

### <a name="resource-manager-examples"></a>Exemples Resource Manager
**Exemple 1** : configuration publique.

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

**Exemple 2** : commande d’exécution dans une configuration protégée.

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

Consultez le magasin de musique hello .net Core démonstration pour obtenir un exemple complet - [démonstration de magasin de musique](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Résolution des problèmes
Lorsque hello Extension de Script personnalisé est exécuté, hello est créé ou téléchargé dans un toohello similaire Active l’exemple suivant. sortie de la commande Hello est également enregistrée dans ce répertoire dans `stdout` et `stderr` fichier.

```bash
/var/lib/waagent/custom-script/download/0/
```

Hello, Extension de Script Azure génère un journal, qui se trouve ici.

```bash
/var/log/azure/custom-script/handler.log
```

l’état d’exécution Hello Hello Extension de Script personnalisé peut également être récupéré avec hello CLI d’Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

sortie de Hello ressemble à hello suivant du texte :

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les autres extensions de script de machine virtuelle, consultez [Vue d’ensemble de l’extension de script Azure pour Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

