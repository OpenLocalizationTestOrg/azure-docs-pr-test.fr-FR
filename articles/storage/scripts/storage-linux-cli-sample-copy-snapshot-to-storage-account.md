---
title: "Exemple de Script Azure CLI - Exporter/copier une capture instantanée en tant que VHD vers un compte de stockage dans une autre région | Microsoft Docs"
description: "Exemple de Script Azure CLI - Exporter/copier une capture instantanée en tant que VHD vers un compte de stockage dans un abonnement identique ou différent"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: fafb74af5f02f74036c770934c5e33f1b8a5593e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="f278e-103">Exporter/copier des captures instantanées managée en tant que VHD vers un compte de stockage dans une région différente avec l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="f278e-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="f278e-104">Ce script exporte une capture instantanée managée vers un compte de stockage dans une région différente.</span><span class="sxs-lookup"><span data-stu-id="f278e-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="f278e-105">Il génère d’abord l’URI SAP de la capture instantanée et l’utilise ensuite pour copier celle-ci vers un compte de stockage dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="f278e-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="f278e-106">Ce script vous permet de conserver la sauvegarde de vos disques gérés dans une autre région en cas de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="f278e-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f278e-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f278e-107">Sample script</span></span>

<span data-ttu-id="f278e-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copier une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="f278e-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="f278e-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f278e-109">Script explanation</span></span>

<span data-ttu-id="f278e-110">Ce script utilise les commandes suivantes afin de générer un URI SAS pour une capture instantanée gérée et copie cette dernière vers un compte de stockage à l’aide de l’URI SAS.</span><span class="sxs-lookup"><span data-stu-id="f278e-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="f278e-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f278e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f278e-112">Commande</span><span class="sxs-lookup"><span data-stu-id="f278e-112">Command</span></span> | <span data-ttu-id="f278e-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="f278e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f278e-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="f278e-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="f278e-115">Génère l’URI SAP en lecture seule qui est utilisé pour copier le fichier de VHD sous-jacent vers un compte de stockage ou le télécharger en local.</span><span class="sxs-lookup"><span data-stu-id="f278e-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="f278e-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="f278e-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="f278e-117">Copie un objet blob de façon asynchrone à partir d’un compte de stockage vers un autre.</span><span class="sxs-lookup"><span data-stu-id="f278e-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f278e-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f278e-118">Next steps</span></span>

[<span data-ttu-id="f278e-119">Créer un disque managé à partir d’un VHD</span><span class="sxs-lookup"><span data-stu-id="f278e-119">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="f278e-120">Créer une machine virtuelle à partir d’un disque managé</span><span class="sxs-lookup"><span data-stu-id="f278e-120">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="f278e-121">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f278e-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f278e-122">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f278e-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
