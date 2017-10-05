---
title: "Intégration du SDK Android d'Azure Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="bd46c-103">comment intégrer GCM à Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="bd46c-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bd46c-104">Vous devez suivre la procédure d'intégration décrite dans le document « Comment intégrer Engagement sur Android » avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="bd46c-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="bd46c-105">Ce document est utile uniquement si vous avez intégré le module Reach et avez l’intention d’effectuer des transmissions de type Push vers des appareils Google Play.</span><span class="sxs-lookup"><span data-stu-id="bd46c-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="bd46c-106">Pour intégrer les couvertures campagnes à votre application, lisez d'abord « Comment intégrer le module de couverture Engagement sur Android ».</span><span class="sxs-lookup"><span data-stu-id="bd46c-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="bd46c-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="bd46c-107">Introduction</span></span>
<span data-ttu-id="bd46c-108">L’intégration de GCM permet à votre application de recevoir des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="bd46c-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="bd46c-109">Les charges GCM envoyées vers le Kit de développement logiciel (SDK) contiennent toujours la clé `azme` dans l’objet de données.</span><span class="sxs-lookup"><span data-stu-id="bd46c-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="bd46c-110">Donc si vous utilisez GCM à d’autres fins dans votre application, vous pouvez filtrer les notifications Push en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="bd46c-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd46c-111">Seuls les appareils disposant d’Android 2.2 ou version ultérieure, de Google Play et d’une connexion d’arrière-plan à Google peuvent faire l’objet d’une notification Push à l’aide de GCM. Toutefois, vous pouvez intégrer ce code en toute sécurité sur les appareils non pris en charge (car il utilise uniquement des intentions).</span><span class="sxs-lookup"><span data-stu-id="bd46c-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="bd46c-112">Créer un projet Google Cloud Messaging avec une clé API</span><span class="sxs-lookup"><span data-stu-id="bd46c-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="bd46c-113">Intégration du SDK</span><span class="sxs-lookup"><span data-stu-id="bd46c-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="bd46c-114">Gestion des inscriptions des appareils</span><span class="sxs-lookup"><span data-stu-id="bd46c-114">Managing device registrations</span></span>
<span data-ttu-id="bd46c-115">Chaque appareil doit envoyer une commande d'inscription aux serveurs Google, sinon il ne pourra pas recevoir de campagnes.</span><span class="sxs-lookup"><span data-stu-id="bd46c-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="bd46c-116">Un appareil peut également se désinscrire des notifications GCM (l'appareil est automatiquement désinscrit quand l'application est désinstallée).</span><span class="sxs-lookup"><span data-stu-id="bd46c-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="bd46c-117">Si vous n’utilisez pas [le Kit de développement logiciel (SDK) Google Play] ou si vous n’avez pas encore envoyé l’intention d’inscription, vous pouvez demander à Engagement d’inscrire automatiquement l’appareil.</span><span class="sxs-lookup"><span data-stu-id="bd46c-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="bd46c-118">Pour cela, ajoutez le code suivant au fichier `AndroidManifest.xml`, à l'intérieur de la balise `<application/>` :</span><span class="sxs-lookup"><span data-stu-id="bd46c-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="bd46c-119">Communiquer l'ID d'inscription au service Push d'Engagement et recevoir des notifications</span><span class="sxs-lookup"><span data-stu-id="bd46c-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="bd46c-120">Pour communiquer l'ID d'inscription de l'appareil au service Push d'Engagement et recevoir ses notifications, ajoutez le code suivant au fichier `AndroidManifest.xml`, à l'intérieur de la balise `<application/>` (même si vous gérez vous-même les inscriptions d'appareil) :</span><span class="sxs-lookup"><span data-stu-id="bd46c-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="bd46c-121">Assurez-vous de disposer des autorisations suivantes dans votre `AndroidManifest.xml` (après la balise `</application>`).</span><span class="sxs-lookup"><span data-stu-id="bd46c-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="bd46c-122">Accorder à Mobile Engagement l’accès à votre clé d’API GCM</span><span class="sxs-lookup"><span data-stu-id="bd46c-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="bd46c-123">Suivez [ce guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) pour accorder à Mobile Engagement l’accès à votre clé API GCM</span><span class="sxs-lookup"><span data-stu-id="bd46c-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="bd46c-124">[le Kit de développement logiciel (SDK) Google Play]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="bd46c-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
