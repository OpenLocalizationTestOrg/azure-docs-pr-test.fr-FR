---
title: "aaaWindows Universal intégration du Kit de développement logiciel atteindre applications"
description: Comment tooIntegrate Azure Mobile Engagement atteindre avec les applications Windows universelles
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="e6b1c-103">Intégration du Kit de développement logiciel du module Couverture des applications Windows Universal</span><span class="sxs-lookup"><span data-stu-id="e6b1c-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="e6b1c-104">Vous devez suivre la procédure d’intégration hello décrite dans hello [intégration du Kit de développement logiciel Windows universel Engagement](mobile-engagement-windows-store-integrate-engagement.md) avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="e6b1c-105">Incorporer hello SDK Reach d’Engagement dans votre projet Windows universel</span><span class="sxs-lookup"><span data-stu-id="e6b1c-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="e6b1c-106">Vous n’avez rien tooadd.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-106">You do not have anything tooadd.</span></span> <span data-ttu-id="e6b1c-107">`EngagementReach` se trouvent déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="e6b1c-108">Vous pouvez personnaliser les images situés dans hello `Resources` dossier de votre projet, en particulier hello marque icône (cette valeur par défaut toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="e6b1c-109">Sur les applications universelles, vous pouvez également déplacer hello `Resources` dossier sur votre tooshare projet partagé son contenu entre les applications, mais vous aurez tookeep hello `Resources\EngagementConfiguration.xml` des fichiers sur son emplacement par défaut car il est dépendant de la plate-forme.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="e6b1c-110">Activer hello Service de Notification Windows</span><span class="sxs-lookup"><span data-stu-id="e6b1c-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="e6b1c-111">Windows 8.x et Windows Phone 8.1 uniquement</span><span class="sxs-lookup"><span data-stu-id="e6b1c-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="e6b1c-112">Bonjour toouse de commande **Service de Notification Windows** (désignées comme WNS) dans votre `Package.appxmanifest` des fichiers sur `Application UI` cliquez sur `All Image Assets` dans zone de gauche bot hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="e6b1c-113">À hello à droite de la zone hello `Notifications`, modifiez `toast capable` de `(not set)` trop`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="e6b1c-114">Toutes les plateformes</span><span class="sxs-lookup"><span data-stu-id="e6b1c-114">All platforms</span></span>
<span data-ttu-id="e6b1c-115">Vous devez toosynchronize votre application tooyour Microsoft compte et toohello engagement plateforme.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="e6b1c-116">Pour cela vous avez besoin toocreate un compte ou une session [centre de développement windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="e6b1c-117">Une fois que créer une application et que vous recherchez hello SID et une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="e6b1c-118">Sur hello engagement frontal, allez sur la configuration de votre application dans `native push` et coller vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="e6b1c-119">Ensuite, cliquez avec le bouton droit sur votre projet, puis sélectionnez `store` et `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="e6b1c-120">Vous devez simplement l’application hello de tooselect vous avez créez-le avant toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="e6b1c-121">Initialiser hello SDK Reach d’Engagement</span><span class="sxs-lookup"><span data-stu-id="e6b1c-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="e6b1c-122">Modifier hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="e6b1c-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="e6b1c-123">Insérez `EngagementReach.Instance.Init` juste après `EngagementAgent.Instance.Init` dans votre méthode `InitEngagement` :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="e6b1c-124">Hello `EngagementReach.Instance.Init` s’exécute dans un thread dédié.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="e6b1c-125">Vous n’avez pas toodo il vous-même.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="e6b1c-126">Si vous utilisez des notifications push ailleurs dans votre application, vous avez trop[partager votre canal push](#push-channel-sharing) avec Engagement atteindre.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="e6b1c-127">Intégration</span><span class="sxs-lookup"><span data-stu-id="e6b1c-127">Integration</span></span>
<span data-ttu-id="e6b1c-128">Engagement fournit les bannières dans l’application de deux façons tooadd hello portée et spot pour annonces et les sondages dans votre application : hello superposition intégration et l’intégration manuelle des vues web hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="e6b1c-129">Vous ne devez pas combiner les deux approches sur hello même page.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="e6b1c-130">choix de Hello entre l’intégration de deux hello peut se résumer ainsi :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="e6b1c-131">Vous pouvez choisir hello superposition intégration si vos pages hérite déjà de hello Agent `EngagementPage`, il vous suffit de remplacement `EngagementPage` par `EngagementPageOverlay` et `xmlns:engagement="using:Microsoft.Azure.Engagement"` par `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` dans vos pages.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="e6b1c-132">Vous pouvez choisir intégration manuelle des vues web hello si vous voulez tooprecisely place hello atteindre de l’interface utilisateur dans vos pages, ou si vous ne souhaitez pas tooadd un autre pages de niveau tooyour d’héritage.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="e6b1c-133">Intégration de superposition</span><span class="sxs-lookup"><span data-stu-id="e6b1c-133">Overlay integration</span></span>
<span data-ttu-id="e6b1c-134">segment de recouvrement Hello Engagement ajoute dynamiquement des éléments d’interface utilisateur hello utilisé toodisplay couvertures campagne dans votre page.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="e6b1c-135">Si hello superposition ne convient à votre disposition vous devez envisager les vues web hello intégration manuelle à la place.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="e6b1c-136">Votre modification de fichier .xaml `EngagementPage` trop de référence`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="e6b1c-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="e6b1c-137">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="e6b1c-138">Remplacez `engagement:EngagementPage` par `engagement:EngagementPageOverlay` :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="e6b1c-139">**Avec EngagementPage :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="e6b1c-140">**Avec EngagementPageOverlay :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="e6b1c-141">Puis, dans le fichier .cs, ajoutez à votre page le mot-clé `EngagementPageOverlay` au lieu de `EngagementPage`, puis importez `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="e6b1c-142">Remplacez `EngagementPage` par `EngagementPageOverlay` :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="e6b1c-143">**Avec EngagementPage :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="e6b1c-144">**Avec EngagementPageOverlay :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="e6b1c-145">Hello superposition d’Engagement ajoute un `Grid` élément au-dessus de votre page composé de votre mise en page et de hello deux `WebView` éléments les uns pour hello bannière et hello autres un pour la vue de spot hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="e6b1c-146">Vous pouvez personnaliser les éléments de segment de recouvrement hello directement dans hello `EngagementPageOverlay.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="e6b1c-147">Intégration manuelle de vues web</span><span class="sxs-lookup"><span data-stu-id="e6b1c-147">Web views manual integration</span></span>
<span data-ttu-id="e6b1c-148">Portée recherchent vos pages pour hello deux `WebView` éléments chargés d’afficher la bannière de hello et affichage de spot hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="e6b1c-149">Hello la seule chose que vous avez toodo est tooadd ces deux `WebView` éléments quelque part dans vos pages, Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="e6b1c-150">Dans cette hello exemple `WebView` éléments est toofit étendue de leur conteneur qui automatiquement les tailles nouveau en cas de changement de taille de fenêtre rotation ou de l’écran.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="e6b1c-151">Il est important de tookeep hello dénomination `engagement_notification_content` et `engagement_announcement_content` pour hello `WebView` éléments.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="e6b1c-152">Reach les identifie par leur nom.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="e6b1c-153">Gérer les Push de données (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e6b1c-153">Handle datapush (optional)</span></span>
<span data-ttu-id="e6b1c-154">Si vous souhaitez que votre push de données application toobe tooreceive en mesure de portée, vous avez tooimplement deux événements de hello EngagementReach classe :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="e6b1c-155">Dans App.xaml.cs dans le constructeur de App() hello ajouter :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-155">In App.xaml.cs in hello App() constructor add:</span></span>

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

<span data-ttu-id="e6b1c-156">Vous pouvez voir que le rappel hello de chaque méthode retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="e6b1c-157">Engagement envoie un back-end de commentaires tooits après la distribution de push de données hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="e6b1c-158">Si le rappel de hello retourne la valeur false, hello `exit` commentaires sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="e6b1c-159">Dans le cas contraire, il s'agira du retour `action`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="e6b1c-160">Si aucun rappel n’est définie pour les événements de hello, hello `drop` commentaires seront affichera tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="e6b1c-161">Engagement n’est pas en mesure de tooreceive des évaluations de multiples pour un push de données.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="e6b1c-162">Si vous prévoyez tooset plusieurs gestionnaires d’un événement, n’oubliez pas que les commentaires hello correspondent toohello dernière celui envoyé.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="e6b1c-163">Dans ce cas, nous vous recommandons de tooalways renvoie hello même valeur tooavoid ayant des commentaires à confusion sur hello frontal.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="e6b1c-164">Personnaliser l'interface utilisateur (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e6b1c-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="e6b1c-165">Première étape</span><span class="sxs-lookup"><span data-stu-id="e6b1c-165">First step</span></span>
<span data-ttu-id="e6b1c-166">Nous permettent de portée de hello toocustomize l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="e6b1c-167">toodo, vous devez toocreate une sous-classe de hello `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="e6b1c-168">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="e6b1c-169">Ensuite, définissez le contenu de hello hello `EngagementReach.Instance.Handler` champ avec votre objet personnalisé dans votre `App.xaml.cs` classe au sein de hello `App()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="e6b1c-170">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="e6b1c-171">Par défaut, Engagement utilise sa propre implémentation de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="e6b1c-172">Vous n’avez pas toocreate votre propre, et si vous procédez ainsi, vous n’avez toooverride chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="e6b1c-173">comportement par défaut de Hello est un objet de base d’Engagement tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="e6b1c-174">Vue web</span><span class="sxs-lookup"><span data-stu-id="e6b1c-174">Web View</span></span>
<span data-ttu-id="e6b1c-175">Par défaut, portée utilisera hello incorporée des ressources de notifications de hello DLL toodisplay hello et pages.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="e6b1c-176">tooprovide complète des possibilités de personnalisation nous utilisons uniquement l’affichage web.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="e6b1c-177">Si vous souhaitez que les dispositions toocustomize, substituer directement les fichiers de ressources hello `EngagementAnnouncement.html` et `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="e6b1c-178">Tout le code a besoin d’engagement `<body></body>` toorun correctement.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="e6b1c-179">Toutefois, vous pouvez ajouter des balises en dehors de `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="e6b1c-180">Toutefois, vous pouvez décider toouse vos propres ressources.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="e6b1c-181">Vous pouvez remplacer `EngagementReachHandler` dans votre toouse d’Engagement de tootell sous-classe vos dispositions, mais acceptent mécanisme hello soins tooembedded :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="e6b1c-182">**Exemple de code :**</span><span class="sxs-lookup"><span data-stu-id="e6b1c-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="e6b1c-183">Par défaut, AnnouncementHTML est `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="e6b1c-184">Il représente le fichier html hello concevoir contenu hello d’un message envoyé (annonce de texte, Web anoucement et annonce d’interrogation).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="e6b1c-185">AnnouncementName est `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="e6b1c-186">Il est le nom hello de conception du webview hello dans votre page xaml.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="e6b1c-187">NotificationHTML est `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="e6b1c-188">Il représente le fichier html hello concevoir notification hello d’un message envoyé.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="e6b1c-189">NotificationName est `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="e6b1c-190">Il est le nom hello de conception du webview hello dans votre page xaml.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="e6b1c-191">Personnalisation</span><span class="sxs-lookup"><span data-stu-id="e6b1c-191">Customization</span></span>
<span data-ttu-id="e6b1c-192">Vous pouvez personnaliser comme bon vous semble les vues web des notifications et des annonces, du moment que vous conservez l'objet Engagement.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="e6b1c-193">Prenez soin que webview objet est décrit trois fois : hello première fois dans votre xaml, deuxième fois dans votre fichier .cs dans la méthode de « setwebview() » hello et troisième heure dans le fichier html de hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="e6b1c-194">Dans votre code xaml, vous décrivez composant webview graphique disposition en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="e6b1c-195">Dans votre fichier .cs, vous pouvez définir « setwebview() », dans laquelle vous définissez dimension hello du webview de deux hello (notification, annonce).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="e6b1c-196">Il est très efficace lors du redimensionne de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="e6b1c-197">Dans le fichier html de Engagement hello nous décrivent la création de contenu, webview hello et hello positions d’éléments entre eux.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="e6b1c-198">Lancer un message</span><span class="sxs-lookup"><span data-stu-id="e6b1c-198">Launch message</span></span>
<span data-ttu-id="e6b1c-199">Lorsqu’un utilisateur clique sur une notification système (un toast), Engagement lance l’application hello, charge le contenu hello Hello transmettre des messages et afficher la page hello pour les campagnes correspondants hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="e6b1c-200">Il existe un décalage entre le lancement de hello de hello application et hello l’affichage de page hello (selon la vitesse de hello de votre réseau).</span><span class="sxs-lookup"><span data-stu-id="e6b1c-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="e6b1c-201">utilisateur toohello tooindicate quelque chose est en cours de chargement, vous devez fournir une informations visuelles, comme une barre de progression ou un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="e6b1c-202">Engagement ne peut pas gérer cela lui-même. Toutefois, il fournit plusieurs gestionnaires à cet effet.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="e6b1c-203">ajouter de rappel hello tooimplement dans App.xaml.cs dans « App() publique {} » :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

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

<span data-ttu-id="e6b1c-204">Vous pouvez définir le rappel de hello dans votre méthode de « Public App() {} » de votre `App.xaml.cs` fichier, de préférence avant hello `EngagementReach.Instance.Init()` appeler.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="e6b1c-205">Chaque gestionnaire est appelé par le Thread d’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="e6b1c-206">Vous n’avez pas de tooworry lorsque vous utilisez un MessageBox ou quelque chose dépendant de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="e6b1c-207"><a id="push-channel-sharing"></a> Partage de canal Push</span><span class="sxs-lookup"><span data-stu-id="e6b1c-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="e6b1c-208">Si vous utilisez des notifications push pour un autre objet dans votre application vous avez la fonctionnalité de partage de hello SDK de l’Engagement de canal de push toouse hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="e6b1c-209">Il s’agit de tooavoid manqué push.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="e6b1c-210">Vous pouvez fournir votre propre push toohello Engagement atteindre l’initialisation de canal.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="e6b1c-211">Hello SDK utilise au lieu de demander un nouveau.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="e6b1c-212">Mettre à jour de l’initialisation d’Engagement atteindre hello avec votre canal push Bonjour `InitEngagement` méthode hello `App.xaml.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="e6b1c-213">Ou bien, si vous souhaitez simplement tooconsume hello push canal après l’initialisation de portée hello vous pouvez définir un rappel sur l’Engagement atteindre de canal tooget hello push qui a été créé par le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="e6b1c-214">Définir votre rappel en tout lieu **après** hello d’initialisation de portée :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="e6b1c-215">Astuce concernant les schémas personnalisés</span><span class="sxs-lookup"><span data-stu-id="e6b1c-215">Custom scheme tip</span></span>
<span data-ttu-id="e6b1c-216">Il est possible d'utiliser des schémas personnalisés.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-216">We provide custom scheme use.</span></span> <span data-ttu-id="e6b1c-217">Vous pouvez envoyer un type différent de l’URI d’engagement toobe de serveur frontal utilisé dans votre application d’engagement.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="e6b1c-218">Les schémas par défaut comme `http, ftp, ...` sont gérés par Windows. Une fenêtre vous informera si aucune application par défaut n'est installée sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="e6b1c-219">Vous pouvez également créer un schéma personnalisé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="e6b1c-220">Hello tooset de façon simple un schéma personnalisé dans votre application est tooopen votre `Package.appxmanifest` accédez dans `Declarations` Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="e6b1c-221">Sélectionnez `Protocol` Bonjour, faites défiler les déclarations disponibles boîte et l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="e6b1c-222">Modifier hello `Name` nom de champ avec votre nouveau protocole voulu.</span><span class="sxs-lookup"><span data-stu-id="e6b1c-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="e6b1c-223">Toouse maintenant ce protocole, modifiez votre `App.xaml.cs` avec hello `OnActivated` (méthode) et n’oubliez pas également engagement tooinitialize ici :</span><span class="sxs-lookup"><span data-stu-id="e6b1c-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

