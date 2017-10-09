---
title: "aaaGet main d’Azure App Service Mobile Apps pour les applications de Xamarin.iOS | Documents Microsoft"
description: "Suivez ce didacticiel tooget main à l’aide des applications mobiles pour le développement de Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Création d’une application Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd un backend de cloud service application mobile de tooa Xamarin.iOS à l’aide d’un serveur principal d’application mobile Azure.  Vous allez créer un serveur principal d’application mobile et une simple application Xamarin.iOS *Todo list* qui stocke les données d’application dans Azure.

Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels de Xamarin.iOS sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* Un compte Azure actif. Si vous n’avez pas un compte, inscrivez-vous pour un essai Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio avec Xamarin. Pour obtenir des instructions, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .
* Un Mac sur lequel sont installés Xcode v7.0 ou version ultérieure et Xamarin Studio Community. Consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) et [Configuration, installation et vérifications pour les utilisateurs de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Créer un serveur principal d'applications mobiles Azure
Suivez ces étapes de toocreate un service principal de l’application Mobile.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello
Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles. Ensuite, télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.

Suivez hello suivant les étapes tooconfigure hello serveur projet toouse soit back-end hello Node.js ou .NET.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Téléchargez et exécutez l’application de Xamarin.iOS hello
1. Ouvrez hello [portail Azure] dans une fenêtre de navigateur.
2. Dans le panneau des paramètres hello pour votre application Mobile, cliquez sur **prise en main** > **Xamarin.iOS**. À l’Étape 3, cliquez sur **Create a new app** si cette option n’est pas déjà sélectionnée.  Cliquez ensuite sur hello **télécharger** bouton.

      Une application cliente qui se connecte le service principal mobile de tooyour est téléchargée. Enregistrer le fichier de projet compressée de hello sur votre ordinateur local et prenez note d’où vous l’enregistrez.
3. Extraire le projet hello que vous avez téléchargé, puis ouvrez-le dans Xamarin Studio (ou Visual Studio).

    ![][9]

    ![][8]
4. Appuyez sur le projet de hello F5 toobuild clé hello et démarrer l’application hello dans l’émulateur d’iPhone hello.
5. Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, puis cliquez sur hello  **+**  bouton.

    ![][10]

    Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello. Éléments stockés dans la table de hello sont retournés par le serveur principal d’application mobile hello et les données sont affichées dans la liste de hello.

> [!NOTE]
> Vous pouvez examiner le code hello qui accède à votre tooquery de serveur principal d’application mobile et insérer des données dans le fichier QSTodoService.cs c# de hello.
>
>

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter une application de tooyour de synchronisation hors connexion](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Ajouter une application de tooyour d’authentification](app-service-mobile-xamarin-ios-get-started-users.md)
* [Ajouter une application de Xamarin.Android de tooyour de notifications push](app-service-mobile-xamarin-ios-get-started-push.md)
* [Comment toouse hello gérées client pour les applications mobiles Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portail Azure]: https://portal.azure.com/
