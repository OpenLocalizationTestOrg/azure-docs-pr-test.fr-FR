---
title: "2 de la mise à jour d’un appareil virtuel aaaStorSimple | Documents Microsoft"
description: "Découvrez comment toocreate, déployer et gérer un périphérique virtuel StorSimple dans un réseau virtuel Microsoft Azure. (S’applique tooStorSimple Update 2)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Déployer et gérer un appareil virtuel StorSimple dans Azure
## <a name="overview"></a>Vue d'ensemble
périphérique virtuel de la gamme StorSimple 8000 Hello est une fonctionnalité supplémentaire qui est fourni avec votre solution Microsoft Azure StorSimple. un appareil virtuel StorSimple Hello s’exécute sur un ordinateur virtuel dans un réseau virtuel Microsoft Azure, et vous pouvez l’utiliser tooback d’et cloner les données de vos hôtes. Ce didacticiel décrit comment toodeploy et de gérer un périphérique virtuel dans Azure et est applicable tooall hello pour les appareils virtuels en cours d’exécution la version mise à jour du logiciel 2 et inférieure.

#### <a name="virtual-device-model-comparison"></a>Comparaison des modèles d’appareils virtuels
Hello StorSimple périphérique virtuel n’est disponible dans les deux modèles, un 8010 standard (anciennement hello 1100) et une prime 8020 (introduite dans Update 2). Une comparaison de deux modèles de hello est sous forme de tableau ci-dessous.

