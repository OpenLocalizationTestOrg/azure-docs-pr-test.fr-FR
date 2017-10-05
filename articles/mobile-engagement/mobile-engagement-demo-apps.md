---
title: "Application de démonstration Azure Mobile Engagement | Microsoft Docs"
description: "Explique où télécharger, et comment utiliser et tirer parti des avantages de l’application de démonstration Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 8381edb569e19a85c1259f7791b477cfa6e51ea3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-demo-app"></a><span data-ttu-id="77d7d-103">Application de démonstration d’Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="77d7d-103">Azure Mobile Engagement demo app</span></span>
<span data-ttu-id="77d7d-104">Nous avons publié une application de démonstration d’Azure Mobile Engagement pour les plateformes **iOS**, **Android** et **Windows** pour vous aider à trouver des ressources utiles et à en savoir plus sur Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-104">We've published an Azure Mobile Engagement demo app for **iOS**, **Android**, and **Windows** platforms to help you to find useful resources and learn more about Mobile Engagement.</span></span>

<span data-ttu-id="77d7d-105">Grâce à cette application, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="77d7d-105">The app helps you to:</span></span>

* <span data-ttu-id="77d7d-106">Trouver facilement des liens utiles vers des ressources pour Mobile Engagement, telles que des vidéos, de la documentation, le forum d’assistance et le centre d’envoi de demandes de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="77d7d-106">Easily find useful links to Mobile Engagement resources like videos, documentation, the support forum, and where to go to raise feature requests.</span></span>
* <span data-ttu-id="77d7d-107">Tester des exemples de notifications prises en charge par Mobile Engagement pour trouver des idées pour vos propres applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="77d7d-107">Experience sample notifications that are supported by Mobile Engagement to get ideas for your own mobile applications.</span></span>
* <span data-ttu-id="77d7d-108">Utiliser une implémentation de référence pour étudier comment implémenter Mobile Engagement dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-108">Use a reference implementation to study how to implement Mobile Engagement into your own app.</span></span> <span data-ttu-id="77d7d-109">Vous découvrirez comment :</span><span class="sxs-lookup"><span data-stu-id="77d7d-109">You can learn to:</span></span>
  
  * <span data-ttu-id="77d7d-110">Recueillir des données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="77d7d-110">Collect analytics data.</span></span>
  * <span data-ttu-id="77d7d-111">Implémenter des scénarios de notification avancés de type *Plein écran interstitiel* ou *Fenêtre contextuelle*.</span><span class="sxs-lookup"><span data-stu-id="77d7d-111">Implement advanced notification scenarios of types such as *Full-screen interstitial* or *Pop-up*.</span></span>
  * <span data-ttu-id="77d7d-112">Implémenter des enquêtes et des sondages.</span><span class="sxs-lookup"><span data-stu-id="77d7d-112">Implement surveys and polls.</span></span>
  * <span data-ttu-id="77d7d-113">Implémenter des scénarios push et push données sans assistance.</span><span class="sxs-lookup"><span data-stu-id="77d7d-113">Implement silent push data and push scenarios.</span></span>   

## <a name="app-installation"></a><span data-ttu-id="77d7d-114">Installation de l’application</span><span class="sxs-lookup"><span data-stu-id="77d7d-114">App installation</span></span>
<span data-ttu-id="77d7d-115">Cette application est disponible dans les magasins d’applications suivants :</span><span class="sxs-lookup"><span data-stu-id="77d7d-115">This app is available in the following app stores:</span></span>

