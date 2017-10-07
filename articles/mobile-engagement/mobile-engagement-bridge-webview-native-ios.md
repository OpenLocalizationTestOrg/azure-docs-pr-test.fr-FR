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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Créer un pont iOS WebView avec le Kit SDK Mobile Engagement iOS natif
> [!div class="op_single_selector"]
> * [Pont Android](mobile-engagement-bridge-webview-native-android.md)
> * [Pont iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Certaines applications mobiles sont conçues comme une application hybride où application hello elle-même est développée à l’aide de développement iOS native Objective-C, mais certains ou tous les écrans hello même sont rendues dans un WebView iOS. Vous pouvez utiliser toujours Mobile Engagement iOS SDK au sein de ces applications et de ce didacticiel décrit comment toogo sur cette opération. 

Il existe deux approches tooachieve ce que les deux ne sont pas documentées :

* La première est décrite dans cet [article](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip). Elle nécessite l’inscription d’un `UIWebViewDelegate` sur votre WebView et l’interception puis l’annulation immédiate d’une modification de l’emplacement effectuée dans Javascript. 
* Une deuxième repose sur ce [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), une approche plus claire que hello tout d’abord et qui nous allons suivre ce guide. Notez que cette approche fonctionne uniquement sur iOS7 et versions ultérieures. 

Suivez les étapes de hello ci-dessous pour hello iOS pont exemple :

1. Tout d’abord, vous devez tooensure que vous avez parcouru notre [didacticiel de mise en route](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK dans votre application hybride. Si vous le souhaitez, vous pouvez également activer la journalisation de test comme suit afin que vous puissiez voir les méthodes du Kit de développement logiciel hello comme nous les déclencher de hello webview. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Vérifiez maintenant que votre application hybride a un écran avec une WebView. Vous pouvez l’ajouter toohello `Main.storyboard` de l’application hello. 
3. Associer ce webview avec votre **ViewController** en faisant glisser hello webview de hello vue contrôleur scène toohello `ViewController.h` modifier l’écran, en plaçant juste en dessous de hello `@interface` ligne. 
4. Après cela, une boîte de dialogue vous invite à fournir un nom. Fournir le nom hello en tant que **webView**. Votre `ViewController.h` fichier doit ressembler à hello suivantes :
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Nous mettrons à jour hello `ViewController.m` fichier ultérieurement, mais tout d’abord, nous allons créer des fichiers de pont hello qui crée un wrapper sur certains iOS Mobile Engagement couramment utilisés méthodes du Kit de développement logiciel. Créer un nouveau fichier d’en-tête appelé **EngagementJsExports.h** qui utilise hello `JSExport` mécanisme décrit dans hello susmentionné [session](https://developer.apple.com/videos/play/wwdc2013/615) méthodes de tooexpose hello iOS natif. 
   
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
6. Ensuite, nous allons créer hello deuxième partie du fichier de pont hello. Créez un fichier appelé **EngagementJsExports.m** qui contiendra la mise en œuvre hello création de wrappers réels hello en appelant des méthodes du Kit de développement logiciel hello Mobile Engagement iOS. Notez également que nous examinons l’analyse hello `extras` transmises à partir de javascript du webview hello et à placer dans un `NSMutableDictionary` toobe de l’objet passé avec la méthode du SDK de l’Engagement de hello appels.  
   
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
7. Maintenant nous reviendrons toohello **ViewController.m** et de mises à jour hello suivant de code : 
   
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
8. Points suivants de hello Remarque à propos hello **ViewController.m** fichier :
   
   * Bonjour `loadWebView` (méthode), nous chargeons un fichier HTML local appelé **LocalPage.html** dont nous allons examiner ensuite le code. 
   * Bonjour `webViewDidFinishLoad` (méthode), nous sommes en saisissant hello `JsContext` et en associant notre classe wrapper. Cela permettra de méthodes de wrapper de notre kit de développement logiciel à l’aide de la poignée de hello **EngagementJs** de hello webView. 
9. Créez un fichier appelé **LocalPage.html** avec hello suivant de code :
   
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
10. Remarque hello points suivants à le sur le fichier HTML de hello ci-dessus :
    
    * Il contient un ensemble de zones d’entrée dans laquelle vous pouvez fournir toobe de données utilisé comme noms pour votre événement, la tâche, l’erreur, l’AppInfo. Lorsque vous cliquez sur tooit de hello bouton suivant, un appel est fait toohello Javascript qui appelle finalement les méthodes de hello de hello pont fichier toopass cette toohello appel SDK iOS de Mobile Engagement. 
    * Nous sommes le marquage sur certains événements de toohello statique informations supplémentaire, les travaux et même erreurs toodemonstrate comment cette opération peut être effectuée. Cette information supplémentaire est envoyée en tant que chaîne de JSON qui, si vous regardez dans hello `EngagementJsExports.m` de fichiers, qui est analysée et passés en même temps que les événements, les tâches, erreurs d’envoi. 
    * Un travail d’Engagement Mobile est lancé avec nom hello vous spécifiez dans la zone d’entrée de hello, exécutez pendant 10 secondes et arrêté. 
    * Un appinfo d’Engagement Mobile ou une balise est passé en tant que clé statique de hello et valeur hello que vous avez entré dans l’entrée de hello en tant que valeur de hello de balise de hello avec 'customer_name'. 
11. Application hello d’exécution et que vous découvrez hello. Maintenant fournir un nom pour un événement de test comme hello suivant et cliquez sur **envoyer** tooit suivant. 
    
     ![][1]
12. Maintenant, si vous accédez toohello **moniteur** onglet de votre application et l’aspect sous **événements -> détails**, vous verrez cet événement s’affichent en même temps que hello statique-informations sur l’application que vous envoyez. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
