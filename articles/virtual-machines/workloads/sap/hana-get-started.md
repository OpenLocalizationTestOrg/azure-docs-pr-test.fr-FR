---
title: "Démarrage rapide : installation manuelle d’un système SAP HANA à instance unique sur des machines virtuelles Azure | Microsoft Docs"
description: "Guide de démarrage rapide pour l’installation manuelle d’un système SAP HANA à instance unique sur des machines virtuelles Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Démarrage rapide : installation manuelle d’un système SAP HANA à instance unique sur des machines virtuelles Azure
## <a name="introduction"></a>Introduction
Ce guide vous aide à configurer un système SAP HANA à instance unique sur des machines virtuelles Azure pendant l’installation manuelle de SAP NetWeaver 7.5 et SAP HANA 1.0 SP12. Hello de ce guide porte sur le déploiement de SAP HANA sur Azure. Il ne remplace pas la documentation SAP. 

>[!Note]
>Ce guide décrit des déploiements de SAP HANA sur des machines virtuelles Azure. Pour plus d’informations sur le déploiement de SAP HANA sur des instances de HANA de grande taille, consultez [Utilisation de SAP sur des machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Prérequis
Ce guide suppose que vous maîtrisiez certaines bases d’IaaS (infrastructure as a service), notamment :
 * Comment toodeploy virtuels ou réseaux virtuels via hello portail Azure ou PowerShell.
 * Hello multiplateforme Azure une interface de ligne (CLI), y compris les modèles de hello option toouse JavaScript Objet Notation (JSON).

Ce guide suppose également que vous êtes familiarisé avec :
* SAP HANA et SAP NetWeaver et comment tooinstall les localement.
* L’installation et l’utilisation d’instances d’application SAP HANA et SAP sur Azure.
* Hello procédures et les concepts suivants :
   * Planification du déploiement de SAP sur Azure, y compris la planification du réseau virtuel Azure et l’utilisation du stockage Azure. Consultez [SAP NetWeaver sur machines virtuelles Azure – Guide de planification et d’implémentation](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Déploiement toodeploy façons les principes et les machines virtuelles dans Azure. Consultez [Déploiement de machines virtuelles Azure pour SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Haute disponibilité pour SAP NetWeaver ASC (ABAP SAP Central Services), SCS (SAP Central Services) et ERS (Evaluated Receipt Settlement) sur Azure. Consultez [Haute disponibilité pour SAP NetWeaver sur des machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Pour plus d’informations sur la façon de l’efficacité de tooimprove en tirant parti d’une installation de multi-SID de ASCS/SCS sur Azure. Consultez [Créer une configuration SAP NetWeaver multi-SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Principes de l’exécution de SAP NetWeaver basée sur des machines virtuelles pilotées par Linux dans Azure. Consultez [Exécution de SAP NetWeaver sur des machines virtuelles Microsoft Azure SUSE Linux](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Ce guide fournit des paramètres spécifiques de Linux dans des machines virtuelles Azure et les détails sur comment tooproperly attacher des disques de stockage Azure tooLinux machines virtuelles.

À l’heure actuelle, les machines virtuelles Azure sont certifiées par SAP pour les configurations de montée en puissance SAP HANA uniquement. Les configurations incluant une augmentation de la taille des instances avec une charge de travail SAP HANA ne sont pas encore prises en charge. Pour la haute disponibilité de SAP HANA dans les configurations de montée en puissance, consultez [Haute disponibilité de SAP HANA sur des machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Si vous cherchez tooget une instance de SAP HANA ou S/4HANA ou BW/4HANA système déployé dans le temps très rapide, vous devez envisager l’utilisation de hello de [SAP Cloud application bibliothèque](http://cal.sap.com). Vous trouverez dans [ce guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h) de la documentation sur le déploiement, par exemple, d’un système S/4HANA par le biais de la bibliothèque SAP CAL sur Azure. Vous devez toohave est un abonnement Azure et un utilisateur SAP qui peut être enregistré avec la bibliothèque de matériel de Cloud de SAP.

## <a name="additional-resources"></a>Ressources supplémentaires
### <a name="sap-hana-backup"></a>Sauvegarde SAP HANA
Pour plus d’informations sur la sauvegarde des bases de données SAP HANA sur des machines virtuelles Azure, consultez :
* [Guide de sauvegarde pour SAP HANA sur des machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Sauvegarde SAP HANA sur Azure au niveau fichier](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [Sauvegarde SAP HANA à partir de captures instantanées de stockage](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>Bibliothèque d’appliances cloud SAP
Pour plus d’informations sur l’utilisation de la bibliothèque de matériel de Cloud SAP toodeploy S/4HANA ou BW/4HANA, consultez [SAP de déployer S/4HANA ou BW/4HANA sur Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>Systèmes d’exploitation pris en charge par SAP HANA
Pour plus d’informations sur les systèmes d’exploitation pris en charge par SAP HANA, consultez la [note de support SAP #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E) (SAP HANA : Systèmes d’exploitation pris en charge). Les machines virtuelles Azure ne prennent en charge qu’un sous-ensemble de ces systèmes d’exploitation. Hello des systèmes d’exploitation suivants sont pris en charge toodeploy HANA SAP sur Azure : 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Pour obtenir de la documentation SAP supplémentaire sur SAP HANA et les différents systèmes d’exploitation Linux, consultez :

* [Note de support SAP #171356 relative aux logiciels SAP sur Linux : informations générales](https://launchpad.support.sap.com/#/notes/1984787)
* [Note de support SAP #1944799 relative aux instructions SAP HANA pour l’installation du système d’exploitation SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [Note de support SAP #2205917 relative aux paramètres de système d’exploitation SAP HANA DB recommandés pour SLES 12 ainsi que les application SAP](https://launchpad.support.sap.com/#/notes/2205917/E)
* [Note de support SAP #1984787 relative à SUSE Linux Enterprise Server 12 : notes d’installation](https://launchpad.support.sap.com/#/notes/1984787)
* [Note de support SAP #1391070 relative aux solutions Linux UUID](https://launchpad.support.sap.com/#/notes/1391070)
* [Note de support SAP #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879) (Instructions SAP HANA pour les systèmes d’exploitation Red Hat Enterprise Linux (RHEL))
* [2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E) (SAP HANA DB : Paramètres de système d’exploitation recommandés pour RHEL 7)

### <a name="sap-monitoring-in-azure"></a>Surveillance SAP dans Azure
Pour plus d’informations sur la surveillance SAP dans Azure, consultez :

* [Note de SAP 2191498](https://launchpad.support.sap.com/#/notes/2191498/E) Cette note aborde la « surveillance améliorée » SAP avec des machines virtuelles Linux sur Azure. 
* [Note de SAP 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Cette note contient des informations relatives à SAPOSCOL sur Linux. 
* [Note de SAP 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Cette note aborde des métriques de surveillance clés pour SAP sur Microsoft Azure.

### <a name="azure-vm-types"></a>Types de machines virtuelles Azure
Les types de machines virtuelles Azure et les scénarios de charge de travail pris en charge par SAP utilisés par SAP HANA sont documentés dans [SAP certified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html) (plateforme IaaS certifiée SAP). 

Les types de machine virtuelle Azure qui sont certifiés par SAP pour SAP NetWeaver ou hello S/4HANA couche d’application sont documentées dans [Note SAP 1928533 - Applications SAP sur Azure : les types pris en charge des produits et de la machine virtuelle Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Intégration de Azure SAP-Linux est prise en charge uniquement sur le Gestionnaire de ressources Azure et pas le modèle de déploiement classique hello. 

## <a name="manual-installation-of-sap-hana"></a>Installation manuelle de SAP HANA
Ce guide décrit comment toomanually installer SAP HANA sur des machines virtuelles Azure de deux manières différentes :

* À l’aide de toujours (pas SAP Software Provisioning Manager pris) dans le cadre d’une installation NetWeaver distribuée à l’étape « installer l’instance de base de données » de hello
* À l’aide de hello SAP HANA et base de données Gestionnaire de cycle de vie, HDBLCM, puis l’installation NetWeaver

Vous pouvez également utiliser toujours pas pris tooinstall tous les composants (SAP HANA, serveur d’applications SAP hello et d’instance ASC hello) dans une seule machine virtuelle, comme décrit dans cette [annonce du blog SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Cette option n’est pas décrite dans ce guide de démarrage rapide, mais hello sont des problèmes que vous devez prendre en considération hello identiques.

Avant de commencer une installation, nous vous recommandons de lire hello « Azure de préparation des machines virtuelles pour l’installation manuelle de SAP HANA « section plus loin dans ce guide. Cela vous aidera à prévenir plusieurs erreurs de base qui peuvent survenir lorsque vous utilisez seulement une configuration de machine virtuelle Azure par défaut.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Étapes clés de l’installation de SAP HANA quand vous utilisez SAP SWPM
Cette section répertorie les principales étapes d’hello pour une installation de SAP HANA manuelle, à instance unique lorsque vous utilisez une installation de tooperform de la SAP NetWeaver version distribuée 7.5 toujours pas pris de SAP. les étapes individuelles Hello sont expliquées plus en détail dans les captures d’écran plus loin dans ce guide.

1. Créer un réseau virtuel Azure qui inclut deux machines virtuelles de test.
2. Déployer des machines virtuelles de Azure hello deux avec les systèmes d’exploitation (dans notre exemple, SUSE Linux Enterprise Server (SLES) et SLES pour SAP Applications 12 SP1), selon le modèle de gestionnaire de ressources Azure toohello.
3. Joindre deux Azure standard ou premium storage (par exemple, les disques 75 Go ou 500 Go) de disques toohello application machine virtuelle du serveur.
4. Attachez premium stockage disques toohello HANA DB machine virtuelle du serveur. Pour plus d’informations, consultez hello « Le programme d’installation de disque » plus loin dans ce guide.
5. Selon les exigences de taille ou de débit, attacher plusieurs disques, puis créez des volumes agrégés par bandes à l’aide de la gestion des volumes logiques ou un outil d’administration de plusieurs dispositifs (MDADM) au niveau de hello du système d’exploitation à l’intérieur de hello machine virtuelle.
6. Créer des systèmes de fichiers XFS sur les disques hello attaché ou des volumes logiques.
7. Montez les systèmes de fichiers XFS nouvelle hello au niveau de hello du système d’exploitation. Utilisez un système de fichiers pour tous les logiciels SAP hello. Utilisez hello autre système de fichiers pour le répertoire de /sapmnt hello et les sauvegardes, par exemple. Sur le serveur de base de données SAP HANA hello, montez les systèmes de fichiers XFS hello sur des disques de stockage premium hello en tant que /hana et /usr/sap. Ce processus est un système de fichiers racine tooprevent nécessaire hello, n’est pas volumineux sur des machines virtuelles Azure de Linux, à partir de saturation.
8. Entrez les adresses IP locales hello du test de hello machines virtuelles dans le fichier hello/etc/hosts.
9. Entrez hello **nofail** paramètre dans le fichier hello/etc/fstab.
10. Définissez les paramètres de noyau Linux selon la version du système d’exploitation Linux toohello que vous utilisez. Pour plus d’informations, consultez les notes SAP appropriées hello qui traitent HANA et hello section « Paramètres de noyau » dans ce guide.
11. Ajouter un espace d’échange.
12. Le cas échéant, installez un graphique de bureau sur machines virtuelles de test hello. Sinon, utiliser une installation SAPinst distante.
13. Télécharger les logiciels SAP hello de hello SAP Service Marketplace.
14. Installez hello SAP d’instance sur le serveur d’application hello machine virtuelle.
15. Répertoire de /sapmnt hello partage entre hello tester des machines virtuelles à l’aide de NFS. serveur d’applications Hello machine virtuelle est serveur NFS de hello.
16. Installer l’instance de base de données hello, y compris HANA, à l’aide de toujours pas pris sur la machine virtuelle du serveur de base de données hello.
17. Installer le serveur du principal de l’application hello (PAS) sur le serveur d’applications hello machine virtuelle.
18. Démarrer la console de gestion SAP. Se connecter avec l’interface graphique utilisateur SAP ou HANA Studio, par exemple.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Étapes clés de l’installation de SAP HANA quand vous utilisez HDBLCM
Cette section répertorie les étapes clés de hello pour une installation de SAP HANA manuelle, à instance unique lorsque vous utilisez une installation de tooperform de la SAP NetWeaver version distribuée 7.5 HDBLCM de SAP. les étapes individuelles Hello sont expliquées plus en détail dans les captures d’écran tout au long de ce guide.

1. Créer un réseau virtuel Azure qui inclut deux machines virtuelles de test.
2. Déployer des machines virtuelles Azure deux avec les systèmes d’exploitation (dans notre exemple, SLES et SLES pour SAP Applications 12 SP1) selon le modèle de gestionnaire de ressources Azure toohello.
3. Joindre deux Azure standard ou premium storage (par exemple, les disques 75 Go ou 500 Go) de disques toohello application machine virtuelle du serveur.
4. Attachez premium stockage disques toohello HANA DB machine virtuelle du serveur. Pour plus d’informations, consultez hello « Le programme d’installation de disque » plus loin dans ce guide.
5. Selon les exigences de taille ou de débit, attacher plusieurs disques et créer des volumes agrégés par bandes à l’aide de la gestion des volumes logiques ou un outil d’administration de plusieurs dispositifs (MDADM) au niveau de hello du système d’exploitation à l’intérieur de hello machine virtuelle.
6. Créer des systèmes de fichiers XFS sur les disques hello attaché ou des volumes logiques.
7. Montez les systèmes de fichiers XFS nouvelle hello au niveau de hello du système d’exploitation. Utilisez un système de fichiers pour tous les logiciels SAP hello, utilisez hello autres un pour le répertoire de /sapmnt hello et les sauvegardes, par exemple. Sur le serveur de base de données SAP HANA hello, montez les systèmes de fichiers XFS hello sur des disques de stockage premium hello en tant que /hana et /usr/sap. Ce processus est nécessaire toohelp empêcher le système de fichiers hello racine, qui n’est pas un objet volumineux sur les machines virtuelles Azure Linux, de saturation.
8. Entrez les adresses IP locales hello du test de hello machines virtuelles dans le fichier hello/etc/hosts.
9. Entrez hello **nofail** paramètre dans le fichier hello/etc/fstab.
10. Définissez les paramètres de noyau selon la version du système d’exploitation Linux toohello que vous utilisez. Pour plus d’informations, consultez les notes SAP appropriées hello qui traitent HANA et hello section « Paramètres de noyau » dans ce guide.
11. Ajouter un espace d’échange.
12. Le cas échéant, installez un graphique de bureau sur machines virtuelles de test hello. Sinon, utiliser une installation SAPinst distante.
13. Télécharger les logiciels SAP hello de hello SAP Service Marketplace.
14. Créer un groupe, sapsys, avec groupe ID 1001, sur la machine virtuelle du serveur de base de données HANA hello.
15. Installation de SAP HANA sur la machine virtuelle du serveur de base de données hello à l’aide du Gestionnaire de cycle de vie de base de données HANA (HDBLCM).
16. Installez hello SAP d’instance sur le serveur d’application hello machine virtuelle.
17. Répertoire de /sapmnt hello partage entre hello tester des machines virtuelles à l’aide de NFS. serveur d’applications Hello machine virtuelle est serveur NFS de hello.
18. Installer l’instance de base de données hello, y compris HANA, à l’aide de toujours pas pris sur la machine virtuelle du serveur de base de données HANA hello.
19. Installer le serveur du principal de l’application hello (PAS) sur le serveur d’applications hello machine virtuelle.
20. Démarrer la console de gestion SAP. Se connecter par le biais de l’interface graphique utilisateur SAP ou HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Préparation des machines virtuelles Azure pour une installation manuelle de SAP HANA
Cette section couvre les rubriques suivantes de hello :

* Mises à jour de système d’exploitation
* Configuration des disques
* Paramètres de noyau
* Systèmes de fichiers
* fichier Hello/etc/hosts
* fichier Hello/etc/fstab

### <a name="os-updates"></a>Mises à jour de système d’exploitation
Vérifiez les mises à jour et les correctifs du système d’exploitation Linux avant d’installer des logiciels supplémentaires. En installant un correctif logiciel, vous pouvez être en mesure de tooavoid un appel toohello le support technique.

Assurez-vous d’utiliser :
* SUSE Linux Enterprise Server pour applications SAP ;
* Red Hat Enterprise Linux pour applications SAP ou Red Hat Enterprise Linux pour SAP HANA. 

Si vous n’avez pas encore, inscrire le déploiement de système d’exploitation hello à votre abonnement de Linux à partir du fournisseur de Linux hello. Notez que SUSE a des images de système d’exploitation pour les applications SAP qui incluent déjà des services et qui sont enregistrées automatiquement.

Voici un exemple de recherche pour les correctifs disponibles pour SUSE Linux à l’aide de hello **zypper** commande :

 `sudo zypper list-patches`

En fonction de type hello du problème, les correctifs sont classées par catégorie et gravité. Parmi les valeurs couramment utilisées pour la catégorie figurent **security**, **recommended**, **optional**, **feature**, **document** ou **yast**.
Parmi les valeurs couramment utilisées pour la gravité figurent **critical**, **important**, **moderate**, **low** ou **unspecified**.

Hello **zypper** commande recherche uniquement pour les mises à jour de hello vos packages installés. Par exemple, vous pouvez utiliser cette commande :

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Vous pouvez ajouter le paramètre hello `--dry-run` mise à jour de hello tootest sans réellement mise à jour de système de hello.


### <a name="disk-setup"></a>Configuration des disques
système de fichiers racine Hello un VM Linux sur Azure a une limite de taille. Par conséquent, il est tooan d’espace disque supplémentaire nécessaire tooattach machine virtuelle Azure pour SAP en cours d’exécution. Pour le serveur d’applications SAP machines virtuelles Azure, utilisez hello des disques de stockage standard Azure peut suffire. Toutefois, pour les machines virtuelles Azure SGBD HANA SAP, hello utilisation de disques de stockage Azure Premium pour les implémentations non-production et est obligatoire.

En fonction de hello [besoins de stockage SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), hello suivant la configuration de stockage Azure Premium est suggéré : 

| Référence de la machine virtuelle | RAM |  /hana/data et /hana/log <br /> agrégés avec LVM ou MDADM | /hana/shared | /root volume | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 Go | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Dans la configuration de disque suggérée hello, volume de données HANA hello et volume de journal sont placés sur le même ensemble de disques de stockage Azure premium qui sont agrégées par bandes avec le Gestionnaire de volume logique ou MDADM de hello. Il n’est pas nécessaire toodefine toute redondance RAID de niveau, car Azure Premium Storage conserve trois images de disques hello pour assurer la redondance. toomake assurer que vous configurez un stockage suffisant, consultez hello [besoins de stockage SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) et [SAP HANA serveur Guide d’Installation et mise à jour](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Également envisager de volumes de débit hello autre disque dur virtuel (VHD) de hello disques de stockage premium Azure différents comme documenté dans [stockage Premium à hautes performances et des disques gérés pour les machines virtuelles](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Vous pouvez ajouter que plus de stockage premium disques des machines virtuelles de SGBD toohello HANA pour le stockage des sauvegardes de journaux de transaction ou de la base de données.

Pour plus d’informations sur tooconfigure de deux principaux outils utilisés hello en distribuant, consultez hello suivant des articles :

* [Configuration d’un RAID logiciel sur Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configurer LVM sur une machine virtuelle Linux dans Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Pour plus d’informations sur l’attachement de disques VM tooAzure exécutant Linux en tant qu’un système d’exploitation invité, consultez [ajouter un tooa de disque Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Stockage Azure Premium vous permet de disque toodefine modes de mise en cache. Pour un jeu de hello répartie maintenant /hana/data et /hana/log, la mise en cache du disque doit être désactivée. Pour hello autres volumes (disques), hello mise en cache en mode doit être défini trop**ReadOnly**.

Pour plus d’informations, consultez [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../../storage/common/storage-premium-storage.md) .

toofind exemples de modèles de JSON pour la création de machines virtuelles, accédez trop[modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).
modèle de machine virtuelle-simple-sles Hello est un modèle de base. Il inclut une section de stockage, avec un disque de données de 100 Go supplémentaires. Ce modèle peut être utilisé comme base. Vous pouvez adapter la configuration spécifique du modèle de tooyour hello.

>[!Note]
>Il est disque de stockage Azure hello tooattach importantes à l’aide d’un UUID comme documenté dans [en cours d’exécution de SAP NetWeaver sur machines virtuelles de Microsoft Azure SUSE Linux](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dans l’environnement de test hello, deux disques de stockage standard Azure ont été toohello joint le serveur application SAP machine virtuelle, comme indiqué dans hello suivant capture d’écran. Un seul disque stockées tous les logiciels SAP hello (y compris les NetWeaver 7.5, interface GUI SAP et SAP HANA) pour l’installation. contenu du deuxième disque Hello garantie que suffisamment d’espace libre est disponible pour les exigences supplémentaires (par exemple, les données de sauvegarde et de test) et pour hello /sapmnt active (autrement dit, les profils SAP) toobe est partagé entre toutes les machines virtuelles qui appartiennent toohello paysage SAP même.

![Fenêtre des disques du serveur d’applications SAP HANA montrant deux disques de données et leur taille](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Paramètres de noyau
SAP HANA requiert des paramètres spécifiques à Linux du noyau, ce qui ne font pas partie des images de la galerie Azure standard hello et doivent être définies manuellement. Si vous utilisez SUSE ou Red Hat, les paramètres de hello peuvent être différents. Notes de SAP Hello répertoriées précédemment fournissent des informations sur ces paramètres. Dans des captures d’écran hello indiqué, SUSE Linux 12 SP1 a été utilisé. 

SLES pour SAP Applications 12 GA et SLES pour SP1 de 12 Applications SAP ont un nouvel outil, **adm paramétrées**, que remplace hello ancien **sapconf** outil. Un profil SAP HANA spécial est disponible pour **tuned-adm**. système de hello tootune pour SAP HANA, entrez les informations suivantes de hello en tant qu’utilisateur racine :

   `tuned-adm profile sap-hana`

Pour plus d’informations sur **adm paramétrées**, consultez hello [documentation SUSE sur adm paramétrées](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

Bonjour suivant capture d’écran, vous pouvez voir comment **adm paramétrées** hello modifiée `transparent_hugepage` et `numa_balancing` toohello de selon les valeurs des paramètres de SAP HANA obligatoirement.

![outil d’adm paramétrées Hello modifie les valeurs en fonction des paramètres de SAP HANA toorequired](./media/hana-get-started/image005.jpg)

toomake hello SAP HANA noyau paramètres permanentes, utilisez **grub2** sur SLES 12. Pour plus d’informations sur **grub2**, accédez toohello [Structure de fichier de Configuration](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section Hello documentation de SUSE.

Hello capture d’écran suivante montre comment les paramètres de noyau hello ont été modifiées dans le fichier de configuration hello et ensuite compilées à l’aide de **grub2-mkconfig**:

![Paramètres de noyau modifié dans le fichier de configuration hello et compilé à l’aide de grub2-mkconfig](./media/hana-get-started/image006.jpg)

Une autre option est de paramètres de hello toochange à l’aide de YaST et hello **chargeur de démarrage** > **noyau paramètres** paramètres :

![onglet Paramètres du chargeur de démarrage YaST Hello noyau paramètres](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Systèmes de fichiers
Hello capture d’écran suivante montre deux systèmes de fichiers qui ont été créées sur le serveur d’applications hello SAP VM sur deux disques de stockage standard Azure attaché hello. Les deux systèmes de fichiers sont de type XFS et sont montées trop/données et /sapsoftware.

Il n’est pas obligatoire toostructure vos systèmes de fichiers de cette façon. Vous disposez d’autres options de structuration de l’espace disque hello. élément le plus important Hello est un système de fichiers racine tooprevent hello du manque d’espace libre.

![Deux systèmes de fichiers créés sur le serveur d’applications SAP hello machine virtuelle](./media/hana-get-started/image008.jpg)

Concernant hello VM de base de données SAP HANA, lors d’une installation de base de données, lorsque vous utilisez SAPinst (toujours pas pris) et hello **classique** option d’installation, tout est installé sous /hana et /usr/sap. Hello par défaut pour la sauvegarde de journal de SAP HANA hello se trouve sous /usr/sap. Là encore, car il est important de tooprevent hello racine du manque d’espace de stockage, assurez-vous qu’il est suffisamment d’espace libre sous /hana et /usr/sap avant d’installer SAP HANA à l’aide de toujours pas pris.

Pour obtenir une description de la disposition du système de fichiers standard hello de SAP HANA, consultez hello [SAP HANA serveur Guide d’Installation et mise à jour](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Systèmes de fichiers supplémentaires créés sur le serveur d’applications SAP hello machine virtuelle](./media/hana-get-started/image009.jpg)

Lorsque vous installez SAP NetWeaver sur SLES/SLES standard pour l’image de la galerie Azure de 12 Applications SAP, un message s’affiche indiquant que l’il n’existe aucun espace d’échange, comme indiqué dans hello suivant capture d’écran. toodismiss ce message, vous pouvez ajouter manuellement un fichier d’échange à l’aide de **jj**, **mkswap**, et **swapon**. toolearn, recherchez « Ajout d’un fichier d’échange manuellement « Bonjour [Using hello YaST partitionneur](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section Hello documentation de SUSE.

Une autre option consiste tooconfigure d’espace d’échange à l’aide de l’agent Linux VM de hello. Pour plus d’informations, consultez hello [Guide de l’utilisateur l’Agent Linux Azure](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Message contextuel indiquant que l’espace d’échange est insuffisant](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>fichier Hello/etc/hosts
Avant de commencer tooinstall SAP, veillez à qu'inclure les noms d’hôte hello et les adresses IP de hello machines virtuelles SAP dans le fichier/etc/hosts de hello. Déployer des machines virtuelles SAP hello tous dans un même réseau virtuel Azure et ensuite utiliser les adresses IP internes hello, comme illustré ici :

![Les noms d’hôte et les adresses IP des machines virtuelles SAP de hello répertoriés dans le fichier/etc/hosts de hello](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>fichier Hello/etc/fstab

Il est utile de tooadd hello **nofail** fichier de paramètres toohello fstab. De cette manière, si une erreur survient avec des disques hello, hello machine virtuelle ne soit pas bloquée dans le processus de démarrage hello. Mais n’oubliez pas que l’espace disque supplémentaire n’est peut-être pas disponible, les processus système de fichiers racine hello peuvent remplir. Si /hana est manquant, SAP HANA ne démarrera pas.

![Ajouter le fichier fstab toohello hello nofail paramètre](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Bureau graphique GNOME sur SLES 12/SLES for SAP Applications 12
Cette section couvre les rubriques suivantes de hello :

* Installation de bureau GNOME hello et xrdp sur SLES 12/SLES 12 des Applications SAP
* Exécution de la console de gestion SAP basée sur Java avec Firefox sur SLES 12/SLES for SAP Applications 12

Vous pouvez également utiliser des alternatives telles que Xterminal ou VNC (non décrites dans ce guide).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Installation de bureau GNOME hello et xrdp sur SLES 12/SLES 12 des Applications SAP
Si vous avez un arrière-plan de Windows, vous pouvez utiliser un graphique de bureau directement dans hello SAP les machines virtuelles Linux toorun Firefox, SAPinst, interface GUI SAP, SAP MC ou HANA Studio et vous connecter facilement toohello machine virtuelle via hello protocole RDP (Remote Desktop) à partir d’un ordinateur Windows. Dépend de vos stratégies d’entreprise sur l’ajout d’interfaces graphiques utilisateur les systèmes Linux basée tooproduction et non de production, vous pouvez tooinstall GNOME sur votre serveur. bureau GNOME tooinstall hello sur un Azure SLES 12/SLES pour la machine virtuelle de SAP Applications 12 :

1. Installer le bureau GNOME hello en hello commande (par exemple, dans une fenêtre PuTTY) suivante :

   `zypper in -t pattern gnome-basic`

2. Installez xrdp tooallow un toohello connexion VM via RDP :

   `zypper in xrdp`

3. Modifier /etc/sysconfig/windowmanager et définissez hello par défaut fenêtre Gestionnaire tooGNOME :

   `DEFAULT_WM="gnome"`

4. Exécutez **commande chkconfig** toomake assurer que xrdp démarre automatiquement après un redémarrage :

   `chkconfig -level 3 xrdp on`

5. Si vous avez un problème avec la connexion RDP de hello, essayez toorestart (à partir d’une fenêtre de PuTTY, par exemple) :

   `/etc/xrdp/xrdp.sh restart`

6. Si un redémarrage xrdp mentionné dans hello précédente étape ne fonctionne pas, recherchez un fichier .pid :

   `check /var/run` 

   Recherchez `xrdp.pid`. Si vous trouvez, supprimez-le et recommencez l’opération toorestart.

### <a name="starting-sap-mc"></a>Démarrage de la console de gestion SAP
Après avoir installé le bureau GNOME hello, démarrage hello graphique basée sur Java de SAP MC de Firefox lors de l’exécution dans un Azure SLES 12/SLES pour la machine virtuelle de SAP Applications 12 peut afficher une erreur en raison de hello manquant Java-navigateur plug-in.

Bonjour Bonjour de toostart URL SAP MC est `<server>:5<instance_number>13`.

Pour plus d’informations, consultez [départ hello Web basée sur une Console de gestion SAP](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Hello capture d’écran suivante montre hello des message d’erreur qui s’affiche lorsque hello Java-navigateur plug-in est manquant :

![Message d’erreur indiquant que le plug-in de navigateur Java est manquant](./media/hana-get-started/image013.jpg)

Problème de hello toosolve unidirectionnelle est hello tooinstall manquant plug-in à l’aide de YaST, comme indiqué dans hello suivant capture d’écran :

![À l’aide de tooinstall YaST manquant plug-in](./media/hana-get-started/image014.jpg)

Lorsque vous entrez de nouveau hello URL SAP de la Console de gestion, un message s’affiche vous demandant vous tooactivate hello plug-in :

![Boîte de dialogue demandant l’activation du plug-in](./media/hana-get-started/image015.jpg)

Un message d’erreur concernant un fichier manquant, à savoir javafx.properties, peut également s’afficher. Il s’agit d’exigence toohello connexes d’Oracle Java 1.8 7.4 d’interface utilisateur graphique SAP. (Consultez la [note de SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Hello version IBM Java, ni package d’openjdk hello remis avec SLES/SLES 12 d’Applications SAP comprend le fichier de javafx.properties nécessaires de hello. solution de Hello est toodownload et installer Java SE 8 à partir d’Oracle.

Pour plus d’informations sur un problème similaire avec openjdk sur openSUSE, consultez le thème de discussion hello [Java de 7.4 d’interface utilisateur graphique SAP pour openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Installation manuelle de SAP HANA : SWPM
série Hello de captures d’écran de cette section montre hello principales étapes de l’installation de SAP NetWeaver 7.5 et SAP HANA SP12 lorsque vous utilisez toujours pas pris (SAPinst). Dans le cadre d’une installation NetWeaver 7.5, toujours pas pris peut également installer des base de données hello HANA en tant qu’une seule instance.

Dans un environnement de test, nous avons installé un seul serveur d’application ABAP (Advanced Business Application Programming). Comme indiqué dans hello suivant capture d’écran, nous avons utilisé hello **système distribués** option tooinstall hello ASC et instances de serveur principal de l’application dans une machine virtuelle Azure et SAP HANA en tant que système de base de données hello dans une autre machine virtuelle de Azure.

![ASC et instances de serveur principal de l’application installés à l’aide d’option de système distribués hello](./media/hana-get-started/image012.jpg)

Une fois d’instance ASC hello est installé sur le serveur d’application hello machine virtuelle et est défini trop » vert « Bonjour Console de gestion de SAP (illustrée dans hello suivant capture d’écran), hello /sapmnt répertoire (y compris le répertoire de profils SAP hello) doit être partagé avec la machine virtuelle du serveur de base de données SAP HANA hello. étape d’installation Hello DB a besoin d’accéder à des informations de toothis. l’accès de Hello meilleure manière tooprovide est toouse NFS, qui peuvent être configurés à l’aide de YaST.

![D’instance ASC SAP Management Console montrant hello installé sur le serveur d’application hello VM et définissez trop « vert »](./media/hana-get-started/image016.jpg)

Sur le serveur application hello VM, hello/sapmnt active doit être partagé via NFS à l’aide de hello **rw** et **no_root_squash** options. Hello valeurs par défaut sont **ro** et **root_squash**, ce qui peut entraîner des tooproblems lorsque vous installez l’instance de base de données hello.

![Partage de répertoire de /sapmnt hello via NFS à l’aide des options de rw et no_root_squash hello](./media/hana-get-started/image017b.jpg)

Comme le montre la capture d’écran suivante de hello, partage de /sapmnt hello à partir de la machine virtuelle du serveur hello application doit être configuré sur la machine virtuelle du serveur de base de données SAP HANA hello à l’aide de **Client NFS** (et YaST).

![partage de /sapmnt Hello configuré à l’aide du Client NFS](./media/hana-get-started/image018b.jpg)

installation de tooperform un 7.5 NetWeaver distribuée (**Instance de base de données**), comme indiqué dans hello suivant capture d’écran, connectez-vous au serveur de base de données SAP HANA toohello machine virtuelle et démarrer toujours pas pris.

![Installation d’une instance de base de données en vous connectant machine virtuelle du serveur de base de données SAP HANA toohello et en commençant toujours pas pris](./media/hana-get-started/image019.jpg)

Après avoir sélectionné **classique** installation et support d’installation toohello hello chemin d’accès, entrez un SID de la base de données, nom d’hôte hello, du nombre d’instances hello et mot de passe administrateur hello de base de données système.

![page de Hello SAP HANA base de données système administrateur connectez-vous](./media/hana-get-started/image035b.jpg)

Entrez le mot de passe de hello pour le schéma DBACOCKPIT hello :

![zone d’entrée de mot de passe de Hello pour le schéma DBACOCKPIT hello](./media/hana-get-started/image036b.jpg)

Entrez une question de mot de passe hello SAPABAP1 schéma :

![Entrez une question de mot de passe hello SAPABAP1 schéma](./media/hana-get-started/image037b.jpg)

Une fois que chaque tâche est terminée, une coche verte s’affiche phase tooeach suivante du processus d’installation de base de données de hello. message de type Hello « d’exécution de... Database Instance has completed. » (L’exécution de... Instance de base de données est terminée.) s’affiche.

![Fenêtre de la tâche terminée avec un message de confirmation](./media/hana-get-started/image023.jpg)

Après l’installation réussie, hello Console de gestion SAP doit également afficher l’instance de base de données hello en tant que « vert » et afficher la liste complète des processus SAP HANA (hdbindexserver, hdbcompileserver et ainsi de suite) hello.

![Fenêtre de la console de gestion SAP montrant la liste des processus SAP HANA](./media/hana-get-started/image024.jpg)

Hello capture d’écran suivante montre les parties hello de structure de fichiers hello sous le répertoire /hana/shared hello toujours pas pris créé au cours de l’installation de HANA de hello. Étant donné qu’aucune option toospecify un autre chemin d’accès, il est important toomount l’espace disque supplémentaire sous le répertoire /hana hello hello installation de SAP HANA à l’aide de toujours pas pris. Cela empêche le système de fichiers racine hello de manque d’espace libre.

![structure de fichier Hello /hana/shared répertoire créé pendant l’installation de HANA](./media/hana-get-started/image025.jpg)

Cette capture d’écran montre la structure des fichiers du répertoire de /usr/sap hello hello :

![structure de fichiers du répertoire Hello /usr/sap](./media/hana-get-started/image026.jpg)

Hello dernière étape d’installation de ABAP hello distribué est l’instance de serveur principal de l’application tooinstall hello :

![Instance de serveur principal de l’application ABAP installation montrant comme étape finale de hello](./media/hana-get-started/image027b.jpg)

Une fois que l’instance de serveur principal de l’application hello et l’interface utilisateur graphique SAP sont installés, utilisez hello **DBA Cockpit** tooconfirm transaction qui hello installation de SAP HANA terminée correctement :

![Fenêtre DBA Cockpit confirmant la réussite de l’installation](./media/hana-get-started/image028b.jpg)

En tant que dernière étape, vous souhaitez toofirst installation HANA Studio dans le serveur d’applications SAP hello machine virtuelle et puis connectez-vous instance SAP HANA toohello qui s’exécute sur une machine virtuelle du serveur de base de données hello :

![L’installation de SAP HANA Studio dans le serveur d’applications SAP hello machine virtuelle](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Installation manuelle de SAP HANA : HDBLCM
Dans Ajout tooinstalling SAP HANA en tant que partie d’une installation distribuée en utilisant toujours pas pris, vous pouvez installer tout d’abord, hello HANA autonome à l’aide de HDBLCM. Vous pouvez ensuite installer SAP NetWeaver 7.5, par exemple. captures d’écran Hello dans cette section montrent comment ce processus fonctionne.

Pour plus d’informations sur l’outil de HANA HDBLCM de hello, consultez :

* [En choisissant l’option hello Correct HDBLCM de HANA SAP pour votre tâche](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools (Outils de gestion du cycle de vie SAP HANA)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide (Guide d’installation et de mise à jour du serveur SAP HANA)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

paramètre d’ID pour hello du groupe de problèmes tooavoid avec une valeur par défaut `\<HANA SID\>adm user` (créée par l’outil HDBLCM hello), définir un nouveau groupe appelé `sapsys` à l’aide des ID de groupe `1001` avant d’installer SAP HANA via HDBLCM :

![Nouveau groupe « sapsys » défini avec l’ID de groupe 1001](./media/hana-get-started/image030.jpg)

Lorsque vous démarrez hello HDBLCM première fois, un menu Démarrer simple s’affiche. Sélectionner un élément 1, **installer le nouveau système**, comme indiqué dans hello suivant capture d’écran :

![Option de « Installer le nouveau système » dans la fenêtre de démarrage hello HDBLCM](./media/hana-get-started/image031.jpg)

Hello capture d’écran suivante affiche toutes les options de clé hello que vous avez sélectionné précédemment.

> [!IMPORTANT]
> Les répertoires nommés pour les journaux HANA et volumes de données, ainsi que les chemin d’installation de hello (/ hana/partagé dans cet exemple) et /usr/sap, ne doivent pas faire partie du système de fichiers racine hello. Ces répertoires appartiennent à des disques de données Azure toohello qui ont été attachée toohello VM (décrite dans la section hello « disque setup »). Cette approche permet d’empêcher l’exécution en dehors de l’espace de système de fichiers racine hello. Bonjour suivant capture d’écran, vous pouvez voir qu’administrateur système HANA hello a l’ID d’utilisateur `1005` et fait partie de hello `sapsys` groupe (ID `1001`) qui a été définie avant l’installation de hello.

![Liste de tous les composants SAP HANA clés sélectionnés précédemment](./media/hana-get-started/image032.jpg)

Vous pouvez vérifier hello `\<HANA SID\>adm user` (`azdadm` Bonjour suivant capture d’écran) détails dans le répertoire/etc/mot de passe de hello :

![HANA \<HANA SID\>détails de l’utilisateur adm répertoriées dans le répertoire/etc/mot de passe de hello](./media/hana-get-started/image033.jpg)

Après l’installation de SAP HANA à l’aide de HDBLCM, vous pouvez voir la structure du fichier hello dans SAP HANA Studio, comme indiqué dans hello suivant capture d’écran de. schéma de SAPABAP1 Hello, qui inclut toutes les tables de SAP NetWeaver hello, n’est encore disponible.

![Structure des fichiers SAP HANA dans SAP HANA Studio](./media/hana-get-started/image034.jpg)

Après avoir installé SAP HANA, vous pouvez installer SAP NetWeaver par-dessus. Comme indiqué dans hello suivant capture d’écran, installation de hello a été effectuée comme une installation distribuée en utilisant toujours pas pris (comme décrit dans la section précédente de hello). Lorsque vous installez l’instance de base de données hello en utilisant toujours pas pris, vous entrez hello mêmes données à l’aide de HDBLCM (par exemple, nom d’hôte, HANA SID et numéro d’instance). Toujours pas pris utilise installation HANA existante de hello et ajoute d’autres schémas.

![Installation distribuée effectuée à l’aide de SWPM](./media/hana-get-started/image035b.jpg)

Hello capture d’écran suivante montre étape d’installation hello toujours pas pris dans lequel vous entrez des données sur le schéma DBACOCKPIT hello :

![étape d’installation Hello toujours pas pris dans lequel les données de schéma DBACOCKPIT sont entrées](./media/hana-get-started/image036b.jpg)

Entrez les données sur le schéma de SAPABAP1 hello :

![Entrer des données sur le schéma de SAPABAP1 hello](./media/hana-get-started/image037b.jpg)

Hello installation de l’instance de base de données toujours pas pris fin, vous pouvez voir le schéma de SAPABAP1 hello dans SAP HANA Studio :

![schéma Hello SAPABAP1 dans SAP HANA Studio](./media/hana-get-started/image038b.jpg)

Enfin, une fois que le serveur d’applications SAP hello et les installations de l’interface utilisateur graphique SAP sont terminées, vous pouvez vérifier instance de base de données HANA hello à l’aide de hello **DBA Cockpit** transaction :

![instance de base de données HANA Hello vérifiées avec hello transaction du Cockpit de DBA](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Téléchargement des logiciels SAP
Vous pouvez télécharger le logiciel à partir de hello SAP Service Marketplace, comme indiqué dans hello suivant des captures d’écran.

Télécharger NetWeaver 7.5 pour Linux/HANA :

 ![Fenêtre Installation and Upgrade (Installation et mise à niveau) de SAP Service pour le téléchargement de NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Télécharger HANA SP12 Platform Edition :

 ![Fenêtre Installation and Upgrade (Installation et mise à niveau) de SAP Service pour le téléchargement de HANA SP12 Platform Edition](./media/hana-get-started/image002.jpg)

