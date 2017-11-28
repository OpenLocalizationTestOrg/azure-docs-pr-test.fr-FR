---
title: "aaaAccessing vos applications à partir de n’importe quel appareil | Documents Microsoft"
description: "Découvrez quels clients sont pris en charge pour Azure RemoteApp et comment tooaccess vos applications."
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
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="ef9ed-103">Accès à vos applications dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ef9ed-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef9ed-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ef9ed-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ef9ed-106">Une des beautés hello d’Azure RemoteApp est que vous pouvez accéder à des applications à partir d’un de vos périphériques.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="ef9ed-107">Mieux encore, vous pouvez commencer à travailler sur un appareil et ensuite une transition transparente tooa deuxième appareil et reprendre là où vous l’avez laissé.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="ef9ed-108">tooget a démarré, vous devez client de toodownload hello approprié pour votre appareil et connectez-vous au service de toohello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="ef9ed-109">Dans cette rubrique, nous verrons clients hello actuellement pris en charge et comment toodownload les avant de voir comment toosign dans tooRemoteApp de chacun des clients de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="ef9ed-110">Clients pris en charge</span><span class="sxs-lookup"><span data-stu-id="ef9ed-110">Supported clients</span></span>
<span data-ttu-id="ef9ed-111">Vous pouvez accéder à l’aide des étapes hello ci-dessous si votre appareil est en cours d’exécution un de ces systèmes d’exploitation de RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="ef9ed-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="ef9ed-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ef9ed-112">Windows 10</span></span> 
* <span data-ttu-id="ef9ed-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ef9ed-113">Windows 8.1</span></span>
* <span data-ttu-id="ef9ed-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ef9ed-114">Windows 8</span></span>
* <span data-ttu-id="ef9ed-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="ef9ed-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="ef9ed-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ef9ed-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="ef9ed-117">iOS</span><span class="sxs-lookup"><span data-stu-id="ef9ed-117">iOS</span></span>
* <span data-ttu-id="ef9ed-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ef9ed-118">Mac OS X</span></span>
* <span data-ttu-id="ef9ed-119">Android</span><span class="sxs-lookup"><span data-stu-id="ef9ed-119">Android</span></span>

 <span data-ttu-id="ef9ed-120">Que se passe-t-il pour les clients légers ? Hello suivant clients légers Windows Embedded est prises en charge :</span><span class="sxs-lookup"><span data-stu-id="ef9ed-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="ef9ed-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="ef9ed-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="ef9ed-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="ef9ed-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="ef9ed-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="ef9ed-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="ef9ed-124">Windows 10 IoT Entreprise</span><span class="sxs-lookup"><span data-stu-id="ef9ed-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="ef9ed-125">Téléchargement du client de hello</span><span class="sxs-lookup"><span data-stu-id="ef9ed-125">Downloading hello client</span></span>
