---
title: aaaBridge iOS WebView avec native SDK iOS de Mobile Engagement
description: "Décrit comment toocreate un pont entre WebView en cours d’exécution Javascript et hello natif Mobile Engagement SDK iOS"
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
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="6d9df-103">Créer un pont iOS WebView avec le Kit SDK Mobile Engagement iOS natif</span><span class="sxs-lookup"><span data-stu-id="6d9df-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d9df-104">Pont Android</span><span class="sxs-lookup"><span data-stu-id="6d9df-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="6d9df-105">Pont iOS</span><span class="sxs-lookup"><span data-stu-id="6d9df-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="6d9df-106">Certaines applications mobiles sont conçues comme une application hybride où application hello elle-même est développée à l’aide de développement iOS native Objective-C, mais certains ou tous les écrans hello même sont rendues dans un WebView iOS.</span><span class="sxs-lookup"><span data-stu-id="6d9df-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="6d9df-107">Vous pouvez utiliser toujours Mobile Engagement iOS SDK au sein de ces applications et de ce didacticiel décrit comment toogo sur cette opération.</span><span class="sxs-lookup"><span data-stu-id="6d9df-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="6d9df-108">Il existe deux approches tooachieve ce que les deux ne sont pas documentées :</span><span class="sxs-lookup"><span data-stu-id="6d9df-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="6d9df-109">La première est décrite dans cet [article](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip). Elle nécessite l’inscription d’un `UIWebViewDelegate` sur votre WebView et l’interception puis l’annulation immédiate d’une modification de l’emplacement effectuée dans Javascript.</span><span class="sxs-lookup"><span data-stu-id="6d9df-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="6d9df-110">Une deuxième repose sur ce [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), une approche plus claire que hello tout d’abord et qui nous allons suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="6d9df-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="6d9df-111">Notez que cette approche fonctionne uniquement sur iOS7 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="6d9df-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="6d9df-112">Suivez les étapes de hello ci-dessous pour hello iOS pont exemple :</span><span class="sxs-lookup"><span data-stu-id="6d9df-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="6d9df-113">Tout d’abord, vous devez tooensure que vous avez parcouru notre [didacticiel de mise en route](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK dans votre application hybride.</span><span class="sxs-lookup"><span data-stu-id="6d9df-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="6d9df-114">Si vous le souhaitez, vous pouvez également activer la journalisation de test comme suit afin que vous puissiez voir les méthodes du Kit de développement logiciel hello comme nous les déclencher de hello webview.</span><span class="sxs-lookup"><span data-stu-id="6d9df-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="6d9df-115">Vérifiez maintenant que votre application hybride a un écran avec une WebView.</span><span class="sxs-lookup"><span data-stu-id="6d9df-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="6d9df-116">Vous pouvez l’ajouter toohello `Main.storyboard` de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6d9df-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="6d9df-117">Associer ce webview avec votre **ViewController** en faisant glisser hello webview de hello vue contrôleur scène toohello `ViewController.h` modifier l’écran, en plaçant juste en dessous de hello `@interface` ligne.</span><span class="sxs-lookup"><span data-stu-id="6d9df-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="6d9df-118">Après cela, une boîte de dialogue vous invite à fournir un nom.</span><span class="sxs-lookup"><span data-stu-id="6d9df-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="6d9df-119">Fournir le nom hello en tant que **webView**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="6d9df-120">Votre `ViewController.h` fichier doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d9df-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="6d9df-121">Nous mettrons à jour hello `ViewController.m` fichier ultérieurement, mais tout d’abord, nous allons créer des fichiers de pont hello qui crée un wrapper sur certains iOS Mobile Engagement couramment utilisés méthodes du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="6d9df-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="6d9df-122">Créer un nouveau fichier d’en-tête appelé **EngagementJsExports.h** qui utilise hello `JSExport` mécanisme décrit dans hello susmentionné [session](https://developer.apple.com/videos/play/wwdc2013/615) méthodes de tooexpose hello iOS natif.</span><span class="sxs-lookup"><span data-stu-id="6d9df-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="6d9df-123">Ensuite, nous allons créer hello deuxième partie du fichier de pont hello.</span><span class="sxs-lookup"><span data-stu-id="6d9df-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="6d9df-124">Créez un fichier appelé **EngagementJsExports.m** qui contiendra la mise en œuvre hello création de wrappers réels hello en appelant des méthodes du Kit de développement logiciel hello Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="6d9df-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="6d9df-125">Notez également que nous examinons l’analyse hello `extras` transmises à partir de javascript du webview hello et à placer dans un `NSMutableDictionary` toobe de l’objet passé avec la méthode du SDK de l’Engagement de hello appels.</span><span class="sxs-lookup"><span data-stu-id="6d9df-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="6d9df-126">Maintenant nous reviendrons toohello **ViewController.m** et de mises à jour hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d9df-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="6d9df-127">Points suivants de hello Remarque à propos hello **ViewController.m** fichier :</span><span class="sxs-lookup"><span data-stu-id="6d9df-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="6d9df-128">Bonjour `loadWebView` (méthode), nous chargeons un fichier HTML local appelé **LocalPage.html** dont nous allons examiner ensuite le code.</span><span class="sxs-lookup"><span data-stu-id="6d9df-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="6d9df-129">Bonjour `webViewDidFinishLoad` (méthode), nous sommes en saisissant hello `JsContext` et en associant notre classe wrapper.</span><span class="sxs-lookup"><span data-stu-id="6d9df-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="6d9df-130">Cela permettra de méthodes de wrapper de notre kit de développement logiciel à l’aide de la poignée de hello **EngagementJs** de hello webView.</span><span class="sxs-lookup"><span data-stu-id="6d9df-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="6d9df-131">Créez un fichier appelé **LocalPage.html** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d9df-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
                       // Example of how extras info can be passed with hello Engagement logs
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
10. <span data-ttu-id="6d9df-132">Remarque hello points suivants à le sur le fichier HTML de hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="6d9df-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="6d9df-133">Il contient un ensemble de zones d’entrée dans laquelle vous pouvez fournir toobe de données utilisé comme noms pour votre événement, la tâche, l’erreur, l’AppInfo.</span><span class="sxs-lookup"><span data-stu-id="6d9df-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="6d9df-134">Lorsque vous cliquez sur tooit de hello bouton suivant, un appel est fait toohello Javascript qui appelle finalement les méthodes de hello de hello pont fichier toopass cette toohello appel SDK iOS de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6d9df-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="6d9df-135">Nous sommes le marquage sur certains événements de toohello statique informations supplémentaire, les travaux et même erreurs toodemonstrate comment cette opération peut être effectuée.</span><span class="sxs-lookup"><span data-stu-id="6d9df-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="6d9df-136">Cette information supplémentaire est envoyée en tant que chaîne de JSON qui, si vous regardez dans hello `EngagementJsExports.m` de fichiers, qui est analysée et passés en même temps que les événements, les tâches, erreurs d’envoi.</span><span class="sxs-lookup"><span data-stu-id="6d9df-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="6d9df-137">Un travail d’Engagement Mobile est lancé avec nom hello vous spécifiez dans la zone d’entrée de hello, exécutez pendant 10 secondes et arrêté.</span><span class="sxs-lookup"><span data-stu-id="6d9df-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="6d9df-138">Un appinfo d’Engagement Mobile ou une balise est passé en tant que clé statique de hello et valeur hello que vous avez entré dans l’entrée de hello en tant que valeur de hello de balise de hello avec 'customer_name'.</span><span class="sxs-lookup"><span data-stu-id="6d9df-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="6d9df-139">Application hello d’exécution et que vous découvrez hello.</span><span class="sxs-lookup"><span data-stu-id="6d9df-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="6d9df-140">Maintenant fournir un nom pour un événement de test comme hello suivant et cliquez sur **envoyer** tooit suivant.</span><span class="sxs-lookup"><span data-stu-id="6d9df-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="6d9df-141">Maintenant, si vous accédez toohello **moniteur** onglet de votre application et l’aspect sous **événements -> détails**, vous verrez cet événement s’affichent en même temps que hello statique-informations sur l’application que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="6d9df-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png