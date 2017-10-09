---
title: "définit des aaaDeploy une application sur l’échelle de machines virtuelles"
description: Utiliser des extensions toodepoy une application sur Azure, machines virtuelles identiques.
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Déployer votre application sur des groupes de machines virtuelles identiques

Cet article décrit les différentes façons de définition de logiciel tooinstall hello hello temporel est configuré.

Vous souhaiterez peut-être tooreview hello [échelle Set conception Overview](virtual-machine-scale-sets-design-overview.md) article, qui décrit quelques-unes des hello les limites imposées par les machines virtuelles identiques.

## <a name="capture-and-reuse-an-image"></a>Capturer et réutiliser une image

Vous pouvez utiliser un ordinateur virtuel que vous avez dans Azure tooprepare une image de base pour votre échelle défini. Ce processus crée un disque géré dans votre compte de stockage, vous pouvez faire référence en tant qu’image de base hello pour votre jeu de mise à l’échelle. 

Hello comme suit :

1. Créer une machine virtuelle Azure
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. À distance dans hello de machine virtuelle et de personnaliser les besoins de tooyour système hello.

   Si vous le souhaitez, vous pouvez installer votre application maintenant. Toutefois, sachez que par l’installation de votre application maintenant, vous pouvez effectuer de mise à niveau de votre application plus complexe, car vous devrez peut-être tooremove il premier. Au lieu de cela, vous pouvez utiliser cette tooinstall étape les conditions préalables que votre application peut avoir besoin, comme une fonctionnalité spécifique de l’exécution ou le système d’exploitation.

3. Suivez hello « capturer une machine » didacticiel pour soit [Linux] [ linux-vm-capture] ou [Windows][windows-vm-capture].

4. Créer un [ensemble d’échelle de Machine virtuelle] [ vmss-create] avec hello image URI que vous avez capturée dans l’étape précédente de hello.

