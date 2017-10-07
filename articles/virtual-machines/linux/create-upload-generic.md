---
title: "aaaCreate et télécharger un VHD Linux dans Azure"
description: "En savoir plus toocreate et téléchargez un Azure disque dur virtuel (VHD) qui contient un système d’exploitation Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Informations concernant les distributions non approuvées
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

contrat SLA de plateforme Windows Azure Hello applique machines toovirtual en cours d’exécution hello du système d’exploitation Linux uniquement lorsqu’un Hello [visé distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) est utilisé. Toutes les distributions Linux qui sont fournis dans hello Azure Galerie d’images sont approuvées distributions avec la configuration requise de hello.

* [Linux sur Azure : Distributions approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Prise en charge d’images Linux dans Microsoft Azure](https://support.microsoft.com/kb/2941892)

Toutes les distributions en cours d’exécution sur Azure devez toomeet un certain nombre de conditions préalables toohave un tooproperly chance s’exécutent sur la plateforme de hello.  Cet article n’est pas complète comme chaque distribution est différente. et il est tout à fait possible que, même si vous répondez à tous les critères de hello ci-dessous que vous devez toujours toosignificantly ajuster votre tooensure système Linux lequel il s’exécute correctement sur la plateforme de hello.

C'est pourquoi nous recommandons de commencer avec une de nos [distributions Linux approuvées sur Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dans la mesure du possible. Hello articles suivants vous guideront à travers comment tooprepare hello différents visé distributions Linux prises en charge sur Azure :

* **[Distributions CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES et openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

reste Hello de cet article traite des indications générales pour l’exécution de votre distribution Linux sur Azure.

## <a name="general-linux-installation-notes"></a>Notes générales d'installation de Linux
* format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**.  Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande convert-vhd. Si vous utilisez VirtualBox, cela signifie en sélectionnant **une taille fixe** en tant qu’et non par défaut de toohello allouée dynamiquement lors de la création du disque de hello.
* Azure ne prend en charge que les machines virtuelles de la génération 1. Vous pouvez convertir une disque de taille 1 machine virtuelle à partir du format de fichier de disque dur virtuel VHDX toohello et à partir de l’extension dynamique tooa fixée de génération. Mais vous ne pouvez pas modifier la génération d’une machine virtuelle. Pour plus d’informations, consultez [Dois-je créer une machine virtuelle de génération 1 ou 2 dans Hyper-V ?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* taille maximale de Hello autorisé pour hello que disque dur virtuel est de 1 023 go.
* Lorsque vous installez le système de Linux hello *recommandé* que vous utilisez les partitions standard au lieu du Gestionnaire de volume logique (souvent hello par défaut pour le nombre d’installations). Cela permet d’éviter Gestionnaire de volume logique nom est en conflit avec des ordinateurs virtuels ont, en particulier si un disque du système d’exploitation a besoin toobe jointe tooanother VM identiques pour le dépannage. La technique [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) peut être utilisée sur les disques de données.
* La prise en charge du noyau pour le montage de systèmes de fichiers UDF est requise. Au premier démarrage sur Azure hello mise en service de configuration est passée toohello Linux VM via un support au format UDF qui est attaché toohello invité. l’agent Azure Linux de Hello doit être en mesure de toomount hello UDF fichier système tooread sa configuration et configurer hello machine virtuelle.
* Les versions du noyau Linux antérieures à la version 2.6.37 ne prennent pas en charge NUMA sur Hyper-V avec des machines virtuelles de taille supérieure. Ce problème principalement les impacts de distributions antérieures à l’aide de hello en amont noyau de Red Hat 2.6.32 et a été corrigé dans RHEL 6.6 (noyau-2.6.32-504). Systèmes en cours d’exécution personnalisées noyaux antérieures à 2.6.37 ou les noyaux basée sur RHEL plus anciens que 2.6.32-504 doit définir hello paramètre démarrage `numa=off` sur noyau hello de ligne de commande dans grub.conf. Pour plus d’informations, consultez l’article [KB 436883](https://access.redhat.com/solutions/436883) sur Red Hat.
* Ne configurez pas une partition d’échange sur le disque du système d’exploitation hello. l’agent de Hello Linux peut être configuré toocreate un fichier d’échange sur le disque de ressources temporaires hello.  Vous trouverez plus d’informations à ce sujet dans les étapes de hello ci-dessous.
* Tous les disques durs virtuels hello doivent avoir des tailles qui sont des multiples de 1 Mo.

### <a name="installing-kernel-modules-without-hyper-v"></a>Installation de modules de noyau sans Hyper-V
Azure s’exécute sur un hyperviseur Hyper-V de hello, pour Linux nécessite l’installation de certains modules noyau dans l’ordre des toorun dans Azure. Si vous avez une machine virtuelle qui a été créée en dehors de Hyper-V, programmes d’installation de Linux hello ne comprennent pas les pilotes hello pour Hyper-V ramdisk initiale de hello (initrd ou initramfs), sauf si elle détecte qu’il s’exécute une un environnement Hyper-V. Lorsque vous utilisez un tooprepare système (Virtualbox, KVM, etc.) de virtualisation différent de votre image Linux, vous devrez peut-être toorebuild hello initrd tooensure qui a au moins hello `hv_vmbus` et `hv_storvsc` modules de noyau sont disponibles sur ramdisk initiale de hello.  Il s’agit au moins un problème connu sur les systèmes en fonction de distribution de Red Hat hello en amont.

mécanisme Hello pour la reconstruction de l’image initrd ou initramfs hello peut varier en fonction de distribution de hello. Veuillez à la documentation de votre distribution ou prend en charge de procédure de hello appropriée.  Voici un exemple de comment toorebuild hello initrd à l’aide de hello `mkinitrd` utilitaire :

Tout d’abord, sauvegardez les image initrd existante hello :

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Ensuite, régénérez initrd hello avec hello `hv_vmbus` et `hv_storvsc` modules de noyau :

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Redimensionnement des disques durs virtuels
Les images de disque dur virtuel sur Azure doivent avoir un too1MB taille virtuelle alignée.  En règle générale, les disques durs virtuels créés à l'aide d'Hyper-V sont déjà alignés correctement.  Si hello disque dur virtuel n’est pas correctement aligné, vous pouvez recevoir une erreur message similaire toohello suivant lorsque vous essayez de toocreate une *image* à partir de votre disque dur virtuel :

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy ce que vous pouvez redimensionner hello machine virtuelle à l’aide de la console du Gestionnaire Hyper-V hello ou hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) applet de commande Powershell.  Si vous n’exécutez pas dans un environnement Windows qu’il est recommandé de toouse qemu-img tooconvert (si nécessaire) et redimensionner hello disque dur virtuel.

> [!NOTE]
> Il existe un bogue connu dans la version 2.2.1 de qemu-img, qui entraîne un formatage incorrect de disque dur virtuel. problème de Hello a été résolu dans QEMU 2.6. Il est recommandé de toouse qemu-img 2.2.0 ou inférieur ou too2.6 de mise à jour ou une version ultérieure. Référence : https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Redimensionnement hello VHD directement l’aide des outils tels que `qemu-img` ou `vbox-manage` peut entraîner un disque dur virtuel non démarrable.  Il est donc recommandé toofirst convert hello image de disque dur virtuel tooa disque RAW.  Si l’image de machine virtuelle hello a déjà été créé en tant qu’image de disque (valeur par défaut de hello pour certains hyperviseurs telles que KVM) vous pouvez ignorer cette étape :
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Calculer hello requises de taille de tooensure d’image de disque hello qui hello taille virtuelle est alignée too1MB.  Hello bash shell script suivant peut aider à cela.  Hello script utilise «`qemu-img info`» toodetermine hello taille virtuelle de l’image de disque hello, puis il calcule hello taille toohello suivant 1 Mo :
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Redimensionner le disque hello à l’aide de $rounded_size en tant qu’ensemble Bonjour au-dessus de script :
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Maintenant, convertissez tooa arrière du disque RAW hello disque dur virtuel de taille fixe :
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Ou, avec la version de qemu **2.6 +** inclure hello `force_size` option :

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Conditions requises pour le noyau Linux
Hello pilotes de Services d’intégration Linux (LIS) pour Hyper-V et Azure sont fournis directement toohello en amont noyau Linux. Ces pilotes sont déjà disponibles dans de nombreuses distributions qui comprennent une version récente du noyau Linux (3.x et supérieures). Sinon, ces distributions fournissent des versions rétroportées de ces pilotes avec leurs noyaux.  Ces pilotes sont constamment mis à jour dans le noyau de hello en amont avec les nouveaux correctifs et fonctionnalités, lorsque cela est possible, il est recommandé toorun un [visé distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui inclut ces correctifs et les mises à jour.

Si vous exécutez une variante de versions de Red Hat Enterprise Linux **6.0-6.3**, vous devez les pilotes les plus récents LIS tooinstall hello pour Hyper-V. Vous pouvez trouver les pilotes de Hello [à cet emplacement](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). À compter de RHEL **6.4 +** (et dérivés) hello LIS pilotes sont déjà inclus avec le noyau de hello et par conséquent, aucune packages d’installation supplémentaires est nécessaire toorun ces systèmes dans Azure.

Si un noyau personnalisé est requis, il est recommandé d’une version plus récente de noyau toouse (c'est-à-dire **3.8 +**). Pour les distributions ou les fournisseurs qui gèrent leur propres noyau, des efforts seront requis tooregularly backport hello LIS pilotes du noyau de hello en amont noyau tooyour personnalisé.  Même si vous exécutez déjà une version de noyau relativement récentes, il est recommandé de suivre tookeep de n’importe quel en amont correctifs dans backport et les pilotes LIS hello celles en fonction des besoins. emplacement de Hello hello LIS source de fichiers de pilote est disponible dans hello [chargés de maintenance](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) fichier dans l’arborescence des sources de noyau Linux hello :

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Au minimum, absence hello Hello suivant les correctifs ont été problèmes toocause sur Azure, et par conséquent, ces doivent être inclus dans le noyau hello. Cette liste n’est pas exhaustive ni complète pour toutes les distributions :

* [ata_piix : différer les pilotes de disques toohello Hyper-V par défaut](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc : le compte pour les paquets de transit dans le chemin d’accès de hello réinitialisation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc : éviter l’utilisation de WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc :désactiver WRITE_SAME pour RAID et les pilotes adaptateurs de l’hôte virtuel](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc : correctif de déréférence du pointeur NULL](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc : des défaillances de la mémoire tampon de l’anneau peuvent entraîner un gel des E/S](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs : se protéger contre une double exécution de __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello Agent Linux Azure
Hello [Linux Agent Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) est requis tooproperly configurer une machine virtuelle de Linux dans Azure. Vous pouvez obtenir la version la plus récente hello, problèmes de fichiers ou envoyer des requêtes de tirage à hello [référentiel GitHub de l’Agent Linux](https://github.com/Azure/WALinuxAgent).

* l’agent de Linux Hello est publié sous licence de hello Apache 2.0. De nombreuses distributions fournissent déjà RPM ou deb packages pour l’agent de hello, et par conséquent, dans certains cas cela peut être installé et mis à jour avec un minimum d’effort.
* Hello Linux Agent Azure nécessite Python v2.6 +.
* agent de Hello nécessite également un module de python-pyasn1 hello. La plupart des distributions le fournissent sous la forme d'un package indépendant que vous pouvez installer.
* Dans certains cas hello Linux Agent Azure n’est peut-être pas compatible avec NetworkManager. Nombre des packages RPM/Deb hello fournies par les distributions de configurer NetworkManager en tant que conflit toohello waagent package et par conséquent désinstallera NetworkManager lorsque vous installez le package de l’agent Linux hello.

## <a name="general-linux-system-requirements"></a>Configuration générale requise Linux

* Modifier la ligne de démarrage de noyau de hello GRUB ou GRUB2 Bonjour tooinclude paramètres suivants. Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage :
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Cela garantit également tous les messages de console sont envoyés toohello premier port série, qui peut aider Azure prise en charge avec les problèmes de débogage.
  
    En outre toohello ci-dessus, il est recommandé de trop*supprimer* hello après les paramètres s’ils existent :
  
        rhgb quiet crashkernel=auto
  
    Graphique et silencieuse de démarrage ne sont pas utiles dans un environnement de cloud que nous voulons tous les toobe de journaux hello envoyé toohello de port série. Hello `crashkernel` option peut être gauche configuré si vous le souhaitez, mais notez que ce paramètre réduit hello de mémoire disponible dans hello VM à 128 Mo ou plus, qui peut être problématique sur les tailles de machine virtuelle plus petites hello.

* Lors de l’installation hello Linux Agent Azure
  
    Hello Linux Agent Azure est requis pour la configuration d’une image Linux sur Azure.  Nombre de distributions fournit agent hello comme un package RPM ou Deb (package de hello est généralement appelée « WALinuxAgent » ou 'walinuxagent').  Hello agent peut également être installé manuellement en suivant les étapes de hello Bonjour [Guide de l’Agent Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.  Cela est généralement hello par défaut.

* Ne créez pas d’espace d’échange sur le disque du système d’exploitation hello
  
    Hello Linux Agent Azure peut configurer automatiquement l’espace d’échange à l’aide du disque de ressources locales hello qui est attaché toohello machine virtuelle après le déploiement sur Azure. Notez que le disque local de ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée. Après avoir installé hello Linux Agent Azure (voir l’étape précédente), modifier hello suivant correctement les paramètres dans /etc/waagent.conf :
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Dans la dernière étape, exécutez hello suivant la machine virtuelle de commandes toodeprovision hello :
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Sur Virtualbox, vous pouvez voir l’erreur suivante après l’exécution de hello ' waagent-force - annuler le déploiement ' : `[Errno 5] Input/output error`. Ce message d’erreur n’est pas critique et peut être ignoré.
  > 
  > 

* Puis vous devez tooshut la machine virtuelle de hello et télécharger tooAzure de disque dur virtuel hello.

