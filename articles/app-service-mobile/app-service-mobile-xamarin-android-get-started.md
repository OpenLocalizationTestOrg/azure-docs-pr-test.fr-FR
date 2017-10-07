---
title: "aaaGet démarré avec les applications mobiles Azure pour les applications de Xamarin.Android"
description: "Suivez ce didacticiel tooget démarré à l’aide des applications mobiles Azure pour le développement de Xamarin Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Création d'une application Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd un backend de cloud service tooa Xamarin.Android application. Pour plus d’informations, consultez [Que sont les applications Mobile Apps ?](app-service-mobile-value-prop.md).

Une capture d’écran à partir de l’application hello terminée est ci-dessous :

![][0]

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Mobile Apps pour les applications Xamarin.Android.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* Un compte Azure actif. Si vous n’avez pas un compte, inscrivez-vous à une version d’évaluation d’Azure et obtenir des applications mobiles libre de too10. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio avec Xamarin. Pour obtenir des instructions, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .

## <a name="create-an-azure-mobile-app-backend"></a>Créer un serveur principal d'applications mobiles Azure
Suivez ces étapes de toocreate un service principal de l’application Mobile.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles. Ensuite, télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Téléchargez et exécutez l’application de Xamarin.Android hello
1. Sous **télécharger et exécuter votre projet Xamarin.Android**, cliquez sur hello **télécharger** bouton.

      Enregistrer l’ordinateur local du tooyour fichier projet compressée hello et prenez note d’où vous l’enregistrez.
2. Hello de presse **F5** clé projet de hello toobuild et démarrer l’application hello.
3. Dans l’application hello, tapez un texte explicite, tel que *didacticiel de hello complète* puis cliquez sur hello **ajouter** bouton.

    ![][10]

    Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello. Éléments stockés dans la table de hello sont retournés par le serveur principal d’application mobile hello et les données apparaissent dans la liste de hello.

   > [!NOTE]
   > Vous pouvez examiner le code hello qui accède à votre tooquery de serveur principal d’application mobile et insérer des données, ce qui se trouve dans le fichier ToDoActivity.cs c# de hello.
   >
   >

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter une application de tooyour de synchronisation hors connexion](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Ajouter une application de tooyour d’authentification](app-service-mobile-xamarin-android-get-started-users.md)
* [Ajouter une application de Xamarin.Android de tooyour de notifications push](app-service-mobile-xamarin-android-get-started-push.md)
* [Comment toouse hello gérées client pour les applications mobiles Azure](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
