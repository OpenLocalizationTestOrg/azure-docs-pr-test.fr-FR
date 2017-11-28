
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="3adbd-101">Mettre à jour le fichier manifeste pour activer les notifications</span><span class="sxs-lookup"><span data-stu-id="3adbd-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="3adbd-102">Copiez les ressources de messagerie in-app ci-dessous dans votre fichier Manifest.xml entre les balises `<application>` et `</application>`.</span><span class="sxs-lookup"><span data-stu-id="3adbd-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="3adbd-103">Spécifier une icône pour les notifications</span><span class="sxs-lookup"><span data-stu-id="3adbd-103">Specify an icon for notifications</span></span>
<span data-ttu-id="3adbd-104">Collez l’extrait de code XML suivant dans votre fichier Manifest.xml entre les balises `<application>` et `</application>`.</span><span class="sxs-lookup"><span data-stu-id="3adbd-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="3adbd-105">Cela définit l’icône qui s’affiche à la fois dans le système et des notifications in-app.</span><span class="sxs-lookup"><span data-stu-id="3adbd-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="3adbd-106">Facultative pour les notifications in-app, cette opération est toutefois obligatoire pour les notifications système.</span><span class="sxs-lookup"><span data-stu-id="3adbd-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="3adbd-107">Android rejettera les notifications système avec des icônes non valides.</span><span class="sxs-lookup"><span data-stu-id="3adbd-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="3adbd-108">Assurez-vous d’utiliser une icône qui existe dans l’un des dossiers **drawable``engagement_close.png`` (comme**).</span><span class="sxs-lookup"><span data-stu-id="3adbd-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="3adbd-109">**mipmap** n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3adbd-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="3adbd-110">Vous ne devez pas utiliser l’icône du **Lanceur** .</span><span class="sxs-lookup"><span data-stu-id="3adbd-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="3adbd-111">Elle a une résolution différente et se trouve généralement dans les dossiers mipmap, que nous ne prenons pas en charge.</span><span class="sxs-lookup"><span data-stu-id="3adbd-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="3adbd-112">Pour les applications réelles, vous pouvez utiliser une icône adaptée aux notifications conformément aux [instructions sur la conception Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="3adbd-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="3adbd-113">Pour veiller à utiliser des icônes de résolutions correctes, vous pouvez consulter [ces exemples](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="3adbd-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="3adbd-114">Faites défiler jusqu’à la section **Notification**, cliquez sur une icône, puis sur `PNGS` pour télécharger le jeu d’icônes.</span><span class="sxs-lookup"><span data-stu-id="3adbd-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="3adbd-115">Vous pouvez voir quels dossiers dessinables utiliser avec quelle résolution pour chaque version de l’icône.</span><span class="sxs-lookup"><span data-stu-id="3adbd-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="3adbd-116">Activer votre application pour recevoir des notifications Push GCM</span><span class="sxs-lookup"><span data-stu-id="3adbd-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="3adbd-117">Collez le code suivant dans votre fichier Manifest.xml entre les balises `<application>` et `</application>` après le remplacement du **Sender ID** obtenu à partir de votre console de projet Firebase.</span><span class="sxs-lookup"><span data-stu-id="3adbd-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="3adbd-118">Le \n est intentionnel alors assurez-vous que le numéro de projet se termine avec ce dernier.</span><span class="sxs-lookup"><span data-stu-id="3adbd-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="3adbd-119">Collez le code ci-dessous dans votre fichier Manifest.xml entre les balises `<application>`et`</application>`.</span><span class="sxs-lookup"><span data-stu-id="3adbd-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="3adbd-120">Remplacez le nom du package <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="3adbd-120">Replace the package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="3adbd-121">Ajoutez le dernier jeu d’autorisations mis en surbrillance avant la balise `<application>` .</span><span class="sxs-lookup"><span data-stu-id="3adbd-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="3adbd-122">Remplacez `<Your package name>` par le nom réel du package de votre application.</span><span class="sxs-lookup"><span data-stu-id="3adbd-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

