---
title: "Didacticiel Utilisation de Notification Hubs pour diffuser les dernières nouvelles - Android"
description: "Découvrez comment utiliser Azure Service Bus Notification Hubs pour envoyer des notifications de dernières nouvelles aux appareils Android."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="8664e-103">Utilisation de Notification Hubs pour diffuser les dernières nouvelles</span><span class="sxs-lookup"><span data-stu-id="8664e-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="8664e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8664e-104">Overview</span></span>
<span data-ttu-id="8664e-105">Cette rubrique vous présente l’utilisation d’Azure Notification Hubs pour diffuser des notifications relatives aux dernières nouvelles vers une application Android.</span><span class="sxs-lookup"><span data-stu-id="8664e-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="8664e-106">Lorsque vous aurez terminé, vous pourrez vous inscrire aux catégories de dernières nouvelles qui vous intéressent et recevoir uniquement des notifications Push pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="8664e-107">Ce scénario est un modèle courant pour de nombreuses applications pour lesquelles des notifications doivent être envoyées à des groupes d'utilisateurs qui ont signalé antérieurement un intérêt, par exemple, lecteur RSS, applications pour fans de musique, etc.</span><span class="sxs-lookup"><span data-stu-id="8664e-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="8664e-108">Les scénarios de diffusion sont activés en incluant une ou plusieurs *balises* durant la création d’une inscription dans le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="8664e-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="8664e-109">Lorsque des notifications sont envoyées à une balise, tous les appareils pour lesquels cette balise est inscrite reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="8664e-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="8664e-110">Les balises étant de simples chaînes, il n’est pas nécessaire de les mettre en service à l’avance.</span><span class="sxs-lookup"><span data-stu-id="8664e-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="8664e-111">Pour plus d’informations sur les balises, consultez [Routage et expressions de balise Notification Hubs](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="8664e-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8664e-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8664e-112">Prerequisites</span></span>
<span data-ttu-id="8664e-113">Cette rubrique s'appuie sur l'application que vous avez créée dans [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="8664e-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="8664e-114">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="8664e-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="8664e-115">Ajout d’une sélection de catégories à l’application</span><span class="sxs-lookup"><span data-stu-id="8664e-115">Add category selection to the app</span></span>
<span data-ttu-id="8664e-116">La première étape consiste à ajouter des éléments de l’interface utilisateur à l’activité principale existante qui permettent à l’utilisateur de sélectionner des catégories auxquelles s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="8664e-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="8664e-117">Les catégories sélectionnées par un utilisateur sont stockées sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="8664e-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="8664e-118">Lorsque l'application démarre, une inscription d'appareil est créée dans votre Notification Hub avec les catégories sélectionnées sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="8664e-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="8664e-119">Ouvrez votre fichier res/layout/activity_main.xml et remplacez le contenu par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8664e-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="8664e-120">Ouvrez votre fichier res\values\string.xml et ajoutez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8664e-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="8664e-121">La présentation graphique de votre fichier main_activity.xml doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="8664e-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="8664e-122">Créez maintenant une classe **Notifications** dans le même package que votre classe **MainActivity**.</span><span class="sxs-lookup"><span data-stu-id="8664e-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="8664e-123">Cette classe utilise le stockage local pour stocker les catégories de nouvelles que cet appareil doit recevoir.</span><span class="sxs-lookup"><span data-stu-id="8664e-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="8664e-124">Elle comporte également des méthodes pour s’inscrire à ces catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="8664e-125">Dans la classe **MainActivity**, supprimez vos champs privés pour **NotificationHub** et **GoogleCloudMessaging**, puis ajoutez un champ pour **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="8664e-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="8664e-126">Ensuite, dans la méthode **onCreate**, supprimez l’initialisation du champ **hub** et de la méthode **registerWithNotificationHubs**.</span><span class="sxs-lookup"><span data-stu-id="8664e-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="8664e-127">Ajoutez ensuite les lignes suivantes, qui initialisent une instance de la classe **Notifications** .</span><span class="sxs-lookup"><span data-stu-id="8664e-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="8664e-128">`HubName` et `HubListenConnectionString` doivent être configurés avec les espaces réservés `<hub name>` et `<connection string with listen access>`, avec le nom du hub de notification et la chaîne de connexion pour *DefaultListenSharedAccessSignature* obtenue précédemment.</span><span class="sxs-lookup"><span data-stu-id="8664e-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="8664e-129">Les informations d’identification distribuées avec une application cliente n’étant généralement pas sécurisées, vous ne devez distribuer que la clé d’accès d’écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="8664e-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="8664e-130">L'accès d'écoute permet à votre application de s'inscrire à des notifications, mais les inscriptions existantes ne peuvent pas être modifiées et les notifications ne peuvent pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="8664e-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="8664e-131">La clé d'accès complet est utilisée dans un service de serveur principal sécurisé pour l'envoi de notifications et la modification d'inscriptions existantes.</span><span class="sxs-lookup"><span data-stu-id="8664e-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="8664e-132">Ensuite, ajoutez les importations ci-après et la méthode `subscribe` pour gérer l’événement de clic sur le bouton d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="8664e-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="8664e-133">Cette méthode crée une liste de catégories et utilise la classe **Notifications** pour stocker la liste dans le stockage local et inscrire les balises correspondantes auprès du Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="8664e-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="8664e-134">Lorsque des catégories sont modifiées, l'inscription est à nouveau créée avec les nouvelles catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="8664e-135">Votre application peut désormais stocker un ensemble de catégories dans le stockage local sur l’appareil et s’inscrire auprès du hub de notification lorsque l’utilisateur modifie la sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="8664e-136">Inscription à des notifications</span><span class="sxs-lookup"><span data-stu-id="8664e-136">Register for notifications</span></span>
<span data-ttu-id="8664e-137">Les étapes suivantes permettent l’inscription auprès du hub de notification au démarrage en utilisant les catégories qui ont été stockées dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="8664e-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="8664e-138">Comme la valeur de registrationId affectée par Google Cloud Messaging (GCM) peut changer à n’importe quel moment, vous devez vous inscrire fréquemment aux notifications afin d’éviter les défaillances.</span><span class="sxs-lookup"><span data-stu-id="8664e-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="8664e-139">Cet exemple s'inscrit aux notifications chaque fois que l'application démarre.</span><span class="sxs-lookup"><span data-stu-id="8664e-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="8664e-140">Pour les applications exécutées fréquemment, plus d'une fois par jour, vous pouvez probablement ignorer l'inscription afin de préserver la bande passante si moins d'un jour s'est écoulé depuis l'inscription précédente.</span><span class="sxs-lookup"><span data-stu-id="8664e-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="8664e-141">Ajoutez le code suivant à la fin de la méthode **onCreate**, dans la classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="8664e-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="8664e-142">Cette opération garantit que chaque fois que l'application démarre, elle récupère les catégories du stockage local et demande une inscription pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="8664e-143">Puis mettez à jour la méthode `onStart()` de la classe `MainActivity`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="8664e-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="8664e-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="8664e-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="8664e-145">}</span><span class="sxs-lookup"><span data-stu-id="8664e-145">}</span></span>
   
    <span data-ttu-id="8664e-146">Cette opération met l'activité principale à jour en fonction du statut des catégories enregistrées précédemment.</span><span class="sxs-lookup"><span data-stu-id="8664e-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="8664e-147">L'application est désormais terminée et peut stocker un ensemble de catégories dans le stockage local de l'appareil utilisé pour s'inscrire auprès du Notification Hub lorsque l'utilisateur modifie la sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="8664e-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="8664e-148">Ensuite, nous allons définir un serveur principal qui peut envoyer des notifications de catégorie à cette application.</span><span class="sxs-lookup"><span data-stu-id="8664e-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="8664e-149">Envoi des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="8664e-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="8664e-150">Exécution de l’application et génération de notifications</span><span class="sxs-lookup"><span data-stu-id="8664e-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="8664e-151">Dans Android Studio, générez l’application et lancez-la sur un appareil ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="8664e-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="8664e-152">Notez que l’interface utilisateur de l’application fournit un ensemble de bascules qui vous permet de choisir les catégories auxquelles vous abonner.</span><span class="sxs-lookup"><span data-stu-id="8664e-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="8664e-153">Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.</span><span class="sxs-lookup"><span data-stu-id="8664e-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="8664e-154">L'application convertit les catégories sélectionnées en balises et demande une nouvelle inscription de l'appareil pour les balises sélectionnées depuis le Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="8664e-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="8664e-155">Les catégories inscrites sont renvoyées et affichées dans une notification toast.</span><span class="sxs-lookup"><span data-stu-id="8664e-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="8664e-156">Envoyer une nouvelle notification en exécutant l’application Console .NET.</span><span class="sxs-lookup"><span data-stu-id="8664e-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="8664e-157">Vous pouvez également envoyer des notifications de modèle avec balises à l’aide de l’onglet de débogage de votre notification hub dans le [portail Azure Classic].</span><span class="sxs-lookup"><span data-stu-id="8664e-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="8664e-158">Les notifications pour les catégories sélectionnées apparaissent comme notifications toast.</span><span class="sxs-lookup"><span data-stu-id="8664e-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8664e-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8664e-159">Next steps</span></span>
<span data-ttu-id="8664e-160">Dans ce didacticiel, nous avons appris à diffuser les dernières nouvelles par catégorie.</span><span class="sxs-lookup"><span data-stu-id="8664e-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="8664e-161">Envisagez de suivre un des didacticiels suivants qui soulignent d’autres scénarios avancés Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="8664e-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="8664e-162">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]</span><span class="sxs-lookup"><span data-stu-id="8664e-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="8664e-163">Apprenez à développer l’application relative aux dernières nouvelles pour permettre l’envoi de notifications localisées.</span><span class="sxs-lookup"><span data-stu-id="8664e-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="8664e-164">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="8664e-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="8664e-165">[portail Azure Classic]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="8664e-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
