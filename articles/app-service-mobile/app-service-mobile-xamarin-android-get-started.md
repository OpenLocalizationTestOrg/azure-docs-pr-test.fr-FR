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
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="59b89-103">Création d'une application Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="59b89-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="59b89-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="59b89-104">Overview</span></span>
<span data-ttu-id="59b89-105">Ce didacticiel vous montre comment tooadd un backend de cloud service tooa Xamarin.Android application.</span><span class="sxs-lookup"><span data-stu-id="59b89-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="59b89-106">Pour plus d’informations, consultez [Que sont les applications Mobile Apps ?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="59b89-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="59b89-107">Une capture d’écran à partir de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="59b89-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="59b89-108">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Mobile Apps pour les applications Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="59b89-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59b89-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="59b89-109">Prerequisites</span></span>
<span data-ttu-id="59b89-110">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="59b89-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="59b89-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="59b89-111">An active Azure account.</span></span> <span data-ttu-id="59b89-112">Si vous n’avez pas un compte, inscrivez-vous à une version d’évaluation d’Azure et obtenir des applications mobiles libre de too10.</span><span class="sxs-lookup"><span data-stu-id="59b89-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="59b89-113">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59b89-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="59b89-114">Visual Studio avec Xamarin.</span><span class="sxs-lookup"><span data-stu-id="59b89-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="59b89-115">Pour obtenir des instructions, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="59b89-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="59b89-116">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="59b89-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="59b89-117">Suivez ces étapes de toocreate un service principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="59b89-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="59b89-118">Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles.</span><span class="sxs-lookup"><span data-stu-id="59b89-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="59b89-119">Ensuite, télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59b89-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="59b89-120">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="59b89-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="59b89-121">Téléchargez et exécutez l’application de Xamarin.Android hello</span><span class="sxs-lookup"><span data-stu-id="59b89-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="59b89-122">Sous **télécharger et exécuter votre projet Xamarin.Android**, cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="59b89-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="59b89-123">Enregistrer l’ordinateur local du tooyour fichier projet compressée hello et prenez note d’où vous l’enregistrez.</span><span class="sxs-lookup"><span data-stu-id="59b89-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="59b89-124">Hello de presse **F5** clé projet de hello toobuild et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="59b89-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="59b89-125">Dans l’application hello, tapez un texte explicite, tel que *didacticiel de hello complète* puis cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="59b89-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="59b89-126">Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="59b89-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="59b89-127">Éléments stockés dans la table de hello sont retournés par le serveur principal d’application mobile hello et les données apparaissent dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="59b89-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="59b89-128">Vous pouvez examiner le code hello qui accède à votre tooquery de serveur principal d’application mobile et insérer des données, ce qui se trouve dans le fichier ToDoActivity.cs c# de hello.</span><span class="sxs-lookup"><span data-stu-id="59b89-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="59b89-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59b89-129">Next steps</span></span>
* [<span data-ttu-id="59b89-130">Ajouter une application de tooyour de synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="59b89-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="59b89-131">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="59b89-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="59b89-132">Ajouter une application de Xamarin.Android de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="59b89-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="59b89-133">Comment toouse hello gérées client pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="59b89-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
