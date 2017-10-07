---
title: "préparer l’aaaPortal StorSimple Virtual Array | Documents Microsoft"
description: "Toodeploy didacticiel premier tableau de virtuel StorSimple implique la préparation hello portail Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Déployer des StorSimple Virtual Array - préparer hello portail Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Vue d'ensemble

Il s’agit hello premier article de hello série de didacticiels de déploiement requis toocompletely déployer votre tableau virtuel en tant que serveur de fichiers ou un serveur iSCSI à l’aide du modèle de gestionnaire de ressources hello. Cet article décrit toocreate de préparation requises hello et configurer votre service de gestionnaire de périphériques StorSimple préalable tooprovisioning un tableau virtuel. Cet article contient également des liens out tooa configuration liste de vérification et de configuration de conditions préalables au déploiement.

Vous avez besoin des privilèges toocomplete hello le programme d’installation et configuration de processus administrateur. Nous recommandons de consulter la liste de vérification de configuration hello déploiement avant de commencer. Préparation de portail Hello prend moins de 10 minutes.

les informations de Hello publiées dans cet article s’appliquent déploiement toohello StorSimple virtuels des baies de Bonjour portail Azure et Microsoft Azure Government Cloud.

### <a name="get-started"></a>Prise en main
flux de travail de déploiement Hello se compose de la préparation du portail de hello, configuration d’un tableau virtuel dans votre environnement virtualisé et terminé l’installation de hello. tooget main le déploiement de StorSimple Virtual Array hello en tant que serveur de fichiers ou un serveur iSCSI, vous devez toohello toorefer suivant le tableau des ressources.

#### <a name="deployment-articles"></a>Articles sur le déploiement

toodeploy votre tableau virtuel StorSimple, consultez toohello suivant articles Bonjour prescrit la séquence.

