---
title: aaaCreate une plate-forme de Windows universelle (UWP) qui utilise des applications mobiles | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement d’applications de plateforme Windows universelle (UWP) en c#, Visual Basic ou JavaScript."
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
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="37bc3-103">Créer une application Windows</span><span class="sxs-lookup"><span data-stu-id="37bc3-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="37bc3-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="37bc3-104">Overview</span></span>
<span data-ttu-id="37bc3-105">Ce didacticiel vous montre comment tooadd un backend de cloud service application de plateforme Windows universelle (UWP) tooa.</span><span class="sxs-lookup"><span data-stu-id="37bc3-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="37bc3-106">Pour plus d’informations, consultez [Que sont les applications Mobile Apps ?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="37bc3-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="37bc3-107">Hello Voici les captures d’écran à partir de l’application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="37bc3-107">hello following are screen captures from hello completed app:</span></span>

![Application de bureau terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="37bc3-109">En cours d’exécution sur un ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="37bc3-109">Running on a desktop.</span></span>

![Application de téléphone terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="37bc3-111">En cours d’exécution sur un téléphone</span><span class="sxs-lookup"><span data-stu-id="37bc3-111">Running on a phone</span></span>

<span data-ttu-id="37bc3-112">Vous devez suivre ce didacticiel avant de pouvoir suivre les autres didacticiels Mobile App pour les applications UWP.</span><span class="sxs-lookup"><span data-stu-id="37bc3-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37bc3-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37bc3-113">Prerequisites</span></span>
<span data-ttu-id="37bc3-114">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="37bc3-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="37bc3-115">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="37bc3-115">An active Azure account.</span></span> <span data-ttu-id="37bc3-116">Si vous n’avez pas un compte, vous pouvez souscrire à la période d’évaluation d’Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="37bc3-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="37bc3-117">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37bc3-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="37bc3-118">[Visual Studio Community 2015] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="37bc3-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="37bc3-119">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="37bc3-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="37bc3-120">Suivez ces étapes de toocreate un serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="37bc3-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="37bc3-121">Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles.</span><span class="sxs-lookup"><span data-stu-id="37bc3-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="37bc3-122">Ensuite, vous allez télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="37bc3-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="37bc3-123">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="37bc3-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="37bc3-124">Téléchargez et exécutez le projet de client hello</span><span class="sxs-lookup"><span data-stu-id="37bc3-124">Download and run hello client project</span></span>
<span data-ttu-id="37bc3-125">Une fois que vous avez configuré votre serveur principal de l’application Mobile, vous pouvez créer une application cliente ou modifier un tooAzure de tooconnect application existante.</span><span class="sxs-lookup"><span data-stu-id="37bc3-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="37bc3-126">Dans cette section, vous téléchargez un projet de modèle d’application UWP est le principal de l’application Mobile tooyour tooconnect personnalisé.</span><span class="sxs-lookup"><span data-stu-id="37bc3-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="37bc3-127">Dans hello **démarrage rapide** panneau pour le service principal de votre application Mobile, cliquez sur **créer une application** > **télécharger**, puis extraire les fichiers de projet hello compressé ordinateur local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="37bc3-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Télécharger le projet de démarrage rapide Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="37bc3-129">(Facultatif) Ajouter toohello de projet application hello UWP même solution en tant que projet de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="37bc3-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="37bc3-130">Cela facilite la toodebug test à la fois hello principal d’application et hello dans hello même solution Visual Studio, si vous choisissez toodo ainsi.</span><span class="sxs-lookup"><span data-stu-id="37bc3-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="37bc3-131">tooadd une solution de toohello de projet application UWP, vous devez être à l’aide de Visual Studio 2015 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="37bc3-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="37bc3-132">Application de plateforme Windows universelle hello en tant que projet de démarrage hello, appuyez sur toodeploy de clé F5 hello et application hello d’exécution.</span><span class="sxs-lookup"><span data-stu-id="37bc3-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="37bc3-133">Dans l’application hello, tapez un texte explicite, tel que *didacticiel de hello complète*, Bonjour **Insert a TodoItem** zone de texte, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="37bc3-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Démarrage rapide Windows - Bureau terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="37bc3-135">Envoie un billet demande toohello application mobile serveur principal qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="37bc3-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="37bc3-136">(Facultatif) Arrêter l’application hello et redémarrer sur un autre appareil ou un émulateur mobile.</span><span class="sxs-lookup"><span data-stu-id="37bc3-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Démarrage rapide Windows - Téléphone terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="37bc3-138">Notez que les données enregistrées à partir de l’étape précédente de hello sont chargées à partir d’Azure après le démarrage de hello application UWP.</span><span class="sxs-lookup"><span data-stu-id="37bc3-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37bc3-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37bc3-139">Next steps</span></span>
* [<span data-ttu-id="37bc3-140">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="37bc3-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="37bc3-141">Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="37bc3-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="37bc3-142">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="37bc3-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="37bc3-143">Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.</span><span class="sxs-lookup"><span data-stu-id="37bc3-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="37bc3-144">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="37bc3-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="37bc3-145">Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="37bc3-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="37bc3-146">Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="37bc3-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
