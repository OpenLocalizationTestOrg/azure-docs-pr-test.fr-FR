---
title: aaaUse hello toocreate portail Azure un IoT Hub | Documents Microsoft
description: "Comment toocreate, gérer et supprimer des hubs Azure IoT via hello portail Azure. Inclut des informations sur les niveaux de tarification, l’évolutivité, la sécurité et la configuration de la messagerie."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Créez un IoT hub à l’aide de hello portail Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Cet article explique :

* Comment toofind hello service IoT Hub Bonjour portail Azure.
* Comment toocreate et gérer les IoT hubs.

## <a name="where-toofind-hello-iot-hub-service"></a>Où toofind hello IoT Hub service

Vous pouvez trouver hello IoT Hub service Bonjour emplacements dans le portail de hello suivants :

* Choisissez **+ Nouveau**, puis **Internet des objets**.
* Bonjour Marketplace, choisissez **Internet of Things**.

## <a name="create-an-iot-hub"></a>Créer un hub IoT

Vous pouvez créer un IoT hub à l’aide de hello méthodes suivantes :

* Hello **+ nouveau** option ouvre le panneau de hello illustré hello suivant capture d’écran. étapes Hello pour la création de hub IoT de hello via cette méthode et marketplace de hello sont identiques.
* Bonjour Marketplace, choisissez **créer** Panneau de hello tooopen illustré hello suivant capture d’écran.

Hello sections suivantes décrivent des hello plusieurs étapes toocreate un IoT hub :

### <a name="choose-hello-name-of-hello-iot-hub"></a>Choisissez le nom hello de hub IoT de hello

toocreate un hub IoT, vous devez nommer hub IoT de hello. Le nom doit être unique parmi tous les hubs IoT.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Choisissez hello niveau tarifaire

Vous pouvez choisir entre quatre niveaux : **Gratuit**, **Standard S1**, **Standard S2** et**Standard S3**. gratuit Hello permet uniquement de 500 périphériques toobe connecté toohello IoT hub et too8, 000 messages par jour.

**Standard S1**: édition de hello S1 d’utilisation pour les solutions IoT avec un grand nombre de périphériques que chaque générer de petites quantités de données. Chaque unité de l’édition de hello S1 permet des too400, 000 messages par jour sur tous les périphériques connectés.

**Standard S2**: édition de hello S2 d’utilisation pour les solutions IoT dans lequel les appareils générer de grandes quantités de données. Chaque unité de l’édition de S2 hello permet des too6 millions de messages par jour entre tous les périphériques connectés.

**Standard S3**: édition de hello S3 d’utilisation pour les solutions IoT qui génèrent de grandes quantités de données. Chaque unité de l’édition de S3 hello permet des too300 millions de messages par jour entre tous les périphériques connectés.

![][4]

> [!NOTE]
> IoT Hub ne permet qu’un hub gratuit par abonnement Azure.

### <a name="iot-hub-units"></a>Unités de hub IoT

nombre de Hello de messages autorisés par unité par jour dépend de la tarification de votre concentrateur. Par exemple, si vous souhaitez hello en entrée toosupport de hub IoT de 700 000 messages, vous choisissez deux unités de couche S1.

### <a name="device-toocloud-partitions-and-resource-group"></a>Partitions de toocloud de périphérique et le groupe de ressources

Vous pouvez modifier le nombre de hello de partitions pour un hub IoT. nombre de partitions par défaut de Hello est 4, vous pouvez choisir un nombre différent à partir de la liste déroulante de hello.

Vous n’avez pas besoin tooexplicitly créer un groupe de ressources vide. Lorsque vous créez une ressource, vous pouvez choisir soit toocreate une nouvelle, ou utiliser un groupe de ressources existant.

![][5]

### <a name="choose-subscription"></a>Choisir un abonnement

IoT Hub Azure automatiquement hello de listes de compte d’utilisateur des abonnements Azure hello est lié. Vous pouvez choisir hello abonnement Azure tooassociate hello IoT hub pour.

### <a name="choose-hello-location"></a>Choisissez l’emplacement de hello

option d’emplacement Hello fournit une liste des régions hello où IoT Hub n’est disponible.

### <a name="create-hello-iot-hub"></a>Créez hello IoT hub

Une fois toutes les étapes précédentes terminées, vous pouvez créez hello IoT hub. Cliquez sur **créer** toostart hello principaux processus toocreate et déployer hello IoT hub avec options hello choisis.

IoT hub de quelques minutes toocreate hello peut prendre comme le temps requis pour hello principal déploiement toorun sur des serveurs hello emplacement approprié.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Modifier les paramètres de hello de hub IoT de hello

Vous pouvez modifier les paramètres de hello d’un hub IoT existant après sa création à partir de hello Panneau de IoT Hub.

![][8]

**Stratégies d’accès partagé**: ces stratégies définissent des autorisations de hello pour les appareils et services tooconnect tooIoT Hub. Vous pouvez accéder à ces stratégies en cliquant sur **Stratégies d’accès partagé** sous **Général**. Dans ce panneau, vous pouvez soit modifier les stratégies existantes, soit ajouter une nouvelle stratégie.

### <a name="create-a-policy"></a>Création d’une stratégie

* Cliquez sur **ajouter** tooopen un panneau. Ici vous pouvez entrer le nom de la nouvelle stratégie hello et autorisations hello que vous souhaitez tooassociate avec cette stratégie, comme indiqué dans les éléments suivants de hello figure :

    Il existe plusieurs autorisations qui peuvent être associées à ces stratégies partagées. Hello **lecture du Registre** et **de Registre** accordent des stratégies en lecture et Registre des identités de toohello droits accès en écriture. Choix d’option d’écriture hello automatiquement choisit hello lire les options.

    Hello **Service de se connecter** stratégie accorde l’autorisation tooaccess points de terminaison de service telles que **réception appareil-à-cloud**. Hello **connexion de périphérique** stratégie accorde des autorisations pour envoyer et recevoir des messages à l’aide de points de terminaison hello IoT Hub côté appareil.

