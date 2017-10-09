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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Déplacer une machine virtuelle Windows à partir de tooAzure Amazon Web Services (AWS) à l’aide de PowerShell

Si vous évaluez des machines virtuelles pour l’hébergement de vos charges de travail, vous pouvez exporter une instance existante de la machine virtuelle Windows de EC2 Amazon Web Services (AWS), puis télécharger tooAzure de disque dur virtuel (VHD) hello. Une fois vous hello que généralisé est téléchargé, vous pouvez créer une nouvelle machine virtuelle dans Azure à partir de hello disque dur virtuel. 

Cette rubrique décrit le déplacement d’une seule machine virtuelle à partir de AWS tooAzure. Si vous souhaitez que les ordinateurs virtuels toomove tooAzure AWS à grande échelle, consultez [migrer des ordinateurs virtuels dans tooAzure Amazon Web Services (AWS) avec Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Préparer hello machine virtuelle 
 
Vous pouvez télécharger tooAzure de disques durs virtuels généralisée et spécialisée. Chaque type nécessite une préparation hello machine virtuelle avant d’exporter à partir de AWS. 

- **Disque dur virtuel généralisé** : toutes les informations de votre compte personnel de ce type de disque ont été supprimées avec Sysprep. Si vous envisagez de toouse hello disque dur virtuel en tant qu’une image de toocreate nouvelles machines virtuelles à partir de, vous devez : 
 
    * [Préparer une machine virtuelle Windows](prepare-for-upload-vhd-image.md).  
    * Généraliser l’ordinateur virtuel de hello à l’aide de Sysprep.  

 
- **Spécialisé de disque dur virtuel** -un disque dur virtuel spécialisé gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine. Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée.  
    * [Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md). **Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep. 
    * Supprimer les outils de virtualisation invité et les agents installés sur hello VM (autrement dit, les outils VMware). 
    * Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP. Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage.  


## <a name="export-and-download-hello-vhd"></a>Exporter et télécharger hello disque dur virtuel 

Exporter hello EC2 instance tooa disque dur virtuel dans un compartiment Amazon S3. Hello les étapes décrites dans la rubrique de documentation Amazon hello [exportation d’une Instance en tant qu’une machine virtuelle à l’aide de machine virtuelle Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) et exécution hello [créer-instance-export-tâche](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) commande tooexport hello EC2 fichier de disque dur virtuel tooa instance. 

Hello fichier de disque dur virtuel exporté est enregistré dans le compartiment hello Amazon S3 que vous spécifiez. Hello syntaxe de base pour l’exportation hello disque dur virtuel est ci-dessous, remplacez simplement texte d’espace réservé hello <brackets> avec vos informations.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Une fois que hello disque dur virtuel a été exporté, suivez les instructions de hello dans [comment télécharger un objet à partir d’un compartiment S3 ?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello de toodownload disque dur virtuel du fichier à partir de compartiment de hello S3. 

> [!IMPORTANT]
> AWS facture des frais de transfert de données pour le téléchargement hello disque dur virtuel. Pour en savoir plus, consultez la page [Tarification Amazon S3](https://aws.amazon.com/s3/pricing/).


## <a name="next-steps"></a>Étapes suivantes

Vous pouvez maintenant télécharger tooAzure de disque dur virtuel hello et créer une machine virtuelle. 

- Si vous avez exécuté Sysprep sur votre source trop**généraliser** avant l’exportation, consultez [télécharger un disque dur virtuel généralisé et son utilisation toocreate un nouvelles machines virtuelles dans Azure](upload-generalized-managed.md)
- Si vous n’avez pas exécuté Sysprep avant l’exportation, hello disque dur virtuel est considéré comme **spécialisées**, consultez [télécharger un tooAzure spécialisé de disque dur virtuel et créer une machine virtuelle](create-vm-specialized.md)

 
