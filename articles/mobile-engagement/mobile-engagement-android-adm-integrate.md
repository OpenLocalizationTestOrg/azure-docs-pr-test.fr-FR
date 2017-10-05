---
title: "Intégration du SDK Android d'Azure Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="e7228-103">Comment intégrer ADM à Engagement</span><span class="sxs-lookup"><span data-stu-id="e7228-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e7228-104">Vous devez suivre la procédure d'intégration décrite dans le document « Comment intégrer Engagement sur Android » avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="e7228-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="e7228-105">Ce document est utile uniquement si vous avez intégré le module Reach et que vous avez l’intention d’effectuer des transmissions de type Push vers des appareils Amazon.</span><span class="sxs-lookup"><span data-stu-id="e7228-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="e7228-106">Pour intégrer les couvertures campagnes à votre application, lisez d'abord « Comment intégrer le module de couverture Engagement sur Android ».</span><span class="sxs-lookup"><span data-stu-id="e7228-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="e7228-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="e7228-107">Introduction</span></span>
<span data-ttu-id="e7228-108">L'intégration d'ADM permet à votre application d’être envoyée lorsque vous ciblez des appareils Android Amazon.</span><span class="sxs-lookup"><span data-stu-id="e7228-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="e7228-109">Les charges utiles ADM envoyées vers le Kit de développement logiciel (SDK) contiennent toujours la clé `azme` dans l'objet de données.</span><span class="sxs-lookup"><span data-stu-id="e7228-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="e7228-110">Donc si vous utilisez ADM à d’autres fins dans votre application, vous pouvez filtrer les notifications push en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="e7228-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7228-111">Seuls les appareils Amazon Kindle exécutant Android 4.0.3 ou version ultérieure sont pris en charge par Amazon Device Messaging. Vous pouvez toutefois intégrer ce code en toute sécurité sur d'autres appareils.</span><span class="sxs-lookup"><span data-stu-id="e7228-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="e7228-112">S'inscrire à ADM</span><span class="sxs-lookup"><span data-stu-id="e7228-112">Sign up to ADM</span></span>
<span data-ttu-id="e7228-113">Si vous ne l'avez pas déjà fait, vous devez activer ADM sur votre compte Amazon.</span><span class="sxs-lookup"><span data-stu-id="e7228-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="e7228-114">La procédure détaillée est disponible ici : [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="e7228-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="e7228-115">À la fin de la procédure, vous obtenez :</span><span class="sxs-lookup"><span data-stu-id="e7228-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="e7228-116">Des informations d'identification OAuth (un ID client et une clé secrète client) pour qu'Engagement puisse effectuer un Push sur vos appareils.</span><span class="sxs-lookup"><span data-stu-id="e7228-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="e7228-117">Une clé d'API qui doit être intégrée à votre application.</span><span class="sxs-lookup"><span data-stu-id="e7228-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="e7228-118">Intégration du SDK</span><span class="sxs-lookup"><span data-stu-id="e7228-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="e7228-119">Gestion des inscriptions des appareils</span><span class="sxs-lookup"><span data-stu-id="e7228-119">Managing device registrations</span></span>
<span data-ttu-id="e7228-120">Chaque appareil doit envoyer une commande d'inscription aux serveurs ADM, sinon il ne pourra pas recevoir de campagnes.</span><span class="sxs-lookup"><span data-stu-id="e7228-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="e7228-121">Si vous utilisez déjà la [bibliothèque cliente ADM] et que vous avez déjà [intégré ADM], vous pouvez accéder directement au fichier android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="e7228-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="e7228-122">Si vous n'avez pas encore intégré ADM, Engagement vous permet de l'activer dans votre application encore plus facilement :</span><span class="sxs-lookup"><span data-stu-id="e7228-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="e7228-123">Modifiez le fichier `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="e7228-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="e7228-124">Ajoutez l'espace de noms Amazon. Le fichier doit commencer ainsi :</span><span class="sxs-lookup"><span data-stu-id="e7228-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="e7228-125">Dans la balise `<application/>`, ajoutez la section suivante :</span><span class="sxs-lookup"><span data-stu-id="e7228-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="e7228-126">Après l'ajout de la balise Amazon, vous pouvez rencontrer une erreur de build si la cible de la build du projet est antérieure à Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="e7228-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="e7228-127">Vous devez utiliser une cible de build **Android 2.1 +** (vous pourrez toujours avoir un `minSdkVersion` défini sur 4).</span><span class="sxs-lookup"><span data-stu-id="e7228-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="e7228-128">Intégrez la clé d'API ADM en tant que ressource en suivant [cette procédure].</span><span class="sxs-lookup"><span data-stu-id="e7228-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="e7228-129">Ensuite, suivez les instructions des sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e7228-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="e7228-130">Communiquer l'ID d'inscription au service Push d'Engagement et recevoir des notifications</span><span class="sxs-lookup"><span data-stu-id="e7228-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="e7228-131">Pour communiquer l'ID d'inscription de l'appareil au service Push d'Engagement et recevoir ses notifications, ajoutez le code suivant au fichier `AndroidManifest.xml`, dans la balise `<application/>` (même si vous utilisez ADM sans Engagement) :</span><span class="sxs-lookup"><span data-stu-id="e7228-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="e7228-132">Assurez-vous de disposer des autorisations suivantes dans votre `AndroidManifest.xml` (avant la balise `</application>`).</span><span class="sxs-lookup"><span data-stu-id="e7228-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="e7228-133">Accorder à Engagement des informations d'identification OAuth</span><span class="sxs-lookup"><span data-stu-id="e7228-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="e7228-134">Envoyez vos informations d’identification OAuth (ID client et clé secrète client) sur le portail Engagement.</span><span class="sxs-lookup"><span data-stu-id="e7228-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="e7228-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="e7228-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="e7228-136">[bibliothèque cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="e7228-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="e7228-137">[intégré ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="e7228-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="e7228-138">[cette procédure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="e7228-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