| **#** | **Dans cette étape** | **Procédez comme suit …** | **Et utilisez ces documents.** |
| --- | --- | --- | --- |
| 1. |**Configurer hello portail Azure** |Créez et configurez votre service de gestionnaire de périphériques StorSimple préalable tooprovisioning un tableau virtuel StorSimple. |[Préparer le portail de hello](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Configurer hello Virtual Array** |Pour Hyper-V, configurer et connecter tooa StorSimple Virtual Array sur un système hôte exécutant Hyper-V sur Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. <br></br> <br></br> Pour VMware, configurer et connecter tooa StorSimple Virtual Array sur un système hôte exécutant VMware ESXi 5.5 et versions ultérieures.<br></br> |[Configuration d’un tableau virtuel dans Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Configuration d’un tableau virtuel dans VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Configurer hello Virtual Array** |Pour votre serveur de fichiers, exécuter le programme d’installation initiale, inscrire votre serveur de fichiers StorSimple et terminer l’installation du périphérique hello. Vous pouvez ensuite configurer les partages SMB. <br></br> <br></br> Pour votre serveur iSCSI, exécuter le programme d’installation initiale, inscrire votre serveur d’iSCSI StorSimple et terminer l’installation du périphérique hello. Vous pouvez ensuite configurer les volumes iSCSI. |[Configuration d’un tableau virtuel comme serveur de fichiers](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Configuration d’un virtuel tableau comme serveur iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Vous pouvez maintenant commencer tooset des hello portail Azure.

## <a name="configuration-checklist"></a>Liste de contrôle de la configuration

liste de vérification de configuration Hello décrit les informations de hello que vous avez besoin de toocollect avant de configurer les logiciels hello sur votre tableau virtuel StorSimple. Préparation ces informations à l’avance le temps permet de rationaliser les processus de hello du déploiement de l’appareil StorSimple hello dans votre environnement. Selon que votre StorSimple Virtual Array est déployé en tant que serveur de fichiers ou un serveur iSCSI, vous devez un des hello suivant des listes de contrôle.

* Télécharger hello [StorSimple Virtual Array fichier Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Télécharger hello [StorSimple Virtual Array iSCSI liste de vérification de Configuration serveur](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Composants requis

Vous trouverez hello configuration requise pour votre service de gestionnaire de périphériques StorSimple votre StorSimple Virtual Array et réseau de centre de données hello.

### <a name="for-hello-storsimple-device-manager-service"></a>Pourquoi le service du Gestionnaire de périphériques StorSimple

Avant de commencer, assurez-vous que :

* Vous disposez d’un compte Microsoft doté d’informations d’identification d’accès.
* Vous disposez d’un compte de stockage Microsoft Azure doté d’informations d’identification d’accès.
* Votre abonnement Microsoft Azure devrait être activé pour le service StorSimple Device Manager.

### <a name="for-hello-storsimple-virtual-array"></a>Pourquoi StorSimple Virtual Array

Avant de déployer un tableau virtuel, assurez-vous que :

* Vous avez accès tooa hôte système exécutant Hyper-V sur Windows Server 2008 R2 ou version ultérieure ou VMware (ESXi 5.5 ou version ultérieure) qui peut être utilisé tooa configurer un périphérique.
* système d’hôte Hello est en mesure de toodedicate hello suivant tooprovision de ressources de votre tableau virtuel :
  
  * Un minimum de 4 cœurs.
  * Au moins 8 Go de RAM. Si vous envisagez d’unité de stockage tooconfigure hello virtuelle en tant que serveur de fichiers, 8 Go prend en charge 2 millions de fichiers. Vous avez besoin de 16 Go de RAM toosupport 2-4 millions de fichiers.
  * Une interface réseau.
  * Un disque virtuel de 500 Go pour les données système.

### <a name="for-hello-datacenter-network"></a>Pour le réseau de centre de données hello

Avant de commencer, assurez-vous que :

* réseau Hello dans votre centre de données est configurée conformément aux exigences de mise en réseau hello pour votre appareil StorSimple. Pour plus d’informations, consultez hello [StorSimple Virtual Array requise](storsimple-ova-system-requirements.md).
* Votre instance StorSimple Virtual Array a une bande passante Internet dédiée de 5 Mbits/s (ou plus) disponible à tout moment. La bande passante ne doit pas être partagée avec d’autres applications.

## <a name="step-by-step-preparation"></a>Préparation étape par étape

Utilisez hello suivant tooprepare des instructions pas à votre portail pour hello service du Gestionnaire de périphériques StorSimple.

## <a name="step-1-create-a-new-service"></a>Étape 1 : Création d’un nouveau service

Une seule instance du service de gestionnaire de périphériques StorSimple hello peut gérer plusieurs groupes virtuel StorSimple. Effectuer hello suivant les étapes toocreate une instance de service du Gestionnaire de périphériques StorSimple hello. Si vous avez un toomanage du service Gestionnaire de périphériques StorSimple existant vos réseaux virtuels, ignorez cette étape et passez trop[étape 2 : clé d’inscription Get hello](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service, vous devez toocreate au moins un compte de stockage une fois que vous avez créé un service.
> 
> * Si vous n’avez pas créé un compte de stockage automatiquement, passez trop[configurer un nouveau compte de stockage pour le service de hello](#optional-step-configure-a-new-storage-account-for-the-service) pour obtenir des instructions détaillées.
> * Si vous avez activé la création automatique d’un compte de stockage hello, passez trop[étape 2 : clé d’inscription Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Étape 2 : Obtenir la clé d’inscription hello

Une fois hello service du Gestionnaire de périphériques StorSimple est en cours d’exécution, vous devez clé d’inscription tooget hello. Cette clé est utilisée tooregister et connecter votre appareil StorSimple hello service.

Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> clé d’inscription Hello est tooregister utilisé toutes hello appareils StorSimple le Gestionnaire de périphériques nécessitant le tooregister avec votre service de gestionnaire de périphériques StorSimple.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Étape 3 : Télécharger l’image du tableau virtuel hello

Une fois la clé d’inscription hello, vous devez toodownload hello tableau virtuel approprié image tooprovision un tableau virtuel sur votre système hôte. images de tableau virtuel Hello sont propres au système d’exploitation et peuvent être téléchargées à partir de la page de démarrage rapide de hello Bonjour portail Azure.

> [!IMPORTANT]
> Hello logiciel s’exécutant sur hello StorSimple Virtual Array ne peut être utilisé avec hello service du Gestionnaire de périphériques StorSimple.
> 
> 

Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>image du tableau virtuel hello tooget

1. L’authentification à hello [portail Azure](https://portal.azure.com/). 
2. Bonjour portail Azure, cliquez sur **Parcourir > gestionnaires d’appareil StorSimple**.
3. Sélectionnez un service StorSimple Device Manager existant. Bonjour **le Gestionnaire de périphériques StorSimple** panneau, cliquez sur **Quick Start**. 
4. Cliquez sur hello correspondant toohello image du lien que vous souhaitez toodownload de hello Microsoft Download Center. fichiers d’image Hello sont environ 4,8 Go.
   
   * VHDX pour Hyper-V sur Windows Server 2012 et versions ultérieures
   * VHD pour Hyper-V sur Windows Server 2008 R2 et versions ultérieures
   * VMDK pour VMWare ESXi 5.5 et versions ultérieures
5. Téléchargez et décompressez hello fichier tooa lecteur local, une annotation d’où se trouve le fichier décompressé de hello.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Étape facultative : configurer un nouveau compte de stockage pour le service de hello

Cette étape est facultative et doit être exécutée uniquement si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service.

Si vous avez besoin d’un compte de stockage Azure dans une région différente de toocreate, consultez [comment toocreate un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour obtenir des instructions pas à pas.

Effectuer hello comme suit dans hello [portail Azure](https://ms.portal.azure.com/) sur hello le Gestionnaire de périphériques StorSimple service page tooadd un compte de stockage Microsoft Azure existant.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd une information d’identification du compte de stockage qui a hello même abonnement Azure en tant que service du Gestionnaire de périphériques hello

1. Accédez tooyour service Gestionnaire de périphériques, sélectionnez et double-cliquez dessus. Cette opération ouvre hello **vue d’ensemble** panneau.
2. Sélectionnez **informations d’identification du compte de stockage** dans hello **Configuration** section.
3. Cliquez sur **Add**.
4. Bonjour **ajouter un compte de stockage** panneau, hello suivant :
   
    1. Pour **Abonnement**, sélectionnez **Actuel**.
   
    2. Fournissez le nom hello de votre compte de stockage Azure.
   
    3. Sélectionnez **activer** toocreate un canal sécurisé pour la communication réseau entre votre cloud de hello et des appareils StorSimple. Sélectionnez **Désactiver** uniquement si vous évoluez au sein d’un cloud privé.
   
    4. Cliquez sur **Add**. Vous êtes averti une fois le compte de stockage hello est créé avec succès.<br></br>
   
     ![Ajouter une information d’identification de compte de stockage existant](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Étape suivante

étape suivante de Hello est tooprovision une machine virtuelle pour votre StorSimple Virtual Array. Selon votre système d’exploitation hôte, consultez hello des instructions dans :

* [Configurer StorSimple Virtual Array dans Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Configurer StorSimple Virtual Array dans VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

