---
title: aaaDeploy votre appareil StorSimple (Update 1) | Documents Microsoft
description: "Décrit les étapes de hello et meilleures pratiques pour le déploiement de service et le périphérique de hello StorSimple Update 1."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ac631d3c-3c53-4c9e-9e4a-5c61c0cd8167
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 339b68f29a73bb77670e76e454cf271c7de4a6e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-1"></a>Déployer votre appareil StorSimple local (Update 1)
> [!div class="op_single_selector"]
> * [Update 2](storsimple-deployment-walkthrough-u2.md)
> * [Update 1](storsimple-deployment-walkthrough-u1.md)
> * [Version Mise à la disposition générale](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Bienvenue dans le déploiement d’appareil Azure StorSimple tooMicrosoft. Ces didacticiels de déploiement s’appliquent tooStorSimple 8000 Series Update 1.0. Cette série de didacticiels décrit comment tooconfigure votre appareil StorSimple et inclut une liste de vérification de configuration, configuration requise et la configuration détaillée comme suit.

informations Hello dans ces didacticiels supposent que vous avez passé en revue les précautions de sécurité hello et décompressé, montés en rack et câblés votre appareil StorSimple. Si vous devez encore tooperform celles, commencez par examiner les hello [précautions de sécurité](storsimple-safety.md). Selon votre modèle d’appareil, vous pouvez ensuite décompresser, monté en rack et câble en suivant les instructions de hello dans :

* [Décompacter, monter en rack et câbler votre appareil 8100](storsimple-8100-hardware-installation.md)
* [Décompacter, monter en rack et câbler votre appareil 8600](storsimple-8600-hardware-installation.md)

Vous aurez besoin des privilèges toocomplete hello le programme d’installation et configuration de processus administrateur. Nous recommandons de consulter la liste de vérification de configuration hello avant de commencer. processus de déploiement et de configuration Hello peut prendre quelques toocomplete de temps.

> [!NOTE]
> informations de déploiement de StorSimple Hello publiées sur le site Web de Microsoft Azure hello s’applique tooStorSimple 8000 series appareils uniquement. Pour plus d’informations sur les périphériques série hello 5000 et 7000, accédez à : [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Pour plus d’informations de déploiement de séries 5000 et 7000, consultez hello [Guide de démarrage rapide StorSimple système](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Étapes du déploiement
Effectuer ces étapes tooconfigure votre appareil StorSimple et le connecter tooyour le service StorSimple Manager. En outre les étapes requises toohello, des étapes facultatives et des procédures, que vous devrez peut-être durant le déploiement de hello. instructions de déploiement étape par étape Hello indiquent le moment où vous devez effectuer chacune de ces étapes facultatives.

| Étape | Description |
| --- | --- |
| **CONFIGURATION REQUISE** |Ceux-ci doivent toobe s’est terminée en préparation du déploiement à venir de hello. |
| Liste de contrôle de la configuration du déploiement. |Utilisez cette liste de vérification toogather et un enregistrement d’informations préalable tooand durant le déploiement de hello. |
| Conditions préalables au déploiement. |Ces valider hello environnement est prêt pour le déploiement. |
|  | |
| **DÉPLOIEMENT ÉTAPE PAR ÉTAPE** |Ces étapes est requise toodeploy votre appareil StorSimple en production. |
| Étape 1 : Création d'un service. |Configurez le stockage et la gestion de cloud pour votre appareil StorSimple. Ignorez cette étape si vous avez un service existant pour d'autres appareils StorSimple. |
| Étape 2 : Obtenir la clé d’inscription hello. |Utilisez cette clé tooregister & connecter votre appareil StorSimple avec le service de gestion hello. |
| Étape 3 : Configurer et inscrire des appareils hello via Windows PowerShell pour StorSimple. |Connecter hello appareil tooyour réseau et l’inscrire avec le programme d’installation hello toocomplete Azure à l’aide du service de gestion hello. |
| Étape 4 : Fin de l'installation minimale de l'appareil</br>Facultatif : mise à jour de votre appareil StorSimple. |Utiliser le programme d’installation de hello management service toocomplete hello appareil et activer tooprovide stockage. |
| Étape 5 : Création d'un conteneur de volumes. |Créer un conteneur de volumes de tooprovision. Un conteneur de volumes a compte de stockage, la bande passante et les paramètres de chiffrement pour tous les volumes hello qu’il contient. |
| Étape 6 : Création d'un volume. |Configurer les volumes de stockage sur l’appareil StorSimple hello pour vos serveurs. |
| Étape 7 : Montage, initialisation et formatage d'un volume.</br>Facultatif : Configuration de solution MPIO. |Se connecter vos serveurs toohello le stockage iSCSI fourni par les périphériques hello. Configurez éventuellement tooensure MPIO que vos serveurs peuvent tolérer lien, de réseau et de défaillance de l’interface. |
| Étape 8 : Sauvegarde. |Configurer votre tooprotect de stratégie de sauvegarde de vos données |
|  | |
| **AUTRES PROCÉDURES** |Vous devrez peut-être des procédures toothese toorefer lorsque vous déployez votre solution. |
| Configurer un nouveau compte de stockage pour le service de hello. | |
| Utilisez la console série du périphérique toohello tooconnect PuTTY. | |
| Obtenir hello IQN d’un hôte Windows Server. | |
| Création d'une sauvegarde manuelle. | |

## <a name="deployment-configuration-checklist"></a>Liste de contrôle de la configuration du déploiement
Hello suivant aide-mémoire de configuration de déploiement décrit les informations de hello que vous avez besoin de toocollect avant et lorsque vous configurez le logiciel de hello sur votre appareil StorSimple. Préparation de certaines de ces informations contribuera à simplifier les processus hello du déploiement de l’appareil StorSimple hello dans votre environnement. Utilisez cette note tooalso de liste de contrôle vers le bas les détails de configuration hello lorsque vous déployez votre appareil.

| Étape | Paramètre | Détails | Valeurs |
| --- | --- | --- | --- |
| **Câblage de l'appareil** |Accès série |Configuration initiale de l’appareil |Oui/Non |
|  | | | |
| **Configuration et inscription de l'appareil** |Paramètres réseau Data 0 |Adresse IP Data 0 :</br>Masque de sous-réseau :</br>Passerelle :</br>Serveur DNS principal :</br>Serveur NTP principal :</br>Serveur de proxy web IP/nom de domaine complet (facultatif) :</br>Port proxy Web : | |
| &nbsp; |Mot de passe d'administrateur de l'appareil |Le mot de passe doit contenir entre 8 et 15 caractères en minuscules, en majuscules, numériques et spéciaux. | |
| &nbsp; |Mot de passe de gestionnaire d’instantanés StorSimple |Le mot de passe doit contenir 14 ou 15 caractères en minuscules, en majuscules, numériques et spéciaux. | |
| &nbsp; |Clé d'inscription du service |Cette clé est générée à partir de hello portail Azure classic. | |
| &nbsp; |Clé de chiffrement des données du service |Cette clé est créée lors de l’appareil de hello est inscrit avec le service de gestion hello via hello Windows PowerShell pour StorSimple. Copiez-la et enregistrez-la en lieu sûr. | |
|  | | | |
| **Mener à bien l'installation minimale de l’appareil** |Nom convivial pour votre appareil |Il s’agit d’un nom descriptif pour le périphérique de hello. | |
| &nbsp; |Fuseau horaire |Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées. | |
| &nbsp; |Serveur DNS secondaire |Il s'agit d'une configuration requise. | |
| &nbsp; |Interface réseau : Adresses IP fixes de contrôleur Data 0 |Ces adresses IP doit être routable toohello Internet.</br>Adresse IP fixe de contrôleur 0 :</br>Adresse IP fixe de contrôleur 1 : | |
|  | | | |
| **Paramètres d'interface réseau supplémentaires** |Interface réseau : Data 1</br>Si iSCSI est activé, ne configurez pas hello passerelle. |Objectif : cloud/iSCSI/non utilisé</br>Adresse IP :</br>Masque de sous-réseau :</br>Passerelle : | |
| &nbsp; |Interface réseau : Data 2</br>Si iSCSI est activé, ne configurez pas hello passerelle. |Objectif : cloud/iSCSI/non utilisé</br>Adresse IP :</br>Masque de sous-réseau :</br>Passerelle : | |
| &nbsp; |Interface réseau : Data 3</br>Si iSCSI est activé, ne configurez pas hello passerelle. |Objectif : cloud/iSCSI/non utilisé</br>Adresse IP :</br>Masque de sous-réseau :</br>Passerelle : | |
| &nbsp; |Interface réseau : Data 4</br>Si iSCSI est activé, ne configurez pas hello passerelle. |Objectif : cloud/iSCSI/non utilisé</br>Adresse IP :</br>Masque de sous-réseau :</br>Passerelle : | |
| &nbsp; |Interface réseau : Data 5</br>Si iSCSI est activé, ne configurez pas hello passerelle. |Objectif : cloud/iSCSI/non utilisé</br>Adresse IP :</br>Masque de sous-réseau :</br>Passerelle : | |
|  | | | |
| **Création d’un conteneur de volumes** |Nom du conteneur de volumes : |Nom de conteneur de hello | |
| &nbsp; |Compte Azure Storage : |Stockage compte nom & accès clé tooassociate avec ce conteneur de volume | |
| &nbsp; |Clé de chiffrement de stockage cloud : |clé de chiffrement pour le stockage dans chaque conteneur | |
|  | | | |
| **Création d’un volume** |Détails de chaque volume |Nom du volume : | |
| &nbsp; |&nbsp; |Taille : | |
| &nbsp; |&nbsp; |Type d'utilisation : | |
| &nbsp; |&nbsp; |Nom ACR : | |
| &nbsp; |&nbsp; |Stratégie de sauvegarde par défaut : | |
|  | | | |
| **Monter, initialiser et formater un volume** |Détails pour chaque serveur hôte de la connexion de stockage de toohello |Nom du serveur Windows : | |
| &nbsp; |&nbsp; |IQN du serveur Windows : | |
| &nbsp; |&nbsp; |Nom de volume du serveur Windows : | |
| &nbsp; |&nbsp; |Point de montage/lettre de lecteur NTFS : | |

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

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service, vous devez toocreate au moins un compte de stockage une fois que vous avez créé un service. Ce compte de stockage est utilisé lorsque vous créez un conteneur de volumes.
> 
> * Si vous n’avez pas créé un compte de stockage automatiquement, passez trop[configurer un nouveau compte de stockage pour le service de hello](#configure-a-new-storage-account-for-the-service) pour obtenir des instructions détaillées.
> * Si vous avez activé la création automatique d’un compte de stockage hello, passez trop[étape 2 : clé d’inscription Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Étape 2 : Obtenir la clé d’inscription hello
Une fois hello service StorSimple Manager est en cours d’exécution, vous devez tooget clé d’inscription hello. Cette clé est utilisée tooregister et connecter votre appareil StorSimple hello service.

Effectuer hello Bonjour portail classique Azure comme suit.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Étape 3 : Configurer et inscrire des appareils hello via Windows PowerShell pour StorSimple
Utiliser Windows PowerShell pour StorSimple toocomplete hello la configuration initiale de votre appareil StorSimple, comme expliqué dans la procédure de hello. Vous devez toocomplete de logiciel d’émulation de terminal toouse cette étape. Pour plus d’informations, consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Étape 4 : Fin de l'installation minimale de l'appareil
Pour hello configuration minimale de votre appareil StorSimple, vous êtes invité à :

* Configurer le serveur DNS secondaire de hello.
* activer la norme iSCSI sur au moins une interface réseau ;
* Affecter des adresses IP fixes contrôleurs de hello tooboth.

Effectuer hello dans le programme d’installation minimale de l’appareil de hello hello toocomplete de portail classique Azure comme suit.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Étape 5 : Création d’un conteneur de volumes
Un conteneur de volumes a compte de stockage, la bande passante et les paramètres de chiffrement pour tous les volumes hello qu’il contient. Vous devez toocreate un conteneur de volumes avant de commencer l’approvisionnement des volumes sur votre appareil StorSimple.

Effectuer hello Bonjour toocreate portail classique Azure un conteneur de volume comme suit.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Étape 6 : Création d’un volume
Après avoir créé un conteneur de volume, vous pouvez configurer un volume de stockage sur l’appareil StorSimple hello pour vos serveurs. Effectuer hello Bonjour toocreate portail classique Azure un volume comme suit.

> [!IMPORTANT]
> StorSimple Manager peut créer uniquement des volumes alloués dynamiquement. Vous ne pouvez pas créer des volumes configurés entièrement ou partiellement.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Étape 7 : Montage, initialisation et formatage d’un volume
Hello suivant les étapes est effectuée sur votre hôte Windows Server.

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

Effectuer hello Bonjour toocreate portail classique Azure une sauvegarde planifiée comme suit.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Vous pouvez à tout moment effectuer une sauvegarde manuelle. Pour les procédures, passez trop[créer une sauvegarde manuelle](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurer un nouveau compte de stockage pour le service de hello
Il s’agit d’une étape facultative que vous avez besoin de tooperform uniquement si vous n’avez pas activé la création automatique d’un compte de stockage hello avec votre service. Un compte de stockage Microsoft Azure est un conteneur de volumes StorSimple de toocreate requis.

Si vous avez besoin d’un compte de stockage Azure dans une région différente de toocreate, consultez [sur les comptes de stockage Azure](../storage/common/storage-create-storage-account.md) pour obtenir des instructions pas à pas.

Effectuer hello comme suit dans hello portail Azure classic sur hello **service StorSimple Manager** page.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Utilisez la console série du périphérique toohello tooconnect PuTTY
tooconnect tooWindows PowerShell pour StorSimple, vous devez le logiciel d’émulation de terminal toouse, tel que PuTTY. Vous pouvez utiliser PuTTY lorsque vous accédez à des périphériques de hello directement via la console série de hello ou en ouvrant une session telnet à partir d’un ordinateur distant.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Recherche et application des mises à jour
La mise à jour de votre appareil peut prendre plusieurs heures. Effectuer hello suivant tooscan étapes pour et appliquer des mises à jour sur votre appareil.
<!--can take 1-4 hours-->

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

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obtenir hello IQN d’un hôte Windows Server
Effectuer hello suivant les étapes tooget hello iSCSI nom qualifié (IQN) d’un hôte Windows qui exécute Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Création d’une sauvegarde manuelle
Effectuer hello comme suit dans la sauvegarde manuelle de hello toocreate portail classique Azure une demande pour un seul volume sur votre appareil StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="configure-mpio"></a>Configuration de solution MPIO
La solution MPIO (Multipath I/O) est une fonctionnalité facultative qui n’est pas installée sur Windows Server par défaut. Il doit être installé en tant que fonctionnalité via le Gestionnaire de serveur. Pour des instructions d’installation MPIO, consultez trop[configuration de MPIO pour votre appareil StorSimple](storsimple-configure-mpio-windows-server.md).

Pour des instructions d’installation pour un appareil StorSimple MPIO connecté tooa hôte Linux, accédez trop[configuration de MPIO pour votre hôte Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> La solution MPIO n’est pas prise en charge sur un appareil virtuel StorSimple.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Configuration d’un [appareil virtuel](storsimple-virtual-device-u2.md).
* Hello d’utilisation [service StorSimple Manager](storsimple-manager-service-administration.md) toomanage votre appareil StorSimple.

