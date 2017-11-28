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
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="4de44-104">Azure Notification Hubs notifie les utilisateurs pour Android avec backend .NET</span><span class="sxs-lookup"><span data-stu-id="4de44-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="4de44-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4de44-105">Overview</span></span>
<span data-ttu-id="4de44-106">Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.</span><span class="sxs-lookup"><span data-stu-id="4de44-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="4de44-107">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="4de44-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="4de44-108">Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients et les notifications de toogenerate, comme indiqué dans la rubrique d’aide hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="4de44-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="4de44-109">Ce didacticiel s’appuie sur le concentrateur de notification hello que vous avez créé dans hello [mise en route avec Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4de44-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="4de44-110">Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification, comme décrit dans [Prise en main de Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4de44-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="4de44-111">Créer hello projet Android</span><span class="sxs-lookup"><span data-stu-id="4de44-111">Create hello Android Project</span></span>
<span data-ttu-id="4de44-112">étape suivante de Hello est l’application Android hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="4de44-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="4de44-113">Suivez hello [mise en route avec Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) toocreate didacticiel et configurer vos notifications push tooreceive application GCM.</span><span class="sxs-lookup"><span data-stu-id="4de44-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="4de44-114">Ouvrez votre **res/layout/activity_main.xml** de fichiers, remplacez hello hello suivant des définitions de contenu.</span><span class="sxs-lookup"><span data-stu-id="4de44-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="4de44-115">Cette opération ajoute de nouveaux contrôles EditText pour la connexion en tant qu'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4de44-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="4de44-116">Un champ est également ajouté pour une balise de nom d'utilisateur qui fera partie des notifications que vous enverrez :</span><span class="sxs-lookup"><span data-stu-id="4de44-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
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
3. <span data-ttu-id="4de44-117">Ouvrez votre **res/values/strings.xml** de fichier et remplacez hello `send_button` définition avec les éléments suivants de hello lignes cette chaîne de hello redefine pour hello `send_button` et ajouter d’autres contrôles des chaînes pour hello :</span><span class="sxs-lookup"><span data-stu-id="4de44-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="4de44-118">La présentation graphique de votre fichier main_activity.xml doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4de44-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="4de44-119">Créer une nouvelle classe nommée **RegisterClient** Bonjour du même package en tant que votre `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="4de44-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="4de44-120">Utilisez le code hello ci-dessous pour le nouveau fichier de classe hello.</span><span class="sxs-lookup"><span data-stu-id="4de44-120">Use hello code below for hello new class file.</span></span>
   
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
   
    <span data-ttu-id="4de44-121">Ce composant implémente hello REST appelle toocontact requis hello serveur principal d’application, dans tooregister d’ordre pour les notifications push.</span><span class="sxs-lookup"><span data-stu-id="4de44-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="4de44-122">Il stocke également localement hello *registrationIds* créé par hello Hub de Notification comme détaillé dans [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="4de44-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="4de44-123">Notez qu’il utilise un jeton d’autorisation stocké dans le stockage local lorsque vous cliquez sur hello **connecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="4de44-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="4de44-124">Dans votre `MainActivity` classe, supprimez ou commentez votre champ privé pour `NotificationHub`, et ajoutez un champ pour hello `RegisterClient` classe et une chaîne pour le point de terminaison de votre principal ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4de44-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="4de44-125">Être vraiment tooreplace `<Enter Your Backend Endpoint>` avec hello votre point de terminaison principal réel obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="4de44-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="4de44-126">Par exemple, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4de44-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="4de44-127">Dans votre `MainActivity` (classe), Bonjour `onCreate` (méthode), supprimez ou commentez l’initialisation de hello Hello `hub` champ et hello appellent toohello `registerWithNotificationHubs` (méthode).</span><span class="sxs-lookup"><span data-stu-id="4de44-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="4de44-128">Ajoutez ensuite le code tooinitialize une instance de hello `RegisterClient` classe.</span><span class="sxs-lookup"><span data-stu-id="4de44-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="4de44-129">méthode Hello doit contenir hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4de44-129">hello method should contain hello following lines:</span></span>
   
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
2. <span data-ttu-id="4de44-130">Dans votre `MainActivity` classe, supprimez ou commentez hello entière `registerWithNotificationHubs` (méthode).</span><span class="sxs-lookup"><span data-stu-id="4de44-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="4de44-131">Celle-ci n'est pas utilisée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4de44-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="4de44-132">Ajoutez hello suivant `import` instructions tooyour **MainActivity.java** fichier.</span><span class="sxs-lookup"><span data-stu-id="4de44-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="4de44-133">Ensuite, ajoutez hello suivant hello toohandle de méthodes **connecter** click du bouton événements et envoyer des notifications push.</span><span class="sxs-lookup"><span data-stu-id="4de44-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
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

    <span data-ttu-id="4de44-134">Hello `login` gestionnaire pour hello **connecter** bouton génère une authentification de base jeton à l’aide sur le nom d’utilisateur d’entrée de hello et un mot de passe (Notez que cela représente n’importe quel jeton utilise de votre schéma d’authentification), puis il utilise `RegisterClient`principal de hello toocall pour l’inscription.</span><span class="sxs-lookup"><span data-stu-id="4de44-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="4de44-135">Hello `sendPush` appels de méthode hello principal tootrigger un utilisateur de toohello notification sécurisée basé sur la balise d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="4de44-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="4de44-136">Hello notification de plateforme de service qui `sendPush` cibles dépend hello `pns` chaîne passée.</span><span class="sxs-lookup"><span data-stu-id="4de44-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="4de44-137">Dans votre `MainActivity` (classe), mise à jour hello `sendNotificationButtonOnClick` hello toocall de méthode `sendPush` méthode avec l’utilisateur hello sélectionné les services de notification de plateforme comme suit.</span><span class="sxs-lookup"><span data-stu-id="4de44-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="4de44-138">Exécutez hello Application</span><span class="sxs-lookup"><span data-stu-id="4de44-138">Run hello Application</span></span>
