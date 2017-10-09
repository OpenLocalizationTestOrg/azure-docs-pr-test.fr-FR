---
title: aaaBridge WebView Android native Mobile Engagement Android SDK
description: "Décrit comment toocreate un pont entre WebView Javascript en cours d’exécution et hello natif Mobile Engagement du SDK Android"
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
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Créer un pont Android WebView avec le Kit SDK Mobile Engagement Android natif
> [!div class="op_single_selector"]
> * [Pont Android](mobile-engagement-bridge-webview-native-android.md)
> * [Pont iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Certaines applications mobiles sont conçues comme une application hybride où application hello elle-même est développée à l’aide de développement Android natif, mais certains ou tous les écrans hello même sont rendues dans un WebView Android. Vous pouvez toujours utiliser Mobile Engagement SDK Android au sein de ces applications et de ce didacticiel décrit comment toogo sur cette opération. Hello exemple de code suivant est basé sur hello documentation Android [ici](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Il décrit comment utiliser cette approche documentée tooimplement même hello pour Mobile Engagement Android SDK méthodes fréquemment utilisées telles qu’un affichage Web à partir d’une application hybride peut également initier des demandes tootrack événements, les travaux, les erreurs, app-info tout en dirigeant les via notre kit de développement logiciel Android. 

1. Tout d’abord, vous devez tooensure que vous avez parcouru notre [didacticiel de mise en route](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK dans votre application hybride. Cela fait, votre `OnCreate` méthode ressemblera à hello suivant.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Vérifiez maintenant que votre application hybride a un écran avec une WebView. Hello code pour qu’il sera similaire toohello suivant où nous chargeons un fichier HTML local **Sample.html** Bonjour Webview Bonjour `onCreate` méthode de votre écran. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Créer un fichier de pont appelé **WebAppInterface** qui crée un wrapper sur certains couramment utilisé des méthodes de Mobile Engagement Android SDK à l’aide de hello `@JavascriptInterface` approche décrite dans hello [documentation Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
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
4. Une fois que nous avons créé hello au-dessus de fichier du pont, nous devons tooensure qu’il est associé à notre Webview. Pour que cette toohappen, vous devez tooedit votre `SetWebview` méthode afin qu’elle ressemble à hello suivantes :
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. Bonjour ci-dessus extrait de code, nous vous avons appelé `addJavascriptInterface` tooassociate notre pont classe avec notre Webview et également créé un handle appelé **EngagementJs** toocall les méthodes de hello à partir du fichier de pont hello. 
6. Créer maintenant les hello appelé le fichier suivant **Sample.html** dans votre projet dans un dossier appelé **actifs** qui est chargé dans hello Webview et où nous appelle les méthodes hello à partir du fichier de pont hello.
   
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
                            // Example of how extras info can be passed with hello Engagement logs
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
7. Remarque hello points suivants à le sur le fichier HTML de hello ci-dessus :
   
   * Il contient un ensemble de zones d’entrée dans laquelle vous pouvez fournir toobe de données utilisé comme noms pour votre événement, la tâche, l’erreur, l’AppInfo. Lorsque vous cliquez sur tooit de hello bouton suivant, un appel est fait toohello Javascript qui appelle finalement les méthodes de hello de hello pont fichier toopass cette toohello appel Mobile Engagement Android SDK. 
   * Nous sommes le marquage sur certains événements de toohello statique informations supplémentaire, les travaux et même erreurs toodemonstrate comment cette opération peut être effectuée. Cette information supplémentaire est envoyée en tant que chaîne de JSON qui, si vous regardez dans hello `WebAppInterface` de fichiers, qui est analysée et placer dans un Android `Bundle` et est transmis en même temps que les événements, les tâches, erreurs d’envoi. 
   * Un travail d’Engagement Mobile est lancé avec nom hello vous spécifiez dans la zone d’entrée de hello, exécutez pendant 10 secondes et arrêté. 
   * Un appinfo d’Engagement Mobile ou une balise est passé en tant que clé statique de hello et valeur hello que vous avez entré dans l’entrée de hello en tant que valeur de hello de balise de hello avec 'customer_name'. 
8. Application hello d’exécution et que vous découvrez hello. Maintenant fournir un nom pour un événement de test comme hello suivant et cliquez sur **envoyer** en dessous. 
   
    ![][1]
9. Maintenant, si vous accédez toohello **moniteur** onglet de votre application et l’aspect sous **événements -> détails**, vous verrez cet événement s’affichent en même temps que hello statique-informations sur l’application que vous envoyez. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
