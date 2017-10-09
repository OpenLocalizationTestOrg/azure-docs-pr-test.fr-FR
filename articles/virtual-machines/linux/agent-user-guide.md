---
title: "aaaAzure présentation de l’Agent de machine virtuelle Linux | Documents Microsoft"
description: "Découvrez comment tooinstall et configurer le Linux Agent (waagent) toomanage interaction de votre machine virtuelle avec le contrôleur de structure Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Présentation et utilisation hello Linux Agent Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introduction
Hello Microsoft Azure Linux (waagent) géré par l’Agent Linux et FreeBSD approvisionnement et machine virtuelle interaction avec hello contrôleur de structure Azure. Il fournit hello suivant de fonctionnalités pour les déploiements de Linux et FreeBSD IaaS :

> [!NOTE]
> Consultez la rubrique hello Azure Linux agent [Lisez-moi](https://github.com/Azure/WALinuxAgent/blob/master/README.md) pour plus d’informations.
> 
> 

* **Approvisionnement d’image**
  
  * Création d'un compte d'utilisateur
  * Configuration des types d'authentification SSH
  * Déploiement des clés publiques et des paires de clés SSH
  * Nom du paramètre hello hôte
  * Plateforme de publication hello hôte nom toohello DNS
  * Toohello plateforme de création de rapports SSH hôte clé empreinte digitale
  * Gestion du disque de ressources
  * Mise en forme et le montage du disque de ressources hello
  * Configuration de l'espace d'échange
* **Mise en réseau**
  
  * Gère les itinéraires tooimprove la compatibilité avec les serveurs DHCP de plateforme
  * Garantit la stabilité hello du nom de l’interface réseau hello
* **Noyau**
  
  * Configure la topologie NUMA virtuelle (désactivée pour le noyau < à 2.6.37)
  * Consommation de l'entropie Hyper-V pour /dev/random
  * Configure les délais d’expiration SCSI pour appareil de racine hello (qui peut être à distance)
* **Diagnostics**
  
  * Port de console redirection toohello série
* **Déploiements SCVMM**
  
  * Détecte et amorce l’agent VMM de hello pour Linux lors de l’exécution dans un environnement de System Center Virtual Machine Manager 2012 R2
* **Extension de machine virtuelle**
  
  * Injecter des composants créés par Microsoft et partenaires dans automation de logiciels et la configuration de tooenable Linux VM (IaaS)
  * Implémentation de référence de l’extension de machine virtuelle à l’adresse [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Communication
Hello flux d’informations à partir de l’agent de hello plateforme toohello se produit via deux canaux :

* Un DVD attaché au moment du démarrage pour les déploiements IaaS. Ce DVD comprend un fichier de configuration conformes OVF qui inclut toutes les informations de configuration autre que les paires de clés hello réel SSH.
* Un point de terminaison TCP exposer une API REST utilisée tooobtain déploiement et configuration de la topologie.

## <a name="requirements"></a>Configuration requise
Hello systèmes suivants ont été testées et sont connues toowork avec hello Linux Agent Azure :

> [!NOTE]
> Cette liste peut différer de la liste officielle de hello des systèmes pris en charge sur hello plateforme Microsoft Azure, comme décrit ici : [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Autres systèmes pris en charge :

* FreeBSD 10+ (agent Azure Linux v2.0.10+)

l’agent de Linux Hello dépend de certains packages de système dans l’ordre toofunction correctement :

* Python 2.6+
* OpenSSL 1.0+
* OpenSSH 5.3+
* Utilitaires de système de fichiers : sfdisk, fdisk, mkfs, séparés
* Outils de mot de passe : chpasswd, sudo
* Outils de traitement de texte : sed, grep
* Outils réseau : ip-route
* Prise en charge du noyau pour le montage de systèmes de fichiers UDF.

## <a name="installation"></a>Installation
Installation à l’aide d’un fichier RPM ou un package DEB à partir d’un référentiel de packages de distribution de votre est la méthode hello préféré de l’installation et la mise à niveau hello Linux Agent Azure. Tous les hello [approuvée des fournisseurs de distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) intégrer leurs images et des référentiels du package de l’agent Azure Linux hello.

Consultez la documentation du toohello Bonjour [référentiel Linux Agent Azure sur GitHub](https://github.com/Azure/WALinuxAgent) pour les options d’installation avancées, telles que l’installation à partir d’emplacements source ou toocustom ou de préfixes.

## <a name="command-line-options"></a>Options de la ligne de commande
### <a name="flags"></a>Indicateurs
* verbose : accroît le niveau de détail de la commande spécifiée.
* force : ignore la confirmation interactive de certaines commandes.

### <a name="commands"></a>Commandes
* aide : répertorie les commandes hello pris en charge et les indicateurs.
* annulation du déploiement : tentative de système de hello tooclean et adapté à la reconfiguration. Cette opération supprimé suivant de hello :
  
  * Toutes les clés d’hôte SSH (si Provisioning.RegenerateSshHostKeyPair est « y » dans le fichier de configuration hello)
  * la configuration de Nameserver dans /etc/resolv.conf ;
  * Mot de passe racine à partir / etc/shadow (si Provisioning.DeleteRootPassword est « y » dans le fichier de configuration hello)
  * les baux du client DHCP mis en cache.
  * Réinitialise héberge nom toolocalhost.localdomain

> [!WARNING]
> Mise hors service ne garantit pas que cette image hello est désactivée de toutes les informations sensibles et appropriée pour la redistribution.
> 
> 

* Annuler le déploiement + utilisateur : effectue tout sous - deprovision (ci-dessus) et également supprime hello dernier compte d’utilisateur configuré (obtenu à partir de /var/lib/waagent) et les données associées. Ce paramètre est utilisé pour annuler l'approvisionnement d'une image qui a été précédemment approvisionnée sur Azure en vue d'être capturée et réutilisée.
* version : affiche la version de waagent hello
* serialconsole : Configure GRUB toomark ttyS0 (hello le premier port série) en tant que console de démarrage hello. Cela garantit que les journaux du démarrage du noyau sont envoyés de port série toothe et sont accessibles pour le débogage.
* démon : exécuté waagent comme une interaction de toomanage démon avec la plateforme de hello. Cet argument est toowaagent spécifié dans le script d’initialisation waagent hello.
* start : exécute waagent en arrière-plan

## <a name="configuration"></a>Configuration
Un fichier de configuration (/ etc/waagent.conf) contrôles hello actions de waagent. Un exemple de fichier de configuration est affiché ci-dessous :

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Hello que différentes options de configuration sont décrites en détail ci-dessous. Elles sont de trois types : Boolean, String ou Integer. options de configuration booléenne de Hello peuvent être spécifiées en tant que « y » ou « n ». Bonjour mot clé spécial « None » peut être utilisé pour une chaîne type entrées de configuration comme indiqué ci-dessous.

**Provisioning.Enabled :**  
Type : booléen  
Par défaut : y

Cela permet de hello utilisateur tooenable ou désactiver hello configuration des fonctionnalités de l’agent de hello. Les valeurs valides sont « y » ou « n ». Si la configuration est désactivée, clés d’hôte et d’utilisateur SSH dans l’image de hello sont conservés et toute configuration spécifiée Bonjour Azure API de configuration est ignorée.

> [!NOTE]
> Hello `Provisioning.Enabled` trop « n » sur les Images de Cloud Ubuntu qui utilisent cloud-init pour la configuration de paramètres par défaut.
> 
> 

**Provisioning.DeleteRootPassword :**  
Type : booléen  
Par défaut : n

Si set, mot de passe racine hello dans le fichier de clichés instantanés/etc/hello est effacé au cours de hello le processus d’approvisionnement.

**Provisioning.RegenerateSshHostKeyPair :**  
Type : booléen  
Par défaut : y

Si l’ensemble, tous les SSH hôte paires de clés (ecdsa, dsa et rsa) est supprimé lors de hello processus à partir d’etc/ssh/de configuration. Une nouvelle paire de clés unique est générée.

le type de chiffrement Hello pour la nouvelle paire de clés de hello est configurable par hello Provisioning.SshHostKeyPairType entrée. Notez que certaines distributions recréera les paires de clés SSH pour les types de chiffrement manquant lorsque le démon SSH hello redémarre (par exemple, après un redémarrage).

**Provisioning.SshHostKeyPairType :**  
Type : string  
Par défaut : rsa

Type d’algorithme de chiffrement tooan est pris en charge par le démon SSH hello sur l’ordinateur virtuel de hello celle-ci peut être définie. les valeurs Hello généralement prises en charge sont « rsa », « dsa » et « ecdsa ». Notez que « putty.exe » sur Windows ne prend pas en charge « ecdsa ». Par conséquent, si vous envisagez de toouse putty.exe Windows tooconnect tooa déploiement Linux, utilisez « rsa » ou « dsa ».

**Provisioning.MonitorHostName :**  
Type : booléen  
Par défaut : y

Si défini, waagent analysez hello Linux virtual machine pour les modifications de nom d’hôte (tel que renvoyé par la commande de « hostname » hello) et mettre à jour automatiquement la configuration du réseau dans la modification de hello hello image tooreflect hello. Dans le nom de l’ordre toopush hello modifier les serveurs DNS toohello, mise en réseau sera redémarré dans la machine virtuelle de hello. La connexion Internet est alors brièvement interrompue.

**Provisioning.DecodeCustomData**  
Type : booléen  
Par défaut : n

Si ce paramètre est défini, waagent décodera CustomData en Base64.

**Provisioning.ExecuteCustomData**  
Type : booléen  
Par défaut : n

Si ce paramètre est défini, waagent exécute CustomData après l’approvisionnement.

**Provisioning.PasswordCryptId**  
Type : chaîne  
Par défaut : 6

Algorithme utilisé par crypt lors de la génération du hachage de mot de passe.  
 1 - MD5  
 2 a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Type : chaîne  
Par défaut : 10

Longueur de la chaîne salt aléatoire utilisée lors de la génération du hachage de mot de passe.

**ResourceDisk.Format :**  
Type : booléen  
Par défaut : y

Si la valeur, disque de ressources hello fournie par la plateforme de hello sera formaté et monté par waagent si le type de système de fichiers hello demandé par l’utilisateur hello dans « ResourceDisk.Filesystem » n’est pas « ntfs ». Une partition unique de type Linux (83) sera disponible sur le disque de hello. Notez que cette partition n'est pas formatée si elle ne peut pas être correctement montée.

**ResourceDisk.Filesystem :**  
Type : string  
Par défaut : ext4

Cela spécifie le type de système de fichiers hello pour le disque de ressources hello. Les valeurs prises en charge diffèrent selon la distribution Linux. Si la chaîne de hello est X, puis mkfs. X doit être présent sur l’image de Linux hello. Les images SLES 11 doivent généralement utiliser « ext3 ». Les images FreeBSD doivent utiliser « ufs2 » ici.

**ResourceDisk.MountPoint :**  
Type : string  
Par défaut : /mnt/resource 

Cela spécifie le chemin d’accès hello à laquelle le disque de ressources hello est monté. Notez que le disque ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.

**ResourceDisk.MountOptions**  
Type : string  
Par défaut : aucun

Spécifie le disque montage options toobe passé toohello mount -o commande. Les valeurs de cette liste sont séparées par des virgules, par exemple 'nodev,nosuid'. Pour plus d’informations, consultez mount(8).

**ResourceDisk.EnableSwap :**  
Type : booléen  
Par défaut : n

Si défini, un fichier d’échange (/ fichier d’échange) est créé sur le disque de ressources hello et ajouté l’espace d’échange système toohello.

**ResourceDisk.SwapSizeMB :**  
Type : entier  
Par défaut : 0

taille de Hello hello du fichier d’échange en mégaoctets.

**Logs.Verbose :**  
Type : booléen  
Par défaut : n

Si elle est définie, le niveau de détail du journal est optimisé. Waagent journaux too/var/log/waagent.log et tire parti des fonctionnalités toorotate journaux de hello système logrotate.

**OS.EnableRDMA**  
Type : booléen  
Par défaut : n

Si la valeur, hello agent essayez tooinstall et ensuite charger un pilote de noyau RDMA qui correspond à la version de hello du microprogramme hello sur hello matériel sous-jacent.

**OS.RootDeviceScsiTimeout :**  
Type : entier  
Par défaut : 300

Cela configure le délai d’attente de hello SCSI en secondes sur les lecteurs de disque et les données hello du système d’exploitation. Si la valeur n’est pas définie, les valeurs par défaut sont utilisées par le système hello.

**OS.OpensslPath :**  
Type : string  
Par défaut : aucun

Cela peut être utilisé toospecify un chemin alternatif pour toouse binaire d’openssl hello pour les opérations de chiffrement.

**HttpProxy.Host, HttpProxy.Port**  
Type : string  
Par défaut : aucun

Si, l’agent de hello utilisera ce proxy server tooaccess hello internet. 

## <a name="ubuntu-cloud-images"></a>Images cloud Ubuntu
Notez que Ubuntu Cloud Images utilisent [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform nombreuses tâches de configuration qui seraient sinon gérés par hello Linux Agent Azure.  Veuillez noter hello suivant différences :

* **Provisioning.Enabled** trop « n » sur les Images de Cloud Ubuntu qui utilisent tooperform cloud-init des tâches de configuration par défaut.
* Hello, paramètres de configuration suivants ont aucun effet sur Ubuntu Cloud Images qui utilisent cloud-init toomanage hello ressources disque et échange d’espace :
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Consultez hello après le point de montage de disque de ressources ressources tooconfigure hello et échange d’espace sur les Images de Cloud Ubuntu lors de la configuration :
  
  * [Wiki Ubuntu : Configurer les partitions d’échange](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Injection de données personnalisées dans une machine virtuelle Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