1. <span data-ttu-id="4de44-139">Exécutez l’application hello sur un périphérique ou un émulateur à l’aide d’Android Studio.</span><span class="sxs-lookup"><span data-stu-id="4de44-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="4de44-140">Dans l’application Android de hello, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4de44-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="4de44-141">Ils doivent tous deux être hello même valeur de chaîne et ne doit pas contenir des espaces ou des caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="4de44-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="4de44-142">Dans l’application Android de hello, cliquez sur **connecter**.</span><span class="sxs-lookup"><span data-stu-id="4de44-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="4de44-143">Attendez que s'affiche un message indiquant **Logged in and registered**.</span><span class="sxs-lookup"><span data-stu-id="4de44-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="4de44-144">Cette opération activera hello **envoyer une Notification** bouton.</span><span class="sxs-lookup"><span data-stu-id="4de44-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="4de44-145">Cliquez sur tooenable de boutons bascule hello toutes les plateformes où vous avez exécuté l’application hello et un utilisateur inscrit.</span><span class="sxs-lookup"><span data-stu-id="4de44-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="4de44-146">Entrez le nom de l’utilisateur hello qui recevra le message de notification hello.</span><span class="sxs-lookup"><span data-stu-id="4de44-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="4de44-147">Cet utilisateur doit être inscrit pour les notifications sur les appareils cibles hello.</span><span class="sxs-lookup"><span data-stu-id="4de44-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="4de44-148">Entrez un message pour hello utilisateur tooreceive comme un message de notification push.</span><span class="sxs-lookup"><span data-stu-id="4de44-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="4de44-149">Cliquez sur **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="4de44-149">Click **Send Notification**.</span></span>  <span data-ttu-id="4de44-150">Chaque périphérique qui est associé à une inscription avec la balise de nom d’utilisateur hello recevra de notifications push hello.</span><span class="sxs-lookup"><span data-stu-id="4de44-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
