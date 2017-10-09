---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une ancienne version de notre kit de développement logiciel dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello. Par exemple, si vous migrez à partir de 1.4.0 too1.6.0 que vous avez toofirst suivez hello » à partir de 1.4.0 too1.5.0 « procédure puis hello » à partir de 1.5.0 too1.6.0 » procédure.

Version hello vous mettez à niveau, vous avez tooreplace hello `mobile-engagement-VERSION.jar` avec hello nouveau.

## <a name="from-420-too421"></a>À partir de 4.2.0 too4.2.1
Cette étape peut effectivement être effectuée sur n’importe quelle version du Kit de développement logiciel de hello, il s’agit d’une amélioration de la sécurité lorsque vous intégrez les activités de portée.

Vous devez maintenant ajouter `exported="false"` tooall portée activités.

Les activités Reach doivent maintenant ressembler à ceci sur votre `AndroidManifest.xml`:

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

## <a name="from-400-too410"></a>À partir de 4.0.0 too4.1.0
Hello SDK maintenant handle nouveau modèle d’autorisation à partir d’Android M.

Si vous utilisez des fonctionnalités de localisation ou des notifications BigPicture, veuillez lire [cette section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

En outre toohello nouveau modèle d’autorisation, nous prennent désormais en charge la configuration des fonctionnalités de l’emplacement lors de l’exécution.
Nous sommes toujours compatibles avec les paramètres de manifeste hello pour l’emplacement, mais il est désormais déconseillée. sections de suivantes de hello de suppression toouse configuration d’exécution, à partir de votre ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

et lecture [cette procédure de mise à jour](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuration d’exécution à la place.

## <a name="from-300-too400"></a>À partir de 3.0.0 too4.0.0
### <a name="native-push"></a>Native Push
Push natif (GCM/ADM) est désormais également utilisé pour des notifications de l’application vous devez configurer les informations d’identification de push natif hello pour n’importe quel type de campagne push.

Si ce n’est déjà fait, suivez [cette procédure](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
L’intégrationReach a été modifiée dans ``AndroidManifest.xml``.

Remplacez ceci :

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

par

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

Il se peut désormais qu’un écran de chargement s’affiche lorsque vous cliquez sur une annonce (avec texte/contenu web) ou sur une interrogation.
Vous avez tooadd cela pour ces toowork campagnes dans 4.0.0 :

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Ressources
Incorporer hello nouvelle `res/layout/engagement_loading.xml` fichier dans votre projet.

## <a name="from-240-too300"></a>À partir de 2.4.0 too3.0.0
Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement. Si vous effectuez une migration à partir d’une version antérieure, consultez hello Capptain site web toomigrate too2.4.0 tout d’abord, puis appliquez hello suivant la procédure.

> [!IMPORTANT]
> Capptain Mobile Engagement sont des services mêmes pas hello et hello la procédure décrite ci-dessous met en évidence uniquement comment toomigrate hello application cliente. Migration hello SDK dans l’application hello ne sera pas migré vos données à partir de serveurs de hello Capptain serveurs toohello Mobile Engagement.
> 
> 

### <a name="jar-file"></a>Fichier JAR
Remplacez `capptain.jar` par `mobile-engagement-VERSION.jar` dans votre dossier `libs`.

### <a name="resource-files"></a>Fichiers de ressources
Chaque fichier de ressources que nous avons fournis (précédé `capptain_`) a toobe remplacé par hello nouveaux (avec le préfixe `engagement_`).

Si vous avez personnalisé ces fichiers, vous avez toore-appliquer votre personnalisation sur les nouveaux fichiers de hello, **tous les identificateurs hello dans les fichiers de ressources hello ont également été renommés**.

### <a name="application-id"></a>ID de l'application
Engagement utilise désormais une connexion chaîne tooconfigure hello Kit de développement logiciel des identificateurs comme identificateur de l’application hello.

Vous avez toouse `EngagementAgent.init` méthode dans votre activité Lanceur comme suit :

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche sur le portail Azure.

Veuillez supprimer n’importe quel appel trop`CapptainAgent.configure` comme `EngagementAgent.init` remplace cette méthode.

Hello `appId` ne peuvent plus être configurées à l’aide de `AndroidManifest.xml`.

Supprimez cette section de votre `AndroidManifest.xml` si elle existe :

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>API Java
Chaque classe Java de notre kit de développement logiciel de tooany appel a toobe renommé ; par exemple, `CapptainAgent.getInstance(this)` doit être renommé `EngagementAgent.getInstance(this)`, `extends CapptainActivity` doit être renommé `extends EngagementActivity` etc....

Si vous ont été intégrées dans les fichiers de préférence de l’agent par défaut, le nom de fichier par défaut hello est désormais `engagement.agent` et clé de hello est `engagement:agent`.

Lorsque vous créez des annonces de web, hello Javascript binder est désormais `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
De nombreuses modifications s’est-il passé et service de hello n’est pas partagé plus un grand nombre de récepteurs ne sont plus exportable.

déclaration du service Hello est désormais plus simple. Supprimez le filtre intention de hello et toutes les métadonnées qu’il contient et ajoutez `exportable=false`.

De plus, tous les éléments sont renommé toouse engagement.

Vous devez obtenir quelque chose similaire à ce qui suit :

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Lorsque vous souhaitez que les journaux des tests tooenable, hello métadonnées ont été déplacés de balise de l’application toohello et a été renommé :

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Toutes les autres métadonnées ont simplement été renommées, voici la liste complète de hello (bien entendu renommer uniquement hello celles que vous utilisez) :

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Suivi de Google Play et SmartAd a été supprimé à partir du Kit de développement logiciel vous devez tooremove cela sans remplacement :

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

activités de portée Hello sont désormais déclarées comme suit :

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

Si vous avez des activités personnalisées de portée, vous devez soit uniquement toochange hello actions intention toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hello récepteurs de diffusion ont été renommés, ainsi que nous ajoutons maintenant `exported=false`. Voici la liste complète de hello de récepteurs hello avec nouvelle spécification hello, (bien entendu renommer uniquement hello celles que vous utilisez) :

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Récepteur de suivi a été supprimé, afin que vous ayez tooremove de cette section :

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Notez que le récepteur de diffusion déclaration hello de votre implémentation de hello **EngagementMessageReceiver** a été modifié dans hello `AndroidManifest.xml`. En effet, messages hello API toosend et remove XMPP arbitraire à partir des entités XMPP arbitraires et hello API toosend et recevoir des messages entre les appareils ont été supprimées. Par conséquent, vous avez également hello toodelete suivant des rappels à partir de votre **EngagementMessageReceiver** implémentation :

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

and

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

puis supprimez tout appel sur **EngagementAgent** dans :

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

and

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Configuration proguard peut être touchée par repositionnement, hello règles sont désormais similaire à :

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

