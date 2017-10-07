---
title: "aaaAzure démarrage rapide : créer une CLI de machine virtuelle Windows | Documents Microsoft"
description: "En savoir plus rapidement toocreate des machines virtuelles Windows avec hello CLI d’Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Créer une machine virtuelle Windows avec hello CLI d’Azure

Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle exécutant Windows Server 2016. Une fois le déploiement terminé, nous connecter toohello serveur et installez IIS.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). 

Hello exemple suivant crée un ordinateur virtuel nommé *myVM*. Cet exemple utilise *azureuser* pour un nom d’utilisateur administratif et *myPassword12* comme mot de passe hello. Mettre à jour ces environnement tooyour approprié de toosomething valeurs. Ces valeurs sont nécessaires lors de la création d’une connexion avec l’ordinateur virtuel de hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant. Prenez note de hello `publicIpAaddress`. Cette adresse est utilisée tooaccess hello machine virtuelle.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Ouvrez le port 80 pour le trafic web 

Par défaut, seules les connexions RDP sont autorisées sur des machines virtuelles tooWindows déployés dans Azure. Si cet ordinateur virtuel est toobe un serveur Web, vous devez tooopen port 80 de hello Internet. Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Connecter toovirtual machine

La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello. Remplacer l’adresse IP de hello avec hello adresse IP publique de votre machine virtuelle. Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création d’ordinateur virtuel de hello.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Installation de IIS à l’aide de PowerShell

Maintenant que vous êtes connecté toohello machine virtuelle Azure, vous pouvez utiliser une seule ligne de PowerShell tooinstall IIS et activer le trafic web tooallow hello pare-feu local règle. Ouvrez une invite de PowerShell et exécutez hello de commande suivante :

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Hello d’affichage page d’accueil IIS

Avec les services IIS sont installés et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut IIS page d’accueil. Être vraiment toouse hello adresse IP publique vous documenté au-dessus de la page par défaut toovisit hello. 

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Supprimer des ressources

Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web. toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Windows.

> [!div class="nextstepaction"]
> [Didacticiels sur les machines virtuelles Azure Windows](./tutorial-manage-vm.md)