| Modèle de l'appareil | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacité maximale** |30 To |64 To |
| **Microsoft Azure** |Standard_A3 (4 cœurs, 7 Go de mémoire) |Standard_DS3 (4 cœurs, 14 Go de mémoire) |
| **Compatibilité des versions** |Les versions exécutant une version antérieure de la mise à jour préliminaire 2 ou version ultérieure |Les versions exécutant Update 2 ou version ultérieure |
| **Disponibilité des régions** |Toutes les régions Azure |Toutes les régions Azure qui prennent en charge le stockage Premium et les machines virtuelles Azure DS3<br></br> Utilisez [cette liste](https://azure.microsoft.com/en-us/regions/services) toosee si les deux *virtuels > série DS* et *stockage > le stockage sur disque* sont disponibles dans votre région. |
| **Type de stockage** |Utilise le stockage Azure Standard pour les disques locaux<br></br> Découvrez comment trop[créer un compte de stockage Standard](../storage/common/storage-create-storage-account.md) |Utilise le stockage Azure Standard pour les disques locaux<sup>2</sup> <br></br>Découvrez comment trop[créer un compte de stockage Premium](../storage/common/storage-premium-storage.md) |
| **Aide relative à la charge de travail** |Récupération au niveau des éléments des fichiers à partir de sauvegardes |Scénarios de développement et de test dans le cloud, faible latence, charges de travail plus performantes <br></br>Appareil secondaire pour la récupération d’urgence |

<sup>1</sup> *anciennement hello 1100*.

<sup>2</sup> *à la fois hello 8010 et 8020 utiliser le stockage Standard de Azure pour hello cloud couche hello différence existe uniquement dans hello local de niveau dans les appareils hello*.

Cet article décrit étape par étape hello du déploiement d’un périphérique virtuel StorSimple dans Azure. À la fin de cet article, vous serez capable :

* Comprendre comment un appareil virtuel hello diffère de périphérique physique de hello.
* Être en mesure de toocreate et configurer un appareil virtuel hello.
* Connecter un appareil virtuel toohello.
* Découvrez comment toowork avec un appareil virtuel hello.

Ce didacticiel s’applique tooall périphériques hello StorSimple virtuels en cours d’exécution mise à jour 2 et versions ultérieures.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Comment un appareil virtuel hello diffère de périphérique physique de hello
un appareil virtuel StorSimple Hello est une version logicielle de StorSimple qui s’exécute sur un seul nœud dans une Machine virtuelle Microsoft Azure. Hello périphérique virtuel prend en charge la récupération d’urgence dans laquelle votre appareil physique n’est pas disponible et convient pour la récupération au niveau de l’élément à partir de sauvegardes, la récupération d’urgence, local et cloud dev et les scénarios de test.

#### <a name="differences-from-hello-physical-device"></a>Différences par rapport à l’unité physique de hello
Hello tableau suivant présente quelques différences clés entre un appareil virtuel StorSimple hello ou un périphérique physique StorSimple de hello.

|  | Appareil physique | Appareil virtuel |
| --- | --- | --- |
| **Emplacement** |Se trouve dans le centre de données hello. |S'exécute dans Azure. |
| **Interfaces réseau** |Comporte six interfaces réseau : de DATA 0 à DATA 5. |A une seule interface réseau : DATA 0. |
| **Inscription** |Enregistrés lors de l’étape de configuration hello. |L'inscription est une tâche distincte. |
| **Clé de chiffrement de données du service** |Régénérer sur l’appareil physique de hello et ensuite mettre à jour d’un appareil virtuel hello avec la nouvelle clé de hello. |Ne peut pas régénérer à partir d’un appareil virtuel hello. |

## <a name="prerequisites-for-hello-virtual-device"></a>Configuration requise pour un appareil virtuel hello
Hello sections suivantes expliquent hello configuration requise pour votre appareil virtuel StorSimple. Toodeploying préalable un appareil virtuel, passez en revue les hello [considérations relatives à l’aide d’un périphérique virtuel](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Conditions requises pour Azure
Avant de configurer un appareil virtuel hello, vous devez hello toomake suivant préparations dans votre environnement Azure :

* Pour un périphérique virtuel hello [configurer un réseau virtuel sur Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Si vous utilisez le stockage Premium, vous devez créer un réseau virtuel dans une région Azure qui prend en charge le stockage Premium. régions de Hello Premium storage sont des régions qui correspondent ligne toohello pour *le stockage sur disque* dans la liste des hello [Services Azure par région](https://azure.microsoft.com/en-us/regions/services).
* Il est serveur DNS recommandé toouse hello par défaut fournie par Azure au lieu de spécifier le nom de votre propre serveur DNS. Si le nom de votre serveur DNS n’est pas valide ou si le serveur DNS de hello n’est pas en mesure de tooresolve des adresses IP correctement, la création d’un appareil virtuel hello hello échoue.
* Les options de point à site et de site à site sont facultatives (non obligatoires). Si vous le souhaitez, vous pouvez configurer ces options pour des scénarios plus avancés.
* Vous pouvez créer [des Machines virtuelles Azure](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (serveurs hôtes) dans un réseau virtuel hello qui peut utiliser des volumes de hello exposées par un appareil virtuel hello. Ces serveurs doivent remplir hello suivant les exigences :                             

  * Il doit s’agir de machines virtuelles Windows ou Linux sur lesquelles l’initiateur iSCSI est installé.
  * Être en cours d’exécution dans hello même réseau virtuel que les périphériques virtuels hello.
  * Être en mesure de tooconnect toohello de cible iSCSI de l’appareil virtuel de hello via hello adresse IP interne du périphérique virtuel de hello.
* Assurez-vous que vous avez configuré la prise en charge pour iSCSI et cloud le trafic sur hello même réseau virtuel.

#### <a name="storsimple-requirements"></a>Conditions requises pour StorSimple
Rendre hello après les mises à jour tooyour Azure StorSimple service avant de créer un périphérique virtuel :

* Ajouter [enregistrements de contrôle d’accès](storsimple-manage-acrs.md) pour hello machines virtuelles que vous allez les serveurs hôtes de toobe pour votre appareil virtuel.
* Utilisez un [compte de stockage](storsimple-manage-storage-accounts.md#add-a-storage-account) Bonjour même région que le périphérique virtuel de hello. Des comptes de stockage dans différentes régions peuvent entraîner une dégradation des performances. Vous pouvez utiliser un compte Standard ou Premium stockage avec un appareil virtuel hello. Plus d’informations sur la façon de toocreate un [compte de stockage Standard](../storage/common/storage-create-storage-account.md) ou un [compte de stockage Premium](../storage/common/storage-premium-storage.md)
* Utilisez un autre compte de stockage pour la création d’un appareil virtuel à partir de hello celui utilisé pour vos données. À l’aide du même compte de stockage peut entraîner une dégradation des performances de hello.

Assurez-vous que vous avez hello suivant informations avant de commencer :

* Votre compte avec les informations d'identification d'accès au portail Azure Classic.
* Une copie de la clé de chiffrement de données de service hello à partir de votre appareil physique.

## <a name="create-and-configure-hello-virtual-device"></a>Créer et configurer un appareil virtuel hello
Avant d’effectuer ces procédures, assurez-vous que vous avez rempli hello [configuration requise pour un appareil virtuel hello](#prerequisites-for-the-virtual-device).

Après avoir créé un réseau virtuel, configuré un service Gestionnaire StorSimple et inscrit votre périphérique physique StorSimple avec le service de hello, vous pouvez utiliser hello suivant les étapes toocreate et configurer un appareil virtuel StorSimple.

### <a name="step-1-create-a-virtual-device"></a>Étape 1 : création d'un appareil virtuel
Effectuer hello suivant un appareil virtuel étapes toocreate hello StorSimple.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Si la création d’un appareil virtuel hello hello échoue dans cette étape, vous ne pouvez pas avoir toohello de connectivité Internet. Pour plus d’informations, consultez trop[résoudre les problèmes de connectivité Internet](#troubleshoot-internet-connectivity-errors) lors de la création d’un périphérique virtuel.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Étape 2 : Configurer et inscrire un appareil virtuel hello
Avant de commencer cette procédure, assurez-vous que vous disposez d’une copie de la clé de chiffrement de données de service hello. Hello clé de chiffrement de données de service a été créé lorsque vous avez configuré votre premier appareil StorSimple et si vous avez demandé toosave dans un emplacement sécurisé. Si vous n’avez pas une copie de la clé de chiffrement de données de service hello, vous devez contacter le Support technique de Microsoft pour obtenir une assistance.

Effectuer hello suivant les étapes tooconfigure et inscrire votre appareil virtuel StorSimple.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Étape 3 : Paramètres de configuration (facultatif) modifier hello
Hello section suivante décrit des paramètres de configuration de périphérique de hello nécessaires pour un appareil virtuel StorSimple hello si vous souhaitez toouse CHAP, gestionnaire d’instantanés StorSimple ou modifiez le mot de passe administrateur de l’appareil hello.

#### <a name="configure-hello-chap-initiator"></a>Configurer l’initiateur CHAP de hello
Ce paramètre contient les informations d’identification de hello votre appareil virtuel (cible) attend des initiateurs de hello (serveurs) qui tentent de volumes de hello tooaccess. Hello initiateurs fournissent un nom d’utilisateur et un tooidentify de mot de passe CHAP eux-mêmes tooyour appareil au cours de cette authentification. Pour des instructions détaillées, consultez trop[configurer CHAP pour votre appareil](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurer la cible CHAP de hello
Ce paramètre contient les informations d’identification de hello votre appareil virtuel utilise lorsqu’un initiateur CHAP demande une authentification mutuelle ou bidirectionnelle. Votre appareil virtuel utilisera un nom d’utilisateur et tooidentify de mot de passe CHAP inversé lui-même toohello initiateur pendant le processus d’authentification. Notez que les paramètres CHAP cibles sont des paramètres globaux. Lorsqu’ils sont appliqués, tous les hello volumes connectés toohello stockage périphérique virtuel utilisent l’authentification CHAP. Pour des instructions détaillées, consultez trop[configurer CHAP pour votre appareil](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurer le mot de passe de gestionnaire d’instantanés StorSimple hello
Gestionnaire d’instantanés StorSimple logiciel réside sur l’hôte Windows et permet aux administrateurs toomanage les sauvegardes de votre appareil StorSimple dans l’écran hello locaux et les instantanés cloud.

> [!NOTE]
> Pour les périphériques virtuels hello, votre hôte Windows est une machine virtuelle Azure.
>
>

Lorsque vous configurez un appareil Bonjour Gestionnaire d’instantanés StorSimple, vous serez invité tooprovide hello StorSimple appareil IP adresse et le mot de passe tooauthenticate votre périphérique de stockage. Pour des instructions détaillées, consultez trop[mot de passe de configurer le Gestionnaire d’instantanés StorSimple](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Mot de passe de l’administrateur d’appareil modification hello
Lorsque vous utilisez hello Windows PowerShell interface tooaccess hello périphérique virtuel, vous serez requis tooenter un mot de passe administrateur. Sécurité hello de vos données, vous êtes toochange requis ce mot de passe avant un appareil virtuel hello peut être utilisé. Pour des instructions détaillées, consultez trop[mot de passe administrateur de périphérique configurer](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Se connecter à distance un appareil virtuel toohello
APPAREIL virtuel de l’accès à distance tooyour via l’interface Windows PowerShell de hello n’est pas activé par défaut. Vous devez tout d’abord les tooenable de gestion à distance sur un appareil virtuel hello et puis l’activer sur le client hello qui sera utilisé tooaccess votre appareil virtuel.

tooconnect de processus en deux étapes Hello à distance est détaillée ci-dessous.

### <a name="step-1-configure-remote-management"></a>Étape 1 : configurer la gestion à distance
Effectuer hello suivant de gestion à distance de tooconfigure étapes pour votre appareil virtuel StorSimple.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Étape 2 : Accès à distance un appareil virtuel hello
Une fois que vous avez activé la gestion à distance sur la page de configuration de périphérique StorSimple hello, vous pouvez utiliser Windows PowerShell remoting tooconnect toohello périphérique virtuel à partir d’un autre ordinateur virtuel à l’intérieur de hello même réseau virtuel. par exemple, vous pouvez vous connecter à partir de l’hôte hello machine virtuelle que vous avez configuré et utilisé tooconnect iSCSI. Dans la plupart des déploiements, est déjà ouverte une tooaccess de point de terminaison public votre hôte de machine virtuelle que vous pouvez utiliser pour accéder à un appareil virtuel hello.

> [!WARNING]
> **Pour renforcer la sécurité, nous recommandons vivement que vous utilisez HTTPS lors de la connexion de points de terminaison toohello et puis supprimez les points de terminaison hello après avoir terminé votre session à distance de PowerShell.**
>
>

Vous devez suivre les procédures hello [connexion à distance de l’appareil StorSimple tooyour](storsimple-remote-connect.md) tooset une communication à distance pour votre appareil virtuel.

## <a name="connect-directly-toohello-virtual-device"></a>Se connecter directement toohello un appareil virtuel
Vous pouvez également vous connecter directement toohello un appareil virtuel. Si vous souhaitez tooconnect directement toohello périphérique virtuel à partir d’un autre ordinateur en dehors de réseau virtuel de hello ou l’environnement de Microsoft Azure hello extérieur, vous devez toocreate des points de terminaison supplémentaires comme décrit dans la procédure de hello.

Effectuer hello suivant les étapes toocreate un point de terminaison public sur un appareil virtuel hello.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

Nous recommandons que vous vous connectez à partir d’un autre ordinateur virtuel à l’intérieur de hello virtuel même réseau, car cette pratique réduit le nombre de hello de points de terminaison publics sur votre réseau virtuel. Lorsque vous utilisez cette méthode, vous suffit de vous connecter toohello virtuels via une session Bureau à distance, puis configurez cet ordinateur virtuel pour une utilisation comme vous le feriez pour n’importe quel autre client Windows sur un réseau local. Vous n’avez pas besoin de numéro de port public tooappend hello, car le port de hello est déjà connu.

## <a name="work-with-hello-storsimple-virtual-device"></a>Travailler avec un appareil virtuel StorSimple hello
Maintenant que vous avez créé et configuré un appareil virtuel StorSimple hello, vous êtes prêt toostart son utilisation. Vous pouvez travailler avec des conteneurs de volumes, des volumes et des stratégies de sauvegarde sur un périphérique virtuel comme vous le feriez sur un appareil StorSimple physique ; Hello seule différence est que vous devez toomake assurer que vous sélectionnez un appareil virtuel hello à partir de votre liste de périphériques. Consultez trop[utiliser hello StorSimple Manager service toomanage un appareil virtuel](storsimple-manager-service-administration.md) pour obtenir des procédures de gestion différentes tâches pour un appareil virtuel hello de hello.

Hello sections suivantes décrivent certaines des différences hello que vous rencontrerez lorsque vous travaillez avec un appareil virtuel hello.

### <a name="maintain-a-storsimple-virtual-device"></a>Maintenance d’un appareil virtuel StorSimple
Car il s’agit d’un dispositif logiciel, le mise à jour pour un appareil virtuel hello est minime lorsque comparées toomaintenance pour les appareils physiques hello. Vous avez hello options suivantes :

* **Mises à jour logicielles** – vous pouvez afficher la date de hello hello logiciel a été dernier mis à jour, ainsi que les messages d’état de mise à jour. Vous pouvez utiliser hello **analyse des mises à jour** bouton bas hello hello page tooperform une analyse manuelle si vous souhaitez toocheck pour les nouvelles mises à jour. Si les mises à jour sont disponibles, cliquez sur **installer les mises à jour** tooinstall. Étant donné seulement une seule interface sur un appareil virtuel hello, cela signifie qu’il y aura une interruption de service légère lorsque les mises à jour sont appliquées. un appareil virtuel Hello s’arrêter, puis redémarre (si nécessaire) tooapply les mises à jour qui ont été publiées. Pour une procédure pas à pas, consultez trop[mettre à jour votre appareil](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Package de support** : vous pouvez créer et télécharger un toohelp de package de prise en charge de Support technique de Microsoft résoudre les problèmes avec votre appareil virtuel. Pour une procédure pas à pas, consultez trop[créer et gérer un package de prise en charge](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Comptes de stockage d’un appareil virtuel
Comptes de stockage sont créés pour une utilisation par le service StorSimple Manager hello, par périphérique virtuel de hello et par unité physique de hello. Lorsque vous créez vos comptes de stockage, nous vous recommandons d’utiliser une région identificateur hello nom convivial toohelp garantir cette région de hello est cohérente dans tous les composants du système hello. Pour un appareil virtuel, il est important que tous les composants de hello hello des problèmes de performances tooprevent même région.

Pour une procédure pas à pas, consultez trop[ajouter un compte de stockage](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Désactivation d’un appareil virtuel StorSimple
La désactivation d’un périphérique virtuel supprime hello VM et ressources hello créés lors de sa préparation. Une fois un appareil virtuel hello est désactivé, il ne peut pas être restauré tooits l’état précédent. Avant de désactiver un appareil virtuel hello, assurez-vous que toostop ou supprimer des clients et les hôtes qui en dépendent.

La désactivation d’un périphérique virtuel renvoie hello suivant des actions :

* un appareil virtuel Hello est supprimé.
* disque de Hello du système d’exploitation et des disques de données créés pour un appareil virtuel hello sont supprimés.
* service de Hello hébergé et le réseau virtuel créé lors de la configuration sont conservés. Si vous ne les utilisez pas, vous devez les supprimer manuellement.
* Les instantanés cloud créés pour un appareil virtuel hello sont conservés.

Pour une procédure pas à pas, consultez trop[désactiver et supprimer votre appareil StorSimple](storsimple-deactivate-and-delete-device.md).

Dès que le périphérique virtuel de hello est indiquée comme étant désactivée sur la page du service Gestionnaire StorSimple hello, vous pouvez supprimer un appareil virtuel hello à partir de la liste des appareils sur hello **périphériques** page.

### <a name="start-stop-and-restart-a-virtual-device"></a>Démarrage, arrêt et redémarrage d’un appareil virtuel
Contrairement aux appareils physiques StorSimple de hello, n’est pas alimenté alimentation toopush bouton sur un périphérique virtuel StorSimple. Toutefois, il peut arriver dans lequel vous avez besoin de toostop et que vous redémarrez un appareil virtuel hello. Par exemple, certaines mises à jour peuvent nécessiter que hello que machine virtuelle redémarré le processus de mise à jour toofinish hello. Hello plus simple pour vous toostart, arrêt et redémarrage d’un périphérique virtuel est toouse hello Console de gestion des ordinateurs virtuels.

Lorsque vous examinez hello Console de gestion, état du périphérique virtuel hello est **en cours d’exécution** , car il est démarré par défaut après sa création. Vous pouvez démarrer, arrêter et redémarrer une machine virtuelle à tout moment.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Réinitialiser les valeurs par défaut toofactory
Si vous décidez que vous souhaitiez toostart sur avec votre appareil virtuel, simplement désactiver et supprimer et créer un nouveau. Lorsque votre appareil physique est réinitialisée, comme votre nouveau périphérique virtuel n’aura pas les mises à jour installées ; Par conséquent, vous toocheck que les mises à jour avant de l’utiliser.

## <a name="fail-over-toohello-virtual-device"></a>Basculer d’un appareil virtuel toohello
La récupération d’urgence (DR) est un des scénarios clés hello hello StorSimple périphérique virtuel a été conçu pour. Dans ce scénario, hello périphérique physique StorSimple ou centre de données entier peut ne pas être disponible. Heureusement, vous pouvez utiliser des opérations toorestore périphérique virtuel dans un autre emplacement. Au cours de la récupération d’urgence, les conteneurs de volumes hello à partir de l’appareil source de hello changent de propriétaire et sont transférés toohello un appareil virtuel. Hello conditions préalables pour la récupération d’urgence sont que les périphériques virtuels hello a été créé et configuré tous les volumes hello dans le conteneur de volume hello ont été mis hors connexion et conteneur de volume hello est associé à un instantané cloud.

> [!NOTE]
> * Lorsque vous utilisez un appareil virtuel en tant que périphérique secondaire de hello pour la récupération d’urgence, gardez à l’esprit que hello 8010 a 30 To de stockage Standard et 8020 a 64 To de stockage Premium. Hello supérieur capacité 8020 périphérique virtuel peut être plus adapté à un scénario de récupération d’urgence.
> * Vous ne pouvez pas le basculement ou clone à partir d’un périphérique exécutant Update 2 tooa appareil exécutant le 1 logiciel avant mise à jour. Vous pouvez toutefois basculer un périphérique qui exécute le périphérique de tooa 2 de la mise à jour 1 de mise à jour (1.1 ou 1.2) en cours d’exécution
>
>

Pour une procédure pas à pas, consultez trop[périphérique virtuel de basculement tooa](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Arrêtez ou supprimez un appareil virtuel hello
Si vous déjà configuré et utilisé un virtuel StorSimple appareil souhaitiez mais désormais toostop accumuler de frais de calcul de son utilisation, vous pouvez arrêter un appareil virtuel hello. Arrêt d’un appareil virtuel hello ne supprime pas son système d’exploitation ou les disques de données dans le stockage. Elle n’arrête pas les frais accumulés sur votre abonnement, mais les frais de stockage pour hello du système d’exploitation et les disques de données continuent.

Si vous supprimez ou arrêtez un appareil virtuel hello, il apparaît comme **hors connexion** sur page de périphériques hello Hello service StorSimple Manager. Vous pouvez choisir toodeactivate ou supprimer des appareils de hello si vous souhaitez également toodelete sauvegardes hello créés par un appareil virtuel hello. Pour plus d’informations, consultez [Désactiver et supprimer un appareil StorSimple](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Résolution des problèmes de connectivité Internet
Au cours de hello la création d’un périphérique virtuel, s’il n’existe aucun toohello de connectivité Internet, étape de la création de hello échoue. tootroubleshoot si l’échec de hello est en raison de la connectivité Internet, effectuez hello Bonjour portail classique Azure comme suit :

1. Créez une machine virtuelle Windows Server 2012 dans Azure. Cet ordinateur virtuel doit utiliser hello même compte de stockage, réseau virtuel et le sous-réseau que celui utilisé par votre appareil virtuel. Si vous disposez déjà d’un hôte Windows Server à l’aide d’Azure hello même compte de stockage, réseau virtuel et sous-réseau, vous pouvez également l’utiliser la connectivité Internet tootroubleshoot hello.
2. Connectez-vous à distance virtuels hello créé Bonjour précédant l’étape.
3. Ouvrez une fenêtre de commande à l’intérieur de machine virtuelle de hello (Win + R, puis tapez `cmd`).
4. Exécutez hello suivant cmd invite hello.

    `nslookup windows.net`
5. Si `nslookup` échoue, Échec de connectivité Internet empêche un appareil virtuel hello lors de l’inscription toohello le service StorSimple Manager.
6. Apportez les modifications de hello requis tooensure de réseau virtuel tooyour qui hello périphérique virtuel est en mesure de tooaccess sites Azure tels que « windows.net ».

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser hello StorSimple Manager service toomanage un appareil virtuel](storsimple-manager-service-administration.md).
* Comprendre comment trop[restaurer un volume StorSimple à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md).
