---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 2 : inscription de l’appareil | Documents Microsoft"
description: "Créer un groupe de ressources, créez un Azure IoT hub, inscrire et Edison dans hello Azure IoT hub aide hello CLI d’Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>Créer votre IoT Hub et inscrire Intel Edison
## <a name="what-you-will-do"></a>Procédure à suivre
* Créez un groupe de ressources.
* Créer votre concentrateur Azure IoT dans le groupe de ressources hello.
* Ajouter le concentrateur de Azure IoT Intel Edison toohello à l’aide de hello Azure interface de ligne de commande (CLI d’Azure).

Lorsque vous utilisez hello CLI d’Azure tooadd hub IoT de tooyour Edison, service de hello génère une clé pour tooauthenticate Edison avec le service de hello. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment toouse hello CLI d’Azure toocreate un IoT hub.
* Comment toocreate une identité d’appareil pour Edison dans votre hub IoT.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un compte Azure. Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.
* Vous devez avoir hello que CLI d’Azure installé.

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
> nom de Hello de votre IoT hub doit être globalement unique.
> Vous ne pouvez créer qu’une seule édition F1 d’Azure IoT Hub sous votre abonnement Azure.


## <a name="register-edison-in-your-iot-hub"></a>Inscription d’Edison dans votre IoT Hub
Chaque périphérique qui envoie IoT hub tooyour de messages et reçoit des messages à partir de votre IoT hub doit être enregistré avec un ID unique.

Inscrivez Edison dans votre IoT Hub en exécutant la commande suivante :

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Résumé
Vous avez créé un IoT Hub et enregistré Edison sous une identité d’appareil dans votre IoT Hub. Vous êtes prêt toolearn comment toosend les messages à partir de hub IoT de tooyour Edison.

## <a name="next-steps"></a>Étapes suivantes
[Créer une application de la fonction Azure et un stockage Azure compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md