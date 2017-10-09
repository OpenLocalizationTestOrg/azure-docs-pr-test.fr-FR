---
title: "aaaNotification concentrateurs dernières actualités didacticiel - Android"
description: "Découvrez comment toouse toosend de concentrateurs de Notification Azure Service Bus avec rupture des appareils de nouvelles notifications tooAndroid."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="9ce73-103">Utilisez toosend concentrateurs de Notification dernières actualités</span><span class="sxs-lookup"><span data-stu-id="9ce73-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="9ce73-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9ce73-104">Overview</span></span>
<span data-ttu-id="9ce73-105">Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooan application Android.</span><span class="sxs-lookup"><span data-stu-id="9ce73-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="9ce73-106">Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="9ce73-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="9ce73-107">Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..</span><span class="sxs-lookup"><span data-stu-id="9ce73-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="9ce73-108">Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="9ce73-109">Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="9ce73-110">Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance.</span><span class="sxs-lookup"><span data-stu-id="9ce73-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="9ce73-111">Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="9ce73-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ce73-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ce73-112">Prerequisites</span></span>
<span data-ttu-id="9ce73-113">Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started].</span><span class="sxs-lookup"><span data-stu-id="9ce73-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="9ce73-114">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="9ce73-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="9ce73-115">Ajouter une application de toohello de sélection de catégorie</span><span class="sxs-lookup"><span data-stu-id="9ce73-115">Add category selection toohello app</span></span>
<span data-ttu-id="9ce73-116">première étape de Hello est tooadd hello éléments tooyour existant principale activité d’interface utilisateur qui permettent de hello utilisateur tooselect catégories tooregister.</span><span class="sxs-lookup"><span data-stu-id="9ce73-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="9ce73-117">catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="9ce73-118">Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="9ce73-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="9ce73-119">Ouvrez votre fichier res/layout/activity_main.xml et remplacer le contenu avec les éléments suivants de hello hello :</span><span class="sxs-lookup"><span data-stu-id="9ce73-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="9ce73-120">Ouvrez votre fichier res/values/strings.xml et ajoutez les lignes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="9ce73-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="9ce73-121">La présentation graphique de votre fichier main_activity.xml doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="9ce73-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="9ce73-122">Créer une classe **Notifications** Bonjour du même package en tant que votre **MainActivity** classe.</span><span class="sxs-lookup"><span data-stu-id="9ce73-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="9ce73-123">Cette classe utilise hello stockage local des catégories de hello toostore de news que ce périphérique a tooreceive.</span><span class="sxs-lookup"><span data-stu-id="9ce73-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="9ce73-124">Il contient également des tooregister des méthodes pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="9ce73-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="9ce73-125">Dans la classe **MainActivity**, supprimez vos champs privés pour **NotificationHub** et **GoogleCloudMessaging**, puis ajoutez un champ pour **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="9ce73-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="9ce73-126">Ensuite, dans hello **onCreate** (méthode), supprimez l’initialisation de hello Hello **hub** champ et hello **registerWithNotificationHubs** (méthode).</span><span class="sxs-lookup"><span data-stu-id="9ce73-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="9ce73-127">Ajoutez ensuite hello après les lignes qui initialise une instance de hello **Notifications** classe.</span><span class="sxs-lookup"><span data-stu-id="9ce73-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="9ce73-128">`HubName`et `HubListenConnectionString` doit déjà être définie avec hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu plus haut.</span><span class="sxs-lookup"><span data-stu-id="9ce73-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="9ce73-129">Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="9ce73-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="9ce73-130">Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="9ce73-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="9ce73-131">clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="9ce73-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="9ce73-132">Ensuite, ajoutez hello suivant importe et `subscribe` hello toohandle de méthode s’abonner bouton événements click :</span><span class="sxs-lookup"><span data-stu-id="9ce73-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="9ce73-133">Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="9ce73-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="9ce73-134">Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="9ce73-135">Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories</span><span class="sxs-lookup"><span data-stu-id="9ce73-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="9ce73-136">Inscription à des notifications</span><span class="sxs-lookup"><span data-stu-id="9ce73-136">Register for notifications</span></span>
<span data-ttu-id="9ce73-137">Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="9ce73-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce73-138">Étant donné que registrationId hello attribué par Google Cloud Messaging (GCM) peut changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification.</span><span class="sxs-lookup"><span data-stu-id="9ce73-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="9ce73-139">Cet exemple inscrit pour la notification chaque fois que cette application hello démarre.</span><span class="sxs-lookup"><span data-stu-id="9ce73-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="9ce73-140">Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.</span><span class="sxs-lookup"><span data-stu-id="9ce73-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="9ce73-141">Ajouter hello suivant du code à la fin de hello de hello **onCreate** méthode Bonjour **MainActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="9ce73-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="9ce73-142">Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et demande une inscription pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="9ce73-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="9ce73-143">Mettez à jour hello `onStart()` méthode Hello `MainActivity` classe comme suit :</span><span class="sxs-lookup"><span data-stu-id="9ce73-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="9ce73-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="9ce73-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="9ce73-145">}</span><span class="sxs-lookup"><span data-stu-id="9ce73-145">}</span></span>
   
    <span data-ttu-id="9ce73-146">Cela met à jour l’activité principale hello basée sur l’état de hello des catégories précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="9ce73-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="9ce73-147">application Hello est maintenant terminée et permettre de stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="9ce73-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="9ce73-148">Ensuite, nous allons définir un serveur principal qui peut envoyer catégorie notifications toothis application.</span><span class="sxs-lookup"><span data-stu-id="9ce73-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="9ce73-149">Envoi des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="9ce73-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="9ce73-150">Exécutez l’application hello et générer des notifications</span><span class="sxs-lookup"><span data-stu-id="9ce73-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="9ce73-151">Dans Android Studio, générez l’application hello et démarrez-le sur un périphérique ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="9ce73-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="9ce73-152">Notez que cette application hello de que l’interface utilisateur fournit un ensemble bascule qui permet de choisir toosubscribe de catégories hello pour.</span><span class="sxs-lookup"><span data-stu-id="9ce73-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="9ce73-153">Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.</span><span class="sxs-lookup"><span data-stu-id="9ce73-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="9ce73-154">application Hello convertit les catégories de hello sélectionné en balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="9ce73-155">Hello catégories inscrits sont retournés et affichés dans une notification toast.</span><span class="sxs-lookup"><span data-stu-id="9ce73-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="9ce73-156">Envoyer une notification en exécutant l’application de Console de .NET hello.</span><span class="sxs-lookup"><span data-stu-id="9ce73-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="9ce73-157">Vous pouvez également envoyer les notifications de modèle avec balises à l’aide d’onglet de débogage de hello de votre concentrateur de notification Bonjour [portail classique Azure].</span><span class="sxs-lookup"><span data-stu-id="9ce73-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="9ce73-158">Les notifications pour les catégories de hello sélectionné s’affichent sous forme de notifications de toast.</span><span class="sxs-lookup"><span data-stu-id="9ce73-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ce73-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ce73-159">Next steps</span></span>
<span data-ttu-id="9ce73-160">Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie.</span><span class="sxs-lookup"><span data-stu-id="9ce73-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="9ce73-161">Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="9ce73-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="9ce73-162">[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]</span><span class="sxs-lookup"><span data-stu-id="9ce73-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="9ce73-163">Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.</span><span class="sxs-lookup"><span data-stu-id="9ce73-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[portail classique Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
