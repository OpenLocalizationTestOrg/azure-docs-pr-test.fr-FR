---
title: aaaMove un tooAzure les machines virtuelles Windows AWS | Documents Microsoft
description: "Déplacer un tooAzure d’instance Amazon Web Services (AWS) EC2 Windows des ordinateurs virtuels à l’aide d’Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="1ac1f-103">Déplacer une machine virtuelle Windows à partir de tooAzure Amazon Web Services (AWS) à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ac1f-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="1ac1f-104">Si vous évaluez des machines virtuelles pour l’hébergement de vos charges de travail, vous pouvez exporter une instance existante de la machine virtuelle Windows de EC2 Amazon Web Services (AWS), puis télécharger tooAzure de disque dur virtuel (VHD) hello.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="1ac1f-105">Une fois vous hello que généralisé est téléchargé, vous pouvez créer une nouvelle machine virtuelle dans Azure à partir de hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="1ac1f-106">Cette rubrique décrit le déplacement d’une seule machine virtuelle à partir de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="1ac1f-107">Si vous souhaitez que les ordinateurs virtuels toomove tooAzure AWS à grande échelle, consultez [migrer des ordinateurs virtuels dans tooAzure Amazon Web Services (AWS) avec Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1ac1f-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="1ac1f-108">Préparer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1ac1f-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="1ac1f-109">Vous pouvez télécharger tooAzure de disques durs virtuels généralisée et spécialisée.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="1ac1f-110">Chaque type nécessite une préparation hello machine virtuelle avant d’exporter à partir de AWS.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="1ac1f-111">**Disque dur virtuel généralisé** : toutes les informations de votre compte personnel de ce type de disque ont été supprimées avec Sysprep.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="1ac1f-112">Si vous envisagez de toouse hello disque dur virtuel en tant qu’une image de toocreate nouvelles machines virtuelles à partir de, vous devez :</span><span class="sxs-lookup"><span data-stu-id="1ac1f-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="1ac1f-113">[Préparer une machine virtuelle Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="1ac1f-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="1ac1f-114">Généraliser l’ordinateur virtuel de hello à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="1ac1f-115">**Spécialisé de disque dur virtuel** -un disque dur virtuel spécialisé gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="1ac1f-116">Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="1ac1f-117">[Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="1ac1f-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="1ac1f-118">**Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="1ac1f-119">Supprimer les outils de virtualisation invité et les agents installés sur hello VM (autrement dit, les outils VMware).</span><span class="sxs-lookup"><span data-stu-id="1ac1f-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="1ac1f-120">Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="1ac1f-121">Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="1ac1f-122">Exporter et télécharger hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="1ac1f-122">Export and download hello VHD</span></span> 

<span data-ttu-id="1ac1f-123">Exporter hello EC2 instance tooa disque dur virtuel dans un compartiment Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="1ac1f-124">Hello les étapes décrites dans la rubrique de documentation Amazon hello [exportation d’une Instance en tant qu’une machine virtuelle à l’aide de machine virtuelle Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) et exécution hello [créer-instance-export-tâche](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) commande tooexport hello EC2 fichier de disque dur virtuel tooa instance.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="1ac1f-125">Hello fichier de disque dur virtuel exporté est enregistré dans le compartiment hello Amazon S3 que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="1ac1f-126">Hello syntaxe de base pour l’exportation hello disque dur virtuel est ci-dessous, remplacez simplement texte d’espace réservé hello <brackets> avec vos informations.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="1ac1f-127">Une fois que hello disque dur virtuel a été exporté, suivez les instructions de hello dans [comment télécharger un objet à partir d’un compartiment S3 ?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello de toodownload disque dur virtuel du fichier à partir de compartiment de hello S3.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1ac1f-128">AWS facture des frais de transfert de données pour le téléchargement hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="1ac1f-129">Pour en savoir plus, consultez la page [Tarification Amazon S3](https://aws.amazon.com/s3/pricing/).</span><span class="sxs-lookup"><span data-stu-id="1ac1f-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1ac1f-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ac1f-130">Next steps</span></span>

<span data-ttu-id="1ac1f-131">Vous pouvez maintenant télécharger tooAzure de disque dur virtuel hello et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1ac1f-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="1ac1f-132">Si vous avez exécuté Sysprep sur votre source trop**généraliser** avant l’exportation, consultez [télécharger un disque dur virtuel généralisé et son utilisation toocreate un nouvelles machines virtuelles dans Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="1ac1f-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="1ac1f-133">Si vous n’avez pas exécuté Sysprep avant l’exportation, hello disque dur virtuel est considéré comme **spécialisées**, consultez [télécharger un tooAzure spécialisé de disque dur virtuel et créer une machine virtuelle](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="1ac1f-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
