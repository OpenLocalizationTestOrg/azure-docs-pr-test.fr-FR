---
title: "l’appareil StorSimple aaaDeploy dans le portail d’administration | Documents Microsoft"
description: "Décrit les étapes hello et meilleures pratiques pour appareil de hello StorSimple Update 2 déploiement et de service dans le portail d’administration d’Azure hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 68104988595341a49a87d78c4a9b1d2675759c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal-update-2"></a>Déployer l’appareil StorSimple local Bonjour gouvernement Portal (Update 2)
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Vue d'ensemble
Bienvenue dans le déploiement d’appareil Azure StorSimple tooMicrosoft. Ces didacticiels de déploiement appliquent toohello StorSimple 8000 Series en cours d’exécution 2 de la mise à jour de logiciel Bonjour Azure Government Portal. Ils proposent une liste de contrôle de la configuration, ainsi qu’une liste des éléments requis et des étapes de configuration détaillées pour votre appareil StorSimple.

informations Hello dans ces didacticiels supposent que vous avez passé en revue les précautions de sécurité hello et décompressé, montés en rack et câblés votre appareil StorSimple. Si vous devez encore tooperform celles, commencez par examiner les hello [précautions de sécurité](storsimple-safety.md). Suivez les instructions de spécifique au périphérique hello toounpack, montage en rack et câbler votre appareil.

* [Décompacter, monter en rack et câbler votre appareil 8100](storsimple-8100-hardware-installation.md)
* [Décompacter, monter en rack et câbler votre appareil 8600](storsimple-8600-hardware-installation.md)

Vous aurez besoin des privilèges toocomplete hello le programme d’installation et configuration de processus administrateur. Nous recommandons de consulter la liste de vérification de configuration hello avant de commencer. processus de déploiement et de configuration Hello peut prendre quelques toocomplete de temps.

