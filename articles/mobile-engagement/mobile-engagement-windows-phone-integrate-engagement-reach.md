---
title: "aaaWindows intégration du Kit de développement logiciel Silverlight atteindre téléphone"
description: Comment tooIntegrate Azure Mobile Engagement atteindre avec les applications Silverlight Windows Phone
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
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="f8bfa-103">Intégration du Kit de développement logiciel (SDK) du module Couverture Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f8bfa-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="f8bfa-104">Vous devez suivre la procédure d’intégration hello décrite dans hello [intégration du Kit de développement logiciel Windows Phone Silverlight Engagement](mobile-engagement-windows-phone-integrate-engagement.md) avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="f8bfa-105">Incorporer hello SDK Reach d’Engagement dans votre projet Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f8bfa-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="f8bfa-106">Vous n’avez rien tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-106">You do not have anything tooadd.</span></span> <span data-ttu-id="f8bfa-107">`EngagementReach` se trouvent déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="f8bfa-108">Vous pouvez personnaliser les images situés dans hello `Resources` dossier de votre projet, en particulier hello marque icône (cette valeur par défaut toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="f8bfa-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="f8bfa-109">Ajouter des fonctionnalités hello</span><span class="sxs-lookup"><span data-stu-id="f8bfa-109">Add hello capabilities</span></span>
<span data-ttu-id="f8bfa-110">Hello SDK Reach d’Engagement a besoin des fonctions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="f8bfa-111">Ouvrez votre `WMAppManifest.xml` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="f8bfa-112">Hello tout d’abord un est utilisé par hello MPNS service tooallow hello affichage de notification de toast.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="f8bfa-113">Hello second est utilisé tooembed une tâche de navigateur dans le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="f8bfa-114">Modifier hello `WMAppManifest.xml` et ajoutez à l’intérieur de hello `<Capabilities />` balise :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="f8bfa-115">Activer hello services de notifications Push Microsoft</span><span class="sxs-lookup"><span data-stu-id="f8bfa-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="f8bfa-116">Bonjour toouse de commande **les services de notifications Push Microsoft** (désignées comme MPNS) votre `WMAppManifest.xml` fichier doit avoir un `<App />` la balise avec un `Publisher` attribut défini toohello nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="f8bfa-117">Initialiser hello SDK Reach d’Engagement</span><span class="sxs-lookup"><span data-stu-id="f8bfa-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="f8bfa-118">Configuration d'Engagement</span><span class="sxs-lookup"><span data-stu-id="f8bfa-118">Engagement configuration</span></span>
<span data-ttu-id="f8bfa-119">configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="f8bfa-120">Modifiez cette configuration de portée de fichier toospecify :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="f8bfa-121">*Facultatif*, indiquent si le push natif hello (MPNS) est activé ou pas entre `<enableNativePush>` et `</enableNativePush>` balises (`true` par défaut).</span><span class="sxs-lookup"><span data-stu-id="f8bfa-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="f8bfa-122">*Facultatif*, indiquez le nom du canal de transmission hello entre hello `<channelName>` et `</channelName>` fournissent des balises, hello même que votre application peut actuellement utiliser ou laissez-le vide.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="f8bfa-123">Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="f8bfa-124">Vous pouvez spécifier le nom de hello de hello de canal MPNS push de votre application.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="f8bfa-125">Par défaut, Engagement crée un nom basé sur hello appId.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="f8bfa-126">Vous n’avez aucun besoin de toospecify hello nom vous-même, sauf si vous prévoyez de canal de transmission toouse hello en dehors de l’Engagement.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="f8bfa-127">Initialisation d'Engagement</span><span class="sxs-lookup"><span data-stu-id="f8bfa-127">Engagement initialization</span></span>
<span data-ttu-id="f8bfa-128">Modifier hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="f8bfa-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="f8bfa-129">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="f8bfa-130">Insérez `EngagementReach.Instance.Init` juste après `EngagementAgent.Instance.Init` dans `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="f8bfa-131">Insérer `EngagementReach.Instance.OnActivated` Bonjour `Application_Activated` méthode :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="f8bfa-132">Hello `EngagementReach.Instance.Init` s’exécute dans un thread dédié.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="f8bfa-133">Vous n’avez pas toodo il vous-même.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="f8bfa-134">Considérations relatives à la soumission App store</span><span class="sxs-lookup"><span data-stu-id="f8bfa-134">App store submission considerations</span></span>
<span data-ttu-id="f8bfa-135">Microsoft impose certaines règles lors de l’utilisation des notifications push de hello :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="f8bfa-136">À partir de hello Microsoft [stratégies d’Application] documentation, section 2.9 :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="f8bfa-137">Vous devez demander des notifications push de hello utilisateur tooaccept tooreceive.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="f8bfa-138">Ajoutez ensuite une notifications push de façon toodisable hello dans vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="f8bfa-139">objet de EngagementReach Hello fournit deux méthodes toomanage hello/opt-retrait, `EnableNativePush()` et `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="f8bfa-140">Par exemple, vous pourriez créer une option dans les paramètres de hello avec un toodisable bascule ou activer MPNS.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="f8bfa-141">Vous pouvez également décider toodeactivate MPNS via la configuration d’Engagement hello\<configuration du portée Kit de développement logiciel windows phone\>.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="f8bfa-142">2.9.1) application hello doit décrivent tout d’abord toobe de notifications hello fourni et **obtenir l’autorisation de l’utilisateur hello express (opt-in)**, et **doivent fournir un mécanisme via le hello utilisateur peut refuser de réception notifications Push**.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="f8bfa-143">Toutes les notifications sont fournies à l’aide de hello services de notifications Push Microsoft doivent être cohérentes avec hello description fournie toohello utilisateur et doit respecter toutes applicables [stratégies d’Application] [ Content Policies]et [des exigences supplémentaires pour les Types d’Application spécifique].</span><span class="sxs-lookup"><span data-stu-id="f8bfa-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="f8bfa-144">Vous ne devez pas utiliser trop de notifications Push.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-144">You should not use too many push notifications.</span></span> <span data-ttu-id="f8bfa-145">Engagement gérera les notifications pour vous.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="f8bfa-146">2.9.2) application hello et son utilisation de services de notifications Push Microsoft de hello ne doivent pas excessivement utiliser la capacité de réseau ou de la bande passante de hello services de notifications Push Microsoft, ou sinon indûment surcharger un Windows Phone ou autre appareil de Microsoft ou un service avec excessive push notifications, comme déterminé par Microsoft à sa discrétion raisonnable et ne doit pas endommager ou interférer avec les réseaux Microsoft ou serveurs ou des serveurs tiers ni toohello de réseaux connectés services de notifications Push Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="f8bfa-147">Ne comptez pas sur des informations critiques et MPNS toosend.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="f8bfa-148">Engagement utilise MPNS, cette règle s’applique également pour les campagnes hello créées à l’intérieur de hello Engagement frontales.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="f8bfa-149">2.9.3) hello services de notifications Push Microsoft n’est peut-être pas les notifications toosend utilisés sont mission critique ou sinon peut affecter les questions de durée de vie ou de décès, y compris sans dispositif médical de limitation des notifications critiques tooa connexes ou de condition.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="f8bfa-150">MICROSOFT expressément exclut toute garantie que hello utilisation de hello MICROSOFT PUSH NOTIFICATION SERVICE ou remise de MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS sera être sans interruption, erreur libre, ou sinon garantie tooOCCUR ON A en temps réel base.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="f8bfa-151">**Nous ne pouvons pas garantir que votre application passe les processus de validation hello si vous ne respectez pas ces recommandations.**</span><span class="sxs-lookup"><span data-stu-id="f8bfa-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="f8bfa-152">Gérer les Push de données (facultatif)</span><span class="sxs-lookup"><span data-stu-id="f8bfa-152">Handle data push (optional)</span></span>
<span data-ttu-id="f8bfa-153">Si vous souhaitez que votre push de données application toobe tooreceive en mesure de portée, vous avez tooimplement deux événements de hello EngagementReach classe :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="f8bfa-154">Vous pouvez voir que le rappel hello de chaque méthode retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="f8bfa-155">Engagement envoie un back-end de commentaires tooits après la distribution de push de données hello.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="f8bfa-156">Si le rappel de hello retourne la valeur false, hello `exit` commentaires sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="f8bfa-157">Dans le cas contraire, il s'agira du retour `action`.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="f8bfa-158">Si aucun rappel n’est définie pour les événements de hello, hello `drop` commentaires seront affichera tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="f8bfa-159">Engagement n’est pas en mesure de tooreceive des évaluations de multiples pour un push de données.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="f8bfa-160">Si vous prévoyez tooset plusieurs gestionnaires d’un événement, n’oubliez pas que les commentaires hello correspondent toohello dernière celui envoyé.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="f8bfa-161">Dans ce cas, nous vous recommandons de tooalways renvoie hello même valeur tooavoid ayant des commentaires à confusion sur hello frontal.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="f8bfa-162">Personnaliser l'interface utilisateur (facultatif)</span><span class="sxs-lookup"><span data-stu-id="f8bfa-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="f8bfa-163">Première étape</span><span class="sxs-lookup"><span data-stu-id="f8bfa-163">First step</span></span>
<span data-ttu-id="f8bfa-164">Nous permettent de portée de hello toocustomize l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="f8bfa-165">toodo, vous devez toocreate une sous-classe de hello `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="f8bfa-166">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="f8bfa-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="f8bfa-167">Ensuite, définissez le contenu de hello hello `EngagementReach.Instance.Handler` champ avec votre objet personnalisé dans votre `App.xaml.cs` classe au sein de hello `Application_Launching` (méthode).</span><span class="sxs-lookup"><span data-stu-id="f8bfa-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="f8bfa-168">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="f8bfa-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="f8bfa-169">Par défaut, Engagement utilise sa propre implémentation de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="f8bfa-170">Vous n’avez pas toocreate votre propre, et si vous procédez ainsi, vous n’avez toooverride chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="f8bfa-171">comportement par défaut de Hello est un objet de base d’Engagement tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="f8bfa-172">Mises en forme</span><span class="sxs-lookup"><span data-stu-id="f8bfa-172">Layouts</span></span>
<span data-ttu-id="f8bfa-173">Par défaut, portée utilisera hello incorporée des ressources de notifications de hello DLL toodisplay hello et pages.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="f8bfa-174">Toutefois, vous pouvez décider toouse tooreflect de vos propres ressources votre marque dans ces composants.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="f8bfa-175">Vous pouvez remplacer `EngagementReachHandler` méthodes dans votre toouse d’Engagement de tootell sous-classe vos dispositions :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="f8bfa-176">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="f8bfa-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="f8bfa-177">Hello `CreateNotification` méthode peut retourner une valeur null.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="f8bfa-178">notification de Hello ne s’affiche et couverture de campagne hello ne sera supprimé.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="f8bfa-179">toosimplify votre implémentation de la mise en page, nous fournissons également notre propre code xaml qui permettre servir comme base pour votre code.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="f8bfa-180">Ils se trouvent dans l’archive du SDK de l’Engagement hello (/ src/portée).</span><span class="sxs-lookup"><span data-stu-id="f8bfa-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="f8bfa-181">sources de Hello que nous fournissons sont hello exacte mêmes que ceux que nous utilisons.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="f8bfa-182">Par conséquent, si vous souhaitez toomodify les directement, n’oubliez espace de noms toochange hello et hello nom.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="f8bfa-183">Position des notifications</span><span class="sxs-lookup"><span data-stu-id="f8bfa-183">Notification position</span></span>
<span data-ttu-id="f8bfa-184">Par défaut, une notification dans l’application s’affiche dans hello partie inférieure gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="f8bfa-185">Vous pouvez modifier ce comportement en substituant hello `GetNotificationPosition` méthode Hello `EngagementReachHandler` objet.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="f8bfa-186">Actuellement, vous pouvez choisir entre hello `BOTTOM` (par défaut) et `TOP` positions.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="f8bfa-187">Lancer un message</span><span class="sxs-lookup"><span data-stu-id="f8bfa-187">Launch message</span></span>
<span data-ttu-id="f8bfa-188">Lorsqu’un utilisateur clique sur une notification système (un toast), lance d’Engagement hello app, charge le contenu hello Hello transmettre des messages et afficher la page hello pour hello correspondant campagne.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="f8bfa-189">Il existe un décalage entre le lancement de hello de hello application et hello l’affichage de page hello (selon la vitesse de hello de votre réseau).</span><span class="sxs-lookup"><span data-stu-id="f8bfa-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="f8bfa-190">utilisateur toohello tooindicate quelque chose est en cours de chargement, vous devez fournir une informations visuelles, comme une barre de progression ou un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="f8bfa-191">Engagement ne peut pas gérer cela lui-même. Toutefois, il fournit plusieurs gestionnaires à cet effet.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="f8bfa-192">tooimplement hello rappel, procédez comme :</span><span class="sxs-lookup"><span data-stu-id="f8bfa-192">tooimplement hello callback, do:</span></span>

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="f8bfa-193">Vous pouvez définir le rappel de hello dans votre `Application_Launching` méthode de votre `App.xaml.cs` fichier, de préférence avant hello `EngagementReach.Instance.Init()` appeler.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="f8bfa-194">Chaque gestionnaire est appelé par le Thread d’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="f8bfa-195">Vous n’avez pas de tooworry lorsque vous utilisez un MessageBox ou quelque chose dépendant de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8bfa-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[stratégies d’Application]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[des exigences supplémentaires pour les Types d’Application spécifique]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

