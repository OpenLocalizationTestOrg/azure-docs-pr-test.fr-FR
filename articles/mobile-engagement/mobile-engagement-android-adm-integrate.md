---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="b9b43-103">Comment tooIntegrate ADM avec Engagement</span><span class="sxs-lookup"><span data-stu-id="b9b43-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b9b43-104">Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="b9b43-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="b9b43-105">Ce document est utile uniquement si vous hello portée module plan toopush Amazon des appareils et déjà intégré.</span><span class="sxs-lookup"><span data-stu-id="b9b43-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="b9b43-106">toointegrate couvertures campagne dans votre application, lisez d’abord comment tooIntegrate Engagement atteindre sur Android.</span><span class="sxs-lookup"><span data-stu-id="b9b43-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="b9b43-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="b9b43-107">Introduction</span></span>
<span data-ttu-id="b9b43-108">Intégration ADM permet à votre toobe application envoyée lors du ciblage des appareils Amazon Android.</span><span class="sxs-lookup"><span data-stu-id="b9b43-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="b9b43-109">Charges utiles ADM envoyées toohello SDK toujours contient hello `azme` clé dans l’objet de données hello.</span><span class="sxs-lookup"><span data-stu-id="b9b43-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="b9b43-110">Donc si vous utilisez ADM à d’autres fins dans votre application, vous pouvez filtrer les notifications push en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="b9b43-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9b43-111">Seuls les appareils Amazon Kindle exécutant Android 4.0.3 ou version ultérieure sont pris en charge par Amazon Device Messaging. Vous pouvez toutefois intégrer ce code en toute sécurité sur d'autres appareils.</span><span class="sxs-lookup"><span data-stu-id="b9b43-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="b9b43-112">S’inscrire tooADM</span><span class="sxs-lookup"><span data-stu-id="b9b43-112">Sign up tooADM</span></span>
<span data-ttu-id="b9b43-113">Si vous ne l'avez pas déjà fait, vous devez activer ADM sur votre compte Amazon.</span><span class="sxs-lookup"><span data-stu-id="b9b43-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="b9b43-114">procédure de Hello est détaillée sur : [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="b9b43-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="b9b43-115">Une fois la procédure de hello, vous obtenez :</span><span class="sxs-lookup"><span data-stu-id="b9b43-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="b9b43-116">OAuth informations d’identification (un ID Client et une clé secrète Client) pour toopush de Engagement toobe en mesure de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="b9b43-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="b9b43-117">Une clé d'API qui doit être intégrée à votre application.</span><span class="sxs-lookup"><span data-stu-id="b9b43-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="b9b43-118">Intégration du SDK</span><span class="sxs-lookup"><span data-stu-id="b9b43-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="b9b43-119">Gestion des inscriptions des appareils</span><span class="sxs-lookup"><span data-stu-id="b9b43-119">Managing device registrations</span></span>
<span data-ttu-id="b9b43-120">Chaque appareil doit envoyer un toohello de commande d’inscription des serveurs ADM, sinon ils ne peuvent pas être atteint.</span><span class="sxs-lookup"><span data-stu-id="b9b43-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="b9b43-121">Si vous utilisez déjà hello [bibliothèque cliente ADM]et vous avez déjà [intégré ADM] vous pouvez directement accéder à recevoir de tooandroid-sdk-adm.</span><span class="sxs-lookup"><span data-stu-id="b9b43-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="b9b43-122">Si vous n’avez pas intégré ADM, Engagement a un tooenable de façon plus simple dans votre application :</span><span class="sxs-lookup"><span data-stu-id="b9b43-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="b9b43-123">Modifiez le fichier `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="b9b43-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="b9b43-124">Ajoutez hello Amazon espace de noms, le fichier de hello doit commencer comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9b43-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="b9b43-125">À l’intérieur hello `<application/>` , ajoutez cette section :</span><span class="sxs-lookup"><span data-stu-id="b9b43-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="b9b43-126">Après avoir ajouté la balise d’amazon hello, vous avez peut-être une erreur de build si votre cible de Build de projet est sous Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="b9b43-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="b9b43-127">Vous avez toouse un **Android 2.1 +** cible de génération (ne vous inquiétez pas, vous pouvez toujours avoir un `minSdkVersion` définir too4).</span><span class="sxs-lookup"><span data-stu-id="b9b43-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="b9b43-128">Intégrer hello ADM clé d’API comme un élément multimédia en suivant [cette procédure].</span><span class="sxs-lookup"><span data-stu-id="b9b43-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="b9b43-129">Suivez ensuite les instructions hello des sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="b9b43-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="b9b43-130">Service de Push de l’Engagement d’enregistrement id toohello de communiquer et de recevoir des notifications</span><span class="sxs-lookup"><span data-stu-id="b9b43-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="b9b43-131">Dans l’ordre toocommunicate hello l’id d’inscription de toohello de périphérique hello Engagement Push du service et recevoir ses notifications, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise (même si vous utilisez ADM sans Engagement) :</span><span class="sxs-lookup"><span data-stu-id="b9b43-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="b9b43-132">Assurez-vous d’avoir hello suivant des autorisations dans votre `AndroidManifest.xml` (avant hello `</application>` balise).</span><span class="sxs-lookup"><span data-stu-id="b9b43-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="b9b43-133">Accorder à Engagement des informations d'identification OAuth</span><span class="sxs-lookup"><span data-stu-id="b9b43-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="b9b43-134">Envoyez vos informations d’identification OAuth (ID client et clé secrète client) sur le portail Engagement.</span><span class="sxs-lookup"><span data-stu-id="b9b43-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[bibliothèque cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[intégré ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[cette procédure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
