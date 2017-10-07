---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>Comment les tooIntegrate Engagement sur Android
> [!IMPORTANT]
> Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.
> 
> 

## <a name="standard-integration"></a>Intégration standard

Copiez les fichiers de ressources de portée de hello SDK dans votre projet :

* Copiez les fichiers hello hello `res/layout` dossier fourni avec le Kit de développement logiciel de hello en hello `res/layout` dossier de votre application.
* Copiez les fichiers hello hello `res/drawable` dossier fourni avec le Kit de développement logiciel de hello en hello `res/drawable` dossier de votre application.

Modifiez le fichier `AndroidManifest.xml` :

* Ajouter hello après section (entre hello `<application>` et `</application>` balises) :
  
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
* Vous avez besoin de cette autorisation tooreplay système les notifications qui n’étaient pas activés au démarrage (sinon ils seront conservés sur le disque, mais ne s’affiche plus, vous devez tooinclude cela).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Spécifier une icône utilisée pour les notifications (à la fois dans l’application et ceux de système) en copiant et en modifiant les hello après section (entre hello `<application>` et `</application>` balises) :
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Cette section est **obligatoire** si vous prévoyez d'utiliser les notifications système lors de la création de campagnes de couverture. Android empêche les notifications système sans icône de s'afficher. Si vous omettez cette section, vos utilisateurs finaux seront donc pas en mesure de tooreceive les.
> 
> 

