---
title: "aaaManage vos machines virtuelles à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Découvrir les commandes que vous pouvez utiliser des tâches tooautomate dans la gestion de vos machines virtuelles."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Gérer vos machines virtuelles à l’aide d’Azure PowerShell
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour les commandes PowerShell communes à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Plusieurs tâches que vous effectuez chaque toomanage jour vos machines virtuelles peuvent être automatisées à l’aide des applets de commande PowerShell de Azure. Cet article vous donne des exemples de commandes pour des tâches plus simples et tooarticles des liens qui montrent les commandes hello pour des tâches plus complexes.

> [!NOTE]
> Si vous n’avez pas encore installé et configuré Azure PowerShell, vous pouvez obtenir des instructions dans l’article de hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Comment toouse hello des exemples de commandes
Vous devez tooreplace une partie du texte hello dans hello commandes avec le texte qui est approprié pour votre environnement. Hello < et > symboles indiquent le texte tooreplace. Lorsque vous remplacez le texte hello, supprimer les symboles de hello, mais laissez les guillemets hello en place.

## <a name="get-a-vm"></a>Obtenir une machine virtuelle
Il s’agit d’une tâche de base que vous utiliserez souvent. Utiliser tooget d’informations sur une machine virtuelle, effectuer des tâches sur une machine virtuelle ou obtenir toostore de sortie dans une variable.

tooget informations hello machine virtuelle, exécutez cette commande, en remplaçant tous les éléments entre guillemets hello, y compris hello < et > :

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

hello toostore de sortie dans une variable $vm, exécutez :

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Ouvrez une session sur tooa ordinateurs virtuels Windows
Exécutez ces commandes :

> [!NOTE]
> Vous pouvez obtenir hello virtual machine et le nom du service cloud à partir de l’affichage de hello Hello **Get-AzureVM** commande.
> 
> $svcName = «<cloud service name>» $vmName = »<virtual machine name>» $localPath = « < lecteur et le dossier fichier emplacement toostore hello téléchargé RDP, par exemple : c:\temp > « $localFile = $localPath + «\" + $vmname + « .rdp « Get-AzureRemoteDesktopFile - ServiceName $svcName-nom - LocalPath $vmName $localFile-lancement
> 
> 

## <a name="stop-a-vm"></a>Arrêter une machine virtuelle
Exécutez cette commande :

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Utilisez cette hello tookeep de paramètre de service IP virtuelle (VIP) du cloud de hello en cas de hello dernier ordinateur virtuel dans ce service cloud. <br><br> Si vous utilisez le paramètre de StayProvisioned hello, vous serez toujours facturé pour hello machine virtuelle.
> 
> 

## <a name="start-a-vm"></a>Démarrer une machine virtuelle
Exécutez cette commande :

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Association d’un disque de données
Cette tâche nécessite de réaliser quelques étapes. Tout d’abord, vous utilisez hello *** Add-AzureDataDisk *** applet de commande tooadd hello toohello $vm objet de disque. Ensuite, vous utilisez **Update-AzureVM** configuration hello applet de commande tooupdate hello machine virtuelle.

Vous devez également toodecide si tooattach un nouveau disque ou un qui contient des données. Commande hello crée le fichier .vhd de hello pour un nouveau disque et l’attache.

tooattach un nouveau disque, exécutez la commande suivante :

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach un disque de données existant, exécutez la commande suivante :

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach des disques de données à partir d’un fichier .vhd existant dans le stockage blob, exécutez la commande suivante :

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Créer une machine virtuelle Windows
toocreate une basé sur Windows machine virtuelle dans Azure, suivez les instructions du hello [toocreate d’utiliser Azure PowerShell et préconfigurer des machines virtuelles basées sur Windows](create-powershell.md). Étapes de cette rubrique vous guide dans la création d’une commande que la valeur de Azure PowerShell hello crée un ordinateur virtuel basé sur Windows qui peut être préconfiguré :

* une appartenance au domaine Active Directory ;
* des disques supplémentaires ;
* une appartenance à un jeu d’équilibrage de la charge ;
* une adresse IP statique.

