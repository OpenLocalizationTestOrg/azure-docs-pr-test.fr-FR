---
title: aaaGet main Android applications Azure Mobile Engagement
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Prise en main d’Azure Mobile Engagement pour les applications Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Android.
Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement. À cette occasion, vous allez créer une application Android vide qui recueille des données de base et reçoit des notifications Push à l'aide de Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Composants requis
Ils auront terminé ce didacticiel requiert hello [Android Developer Tools](https://developer.android.com/sdk/index.html), qui inclut l’environnement de développement intégré Android hello et la plateforme Android hello la plus récente.

Elle requiert également hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Configuration de Mobile Engagement pour votre application Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push. Vous créez une application de base avec l’intégration de hello toodemonstrate Android Studio.

Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration de Mobile Engagement Android SDK](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Création d’une application Android
1. Démarrer **Android Studio**et dans la fenêtre contextuelle hello, sélectionnez **démarrer un nouveau projet Android Studio**.

    ![][1]
2. Indiquez un nom d’application et un domaine d’entreprise. Notez les valeurs que vous saisissez, car vous en aurez besoin ultérieurement. Cliquez sur **Suivant**.

    ![][2]
3. Sélectionnez le facteur de forme hello cible et le niveau de l’API, puis cliquez sur **suivant**.

   > [!NOTE]
   > Mobile Engagement requiert au minimum le niveau d'API 10 (Android 2.3.3).
   >
   >

    ![][3]
4. Sélectionnez **activité vide** ici, écran uniquement hello pour cette application et le clic **suivant**.

    ![][4]
5. Enfin, laissez les valeurs par défaut hello et cliquez sur **Terminer**.

    ![][5]

Android Studio crée app de démo hello dans laquelle nous intégrer Mobile Engagement.

### <a name="include-hello-sdk-library-in-your-project"></a>Inclure la bibliothèque du Kit de développement logiciel hello dans votre projet
1. Télécharger hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).
2. Extrayez hello fichier tooa dossier d’archivage dans votre ordinateur.
3. Identifier la bibliothèque de .jar hello pour la version actuelle de hello de ce Kit de développement logiciel et copiez-le toohello du Presse-papiers.

      ![][6]
4. Accédez toohello **projet** section (1) et collez hello .jar dans le dossier de bibliothèques hello (2).

      ![][7]
5. bibliothèque de hello tooload, projet hello de synchronisation.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Rejoignez votre serveur principal d’application tooMobile Engagement hello chaîne de connexion
1. Copiez hello après des lignes de code dans la création de l’activité hello (doit être effectuée uniquement dans un emplacement de votre application, généralement une activité principale hello). Pour cet exemple d’application, ouvrez hello MainActivity sous src -> principal -> dossier java et ajoutez hello qui suit :

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Résoudre les références de hello en appuyant sur Alt + Entrée ou en ajoutant des hello suivant les instructions d’importation :

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Revenir en arrière toohello portail classique de Azure dans votre application **informations de connexion** page et copie hello **chaîne de connexion**.

      ![][9]
4. Collez-le dans hello `setConnectionString` paramètre, en remplaçant la chaîne entière de hello Bonjour suivant de code :

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Ajouter des autorisations et une déclaration de service
1. Ajoutez ces toohello autorisations Manifest.xml de votre projet immédiatement avant ou après hello `<application>` balise :

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare hello du service de l’agent, ajoutez le code entre hello `<application>` et `</application>` balises :

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. Dans le code hello vous avez collé, remplacez `"<Your application name>"` dans l’étiquette de hello, qui s’affichent dans hello **paramètres** menu où vous pouvez consulter les services en cours d’exécution sur l’appareil de hello. Vous pouvez ajouter le mot hello « Service » de cette étiquette par exemple.

### <a name="send-a-screen-toomobile-engagement"></a>Envoyer un tooMobile écran Engagement
toostart envoi de données et vous assurer que les utilisateurs hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).

Accédez trop**MainActivity.java** et ajoutez hello après la classe de base pour hello tooreplace **MainActivity** trop**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Si votre classe de base n’est pas *activité*, consultez [avancé de Reporting Android](mobile-engagement-android-advanced-reporting.md) sur la manière de tooinherit à partir de différentes classes.
>
>

Commentaire hello ligne pour ce scénario d’exemple simple suivante :

    // setSupportActionBar(toolbar);

Si vous souhaitez tookeep hello `ActionBar` dans votre application, consultez [avancé de Reporting Android](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Activation des notifications push et de la messagerie in-app
Pendant une campagne, Mobile Engagement vous permet d’interagir avec vos utilisateurs à l’aide de notifications Push et de messages dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello suivant la section des tooreceive de votre application les définit.

### <a name="copy-sdk-resources-in-your-project"></a>Copier les ressources du SDK dans votre projet
1. Accédez tooyour arrière du téléchargement contenu et la copie du hello du Kit de développement logiciel **res** dossier.

    ![][10]
2. Revenir en arrière tooAndroid Studio, sélectionnez hello **principal** répertoire de vos fichiers projet, puis collez-la tooadd hello de ressources tooyour project.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Étapes suivantes
Accédez trop[du SDK Android](mobile-engagement-android-sdk-overview.md) tooget connaissance sur hello intégration du Kit de développement logiciel.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