* <span data-ttu-id="77d7d-116">**Application de démonstration universelle Windows**:</span><span class="sxs-lookup"><span data-stu-id="77d7d-116">**Windows Universal demo app**:</span></span>
  
  * <span data-ttu-id="77d7d-117">Téléchargez l’application à partir du [Windows Store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span><span class="sxs-lookup"><span data-stu-id="77d7d-117">Download the app at the [Windows App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span></span>
  * <span data-ttu-id="77d7d-118">L’application a été développée comme application universelle Windows 10.</span><span class="sxs-lookup"><span data-stu-id="77d7d-118">The app was developed as a Windows 10 Universal app.</span></span> <span data-ttu-id="77d7d-119">Le code source est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span><span class="sxs-lookup"><span data-stu-id="77d7d-119">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span></span>
* <span data-ttu-id="77d7d-120">**Application de démonstration iOS**:</span><span class="sxs-lookup"><span data-stu-id="77d7d-120">**iOS demo app**:</span></span>
  
  * <span data-ttu-id="77d7d-121">Téléchargez l’application à partir de l’ [Apple Store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span><span class="sxs-lookup"><span data-stu-id="77d7d-121">Download the app at the [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span></span>
  * <span data-ttu-id="77d7d-122">L’application a été développée dans iOS Swift.</span><span class="sxs-lookup"><span data-stu-id="77d7d-122">The app was developed in iOS Swift.</span></span> <span data-ttu-id="77d7d-123">Le code source est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span><span class="sxs-lookup"><span data-stu-id="77d7d-123">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span></span>
* <span data-ttu-id="77d7d-124">**Application de démonstration Android**:</span><span class="sxs-lookup"><span data-stu-id="77d7d-124">**Android demo app**:</span></span>
  
  * <span data-ttu-id="77d7d-125">Téléchargez l’application à partir du [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span><span class="sxs-lookup"><span data-stu-id="77d7d-125">Download the app at the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span></span>
  * <span data-ttu-id="77d7d-126">Le code source est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span><span class="sxs-lookup"><span data-stu-id="77d7d-126">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span></span>

![Application de démonstration universelle Windows][1]

<span data-ttu-id="77d7d-128">![Application de démonstration iOS][2]
![Application de démonstration Android][3]</span><span class="sxs-lookup"><span data-stu-id="77d7d-128">![iOS demo app][2]
![Android demo app][3]</span></span>

## <a name="usage"></a><span data-ttu-id="77d7d-129">Usage</span><span class="sxs-lookup"><span data-stu-id="77d7d-129">Usage</span></span>
<span data-ttu-id="77d7d-130">Vous pouvez utiliser cette application des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="77d7d-130">You can use this app in the following ways:</span></span>

<span data-ttu-id="77d7d-131">**Téléchargez l’application sur votre appareil à partir des liens des boutiques d’applications (fournis ci-dessus) :**</span><span class="sxs-lookup"><span data-stu-id="77d7d-131">**Download the app on your device from the application store links (provided earlier):**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77d7d-132">Vous n’avez pas besoin de compte Azure, ni de connecter l’application à un serveur principal.</span><span class="sxs-lookup"><span data-stu-id="77d7d-132">You don't need an Azure account or need to connect the app to a back end.</span></span> <span data-ttu-id="77d7d-133">L’application fonctionne de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="77d7d-133">The app works independently.</span></span>
> 
> 

* <span data-ttu-id="77d7d-134">Une fois l’application téléchargée sur votre appareil, faites défiler les liens dans le menu de gauche pour rechercher les ressources utiles concernant Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-134">After you have the app on your device, then you can go through the links in the left-side menu to find the useful resources about Mobile Engagement.</span></span>
* <span data-ttu-id="77d7d-135">Nous avons ajouté le [flux RSS de notre service](https://aka.ms/azmerssfeed) dans cette application pour vous tenir informé des dernières mises à jour de produits.</span><span class="sxs-lookup"><span data-stu-id="77d7d-135">We've added the [service's RSS feed](https://aka.ms/azmerssfeed) into this application so that you're always updated about the latest product updates.</span></span>
* <span data-ttu-id="77d7d-136">Vous pouvez également parcourir les exemples de scénarios de notification pour découvrir les types de notifications prises en charge par Mobile Engagement pour chacune des plateformes.</span><span class="sxs-lookup"><span data-stu-id="77d7d-136">You can also go through the sample notification scenarios to experience the type of notifications that are supported by Mobile Engagement for each platform.</span></span> <span data-ttu-id="77d7d-137">Ces notifications peuvent être testées localement. Vous pouvez par exemple cliquer sur les boutons des écrans pour obtenir une expérience de notifications identique à celle dont vous bénéficiez quand vous envoyez les notifications à partir de la plateforme Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-137">These notifications can be experienced locally--that is, you can click the buttons on the screens to show you the notifications experience, which is identical to sending the notifications from the Mobile Engagement platform.</span></span>

![Menu de l’application pour Windows][4]

<span data-ttu-id="77d7d-139">![Menu de l’application pour iOS][5]
![Menu de l’application pour Android][6]</span><span class="sxs-lookup"><span data-stu-id="77d7d-139">![App menu for iOS][5]
![App menu for Android][6]</span></span>

<span data-ttu-id="77d7d-140">**Téléchargez le code source à partir des liens Github (fournis ci-dessus) :**</span><span class="sxs-lookup"><span data-stu-id="77d7d-140">**Download the source code from the GitHub links (provided earlier):**</span></span>

* <span data-ttu-id="77d7d-141">Une fois que vous avez téléchargé le code source, ouvrez-le dans votre environnement de développement, c’est-à-dire XCode pour iOS, Android Studio pour Android et Visual Studio pour Windows.</span><span class="sxs-lookup"><span data-stu-id="77d7d-141">After you've downloaded the source code, open it in the respective development environment--XCode for iOS, Android Studio for Android, and Visual Studio for Windows.</span></span>
* <span data-ttu-id="77d7d-142">Nous vous invitons ensuite à suivre les [étapes de base de l’intégration du SDK](mobile-engagement-windows-store-dotnet-get-started.md) pour pouvoir connecter cette application à sa propre instance de serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-142">You should next follow our [basic SDK integration steps](mobile-engagement-windows-store-dotnet-get-started.md) so that you're able to connect this app to its own Mobile Engagement back-end instance.</span></span>
  * <span data-ttu-id="77d7d-143">Vous devez configurer une chaîne de connexion dans l’application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-143">You need to configure a connection string in the app.</span></span>
  * <span data-ttu-id="77d7d-144">Vous devez également configurer la plateforme de notifications push pour votre application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-144">You also need to configure the push notification platform for your app.</span></span>
* <span data-ttu-id="77d7d-145">Vous remarquerez que l’application proprement dite est instrumentée avec Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-145">You'll notice that the app itself is instrumented with Mobile Engagement.</span></span> <span data-ttu-id="77d7d-146">Ainsi, quand vous ouvrez l’application après l’avoir connectée au serveur principal, vous pouvez voir la session utilisateur, les activités, les événements, et ainsi de suite, sous l’onglet **Monitor** (Surveiller).</span><span class="sxs-lookup"><span data-stu-id="77d7d-146">Therefore, as you open the app after connecting it to the back end, you'll be able to see the user session, activities, events, and so on, on the **Monitor** tab.</span></span>
* <span data-ttu-id="77d7d-147">Vous pouvez également envoyer des notifications à cette application à partir de votre propre instance Mobile Engagement, au lieu de recourir à des notifications locales.</span><span class="sxs-lookup"><span data-stu-id="77d7d-147">You'll also be able to send notifications to this app from your own Mobile Engagement instance, instead of using local notifications.</span></span>
  
  * <span data-ttu-id="77d7d-148">Ici vous pouvez ajouter votre appareil comme appareil test à l’aide de l’élément de menu **Get the Device ID** (Obtenir l’ID d’appareil) dans l’application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-148">Here you can add your device as a test device by using the **Get the Device ID** menu item in the app.</span></span> <span data-ttu-id="77d7d-149">Vous obtenez alors un ID d’appareil, que vous inscrivez ensuite comme appareil test avec l’instance de serveur principal de votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="77d7d-149">This gives you a device ID that you then register as a test device with your platform back-end instance.</span></span>
    
    ![ID d’appareil sur Windows][7]
    
    <span data-ttu-id="77d7d-151">![ID d’appareil sur iOS][8]
    ![ID d’appareil sur Android][9]</span><span class="sxs-lookup"><span data-stu-id="77d7d-151">![Device ID on iOS][8]
![Device ID on Android][9]</span></span>

## <a name="key-features-of-the-demo-app"></a><span data-ttu-id="77d7d-152">Principales fonctionnalités de l’application de démonstration</span><span class="sxs-lookup"><span data-stu-id="77d7d-152">Key features of the demo app</span></span>
* <span data-ttu-id="77d7d-153">Comme nous l’avons indiqué plus haut, cette application réunit toutes les ressources essentielles liées à Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-153">As mentioned earlier, with this app, you have all the key resources for Mobile Engagement in your hand.</span></span> <span data-ttu-id="77d7d-154">Vous pouvez faire défiler les liens dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="77d7d-154">You can go through the links on the left menu.</span></span>
* <span data-ttu-id="77d7d-155">Pour chaque plateforme, vous pouvez tester les notifications hors de l’application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-155">You can experience out-of-app notifications for each platform.</span></span> <span data-ttu-id="77d7d-156">Ces notifications peuvent être fournies sous forme de **notification uniquement**, auquel cas le fait de cliquer sur la notification a simplement pour effet d’ouvrir un écran natif de l’application (à l’aide de **liens profonds**), ou sous forme **d’annonce web**, auquel cas vous pouvez fournir du contenu HTML supplémentaire à partir du serveur principal Mobile Engagement qui sera affiché chaque fois que l’utilisateur cliquera sur la notification.</span><span class="sxs-lookup"><span data-stu-id="77d7d-156">These notifications can be delivered as **Notification only**, where clicking the notification simply opens up a native screen of the application (by using **deep linking**)--or as a **Web announcement**, where you can deliver additional HTML content from the Mobile Engagement back end to be displayed when the notification is clicked.</span></span>
  
    ![Notifications hors de l’application][29]
* <span data-ttu-id="77d7d-158">Dans iOS, vous devez fermer l’application pour voir les notifications hors de l’application ou les notifications push système.</span><span class="sxs-lookup"><span data-stu-id="77d7d-158">On iOS, you have to close the app to see the out-of-app or system push notifications.</span></span> <span data-ttu-id="77d7d-159">Vous pouvez examiner ici l’implémentation pour ajouter des **boutons d’action** comme ceux ajoutés à cette notification hors de l’application pour les fonctions *Feedback* (Commentaires) et *Share* (Partager) (pour que l’utilisateur puisse prendre des mesures directement à partir de la notification).</span><span class="sxs-lookup"><span data-stu-id="77d7d-159">You can look at the implementation here for adding **Action buttons**, like the ones that are added to this out-of-app notification for *Feedback* and *Share* (so that the user can take action right from the notification itself).</span></span>
  
    ![Notifications hors de l’application sur iOS][11] ![Affichage de notification hors de l’application sur iOS][14]
* <span data-ttu-id="77d7d-162">Dans Android, les options prises en charge ajoutent un texte multiligne (**Big Text**) ou une image de notification (**Big Picture**) ajouté(e) à la notification parallèlement aux **boutons d’action** (pris en charge par iOS).</span><span class="sxs-lookup"><span data-stu-id="77d7d-162">On Android, the options that are supported are adding multiline text (**Big Text**) or a notification image (**Big Picture**) to the notification, along with the **Action buttons** (as supported by iOS).</span></span>
  
    ![Notifications hors de l’application sur Android][12] ![Affichage de notification hors de l’application sur Android][15]
* <span data-ttu-id="77d7d-165">Dans Windows 10, vous pouvez visualiser les notifications telles qu’elles apparaissent sur le PC.</span><span class="sxs-lookup"><span data-stu-id="77d7d-165">On Windows 10, you can see how the notifications look on the PC.</span></span> <span data-ttu-id="77d7d-166">Cette notification s’affiche également dans le **Centre de notifications**Windows 10.</span><span class="sxs-lookup"><span data-stu-id="77d7d-166">This notification also shows up in the Windows 10 **Notification Center**.</span></span> <span data-ttu-id="77d7d-167">L’ajout de **boutons d’action** n’est pour le moment pas pris en charge avec le SDK Windows.</span><span class="sxs-lookup"><span data-stu-id="77d7d-167">There is no support for adding **Action buttons** at the moment in the Windows SDK.</span></span>
  
    ![Notifications hors de l’application sur Windows][10] ![Affichage de notification hors de l’application sur Windows][13]
* <span data-ttu-id="77d7d-170">Pour chaque plateforme, vous pouvez tester les notifications « dans l’application ».</span><span class="sxs-lookup"><span data-stu-id="77d7d-170">You can experience default "in-app" notifications for each platform.</span></span> <span data-ttu-id="77d7d-171">Il s’agit d’une expérience en deux étapes où une fenêtre **Notification** est affichée en premier.</span><span class="sxs-lookup"><span data-stu-id="77d7d-171">This is a two-step experience where a **Notification** window is displayed first.</span></span> <span data-ttu-id="77d7d-172">Quand vous cliquez dessus, une **annonce**s’affiche en plein écran, comme illustré dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="77d7d-172">When you click it, it opens up a full screen **Announcement**, as displayed in the following screenshot.</span></span> <span data-ttu-id="77d7d-173">Le contenu de cette annonce provient de votre instance de serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77d7d-173">The content of this announcement comes from your Mobile Engagement back-end instance.</span></span> <span data-ttu-id="77d7d-174">Le SDK contient les modèles pour les notifications et les annonces.</span><span class="sxs-lookup"><span data-stu-id="77d7d-174">The SDK has the templates for both notifications and announcements.</span></span> <span data-ttu-id="77d7d-175">Vous pouvez facilement les personnaliser, comme illustré dans cette application de démonstration, avec l’ajout de notre logo et de nos couleurs.</span><span class="sxs-lookup"><span data-stu-id="77d7d-175">You can easily customize them, as shown in this demo app with the addition of our logo and coloring.</span></span>  
  
    ![Notifications dans l’application sur Windows][16]
  
    ![Notifications dans l’application sur iOS][17]  ![Notifications dans l’application sur Android][18]
  
    <span data-ttu-id="77d7d-179">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="77d7d-179">**iOS**, **Android**</span></span>
* <span data-ttu-id="77d7d-180">Vous pouvez également utiliser la fonction **Catégorie** de Mobile Engagement pour personnaliser cette expérience par défaut.</span><span class="sxs-lookup"><span data-stu-id="77d7d-180">You can also use the **Category** feature of Mobile Engagement to customize this default experience.</span></span> <span data-ttu-id="77d7d-181">Dans l’application de démonstration, nous avons présenté deux façons courantes de modifier l’expérience des notifications.</span><span class="sxs-lookup"><span data-stu-id="77d7d-181">In the demo app, we've demonstrated two common ways to change the experience of the notifications.</span></span> <span data-ttu-id="77d7d-182">Notez que la fonction Catégorie n’est pas encore prise en charge dans le SDK Windows.</span><span class="sxs-lookup"><span data-stu-id="77d7d-182">Note that the Category feature is not yet supported in the Windows SDK.</span></span>
  
    <span data-ttu-id="77d7d-183">**Plein écran interstitiel :**</span><span class="sxs-lookup"><span data-stu-id="77d7d-183">**Full-screen interstitial:**</span></span>
  
    ![Notification dans l’application - catégorie interstitielle][30]
  
    ![Catégorie interstitielle sur iOS][21]     ![Catégorie interstitielle sur Android][22]
  
    <span data-ttu-id="77d7d-187">**Notification contextuelle :**</span><span class="sxs-lookup"><span data-stu-id="77d7d-187">**Pop-up notification:**</span></span>
  
    ![Notification dans l’application - catégorie contextuelle][31]
  
    ![Notification contextuelle sur iOS][19]    ![Notification contextuelle sur Android][20]

<span data-ttu-id="77d7d-191">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="77d7d-191">**iOS**, **Android**</span></span>

* <span data-ttu-id="77d7d-192">Mobile Engagement prend également en charge un type spécialisé de notification dans l’application appelée **Sondages**.</span><span class="sxs-lookup"><span data-stu-id="77d7d-192">Mobile Engagement also supports a specialized type of in-app notification called **Polls**.</span></span> <span data-ttu-id="77d7d-193">Vous pouvez envoyer rapidement des enquêtes à vos utilisateurs d’application segmentés.</span><span class="sxs-lookup"><span data-stu-id="77d7d-193">This allows you to send out quick surveys to your segmented app users.</span></span> <span data-ttu-id="77d7d-194">Vous pouvez aussi ajouter des questions et des options pour chaque question, comme illustré dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="77d7d-194">You can add questions and options for each question as in the following screenshot.</span></span> <span data-ttu-id="77d7d-195">Ces éléments sont ensuite présentés à l’utilisateur de l’application comme notification dans l’application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-195">This will then get displayed as an in-app notification to the app user.</span></span>   
  
    ![Notifications d’interrogation][32]
  
    ![Enquête sur Windows][26]
  
    ![Enquête sur iOS][27]   ![Enquête sur Android][28]

<span data-ttu-id="77d7d-200">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="77d7d-200">**iOS**, **Android**</span></span>

* <span data-ttu-id="77d7d-201">Mobile Engagement prend également en charge l’envoi en mode silencieux de notifications **Push de données** .</span><span class="sxs-lookup"><span data-stu-id="77d7d-201">Mobile Engagement also supports sending silent **Data Push** notifications.</span></span> <span data-ttu-id="77d7d-202">Avec ces notifications, vous pouvez envoyer des données à partir de votre service (comme les données JSON dans l’exemple suivant), que vous pouvez gérer et exploiter directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="77d7d-202">With these notifications, you can send data from your service (like the JSON data in the following example), which you can handle in your app and take some action.</span></span> <span data-ttu-id="77d7d-203">La modification du prix d’un article de manière sélective à l’aide des notifications Push de données constitue un bon exemple.</span><span class="sxs-lookup"><span data-stu-id="77d7d-203">An example is how we're changing the price of an item selectively by using data push notifications.</span></span>
  
    ![Notification Push de données][33]
  
    ![Notification Push de données sur Windows][23]
  
    ![Notification Push de données sur iOS][24]  ![Notification Push de données sur Android][25]

<span data-ttu-id="77d7d-208">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="77d7d-208">**iOS**, **Android**</span></span>

> [!NOTE]
> <span data-ttu-id="77d7d-209">Vous pouvez afficher des instructions détaillées pour chacune de ces notifications en cliquant sur le lien **Cliquez ici pour obtenir des instructions sur l’envoi de ces notifications à partir de la plateforme Mobile Engagement** à partir de n’importe quel écran d’exemple de notification.</span><span class="sxs-lookup"><span data-stu-id="77d7d-209">You can view detailed step-by-step instructions for any of these notifications by clicking **Click here for instructions on how to send these notifications from Mobile Engagement platform** on any sample notification screen.</span></span>
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
