---
title: aaaStorSimple Cloud Appliance Update 3 | Documents Microsoft
description: "Découvrez comment toocreate, déployer et gérer une application de Cloud StorSimple dans un réseau virtuel Microsoft Azure. (S’applique tooStorSimple mise à jour 3 et versions ultérieur)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Déployer et gérer une appliance cloud StorSimple dans Azure (Update 3 et versions ultérieures)

## <a name="overview"></a>Vue d'ensemble

Hello StorSimple 8000 Series Cloud Appliance est une fonctionnalité supplémentaire qui est fourni avec votre solution Microsoft Azure StorSimple. Hello StorSimple Cloud Appliance s’exécute sur un ordinateur virtuel dans un réseau virtuel Microsoft Azure, et vous pouvez l’utiliser tooback d’et cloner les données de vos hôtes.

Cet article décrit toodeploy de procédure pas à pas hello et gérer un dispositif de StorSimple de Cloud dans Azure. À la fin de cet article, vous serez capable :

* Comprendre comment dispositif de cloud hello diffère de périphérique physique de hello.
* Être en mesure de toocreate et configurer le matériel de cloud hello.
* Connectez toohello cloud matériel.
* Découvrez le matériel de cloud toowork avec hello.

Ce didacticiel s’applique tooall hello équipements de Cloud StorSimple en cours d’exécution Update 3 et versions ultérieures.

#### <a name="cloud-appliance-model-comparison"></a>Comparaison des modèles d’appliance cloud

Hello StorSimple Appliance de Cloud est disponible dans les deux modèles, un 8010 standard (anciennement hello 1100) et une prime 8020 (introduite dans Update 2). Hello tableau suivant présente une comparaison de deux modèles de hello.

