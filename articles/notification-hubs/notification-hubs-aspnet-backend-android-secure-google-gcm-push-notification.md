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
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="5b833-105">Envoi de notifications push sécurisées avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5b833-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b833-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="5b833-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="5b833-107">iOS</span><span class="sxs-lookup"><span data-stu-id="5b833-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="5b833-108">Android</span><span class="sxs-lookup"><span data-stu-id="5b833-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="5b833-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5b833-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5b833-110">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5b833-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5b833-111">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5b833-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5b833-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="5b833-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="5b833-113">Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure de message push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="5b833-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="5b833-114">En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello.</span><span class="sxs-lookup"><span data-stu-id="5b833-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="5b833-115">Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre un appareil Android de hello client et le serveur principal d’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b833-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="5b833-116">À un niveau élevé, les flux hello sont comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b833-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="5b833-117">Hello serveur principal d’application :</span><span class="sxs-lookup"><span data-stu-id="5b833-117">hello app back-end:</span></span>
   * <span data-ttu-id="5b833-118">stocke la charge utile sécurisée dans la base de données principale ;</span><span class="sxs-lookup"><span data-stu-id="5b833-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="5b833-119">Envoie un ID hello de cet appareil Android notification toohello (aucune information sécurisée est envoyée).</span><span class="sxs-lookup"><span data-stu-id="5b833-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="5b833-120">application Hello sur périphérique hello, lors de la réception de notification de hello :</span><span class="sxs-lookup"><span data-stu-id="5b833-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="5b833-121">les appareils Android Hello contacte hello principal demande hello sécurisé charge utile.</span><span class="sxs-lookup"><span data-stu-id="5b833-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="5b833-122">application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="5b833-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="5b833-123">Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="5b833-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="5b833-124">Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton.</span><span class="sxs-lookup"><span data-stu-id="5b833-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="5b833-125">Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, application d’appareil hello, lors de la réception de notifications push hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application.</span><span class="sxs-lookup"><span data-stu-id="5b833-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="5b833-126">application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.</span><span class="sxs-lookup"><span data-stu-id="5b833-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="5b833-127">Ce didacticiel montre comment les notifications push toosend sécurisé.</span><span class="sxs-lookup"><span data-stu-id="5b833-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="5b833-128">Il repose sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) (didacticiel), donc vous devez effectuer tout d’abord les étapes hello dans ce didacticiel si vous n’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="5b833-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="5b833-129">Ce didacticiel part du principe que vous avez créé et configuré votre hub de notification, comme décrit dans [Prise en main de Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5b833-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="5b833-130">Modifier le projet Android de hello</span><span class="sxs-lookup"><span data-stu-id="5b833-130">Modify hello Android project</span></span>
<span data-ttu-id="5b833-131">Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification push, vous avez toochange votre toohandle application Android notification et rappeler votre hello principal tooretrieve secure toobe message affiché.</span><span class="sxs-lookup"><span data-stu-id="5b833-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="5b833-132">tooachieve cet objectif, vous avez toomake sûr que votre application Android sait comment tooauthenticate lui-même avec votre serveur principal lorsqu’il reçoit des notifications push de hello.</span><span class="sxs-lookup"><span data-stu-id="5b833-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="5b833-133">Maintenant, nous allons modifier hello *connexion* flux de valeur d’en-tête d’authentification ordre toosave hello Bonjour partagé des préférences de votre application.</span><span class="sxs-lookup"><span data-stu-id="5b833-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="5b833-134">Le mécanisme similaire peut être utilisé toostore n’importe quel jeton d’authentification (par exemple, les jetons OAuth) hello application aura toouse sans nécessiter des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b833-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="5b833-135">Dans votre projet d’application Android, ajoutez hello suivant constantes haut hello hello **MainActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="5b833-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="5b833-136">Toujours en hello **MainActivity** (classe), mise à jour hello `getAuthorizationHeader()` hello toocontain de méthode suivante de code :</span><span class="sxs-lookup"><span data-stu-id="5b833-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="5b833-137">Ajoutez hello suivant `import` instructions haut hello hello **MainActivity** fichier :</span><span class="sxs-lookup"><span data-stu-id="5b833-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="5b833-138">Nous allons maintenant modifier le Gestionnaire de hello qui est appelé lors de la notification de hello est reçue.</span><span class="sxs-lookup"><span data-stu-id="5b833-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="5b833-139">Bonjour **MyHandler** classe modifier hello `OnReceive()` toocontain de méthode :</span><span class="sxs-lookup"><span data-stu-id="5b833-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="5b833-140">Ajoutez ensuite hello `retrieveNotification()` méthode, en remplaçant l’espace réservé de hello `{back-end endpoint}` avec point de terminaison principal hello obtenue lors du déploiement de votre serveur principal :</span><span class="sxs-lookup"><span data-stu-id="5b833-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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

<span data-ttu-id="5b833-141">Cette méthode appelle votre application back-end tooretrieve hello contenu de notification à l’aide des informations d’identification de hello stockées Bonjour partagé préférences et l’affiche sous forme normale de la notification.</span><span class="sxs-lookup"><span data-stu-id="5b833-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="5b833-142">notification de Hello recherche un utilisateur d’application toohello exactement comme les autres notifications push.</span><span class="sxs-lookup"><span data-stu-id="5b833-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="5b833-143">Notez qu’il s’agit de cas de hello toohandle préférable de propriété d’en-tête d’authentification manquante ou du rejet par hello back-end.</span><span class="sxs-lookup"><span data-stu-id="5b833-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="5b833-144">gestion spécifique de Hello de ces cas dépendent principalement de votre expérience d’utilisateur cible.</span><span class="sxs-lookup"><span data-stu-id="5b833-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="5b833-145">Une option consiste à toodisplay une notification avec un message générique pour hello tooauthenticate tooretrieve hello réel notification à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b833-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="5b833-146">Exécutez hello Application</span><span class="sxs-lookup"><span data-stu-id="5b833-146">Run hello Application</span></span>
<span data-ttu-id="5b833-147">toorun hello application, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="5b833-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="5b833-148">Assurez-vous que **AppBackend** est déployé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b833-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="5b833-149">Si vous utilisez Visual Studio, exécutez hello **AppBackend** application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="5b833-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="5b833-150">Une page web ASP.NET s'affiche.</span><span class="sxs-lookup"><span data-stu-id="5b833-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="5b833-151">Dans Eclipse, exécutez l’application hello sur un émulateur d’appareil ou hello Android physique.</span><span class="sxs-lookup"><span data-stu-id="5b833-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="5b833-152">Dans l’interface utilisateur d’application Android hello, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5b833-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="5b833-153">Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.</span><span class="sxs-lookup"><span data-stu-id="5b833-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="5b833-154">Dans l’interface utilisateur d’application Android hello, cliquez sur **connecter**.</span><span class="sxs-lookup"><span data-stu-id="5b833-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="5b833-155">Cliquez ensuite sur **Send push**.</span><span class="sxs-lookup"><span data-stu-id="5b833-155">Then click **Send push**.</span></span>

