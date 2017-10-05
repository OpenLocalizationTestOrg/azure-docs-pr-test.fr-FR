---
title: "Intégration du Kit de développement logiciel (SDK) du module Couverture Windows Phone Silverlight"
description: "Intégration du module Couverture d’Azure Mobile Engagement avec des applications Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="554d6-103">Intégration du Kit de développement logiciel (SDK) du module Couverture Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="554d6-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="554d6-104">Vous devez suivre la procédure d'intégration décrite dans la rubrique [Intégration du Kit de développement logiciel d’Engagement Windows Phone Silverlight  Engagement](mobile-engagement-windows-phone-integrate-engagement.md) avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="554d6-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="554d6-105">Intégration du SDK du module Couverture d'Engagement dans votre projet Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="554d6-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="554d6-106">Vous n'avez rien à ajouter.</span><span class="sxs-lookup"><span data-stu-id="554d6-106">You do not have anything to add.</span></span> <span data-ttu-id="554d6-107">`EngagementReach` se trouvent déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="554d6-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="554d6-108">Vous pouvez personnaliser les images situées dans le dossier `Resources` de votre projet, en particulier l'icône de marque (par défaut, il s'agit de l'icône d'Engagement).</span><span class="sxs-lookup"><span data-stu-id="554d6-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="554d6-109">Ajouter les fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="554d6-109">Add the capabilities</span></span>
<span data-ttu-id="554d6-110">Le Kit de développement logiciel (SDK) du module Couverture d'Engagement nécessite l'ajout de certaines fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="554d6-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="554d6-111">Ouvrez votre fichier `WMAppManifest.xml` et vérifiez que les fonctionnalités suivantes sont déclarées :</span><span class="sxs-lookup"><span data-stu-id="554d6-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="554d6-112">Le premier est utilisé par le service MPNS pour permettre l'affichage de notification toast.</span><span class="sxs-lookup"><span data-stu-id="554d6-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="554d6-113">L'autre est utilisé pour intégrer une tâche du navigateur dans le Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="554d6-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="554d6-114">Modifiez le fichier `WMAppManifest.xml` et ajoutez-le à l'intérieur de la balise `<Capabilities />` :</span><span class="sxs-lookup"><span data-stu-id="554d6-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="554d6-115">Activation du service de notifications Push Microsoft</span><span class="sxs-lookup"><span data-stu-id="554d6-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="554d6-116">Pour utiliser le **service de notifications Push Microsoft** (appelé MPNS), votre fichier `WMAppManifest.xml` doit contenir une balise `<App />` avec un attribut `Publisher` défini sur le nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="554d6-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="554d6-117">Initialiser le SDK du module Couverture d'Engagement</span><span class="sxs-lookup"><span data-stu-id="554d6-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="554d6-118">Configuration d'Engagement</span><span class="sxs-lookup"><span data-stu-id="554d6-118">Engagement configuration</span></span>
<span data-ttu-id="554d6-119">La configuration d'Engagement est centralisée dans le fichier `Resources\EngagementConfiguration.xml` de votre projet.</span><span class="sxs-lookup"><span data-stu-id="554d6-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="554d6-120">Modifiez ce fichier pour spécifier la configuration de couverture :</span><span class="sxs-lookup"><span data-stu-id="554d6-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="554d6-121">*Facultatif*, indiquez si l’installation du service Push natif (MPNS) est activée ou non entre les balises `<enableNativePush>` et `</enableNativePush>` (`true` par défaut).</span><span class="sxs-lookup"><span data-stu-id="554d6-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="554d6-122">*Facultatif*, indiquez le nom du canal de transmission Push entre les balises `<channelName>` et `</channelName>`. Indiquez celui utilisé par votre application ou laissez-le vide.</span><span class="sxs-lookup"><span data-stu-id="554d6-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="554d6-123">Si vous souhaitez plutôt le spécifier lors de l'exécution, vous pouvez appeler la méthode suivante avant l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="554d6-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="554d6-124">Vous pouvez spécifier le nom du canal de transmission MPNS de votre application.</span><span class="sxs-lookup"><span data-stu-id="554d6-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="554d6-125">Par défaut, Engagement crée un nom basé sur l'ID de l'application.</span><span class="sxs-lookup"><span data-stu-id="554d6-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="554d6-126">Il n'est pas nécessaire de spécifier le nom vous-même, sauf si vous prévoyez d'utiliser le canal Push en dehors d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="554d6-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="554d6-127">Initialisation d'Engagement</span><span class="sxs-lookup"><span data-stu-id="554d6-127">Engagement initialization</span></span>
<span data-ttu-id="554d6-128">Modifiez le fichier `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="554d6-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="554d6-129">Ajoutez à vos instructions `using` :</span><span class="sxs-lookup"><span data-stu-id="554d6-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="554d6-130">Insérez `EngagementReach.Instance.Init` juste après `EngagementAgent.Instance.Init` dans `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="554d6-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="554d6-131">Insérez `EngagementReach.Instance.OnActivated` dans la méthode `Application_Activated` :</span><span class="sxs-lookup"><span data-stu-id="554d6-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="554d6-132">`EngagementReach.Instance.Init` est exécuté dans un thread dédié.</span><span class="sxs-lookup"><span data-stu-id="554d6-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="554d6-133">Vous n'avez pas à le faire vous-même.</span><span class="sxs-lookup"><span data-stu-id="554d6-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="554d6-134">Considérations relatives à la soumission App store</span><span class="sxs-lookup"><span data-stu-id="554d6-134">App store submission considerations</span></span>
<span data-ttu-id="554d6-135">Microsoft impose certaines règles lors de l'utilisation de notifications Push :</span><span class="sxs-lookup"><span data-stu-id="554d6-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="554d6-136">Selon la documentation sur les [politiques d'applications] Microsoft, section 2.9 :</span><span class="sxs-lookup"><span data-stu-id="554d6-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="554d6-137">vous devez demander à l'utilisateur s'il accepte de recevoir des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="554d6-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="554d6-138">Ensuite, ajoutez un moyen de désactiver les notifications Push dans vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="554d6-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="554d6-139">L'objet EngagementReach fournit deux méthodes pour gérer les autorisations de réception : `EnableNativePush()` et `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="554d6-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="554d6-140">Par exemple, vous pouvez créer une option dans les paramètres avec un bouton bascule pour désactiver ou activer le service MPNS.</span><span class="sxs-lookup"><span data-stu-id="554d6-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="554d6-141">Vous pouvez également décider de désactiver MPNS via la configuration Engagement \<windows-phone-sdk-reach-configuration\>.</span><span class="sxs-lookup"><span data-stu-id="554d6-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="554d6-142">2.9.1) L’application doit tout d’abord décrire les notifications envoyées et **obtenir l’autorisation expresse de l’utilisateur**. Elle **doit également proposer un moyen de désactiver la réception de notifications Push**.</span><span class="sxs-lookup"><span data-stu-id="554d6-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="554d6-143">Toutes les notifications fournies par le biais des services Microsoft Push Notification doivent être cohérentes avec la description fournie à l'utilisateur et respecter toutes les [Stratégies d'application][Content Policies] et [exigences supplémentaires pour les types d'application spécifiques] applicables.</span><span class="sxs-lookup"><span data-stu-id="554d6-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="554d6-144">Vous ne devez pas utiliser trop de notifications Push.</span><span class="sxs-lookup"><span data-stu-id="554d6-144">You should not use too many push notifications.</span></span> <span data-ttu-id="554d6-145">Engagement gérera les notifications pour vous.</span><span class="sxs-lookup"><span data-stu-id="554d6-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="554d6-146">2.9.2) L'application et son utilisation du service MPNS ne doivent pas utiliser une capacité réseau ou une bande passante MNPS excessive, ni surcharger de notifications un appareil Windows Phone ou autre service ou appareil Microsoft, comme déterminé par Microsoft à sa discrétion, ni endommager ou interférer avec les réseaux ou serveurs Microsoft ou tout serveur ou serveurs tiers connectés au service MNPS.</span><span class="sxs-lookup"><span data-stu-id="554d6-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="554d6-147">N’utilisez pas le service MPNS pour envoyer des informations critiques.</span><span class="sxs-lookup"><span data-stu-id="554d6-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="554d6-148">Engagement utilise MPNS, cette règle s'applique donc aussi pour les campagnes créées dans le serveur frontal Engagement.</span><span class="sxs-lookup"><span data-stu-id="554d6-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="554d6-149">2.9.3) Le service MNPS ne peut pas être utilisé pour envoyer des notifications stratégiques ou pouvant toucher à la vie des utilisateurs, y compris, mais sans s'y limiter, les notifications critiques liées à une affection ou un dispositif médical.</span><span class="sxs-lookup"><span data-stu-id="554d6-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="554d6-150">MICROSOFT NE GARANTIT AUCUNEMENT LA NON-INTERRUPTION, L'ABSENCE D'ERREUR OU L'EXÉCUTION EN TEMPS RÉEL DE L'UTILISATION DU SERVICE MPNS OU DE LA LIVRAISON DES NOTIFICATIONS MPNS.</span><span class="sxs-lookup"><span data-stu-id="554d6-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="554d6-151">**Nous ne pouvons pas garantir que votre application soit validée si vous ne respectez pas ces recommandations.**</span><span class="sxs-lookup"><span data-stu-id="554d6-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="554d6-152">Gérer les Push de données (facultatif)</span><span class="sxs-lookup"><span data-stu-id="554d6-152">Handle data push (optional)</span></span>
<span data-ttu-id="554d6-153">Si vous voulez que votre application puisse recevoir les Push de données du module Couverture, vous devez implémenter deux événements de la classe EngagementReach :</span><span class="sxs-lookup"><span data-stu-id="554d6-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

