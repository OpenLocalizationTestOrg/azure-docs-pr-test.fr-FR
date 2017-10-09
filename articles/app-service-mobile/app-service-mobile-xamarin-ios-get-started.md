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
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="d038b-103">Création d’une application Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d038b-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d038b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d038b-104">Overview</span></span>
<span data-ttu-id="d038b-105">Ce didacticiel vous montre comment tooadd un backend de cloud service application mobile de tooa Xamarin.iOS à l’aide d’un serveur principal d’application mobile Azure.</span><span class="sxs-lookup"><span data-stu-id="d038b-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="d038b-106">Vous allez créer un serveur principal d’application mobile et une simple application Xamarin.iOS *Todo list* qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d038b-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="d038b-107">Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels de Xamarin.iOS sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d038b-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d038b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d038b-108">Prerequisites</span></span>
<span data-ttu-id="d038b-109">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="d038b-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="d038b-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d038b-110">An active Azure account.</span></span> <span data-ttu-id="d038b-111">Si vous n’avez pas un compte, inscrivez-vous pour un essai Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="d038b-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="d038b-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d038b-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d038b-113">Visual Studio avec Xamarin.</span><span class="sxs-lookup"><span data-stu-id="d038b-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="d038b-114">Pour obtenir des instructions, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d038b-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="d038b-115">Un Mac sur lequel sont installés Xcode v7.0 ou version ultérieure et Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="d038b-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="d038b-116">Consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) et [Configuration, installation et vérifications pour les utilisateurs de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="d038b-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="d038b-117">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="d038b-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="d038b-118">Suivez ces étapes de toocreate un service principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="d038b-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="d038b-119">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="d038b-119">Configure hello server project</span></span>
<span data-ttu-id="d038b-120">Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles.</span><span class="sxs-lookup"><span data-stu-id="d038b-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="d038b-121">Ensuite, télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d038b-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="d038b-122">Suivez hello suivant les étapes tooconfigure hello serveur projet toouse soit back-end hello Node.js ou .NET.</span><span class="sxs-lookup"><span data-stu-id="d038b-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="d038b-123">Téléchargez et exécutez l’application de Xamarin.iOS hello</span><span class="sxs-lookup"><span data-stu-id="d038b-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="d038b-124">Ouvrez hello [portail Azure] dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="d038b-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="d038b-125">Dans le panneau des paramètres hello pour votre application Mobile, cliquez sur **prise en main** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="d038b-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="d038b-126">À l’Étape 3, cliquez sur **Create a new app** si cette option n’est pas déjà sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d038b-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="d038b-127">Cliquez ensuite sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="d038b-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="d038b-128">Une application cliente qui se connecte le service principal mobile de tooyour est téléchargée.</span><span class="sxs-lookup"><span data-stu-id="d038b-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="d038b-129">Enregistrer le fichier de projet compressée de hello sur votre ordinateur local et prenez note d’où vous l’enregistrez.</span><span class="sxs-lookup"><span data-stu-id="d038b-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="d038b-130">Extraire le projet hello que vous avez téléchargé, puis ouvrez-le dans Xamarin Studio (ou Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d038b-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="d038b-131">Appuyez sur le projet de hello F5 toobuild clé hello et démarrer l’application hello dans l’émulateur d’iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="d038b-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="d038b-132">Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, puis cliquez sur hello  **+**  bouton.</span><span class="sxs-lookup"><span data-stu-id="d038b-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="d038b-133">Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="d038b-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="d038b-134">Éléments stockés dans la table de hello sont retournés par le serveur principal d’application mobile hello et les données sont affichées dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="d038b-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="d038b-135">Vous pouvez examiner le code hello qui accède à votre tooquery de serveur principal d’application mobile et insérer des données dans le fichier QSTodoService.cs c# de hello.</span><span class="sxs-lookup"><span data-stu-id="d038b-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d038b-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d038b-136">Next steps</span></span>
* [<span data-ttu-id="d038b-137">Ajouter une application de tooyour de synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="d038b-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="d038b-138">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="d038b-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="d038b-139">Ajouter une application de Xamarin.Android de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="d038b-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="d038b-140">Comment toouse hello gérées client pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="d038b-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
