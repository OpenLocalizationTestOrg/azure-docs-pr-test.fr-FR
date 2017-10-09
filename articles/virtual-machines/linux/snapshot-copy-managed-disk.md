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
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="ff3ac-103">Créer une copie d’un disque dur virtuel stocké en tant que disque Azure géré à l’aide de captures instantanées gérées</span><span class="sxs-lookup"><span data-stu-id="ff3ac-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="ff3ac-104">Prendre un instantané d’un disque géré pour la sauvegarde ou créer un disque gérés à partir de la capture instantanée de hello et attachez-le tootroubleshoot de machine virtuelle de test tooa.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="ff3ac-105">Une capture instantanée gérée est une copie complète d’un disque géré de machine virtuelle à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="ff3ac-106">Elle crée une copie en lecture seule de votre disque dur virtuel et, par défaut, le stocke sous la forme d’un disque géré Standard.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="ff3ac-107">Pour plus d’informations sur la tarification, consultez la page [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="ff3ac-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="ff3ac-108">Utilisez soit hello tootake de Azure CLI 2.0 Azure portal ou hello un instantané de hello géré disque.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="ff3ac-109">Utilisez Azure CLI 2.0 tootake un instantané</span><span class="sxs-lookup"><span data-stu-id="ff3ac-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="ff3ac-110">Hello exemple suivant requiert hello Azure CLI 2.0 installé et connecté à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="ff3ac-111">Hello étapes suivantes montrent tooobtain et prenez un instantané d’un système d’exploitation géré de disque à l’aide de hello `az snapshot create` avec hello `--source-disk` paramètre.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="ff3ac-112">Hello exemple suivant suppose qu’il existe un ordinateur virtuel appelé `myVM` créé avec un disque du système d’exploitation géré Bonjour `myResourceGroup` groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="ff3ac-113">sortie de Hello doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="ff3ac-113">hello output should look something like:</span></span>

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

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="ff3ac-114">Utilisez tootake portail Azure un instantané</span><span class="sxs-lookup"><span data-stu-id="ff3ac-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="ff3ac-115">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff3ac-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ff3ac-116">À compter de hello supérieur gauche, cliquez sur **nouveau** et recherchez **instantané**.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="ff3ac-117">Dans le panneau de la capture instantanée hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="ff3ac-118">Entrez un **nom** pour la capture instantanée de hello.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="ff3ac-119">Sélectionnez un existant [groupe de ressources](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="ff3ac-120">Sélectionnez un emplacement de centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="ff3ac-121">Pour **disque Source**, sélectionnez hello toosnapshot de disques gérés.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="ff3ac-122">Sélectionnez hello **type de compte** instantané d’hello toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="ff3ac-123">Nous vous recommandons d’utiliser le type **Standard_LRS**, sauf si vous avez besoin de la stocker sur un disque hautes performances.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="ff3ac-124">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-124">Click **Create**.</span></span>

<span data-ttu-id="ff3ac-125">Toouse hello instantané toocreate un disque géré et d’attacher une machine virtuelle qui doit effectuer haute toobe, utilisez le paramètre hello `--sku Premium_LRS` avec hello `az snapshot create` commande.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="ff3ac-126">Cette opération crée instantané d’hello pour qu’il est stocké comme disque Premium gérés.</span><span class="sxs-lookup"><span data-stu-id="ff3ac-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="ff3ac-127">Les disques gérés Premium sont plus performants, car il s’agit de disques SSD, mais ils coûtent plus cher que des disques Standard (HDD).</span><span class="sxs-lookup"><span data-stu-id="ff3ac-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