<span data-ttu-id="ef9ed-126">Quelle que soit la plate-forme que vous utilisez, le client hello vous devez tooaccess RemoteApp se trouvent sur hello [téléchargement du client Bureau à distance](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="ef9ed-127">Cliquez sur liens différents hello soit directement commencent le téléchargement de client de hello ou vous enverra toohello page de téléchargement du client dans le magasin d’applications hello pour cette plateforme.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="ef9ed-128">Installer le client de hello en suivant les instructions de hello sur l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="ef9ed-129">Une fois que vous avez installé le client de hello sur votre appareil et a lancé, passer toohello la section correspondante ci-dessous toolearn comment toosign dans tooRemoteApp à partir de ce client.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="ef9ed-130">Android</span><span class="sxs-lookup"><span data-stu-id="ef9ed-130">Android</span></span>
<span data-ttu-id="ef9ed-131">Une fois que vous avez installé l’application de bureau à distance Microsoft hello de hello Google Play store, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ef9ed-132">Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="ef9ed-133">tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** , puis appuyez sur **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centre de connexion vide](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="ef9ed-135">Vous devez toosign avec votre service de messagerie adresse tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="ef9ed-136">Appuyez sur **Prise en main**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-136">Tap **Get started**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="ef9ed-138">Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ef9ed-139">Cela lance hello processus de connexion à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="ef9ed-141">Suivez les instructions de hello à toosign d’écran hello avec votre compte Microsoft (précédemment appelé « LiveID ») ou l’ID d’organisation.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="ef9ed-142">Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="ef9ed-143">Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Page des invitations](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="ef9ed-145">Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="ef9ed-146">Cliquez sur un des toostart d’applications hello à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="ef9ed-148">Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="ef9ed-149">est par conséquent, appuyez sur toodo **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="ef9ed-151">Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="ef9ed-153">iOS</span><span class="sxs-lookup"><span data-stu-id="ef9ed-153">iOS</span></span>
<span data-ttu-id="ef9ed-154">Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin d’applications hello, vous pouvez le trouver dans votre liste d’applications sous **Client Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="ef9ed-155">Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="ef9ed-156">tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** , puis appuyez sur **ajouter Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="ef9ed-158">Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart ce processus, le type dans votre **adresse de messagerie** , puis appuyez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="ef9ed-160">Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ef9ed-161">Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="ef9ed-162">Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="ef9ed-164">Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="ef9ed-165">Cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="ef9ed-167">Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="ef9ed-168">est par conséquent, appuyez sur toodo **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="ef9ed-170">Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="ef9ed-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ef9ed-172">Mac OS X</span></span>
<span data-ttu-id="ef9ed-173">Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin d’applications hello, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="ef9ed-174">Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="ef9ed-175">tooget main d’Azure RemoteApp, cliquez sur hello **Azure RemoteApp** bouton.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="ef9ed-177">Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart traiter, appuyez sur **prise en main**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="ef9ed-179">Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ef9ed-180">Cela lance hello se connecte à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="ef9ed-182">Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ef9ed-183">Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="ef9ed-184">Si vous êtes, sélectionnez les invitations hello vous faites confiance et fermez la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="ef9ed-186">Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="ef9ed-187">Double-cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="ef9ed-189">Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="ef9ed-190">toodo, cliquez sur **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="ef9ed-192">Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="ef9ed-194">Windows (Toutes les versions prises en charge sauf Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="ef9ed-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="ef9ed-195">Hello client lance automatiquement une fois l’installation, toutefois lorsque vous avez besoin tooaccess il plus tard il sont accessibles dans votre liste d’applications sous le nom de hello **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="ef9ed-196">Lus tard du lancement hello client, hello première page qui apparaît vous souhaite la bienvenue tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="ef9ed-197">tooproceed, cliquez sur **prise en main**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Page d’accueil du client d’Azure RemoteApp hello](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="ef9ed-199">page suivante de Hello démarre hello signe dans le processus d’Azure RemoteApp à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="ef9ed-200">Ce processus doivent sembler familière si vous avez utilisé les services Microsoft Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="ef9ed-201">Commencez par taper votre **adresse de messagerie**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Invite de la première page Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="ef9ed-203">Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ef9ed-204">Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="ef9ed-205">Si vous êtes, sélectionnez les invitations hello vous faites confiance, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Page invitations à participer à des clients d’Azure RemoteApp hello](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="ef9ed-207">Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="ef9ed-208">Double-cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centre de connexion du client d’Azure RemoteApp hello](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="ef9ed-210">Si personne ne vous a encore envoyé d'invitation, ne vous inquiétez pas : nous avons paré à cette éventualité !</span><span class="sxs-lookup"><span data-stu-id="ef9ed-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="ef9ed-211">Vous aurez toujours accès tooa démonstration collection afin de tester les service hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="ef9ed-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ef9ed-213">Windows Phone 8.1</span></span>
<span data-ttu-id="ef9ed-214">Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin de hello Windows Phone 8.1, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ef9ed-215">Lors du lancement du application hello vous procure directement tooan centre de connexion vide, sauf si vous avez déjà l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="ef9ed-216">tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Centre de connexion vide](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="ef9ed-218">Appuyez ensuite sur **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Page Ajouter des éléments](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="ef9ed-220">Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart traiter, appuyez sur **connecter**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Invite de connexion](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="ef9ed-222">Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ef9ed-223">Cela lance hello se connecte à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="ef9ed-225">Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ef9ed-226">Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="ef9ed-227">Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Page des invitations](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="ef9ed-229">Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="ef9ed-230">Cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="ef9ed-232">Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="ef9ed-233">est par conséquent, appuyez sur toodo **Oui** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="ef9ed-235">Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ef9ed-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

