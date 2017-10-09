1. Hello Open Android SDK Manager en cliquant sur icône hello sur la barre d’outils hello de Android Studio ou en cliquant sur **outils** -> **Android** -> **SDK Manager**menu hello. Localiser la version cible de hello Hello du SDK Android qui est utilisé dans votre projet, ouvrez-le en cliquant sur **afficher les détails de Package**, puis choisissez **APIs Google**, s’il n’est pas déjà installé.
2. Cliquez sur hello **outils SDK** onglet. Si vous n’avez pas encore installé Google Play Service, cliquez sur **Services Google Play** comme indiqué ci-dessous. Puis cliquez sur **appliquer** tooinstall. 
   
    Notez le chemin d’accès du Kit de développement logiciel hello, pour une utilisation dans une étape ultérieure. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Ouvrez hello **build.gradle** fichier dans le répertoire de l’application hello.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Ajoutez la ligne suivante sous *dépendances*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Cliquez sur hello **projet de synchronisation avec les fichiers Gradle** icône dans la barre d’outils hello.
6. Ouvrez **AndroidManifest.xml** et ajoutez cette balise toohello *application* balise.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

