---
title: "aaaAzure Guide de dépannage de Engagement Mobile - Service"
description: "Guides de dépannage pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="a6641-103">Guide de résolution des problèmes de service</span><span class="sxs-lookup"><span data-stu-id="a6641-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="a6641-104">Hello Voici les problèmes possibles, que vous pouvez rencontrer avec le mode d’exécution de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="a6641-105">Interruptions de service</span><span class="sxs-lookup"><span data-stu-id="a6641-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="a6641-106">Problème</span><span class="sxs-lookup"><span data-stu-id="a6641-106">Issue</span></span>
* <span data-ttu-id="a6641-107">Problèmes apparaissant toobe dû à des interruptions de Service Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="a6641-108">Causes</span><span class="sxs-lookup"><span data-stu-id="a6641-108">Causes</span></span>
* <span data-ttu-id="a6641-109">Les problèmes apparaissant toobe dû à des interruptions de Service Azure Mobile Engagement peuvent être dû à plusieurs problèmes différents :</span><span class="sxs-lookup"><span data-stu-id="a6641-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="a6641-110">Problèmes apparaissant à l’origine tooall systémique de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a6641-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="a6641-111">Problèmes connus provoqués par des pannes de serveur (ne s'affichent pas toujours dans l'état du serveur) :</span><span class="sxs-lookup"><span data-stu-id="a6641-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="a6641-112">Planification des retards, des erreurs de ciblage, les problèmes de mise à jour de Badge, stop statistiques collecte, par envoi de données s’arrête de fonctionner, cessent de fonctionner, les nouvelles applications ou les utilisateurs de l’API ne peut pas créer, erreurs DNS et délai d’attente dans hello l’interface utilisateur, des API ou des applications sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="a6641-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="a6641-113">Interruptions de dépendance de cloud [État du Service Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a6641-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="a6641-114">Interruptions de dépendance des Services de notification push (PNS)</span><span class="sxs-lookup"><span data-stu-id="a6641-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="a6641-115">Interruptions App Store</span><span class="sxs-lookup"><span data-stu-id="a6641-115">App Store Outages</span></span>

