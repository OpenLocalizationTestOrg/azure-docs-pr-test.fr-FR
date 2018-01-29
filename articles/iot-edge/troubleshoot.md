---
title: "Résoudre les problèmes d’Azure IoT Edge | Microsoft Docs"
description: "Résoudre les problèmes courants et découvrir les compétences de dépannage requises pour Azure IoT Edge"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 12/15/2017
ms.topic: tutorial
ms.service: iot-edge
ms.custom: mvc
ms.openlocfilehash: 3f61f0bf8234e747ae38146d1a5ea030e3163fa3
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/21/2017
---
# <a name="common-issues-and-resolutions-for-azure-iot-edge"></a>Problèmes courants et résolutions pour Azure IoT Edge

Si vous rencontrez des problèmes lors de l’exécution d’Azure IoT Edge dans votre environnement, consultez cet article qui vous guidera pour la résolution des problèmes. 

## <a name="standard-diagnostic-steps"></a>Étapes de diagnostic standard 

Lorsque vous rencontrez un problème, obtenez des informations supplémentaires sur l’état de votre appareil IoT Edge en examinant les journaux du conteneur et les messages transitant par l’appareil. Utilisez les commandes et les outils de cette section pour recueillir des informations. 

* Examinez les journaux des conteneurs docker pour détecter les problèmes. Commencez par les conteneurs déployés, puis examinez les conteneurs qui composent le runtime IoT Edge : Edge Agent et Edge Hub. En général, les journaux Edge Agent fournissent des informations sur le cycle de vie de chaque conteneur. Les journaux Edge Hub fournissent des informations sur la messagerie et le routage. 

   ```cmd
   docker logs <container name>
   ```

* Affichez les messages acheminés via Edge Hub et recueillez des insights sur les mises à jour des propriétés de l’appareil à l’aide de journaux détaillés issus des conteneurs du runtime.

   ```cmd
   iotedgectl setup --runtime-log-level DEBUG
   ```

* Si vous rencontrez des problèmes de connectivité, examinez les variables d’environnement de votre appareil edge, comme la chaîne de connexion de votre appareil :

   ```cmd
   docker exec edgeAgent printenv
   ```

Vous pouvez également vérifier les messages envoyés entre IoT Hub et les appareils IoT Edge. Affichez ces messages à l’aide de l’extension [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) pour Visual Studio Code. Pour plus d’informations, consultez [Handy tool when you develop with Azure IoT](https://blogs.msdn.microsoft.com/iotdev/2017/09/01/handy-tool-when-you-develop-with-azure-iot/) (Outil pratique pour le développement avec Azure IoT).

Après avoir examiné les journaux et les messages pour obtenir plus d’informations, vous pouvez également essayer de redémarrer le runtime Azure IoT Edge :

   ```cmd
   iotedgectl restart
   ```

## <a name="edge-agent-stops-after-about-a-minute"></a>Edge Agent s’arrête après environ une minute

Edge Agent démarre et s’exécute avec succès pendant environ une minute, puis s’arrête. Les journaux indiquent qu’Edge Agent tente de se connecter au IoT Hub via AMQP, puis essaie environ 30 secondes plus tard de se connecter à l’aide d’AMQP sur websocket. Lorsque cette tentative échoue, Edge Agent se ferme. 

Exemples de journaux Edge Agent :

```
2017-11-28 18:46:19 [INF] - Starting module management agent. 
2017-11-28 18:46:19 [INF] - Version - 1.0.7516610 (03c94f85d0833a861a43c669842f0817924911d5) 
2017-11-28 18:46:19 [INF] - Edge agent attempting to connect to IoT Hub via AMQP... 
2017-11-28 18:46:49 [INF] - Edge agent attempting to connect to IoT Hub via AMQP over WebSocket... 
```

### <a name="root-cause"></a>Cause racine
Une configuration de mise en réseau sur le réseau hôte empêche Edge Agent d’atteindre le réseau. L’agent tente de se connecter via AMQP (port 5671) en premier. En cas d’échec, il essaie via les websocket (port 443).

Le runtime IoT Edge configure un réseau pour chacun des modules sur lesquels communiquer. Sur Linux, ce réseau est un réseau de pont. Sur Windows, il utilise NAT. Ce problème est plus courant sur les appareils Windows utilisant des conteneurs Windows qui utilisent le réseau NAT. 

### <a name="resolution"></a>Résolution :
Assurez-vous qu’il existe un itinéraire vers Internet pour les adresses IP affectées à ce réseau pont/NAT. Parfois, une configuration VPN sur l’hôte remplace le réseau IoT Edge. 

## <a name="edge-hub-fails-to-start"></a>Edge Hub ne parvient pas à démarrer

Edge Hub ne parvient pas à démarrer et le message suivant est consigné dans les journaux : 

```
One or more errors occurred. 
(Docker API responded with status code=InternalServerError, response=
{\"message\":\"driver failed programming external connectivity on endpoint edgeHub (6a82e5e994bab5187939049684fb64efe07606d2bb8a4cc5655b2a9bad5f8c80): 
Error starting userland proxy: Bind for 0.0.0.0:443 failed: port is already allocated\"}\n) 
```

### <a name="root-cause"></a>Cause racine
Un autre processus de l’ordinateur hôte est lié au port 443. Edge Hub mappe les ports 5671 et 443 pour une utilisation dans les scénarios de passerelle. Ce mappage de port échoue si un autre processus est déjà lié à ce port. 

### <a name="resolution"></a>Résolution :
Recherchez et arrêtez le processus qui utilise le port 443. Ce processus est généralement un serveur web.

## <a name="edge-agent-cant-access-a-modules-image-403"></a>Edge Agent ne peut pas accéder à l’image d’un module (403)
Un conteneur ne s’exécute pas et les journaux Edge Agent comportent une erreur 403. 

### <a name="root-cause"></a>Cause racine
Edge Agent ne possède pas les autorisations pour accéder à l’image d’un module. 

### <a name="resolution"></a>Résolution :
Essayez d’exécuter à nouveau la commande `iotedgectl login`.

## <a name="next-steps"></a>Étapes suivantes
Vous pensez que vous avez trouvé un bogue dans la plateforme IoT Edge ? Veuillez [soumettre un problème](https://github.com/Azure/iot-edge/issues) afin que nous puissions poursuivre les améliorations. 