Pour plus d’informations sur les disques, consultez [Vue d’ensemble de Managed Disks](../virtual-machines/windows/managed-disks-overview.md) et [Utiliser des disques de données attachés](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Installer lors de la configuration de l’ensemble d’échelle hello

Extensions de machine virtuelle peuvent être appliqué tooa machines virtuelles identiques. Avec une extension de machine virtuelle, vous pouvez personnaliser des machines virtuelles de hello dans une échelle définie en tant qu’ensemble d’un groupe. Pour plus d’informations sur les extensions, consultez [Extensions de machine virtuelle](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Il existe trois extensions principales que vous pouvez utiliser, selon que votre système d’exploitation est Linux ou Windows.

### <a name="windows"></a>Windows

Pour un système d’exploitation Windows, utilisez soit hello **Script personnalisé v1.8** extension ou hello **DSC PowerShell** extension.

#### <a name="custom-script"></a>Script personnalisé

extension de Script personnalisé de Hello exécute un script sur chaque instance de machine virtuelle dans un ensemble d’échelle hello. Un fichier de configuration ou une variable indique quels fichiers sont téléchargés toohello virtual machine, puis quelle commande s’exécute. Vous pouvez par exemple utiliser cette toorun un programme d’installation, un script, un fichier de commandes, tout fichier exécutable.

PowerShell utilise une table de hachage pour les paramètres de hello. Cet exemple configure toorun extension de script personnalisé hello un script PowerShell qui installe les services IIS.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hello d’utilisation `-ProtectedSetting` basculer pour tous les paramètres qui contiennent des informations sensibles.

---------


Azure CLI utilise un fichier json pour les paramètres de hello. Cet exemple configure toorun extension de script personnalisé hello un script PowerShell qui installe les services IIS. Enregistrer hello en tant que le fichier json suivant _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Ensuite, exécutez cette commande Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.

### <a name="powershell-dsc"></a>DSC PowerShell

Vous pouvez utiliser des instances de machine virtuelle DSC PowerShell toocustomize hello échelle ensemble. Hello **DSC** extension publié par **Microsoft.Powershell** déploie et exécute la configuration DSC de hello fourni sur chaque instance de machine virtuelle. Un fichier de configuration ou une variable indique l’extension de hello où *.zip* package est et qui _fonction de script_ toorun de combinaison.

PowerShell utilise une table de hachage pour les paramètres de hello. Cet exemple déploie un package DSC qui installe IIS.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hello d’utilisation `-ProtectedSetting` basculer pour tous les paramètres qui contiennent des informations sensibles.

-----------

CLI Azure utilise json pour les paramètres de hello. Cet exemple déploie un package DSC qui installe IIS. Enregistrer hello en tant que le fichier json suivant _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Ensuite, exécutez cette commande Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.

### <a name="linux"></a>Linux

Linux permettre utiliser soit hello **Script personnalisé v2.0** extension ou utilisez **cloud-init** lors de la création.

Script personnalisé est une extension simple qui télécharge les instances de machine virtuelle toohello de fichiers et exécute une commande.

#### <a name="custom-script"></a>Script personnalisé

Enregistrer hello en tant que le fichier json suivant _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Utilisez hello CLI d’Azure tooadd cette tooan extension existante de machines virtuelles identiques. Chaque ordinateur virtuel dans l’échelle de hello définir automatiquement s’exécute hello extension.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello d’utilisation `--protected-settings` basculer pour tous les paramètres qui contiennent des informations sensibles.

#### <a name="cloud-init"></a>Cloud-Init

Init-cloud est utilisée lors de la création d’un ensemble d’échelle hello. Commencez par créer un fichier local nommé _cloud-init.txt_ et ajoutez votre tooit de configuration. Par exemple, consultez [ce Gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Hello d’utiliser Azure CLI toocreate une échelle définie. Hello `--custom-data` champ accepte le nom de fichier hello d’un script d’initialisation de cloud.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Comment gérer les mises à jour de l’application ?

Si vous avez déployé votre application via une extension, modifiez la définition d’extension hello d’une certaine façon. Cette modification entraîne des instances de machine virtuelle tooall hello extension toobe redéployé. Un élément **doit** être modifié sur l’extension hello, comme le renommage d’un fichier référencé, dans le cas contraire, Azure fait pas les voir qui hello extension a changé.

Si l’application hello intégrées de votre propre image de système d’exploitation, utilisez un pipeline de déploiement automatisé des mises à jour de l’application. Concevoir votre toofacilitate architecture rapide le remplacement d’une échelle intermédiaire en production. Un bon exemple de cette approche est hello [fonctionne-t-elle Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Programme de compression](https://www.packer.io/) et [Terraform](https://www.terraform.io/) prise en charge Azure Resource Manager, donc vous pouvez également définir vos images « en tant que code » et les générer dans Azure, puis utiliser hello disque dur virtuel dans votre ensemble d’échelle. Cependant, cette opération devient problématique pour les images de place de marché, pour lesquelles les extensions / scripts personnalisés deviennent plus importants, car vous ne manipulez pas directement les éléments exécutables de la Place de marché.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Que se passe-t-il quand le nombre de machines virtuelles d’un groupe de machines virtuelles identiques augmente ?
Lorsque vous ajoutez un ou plusieurs ordinateurs virtuels tooa identiques, application hello est installée automatiquement. Pour exemple, si la valeur de l’échelle de hello a extensions définies, ils s’exécuter sur un nouvel ordinateur virtuel chaque fois qu’il est créé. Si l’ensemble d’échelle hello est basé sur une image personnalisée, tout nouvel ordinateur virtuel est une copie de l’image personnalisée de hello source. Si hello échelle jeu d’ordinateurs virtuels sont des hôtes de conteneur, peut-être conteneurs de démarrage du code tooload hello dans une Extension de Script personnalisé. Une extension peut aussi installer un agent qui s’inscrit auprès d’un orchestrateur de cluster, comme Azure Container Service.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Comment déployer une mise à jour du système d’exploitation sur plusieurs domaines de mise à jour ?
Supposons que vous tooupdate votre image de système d’exploitation tout en conservant l’échelle de machines virtuelles hello configuré pour s’exécuter. PowerShell et hello CLI d’Azure peuvent mettre à jour des images de machine virtuelle hello, un seul ordinateur virtuel à la fois. Hello [mise à niveau d’un ensemble d’échelle de Machine virtuelle](./virtual-machine-scale-sets-upgrade-scale-set.md) article fournit également des informations supplémentaires sur les options disponible tooperform mise à niveau du système d’exploitation sur un ensemble d’échelle de machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

* [Utilisez PowerShell toomanage votre ensemble d’échelle.](virtual-machine-scale-sets-windows-manage.md)
* [Créez un modèle de groupe identique](virtual-machine-scale-sets-mvss-start.md).


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

