---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
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
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="84ead-103">Comment tooIntegrate GCM avec Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="84ead-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="84ead-104">Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="84ead-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="84ead-105">Ce document est utile uniquement si vous déjà intégré hello atteindre toopush module et le plan de Google Play périphériques.</span><span class="sxs-lookup"><span data-stu-id="84ead-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="84ead-106">toointegrate couvertures campagne dans votre application, lisez d’abord comment tooIntegrate Engagement atteindre sur Android.</span><span class="sxs-lookup"><span data-stu-id="84ead-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="84ead-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="84ead-107">Introduction</span></span>
<span data-ttu-id="84ead-108">Intégration GCM permet à votre toobe application envoyée.</span><span class="sxs-lookup"><span data-stu-id="84ead-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="84ead-109">Charges utiles GCM envoyées toohello SDK toujours contient hello `azme` clé dans l’objet de données hello.</span><span class="sxs-lookup"><span data-stu-id="84ead-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="84ead-110">Donc si vous utilisez GCM à d’autres fins dans votre application, vous pouvez filtrer les notifications Push en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="84ead-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84ead-111">Seuls les appareils disposant d’Android 2.2 ou version ultérieure, de Google Play et d’une connexion d’arrière-plan à Google peuvent faire l’objet d’une notification Push à l’aide de GCM. Toutefois, vous pouvez intégrer ce code en toute sécurité sur les appareils non pris en charge (car il utilise uniquement des intentions).</span><span class="sxs-lookup"><span data-stu-id="84ead-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="84ead-112">Créer un projet Google Cloud Messaging avec une clé API</span><span class="sxs-lookup"><span data-stu-id="84ead-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="84ead-113">Intégration du SDK</span><span class="sxs-lookup"><span data-stu-id="84ead-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="84ead-114">Gestion des inscriptions des appareils</span><span class="sxs-lookup"><span data-stu-id="84ead-114">Managing device registrations</span></span>
<span data-ttu-id="84ead-115">Chaque appareil doit envoyer un toohello de commande d’inscription des serveurs de Google, sinon ils ne peuvent pas être atteint.</span><span class="sxs-lookup"><span data-stu-id="84ead-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="84ead-116">Un périphérique peut également annuler l’inscription de notifications GCM (appareil de hello est automatiquement annulée si la désinstallation de l’application hello).</span><span class="sxs-lookup"><span data-stu-id="84ead-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="84ead-117">Si vous n’utilisez pas [SDK de Google Play] ou vous ne déjà envoyer intention de l’inscription de hello vous-même, vous pouvez apporter Engagement inscrire les appareils hello automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="84ead-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="84ead-118">tooenable, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise :</span><span class="sxs-lookup"><span data-stu-id="84ead-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="84ead-119">Service de Push de l’Engagement d’enregistrement id toohello de communiquer et de recevoir des notifications</span><span class="sxs-lookup"><span data-stu-id="84ead-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="84ead-120">Dans l’ordre toocommunicate hello l’id d’inscription de toohello de périphérique hello Engagement Push du service et recevoir ses notifications, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise (même si vous gérez vous-même inscriptions d’appareils) :</span><span class="sxs-lookup"><span data-stu-id="84ead-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="84ead-121">Assurez-vous d’avoir hello suivant des autorisations dans votre `AndroidManifest.xml` (après hello `</application>` balise).</span><span class="sxs-lookup"><span data-stu-id="84ead-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="84ead-122">Grant Mobile Engagement accès tooyour clé API GCM</span><span class="sxs-lookup"><span data-stu-id="84ead-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="84ead-123">Suivez [ce guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement accès tooyour clé API GCM.</span><span class="sxs-lookup"><span data-stu-id="84ead-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[SDK de Google Play]:https://developers.google.com/cloud-messaging/android/start
