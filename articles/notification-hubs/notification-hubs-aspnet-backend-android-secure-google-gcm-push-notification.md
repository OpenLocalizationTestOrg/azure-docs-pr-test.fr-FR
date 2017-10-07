---
title: "aaaSending sécuriser des Notifications Push avec Azure Notification Hubs"
description: "Découvrez comment toosend sécurisée push application Android de tooan des notifications à partir d’Azure. Exemples de code écrits en Java et C#."
documentationcenter: android
keywords: notification push,notifications push,messages push,notifications push android
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Envoi de notifications push sécurisées avec Azure Notification Hubs
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure de message push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise plateformes mobiles.

En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello. Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre un appareil Android de hello client et le serveur principal d’application hello.

À un niveau élevé, les flux hello sont comme suit :

1. Hello serveur principal d’application :
   * stocke la charge utile sécurisée dans la base de données principale ;
   * Envoie un ID hello de cet appareil Android notification toohello (aucune information sécurisée est envoyée).
2. application Hello sur périphérique hello, lors de la réception de notification de hello :
   * les appareils Android Hello contacte hello principal demande hello sécurisé charge utile.
   * application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.

Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte. Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton. Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, application d’appareil hello, lors de la réception de notifications push hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application. application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.

Ce didacticiel montre comment les notifications push toosend sécurisé. Il repose sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) (didacticiel), donc vous devez effectuer tout d’abord les étapes hello dans ce didacticiel si vous n’avez pas déjà.

> [!NOTE]
> Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification, comme décrit dans [Prise en main de Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Modifier le projet Android de hello
Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification push, vous avez toochange votre toohandle application Android notification et rappeler votre hello principal tooretrieve secure toobe message affiché.
tooachieve cet objectif, vous avez toomake sûr que votre application Android sait comment tooauthenticate lui-même avec votre serveur principal lorsqu’il reçoit des notifications push de hello.

Maintenant, nous allons modifier hello *connexion* flux de valeur d’en-tête d’authentification ordre toosave hello Bonjour partagé des préférences de votre application. Le mécanisme similaire peut être utilisé toostore n’importe quel jeton d’authentification (par exemple, les jetons OAuth) hello application aura toouse sans nécessiter des informations d’identification de l’utilisateur.

1. Dans votre projet d’application Android, ajoutez hello suivant constantes haut hello hello **MainActivity** classe :
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Toujours en hello **MainActivity** (classe), mise à jour hello `getAuthorizationHeader()` hello toocontain de méthode suivante de code :
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Ajoutez hello suivant `import` instructions haut hello hello **MainActivity** fichier :
   
        import android.content.SharedPreferences;

Nous allons maintenant modifier le Gestionnaire de hello qui est appelé lors de la notification de hello est reçue.

1. Bonjour **MyHandler** classe modifier hello `OnReceive()` toocontain de méthode :
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Ajoutez ensuite hello `retrieveNotification()` méthode, en remplaçant l’espace réservé de hello `{back-end endpoint}` avec point de terminaison principal hello obtenue lors du déploiement de votre serveur principal :
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Cette méthode appelle votre application back-end tooretrieve hello contenu de notification à l’aide des informations d’identification de hello stockées Bonjour partagé préférences et l’affiche sous forme normale de la notification. notification de Hello recherche un utilisateur d’application toohello exactement comme les autres notifications push.

Notez qu’il s’agit de cas de hello toohandle préférable de propriété d’en-tête d’authentification manquante ou du rejet par hello back-end. gestion spécifique de Hello de ces cas dépendent principalement de votre expérience d’utilisateur cible. Une option consiste à toodisplay une notification avec un message générique pour hello tooauthenticate tooretrieve hello réel notification à l’utilisateur.

## <a name="run-hello-application"></a>Exécutez hello Application
toorun hello application, procédez comme hello suivant :

1. Assurez-vous que **AppBackend** est déployé dans Azure. Si vous utilisez Visual Studio, exécutez hello **AppBackend** application d’API Web. Une page web ASP.NET s'affiche.
2. Dans Eclipse, exécutez l’application hello sur un émulateur d’appareil ou hello Android physique.
3. Dans l’interface utilisateur d’application Android hello, entrez un nom d’utilisateur et un mot de passe. Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.
4. Dans l’interface utilisateur d’application Android hello, cliquez sur **connecter**. Cliquez ensuite sur **Send push**.

