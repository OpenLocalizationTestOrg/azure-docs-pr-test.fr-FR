---
title: aaaFrequently aux questions sur la pile de Azure | Documents Microsoft
description: "Pile Azure les questions fréquemment posées."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a>Forum aux questions sur la pile de Azure
## <a name="deployment"></a>Déploiement
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a>Dois-je tooformat mes disques de données avant de démarrer ou redémarrer une installation ?
Disques doivent être au format brut. Si vous réinstallez le système d’exploitation de hello, devez toocheck si le pool de stockage ancien hello est encore présent, vous supprimer à l’aide de hello comme suit :

1. Ouvrez le Gestionnaire de serveurs.
2. Sélectionnez les Pools de stockage.
3. Voir si un pool de stockage est répertorié.
4. Avec le bouton droit **pool de stockage** si répertoriés et activer en lecture / écriture.
5. Avec le bouton droit **disque dur virtuel** (en bas à gauche), puis sélectionnez Supprimer.
6. Avec le bouton droit **Pool de stockage** et cliquez sur Supprimer.
7. Relancez le script de la pile d’Azure et vérifiez que passe la vérification de disque hello.

Si vous le souhaitez, hello script suivant peut être utilisé :

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a>Puis-je utiliser tous les disques SSD pour le pool de stockage hello Bonjour installation de preuve de concept ?
Pour plus d’informations sur les configurations de stockage, consultez hello [guide des spécifications](azure-stack-deploy.md).

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a>Puis-je utiliser des disques de données NVMe pour hello preuve de concept pile Microsoft Azure ?
Espaces de stockage Direct prend en charge les disques NVMe, pile de Azure ne prend en charge un sous-ensemble des types de lecteurs de hello et combinaisons possibles des espaces de stockage Direct.  Consultez hello [guide des spécifications](azure-stack-deploy.md) pour plus d’informations. 

### <a name="how-can-i-reinstall-azure-stack"></a>Comment puis-je réinstaller Azure pile ?
Vous pouvez suivre les étapes de hello Bonjour [guide de redéploiement](azure-stack-redeploy.md).  

## <a name="tenant"></a>Locataire
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a>Puis-je déployer mon propre images en tant que client ?
Oui, tout comme dans Azure, un client peut télécharger des images dans la pile d’Azure, en outre images hello toousing hello administrateur de service. Pour une vue d’ensemble, consultez hello [Ajout d’une Image de machine virtuelle](azure-stack-add-vm-image.md). 

## <a name="testing"></a>Test
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a>Puis-je utiliser hello tootest de virtualisation imbriquée preuve de concept pile Microsoft Azure ?
La virtualisation imbriquée n’est pas pris en charge ou n’est pas testée avec Azure pile Technical Preview 3.

## <a name="virtual-machines"></a>Machines virtuelles
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a>Pile de Azure prend-il en charge les disques dynamiques pour les ordinateurs virtuels ?
Pile Azure ne prend pas en charge les disques dynamiques.


## <a name="next-steps"></a>Étapes suivantes
[Dépannage](azure-stack-troubleshooting.md)

