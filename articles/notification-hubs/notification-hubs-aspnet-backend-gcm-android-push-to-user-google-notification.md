---
title: "aaaAzure concentrateurs de Notification d’avertir les utilisateurs pour Android avec le serveur principal .NET"
description: "Découvrez comment toosend push notifications toousers dans Azure. Exemples de code écrits en Java pour Android"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a>Azure Notification Hubs notifie les utilisateurs pour Android avec backend .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Vue d'ensemble
Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes. Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique. Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients et les notifications de toogenerate, comme indiqué dans la rubrique d’aide hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend). Ce didacticiel s’appuie sur le concentrateur de notification hello que vous avez créé dans hello [mise en route avec Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) didacticiel.

> [!NOTE]
> Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification, comme décrit dans [Prise en main de Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a>Créer hello projet Android
étape suivante de Hello est l’application Android hello de toocreate.

1. Suivez hello [mise en route avec Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) toocreate didacticiel et configurer vos notifications push tooreceive application GCM.
2. Ouvrez votre **res/layout/activity_main.xml** de fichiers, remplacez hello hello suivant des définitions de contenu.
   
    Cette opération ajoute de nouveaux contrôles EditText pour la connexion en tant qu'utilisateur. Un champ est également ajouté pour une balise de nom d'utilisateur qui fera partie des notifications que vous enverrez :
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. Ouvrez votre **res/values/strings.xml** de fichier et remplacez hello `send_button` définition avec les éléments suivants de hello lignes cette chaîne de hello redefine pour hello `send_button` et ajouter d’autres contrôles des chaînes pour hello :
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    La présentation graphique de votre fichier main_activity.xml doit ressembler à ceci :
   
    ![][A1]
4. Créer une nouvelle classe nommée **RegisterClient** Bonjour du même package en tant que votre `MainActivity` classe. Utilisez le code hello ci-dessous pour le nouveau fichier de classe hello.
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    Ce composant implémente hello REST appelle toocontact requis hello serveur principal d’application, dans tooregister d’ordre pour les notifications push. Il stocke également localement hello *registrationIds* créé par hello Hub de Notification comme détaillé dans [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend). Notez qu’il utilise un jeton d’autorisation stocké dans le stockage local lorsque vous cliquez sur hello **connecter** bouton.
5. Dans votre `MainActivity` classe, supprimez ou commentez votre champ privé pour `NotificationHub`, et ajoutez un champ pour hello `RegisterClient` classe et une chaîne pour le point de terminaison de votre principal ASP.NET. Être vraiment tooreplace `<Enter Your Backend Endpoint>` avec hello votre point de terminaison principal réel obtenu précédemment. Par exemple, `http://mybackend.azurewebsites.net`.

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. Dans votre `MainActivity` (classe), Bonjour `onCreate` (méthode), supprimez ou commentez l’initialisation de hello Hello `hub` champ et hello appellent toohello `registerWithNotificationHubs` (méthode). Ajoutez ensuite le code tooinitialize une instance de hello `RegisterClient` classe. méthode Hello doit contenir hello lignes suivantes :
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. Dans votre `MainActivity` classe, supprimez ou commentez hello entière `registerWithNotificationHubs` (méthode). Celle-ci n'est pas utilisée dans ce didacticiel.
3. Ajoutez hello suivant `import` instructions tooyour **MainActivity.java** fichier.
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. Ensuite, ajoutez hello suivant hello toohandle de méthodes **connecter** click du bouton événements et envoyer des notifications push.
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    Hello `login` gestionnaire pour hello **connecter** bouton génère une authentification de base jeton à l’aide sur le nom d’utilisateur d’entrée de hello et un mot de passe (Notez que cela représente n’importe quel jeton utilise de votre schéma d’authentification), puis il utilise `RegisterClient`principal de hello toocall pour l’inscription.

    Hello `sendPush` appels de méthode hello principal tootrigger un utilisateur de toohello notification sécurisée basé sur la balise d’utilisateur hello. Hello notification de plateforme de service qui `sendPush` cibles dépend hello `pns` chaîne passée.

1. Dans votre `MainActivity` (classe), mise à jour hello `sendNotificationButtonOnClick` hello toocall de méthode `sendPush` méthode avec l’utilisateur hello sélectionné les services de notification de plateforme comme suit.
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a>Exécutez hello Application
1. Exécutez l’application hello sur un périphérique ou un émulateur à l’aide d’Android Studio.
2. Dans l’application Android de hello, entrez un nom d’utilisateur et un mot de passe. Ils doivent tous deux être hello même valeur de chaîne et ne doit pas contenir des espaces ou des caractères spéciaux.
3. Dans l’application Android de hello, cliquez sur **connecter**. Attendez que s'affiche un message indiquant **Logged in and registered**. Cette opération activera hello **envoyer une Notification** bouton.
   
    ![][A2]
4. Cliquez sur tooenable de boutons bascule hello toutes les plateformes où vous avez exécuté l’application hello et un utilisateur inscrit.
5. Entrez le nom de l’utilisateur hello qui recevra le message de notification hello. Cet utilisateur doit être inscrit pour les notifications sur les appareils cibles hello.
6. Entrez un message pour hello utilisateur tooreceive comme un message de notification push.
7. Cliquez sur **Send Notification**.  Chaque périphérique qui est associé à une inscription avec la balise de nom d’utilisateur hello recevra de notifications push hello.

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