> [!NOTE]
> informations de déploiement de StorSimple Hello publiées sur le site Web de Microsoft Azure hello s’applique tooStorSimple 8000 series appareils uniquement. Pour plus d’informations sur les périphériques série hello 7000, accédez à : [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Pour plus d’informations de déploiement de 7000 série, voir hello [Guide de démarrage rapide StorSimple système](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Étapes du déploiement
Effectuer ces étapes tooconfigure votre appareil StorSimple et le connecter tooyour le service StorSimple Manager. En outre les étapes requises toohello, il existe des étapes facultatives et les procédures que vous devrez peut-être toocomplete durant le déploiement de hello. instructions de déploiement étape par étape Hello indiquent le moment où vous devez effectuer chacune de ces étapes facultatives.

| Étape | Description |
| --- | --- |
| **CONFIGURATION REQUISE** |Ceux-ci doivent toobe s’est terminée en préparation du déploiement à venir de hello. |
| [Liste de contrôle de la configuration du déploiement](#deployment-configuration-checklist) |Utilisez cette liste de vérification toogather et un enregistrement d’informations préalable tooand durant le déploiement de hello. |
| [Conditions préalables au déploiement](#deployment-prerequisites) |Ces valider ce hello environnement est prêt pour le déploiement. |
|  | |
| **DÉPLOIEMENT ÉTAPE PAR ÉTAPE** |Ces étapes est requise toodeploy votre appareil StorSimple en production. |
| [Étape 1 : Création d’un nouveau service](#step-1-create-a-new-service) |Configurez le stockage et la gestion de cloud pour votre appareil StorSimple. *Ignorez cette étape si vous avez un service existant pour d'autres appareils StorSimple*. |
| [Étape 2 : Obtenir la clé d’inscription hello](#step-2-get-the-service-registration-key) |Utilisez cette clé tooregister et connecter votre appareil StorSimple avec le service de gestion hello. |
| [Étape 3 : Configurer et inscrire des appareils hello via Windows PowerShell pour StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Connecter hello appareil tooyour réseau et l’inscrire avec le programme d’installation hello toocomplete Azure à l’aide du service de gestion hello. |
| [Étape 4 : Terminer l’installation minimale hello](#step-4-complete-minimum-device-setup) </br>Facultatif : mise à jour de votre appareil StorSimple. |Utiliser le programme d’installation de hello management service toocomplete hello appareil et activer tooprovide stockage. |
| [Étape 5 : Création d’un conteneur de volumes](#step-5-create-a-volume-container) |Créer un conteneur de volumes de tooprovision. Un conteneur de volumes a compte de stockage, la bande passante et les paramètres de chiffrement pour tous les volumes hello qu’il contient. |
| [Étape 6 : Création d’un volume](#step-6-create-a-volume) |Configurer les volumes de stockage sur l’appareil StorSimple hello pour vos serveurs. |
| [Étape 7 : Montage, initialisation et formatage d’un volume](#step-7-mount-initialize-and-format-a-volume) </br>Facultatif : Configuration de solution MPIO. |Se connecter vos serveurs toohello le stockage iSCSI fourni par les périphériques hello. Éventuellement, configurez tooensure MPIO que vos serveurs peuvent tolérer lien, de réseau et de défaillance de l’interface. |
| [Étape 8 : Sauvegarde](#step-8-take-a-backup) |Configurer votre tooprotect de stratégie de sauvegarde de vos données |
|  | |
| **AUTRES PROCÉDURES** |Vous devrez peut-être des procédures toothese toorefer lorsque vous déployez votre solution. |
| [Configurer un nouveau compte de stockage pour le service de hello](#configure-a-new-storage-account-for-the-service) | |
| [Utilisez la console série du périphérique toohello tooconnect PuTTY](#use-putty-to-connect-to-the-device-serial-console) | |
| [Recherche et application des mises à jour](#scan-for-and-apply-updates) | |
| [Obtenir hello IQN d’un hôte Windows Server](#get-the-iqn-of-a-windows-server-host) | |
| [Création d’une sauvegarde manuelle](#create-a-manual-backup) | |
| [Configuration de solution MPIO](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>Liste de contrôle de la configuration du déploiement
Avant de déployer votre appareil StorSimple, vous devez logiciel de hello tooconfigure toocollect plus d’informations sur votre appareil. Préparation de certaines de ces informations contribuera à simplifier les processus hello du déploiement de l’appareil StorSimple hello dans votre environnement. Téléchargez et utilisez les détails de la configuration de hello du toonote de cette liste de vérification que vous déployez votre appareil.  

[Télécharger la liste de contrôle de la configuration du déploiement StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>Conditions préalables au déploiement
Hello les sections suivantes explique hello configuration requise pour votre service StorSimple Manager et de votre appareil StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Pourquoi le service StorSimple Manager
Avant de commencer, assurez-vous que :

* Vous disposez d’un compte Microsoft doté d’informations d’identification d’accès.
* Vous disposez d’un compte de stockage Microsoft Azure doté d’informations d’identification d’accès.
* Votre abonnement Microsoft Azure est activée pour hello service StorSimple Manager. Votre abonnement doit être souscrit via hello [accord entreprise](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Vous avez accès tooterminal émulation logicielle, tel que PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Périphérique hello dans le centre de données hello
Avant de configurer le périphérique de hello, assurez-vous que :

* Votre appareil est correctement décompacté, monté en rack et câblé à l’alimentation, au réseau et au port série comme cela est indiqué dans les articles suivants :
  
  * [Décompacter, monter en rack et câbler votre appareil 8100](storsimple-8100-hardware-installation.md)
  * [Décompacter, monter en rack et câbler votre appareil 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Pour le réseau hello dans le centre de données hello
Avant de commencer, assurez-vous que :

* Hello ports dans le pare-feu de votre centre de données sont tooallow ouvert pour le trafic iSCSI et cloud comme décrit dans [configuration réseau requise pour votre appareil StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>DÉPLOIEMENT ÉTAPE PAR ÉTAPE
Utilisez hello suivant toodeploy des instructions pas à votre appareil StorSimple dans le centre de données hello.

## <a name="step-1-create-a-new-service"></a>Étape 1 : Création d’un nouveau service
Un service StorSimple Manager peut gérer plusieurs appareils StorSimple. Effectuer hello suivant les étapes toocreate une nouvelle instance de service de StorSimple Manager hello.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service, vous devez toocreate au moins un compte de stockage une fois que vous avez créé un service. Ce compte de stockage est utilisé lorsque vous créez un conteneur de volumes.
> 
> * Si vous n’avez pas créé un compte de stockage automatiquement, passez trop[configurer un nouveau compte de stockage pour le service de hello](#configure-a-new-storage-account-for-the-service) pour obtenir des instructions détaillées.
> * Si vous avez activé la création automatique d’un compte de stockage hello, passez trop[étape 2 : clé d’inscription Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Étape 2 : Obtenir la clé d’inscription hello
Une fois hello service StorSimple Manager est en cours d’exécution, vous devez tooget clé d’inscription hello. Cette clé est utilisée tooregister et se connecter à votre service de toohello de périphérique StorSimple.

Effectuer hello Bonjour gouvernement portail comme suit.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Étape 3 : Configurer et inscrire des appareils hello via Windows PowerShell pour StorSimple
Utiliser Windows PowerShell pour StorSimple toocomplete hello la configuration initiale de votre appareil StorSimple, comme expliqué dans la procédure de hello. Vous devez toocomplete de logiciel d’émulation de terminal toouse cette étape. Pour plus d’informations, consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Étape 4 : Fin de l'installation minimale de l'appareil
Pour hello configuration minimale de votre appareil StorSimple, vous êtes invité à :

* Configurer le serveur DNS secondaire de hello.
* activer la norme iSCSI sur au moins une interface réseau ;
* Affecter des adresses IP fixes contrôleurs de hello tooboth.

Effectuer hello comme suit dans le programme d’installation de hello gouvernement portail toocomplete hello minimale de l’appareil.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Étape 5 : Création d’un conteneur de volumes
Un conteneur de volumes a compte de stockage, la bande passante et les paramètres de chiffrement pour tous les volumes hello qu’il contient. Vous devez toocreate un conteneur de volumes avant de commencer l’approvisionnement des volumes sur votre appareil StorSimple.

Effectuer hello dans hello gouvernement portail toocreate un conteneur de volume comme suit.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Étape 6 : Création d’un volume
Après avoir créé un conteneur de volume, vous pouvez configurer un volume de stockage sur l’appareil StorSimple hello pour vos serveurs. Effectuer hello dans hello gouvernement portail toocreate un volume comme suit.

> [!IMPORTANT]
> Azure StorSimple peut créer uniquement des volumes alloués dynamiquement.  Vous ne pouvez pas créer de volumes entièrement ou partiellement alloués sur un système Azure StorSimple.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Étape 7 : Montage, initialisation et formatage d’un volume
Procédez comme suit sur votre hôte Windows Server.

> [!IMPORTANT]
> * Hello haute disponibilité de votre solution StorSimple, nous vous recommandons de configurer MPIO sur tooconfiguring préalable de serveurs (facultatif) votre hôte iSCSI. Configuration de MPIO sur les serveurs hôtes garantit que les serveurs hello peuvent tolérer un lien, un réseau ou une défaillance de l’interface.
> * Pour MPIO et iSCSI installation et configuration des instructions sur l’hôte Windows Server, accédez trop[configuration de MPIO pour votre appareil StorSimple](storsimple-configure-mpio-windows-server.md). Ceux-ci incluent hello étapes toomount également, initialiser et formater les volumes StorSimple.
> * Pour MPIO et iSCSI configuration instructions d’installation et sur un hôte Linux, consultez trop[configuration de MPIO pour votre hôte StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Si vous ne décidez pas tooconfigure MPIO, effectuez hello suivant les étapes toomount, initialiser et formater vos volumes StorSimple sur un ordinateur hôte Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Étape 8 : Sauvegarde
Les sauvegardes fournissent une protection jusqu’à une date et une heure des volumes et optimisent la récupération tout en réduisant les délais de restauration. Vous pouvez effectuer deux types de sauvegarde sur votre appareil StorSimple : les instantanés locaux et les instantanés cloud. Chacun de ces types de sauvegarde peut être **Planifié** ou **Manuel**.

Effectuer hello comme suit dans hello gouvernement portail toocreate une sauvegarde planifiée.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Vous pouvez à tout moment effectuer une sauvegarde manuelle. Pour les procédures, passez trop[créer une sauvegarde manuelle](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurer un nouveau compte de stockage pour le service de hello
Il s’agit d’une étape facultative que vous avez besoin de tooperform uniquement si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service. Un compte de stockage Microsoft Azure est un conteneur de volumes StorSimple de toocreate requis.

Si vous avez besoin d’un compte de stockage Azure dans une région différente de toocreate, consultez [sur les comptes de stockage Azure](../storage/common/storage-create-storage-account.md) pour obtenir des instructions pas à pas.

Effectuer hello comme suit dans hello gouvernement portail, sur hello **service StorSimple Manager** page.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Utilisez la console série du périphérique toohello tooconnect PuTTY
tooconnect tooWindows PowerShell pour StorSimple, vous devez le logiciel d’émulation de terminal toouse, tel que PuTTY. Vous pouvez utiliser PuTTY lorsque vous accédez à des périphériques de hello directement via la console série de hello ou en ouvrant une session telnet à partir d’un ordinateur distant.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Recherche et application des mises à jour
La mise à jour de votre appareil peut prendre plusieurs heures. Effectuer hello suivant tooscan étapes pour et appliquer des mises à jour sur votre appareil.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate votre appareil
1. Sur l’appareil de hello **Quick Start** , cliquez sur **périphériques**. Sélectionnez l’unité physique de hello, cliquez sur **Maintenance** puis cliquez sur **d’analyse des mises à jour**.  
2. Un tooscan de travail mises à jour disponibles est créé. Si les mises à jour sont disponibles, hello **d’analyse des mises à jour** change également**installer les mises à jour**. Cliquez sur **Installer les mises à jour**.
3. Une tâche de mise à jour est créée. Surveiller l’état de hello de votre mise à jour en accédant trop**travaux**.
   
   > [!NOTE]
   > Lorsque le travail de mise à jour hello démarre, il affiche immédiatement hello statut 50 pour cent. Hello devient too100 % uniquement après que la tâche de mise à jour hello est terminée. Il n’existe aucun état en temps réel pour les processus de mise à jour hello.
   > 
   > 
4. Une fois que l’appareil de hello est correctement mise à jour, activer des interfaces réseau Data 2 et 3 de données si elles ont été désactivés.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obtenir hello IQN d’un hôte Windows Server
Effectuer hello suivant les étapes tooget hello iSCSI nom qualifié (IQN) d’un hôte Windows qui exécute Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Création d’une sauvegarde manuelle
Effectuer hello comme suit dans une sauvegarde manuelle de hello gouvernement portail toocreate une demande pour un seul volume sur votre appareil StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Configuration de solution MPIO
La solution MPIO (Multipath I/O) est une fonctionnalité facultative qui n’est pas installée sur Windows Server par défaut. Il doit être installé en tant que fonctionnalité via le Gestionnaire de serveur. Pour des instructions d’installation MPIO, consultez trop[configuration de MPIO pour votre appareil StorSimple](storsimple-configure-mpio-windows-server.md).

Pour des instructions d’installation pour un appareil StorSimple MPIO connecté tooa hôte Linux, accédez trop[configuration de MPIO pour votre hôte Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> La solution MPIO n’est pas prise en charge sur un appareil virtuel StorSimple dans Azure.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Configuration d’un [appareil virtuel](storsimple-virtual-device-u2.md).
* Hello d’utilisation [service StorSimple Manager](storsimple-manager-service-administration.md) toomanage votre appareil StorSimple.