* Si vous créez des campagnes avec les notifications système à l’aide de la vue d’ensemble, vous devez hello tooadd les autorisations suivantes (après hello `</application>` balise) si manquant :
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Sur Android M et si votre application cible un niveau d’API Android 23 ou supérieur, l’autorisation ``WRITE_EXTERNAL_STORAGE`` nécessite l’approbation de l’utilisateur. Veuillez lire [cette section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Pour les notifications système que vous pouvez également spécifier dans hello atteindre campagne si l’appareil de hello doit sonner et/ou faire vibrer. Pour qu’il toowork, que vous avez toomake que vous avez déclaré hello suivant d’autorisation (après hello `</application>` étiquette) :
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Sans cette autorisation, Android empêche les notifications système est affichée si vous avez coché anneau de hello ou hello faire vibrer option dans le Gestionnaire d’atteindre une campagne hello.

## <a name="native-push"></a>Native Push
Maintenant que vous avez configuré le module de couverture, vous devez tooconfigure push natif toobe tooreceive en mesure de hello campagnes marketing sur les appareils hello.

Nous prenons en charge les deux services sur Android :

* Les appareils Google Play : utilisez [messagerie Cloud Google] par hello suivant [comment tooIntegrate GCM avec Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.
* Les appareils Amazon : utilisez [Amazon Device Messaging] par hello suivant [comment tooIntegrate ADM avec Engagement guide](mobile-engagement-android-adm-integrate.md) guide.

Si vous souhaitez tootarget appareils Amazon et Google Play, ses toohave possible tout son contenu 1 AndroidManifest.xml/APK pour le développement. Mais lorsque vous soumettez tooAmazon, ils peuvent rejeter votre application s’ils trouvent le code GCM.

Dans ce cas, vous devrez utiliser plusieurs fichiers APK.

**Votre application est maintenant prêt tooreceive et affichage atteint campagnes !**

## <a name="how-toohandle-data-push"></a>Comment les données toohandle push
### <a name="integration"></a>Intégration
Si vous souhaitez que votre application toobe en mesure d’exécute un push de tooreceive les données de couverture, que vous avez toocreate une sous-classe de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` et référencez-la dans hello `AndroidManifest.xml` fichier (entre hello `<application>` et/ou `</application>` balises) :

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Vous pouvez remplacer hello `onDataPushStringReceived` et `onDataPushBase64Received` rappels. Voici un exemple :

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Catégorie
paramètre de catégorie Hello est facultatif lorsque vous créez une campagne de Push de données et permet de que vous toofilter données exécute un push. Cela est utile si vous avez plusieurs récepteurs de diffusion la gestion des différents types de push de données, ou si vous souhaitez toopush différents types de `Base64` tooidentify de données et que vous souhaitez leur type avant de les analyser.

### <a name="callbacks-return-parameter"></a>Paramètre de retour des rappels
Voici quelques recommandations tooproperly handle hello paramètre de retour de `onDataPushStringReceived` et `onDataPushBase64Received`:

* Un récepteur de diffusion doit retourner `null` dans le rappel hello si elles ne savent pas comment toohandle données push. Vous devez utiliser hello catégorie toodetermine si votre récepteur de diffusion doit gérer la transmission de données hello ou non.
* Un récepteur de diffusion hello doit retourner `true` dans le rappel hello si ce dernier accepte push de données hello.
* Un récepteur de diffusion hello doit retourner `false` dans le rappel hello s’il reconnaît le push de données hello, mais il ignore pour une raison quelconque. Par exemple, retourner `false` lorsque les données de salutation reçue ne sont pas valides.
* Si une diffusion récepteur retourne `true` tandis que l’autre un retourne `false` pour hello même push de données, le comportement de hello n’est pas défini, vous devez le faire jamais.

type de retour Hello est utilisé uniquement pour les statistiques de couverture hello :

* `Replied`est incrémenté si un des récepteurs de diffusion hello renvoyées `true` ou `false`.
* `Actioned`est incrémenté uniquement si un des hello diffusion récepteurs retournés `true`.

## <a name="how-toocustomize-campaigns"></a>Comment les campagnes toocustomize
toocustomize campagnes, vous pouvez modifier les présentations hello Bonjour SDK Reach.

Vous devez conserver tous les identificateurs hello sont utilisées dans les dispositions de hello et maintenir des types hello de vues hello qui utilisent un identificateur, en particulier pour les affichages de texte et image. Certaines vues sont toohide uniquement utilisé ou affichent les zones de leur type peut être modifié. Vérifiez le code source de hello si vous envisagez de type hello de toochange d’une vue dans les dispositions de hello fourni.

### <a name="notifications"></a>Notifications
Il existe deux types de notifications : les notifications système et les notifications dans l'application qui utilisent des fichiers de disposition différents.

#### <a name="system-notifications"></a>Notifications système
les notifications système toocustomize vous devez toouse hello **catégories**. Vous pouvez passer trop[catégories](#categories).

#### <a name="in-app-notifications"></a>Notifications dans l'application
Par défaut, une notification dans l’application est une vue qui est la méthode Android toohello ajoutées de manière dynamique actuelle activité utilisateur interface Merci toohello `addContentView()`. Il s'agit d'une superposition de notification. Superpositions de notification sont parfaites pour une intégration rapide, car ils ne nécessitent pas vous toomodify toute disposition dans votre application.

apparence hello toomodify votre superpositions de notification, il suffit de modifier le fichier de hello `engagement_notification_area.xml` tooyour a besoin.

> [!NOTE]
> fichier de Hello `engagement_notification_overlay.xml` est celui utilisé toocreate hello du segment de recouvrement de la notification, elle inclut les fichiers hello `engagement_notification_area.xml`. Vous pouvez également personnaliser toosuit (par exemple pour positionner la zone de notification hello dans un segment de recouvrement hello) de vos besoins.
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Inclure une disposition de notification dans une disposition d'activité
Les superpositions sont idéales pour une intégration rapide, mais peuvent être gênantes ou avoir des effets indésirables dans certains cas. Hello superposition système peut être personnalisé à un niveau d’activité, rendant les effets secondaires tooprevent facile pour les activités spéciales.

Vous pouvez décider tooinclude à notre disposition de notification dans votre toohello Merci d’existant disposition Android **incluent** instruction. Hello Voici un exemple d’une modification `ListActivity` disposition contenant simplement un `ListView`.

**Avant l'intégration d'Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Après l'intégration d'Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

Dans cet exemple, nous avons ajouté un conteneur parent car mise hello utilisé un affichage de liste en tant qu’élément de niveau supérieur hello. Nous avons également ajouté `android:layout_weight="1"` tooadd en mesure de toobe une vue au-dessous d’un affichage de liste configurés avec `android:layout_height="fill_parent"`.

Hello SDK Reach d’Engagement détecte automatiquement cette mise en page de notification hello est inclus dans cette activité et n’ajoute pas d’un segment de recouvrement pour cette activité.

> [!TIP]
> Si vous utilisez un ListActivity dans votre application, un segment de recouvrement portée visible vous empêcheront les éléments tooclicked réaction en mode hello plus. Il s'agit d'un problème connu. toowork résoudre ce problème, nous vous suggérons tooembed hello notification mise en page dans votre propre disposition de liste d’activités, comme dans l’exemple précédent hello.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Désactivation des notifications d'application par activité
Si vous ne souhaitez pas hello superposition toobe ajouté tooyour activité, et si vous n’incluez pas mise en page de notification hello dans votre propre mise en page, vous pouvez désactiver la superposition hello pour cette activité Bonjour `AndroidManifest.xml` en ajoutant un `meta-data` section comme dans les éléments suivants de hello exemple :

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> Catégories
Lorsque vous modifiez hello fourni mises en page, vous modifiez apparence hello toutes vos notifications. Les catégories permettent toodefine que différents ciblés recherche (et éventuellement des comportements) pour les notifications. Une catégorie peut être spécifiée lorsque vous créez une campagne Reach. N'oubliez pas que les catégories vous permettent également de personnaliser les annonces et les sondages, décrits plus avant dans ce document.

tooregister un gestionnaire de catégorie pour les notifications, vous devez tooadd un appel lorsque l’application hello est initialisée.

> [!IMPORTANT]
> Veuillez lire avertissement hello sur hello android : traiter l’attribut \<android-sdk-engagement-process\> Bonjour comment tooIntegrate Engagement sur la rubrique Android avant de continuer.
> 
> 

Hello exemple suivant suppose que vous les avertissement précédent hello d’accusé de réception et que vous utilisez une sous-classe de `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Hello `MyNotifier` objet est mise en oeuvre de hello du Gestionnaire de catégorie de notification hello. Il s’agit d’une mise en œuvre de hello `EngagementNotifier` interface ou une sous-classe de l’implémentation par défaut de hello : `EngagementDefaultNotifier`.

Notez que hello même notifiant peut gérer plusieurs catégories, vous pouvez les enregistrer comme suit :

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello catégorie l’implémentation par défaut, vous pouvez inscrire votre implémentation comme Bonjour l’exemple suivant :

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

catégorie de Hello actuelle utilisée dans un gestionnaire est passé en tant que paramètre dans la plupart des méthodes que vous pouvez substituer dans `EngagementDefaultNotifier`.

Elle est passée en tant que paramètre `String` ou indirectement dans un objet `EngagementReachContent` ayant une méthode `getCategory()`.

Vous pouvez modifier la plupart des processus de création de notification hello en redéfinissant les méthodes sur `EngagementDefaultNotifier`, pour une personnalisation plus avancée sentir libre tootake un coup de œil à la documentation technique hello et au code source de hello.

##### <a name="in-app-notifications"></a>Notifications dans l'application
Si vous souhaitez simplement toouse différentes dispositions pour une catégorie spécifique, vous pouvez implémenter cela comme hello l’exemple suivant :

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Exemple de `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Comme vous pouvez le voir, identificateur d’affichage superposition hello est différent de celui standard de hello un. Il est important que chaque disposition utilise un identificateur unique pour les superpositions.

**Exemple de `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Comme vous pouvez le voir, identificateur de vue de zone de notification hello est différente de celle standard de hello un. Il est important que chaque disposition utilise un identificateur unique pour les zones de notification.

Cet exemple simple de la catégorie rend l’application (ou dans l’application) des notifications affichées en haut de hello d’écran hello. Nous n’a pas changé les identificateurs standard hello utilisés dans la zone de notification hello lui-même.

Si vous souhaitez toochange que vous avez tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` (méthode). Il est recommandé de toolook à la documentation technique hello et au code source de hello de `EngagementNotifier` et `EngagementDefaultNotifier` si vous souhaitez que ce niveau de personnalisation avancée.

##### <a name="system-notifications"></a>Notifications système
En étendant `EngagementDefaultNotifier`, vous pouvez remplacer `onNotificationPrepared` notification hello tooalter qui a été préparée par l’implémentation par défaut de hello.

Par exemple :

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

Cet exemple montre une notification du système pour un contenu affiché sous la forme d’un événement en cours lors de la catégorie « en cours » hello est utilisée.

Si vous souhaitez toobuild hello `Notification` de l’objet à partir de zéro, vous pouvez retourner `false` toohello méthode et appel `notify` vous-même sur hello `NotificationManager`. Dans ce cas, il est important de conserver un `contentIntent`, un `deleteIntent` et hello identificateur de notification utilisé par `EngagementReachReceiver`.

Voici un exemple correct d'une telle implémentation :

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Annonces avec notifications uniquement
Hello Hello, cliquez sur une notification annonce uniquement peut être personnalisé en substituant `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify préparée `Intent`. À l’aide de cette méthode vous permet des indicateurs de hello tootune facilement.

Par exemple tooadd hello `SINGLE_TOP` indicateur :

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Pour les utilisateurs d’Engagement hérités, notez que les notifications système sans intervention de l’URL maintenant lance application hello si elle était en arrière-plan, cette méthode peut être appelée avec une annonce sans URL de l’action. Vous devez envisager que lors de la personnalisation d’intention de hello.

Vous pouvez également implémenter `EngagementNotifier.executeNotifAnnouncementAction` à partir de zéro.

##### <a name="notification-life-cycle"></a>Cycle de vie des notifications
Lorsque vous utilisez la catégorie par défaut de hello, certaines méthodes de cycle de vie sont appelées sur hello `EngagementReachInteractiveContent` tooreport des statistiques et mise à jour hello campagne l’état de l’objet :

* Lors de la notification de hello est affichée dans l’application ou placée dans la barre d’état hello, hello `displayNotification` méthode est appelée (qui fournit des statistiques) par `EngagementReachAgent` si `handleNotification` retourne `true`.
* Si la notification de hello est fermée, hello `exitNotification` méthode est appelée, la statistique est signalée et campagnes suivants peuvent maintenant être traités.
* Cliquez sur la notification de hello `actionNotification` est appelée, la statistique est signalée et l’intention de hello associé est lancée.

Si votre implémentation de `EngagementNotifier` contournements hello le comportement par défaut, vous pouvez toocall ces méthodes de cycle de vie vous-même. Hello suivant exemples illustre certains cas où le comportement par défaut de hello est ignorée :

* Vous n'étendez pas `EngagementDefaultNotifier`, par exemple, vous avez implémenté la gestion des catégories à partir de zéro.
* Pour les notifications système, vous a substitué hello `onNotificationPrepared` et vous avez modifié `contentIntent` ou `deleteIntent` Bonjour `Notification` objet.
* Pour les notifications dans l’application, vous se `prepareInAppArea`, être d’au moins sûr toomap `actionNotification` tooone de vos contrôles U.I.

> [!NOTE]
> Si `handleNotification` lève une exception, hello contenu est supprimé et `dropContent` est appelée. Ceci est signalé dans les statistiques et les campagnes suivantes peuvent être traitées.
> 
> 

### <a name="announcements-and-polls"></a>Annonces et sondages
#### <a name="layouts"></a>Mises en forme
Vous pouvez modifier hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` et `engagement_poll.xml` toocustomize texte annonces, des annonces de web et des interrogations de fichiers.

Ces fichiers partagent deux dispositions courantes pour la zone de titre hello et zone de bouton hello. mise en page Hello pour le titre de hello est `engagement_content_title.xml` et utilise hello éponyme fichier drawable pour l’arrière-plan de hello. Hello la disposition des boutons d’action et quitter hello est `engagement_button_bar.xml` et utilise hello éponyme fichier drawable pour l’arrière-plan de hello.

Dans un sondage, hello mise en page de question et de leur choix est dynamiquement à l’aide de plusieurs fois hello `engagement_question.xml` fichier de disposition pour les questions de hello et hello `engagement_choice.xml` fichier pour les choix de hello.

#### <a name="categories"></a>Catégories
##### <a name="alternate-layouts"></a>Autres dispositions
Telles que les notifications, catégorie de la campagne hello peut être utilisé toohave des formes différentes vos annonces et les interroge.

Par exemple, de le toocreate une catégorie pour une annonce de texte, vous pouvez étendre `EngagementTextAnnouncementActivity` et à le référencer hello `AndroidManifest.xml` fichier :

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Notez cette catégorie hello dans l’intention de hello sert de filtre de différence de hello toomake avec une activité d’annonce hello par défaut.

Hello SDK Reach utilise hello intention tooresolve hello droite l’activité du système pour une catégorie spécifique et qu’il revient de catégorie par défaut de hello en cas d’échec de la résolution de hello.

Vous devez tooimplement `MyCustomTextAnnouncementActivity`, si vous venez laquelle toochange hello présentation (mais conservez hello même afficher les identificateurs), vous avez simplement classe hello toodefine, telles que Bonjour l’exemple suivant :

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

catégorie de par défaut hello tooreplace des annonces de texte, remplacez simplement `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` par votre implémentation.

Les annonces web et les sondages peuvent être personnalisés de la même manière.

Les annonces de web, vous pouvez étendre `EngagementWebAnnouncementActivity` et déclarer votre activité Bonjour `AndroidManifest.xml` comme Bonjour l’exemple suivant :

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Pour les sondages, vous pouvez étendre `EngagementPollActivity` et déclarer votre hello en `AndroidManifest.xml` comme Bonjour l’exemple suivant :

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implémentation à partir de zéro
Vous pouvez implémenter des catégories pour vos activités d’annonce (et d’interrogation) sans étendre un des hello `Engagement*Activity` classes fournies par hello SDK Reach. Cela est utile par exemple si vous souhaitez toodefine une disposition qui n’utilise pas de hello même vues comme les dispositions standard hello.

Comme pour la personnalisation de la notification avancés, il est recommandé toolook au code source de hello d’implémentation standard de hello.

Voici certains tookeep choses à l’esprit : portée lancera activité hello avec un mode spécifique (filtre intention toohello correspondant) ainsi que d’un paramètre supplémentaire qui est l’identificateur de contenu hello.

objet contenu tooretrieve hello qui contiennent des champs hello vous avez spécifié lorsque hello de création de la campagne sur le site web de hello vous pouvez procédez comme suit :

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Pour les statistiques, vous devez signaler l’affichage du contenu de hello dans hello `onResume` événement :

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Ensuite, n’oubliez pas toocall soit `actionContent(this)` ou `exitContent(this)` sur l’objet de contenu hello avant l’activité hello passe en arrière-plan.

Si vous n’appelez pas soit `actionContent` ou `exitContent`, les statistiques ne seront pas envoyées (autrement dit, aucune analytique sur une campagne de hello) et plus important encore, hello campagnes suivants ne seront pas informés qu’après le redémarrage du processus d’application hello.

L’orientation ou autres modifications de configuration peut prendre de toodetermine difficile de code hello activité hello passe en arrière-plan ou non, hello rend implémentation standard que contenu de hello est signalé comme quitté si l’utilisateur de hello quitte activité hello (soit en en appuyant sur `HOME` ou `BACK`), mais pas si hello orientation change.

Ici est hello intéressantes dans hello implémentation :

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Comme vous pouvez le voir, si vous avez appelé `actionContent(this)` puis terminé l’activité hello, `exitContent(this)` peut être appelée en toute sécurité sans avoir aucun effet.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[messagerie Cloud Google]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
