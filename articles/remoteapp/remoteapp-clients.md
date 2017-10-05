---
title: "Accès à vos applications à partir de n’importe quel appareil | Microsoft Docs"
description: "Découvrez quels clients sont pris en charge pour Azure RemoteApp et comment accéder à vos applications."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="ab487-103">Accès à vos applications dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ab487-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ab487-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="ab487-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ab487-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="ab487-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ab487-106">L'un des intérêts de RemoteApp repose sur le fait que vous pouvez accéder à des applications à partir de l'un de vos appareils.</span><span class="sxs-lookup"><span data-stu-id="ab487-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="ab487-107">Mieux encore, vous pouvez commencer à travailler sur un appareil, puis passer sur un autre et reprendre exactement là où vous vous étiez arrêté.</span><span class="sxs-lookup"><span data-stu-id="ab487-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="ab487-108">Pour commencer, vous devez télécharger le client adapté à votre appareil et vous connecter au service.</span><span class="sxs-lookup"><span data-stu-id="ab487-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="ab487-109">Dans cette rubrique, nous allons passer en revue les clients actuellement pris en charge et les modes de téléchargement, avant de découvrir comment vous connecter à RemoteApp à partir de chacun de ces clients.</span><span class="sxs-lookup"><span data-stu-id="ab487-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="ab487-110">Clients pris en charge</span><span class="sxs-lookup"><span data-stu-id="ab487-110">Supported clients</span></span>
<span data-ttu-id="ab487-111">Vous pouvez accéder à RemoteApp en suivant la procédure mentionnée ci-dessous si votre appareil exécute l'un des systèmes d'exploitation suivants :</span><span class="sxs-lookup"><span data-stu-id="ab487-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="ab487-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ab487-112">Windows 10</span></span> 
* <span data-ttu-id="ab487-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ab487-113">Windows 8.1</span></span>
* <span data-ttu-id="ab487-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ab487-114">Windows 8</span></span>
* <span data-ttu-id="ab487-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="ab487-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="ab487-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ab487-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="ab487-117">iOS</span><span class="sxs-lookup"><span data-stu-id="ab487-117">iOS</span></span>
* <span data-ttu-id="ab487-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ab487-118">Mac OS X</span></span>
* <span data-ttu-id="ab487-119">Android</span><span class="sxs-lookup"><span data-stu-id="ab487-119">Android</span></span>

 <span data-ttu-id="ab487-120">Qu'en est-il des clients légers ?</span><span class="sxs-lookup"><span data-stu-id="ab487-120">What about thin clients?</span></span> <span data-ttu-id="ab487-121">Les clients légers Windows Embedded suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="ab487-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="ab487-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="ab487-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="ab487-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="ab487-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="ab487-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="ab487-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="ab487-125">Windows 10 IoT Entreprise</span><span class="sxs-lookup"><span data-stu-id="ab487-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="ab487-126">Téléchargement du client</span><span class="sxs-lookup"><span data-stu-id="ab487-126">Downloading the client</span></span>