* Cliquez sur **créer** tooadd nouvellement créé la liste de stratégie toohello existante.

![][10]

## <a name="endpoints"></a>Points de terminaison

Cliquez sur **points de terminaison** toodisplay une liste de points de terminaison de hub IoT hello que vous souhaitez modifier. Il existe deux types de points de terminaison : points de terminaison qui sont intégrées à un hub IoT de hello et que vous ajoutez toohello IoT hub après sa création.

![][11]

### <a name="built-in-endpoints"></a>Points de terminaison intégrés

Il existe deux points de terminaison intégrés : **Cloud toodevice commentaires** et **événements**.

* **Cloud toodevice commentaires** paramètres : ce paramètre n’a deux sous-Paramètres : **Cloud tooDevice TTL** (time-to-live) et **durée de rétention** (en heures) pour les messages de type hello. Lorsque votre premier créez un IoT hub, ces deux paramètres ont par défaut hello d’une heure. tooadjust ces paramètres, utilisez les curseurs hello ou tapez les valeurs hello.
* Paramètres **Événements** : ils présentent plusieurs configurations secondaires, qui sont pour certaines en lecture seule. Hello suivant liste décrit ces paramètres :

  * **Partitions**: une valeur par défaut est définie lorsque hello IoT hub est créé. Vous pouvez modifier le nombre de hello de partitions avec ce paramètre.

  * **Nom de Hub compatible avec l’événement et le point de terminaison**: lorsque hello IoT concentrateur est créé, un concentrateur d’événements est créé en interne que vous pouvez peut-être accéder à toounder certaines circonstances. Vous ne pouvez pas personnaliser les valeurs nom et le point de terminaison hello compatible concentrateur d’événements, mais vous pouvez les copier en cliquant sur **copie**.

  * **Durée de rétention**: tooone jour la valeur par défaut mais vous pouvez modifier à l’aide de la liste déroulante de hello. Cette valeur est en jours pour le paramètre de périphérique dans le cloud hello.

  * **Groupes de consommateurs**: groupes de consommateurs activer plusieurs messages tooread de lecteurs indépendamment de hub IoT de hello. Chaque hub IoT est créé avec un groupe de consommateurs par défaut. Toutefois, vous pouvez ajouter ou supprimer des concentrateurs d’IoT tooyour groupes consommateur à l’aide de ce paramètre.

  > [!NOTE]
  > groupe de consommateurs Hello par défaut ne peut pas être modifié ou supprimé.

### <a name="custom-endpoints"></a>Points de terminaison personnalisés

Vous pouvez ajouter des points de terminaison personnalisés sur votre IoT hub à l’aide du portail de hello. À partir de hello **points de terminaison** panneau, cliquez sur **ajouter** à Bonjour tooopen supérieur Bonjour **ajouter le point de terminaison** panneau. Entrez les informations de hello requis, puis cliquez sur **OK**. Votre point de terminaison personnalisé est maintenant répertoriée dans hello principal **points de terminaison** panneau.

![][13]

Pour en savoir plus sur les points de terminaison personnalisés, consultez [Référence - Points de terminaison IoT Hub][lnk-devguide-endpoints].

## <a name="routes"></a>Itinéraires

Cliquez sur **itinéraires** toomanage comment IoT Hub distribue vos messages appareil-à-cloud.

![][14]

Vous pouvez ajouter le concentrateur de IoT itinéraires tooyour en cliquant sur **ajouter** haut hello hello **itinéraires*** panneau, la saisie des informations de hello requis, puis cliquez sur **OK**. L’itinéraire est ensuite répertorié dans hello principal **itinéraires** panneau. Vous pouvez modifier un itinéraire en cliquant dessus dans la liste hello des itinéraires. tooenable un itinéraire, cliquez dessus dans la liste hello des itinéraires et définir hello **activé** basculer trop**hors**. modification de hello toosave, cliquez sur **OK** bas hello du Panneau de hello.

![][15]

## <a name="pricing-and-scale"></a>Tarification et mise à l'échelle

Hello tarification d’un hub IoT existant peut être modifiée via hello **tarification** paramètres, par hello suivant des exceptions :

* Dans l’implémentation actuelle de hello, un IoT hub avec une référence SKU libre ne peut pas modifier tooone niveaux de hello payé références (SKU), ou vice versa.
* Il ne doit contenir qu’un seul hub IoT de niveau gratuit hello abonnement Azure.

![][12]

Vous pouvez déplacer à partir d’un niveau supérieur de toolower uniquement lorsque le nombre hello de messages envoyés dans la journée dépasse le quota hello pour le niveau inférieur de hello. Par exemple, si nombre hello de messages par jour dépasse 400 000, puis hello couche pour hello IoT hub peut être modifié. Toutefois, si vous modifiez le niveau de S1 toohello hub IoT de hello est limitée pour ce jour.

## <a name="delete-hello-iot-hub"></a>Supprimer le hello IoT hub

Vous pouvez parcourir toohello IoT hub souhaité en cliquant sur toodelete **Parcourir**, et puis en choisissant hello toodelete de concentrateur approprié. toodelete hello IoT hub, cliquez sur hello **supprimer** situé sous le nom de hub IoT hello.

## <a name="next-steps"></a>Étapes suivantes

Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :

* [Gérer en bloc des appareils IoT][lnk-bulk]
* [Métriques d’IoT Hub][lnk-metrics]
* [Surveillance des opérations][lnk-monitor]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]
* [Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
