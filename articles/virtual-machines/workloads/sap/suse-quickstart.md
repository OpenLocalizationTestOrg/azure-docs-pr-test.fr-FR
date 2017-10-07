---
title: aaaTesting SAP NetWeaver sur machines virtuelles de Microsoft Azure SUSE Linux | Documents Microsoft
description: Test de SAP NetWeaver sur les machines virtuelles Microsoft Azure SUSE Linux
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Exécution de SAP NetWeaver sur des machines virtuelles Microsoft Azure SUSE Linux
Cet article décrit les différentes choses tooconsider lorsque vous exécutez SAP NetWeaver sur Microsoft Azure SUSE Linux virtual machines virtuelles. À compter du 19 mai 2016, SAP NetWeaver est officiellement pris en charge sur les machines virtuelles SUSE Linux dans Azure. Vous trouverez tous les détails concernant les versions de Linux, les versions du noyau SAP, etc. dans la note SAP 1928533 « Applications SAP sur Azure : produits et types de machines virtuelles pris en charge (SAP Applications on Azure: Supported Products and Azure VM types) ».
Vous trouverez une documentation supplémentaire concernant SAP sur des machines virtuelles Linux ici : [Utilisation de SAP sur des machines virtuelles Linux](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello informations suivantes devrait vous aider à éviter certains pièges potentiels.

## <a name="suse-images-on-azure-for-running-sap"></a>Images SUSE sur Azure pour l’exécution de SAP
Pour exécuter SAP NetWeaver sur Azure, utilisez uniquement SUSE Linux Enterprise Server SLES 12 (SPx) - Voir également la note SAP 1928533. Une image SUSE particulière est Bonjour Azure Marketplace (« SLES 11 Service Pack 3 pour les licences d’accès client SAP »), mais cela n’est pas prévu pour l’utilisation générale. N’utilisez pas cette image, car il est réservé pour hello [SAP Cloud application bibliothèque](https://cal.sap.com/) solution.  

Tous les nouveaux tests et toutes les installations sur Azure doivent être effectués avec Azure Resource Manager. toolook pour les images SUSE SLES et les versions à l’aide d’Azure PowerShell ou hello Azure interface de ligne de commande (CLI), hello utilisation suivant les commandes. Vous pouvez ensuite utiliser la sortie hello, par exemple, toodefine l’image hello du système d’exploitation dans un modèle JSON pour le déploiement d’une machine virtuelle de Linux SUSE.
Ces commandes PowerShell sont valides pour Azure PowerShell version 1.0.1 et ses versions ultérieures.

Alors qu’il est toujours possible de toouse hello standard SLES images pour les installations SAP qu’il est recommandé d’utiliser toomake hello SLES nouvelle pour les images de SAP qui sont disponibles maintenant sur hello Azure Galerie d’image. Vous trouverez plus d’informations sur ces images sur hello correspondant [page Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) ou hello [page web de SUSE FAQ sur SLES pour SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Rechercher les éditeurs existants, notamment SUSE :
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Rechercher les offres existantes de SUSE :
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Rechercher les offres SUSE SLES :
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Rechercher une version spécifique d’un SKU SLES :
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Installation de WALinuxAgent dans une machine virtuelle SUSE
agent Hello appelé WALinuxAgent fait partie des images SLES hello Bonjour Azure Marketplace. Pour plus d’informations sur son installation manuelle (par exemple, lors du chargement d’un disque dur virtuel (VHD) du système d’exploitation SLES à partir d’un emplacement local), voir les articles suivants :

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Microsoft Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>« Surveillance améliorée (Enhanced Monitoring) » SAP
SAP « surveillance améliorée » est un toorun prérequis obligatoire SAP sur Azure. Vérifiez les détails dans la note SAP 2191498 « SAP sur Linux avec Azure : surveillance améliorée (SAP on Linux with Azure: Enhanced Monitoring) ».

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Attachement de disques de données Azure tooan machine virtuelle de Azure Linux
Montez jamais tooan de disques de données Azure machine virtuelle de Azure Linux à l’aide des ID de périphérique hello. Utilisez plutôt l’identificateur unique universel de hello (UUID). Soyez prudent lorsque vous utilisez des outils graphiques toomount Azure des disques de données, par exemple. Vérifiez les entrées de hello dans/etc/fstab.

problème Hello avec l’ID de périphérique hello est qu’il peut changer et puis hello machine virtuelle Azure peut se bloquer dans le processus de démarrage hello. problème de hello toomitigate, vous pouvez ajouter le paramètre nofail de hello dans/etc/fstab. Cependant, soyez prudent avec nofail, car les applications peuvent utiliser de point de montage hello comme avant et peuvent écrire dans le système de fichiers racine hello en cas d’un disque de données Azure externe n’a pas été monté pendant le démarrage de hello.

toomounting de seule exception Hello via UUID attachement d’un disque du système d’exploitation pour résoudre des problèmes, comme décrit dans hello suivant la section.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Résolution des problèmes d’une machine virtuelle SUSE devenue inaccessible
Il peut y avoir des situations où un VM SUSE sur Azure se bloque dans le processus de démarrage hello (par exemple, avec une erreur liée à monter les disques). Vous pouvez vérifier ce problème à l’aide de la fonctionnalité diagnostics de démarrage hello pour v2 de Machines virtuelles Azure Bonjour portail Azure. Pour plus d’informations, voir [Boot diagnostics](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)(Diagnostics de démarrage).

Problème de hello toosolve unidirectionnelle est tooattach hello du système d’exploitation à partir de hello endommagé VM tooanother VM SUSE sur Azure. Apportez les modifications appropriées, comme modifier/etc/fstab ou suppression des règles d’udev réseau, comme décrit dans la section suivante de hello.

Il existe un point essentiel tooconsider. Déploiement de plusieurs machines virtuelles de SUSE à partir de hello entraîne la même image Azure Marketplace (par exemple, SLES 11 SP4) hello du système d’exploitation disque tooalways être montés par hello même UUID. Par conséquent, à l’aide de hello UUID tooattach un disque du système d’exploitation d’une autre machine virtuelle a été déployée à l’aide de hello même image Azure Marketplace entraîne deux UUID identiques. Cela provoque des problèmes et peut signifier que hello destinée à la résolution des problèmes de machine virtuelle démarre en fait à partir de hello attaché et disque du système d’exploitation endommagé à la place de hello d’origine.

Il existe deux façons tooavoid cela :

* Utiliser une autre image Azure Marketplace pour hello résolution des problèmes d’ordinateur virtuel (par exemple, SLES 11 SPx au lieu de SLES 12).
* Ne pas attacher le disque du système d’exploitation hello endommagé à partir d’un autre ordinateur virtuel à l’aide d’UUID--utilisez autre chose.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Télécharger un VM SUSE de local tooAzure
Pour obtenir une description de tooupload d’étapes hello un VM SUSE de local tooAzure, consultez [préparer un ordinateur virtuel SLES ou openSUSE Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Si vous souhaitez tooupload une machine virtuelle sans annuler le déploiement hello étape à fin hello (par exemple, tookeep une installation existante de SAP, comme nom d’hôte hello), vérifiez hello éléments suivants :

* Assurez-vous que ce disque hello du système d’exploitation est monté à l’aide des ID de périphérique UUID et pas hello. Modification tooUUID simplement dans/etc/fstab n’est pas suffisant pour le disque du système d’exploitation hello. En outre, n’oubliez pas tooadapt hello du chargeur de démarrage par YaST ou en modifiant les /boot/grub/menu.lst.
* Si vous utilisez le format VHDX de hello pour le disque du système d’exploitation SUSE hello et convertissez tooVHD pour le téléchargement tooAzure, il est très probable que ce périphérique de réseau hello pourra eth0 tooeth1. tooavoid problèmes lorsque vous utilisez le démarrage sur Azure plus tard, modifiez tooeth0 précédent, comme décrit dans [fixation eth0 dans cloné SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

De plus toowhat décrit dans l’article hello, nous vous recommandons de supprimer ce :

   /lib/udev/rules.d/75-persistent-net-generator.rules

Vous pouvez également installer toohelp de Azure (waagent) de le Linux Agent hello vous éviterez des problèmes potentiels, tant qu’il n’existe pas de plusieurs cartes réseau.

## <a name="deploying-a-suse-vm-on-azure"></a>Déploiement d’une machine virtuelle SUSE sur Azure
Vous devez créer de nouvelles machines virtuelles de SUSE à l’aide de fichiers de modèle JSON dans le nouveau modèle de gestionnaire de ressources Azure hello. Une fois le fichier de modèle JSON hello est créé, vous pouvez déployer hello machine virtuelle à l’aide de hello commande CLI comme un autre tooPowerShell suivante :

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Pour plus d’informations sur les fichiers de modèle JSON, voir [Création de modèles Azure Resource Manager](../../../resource-group-authoring-templates.md) et [Modèles de démarrage rapide Microsoft Azure](https://azure.microsoft.com/documentation/templates/).

Pour plus d’informations sur l’interface CLI et Azure Resource Manager, consultez [hello d’utilisation CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Licence SAP et clé matérielle
Pour la certification SAP-Azure officielle hello, un nouveau mécanisme a été clé toocalculate introduites hello SAP matérielle qui est utilisé pour la licence SAP hello. noyau SAP Hello avait toobe adapté toomake utilisation. Les anciennes versions du noyau SAP pour Linux n’incluent pas cette modification du code. Par conséquent, dans certaines situations (par exemple, Azure VM redimensionnement), de modifier la clé de matériel SAP hello et licence SAP hello n’a été n’est plus valide. Cela peut être résolu dans les noyaux Linux de SAP de la dernière hello. Pour plus d’informations, consultez la note SAP 1928533.

## <a name="suse-sapconf-package--tuned-adm"></a>Package sapconf SUSE / tuned-adm
SUSE fournit un package appelé « sapconf » qui gère un ensemble de paramètres propres à SAP. Pour plus d’informations sur le ce package et comment tooinstall et l’utiliser, consultez [à l’aide de sapconf tooprepare les systèmes SAP un SUSE Linux Enterprise Server toorun](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) et [What ' s sapconf ou comment tooprepare un SUSE Linux Enterprise Serveur pour l’exécution de systèmes SAP ? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Bonjour attendant il existe un nouvel outil qui remplace sapconf - ADM-paramétrées. Un trouverez plus d’informations sur cet outil suit hello deux des liens ci-dessous.

Vous trouverez [ici](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Les systèmes de paramétrage pour les charges de travail SAP avec tuned-adm se trouvent [ici](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) , au chapitre 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>Partage NFS dans les installations SAP distribuées
Si vous avez une installation distribuée--par exemple, où vous souhaitez la base de données tooinstall hello et que vous hello des serveurs d’applications SAP dans les machines virtuelles distinctes--vous pouvez partagent hello /sapmnt répertoire via le système NFS (Network File). Si vous avez des problèmes avec les étapes d’installation hello après avoir créé hello pour /sapmnt de partage NFS, vérifiez toosee si « no_root_squash » est définie pour le partage de hello.

## <a name="logical-volumes"></a>Volumes logiques
Bonjour passées si nécessaires un gros volume logique sur plusieurs disques de données Azure (par exemple, pour hello SAP de base de données), il était recommandé toouse mdadm comme gestionnaire de volume logique n’a pas été entièrement validé encore sur Azure. toolearn tooset RAID Linux sur Azure à l’aide de mdadm, voir [configurer le logiciel RAID sur Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bonjour attendant depuis le début de mai 2016 également Gestionnaire de volume logique est entièrement pris en charge sur Azure et peut être utilisé comme un autre toomdadm. Pour en savoir plus sur lvm sur Azure, consultez la rubrique [Configurer LVM sur une machine virtuelle Linux dans Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Dépôt SUSE Azure
Si vous avez un problème avec le référentiel de Azure SUSE accès toohello standard, vous pouvez utiliser une simple commande tooreset il. Cela peut se produire si vous créez une image de système d’exploitation privée dans une région Azure, puis copie hello tooa autre région de l’image où vous souhaitez toodeploy nouvelles machines virtuelles qui sont basés sur cette image de système d’exploitation privée. Il suffit d’exécuter hello commande à l’intérieur de hello machine virtuelle suivante :

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Bureau Gnome
Toouse hello Gnome bureau tooinstall un système complet de démonstration SAP à l’intérieur d’une seule machine virtuelle, notamment une interface utilisateur graphique SAP, navigateur et la console de gestion SAP--utilisent cet indicateur de tooinstall sur les images de Azure SLES hello :

   Pour SLES 11 :

   ```
   zypper in -t pattern gnome
   ```

   Pour SLES 12 :

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Prise en charge SAP pour Oracle sur Linux dans le cloud de hello
Il existe une restriction de prise en charge d’Oracle sur Linux dans les environnements virtualisés. Bien que cela n’est pas une rubrique Azure spécifique, il est important toounderstand. SAP ne prend pas en charge Oracle sur SUSE ni Red Hat dans un cloud public comme Azure. toodiscuss cette rubrique, contactez directement le Oracle.