1) <span data-ttu-id="a6641-116">tootest toosee si le problème de hello est systémique, vous pouvez tester hello même fonction à partir d’un autre</span><span class="sxs-lookup"><span data-stu-id="a6641-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="a6641-117">Application intégrée d’Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a6641-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="a6641-118">Appareil de test</span><span class="sxs-lookup"><span data-stu-id="a6641-118">Test device</span></span>
* <span data-ttu-id="a6641-119">Version du système d’exploitation de l’appareil de test</span><span class="sxs-lookup"><span data-stu-id="a6641-119">Test device OS version</span></span>
* <span data-ttu-id="a6641-120">Campagne</span><span class="sxs-lookup"><span data-stu-id="a6641-120">Campaign</span></span>
* <span data-ttu-id="a6641-121">Compte utilisateur de l’administrateur</span><span class="sxs-lookup"><span data-stu-id="a6641-121">Administrator user account</span></span>
* <span data-ttu-id="a6641-122">Navigateur (Internet Explorer, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="a6641-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="a6641-123">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="a6641-123">Computer</span></span>

2) <span data-ttu-id="a6641-124">tootest si le problème de hello affecte uniquement hello hello interface utilisateur ou l’API :</span><span class="sxs-lookup"><span data-stu-id="a6641-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="a6641-125">Test hello même fonction à partir de ces deux hello Azure Mobile Engagement UI et hello API Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="a6641-126">tootest si hello problème avec le réseau de votre téléphone cellulaire :</span><span class="sxs-lookup"><span data-stu-id="a6641-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="a6641-127">Test lors de la toohello connecté Internet via le Wi-Fi et tout en étant connecté via le réseau de votre téléphone cellulaire 3G.</span><span class="sxs-lookup"><span data-stu-id="a6641-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="a6641-128">Vérifiez que votre pare-feu ne bloque pas un des Ports ou des adresses IP de hello Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="a6641-129">tootest si hello problème avec votre appareil :</span><span class="sxs-lookup"><span data-stu-id="a6641-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="a6641-130">Tester si votre appareil est en mesure de tooconnect tooAzure Mobile Engagement avec une autre application intégrée Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="a6641-131">Vérifiez que vous pouvez générer des incidents, des travaux et des événements à partir de votre téléphone, qui peut être consulté dans hello Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="a6641-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="a6641-132">Vérifier si vous pouvez envoyer des notifications push à partir de l’appareil de tooyour de l’interface utilisateur de Azure Mobile Engagement hello en fonction de son ID de périphérique.</span><span class="sxs-lookup"><span data-stu-id="a6641-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="a6641-133">tootest si hello problème avec votre application :</span><span class="sxs-lookup"><span data-stu-id="a6641-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="a6641-134">Installez et testez votre application à partir d’un émulateur plutôt qu’à partir d'un appareil physique :</span><span class="sxs-lookup"><span data-stu-id="a6641-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="a6641-135">tootest si hello problème avec l’utilisateur tooend de mises à niveau du système d’exploitation des appareils, qui nécessitent une tooresolve de mise à niveau du Kit de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="a6641-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="a6641-136">Tester votre application sur différents appareils avec différentes versions de hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a6641-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="a6641-137">Vérifiez que vous utilisez la version la plus récente du Kit de développement logiciel de hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6641-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="a6641-138">Problèmes de connectivité et informations incorrectes</span><span class="sxs-lookup"><span data-stu-id="a6641-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="a6641-139">Problème</span><span class="sxs-lookup"><span data-stu-id="a6641-139">Issue</span></span>
* <span data-ttu-id="a6641-140">Problèmes de connexion à Bonjour Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="a6641-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="a6641-141">Erreurs de connexion avec hello Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="a6641-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="a6641-142">Problèmes lors du chargement des balises d’informations sur application via hello API de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="a6641-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="a6641-143">Problèmes lors du téléchargement des journaux ou des données exportées à partir d'Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="a6641-144">Informations incorrectes indiquées Bonjour Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="a6641-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="a6641-145">Informations incorrectes indiquées dans les journaux Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6641-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="a6641-146">Causes</span><span class="sxs-lookup"><span data-stu-id="a6641-146">Causes</span></span>
* <span data-ttu-id="a6641-147">Confirmez que votre compte d’utilisateur a des tâches de hello de tooperform autorisations suffisantes.</span><span class="sxs-lookup"><span data-stu-id="a6641-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="a6641-148">Vérifiez que ce problème hello n’est pas isolé tooone ordinateur ou votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="a6641-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="a6641-149">Vérifiez que ce service de Azure Mobile Engagement hello ne dispose d’aucune les pannes signalées.</span><span class="sxs-lookup"><span data-stu-id="a6641-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="a6641-150">Vérifiez que vos fichiers de balise d'informations d'application respectent toutes ces règles :</span><span class="sxs-lookup"><span data-stu-id="a6641-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="a6641-151">Utilisez hello uniquement le jeu de caractères UTF-8 (jeu de caractères ANSI hello n’est pas pris en charge).</span><span class="sxs-lookup"><span data-stu-id="a6641-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="a6641-152">Utilisez une virgule «, » comme séparateur de hello (vous pouvez ouvrir un caractère de séparation service demande hello toorequest toochange .csv à partir d’une virgule «, » caractères tooanother comme un point-virgule « ; »).</span><span class="sxs-lookup"><span data-stu-id="a6641-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="a6641-153">Utilisez des minuscules pour les valeurs booléennes « true » et « false ».</span><span class="sxs-lookup"><span data-stu-id="a6641-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="a6641-154">Utiliser un fichier qui est plus petit que la taille de fichier maximale hello de 35 Mo.</span><span class="sxs-lookup"><span data-stu-id="a6641-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

