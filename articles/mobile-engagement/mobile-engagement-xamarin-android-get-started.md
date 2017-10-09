---
title: "aaaGet main d’Azure Mobile Engagement pour Xamarin.Android"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications de Xamarin.Android."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Prise en main d’Azure Mobile Engagement pour les applications Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Xamarin.Android.
Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement. À cette occasion, vous allez créer une application Xamarin.Android vide qui recueille des données de base et reçoit des notifications Push à l’aide de Google Cloud Messaging (GCM).

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ce didacticiel requiert hello qui suit :

* [Xamarin Studio](http://xamarin.com/studio). Vous pouvez également utiliser Visual Studio avec Xamarin, mais ce didacticiel utilise Xamarin Studio. Pour obtenir des instructions sur l’installation, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [Kit de développement logiciel (SDK) Mobile Engagement pour Xamarin](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push. 

Nous allons créer une application de base avec l’intégration de Xamarin Studio toodemonstrate hello.

### <a name="create-a-new-xamarinandroid-project"></a>Créer un projet Xamarin.Android
1. Lancez **Xamarin Studio** accédez trop**fichier** -> **nouveau** -> **Solution** 
   
    ![][1]
2. Sélectionnez **application Android** puis assurez-vous que la langue hello sélectionné est **c#** et cliquez sur **suivant**.
   
    ![][2]
3. Renseignez hello **nom de l’application** et hello **identifiant d’organisation**. Assurez-vous que toocheckmark **Services Google Play** puis cliquez sur **suivant**. 
   
    ![][3]
4. Hello de mise à jour **nom du projet**, **nom de la Solution** et **emplacement** si nécessaire et cliquez sur **créer**.
   
    ![][4]

Xamarin Studio créera une application hello dans lequel nous intégrera Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Cliquez avec le bouton droit sur hello **Packages** dossier dans windows de Solution hello et sélectionnez **ajouter des Packages en cours...**
   
    ![][5]
2. Recherchez hello **Microsoft Azure Mobile Engagement Xamarin SDK** et ajoutez-le tooyour solution.  
   
    ![][6]
3. Ouvrez **MainActivity.cs** et ajoutez hello qui suit à l’aide des instructions :
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. Bonjour `OnCreate` (méthode), ajouter hello après la connexion de hello tooinitialize avec le serveur principal Mobile Engagement. Assurez-vous que tooadd votre **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Ajouter des autorisations et une déclaration de service
1. Ouvrez hello **Manifest.xml** fichier sous le dossier Propriétés de hello. Sélectionnez l’onglet Source afin que la mise à jour source XML hello.
2. Ajoutez ces toohello autorisations Manifest.xml (qui peut être trouvé sous hello **propriétés** dossier) de votre projet immédiatement avant ou après hello `<application>` balise :
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Ajoutez suit hello entre hello `<application>` et `</application>` balises de service de l’agent toodeclare hello :
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. Dans le code hello vous venez de coller, remplacez `"<Your application name>"` dans l’étiquette de hello. Il est affiché dans hello **paramètres** menu dans lequel les utilisateurs peuvent voir les services qui s’exécutent sur le périphérique de hello. Vous pouvez ajouter le mot hello « Service » de cette étiquette par exemple.

### <a name="send-a-screen-toomobile-engagement"></a>Envoyer un tooMobile écran Engagement
Dans l’ordre toostart envoi de données et en garantissant hello utilisateurs sont actifs, vous devez envoyer au moins un écran toohello Mobile Engagement principal. Pour y parvenir-Vérifiez que hello `MainActivity` hérite `EngagementActivity` au lieu de `Activity`.

    public class MainActivity : EngagementActivity

Si vous ne pouvez pas hériter de `EngagementActivity`, vous devez alors ajouter les méthodes `.StartActivity` et `.EndActivity` respectivement dans `OnResume` et `OnPause`.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract avec et atteindre vos utilisateurs avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
les sections suivantes de Hello configure tooreceive de votre application les.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