<span data-ttu-id="554d6-154">Vous pouvez voir que le rappel de chaque méthode renvoie un booléen.</span><span class="sxs-lookup"><span data-stu-id="554d6-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="554d6-155">Engagement envoie un feedback à son serveur principal après la répartition des Push de données.</span><span class="sxs-lookup"><span data-stu-id="554d6-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="554d6-156">Si le rappel renvoie la valeur false, le retour `exit` sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="554d6-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="554d6-157">Dans le cas contraire, il s'agira du retour `action`.</span><span class="sxs-lookup"><span data-stu-id="554d6-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="554d6-158">Si aucun rappel n'est défini pour les événements, le retour `drop` sera envoyé à Engagement.</span><span class="sxs-lookup"><span data-stu-id="554d6-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="554d6-159">Engagement ne peut pas recevoir plusieurs feedbacks pour un Push de données.</span><span class="sxs-lookup"><span data-stu-id="554d6-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="554d6-160">Si vous prévoyez de définir plusieurs gestionnaires pour un événement, sachez que le feedback correspondra au dernier envoyé.</span><span class="sxs-lookup"><span data-stu-id="554d6-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="554d6-161">Dans ce cas, nous vous recommandons de toujours retourner la même valeur afin d'éviter un feedback prêtant à confusion sur le serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="554d6-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="554d6-162">Personnaliser l'interface utilisateur (facultatif)</span><span class="sxs-lookup"><span data-stu-id="554d6-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="554d6-163">Première étape</span><span class="sxs-lookup"><span data-stu-id="554d6-163">First step</span></span>
<span data-ttu-id="554d6-164">Il vous est possible de personnaliser l'interface utilisateur du module Couverture.</span><span class="sxs-lookup"><span data-stu-id="554d6-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="554d6-165">Pour cela, vous devez créer une sous-classe de la classe `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="554d6-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="554d6-166">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="554d6-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="554d6-167">Ensuite, définissez le contenu du champ `EngagementReach.Instance.Handler` à l'aide de votre objet personnalisé dans la classe `App.xaml.cs` de la méthode `Application_Launching`.</span><span class="sxs-lookup"><span data-stu-id="554d6-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="554d6-168">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="554d6-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="554d6-169">Par défaut, Engagement utilise sa propre implémentation de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="554d6-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="554d6-170">Il n'est pas nécessaire de créer votre propre implémentation. Toutefois, si vous le faites, vous n'aurez pas à remplacer chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="554d6-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="554d6-171">Le comportement par défaut consiste à sélectionner l'objet de base Engagement.</span><span class="sxs-lookup"><span data-stu-id="554d6-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="554d6-172">Mises en forme</span><span class="sxs-lookup"><span data-stu-id="554d6-172">Layouts</span></span>
<span data-ttu-id="554d6-173">Par défaut, le module Couverture utilise les ressources intégrées du DLL pour afficher les notifications et les pages.</span><span class="sxs-lookup"><span data-stu-id="554d6-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="554d6-174">Toutefois, vous pouvez décider d'utiliser vos propres ressources pour refléter votre marque dans ces composants.</span><span class="sxs-lookup"><span data-stu-id="554d6-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="554d6-175">Vous pouvez remplacer les méthodes `EngagementReachHandler` dans votre sous-classe pour indiquer à Engagement d'utiliser vos mises en forme :</span><span class="sxs-lookup"><span data-stu-id="554d6-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="554d6-176">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="554d6-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="554d6-177">La méthode `CreateNotification` peut renvoyer un résultat null.</span><span class="sxs-lookup"><span data-stu-id="554d6-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="554d6-178">La notification ne s'affichera pas et la couverture campagne est abandonnée.</span><span class="sxs-lookup"><span data-stu-id="554d6-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="554d6-179">Pour simplifier l'implémentation de votre mise en forme, nous fournissons également notre propre xaml qui peut servir de base pour votre code.</span><span class="sxs-lookup"><span data-stu-id="554d6-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="554d6-180">Il se trouve dans l'archive du SDK Engagement (/src/reach/).</span><span class="sxs-lookup"><span data-stu-id="554d6-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="554d6-181">Les sources que nous proposons sont absolument identiques à celles que nous utilisons.</span><span class="sxs-lookup"><span data-stu-id="554d6-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="554d6-182">Par conséquent, si vous souhaitez les modifier directement, n'oubliez pas de modifier l'espace de noms et le nom.</span><span class="sxs-lookup"><span data-stu-id="554d6-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="554d6-183">Position des notifications</span><span class="sxs-lookup"><span data-stu-id="554d6-183">Notification position</span></span>
<span data-ttu-id="554d6-184">Par défaut, une notification interne à l'application s'affiche dans la partie inférieure gauche de l'application.</span><span class="sxs-lookup"><span data-stu-id="554d6-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="554d6-185">Vous pouvez modifier ce comportement en remplaçant la méthode `GetNotificationPosition` de l'objet `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="554d6-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="554d6-186">Actuellement, vous pouvez choisir entre les positions `BOTTOM` (par défaut) et `TOP`.</span><span class="sxs-lookup"><span data-stu-id="554d6-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="554d6-187">Lancer un message</span><span class="sxs-lookup"><span data-stu-id="554d6-187">Launch message</span></span>
<span data-ttu-id="554d6-188">Lorsqu'un utilisateur clique sur une notification du système (un toast), Engagement lance l'application, charge le contenu des messages envoyés et affiche la page de la campagne correspondante.</span><span class="sxs-lookup"><span data-stu-id="554d6-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="554d6-189">Il y a un délai entre le lancement de l'application et l'affichage de la page (qui dépend de la vitesse de votre réseau).</span><span class="sxs-lookup"><span data-stu-id="554d6-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="554d6-190">Pour indiquer à l'utilisateur qu'un chargement est en cours, vous devez fournir une indication visuelle, telle qu'une barre ou un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="554d6-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="554d6-191">Engagement ne peut pas gérer cela lui-même. Toutefois, il fournit plusieurs gestionnaires à cet effet.</span><span class="sxs-lookup"><span data-stu-id="554d6-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="554d6-192">Pour implémenter le rappel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="554d6-192">To implement the callback, do:</span></span>

    /* The application has launched and the content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* The application has finished loading the content and the page
     * is about to be displayed.
     * You should hide the indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* The content has been loaded, but an error has occurred.
     * You can provide an information to the user.
     * You should hide the indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="554d6-193">Vous pouvez définir le rappel dans la méthode `Application_Launching` de votre fichier `App.xaml.cs`, de préférence avant l'appel `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="554d6-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="554d6-194">Chaque gestionnaire est appelé par le thread d'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="554d6-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="554d6-195">Vous n'avez pas de souci à vous faire quand vous utilisez un MessageBox ou autre objet d'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="554d6-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="554d6-196">[politiques d'applications]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="554d6-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="554d6-197">[exigences supplémentaires pour les types d'application spécifiques]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="554d6-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

