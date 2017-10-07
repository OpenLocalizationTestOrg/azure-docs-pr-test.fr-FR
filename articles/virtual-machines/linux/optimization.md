---
title: aaaOptimize votre VM Linux sur Azure | Documents Microsoft
description: "Découvrez certaines toomake de conseils d’optimisation que vous avez configuré votre VM Linux pour des performances optimales sur Azure"
keywords: machine virtuelle linux, linux machine virtuelle, machine virtuelle ubuntu
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Optimiser votre machine virtuelle Linux sur Azure
Création d’une machine virtuelle de Linux (VM) est toodo facile à partir de la ligne de commande hello ou à partir du portail de hello. Ce didacticiel vous montre comment tooensure vous l’avez configuré toooptimize ses performances sur la plateforme de Microsoft Azure hello. Dans cette rubrique, une machine virtuelle de serveur Ubuntu est utilisée, mais vous pouvez également créer des machines virtuelles Linux en utilisant vos [propres images en tant que modèles](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Composants requis
Cet article repose sur l’hypothèse que vous disposez déjà d’un abonnement Azure actif ([s’inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)) et que vous avez déjà approvisionné une machine virtuelle dans votre abonnement Azure. Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté tooyour abonnement Azure avec [ouverture de session az](/cli/azure/#login) avant [créer une machine virtuelle](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Disque de système d’exploitation Azure
Lorsque vous créez une machine virtuelle Linux dans Azure, deux disques lui sont associés. **/dev/sda** est le disque de votre système d’exploitation, et **/dev/sdb** est votre disque temporaire.  N’utilisez pas de disque de système d’exploitation principal hello (**/dev/sda**) pour tout élément à l’exception de système d’exploitation de hello tel qu’il est optimisé pour les temps de démarrage rapide machine virtuelle et ne fournit pas de bonnes performances pour vos charges de travail. Vous souhaitez tooattach un ou plusieurs disques tooyour VM tooget persistant et optimisé le stockage pour vos données. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Ajout de disques selon vos objectifs de taille et de performances
En fonction de hello taille de machine virtuelle, vous pouvez attacher des too16 des disques supplémentaires sur une série, 32 disques sur une série D et 64 disques sur un ordinateur de la série G - chacun jusqu'à to too1 taille. Ajoutez des disques en fonction de vos besoins en matière d’espace et d’E/S par seconde. Chaque disque a une cible de performances de 500 IOps pour le stockage Standard et des e/s de too5000 par disque pour le stockage Premium.  Pour plus d’informations sur les disques de Stockage Premium, consultez l’article [Stockage Premium : stockage à hauts niveaux de performances pour les machines virtuelles Azure](../../storage/common/storage-premium-storage.md).

tooachieve hello IOps plus élevé sur des disques de stockage Premium où leurs paramètres de cache a tooeither **ReadOnly** ou **aucun**, vous devez désactiver **barrières** tandis que le montage de système de fichiers hello dans Linux. Vous n’avez pas besoin de barrières car hello écrit tooPremium stockage disques sauvegardées sont durables pour ces paramètres de cache.

* Si vous utilisez **reiserFS**, désactiver les obstacles à l’aide d’option de montage hello `barrier=none` (pour l’activation de barrières, utilisez `barrier=flush`)
* Si vous utilisez **ext3/ext4**, désactiver les obstacles à l’aide d’option de montage hello `barrier=0` (pour l’activation de barrières, utilisez `barrier=1`)
* Si vous utilisez **XFS**, désactiver les obstacles à l’aide d’option de montage hello `nobarrier` (pour l’activation de barrières, utilisez option de hello `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Considérations relatives aux comptes de stockage non gérés
Hello par défaut lorsque vous créez une machine virtuelle avec hello Azure CLI 2.0 sont toouse Azure géré disques.  Ces disques sont gérées par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les.  Les disques non gérés requièrent un compte de stockage et sont associés à certaines autres considérations en matière de performances.  Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).  Hello section suivante décrit les considérations de performances uniquement lorsque vous utilisez des disques non managés.  Là encore, hello par défaut et solution de stockage recommandée est de disques toouse géré.

Si vous créez une machine virtuelle avec des disques non managés, assurez-vous que vous attachez des disques à partir de comptes de stockage résidant dans hello même région que votre tooensure VM proximité et de réduire la latence du réseau.  Chaque compte de stockage Standard présente une limite de 20 000 E/S par seconde et une taille maximale de 500 To.  Cette limite fonctionne, y compris les disques hello du système d’exploitation et les disques de données que vous créez des disques tooapproximately 40 très sollicité. Pour les comptes de stockage Premium, il n’existe aucun nombre maximal d’E/S par seconde, mais une limite de taille de 32 To. 

Lors de travailler au niveau élevé IOps des charges de travail et que vous avez choisi de stockage Standard pour vos disques, vous devrez peut-être les disques hello toosplit entre plusieurs toomake des comptes de stockage que vous n’avez pas atteint hello 20 000 IOps limite pour les comptes de stockage Standard. Votre machine virtuelle peut contenir une combinaison de disques de différents comptes de stockage et tooachieve de types de compte de stockage votre configuration optimale.
 

## <a name="your-vm-temporary-drive"></a>Votre lecteur temporaire de machine virtuelle
Lorsque vous créez une machine virtuelle, Azure vous fournit par défaut un disque de système d’exploitation (**/dev/sda**) et un disque temporaire (**/dev/sdb**).  Tous les disques que vous ajoutez apparaissent sous la forme **/dev/sdc**, **/dev/sdd**, **/dev/sde**, etc. Les données figurant sur votre disque temporaire (**/dev/sdb**) ne sont pas pérennes et risquent d’être perdues si des événements spécifiques, tels qu’un redimensionnement, un redéploiement ou une maintenance de machine virtuelle, imposent un redémarrage de votre machine virtuelle.  taille de Hello et le type de votre disque temporaire est connexes toohello taille de machine virtuelle choisie au moment du déploiement. Tous les lecteur temporaire hello de machines virtuelles (série DS, G et DS_V2) taille hello premium sont soutenues par un disque SSD local pour augmenter les performances des e/s too48k. 

## <a name="linux-swap-file"></a>Fichier d’échange Linux
Si votre machine virtuelle Azure est à partir d’une image Ubuntu ou CoreOS, vous pouvez utiliser CustomData toosend un toocloud cloud-config-init. Si vous [avez téléchargé une image Linux personnalisée](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui utilise cloud-init, vous configurez également les partitions d’échange à l’aide de cloud-init.

Sur Ubuntu Cloud Images, vous devez utiliser partition d’échange cloud-init tooconfigure hello. Pour plus d’informations, consultez l’article [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Pour les images sans prise en charge de l’initialisation de nuage, des images de machine virtuelle déployées à partir d’Azure Marketplace de hello ont un Agent de Linux de machine virtuelle intégré à hello du système d’exploitation. Cet agent permet de toointeract de machine virtuelle hello avec différents services Azure. En supposant que vous avez déployé une image standard à partir de hello Azure Marketplace, vous devez toodo hello suivant toocorrectly configurer vos paramètres de fichier d’échange Linux :

Rechercher et modifier les deux entrées de hello **/etc/waagent.conf** fichier. Ils contrôlent hello l’existence d’un fichier d’échange dédié et de taille de fichier d’échange hello. paramètres Hello vous cherchez toomodify sont `ResourceDisk.EnableSwap=N` et`ResourceDisk.SwapSizeMB=0` 

Modifier hello toohello de paramètres suivant les paramètres :

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size dans Mo toomeet vos besoins} 

Une fois que vous avez modifié hello, vous devez toorestart hello waagent ou redémarrez votre tooreflect Linux VM ces modifications.  Vous connaissez les modifications hello ont été implémentées et un fichier d’échange a été créé lorsque vous utilisez hello `free` tooview d’espace libre de la commande. Hello exemple suivant comprend un fichier d’échange de 512 Mo créé suite à la modification hello **waagent.conf** fichier :

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>Algorithme de planification d’E/S pour le stockage Premium
Avec le noyau Linux hello 2.6.18 algorithme de planification hello par défaut d’e/s a été modifiée à partir de la date d’échéance tooCFQ (algorithme de file d’attente complètement juste). Pour les modèles d’E/S à accès aléatoire, les différences de performances entre CFQ et Deadline sont minimes.  Pour des disques SSD où le modèle d’e/s disque hello est essentiellement séquentielles, le retour toohello NOOP ou échéance d’un algorithme peut atteindre améliorer les performances d’e/s.

### <a name="view-hello-current-io-scheduler"></a>Planificateur de vue hello actuel d’e/s
Utilisez hello de commande suivante :  

```bash
cat /sys/block/sda/queue/scheduler
```

Vous consultez suivant de sortie, ce qui indique le planificateur actuel de hello.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Changer de périphérique en cours hello (/ dev/sda) des e/s de l’algorithme de planification
Utilisez hello suivant de commandes :  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> L’application de ce paramètre uniquement pour le disque **/dev/sda** n’a pas d’utilité. Définir sur tous les disques de données où les e/s séquentielles domine modèle d’e/s de hello.  

Vous devez voir hello suivant de sortie, ce qui indique que **grub.cfg** a été reconstruite avec succès et que le planificateur par défaut hello a été mis à jour tooNOOP.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Pourquoi la famille de Redhat distribution, vous devez uniquement hello de commande suivante :   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>À l’aide de tooachieve logiciel RAID de niveau supérieur I / Ops
Si vos charges de travail nécessitent plus d’IOps qu’un seul disque peut fournir, vous devez toouse une configuration RAID de logiciel de plusieurs disques. Étant donné que Azure effectue déjà la résilience de disque au niveau de l’infrastructure locale hello, vous obtenir hello plus haut niveau de performances d’une configuration d’agrégation par bandes RAID-0.  Configurer et créer des disques Bonjour environnement Azure et définissez-les tooyour Linux VM avant de partitionnement, de mise en forme et de montage de lecteurs hello.  Vous trouverez plus d’informations sur la configuration d’un programme d’installation RAID logiciels sur votre VM Linux dans azure Bonjour  **[configuration de RAID logiciels sur Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  document.

## <a name="next-steps"></a>Étapes suivantes
N’oubliez pas, comme avec toutes les discussions d’optimisation, vous devez tooperform des tests avant et après chaque impact sur les modifications toomeasure hello hello modification a.  L’optimisation est un processus graduel dont les résultats varient d’une machine à l’autre dans votre environnement.  Ce qui fonctionne bien pour une configuration donnée n’offre pas nécessairement de bons résultats pour d’autres.

Certaines ressources tooadditional de liens utiles : 

* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md)
* [Guide d’utilisateur de l’agent Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Optimisation des performances MySQL sur les machines virtuelles Linux Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configuration d’un RAID logiciel sur Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

