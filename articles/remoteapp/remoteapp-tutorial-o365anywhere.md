---
title: "Profitez de la même expérience d’Office 365 sur n’importe quel appareil avec Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment partager n’importe quelle application Office 365 avec vos utilisateurs grâce à Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="9a22f-103">Bénéficiez de la même expérience Office 365 sur n’importe quel appareil avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9a22f-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9a22f-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="9a22f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9a22f-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="9a22f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9a22f-106">Cet article explique comment déployer Office 365 sur n’importe quel appareil au sein de votre société.</span><span class="sxs-lookup"><span data-stu-id="9a22f-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="9a22f-107">Vos utilisateurs peuvent bénéficier des mêmes fonctionnalités et de la même interface utilisateur sur Android, Apple et Windows.</span><span class="sxs-lookup"><span data-stu-id="9a22f-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="9a22f-108">Pour ce faire, nous allons utiliser Azure RemoteApp en hébergeant Office 365 sur des machines virtuelles évolutives dans Azure, auxquelles les utilisateurs peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="9a22f-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="9a22f-109">Nous appelons cet ensemble de machines virtuelles une « collection cloud ».</span><span class="sxs-lookup"><span data-stu-id="9a22f-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="9a22f-110">Création d'une collection cloud</span><span class="sxs-lookup"><span data-stu-id="9a22f-110">Create a cloud collection</span></span>
<span data-ttu-id="9a22f-111">Après avoir créé un compte Azure, accédez à **RemoteApp** en cliquant sur le lien situé à gauche.</span><span class="sxs-lookup"><span data-stu-id="9a22f-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="9a22f-112">![Affichage d’Azure RemoteApp sur le portail Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="9a22f-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="9a22f-113">Continuez en cliquant sur **Nouveau** en bas de la fenêtre, puis sur Création rapide, afin de créer une collection.</span><span class="sxs-lookup"><span data-stu-id="9a22f-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="9a22f-114">Indiquez un nom, la région, l’abonnement, le plan et l’image « Office Professionnel 2013 » proposée.</span><span class="sxs-lookup"><span data-stu-id="9a22f-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="9a22f-115">![Boîte de dialogue Créer](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="9a22f-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="9a22f-116">Une fois le formulaire rempli, le processus de création de formulaire devrait démarrer.</span><span class="sxs-lookup"><span data-stu-id="9a22f-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="9a22f-117">Cette procédure peut prendre environ une heure.</span><span class="sxs-lookup"><span data-stu-id="9a22f-117">This may take up to an hour or so.</span></span>

![En attente](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="9a22f-119">Une fois le processus terminé, vous devriez obtenir le résultat suivant.</span><span class="sxs-lookup"><span data-stu-id="9a22f-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="9a22f-120">Si vous cliquez sur **Publication** , vous voyez que la plupart des applications Office ont déjà été publiées.</span><span class="sxs-lookup"><span data-stu-id="9a22f-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="9a22f-121">![La collection a été créée](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="9a22f-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Applications publiées](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="9a22f-123">À ce stade, vous pouvez également ajouter des utilisateurs ayant accès à cette collection en cliquant sur **Accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9a22f-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="9a22f-124">![Configuration de l'accès utilisateur](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="9a22f-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="9a22f-125">À présent, nous allons essayer de nous connecter à Office 365 !</span><span class="sxs-lookup"><span data-stu-id="9a22f-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="9a22f-126">Connexion à Office 365</span><span class="sxs-lookup"><span data-stu-id="9a22f-126">Connect to Office 365</span></span>
<span data-ttu-id="9a22f-127">Rendez-vous sur [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), faites défiler la page vers le bas et cliquez sur **Télécharger les clients** pour installer le client Azure RemoteApp sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="9a22f-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="9a22f-128">Les captures d’écran ci-dessous correspondent à l’environnement Windows.</span><span class="sxs-lookup"><span data-stu-id="9a22f-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="9a22f-129">Lorsque l’application démarre, le système vous demande de vous connecter à l’aide de votre compte Microsoft (anciennement dénommé « Windows Live ID »). Utilisez celui de votre compte Azure pour le moment.</span><span class="sxs-lookup"><span data-stu-id="9a22f-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="9a22f-130">Une fois connecté, vous devriez voir une notification vous indiquant de nouvelles invitations. Cliquez dessus pour afficher une liste comme celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9a22f-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="9a22f-131">Acceptez l’invitation correspondant à l’adresse e-mail de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="9a22f-131">Accept the invitation that matches your Azure account owner email.</span></span>

![Nouvelle invitation](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="9a22f-133">Ce que vous voyez lorsque de nouvelles invitations sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="9a22f-133">What it looks like when there are new invitations.</span></span>

![Accepter une application](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="9a22f-135">Une fois l’invitation acceptée, vous devriez voir toutes les applications Office dans le client Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9a22f-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![Liste des applications](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="9a22f-137">Lorsque vous cliquez sur l’une de ces applications, celle-ci démarre sur la machine virtuelle Azure, entièrement configurée !</span><span class="sxs-lookup"><span data-stu-id="9a22f-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="9a22f-138">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="9a22f-138">Enjoy!</span></span>

![démarrage en cours](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

