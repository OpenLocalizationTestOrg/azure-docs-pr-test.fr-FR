
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="d8874-101">Mettre à jour le fichier manifeste tooenable notifications</span><span class="sxs-lookup"><span data-stu-id="d8874-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="d8874-102">Copier les ressources de messagerie dans l’application hello ci-dessous dans votre Manifest.xml entre hello `<application>` et `</application>` balises.</span><span class="sxs-lookup"><span data-stu-id="d8874-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="d8874-103">Spécifier une icône pour les notifications</span><span class="sxs-lookup"><span data-stu-id="d8874-103">Specify an icon for notifications</span></span>
<span data-ttu-id="d8874-104">Hello coller suivant extrait de code XML dans votre Manifest.xml entre hello `<application>` et `</application>` balises.</span><span class="sxs-lookup"><span data-stu-id="d8874-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="d8874-105">Icône de hello qui s’affiche à la fois dans le système et les notifications dans l’application définit.</span><span class="sxs-lookup"><span data-stu-id="d8874-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="d8874-106">Facultative pour les notifications in-app, cette opération est toutefois obligatoire pour les notifications système.</span><span class="sxs-lookup"><span data-stu-id="d8874-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="d8874-107">Android rejettera les notifications système avec des icônes non valides.</span><span class="sxs-lookup"><span data-stu-id="d8874-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="d8874-108">Assurez-vous que vous utilisez une icône qui existe dans un des hello **drawable** dossiers (comme ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="d8874-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="d8874-109">**mipmap** n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d8874-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="d8874-110">Vous ne devez pas utiliser hello **Lanceur** icône.</span><span class="sxs-lookup"><span data-stu-id="d8874-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="d8874-111">Il présente une résolution différente et est généralement dans des dossiers mipmap hello que nous ne prennent pas en charge.</span><span class="sxs-lookup"><span data-stu-id="d8874-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="d8874-112">Pour les applications réelles, vous pouvez utiliser une icône adaptée aux notifications conformément aux [instructions sur la conception Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="d8874-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="d8874-113">toouse vraiment de toobe correct résolutions d’icône, vous pouvez examiner [ces exemples](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="d8874-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="d8874-114">Faites défiler vers le bas toohello **Notification** section, cliquez sur une icône, puis cliquez sur `PNGS` jeu drawable hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="d8874-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="d8874-115">Vous pouvez voir quels dossiers drawable avec le toouse de résolution pour chaque version de l’icône de hello.</span><span class="sxs-lookup"><span data-stu-id="d8874-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="d8874-116">Activer les notifications de push application tooreceive GCM</span><span class="sxs-lookup"><span data-stu-id="d8874-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="d8874-117">Collez hello qui suit dans votre Manifest.xml entre hello `<application>` et `</application>` balises après le remplacement hello **ID de l’expéditeur** obtenu à partir de votre console de projet Firebase.</span><span class="sxs-lookup"><span data-stu-id="d8874-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="d8874-118">Hello \n est intentionnel donc vous assurer que vous mettez fin à projet hello nombre avec lui.</span><span class="sxs-lookup"><span data-stu-id="d8874-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="d8874-119">Collez le code hello ci-dessous dans votre Manifest.xml entre hello `<application>` et `</application>` balises.</span><span class="sxs-lookup"><span data-stu-id="d8874-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="d8874-120">Remplacez le nom du package hello <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="d8874-120">Replace hello package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="d8874-121">Ajouter le dernier jeu d’autorisations qui sont mis en surbrillance avant hello de hello `<application>` balise.</span><span class="sxs-lookup"><span data-stu-id="d8874-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="d8874-122">Remplacez `<Your package name>` par nom de package réel hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="d8874-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

