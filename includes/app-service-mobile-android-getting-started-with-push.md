1. <span data-ttu-id="b9b1c-101">Dans votre **application** projet, les fichiers ouverts hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="b9b1c-102">Dans le code hello dans hello deux étapes suivantes, remplacez  *`**my_app_package**`*  par nom de hello du package d’application hello pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="b9b1c-103">Valeur hello Hello `package` attribut Hello `manifest` balise.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="b9b1c-104">Ajouter hello suivant nouvelles autorisations après hello existant `uses-permission` élément :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="b9b1c-105">Ajouter hello après le code après hello `application` balise d’ouverture :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="b9b1c-106">Les fichiers ouverts hello *ToDoActivity.java*et ajoutez hello après l’instruction d’importation :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="b9b1c-107">Ajoutez hello suivant toohello variable privée classe.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="b9b1c-108">Remplacez  *`<PROJECT_NUMBER>`*  avec numéro de projet de hello attribué par Google tooyour application hello précédente procédure.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="b9b1c-109">Modifier la définition de hello de *MobileServiceClient* de **privé** trop**statique public**, donc il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="b9b1c-110">Ajoutez un nouvelles notifications toohandle de classe.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="b9b1c-111">Dans l’Explorateur de projets, ouvrez hello **src** > **principal** > **java** nœuds et nœud de nom de package avec le bouton hello.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="b9b1c-112">Cliquez sur **Nouveau**, puis sur **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="b9b1c-113">Dans **Nom**, tapez `MyHandler`, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="b9b1c-114">Dans le fichier de MyHandler hello, remplacez la déclaration de classe de hello avec :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="b9b1c-115">Ajouter hello suivant les instructions d’importation pour hello `MyHandler` classe :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="b9b1c-116">Ensuite, ajoutez cette toohello membre `MyHandler` classe :</span><span class="sxs-lookup"><span data-stu-id="b9b1c-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="b9b1c-117">Bonjour `MyHandler` de classe, ajoutez hello suivant hello toooverride de code **onRegistered** (méthode), qui inscrit votre appareil avec un concentrateur de notification du service mobile hello.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="b9b1c-118">}</span><span class="sxs-lookup"><span data-stu-id="b9b1c-118">}</span></span>
13. <span data-ttu-id="b9b1c-119">Bonjour `MyHandler` de classe, ajoutez hello suivant hello toooverride de code **onReceive** (méthode), ce qui amène hello notification toodisplay lorsqu’elle est reçue.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="b9b1c-120">}</span><span class="sxs-lookup"><span data-stu-id="b9b1c-120">}</span></span>
14. <span data-ttu-id="b9b1c-121">Dans le fichier de TodoActivity.java hello, mettre à jour de hello **onCreate** méthode Hello *ToDoActivity* classe classe du Gestionnaire de notification tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="b9b1c-122">Rendre le code que tooadd après hello *MobileServiceClient* est instancié.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="b9b1c-123">Votre application est maintenant des notifications push de toosupport mis à jour.</span><span class="sxs-lookup"><span data-stu-id="b9b1c-123">Your app is now updated toosupport push notifications.</span></span>
