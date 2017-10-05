---
title: "Créer une plateforme Windows universelle sur Mobile Apps| Microsoft Docs"
description: "Suivez ce didacticiel pour commencer à utiliser des services principaux d’applications mobiles Azure pour le développement d’applications UWP en C#, Visual Basic ou JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="7d7e9-103">Créer une application Windows</span><span class="sxs-lookup"><span data-stu-id="7d7e9-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7d7e9-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7d7e9-104">Overview</span></span>
<span data-ttu-id="7d7e9-105">Ce didacticiel présente l’ajout d’un service principal cloud à une application de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="7d7e9-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="7d7e9-106">Pour plus d’informations, consultez [Que sont les applications Mobile Apps ?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="7d7e9-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="7d7e9-107">Voici les captures d’écran générées à partir de l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="7d7e9-107">The following are screen captures from the completed app:</span></span>

![Application de bureau terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="7d7e9-109">En cours d’exécution sur un ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-109">Running on a desktop.</span></span>

![Application de téléphone terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="7d7e9-111">En cours d’exécution sur un téléphone</span><span class="sxs-lookup"><span data-stu-id="7d7e9-111">Running on a phone</span></span>

<span data-ttu-id="7d7e9-112">Vous devez suivre ce didacticiel avant de pouvoir suivre les autres didacticiels Mobile App pour les applications UWP.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7e9-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d7e9-113">Prerequisites</span></span>
<span data-ttu-id="7d7e9-114">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7d7e9-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="7d7e9-115">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-115">An active Azure account.</span></span> <span data-ttu-id="7d7e9-116">Si vous n'avez pas de compte, vous pouvez vous inscrire pour une évaluation d'Azure et obtenir jusqu'à 10 applications mobiles gratuites que vous pourrez conserver après l'expiration de votre période d'évaluation.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="7d7e9-117">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d7e9-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7d7e9-118">[Visual Studio Community 2015] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="7d7e9-119">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="7d7e9-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="7d7e9-120">Suivez ces étapes pour créer un serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="7d7e9-121">Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="7d7e9-122">Vous allez ensuite télécharger un projet de serveur pour un serveur principal « todo list » simple et le publier dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="7d7e9-123">Configurer le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="7d7e9-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="7d7e9-124">Télécharger et exécuter le projet client</span><span class="sxs-lookup"><span data-stu-id="7d7e9-124">Download and run the client project</span></span>
<span data-ttu-id="7d7e9-125">Une fois que vous avez configuré le serveur principal de votre application Mobile App, vous pouvez créer une application cliente ou modifier une application existante pour se connecter à Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="7d7e9-126">Dans cette section, vous téléchargez un projet de modèle d’application UWP, personnalisé pour se connecter à votre serveur principal Mobile App.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="7d7e9-127">De retour dans le panneau **Démarrage rapide** pour votre serveur principal Mobile App, cliquez sur **Créer une application** > **Télécharger**, puis extrayez les fichiers de projet compressés sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Télécharger le projet de démarrage rapide Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="7d7e9-129">(Facultatif) Ajoutez le projet d’application UWP à la solution avec le projet de serveur.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="7d7e9-130">Cela rend plus facile le débogage et les tests de l'application et du backend dans la même solution Visual Studio, si vous choisissez de le faire.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="7d7e9-131">Pour ajouter un projet d’application UWP à la solution, vous devez utiliser Visual Studio 2015 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="7d7e9-132">Avec l’application UWP comme projet de démarrage, appuyez sur la touche F5 pour déployer et exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="7d7e9-133">Dans l’application, tapez un texte explicite, comme *Suivre le didacticiel*, dans la zone de texte **Insérer un TodoItem**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Démarrage rapide Windows - Bureau terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="7d7e9-135">Ceci envoie une demande POST vers le nouveau backend d'application mobile qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="7d7e9-136">(Facultatif) Arrêtez l’application et redémarrez-la sur un autre périphérique ou un émulateur mobile.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Démarrage rapide Windows - Téléphone terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="7d7e9-138">Notez que les données enregistrées à l’étape précédente sont chargées à partir d’Azure après le démarrage de l’application UWP.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d7e9-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d7e9-139">Next steps</span></span>
* [<span data-ttu-id="7d7e9-140">Ajout de l’authentification à votre application</span><span class="sxs-lookup"><span data-stu-id="7d7e9-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="7d7e9-141">Découvrez comment authentifier les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="7d7e9-142">Ajouter des notifications Push à votre application</span><span class="sxs-lookup"><span data-stu-id="7d7e9-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="7d7e9-143">Apprenez à ajouter la prise en charge des notifications Push à votre application et à configurer le serveur principal d’applications mobiles pour utiliser Azure Notification Hubs afin d’envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="7d7e9-144">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="7d7e9-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="7d7e9-145">Apprenez à ajouter une prise en charge hors connexion à votre application à l’aide d’un backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="7d7e9-146">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="7d7e9-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="7d7e9-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="7d7e9-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
