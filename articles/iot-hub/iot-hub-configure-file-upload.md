---
title: "Utilisation du portail Azure pour configurer le téléchargement du fichier | Microsoft Docs"
description: "Utilisation du portail Azure pour configurer votre IoT Hub en vue d’activer les transferts de fichiers à partir d’appareils connectés. Comprend des informations sur la configuration du compte de stockage Azure de destination."
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
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="038de-104">Configurer les chargements de fichiers IoT Hub à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="038de-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="038de-105">Chargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="038de-105">File upload</span></span>

<span data-ttu-id="038de-106">Pour utiliser la [fonctionnalité de chargement de fichiers dans IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure à votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="038de-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="038de-107">Sélectionnez **Chargement de fichier** pour afficher une liste de propriétés de chargement de fichiers pour l’IoT Hub en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="038de-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Afficher les paramètres de chargement de fichier IoT Hub dans le portail][13]

<span data-ttu-id="038de-109">**Conteneur de stockage**: utilisez le portail Azure pour sélectionner un conteneur d’objets blob dans un compte Azure Storage de votre abonnement Azure actuel à associer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="038de-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="038de-110">Si nécessaire, vous pouvez créer un compte Azure Storage dans le panneau **Comptes de stockage** et un conteneur d’objets blob dans le panneau **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="038de-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="038de-111">IoT Hub génère automatiquement des URI SAS avec des autorisations d’écriture pour ce conteneur d’objets blob pour les appareils à utiliser lorsqu’ils chargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="038de-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Afficher les conteneurs de stockage pour le chargement de fichiers dans le portail][14]

<span data-ttu-id="038de-113">**Recevoir des notifications pour les fichiers chargés**: activez ou désactivez les notifications de chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="038de-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="038de-114">**SAS TTL**: ce paramètre est la durée de vie des URI de signature d’accès partagé renvoyés à l’appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="038de-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="038de-115">Il est défini par défaut sur une heure, mais il peut être personnalisé avec d’autres valeurs à l’aide du curseur.</span><span class="sxs-lookup"><span data-stu-id="038de-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="038de-116">**Durée de vie par défaut des paramètres de notification de fichiers**: la durée de vie d’une notification de chargement avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="038de-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="038de-117">Il est défini par défaut sur un jour, mais il peut être personnalisé avec d’autres valeurs à l’aide du curseur.</span><span class="sxs-lookup"><span data-stu-id="038de-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="038de-118">**Nombre maximal de remises de notifications de fichier**: le nombre de tentatives de remise d’une notification de chargement de fichier par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="038de-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="038de-119">Il est défini par défaut sur 10, mais il peut être personnalisé avec d’autres valeurs à l’aide du curseur.</span><span class="sxs-lookup"><span data-stu-id="038de-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Configurer le chargement de fichier IoT Hub dans le portail][15]

## <a name="next-steps"></a><span data-ttu-id="038de-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="038de-121">Next steps</span></span>

<span data-ttu-id="038de-122">Pour plus d’informations sur les fonctionnalités de téléchargement de fichiers d’IoT Hub, consultez [Télécharger des fichiers à partir d’un appareil][lnk-upload] dans le guide du développeur IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="038de-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="038de-123">Suivez ces liens pour en savoir plus sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="038de-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="038de-124">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="038de-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="038de-125">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="038de-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="038de-126">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="038de-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="038de-127">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="038de-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="038de-128">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="038de-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="038de-129">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="038de-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="038de-130">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="038de-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
