
### <a name="update-manifest-file-tooenable-notifications"></a>Mettre à jour le fichier manifeste tooenable notifications
Copier les ressources de messagerie dans l’application hello ci-dessous dans votre Manifest.xml entre hello `<application>` et `</application>` balises.

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a>Spécifier une icône pour les notifications
Hello coller suivant extrait de code XML dans votre Manifest.xml entre hello `<application>` et `</application>` balises.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Icône de hello qui s’affiche à la fois dans le système et les notifications dans l’application définit. Facultative pour les notifications in-app, cette opération est toutefois obligatoire pour les notifications système. Android rejettera les notifications système avec des icônes non valides.

Assurez-vous que vous utilisez une icône qui existe dans un des hello **drawable** dossiers (comme ``engagement_close.png``). **mipmap** n’est pas pris en charge.

> [!NOTE]
> Vous ne devez pas utiliser hello **Lanceur** icône. Il présente une résolution différente et est généralement dans des dossiers mipmap hello que nous ne prennent pas en charge.
> 
> 

Pour les applications réelles, vous pouvez utiliser une icône adaptée aux notifications conformément aux [instructions sur la conception Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toouse vraiment de toobe correct résolutions d’icône, vous pouvez examiner [ces exemples](https://www.google.com/design/icons).
> Faites défiler vers le bas toohello **Notification** section, cliquez sur une icône, puis cliquez sur `PNGS` jeu drawable hello toodownload. Vous pouvez voir quels dossiers drawable avec le toouse de résolution pour chaque version de l’icône de hello.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Activer les notifications de push application tooreceive GCM
1. Collez hello qui suit dans votre Manifest.xml entre hello `<application>` et `</application>` balises après le remplacement hello **ID de l’expéditeur** obtenu à partir de votre console de projet Firebase. Hello \n est intentionnel donc vous assurer que vous mettez fin à projet hello nombre avec lui.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Collez le code hello ci-dessous dans votre Manifest.xml entre hello `<application>` et `</application>` balises. Remplacez le nom du package hello <Your package name>.
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. Ajouter le dernier jeu d’autorisations qui sont mis en surbrillance avant hello de hello `<application>` balise. Remplacez `<Your package name>` par nom de package réel hello de votre application.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

