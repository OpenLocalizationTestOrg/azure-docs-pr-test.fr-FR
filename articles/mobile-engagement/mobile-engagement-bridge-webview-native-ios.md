---
title: "Créer un pont iOS WebView avec le Kit SDK Mobile Engagement iOS natif"
description: "Décrit comment créer un pont entre WebView exécutant Javascript et le kit SDK Mobile Engagement iOS natif"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="899b0-103">Créer un pont iOS WebView avec le Kit SDK Mobile Engagement iOS natif</span><span class="sxs-lookup"><span data-stu-id="899b0-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="899b0-104">Pont Android</span><span class="sxs-lookup"><span data-stu-id="899b0-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="899b0-105">Pont iOS</span><span class="sxs-lookup"><span data-stu-id="899b0-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="899b0-106">Certaines applications mobiles sont conçues comme applications hybrides : le développement de l’application proprement dite s’effectue de manière native dans iOS Objective-C, mais certains ou même tous les écrans sont rendus dans une WebView iOS.</span><span class="sxs-lookup"><span data-stu-id="899b0-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="899b0-107">Vous pouvez toujours utiliser le Kit SDK Mobile Engagement iOS dans ces applications. Ce didacticiel explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="899b0-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="899b0-108">Il existe deux approches, mais aucune n’est documentée :</span><span class="sxs-lookup"><span data-stu-id="899b0-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="899b0-109">La première est décrite dans cet [article](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip). Elle nécessite l’inscription d’un `UIWebViewDelegate` sur votre WebView et l’interception puis l’annulation immédiate d’une modification de l’emplacement effectuée dans Javascript.</span><span class="sxs-lookup"><span data-stu-id="899b0-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="899b0-110">La deuxième approche est basée sur cette [session WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615). Elle est plus claire que la première, c’est pourquoi nous allons la suivre dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="899b0-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="899b0-111">Notez que cette approche fonctionne uniquement sur iOS7 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="899b0-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="899b0-112">Suivez les étapes ci-dessous pour l’exemple de pont iOS :</span><span class="sxs-lookup"><span data-stu-id="899b0-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="899b0-113">Tout d’abord, vous devez vérifier que vous avez bien effectué notre [didacticiel de prise en main](mobile-engagement-ios-get-started.md) pour intégrer le Kit SDK Mobile Engagement iOS à votre application hybride.</span><span class="sxs-lookup"><span data-stu-id="899b0-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="899b0-114">Si vous le souhaitez, vous pouvez activer la journalisation de test comme suit, pour voir les méthodes du Kit SDK à mesure que nous les déclenchons à partir de la WebView.</span><span class="sxs-lookup"><span data-stu-id="899b0-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="899b0-115">Vérifiez maintenant que votre application hybride a un écran avec une WebView.</span><span class="sxs-lookup"><span data-stu-id="899b0-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="899b0-116">Vous pouvez l’ajouter au `Main.storyboard` de l’application.</span><span class="sxs-lookup"><span data-stu-id="899b0-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="899b0-117">Associez cette WebView à votre **ViewController** en faisant glisser la WebView de la scène de contrôleur d’affichage vers l’écran de modification `ViewController.h`, et en la plaçant juste en dessous de la ligne `@interface`.</span><span class="sxs-lookup"><span data-stu-id="899b0-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="899b0-118">Après cela, une boîte de dialogue vous invite à fournir un nom.</span><span class="sxs-lookup"><span data-stu-id="899b0-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="899b0-119">Tapez **webView**.</span><span class="sxs-lookup"><span data-stu-id="899b0-119">Provide the name as **webView**.</span></span> <span data-ttu-id="899b0-120">Le fichier `ViewController.h` doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="899b0-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="899b0-121">Nous mettrons à jour le fichier `ViewController.m` ultérieurement. Tout d’abord, nous allons créer le fichier de pont qui crée un wrapper sur certaines méthodes du Kit SDK Mobile Engagement iOS couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="899b0-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="899b0-122">Créez un fichier d’en-tête nommé **EngagementJsExports.h** qui utilise le mécanisme `JSExport` décrit dans la [session](https://developer.apple.com/videos/play/wwdc2013/615) mentionnée précédemment pour exposer les méthodes iOS natives.</span><span class="sxs-lookup"><span data-stu-id="899b0-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. <span data-ttu-id="899b0-123">Nous allons ensuite créer la deuxième partie du fichier de pont.</span><span class="sxs-lookup"><span data-stu-id="899b0-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="899b0-124">Créez un fichier nommé **EngagementJsExports.m** qui contiendra l’implémentation créant les wrappers réels en appelant les méthodes du Kit SDK Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="899b0-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="899b0-125">Notez également que nous analysons le `extras` qui est passé à partir du code Javascript de la WebView et que nous le mettons dans un objet `NSMutableDictionary` à passer avec les appels de méthode du Kit SDK Engagement.</span><span class="sxs-lookup"><span data-stu-id="899b0-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. <span data-ttu-id="899b0-126">Maintenant, nous revenons à **ViewController.m** et nous le mettons à jour avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="899b0-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. <span data-ttu-id="899b0-127">Notez les points suivants concernant le fichier **ViewController.m** :</span><span class="sxs-lookup"><span data-stu-id="899b0-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="899b0-128">Dans la méthode `loadWebView` , nous chargeons un fichier HTML local nommé **LocalPage.html** , dont nous allons maintenant examiner le code.</span><span class="sxs-lookup"><span data-stu-id="899b0-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="899b0-129">Dans la méthode `webViewDidFinishLoad`, nous prenons le `JsContext` et nous l’associons à notre classe wrapper.</span><span class="sxs-lookup"><span data-stu-id="899b0-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="899b0-130">Cela va nous permettre d’appeler nos méthodes du Kit SDK de wrapper **EngagementJs** à partir de la WebView.</span><span class="sxs-lookup"><span data-stu-id="899b0-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="899b0-131">Créez un fichier nommé **LocalPage.html** avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="899b0-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with the Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. <span data-ttu-id="899b0-132">Notez les points suivants concernant le fichier HTML ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="899b0-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="899b0-133">Il contient un ensemble de zones d’entrée où vous pouvez fournir des données à utiliser comme noms pour votre event, job, error et appInfo.</span><span class="sxs-lookup"><span data-stu-id="899b0-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="899b0-134">Quand vous cliquez sur le bouton en regard, le code Javascript est appelé, et celui-ci appelle les méthodes à partir du fichier de pont pour passer cet appel au kit SDK Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="899b0-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="899b0-135">Nous associons certaines informations statiques supplémentaire aux événements, aux tâches et même aux erreurs pour illustrer comment cela est réalisable.</span><span class="sxs-lookup"><span data-stu-id="899b0-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="899b0-136">Ces informations supplémentaires sont envoyées sous forme de chaîne JSON qui, si vous regardez dans le fichier `EngagementJsExports.m` , est analysée et transmise lors de l’envoi des événements, tâches et erreurs.</span><span class="sxs-lookup"><span data-stu-id="899b0-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="899b0-137">Une tâche Mobile Engagement est démarrée avec le nom que vous spécifiez dans la zone d’entrée, elle s’exécute pendant 10 secondes, puis elle s’arrête.</span><span class="sxs-lookup"><span data-stu-id="899b0-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="899b0-138">Une balise ou une appinfo Mobile Engagement est passée avec « customer_name » comme clé statique et la valeur que vous avez entrée comme valeur de balise.</span><span class="sxs-lookup"><span data-stu-id="899b0-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="899b0-139">Exécutez l’application. Vous verrez ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="899b0-139">Run the app and you will see the following.</span></span> <span data-ttu-id="899b0-140">Maintenant, fournissez un nom pour un événement de test comme celui qui suit et cliquez sur **Send** à côté.</span><span class="sxs-lookup"><span data-stu-id="899b0-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="899b0-141">Maintenant, si vous accédez à l’onglet **Surveiller** de votre application et que vous regardez sous **Événements -> Détails**, vous voyez cet événement et les informations d’application statiques que nous envoyons.</span><span class="sxs-lookup"><span data-stu-id="899b0-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