<span data-ttu-id="ab487-127">Quelle que soit la plateforme utilisée, le client dont vous avez besoin pour accéder à RemoteApp est disponible dans la page de [Téléchargement du client Bureau à distance](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ab487-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="ab487-128">Si vous cliquez sur les différents liens, vous commencez directement le téléchargement du client ou vous accédez à la page de téléchargement du client dans le magasin d'applications de cette plateforme.</span><span class="sxs-lookup"><span data-stu-id="ab487-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="ab487-129">Installez le client en suivant les instructions qui s'affichent à l'écran.</span><span class="sxs-lookup"><span data-stu-id="ab487-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="ab487-130">Après avoir installé le client sur votre appareil et l'avoir lancé, passez à la section appropriée ci-dessous pour savoir comment vous connecter à RemoteApp à partir de ce client.</span><span class="sxs-lookup"><span data-stu-id="ab487-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="ab487-131">Android</span><span class="sxs-lookup"><span data-stu-id="ab487-131">Android</span></span>
<span data-ttu-id="ab487-132">Une fois l'application Bureau à distance Microsoft installée à partir du Google Play Store, elle apparaît dans votre liste d'applications sous **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ab487-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ab487-133">Lorsque vous lancez l'application, vous accédez à un centre de connexion vide, sauf si vous avez déjà utilisé l'application.</span><span class="sxs-lookup"><span data-stu-id="ab487-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ab487-134">Pour prendre en main Azure RemoteApp, cliquez sur le bouton d'ajout **""+""**, puis sur **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ab487-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centre de connexion vide](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="ab487-136">Vous devez vous connecter avec votre adresse de messagerie pour accéder au service.</span><span class="sxs-lookup"><span data-stu-id="ab487-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="ab487-137">Appuyez sur **Prise en main**.</span><span class="sxs-lookup"><span data-stu-id="ab487-137">Tap **Get started**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="ab487-139">Dans la page suivante, tapez votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ab487-140">Le processus de connexion à l'aide d'Azure Active Directory commence alors.</span><span class="sxs-lookup"><span data-stu-id="ab487-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="ab487-142">Suivez les instructions qui s'affichent à l'écran pour vous connecter avec votre compte Microsoft (précédemment appelé « LiveID ») ou votre ID d'organisation.</span><span class="sxs-lookup"><span data-stu-id="ab487-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="ab487-143">Une fois que vous êtes connecté, une page répertoriant toutes les invitations que vous avez reçues peut s'afficher.</span><span class="sxs-lookup"><span data-stu-id="ab487-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ab487-144">Le cas échéant, sélectionnez les invitations que vous jugez fiables, puis cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ab487-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![Page des invitations](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="ab487-146">Une fois vos invitations acceptées, la liste des applications auxquelles vous avez accès est téléchargée sur votre appareil et devient disponible dans le centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ab487-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ab487-147">Cliquez sur l'une des applications pour la lancer et commencer à l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ab487-147">Tap one of the apps to start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="ab487-149">Si vous n'avez pas encore d'invitation, vous pouvez tout de même essayer le service.</span><span class="sxs-lookup"><span data-stu-id="ab487-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ab487-150">Pour ce faire, cliquez sur **Accéder à un essai gratuit** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ab487-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="ab487-152">Cela vous permet d'accéder à un ensemble d'applications de base qui vous permettent de commencer à utiliser RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ab487-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="ab487-154">iOS</span><span class="sxs-lookup"><span data-stu-id="ab487-154">iOS</span></span>
<span data-ttu-id="ab487-155">Une fois l'application Bureau à distance Microsoft installée à partir du magasin d'applications, elle apparaît dans votre liste d'applications sous **Client Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ab487-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="ab487-156">Lorsque vous lancez l'application, vous accédez à un centre de connexion vide, sauf si vous avez déjà utilisé l'application.</span><span class="sxs-lookup"><span data-stu-id="ab487-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ab487-157">Pour prendre en main Azure RemoteApp, cliquez sur le bouton **""+""**, puis sur **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ab487-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="ab487-159">Vous devez vous connecter avec votre adresse de messagerie pour accéder au service. Pour démarrer ce processus, tapez votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="ab487-161">Suivez les instructions qui s'affichent à l'écran pour vous connecter avec votre compte Microsoft (LiveID) ou votre ID d'organisation.</span><span class="sxs-lookup"><span data-stu-id="ab487-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ab487-162">Une fois que vous êtes connecté, une page répertoriant toutes les invitations que vous avez reçues peut s'afficher.</span><span class="sxs-lookup"><span data-stu-id="ab487-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ab487-163">Le cas échéant, sélectionnez les invitations que vous jugez fiables, puis cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ab487-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="ab487-165">Une fois vos invitations acceptées, la liste des applications auxquelles vous avez accès est téléchargée sur votre appareil et devient disponible dans le centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ab487-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ab487-166">Cliquez sur l'une des applications pour la lancer et commencer à l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ab487-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="ab487-168">Si vous n'avez pas encore d'invitation, vous pouvez tout de même essayer le service.</span><span class="sxs-lookup"><span data-stu-id="ab487-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ab487-169">Pour ce faire, cliquez sur **Accéder à un essai gratuit** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ab487-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="ab487-171">Cela vous permet d'accéder à un ensemble d'applications de base qui vous permettent de commencer à utiliser RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ab487-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="ab487-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ab487-173">Mac OS X</span></span>
<span data-ttu-id="ab487-174">Une fois l'application Bureau à distance Microsoft installée à partir du magasin d'applications, elle apparaît dans votre liste d'applications sous **Bureau à distance Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ab487-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="ab487-175">Lorsque vous lancez l'application, vous accédez à un centre de connexion vide, sauf si vous avez déjà utilisé l'application.</span><span class="sxs-lookup"><span data-stu-id="ab487-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ab487-176">Pour commencer à utiliser Azure RemoteApp, cliquez sur le bouton **Azure RemoteApp** .</span><span class="sxs-lookup"><span data-stu-id="ab487-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="ab487-178">Vous devez vous connecter avec votre adresse de messagerie pour accéder au service. Pour démarrer ce processus, cliquez sur **Prendre en main**.</span><span class="sxs-lookup"><span data-stu-id="ab487-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="ab487-180">Dans la page suivante, tapez votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ab487-181">Le processus de connexion à l'aide d'Azure Active Directory commence alors.</span><span class="sxs-lookup"><span data-stu-id="ab487-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="ab487-183">Suivez les instructions qui s'affichent à l'écran pour vous connecter avec votre compte Microsoft (LiveID) ou votre ID d'organisation.</span><span class="sxs-lookup"><span data-stu-id="ab487-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ab487-184">Une fois que vous êtes connecté, une page répertoriant toutes les invitations que vous avez reçues peut s'afficher.</span><span class="sxs-lookup"><span data-stu-id="ab487-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ab487-185">Le cas échéant, sélectionnez les invitations que vous jugez fiables, puis fermez la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ab487-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="ab487-187">Une fois vos invitations acceptées, la liste des applications auxquelles vous avez accès est téléchargée sur votre appareil et devient disponible dans le centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ab487-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ab487-188">Double-cliquez sur l'une des applications pour la lancer et commencer à l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ab487-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="ab487-190">Si vous n'avez pas encore d'invitation, vous pouvez tout de même essayer le service.</span><span class="sxs-lookup"><span data-stu-id="ab487-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ab487-191">Pour ce faire, cliquez sur **Accéder à un essai gratuit** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ab487-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="ab487-193">Cela vous permet d'accéder à un ensemble d'applications de base qui vous permettent de commencer à utiliser RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ab487-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="ab487-195">Windows (Toutes les versions prises en charge sauf Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="ab487-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="ab487-196">Le client se lance automatiquement une fois son installation terminée. Cependant, pour y accéder à nouveau ultérieurement, vous le trouverez dans votre liste d'applications sous le nom **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ab487-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="ab487-197">Une fois le client lancé, la première page qui s'affiche vous souhaite la bienvenue dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ab487-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="ab487-198">Pour continuer, cliquez sur **Prise en main**.</span><span class="sxs-lookup"><span data-stu-id="ab487-198">To proceed, click on **Get Started**.</span></span>
   
    ![Page d'accueil du client Azure RemoteApp](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="ab487-200">La page suivante commence le processus de connexion pour Azure RemoteApp à l'aide d'Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab487-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="ab487-201">Ce processus vous semblera familier si vous avez déjà utilisé des services Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ab487-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="ab487-202">Commencez par taper votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Invite de la première page Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="ab487-204">Suivez les instructions qui s'affichent à l'écran pour vous connecter avec votre compte Microsoft (LiveID) ou votre ID d'organisation.</span><span class="sxs-lookup"><span data-stu-id="ab487-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ab487-205">Une fois que vous êtes connecté, une page répertoriant toutes les invitations que vous avez reçues peut s'afficher.</span><span class="sxs-lookup"><span data-stu-id="ab487-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ab487-206">Le cas échéant, sélectionnez les invitations que vous jugez fiables, puis cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ab487-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Page des invitations du client Azure RemoteApp](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="ab487-208">Une fois vos invitations acceptées, la liste des applications auxquelles vous avez accès est téléchargée sur votre appareil et devient disponible dans le centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ab487-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ab487-209">Double-cliquez sur l'une des applications pour la lancer et commencer à l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ab487-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centre de connexion du client Azure RemoteApp](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="ab487-211">Si personne ne vous a encore envoyé d'invitation, ne vous inquiétez pas : nous avons paré à cette éventualité !</span><span class="sxs-lookup"><span data-stu-id="ab487-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="ab487-212">Vous avez tout de même accès à une collection de démonstration afin de pouvoir tester le service.</span><span class="sxs-lookup"><span data-stu-id="ab487-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="ab487-214">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ab487-214">Windows Phone 8.1</span></span>
<span data-ttu-id="ab487-215">Une fois l'application Bureau à distance Microsoft installée à partir du magasin Windows Phone 8.1, elle apparaît dans votre liste d'applications sous **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ab487-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ab487-216">Lorsque vous lancez l'application, vous accédez directement à un centre de connexion vide, sauf si vous avez déjà utilisé l'application.</span><span class="sxs-lookup"><span data-stu-id="ab487-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ab487-217">Pour prendre en main Azure RemoteApp, cliquez sur le bouton d'ajout **""+""** situé en bas de l'écran.</span><span class="sxs-lookup"><span data-stu-id="ab487-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="ab487-219">Appuyez ensuite sur **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ab487-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Page Ajouter des éléments](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="ab487-221">Vous devez vous connecter avec votre adresse de messagerie pour accéder au service. Pour démarrer ce processus, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ab487-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="ab487-223">Dans la page suivante, tapez votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ab487-224">Le processus de connexion à l'aide d'Azure Active Directory commence alors.</span><span class="sxs-lookup"><span data-stu-id="ab487-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="ab487-226">Suivez les instructions qui s'affichent à l'écran pour vous connecter avec votre compte Microsoft (LiveID) ou votre ID d'organisation.</span><span class="sxs-lookup"><span data-stu-id="ab487-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ab487-227">Une fois que vous êtes connecté, une page répertoriant toutes les invitations que vous avez reçues peut s'afficher.</span><span class="sxs-lookup"><span data-stu-id="ab487-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ab487-228">Le cas échéant, sélectionnez les invitations que vous jugez fiables, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ab487-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="ab487-230">Une fois vos invitations acceptées, la liste des applications auxquelles vous avez accès est téléchargée sur votre appareil et devient disponible dans le centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ab487-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ab487-231">Cliquez sur l'une des applications pour la lancer et commencer à l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ab487-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="ab487-233">Si vous n'avez pas encore d'invitation, vous pouvez tout de même essayer le service.</span><span class="sxs-lookup"><span data-stu-id="ab487-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ab487-234">Pour ce faire, cliquez sur **Oui** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ab487-234">To do so, tap **yes** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="ab487-236">Cela vous permet d'accéder à un ensemble d'applications de base qui vous permettent de commencer à utiliser RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ab487-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

