---
title: "Guide de dépannage d’Azure Mobile Engagement - Service"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="a3e11-103">Guide de résolution des problèmes de service</span><span class="sxs-lookup"><span data-stu-id="a3e11-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="a3e11-104">Les éléments suivants sont des problèmes potentiels liés à l’exécution d’Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="a3e11-105">Interruptions de service</span><span class="sxs-lookup"><span data-stu-id="a3e11-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="a3e11-106">Problème</span><span class="sxs-lookup"><span data-stu-id="a3e11-106">Issue</span></span>
* <span data-ttu-id="a3e11-107">Problèmes qui semblent provenir des interruptions de service d’Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="a3e11-108">Causes</span><span class="sxs-lookup"><span data-stu-id="a3e11-108">Causes</span></span>
* <span data-ttu-id="a3e11-109">Problèmes qui semblent provenir d'Azure Mobile Engagement des interruptions de Service peuvent être dû à plusieurs problèmes différents :</span><span class="sxs-lookup"><span data-stu-id="a3e11-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="a3e11-110">Problèmes isolés systémiques à l'origine sur l'ensemble d'Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a3e11-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="a3e11-111">Problèmes connus provoqués par des pannes de serveur (ne s'affichent pas toujours dans l'état du serveur) :</span><span class="sxs-lookup"><span data-stu-id="a3e11-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="a3e11-112">Retards de planification, erreurs de ciblage, problèmes de mise à jour de Badge, arrêt de la collecte des statistiques, arrêt du fonctionnement des notifications Push, arrêt du fonctionnement des API, impossibilité de créer des applications ou des utilisateurs, erreurs DNS et erreurs de délai d’attente dans l’interface utilisateur, les API ou les applications sur un périphérique.</span><span class="sxs-lookup"><span data-stu-id="a3e11-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="a3e11-113">Interruptions de dépendance de cloud [État du Service Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a3e11-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="a3e11-114">Interruptions de dépendance des Services de notification push (PNS)</span><span class="sxs-lookup"><span data-stu-id="a3e11-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="a3e11-115">Interruptions App Store</span><span class="sxs-lookup"><span data-stu-id="a3e11-115">App Store Outages</span></span>

1) <span data-ttu-id="a3e11-116">Pour savoir si le problème est lié au système, vous pouvez tester la même fonction à partir d’une autre</span><span class="sxs-lookup"><span data-stu-id="a3e11-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="a3e11-117">Application intégrée d’Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a3e11-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="a3e11-118">Appareil de test</span><span class="sxs-lookup"><span data-stu-id="a3e11-118">Test device</span></span>
* <span data-ttu-id="a3e11-119">Version du système d’exploitation de l’appareil de test</span><span class="sxs-lookup"><span data-stu-id="a3e11-119">Test device OS version</span></span>
* <span data-ttu-id="a3e11-120">Campagne</span><span class="sxs-lookup"><span data-stu-id="a3e11-120">Campaign</span></span>
* <span data-ttu-id="a3e11-121">Compte utilisateur de l’administrateur</span><span class="sxs-lookup"><span data-stu-id="a3e11-121">Administrator user account</span></span>
* <span data-ttu-id="a3e11-122">Navigateur (Internet Explorer, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="a3e11-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="a3e11-123">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="a3e11-123">Computer</span></span>

2) <span data-ttu-id="a3e11-124">Pour savoir si le problème affecte uniquement l'interface utilisateur ou les API :</span><span class="sxs-lookup"><span data-stu-id="a3e11-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="a3e11-125">Testez la même fonction à partir de l’interface utilisateur d’Azure Mobile Engagement et l’API d’Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="a3e11-126">Pour tester si le problème provient du réseau de votre téléphone cellulaire :</span><span class="sxs-lookup"><span data-stu-id="a3e11-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="a3e11-127">Testez quand vous êtes connecté à Internet via le Wi-Fi et quand vous êtes connecté via le réseau de votre téléphone portable 3G de test.</span><span class="sxs-lookup"><span data-stu-id="a3e11-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="a3e11-128">Confirmez que votre pare-feu ne bloque pas les ports ni les adresses IP Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="a3e11-129">Pour tester si le problème provient de votre périphérique :</span><span class="sxs-lookup"><span data-stu-id="a3e11-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="a3e11-130">Testez si votre appareil est en mesure de se connecter à Azure Mobile Engagement avec une autre application intégrée Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="a3e11-131">Testez que vous pouvez générer des événements, des travaux et des incidents à partir de votre téléphone, qui peuvent être consultés dans l’interface utilisateur d’Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="a3e11-132">Vérifiez si vous pouvez envoyer des notifications push à partir de l’interface utilisateur d’Azure Mobile Engagement sur votre appareil en fonction de son ID d’appareil.</span><span class="sxs-lookup"><span data-stu-id="a3e11-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="a3e11-133">Pour tester si le problème provient de votre application :</span><span class="sxs-lookup"><span data-stu-id="a3e11-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="a3e11-134">Installez et testez votre application à partir d’un émulateur plutôt qu’à partir d'un appareil physique :</span><span class="sxs-lookup"><span data-stu-id="a3e11-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="a3e11-135">Pour tester si le problème avec les mises à niveau du système d'exploitation à l'utilisateur final les périphériques qui nécessitent une mise à niveau du Kit de développement logiciel pour résoudre :</span><span class="sxs-lookup"><span data-stu-id="a3e11-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="a3e11-136">Testez votre application sur différents appareils avec différentes versions du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a3e11-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="a3e11-137">Confirmez que vous utilisez la version la plus récente du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="a3e11-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="a3e11-138">Problèmes de connectivité et informations incorrectes</span><span class="sxs-lookup"><span data-stu-id="a3e11-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="a3e11-139">Problème</span><span class="sxs-lookup"><span data-stu-id="a3e11-139">Issue</span></span>
* <span data-ttu-id="a3e11-140">Problèmes de connexion à l'interface utilisateur d'Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="a3e11-141">Erreurs de connexion avec l'API d'Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="a3e11-142">Problèmes lors du chargement des balises d'informations d'application via l'API de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="a3e11-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="a3e11-143">Problèmes lors du téléchargement des journaux ou des données exportées à partir d'Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="a3e11-144">Informations incorrectes indiquées dans l'interface utilisateur de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="a3e11-145">Informations incorrectes indiquées dans les journaux Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a3e11-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="a3e11-146">Causes</span><span class="sxs-lookup"><span data-stu-id="a3e11-146">Causes</span></span>
* <span data-ttu-id="a3e11-147">Confirmez que votre compte d'utilisateur dispose des autorisations nécessaires pour effectuer la tâche.</span><span class="sxs-lookup"><span data-stu-id="a3e11-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="a3e11-148">Vérifiez que le problème n'est pas isolé sur un seul ordinateur ou votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="a3e11-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="a3e11-149">Vérifiez que que le service Azure Mobile Engagement n'a pas signalé d'interruptions.</span><span class="sxs-lookup"><span data-stu-id="a3e11-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="a3e11-150">Vérifiez que vos fichiers de balise d'informations d'application respectent toutes ces règles :</span><span class="sxs-lookup"><span data-stu-id="a3e11-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="a3e11-151">Utilisez uniquement le jeu de caractères UTF8 (le jeu de caractères ANSI n'est pas pris en charge).</span><span class="sxs-lookup"><span data-stu-id="a3e11-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="a3e11-152">Utilisez une virgule « , » comme caractère de séparation (vous pouvez ouvrir une demande de service pour modifier le caractère de séparation .csv afin que ce ne soit plus une virgule (« , ») mais un autre caractère, par exemple un point-virgule « ; »).</span><span class="sxs-lookup"><span data-stu-id="a3e11-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="a3e11-153">Utilisez des minuscules pour les valeurs booléennes « true » et « false ».</span><span class="sxs-lookup"><span data-stu-id="a3e11-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="a3e11-154">Utilisez un fichier d'une taille inférieure à la taille maximale de 35 Mo.</span><span class="sxs-lookup"><span data-stu-id="a3e11-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

