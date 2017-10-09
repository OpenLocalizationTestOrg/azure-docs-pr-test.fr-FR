---
title: aaaOverview Azure IoT bord | Documents Microsoft
description: "Décrit hello concepts architecturaux clés dans Azure IoT Edge tels que les passerelles, les modules et les services Broker."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Concepts architecturaux d’Azure IoT Edge

Avant de consulter des exemples de code ou créer votre propre passerelle de champ à l’aide de IoT Edge, vous devez comprendre hello principaux concepts qui sous-tendent l’architecture hello du bord de IoT.

## <a name="iot-edge-modules"></a>Modules IoT Edge

Vous créez une passerelle avec Azure IoT Edge en créant et en assemblant des *modules IoT Edge*. Utilisent des modules *messages* tooexchange des données entre eux. Un module reçoit un message, effectue une action sur celui-ci, éventuellement transforme un nouveau message et le publie ensuite pour les autres tooprocess modules. Certains modules peuvent uniquement produire de nouveaux messages et ne jamais traiter les messages entrants. Une chaîne de modules crée un pipeline de traitement des données avec chaque module effectuant une transformation sur des données à un moment donné de ce pipeline hello.

![Chaîne de modules dans la passerelle créée avec Azure IoT Edge][1]

IoT bord contient hello suivant des composants :

* Des modules pré-écrits qui exécutent des fonctions de passerelles courantes.
* interfaces Hello un développeur peuvent utiliser toowrite des modules personnalisés.
* Hello toodeploy nécessaire d’infrastructure et d’exécuter un ensemble de modules.

Hello SDK fournit une couche d’abstraction qui vous permet de toobuild passerelles toorun sur différentes plateformes et les systèmes d’exploitation.

![Couche d’abstraction Azure IoT Edge][2]

## <a name="messages"></a>Messages

Bien que vous réfléchissez à passer de modules, messages tooeach autres est un moyen pratique de tooconceptualize fonctionnement d’une passerelle, il ne pas refléter correctement ce qui se passe. Les modules IoT bord utilisent un toocommunicate broker entre eux. Les modules publier broker toohello de messages (à l’aide de modèles de messagerie telles que les bus ou la publication/abonnement) et laisser ensuite hello broker itinéraire hello message toohello modules tooit connecté.

Un module utilise hello **Broker_Publish** toopublish toohello message broker de la fonction. service broker de Hello remet module tooa de messages en appelant une fonction de rappel. Un message se compose d'un ensemble de propriétés de clés/valeurs et d’un contenu transmis sous forme d’un bloc de mémoire.

![rôle Hello Hello Broker dans Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a>Routage et filtrage des messages

Il existe deux façons de modules de IoT bord corrects toodirect messages toohello :

* Vous pouvez passer un ensemble de liens peuvent être passés toohello broker afin que service broker de hello sache source de hello et le récepteur pour chaque module.
* Un module peut filtrer sur les propriétés de hello de message de type hello.

Un module doit agir uniquement un message si le message de type hello est destiné. Les liens et le filtrage des messages permettent de créer efficacement un pipeline de messages.

## <a name="next-steps"></a>Étapes suivantes

consultez de ces concepts appliqués dans un exemple, vous pouvez exécuter, toosee [architecture Explorer de Azure IoT Edge][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md