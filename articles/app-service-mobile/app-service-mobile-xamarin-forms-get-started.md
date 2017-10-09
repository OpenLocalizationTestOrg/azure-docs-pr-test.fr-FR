---
title: "aaaGet démarrée avec des applications mobiles à l’aide de Xamarin.Forms"
description: "Suivez ce didacticiel toostart à l’aide des applications mobiles pour le développement de Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Créer une application Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment une application mobile principaux services de cloud computing tooa Xamarin.Forms à l’aide de tooadd hello fonctionnalité des applications mobiles de Service d’applications Azure en tant que serveur principal de hello. Vous allez créer un serveur principal d’applications mobiles et une simple application Xamarin.Forms de liste de tâches qui stocke les données d’application dans Azure.

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Mobile Apps pour les applications Xamarin.Forms.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous n’avez pas un compte, vous pouvez souscrire à la période d’évaluation d’Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio avec Xamarin. Pour plus d’informations, consultez hello [définir configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.

* Un Mac sur lequel sont installés Xcode v7.0 ou version ultérieure et Xamarin Studio Community. Pour plus d’informations, consultez les articles [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) et [Configurer, installer et vérifier pour les utilisateurs de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Créer un back end Mobile Apps

toocreate mettre fin à un nouveau Mobile Apps précédent, procédez comme hello suivant :

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Vous avez maintenant configuré un back end Mobile Apps que vos applications client mobiles peuvent utiliser. Ensuite, télécharger un projet de serveur pour des tâches simples liste principale et publiez-le tooAzure.

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello

toouse de project server tooconfigure hello hello back-end Node.js ou .NET, hello suivant :

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Téléchargez et exécutez la solution de Xamarin.Forms hello

Vous pouvez télécharger la solution hello de deux manières. Téléchargez-le tooa Mac et ouvrez-le dans Xamarin Studio, ou téléchargez-le tooa l’ordinateur Windows et ouvrez-le dans Visual Studio à l’aide d’un Mac en réseau pour la création d’application iOS de hello. Pour plus d’informations, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).

Sur un ordinateur Mac ou Windows, hello suivant :

1. Accédez toohello [portail Azure].

2. Sur hello **paramètres** panneau pour votre application mobile, sous **Mobile**, sélectionnez **prise en main** > **Xamarin.Forms**. À l’**étape 3**, sélectionnez **Créer une application**, puis sélectionnez **Télécharger**.

   Cette action télécharge un projet qui contient une application cliente qui est connecté tooyour des applications mobiles. Enregistrer l’ordinateur local du tooyour fichier projet compressée hello et prenez note d’où vous l’enregistrez.

3. Extraire le projet hello que vous avez téléchargé, puis ouvrez-le dans Visual Studio (Windows) ou de Xamarin Studio (Mac).

   ![Projet extrait dans Xamarin Studio][9]

   ![Projet extrait dans Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Facultatif) Exécutez le projet iOS de hello
Dans cette section, vous exécutez projet d’iOS Xamarin hello pour les appareils iOS. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.

#### <a name="in-xamarin-studio"></a>Dans Xamarin Studio
1. Projet d’iOS hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.

2. Sur hello **exécuter** menu, sélectionnez **démarrer le débogage** toobuild hello du projet et démarrer l’application hello dans l’émulateur d’iPhone hello.

#### <a name="in-visual-studio"></a>Dans Visual Studio
1. Projet d’iOS hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.

2. Sur hello **générer** menu, sélectionnez **Configuration Manager**.

3. Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** projet iOS toohello suivant de cases à cocher.

4. toobuild hello du projet et démarrer l’application hello dans l’émulateur de hello iPhone, sélectionnez hello **F5** clé.

   > [!NOTE]
   > Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello. Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.    
   >
   >

5. Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).

    ![][10]

    Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure. Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello. Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.

    > [!NOTE]
    > Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Facultatif) Exécutez le projet Android de hello
Dans cette section, vous exécutez le projet de droid Xamarin hello pour Android. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.

#### <a name="in-xamarin-studio"></a>Dans Xamarin Studio

1. Les projets Android hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.

2. toobuild hello du projet et démarrer l’application hello dans un émulateur Android, sur hello **exécuter** menu, sélectionnez **démarrer le débogage**.

#### <a name="in-visual-studio"></a>Dans Visual Studio

1. Projet Android (Droid) de hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.

2. Sur hello **générer** menu, sélectionnez **Configuration Manager**.

3. Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** prochain projet de Android toohello cases à cocher.

4. toobuild hello du projet et démarrer l’application hello dans un émulateur Android, sélectionnez hello **F5** clé.

   > [!NOTE]
   > Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello. Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.    
   >
   >

5. Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).

    ![][11]
    
    Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure. Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello. Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.
    
    > [!NOTE]
    > Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Facultatif) Exécutez le projet d’application Windows hello

Dans cette section, vous exécutez hello projet Xamarin WinApp pour les appareils Windows. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.

#### <a name="in-visual-studio"></a>Dans Visual Studio

1. Cliquez sur un des projets d’application Windows hello et sélectionnez **définir comme projet de démarrage**.

2. Sur hello **générer** menu, sélectionnez **Configuration Manager**.

3. Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** cases à cocher prochain toohello Windows projet que vous avez choisi.

4. toobuild hello du projet et démarrer l’application hello dans un émulateur de Windows, sélectionnez hello **F5** clé.

   > [!NOTE]
   > Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello. Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.    
   >
   >

5. Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).

    Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure. Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello. Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.
    
    ![][12]
    
    > [!NOTE]
    > Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.
    >
    >

## <a name="next-steps"></a>Étapes suivantes

* [Ajouter une application de tooyour d’authentification](app-service-mobile-xamarin-forms-get-started-users.md)  
  Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.

* [Ajouter une application de tooyour de notifications push](app-service-mobile-xamarin-forms-get-started-push.md)  
  Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer vos applications mobiles back-end toouse Azure Notification Hubs toosend hello des notifications push.

* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Découvrez comment tooadd la prise en charge en mode hors connexion pour votre application à l’aide d’un Mobile Apps back-end. La synchronisation hors connexion permet d’afficher, d’ajouter ou de modifier les données d’une application mobile même en l’absence de connexion au réseau.

* [Utiliser les clients gérés hello pour les applications mobiles](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Découvrez comment toowork avec hello gérées client SDK dans votre application Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portail Azure]: https://portal.azure.com/
