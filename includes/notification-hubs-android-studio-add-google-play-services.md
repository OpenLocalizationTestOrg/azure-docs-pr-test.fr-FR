1. <span data-ttu-id="95aa8-101">Hello Open Android SDK Manager en cliquant sur icône hello sur la barre d’outils hello de Android Studio ou en cliquant sur **outils** -> **Android** -> **SDK Manager**menu hello.</span><span class="sxs-lookup"><span data-stu-id="95aa8-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="95aa8-102">Localiser la version cible de hello Hello du SDK Android qui est utilisé dans votre projet, ouvrez-le en cliquant sur **afficher les détails de Package**, puis choisissez **APIs Google**, s’il n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="95aa8-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="95aa8-103">Cliquez sur hello **outils SDK** onglet. Si vous n’avez pas encore installé Google Play Service, cliquez sur **Services Google Play** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="95aa8-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="95aa8-104">Puis cliquez sur **appliquer** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="95aa8-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="95aa8-105">Notez le chemin d’accès du Kit de développement logiciel hello, pour une utilisation dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="95aa8-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="95aa8-106">Ouvrez hello **build.gradle** fichier dans le répertoire de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="95aa8-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="95aa8-107">Ajoutez la ligne suivante sous *dépendances*:</span><span class="sxs-lookup"><span data-stu-id="95aa8-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="95aa8-108">Cliquez sur hello **projet de synchronisation avec les fichiers Gradle** icône dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="95aa8-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="95aa8-109">Ouvrez **AndroidManifest.xml** et ajoutez cette balise toohello *application* balise.</span><span class="sxs-lookup"><span data-stu-id="95aa8-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

