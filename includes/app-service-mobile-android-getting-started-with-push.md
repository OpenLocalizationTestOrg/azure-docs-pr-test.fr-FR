1. Dans votre **application** projet, les fichiers ouverts hello `AndroidManifest.xml`. Dans le code hello dans hello deux étapes suivantes, remplacez  *`**my_app_package**`*  par nom de hello du package d’application hello pour votre projet. Valeur hello Hello `package` attribut Hello `manifest` balise.
2. Ajouter hello suivant nouvelles autorisations après hello existant `uses-permission` élément :

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Ajouter hello après le code après hello `application` balise d’ouverture :

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Les fichiers ouverts hello *ToDoActivity.java*et ajoutez hello après l’instruction d’importation :

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Ajoutez hello suivant toohello variable privée classe. Remplacez  *`<PROJECT_NUMBER>`*  avec numéro de projet de hello attribué par Google tooyour application hello précédente procédure.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Modifier la définition de hello de *MobileServiceClient* de **privé** trop**statique public**, donc il ressemble à ceci :

        public static MobileServiceClient mClient;
7. Ajoutez un nouvelles notifications toohandle de classe. Dans l’Explorateur de projets, ouvrez hello **src** > **principal** > **java** nœuds et nœud de nom de package avec le bouton hello. Cliquez sur **Nouveau**, puis sur **Classe Java**.
8. Dans **Nom**, tapez `MyHandler`, puis cliquez sur **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. Dans le fichier de MyHandler hello, remplacez la déclaration de classe de hello avec :

        public class MyHandler extends NotificationsHandler {
10. Ajouter hello suivant les instructions d’importation pour hello `MyHandler` classe :

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Ensuite, ajoutez cette toohello membre `MyHandler` classe :

        public static final int NOTIFICATION_ID = 1;
12. Bonjour `MyHandler` de classe, ajoutez hello suivant hello toooverride de code **onRegistered** (méthode), qui inscrit votre appareil avec un concentrateur de notification du service mobile hello.

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
       }
13. Bonjour `MyHandler` de classe, ajoutez hello suivant hello toooverride de code **onReceive** (méthode), ce qui amène hello notification toodisplay lorsqu’elle est reçue.

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
       }
14. Dans le fichier de TodoActivity.java hello, mettre à jour de hello **onCreate** méthode Hello *ToDoActivity* classe classe du Gestionnaire de notification tooregister hello. Rendre le code que tooadd après hello *MobileServiceClient* est instancié.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Votre application est maintenant des notifications push de toosupport mis à jour.