| Modèle de l'appareil | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacité maximale** |30 To |64 To |
| **Microsoft Azure** |Standard_A3 (4 cœurs, 7 Go de mémoire)| Standard_DS3 (4 cœurs, 14 Go de mémoire)|
| **Disponibilité des régions** |Toutes les régions Azure |Régions Azure qui prennent en charge le stockage Premium et les machines virtuelles Azure DS3<br></br>Utilisez [cette liste](https://azure.microsoft.com/regions/services/) toosee si les deux **virtuels > série DS** et **stockage > le stockage sur disque** sont disponibles dans votre région. |
| **Type de stockage** |Utilise le stockage Azure Standard pour les disques locaux<br></br> Découvrez comment trop[créer un compte de stockage Standard](../storage/common/storage-create-storage-account.md) |Utilise le stockage Azure Standard pour les disques locaux<sup>2</sup> <br></br>Découvrez comment trop[créer un compte de stockage Premium](../storage/common/storage-premium-storage.md) |
| **Aide relative à la charge de travail** |Récupération au niveau des éléments des fichiers à partir de sauvegardes |Scénarios de développement et de test cloud <br></br>Faible latence et charges de travail aux performances plus élevées<br></br>Appareil secondaire pour la récupération d’urgence |

<sup>1</sup> *anciennement hello 1100*.

<sup>2</sup> *à la fois hello 8010 et 8020 utiliser le stockage Standard de Azure pour hello cloud couche hello différence existe uniquement dans hello local de niveau dans les appareils hello*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Comment dispositif de cloud hello diffère de périphérique physique de hello

Hello équipement de Cloud StorSimple est une version logicielle de StorSimple qui s’exécute sur un seul nœud dans une Machine virtuelle Microsoft Azure. Hello cloud prend en charge les scénarios de récupération d’urgence dans lesquels votre appareil physique n’est pas disponible. Dispositif de cloud Hello est appropriée pour une utilisation dans la récupération au niveau de l’élément à partir de sauvegardes, la récupération d’urgence sur site et les scénarios de développement et de test cloud.

#### <a name="differences-from-hello-physical-device"></a>Différences par rapport à l’unité physique de hello

Hello tableau suivant présente quelques différences clés entre hello StorSimple Appliance de Cloud et l’appareil physique StorSimple de hello.

|  | Appareil physique | Appliance cloud |
| --- | --- | --- |
| **Emplacement** |Se trouve dans le centre de données hello. |S'exécute dans Azure. |
| **Interfaces réseau** |Comporte six interfaces réseau : de DATA 0 à DATA 5. |A une seule interface réseau : DATA 0. |
| **Inscription** |Enregistrés lors de l’étape de la configuration initiale de hello. |L'inscription est une tâche distincte. |
| **Clé de chiffrement de données du service** |Régénérer sur l’appareil physique de hello et ensuite mettre à jour l’équipement de cloud hello avec la nouvelle clé de hello. |Ne peut pas régénérer à partir de l’équipement de cloud hello. |
| **Types de volumes pris en charge** |Prend en charge les volumes hiérarchisés et les volumes attachés localement. |Ne prend en charge que les volumes hiérarchisés. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Configuration requise pour le matériel de cloud hello

Hello les sections suivantes explique hello configuration requise pour votre solution de Cloud StorSimple. Avant de déployer une application cloud, passez en revue hello considérations relatives à l’aide d’un dispositif de cloud.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Conditions requises pour Azure

Avant de préparer dispositif de cloud hello, vous devez hello toomake suivant préparations dans votre environnement Azure :

* Assurez-vous qu’un appareil physique de la série StorSimple 8000 (modèle 8100 ou 8600) est déployé et exécuté dans votre centre de données. Inscrire cet appareil auprès de hello même service de gestionnaire de périphériques StorSimple que vous avez l’intention toocreate une Appliance au Cloud StorSimple.
* Pour le matériel de cloud hello, [configurer un réseau virtuel sur Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Si vous utilisez le stockage Premium, vous devez créer un réseau virtuel dans une région Azure qui prend en charge le stockage Premium. régions de stockage Premium Hello sont des régions qui correspondent ligne toohello pour le stockage de disque Bonjour [liste des Services Azure par région](https://azure.microsoft.com/regions/services/).
* Nous vous recommandons d’utiliser serveurDNS hello par défaut fournie par Azure au lieu de spécifier le nom de votre propre serveur DNS. Si le nom de votre serveur DNS n’est pas valide ou si le serveur DNS de hello n’est pas en mesure de tooresolve des adresses IP correctement, la création de hello de dispositif de cloud hello échoue.
* Les options de point à site et de site à site sont facultatives (non obligatoires). Si vous le souhaitez, vous pouvez configurer ces options pour des scénarios plus avancés.
* Vous pouvez créer [des Machines virtuelles Azure](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (serveurs hôtes) dans un réseau virtuel hello qui peut utiliser des volumes de hello exposées par le dispositif de cloud hello. Ces serveurs doivent remplir hello suivant les exigences :

  * Il doit s’agir de machines virtuelles Windows ou Linux sur lesquelles l’initiateur iSCSI est installé.
  * Être en cours d’exécution dans hello même réseau virtuel en tant que dispositif de cloud hello.
  * Être en mesure de tooconnect toohello de cible iSCSI de dispositif de cloud hello via hello adresse IP interne du dispositif de cloud hello.
  * Assurez-vous que vous avez configuré la prise en charge pour iSCSI et cloud le trafic sur hello même réseau virtuel.

#### <a name="storsimple-requirements"></a>Conditions requises pour StorSimple

Rendre hello suivant le service de gestionnaire de périphériques StorSimple tooyour mises à jour avant de créer une application cloud :

* Ajouter [enregistrements de contrôle d’accès](storsimple-8000-manage-acrs.md) pour les machines virtuelles hello qui sont des serveurs d’hôte continu toobe hello pour votre solution de cloud.
* Utilisez un [compte de stockage](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) Bonjour même région que le matériel de cloud hello. Des comptes de stockage dans différentes régions peuvent entraîner une dégradation des performances. Vous pouvez utiliser un compte Standard ou Premium stockage avec le matériel de cloud hello. Plus d’informations sur la façon de toocreate un [compte de stockage Standard](../storage/common/storage-create-storage-account.md) ou un [compte de stockage Premium](../storage/common/storage-premium-storage.md)
* Utilisez un autre compte de stockage pour la création d’application cloud à partir de hello celui utilisé pour vos données. À l’aide du même compte de stockage peut entraîner une dégradation des performances de hello.

Assurez-vous que vous avez hello suivant informations avant de commencer :

* Votre compte avec les informations d’identification d’accès au portail Azure.
* Une copie de la clé de chiffrement de données de service hello à partir de votre appareil physique inscrit le service du Gestionnaire de périphériques StorSimple toohello.

## <a name="create-and-configure-hello-cloud-appliance"></a>Créer et configurer le matériel de cloud hello

Avant d’effectuer ces procédures, assurez-vous que vous avez rempli hello [configuration requise pour le matériel de cloud hello](#prerequisites-for-the-cloud-appliance).

Effectuer hello suivant les étapes toocreate un dispositif de StorSimple de Cloud.

### <a name="step-1-create-a-cloud-appliance"></a>Étape 1: créer une appliance cloud

Effectuer hello suivant les étapes toocreate hello StorSimple Appliance de Cloud.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Si la création de hello du dispositif de cloud hello échoue dans cette étape, vous ne pouvez pas avoir toohello de connectivité Internet. Pour plus d’informations, consultez trop[résoudre les problèmes de connectivité Internet](#troubleshoot-internet-connectivity-errors) lors de la création d’une application cloud.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Étape 2 : Configurer et inscrire le dispositif de cloud hello

Avant de commencer cette procédure, assurez-vous que vous disposez d’une copie de la clé de chiffrement de données de service hello. clé de chiffrement de données de service Hello est créé lorsque vous avez inscrit votre premier appareil physique StorSimple avec hello service du Gestionnaire de périphériques StorSimple. Vous avez demandé toosave dans un emplacement sécurisé. Si vous n’avez pas une copie de la clé de chiffrement de données de service hello, vous devez contacter le Support technique de Microsoft pour obtenir une assistance.

Effectuer hello suivant les étapes tooconfigure et inscrire votre dispositif de StorSimple de Cloud.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Étape 3 : Paramètres de configuration (facultatif) modifier hello

Hello section suivante décrit des paramètres de configuration de périphérique de hello nécessaires pour hello StorSimple Appliance de Cloud si vous souhaitez toouse CHAP, gestionnaire d’instantanés StorSimple ou modifiez le mot de passe administrateur de périphérique hello.

#### <a name="configure-hello-chap-initiator"></a>Configurer l’initiateur CHAP de hello

Ce paramètre contient les informations d’identification hello votre solution de cloud (cible) attend des initiateurs de hello (serveurs) qui tentent de volumes de hello tooaccess. les initiateurs Hello fournissent un nom d’utilisateur et un tooidentify de mot de passe CHAP eux-mêmes tooyour appareil au cours de cette authentification. Pour des instructions détaillées, consultez trop[configurer CHAP pour votre appareil](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurer la cible CHAP de hello

Ce paramètre contient les informations d’identification de hello votre solution de cloud utilise lorsqu’un initiateur CHAP demande une authentification mutuelle ou bidirectionnelle. Votre solution de cloud utilise un nom d’utilisateur et un tooidentify de mot de passe CHAP inversé lui-même toohello initiateur pendant le processus d’authentification.

> [!NOTE]
> Les paramètres CHAP cibles sont des paramètres globaux. Lorsque ces paramètres sont appliqués, tous les volumes hello connecté toohello cloud utilisez CHAP l’authentification.

Pour des instructions détaillées, consultez trop[configurer CHAP pour votre appareil](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurer le mot de passe de gestionnaire d’instantanés StorSimple hello

Gestionnaire d’instantanés StorSimple logiciel réside sur l’hôte Windows et permet aux administrateurs toomanage les sauvegardes de votre appareil StorSimple dans l’écran hello locaux et les instantanés cloud.

> [!NOTE]
> Pour le matériel de cloud hello, votre hôte Windows est une machine virtuelle Azure.

Lorsque vous configurez un appareil Bonjour Gestionnaire d’instantanés StorSimple, vous êtes invité tooprovide hello StorSimple appareil IP adresse et le mot de passe tooauthenticate votre périphérique de stockage. Pour des instructions détaillées, consultez trop[mot de passe de configurer le Gestionnaire d’instantanés StorSimple](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Mot de passe de l’administrateur d’appareil modification hello

Lorsque vous utilisez hello Windows PowerShell interface tooaccess hello DISPOSITIF cloud, vous êtes tooenter requis un mot de passe administrateur. Pour une sécurité hello de vos données, vous devez modifier ce mot de passe avant de l’application de cloud hello peut être utilisée. Pour des instructions détaillées, consultez trop[mot de passe administrateur de périphérique configurer](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Se connecter à distance de dispositif de cloud toohello

Dispositif de cloud tooyour l’accès à distance via l’interface Windows PowerShell de hello n’est pas activé par défaut. Vous devez activer la gestion à distance sur l’équipement de cloud hello tout d’abord, et ensuite sur hello client Dispositif de cloud tooaccess hello.

Hello en deux étapes procédure décrit comment tooconnect à distance tooyour cloud appliance.

### <a name="step-1-configure-remote-management"></a>Étape 1 : configurer la gestion à distance

Effectuer hello suivant de gestion à distance de tooconfigure étapes pour votre solution de Cloud StorSimple.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Étape 2 : Accéder à distance au dispositif de cloud hello

Après avoir activé la gestion à distance sur l’équipement de cloud hello, utiliser Windows PowerShell remoting tooconnect toohello à partir d’un autre ordinateur virtuel à l’intérieur de hello même réseau virtuel. Par exemple, vous pouvez vous connecter à partir de l’hôte hello machine virtuelle que vous avez configuré et utilisé tooconnect iSCSI. Dans la plupart des déploiements, vous allez ouvrir un point de terminaison public de tooaccess votre hôte de machine virtuelle que vous pouvez utiliser pour accéder au dispositif de cloud hello.

> [!WARNING]
> **Pour renforcer la sécurité, nous recommandons vivement que vous utilisez HTTPS lors de la connexion de points de terminaison toohello et puis supprimez les points de terminaison hello après avoir terminé votre session à distance de PowerShell.**

Vous devez suivre les procédures hello [connexion à distance de l’appareil StorSimple tooyour](storsimple-8000-remote-connect.md) tooset une communication à distance pour votre solution de cloud.

## <a name="connect-directly-toohello-cloud-appliance"></a>Connecter directement toohello cloud matériel

Vous pouvez également vous connecter directement dispositif de toohello de cloud. tooconnect directement de l’équipement à partir d’un autre ordinateur en dehors de cloud computing toohello hello environnement de Microsoft Azure hello externe ou de réseau virtuel, vous devez créer des points de terminaison supplémentaires.

Effectuer hello suivant les étapes toocreate un point de terminaison public sur l’équipement de cloud hello.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

Nous recommandons que vous vous connectez à partir d’un autre ordinateur virtuel à l’intérieur de hello virtuel même réseau, car cette pratique réduit le nombre de hello de points de terminaison publics sur votre réseau virtuel. Dans ce cas, connecter l’ordinateur virtuel de toohello via une session Bureau à distance et puis configurez cet ordinateur virtuel pour une utilisation comme vous le feriez pour n’importe quel autre client Windows sur un réseau local. Il est inutile numéro de port public tooappend hello car hello port est déjà connu.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Travailler avec hello StorSimple Appliance de Cloud

Maintenant que vous avez créé et configuré des hello StorSimple Appliance de Cloud, vous êtes prêt toostart son utilisation. Vous pouvez travailler avec des conteneurs de volumes, des volumes et des stratégies de sauvegarde sur une appliance cloud comme vous le feriez sur un appareil physique StorSimple. Hello seule différence est que vous devez toomake Sélectionnez Dispositif de cloud hello à partir de votre liste de périphériques. Consultez trop[utiliser hello le Gestionnaire de périphériques StorSimple service toomanage un dispositif de cloud](storsimple-8000-manager-service-administration.md) pour obtenir des procédures de gestion différentes tâches pour le dispositif de cloud hello de hello.

Hello sections suivantes décrivent certaines des différences de hello que vous rencontrez lorsque vous travaillez avec un dispositif de cloud hello.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Assurer la maintenance de StorSimple Cloud Appliance

Car il s’agit d’un dispositif logiciel, le mise à jour pour le dispositif de cloud hello est minime lorsque comparées toomaintenance pour les appareils physiques hello.

Vous ne pouvez pas mettre à jour une appliance cloud. Utiliser hello la dernière version du logiciel toocreate un nouveau matériel de cloud.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Comptes de stockage pour une appliance cloud

Comptes de stockage sont créés pour une utilisation par hello service du Gestionnaire de périphériques StorSimple, par application de cloud hello et par unité physique de hello. Lorsque vous créez vos comptes de stockage, nous vous recommandons d’utiliser un identificateur de région dans le nom convivial de hello. Cela permet de garantir que cette région de hello est cohérente dans tous les composants du système hello. Pour un dispositif de cloud, il est important que tous les composants hello Bonjour les problèmes de performances tooprevent même région.

Pour une procédure pas à pas, consultez trop[ajouter un compte de stockage](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Désactiver StorSimple Cloud Appliance

Lorsque vous désactivez un dispositif de cloud, action de hello supprime hello VM et ressources hello créés lors de sa préparation. Une fois que le matériel de cloud hello est désactivé, il ne peut pas être restauré tooits l’état précédent. Avant de désactiver dispositif de cloud hello, assurez-vous que toostop ou supprimer des clients et les hôtes qui en dépendent.

La désactivation d’une application cloud renvoie hello suivant des actions :

* Dispositif de cloud Hello est supprimé.
* disque de Hello du système d’exploitation et des disques de données créés pour le dispositif de cloud hello sont supprimés.
* service de Hello hébergé et le réseau virtuel créé lors de la configuration sont conservés. Si vous ne les utilisez pas, vous devez les supprimer manuellement.
* Les instantanés cloud créés pour le dispositif de cloud hello sont conservés.

Pour une procédure pas à pas, consultez trop[désactiver et supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).

Dès que le matériel de cloud hello est indiquée comme étant désactivés sur le panneau de service de gestionnaire de périphériques StorSimple hello, vous pouvez supprimer le dispositif de cloud hello à partir de la liste des appareils sur hello **périphériques** panneau.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Démarrer, arrêter et redémarrer une appliance cloud
Contrairement aux appareils physiques StorSimple de hello, n’est pas alimenté alimentation toopush bouton sur un dispositif de Cloud StorSimple. Toutefois, il peut arriver où vous devez toostop et redémarrez le dispositif de cloud hello.

Hello plus facile pour vous toostart, arrêt et redémarrage de qu'une application cloud est via le panneau de service de Machines virtuelles hello. Atteindre le service de machine virtuelle hello. À partir de la liste de hello des machines virtuelles, identifier l’application de cloud de tooyour correspondante hello VM (même nom), cliquez sur le nom d’ordinateur virtuel hello. Lorsque vous examinez le panneau de votre machine virtuelle, état appliance de cloud hello est **en cours d’exécution** , car il est démarré par défaut après sa création. Vous pouvez démarrer, arrêter et redémarrer une machine virtuelle à tout moment.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Réinitialiser les valeurs par défaut toofactory
Si vous décidez que vous souhaitez toostart par avec votre application cloud, désactiver et supprimer et créer un nouveau.

## <a name="fail-over-toohello-cloud-appliance"></a>Basculer le dispositif de toohello de cloud
La récupération d’urgence (DR) est un de hello principaux scénarios que hello StorSimple Appliance de Cloud a été conçu pour. Dans ce scénario, hello périphérique physique StorSimple ou centre de données entier n’est peut-être pas disponible. Heureusement, vous pouvez utiliser une cloud appliance toorestore les opérations dans un autre emplacement. Au cours de la récupération d’urgence, les conteneurs de volumes hello à partir de l’appareil source de hello changent de propriétaire et sont le dispositif de cloud toohello transférés.

conditions préalables de Hello pour la récupération d’urgence sont :

* Dispositif de cloud Hello est créé et configuré.
* Tous les volumes de hello dans le conteneur de volume hello sont hors connexion.
* conteneur de volumes Hello basculer, est associé à un instantané cloud.

> [!NOTE]
> * Lorsque vous utilisez un dispositif de cloud en tant que périphérique secondaire de hello pour la récupération d’urgence, gardez à l’esprit que hello 8010 a 30 To de stockage Standard et 8020 a 64 To de stockage Premium. Hello supérieur capacité 8020 cloud peut être plus adapté à un scénario de récupération d’urgence.

Pour une procédure pas à pas, consultez trop[basculer le dispositif de cloud tooa](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Supprimer le dispositif de cloud hello
Si vous déjà configuré et utilisé un dispositif de StorSimple de Cloud, mais vous souhaitez que toostop accumuler de frais de calcul de son utilisation, vous devez arrêter dispositif de cloud hello. Dispositif de cloud hello arrêt désalloue hello machine virtuelle. Cette action empêche le cumul des frais sur votre abonnement. frais de stockage Hello pour hello du système d’exploitation et des disques de données continue toutefois.

les frais toostop tous hello, vous devez supprimer le dispositif de cloud hello. sauvegardes de hello toodelete créés par le dispositif de cloud hello, vous pouvez désactiver ou supprimer des appareils de hello. Pour plus d’informations, consultez [Désactiver et supprimer un appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Résolution des problèmes de connectivité Internet
Lors de la création de hello d’un appareil de cloud computing, s’il n’existe aucun toohello de connectivité Internet, étape de la création de hello échoue. défaillances de connectivité Internet tootroubleshoot, effectuez hello Bonjour portail Azure comme suit :

1. [Créez une machine virtuelle Windows Server 2012 dans Azure](/articles/virtual-machines/windows/quick-create-portal.md). Cet ordinateur virtuel doit utiliser hello même compte de stockage, réseau virtuel et sous-réseau que celui utilisé par votre solution de cloud. S’il existe un hôte Windows Server à l’aide d’Azure hello même compte de stockage, réseau virtuel et sous-réseau, vous pouvez également l’utiliser la connectivité Internet tootroubleshoot hello.
2. Connectez-vous à distance virtuels hello créé Bonjour précédant l’étape.
3. Ouvrez une fenêtre de commande à l’intérieur de machine virtuelle de hello (Win + R, puis tapez `cmd`).
4. Exécutez hello suivant cmd invite hello.

    `nslookup windows.net`
5. Si `nslookup` échoue, empêche l’équipement de cloud hello lors de l’inscription du service de gestionnaire de périphériques StorSimple toohello Échec de connectivité Internet.
6. Apporter des modifications de hello requis tooensure de réseau virtuel tooyour qui hello DISPOSITIF cloud est en mesure de tooaccess sites Azure comme _windows.net_.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser hello le Gestionnaire de périphériques StorSimple service toomanage un dispositif de cloud](storsimple-8000-manager-service-administration.md).
* Comprendre comment trop[restaurer un volume StorSimple à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).
