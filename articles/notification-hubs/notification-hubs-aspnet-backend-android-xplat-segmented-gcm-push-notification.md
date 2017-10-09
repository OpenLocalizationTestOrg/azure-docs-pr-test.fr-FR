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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilisez toosend concentrateurs de Notification dernières actualités
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooan application Android. Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories. Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..

Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello. Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello. Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance. Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Composants requis
Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started]. Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Ajouter une application de toohello de sélection de catégorie
première étape de Hello est tooadd hello éléments tooyour existant principale activité d’interface utilisateur qui permettent de hello utilisateur tooselect catégories tooregister. catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello. Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.

1. Ouvrez votre fichier res/layout/activity_main.xml et remplacer le contenu avec les éléments suivants de hello hello :
   
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
2. Ouvrez votre fichier res/values/strings.xml et ajoutez les lignes suivantes de hello :
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    La présentation graphique de votre fichier main_activity.xml doit ressembler à ceci :
   
    ![][A1]
3. Créer une classe **Notifications** Bonjour du même package en tant que votre **MainActivity** classe.
   
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
   
    Cette classe utilise hello stockage local des catégories de hello toostore de news que ce périphérique a tooreceive. Il contient également des tooregister des méthodes pour ces catégories.
4. Dans la classe **MainActivity**, supprimez vos champs privés pour **NotificationHub** et **GoogleCloudMessaging**, puis ajoutez un champ pour **Notifications** :
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Ensuite, dans hello **onCreate** (méthode), supprimez l’initialisation de hello Hello **hub** champ et hello **registerWithNotificationHubs** (méthode). Ajoutez ensuite hello après les lignes qui initialise une instance de hello **Notifications** classe. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`et `HubListenConnectionString` doit déjà être définie avec hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu plus haut.

    > [AZURE.NOTE] Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente. Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées. clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.


1. Ensuite, ajoutez hello suivant importe et `subscribe` hello toohandle de méthode s’abonner bouton événements click :
   
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
   
    Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification. Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.

Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories

## <a name="register-for-notifications"></a>Inscription à des notifications
Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.

> [!NOTE]
> Étant donné que registrationId hello attribué par Google Cloud Messaging (GCM) peut changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification. Cet exemple inscrit pour la notification chaque fois que cette application hello démarre. Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.
> 
> 

1. Ajouter hello suivant du code à la fin de hello de hello **onCreate** méthode Bonjour **MainActivity** classe :
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et demande une inscription pour ces catégories. 
2. Mettez à jour hello `onStart()` méthode Hello `MainActivity` classe comme suit :
   
    @Override  protected void onStart() {
   
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
    }
   
    Cela met à jour l’activité principale hello basée sur l’état de hello des catégories précédemment enregistrés.

application Hello est maintenant terminée et permettre de stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories. Ensuite, nous allons définir un serveur principal qui peut envoyer catégorie notifications toothis application.

## <a name="sending-tagged-notifications"></a>Envoi des notifications avec balises
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Exécutez l’application hello et générer des notifications
1. Dans Android Studio, générez l’application hello et démarrez-le sur un périphérique ou un émulateur.
   
    Notez que cette application hello de que l’interface utilisateur fournit un ensemble bascule qui permet de choisir toosubscribe de catégories hello pour.
2. Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.
   
    application Hello convertit les catégories de hello sélectionné en balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello. Hello catégories inscrits sont retournés et affichés dans une notification toast.
3. Envoyer une notification en exécutant l’application de Console de .NET hello.  Vous pouvez également envoyer les notifications de modèle avec balises à l’aide d’onglet de débogage de hello de votre concentrateur de notification Bonjour [portail classique Azure].
   
    Les notifications pour les catégories de hello sélectionné s’affichent sous forme de notifications de toast.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie. Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :

* [Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]
  
    Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.

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
