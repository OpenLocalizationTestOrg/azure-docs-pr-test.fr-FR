---
title: "Appareil simulé et passerelle Azure IoT - Leçon 2 : Enregistrer un appareil | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, cloud de l’internet des objets, créer un appareil azure iot hub, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Créer un Azure IoT Hub et inscrire votre appareil

## <a name="what-you-will-do"></a>Procédure à suivre

- Créer un groupe de ressources
- Créer votre premier IoT Hub
- Inscrire votre appareil dans votre IoT hub à l’aide de hello CLI d’Azure. 

Lorsque vous inscrivez votre appareil à votre hub IoT, hello Azure IoT Hub service génère une clé pour votre tooauthenticate toouse de périphérique avec le service de hello. 

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Dans cette leçon, vous allez apprendre :

- Comment toouse hello CLI d’Azure toocreate un IoT hub.
- Comment tooregister un périphérique dans un hub IoT.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.
- Vous devez avoir hello que CLI d’Azure installé.

## <a name="create-an-iot-hub"></a>Créer un hub IoT

toocreate un IoT hub, procédez comme suit :

1. La connexion tooyour compte Azure en exécutant hello de commande suivante :

   ```bash
   az login
   ```

   Une fois la connexion établie, tous vos abonnements disponibles sont répertoriés.

2. Définir la valeur par défaut de hello abonnement Azure que vous souhaitez toouse en exécutant hello de commande suivante :

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`se trouvent dans la sortie de hello Hello `az login` ou hello `az account list` commande.

3. Inscription du fournisseur de hello en hello suivant de commande en cours d’exécution. Les fournisseurs de ressources sont des services qui fournissent des ressources pour votre application. Vous devez inscrire le fournisseur de hello avant de pouvoir déployer hello ressource Azure qui hello offres du fournisseur.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Créer un groupe de ressources nommé `iot-gateway` dans la région ouest des États-Unis hello en exécutant hello de commande suivante :

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`est l’emplacement hello vous créez votre groupe de ressources. Si vous voulez toouse un autre emplacement, vous pouvez exécuter `az account list-locations -o table` toosee tous hello emplacements Azure prend en charge.

5. Créez un hub IoT Bonjour `iot-gateway` groupe de ressources en exécutant hello de commande suivante :

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Par défaut, hello outil crée un IoT Hub niveau de tarification gratuit hello. Pour plus d’informations, consultez la [tarification Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> nom de Hello de votre IoT hub doit être globalement unique. Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.

## <a name="register-your-device-in-your-iot-hub"></a>Inscrire votre appareil dans votre IoT Hub

Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique.
Inscrivez votre appareil dans votre Azure IoT Hub en exécutant la commande suivante :

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Résumé

Vous avez créé un IoT Hub et inscrit votre appareil logique sous une identité d’appareil dans votre IoT Hub. Vous êtes prêt toolearn tooconfigure et exécuter une passerelle exemples application toosend de données à partir de votre concentrateur périphérique physique tooyour IoT hello de cloud.

## <a name="next-steps"></a>Étapes suivantes
[Configurer et exécuter un exemple d’application de téléchargement cloud d’appareil simulé](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)