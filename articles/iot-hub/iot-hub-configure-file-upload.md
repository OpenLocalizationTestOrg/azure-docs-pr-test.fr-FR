---
title: "téléchargement du fichier aaaUse hello tooconfigure portail Azure | Documents Microsoft"
description: "Comment toouse hello tooconfigure portail Azure votre fichier tooenable de hub IoT télécharge à partir d’appareils connectés. Inclut des informations sur la configuration du compte de stockage Azure hello destination."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="510d1-104">Configurer des téléchargements de fichiers IoT Hub à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="510d1-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="510d1-105">Chargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="510d1-105">File upload</span></span>

<span data-ttu-id="510d1-106">toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="510d1-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="510d1-107">Sélectionnez **téléchargement du fichier** toodisplay une liste de propriétés de téléchargement de fichier pour le hub IoT hello qui est en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="510d1-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Afficher le fichier IoT Hub télécharger les paramètres dans le portail de hello][13]

<span data-ttu-id="510d1-109">**Conteneur de stockage**: utilisez hello tooselect portail Azure un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="510d1-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="510d1-110">Si il nécessaire, vous pouvez créer un compte Azure Storage sur hello **comptes de stockage** conteneur lame et d’objets blob sur hello **conteneurs** panneau.</span><span class="sxs-lookup"><span data-stu-id="510d1-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="510d1-111">IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="510d1-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Afficher les conteneurs de stockage pour le téléchargement du fichier dans le portail de hello][14]

<span data-ttu-id="510d1-113">**Recevoir des notifications pour les fichiers téléchargés**: activer ou désactiver les notifications de téléchargement de fichier par le biais bascule de hello.</span><span class="sxs-lookup"><span data-stu-id="510d1-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="510d1-114">**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="510d1-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="510d1-115">Heure de tooone la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.</span><span class="sxs-lookup"><span data-stu-id="510d1-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="510d1-116">**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="510d1-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="510d1-117">Jour de tooone la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.</span><span class="sxs-lookup"><span data-stu-id="510d1-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="510d1-118">**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="510d1-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="510d1-119">Too10 la valeur par défaut, mais peuvent être personnalisé tooother valeurs à l’aide de curseur de hello.</span><span class="sxs-lookup"><span data-stu-id="510d1-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Configurer le téléchargement du fichier IoT Hub dans le portail de hello][15]

## <a name="next-steps"></a><span data-ttu-id="510d1-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="510d1-121">Next steps</span></span>

<span data-ttu-id="510d1-122">Pour plus d’informations sur les fonctionnalités de téléchargement de fichier hello IoT Hub, consultez [télécharger des fichiers à partir d’un appareil] [ lnk-upload] Bonjour guide du développeur IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="510d1-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="510d1-123">Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="510d1-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="510d1-124">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="510d1-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="510d1-125">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="510d1-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="510d1-126">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="510d1-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="510d1-127">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="510d1-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="510d1-128">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="510d1-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="510d1-129">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="510d1-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="510d1-130">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="510d1-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
