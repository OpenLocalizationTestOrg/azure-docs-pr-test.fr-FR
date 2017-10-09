---
title: "aaaCopy un géré Azure du disque pour la sauvegarde des | Documents Microsoft"
description: "Découvrez comment toocreate émet une copie d’un toouse des disques gérés Azure précédent ou de résolution des problèmes de disque."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Créer une copie d’un disque dur virtuel stocké en tant que disque Azure géré à l’aide de captures instantanées gérées
Prendre un instantané d’un disque géré pour la sauvegarde ou créer un disque gérés à partir de la capture instantanée de hello et attachez-le tootroubleshoot de machine virtuelle de test tooa. Une capture instantanée gérée est une copie complète d’un disque géré de machine virtuelle à un moment donné. Elle crée une copie en lecture seule de votre disque dur virtuel et, par défaut, le stocke sous la forme d’un disque géré Standard. 

Pour plus d’informations sur la tarification, consultez la page [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Utilisez soit hello tootake de Azure CLI 2.0 Azure portal ou hello un instantané de hello géré disque.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Utilisez Azure CLI 2.0 tootake un instantané

> [!NOTE] 
> Hello exemple suivant requiert hello Azure CLI 2.0 installé et connecté à votre compte Azure.

Hello étapes suivantes montrent tooobtain et prenez un instantané d’un système d’exploitation géré de disque à l’aide de hello `az snapshot create` avec hello `--source-disk` paramètre. Hello exemple suivant suppose qu’il existe un ordinateur virtuel appelé `myVM` créé avec un disque du système d’exploitation géré Bonjour `myResourceGroup` groupe de ressources.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

sortie de Hello doit ressembler à :

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Utilisez tootake portail Azure un instantané 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. À compter de hello supérieur gauche, cliquez sur **nouveau** et recherchez **instantané**.
3. Dans le panneau de la capture instantanée hello, cliquez sur **créer**.
4. Entrez un **nom** pour la capture instantanée de hello.
5. Sélectionnez un existant [groupe de ressources](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau. 
6. Sélectionnez un emplacement de centre de données Azure.  
7. Pour **disque Source**, sélectionnez hello toosnapshot de disques gérés.
8. Sélectionnez hello **type de compte** instantané d’hello toouse toostore. Nous vous recommandons d’utiliser le type **Standard_LRS**, sauf si vous avez besoin de la stocker sur un disque hautes performances.
9. Cliquez sur **Créer**.

Toouse hello instantané toocreate un disque géré et d’attacher une machine virtuelle qui doit effectuer haute toobe, utilisez le paramètre hello `--sku Premium_LRS` avec hello `az snapshot create` commande. Cette opération crée instantané d’hello pour qu’il est stocké comme disque Premium gérés. Les disques gérés Premium sont plus performants, car il s’agit de disques SSD, mais ils coûtent plus cher que des disques Standard (HDD).


