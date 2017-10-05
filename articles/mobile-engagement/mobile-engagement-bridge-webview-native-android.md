---
title: "Créer un pont Android WebView avec le Kit SDK Mobile Engagement Android natif"
description: "Décrit comment créer un pont entre WebView exécutant Javascript et le Kit SDK Mobile Engagement Android natif"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="372be-103">Créer un pont Android WebView avec le Kit SDK Mobile Engagement Android natif</span><span class="sxs-lookup"><span data-stu-id="372be-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="372be-104">Pont Android</span><span class="sxs-lookup"><span data-stu-id="372be-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="372be-105">Pont iOS</span><span class="sxs-lookup"><span data-stu-id="372be-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="372be-106">Certaines applications mobiles sont conçues comme applications hybrides : le développement de l’application proprement dite s’effectue de manière native dans Android, mais certains ou même tous les écrans sont rendus dans une WebView Android.</span><span class="sxs-lookup"><span data-stu-id="372be-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="372be-107">Vous pouvez quand même utiliser le Kit SDK Mobile Engagement Android dans ces applications. Ce didacticiel explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="372be-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="372be-108">L’exemple de code ci-dessous est basé sur la documentation Android accessible [ici](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="372be-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="372be-109">Il décrit comment utiliser cette approche documentée pour obtenir une implémentation semblable pour des méthodes couramment utilisées du Kit SDK Mobile Engagement Android, pour qu’une WebView d’une application hybride puisse également lancer des demandes pour le suivi des événements, des tâches, des erreurs et des informations sur l’application tout en les transférant par le biais de notre Kit SDK Android.</span><span class="sxs-lookup"><span data-stu-id="372be-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="372be-110">Tout d’abord, vous devez vérifier que vous avez bien effectué notre [didacticiel de prise en main](mobile-engagement-android-get-started.md) pour intégrer le Kit SDK Mobile Engagement Android à votre application hybride.</span><span class="sxs-lookup"><span data-stu-id="372be-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="372be-111">Votre méthode `OnCreate` ressemble alors à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="372be-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="372be-112">Vérifiez maintenant que votre application hybride a un écran avec une WebView.</span><span class="sxs-lookup"><span data-stu-id="372be-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="372be-113">Son code est semblable au suivant, dans lequel nous chargeons un fichier HTML local **Sample.html** dans la WebView de la méthode `onCreate` de l’écran.</span><span class="sxs-lookup"><span data-stu-id="372be-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="372be-114">Maintenant, créez un fichier de pont nommé **WebAppInterface** qui crée un wrapper sur certaines méthodes du Kit SDK Mobile Engagement Android couramment utilisées à l’aide de l’approche `@JavascriptInterface` décrite dans la [documentation Android](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript) :</span><span class="sxs-lookup"><span data-stu-id="372be-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="372be-115">Une fois que nous avons créé le fichier de pont ci-dessus, nous devons vérifier qu’il est associé à notre WebView.</span><span class="sxs-lookup"><span data-stu-id="372be-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="372be-116">Pour cela, nous devons modifier la méthode `SetWebview` pour qu’elle ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="372be-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="372be-117">Dans l’extrait de code ci-dessus, nous avons appelé `addJavascriptInterface` pour associer notre classe de pont à notre WebView, et nous avons aussi créé un handle nommé **EngagementJs** pour appeler les méthodes à partir du fichier de pont.</span><span class="sxs-lookup"><span data-stu-id="372be-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="372be-118">Maintenant, créez le fichier suivant nommé **Sample.html** dans votre projet dans un dossier nommé **assets** qui est chargé dans la WebView et où nous appellerons les méthodes à partir du fichier de pont.</span><span class="sxs-lookup"><span data-stu-id="372be-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with the Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="372be-119">Notez les points suivants concernant le fichier HTML ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="372be-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="372be-120">Il contient un ensemble de zones d’entrée où vous pouvez fournir des données à utiliser comme noms pour votre event, job, error et appInfo.</span><span class="sxs-lookup"><span data-stu-id="372be-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="372be-121">Quand vous cliquez sur le bouton à côté, le code Javascript est appelé, et celui-ci appelle les méthodes à partir du fichier de pont pour passer cet appel au Kit SDK Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="372be-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="372be-122">Nous associons certaines informations statiques supplémentaire aux événements, aux tâches et même aux erreurs pour illustrer comment cela est réalisable.</span><span class="sxs-lookup"><span data-stu-id="372be-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="372be-123">Ces informations supplémentaires sont envoyées sous forme de chaîne JSON qui, si vous regardez dans le fichier `WebAppInterface`, est analysée et placée dans un `Bundle` Android et transmise lors de l’envoi des événements, tâches et erreurs.</span><span class="sxs-lookup"><span data-stu-id="372be-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="372be-124">Une tâche Mobile Engagement est démarrée avec le nom que vous spécifiez dans la zone d’entrée, elle s’exécute pendant 10 secondes, puis elle s’arrête.</span><span class="sxs-lookup"><span data-stu-id="372be-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="372be-125">Une balise ou une appinfo Mobile Engagement est passée avec « customer_name » comme clé statique et la valeur que vous avez entrée comme valeur de balise.</span><span class="sxs-lookup"><span data-stu-id="372be-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="372be-126">Exécutez l’application. Vous verrez ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="372be-126">Run the app and you will see the following.</span></span> <span data-ttu-id="372be-127">Maintenant, fournissez un nom pour un événement de test comme celui qui suit et cliquez sur **Send** en dessous.</span><span class="sxs-lookup"><span data-stu-id="372be-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="372be-128">Maintenant, si vous accédez à l’onglet **Surveiller** de votre application et que vous regardez sous **Événements -> Détails**, vous voyez cet événement et les informations d’application statiques que nous envoyons.</span><span class="sxs-lookup"><span data-stu-id="372be-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
