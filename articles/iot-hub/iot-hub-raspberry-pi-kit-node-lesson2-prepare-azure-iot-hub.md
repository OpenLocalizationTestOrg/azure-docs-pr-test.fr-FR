---
featureFlags: usabilla
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 2 : inscription de l’appareil | Documents Microsoft"
description: "Créer un groupe de ressources, créez un Azure IoT hub, inscrire et Pi Bonjour Registre des identités IoT Hub aide CLI d’Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: raspberry pi cloud, connexion pi cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>Création de votre IoT Hub et inscription de Raspberry Pi 3
## <a name="what-you-will-do"></a>Procédure à suivre
* Créez un groupe de ressources.
* Créer votre concentrateur Azure IoT dans le groupe de ressources hello.
* Ajouter framboises Pi 3 toohello Azure IoT hub à l’aide de hello Azure interface de ligne de commande (CLI d’Azure).

Lorsque vous utilisez le hub IoT tooyour CLI d’Azure tooadd Pi, service de hello génère une clé pour tooauthenticate Pi avec le service de hello. Si vous rencontrez des problèmes, rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment toouse CLI d’Azure toocreate un IoT hub
* Comment toocreate une identité d’appareil de Pi dans votre IoT hub

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un compte Azure
* Un Mac ou un ordinateur Windows avec hello CLI d’Azure installé

## <a name="create-your-iot-hub"></a>Création de votre IoT Hub
Azure IoT Hub vous permet de connecter, surveiller et gérer des millions de ressources IoT. toocreate votre hub IoT, procédez comme suit :

1. La connexion tooyour compte Azure en exécutant hello de commande suivante :

   ```bash
   az login
   ```

   Après une connexion réussie, tous vos abonnements disponibles sont répertoriés.

2. Définissez hello abonnement de valeur par défaut que vous souhaitez toouse en exécutant hello de commande suivante :

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`se trouvent dans la sortie de hello Hello `az login` ou hello `az account list` commande.

3. Inscription du fournisseur de hello en hello suivant de commande en cours d’exécution. Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application. Vous devez inscrire le fournisseur de hello avant de pouvoir déployer hello ressource Azure qui hello offres du fournisseur.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Créer un groupe de ressources nommé iot-exemple dans la région ouest des États-Unis hello en exécutant hello de commande suivante :

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`est l’emplacement hello vous créez votre groupe de ressources. Si vous voulez toouse un autre emplacement, vous pouvez exécuter `az account list-locations -o table` toosee tous hello emplacements Azure prend en charge.
 
5. Créez un hub IoT hello iot-exemple groupe de ressources en exécutant hello de commande suivante :

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   Par défaut, hello outil crée un IoT Hub niveau de tarification gratuit hello. Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE] 
> nom de Hello de votre IoT hub doit être globalement unique. Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.

## <a name="register-pi-in-your-iot-hub"></a>Inscription de Pi dans votre IoT Hub
Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique. Vous utilisez Azure CLI tooregister votre Pi et créer un certificat X.509 auto-signé pour l’authentification des appareils.

Exécutez hello de commande suivante :

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Résumé
Vous avez créé un IoT Hub et enregistré Pi sous une identité d’appareil dans votre IoT Hub. Vous êtes prêt toolearn comment toosend les messages à partir de hub IoT de tooyour Pi.

## <a name="next-steps"></a>Étapes suivantes
[Créer une application de la fonction Azure et un tooprocess de compte de stockage Azure et de stocker les messages de hub IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

