---
title: "aaaGet hello même expérience Office 365 sur n’importe quel appareil avec Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooshare n’importe quelle application Office 365 avec vos utilisateurs à l’aide d’Azure RemoteApp."
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
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="f6613-103">Get hello même expérience Office 365 sur n’importe quel appareil avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f6613-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f6613-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="f6613-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f6613-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f6613-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f6613-106">Cet article décrit comment toodeploy Office 365 sur n’importe quel appareil dans votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="f6613-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="f6613-107">Les utilisateurs peuvent obtenir les mêmes fonctionnalités hello et l’interface utilisateur d’expérience sur Android, Apple et Windows.</span><span class="sxs-lookup"><span data-stu-id="f6613-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="f6613-108">Pour ce faire, nous allons utiliser Azure RemoteApp en hébergeant Office 365 sur des machines virtuelles évolutives dans Azure, auxquelles les utilisateurs peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="f6613-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="f6613-109">Nous appelons cet ensemble de machines virtuelles une « collection cloud ».</span><span class="sxs-lookup"><span data-stu-id="f6613-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="f6613-110">Création d'une collection cloud</span><span class="sxs-lookup"><span data-stu-id="f6613-110">Create a cloud collection</span></span>
<span data-ttu-id="f6613-111">Après avoir créé un compte Azure, accédez d’abord trop**RemoteApp** en cliquant sur le lien hello sur hello côté gauche.</span><span class="sxs-lookup"><span data-stu-id="f6613-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="f6613-112">![Affichage d’Azure RemoteApp sur hello portail Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="f6613-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="f6613-113">Poursuivez en cliquant sur **nouveau** sur bas de hello et « création rapide » une collection.</span><span class="sxs-lookup"><span data-stu-id="f6613-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="f6613-114">Fournir le nom, région de hello, abonnement de hello, plan de hello et l’image hello « Proffesional Office 2013 » que nous fournissons.</span><span class="sxs-lookup"><span data-stu-id="f6613-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="f6613-115">![Boîte de dialogue Créer](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="f6613-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="f6613-116">Une fois que vous avez terminé le processus de création de collection hello écran hello doit démarrer.</span><span class="sxs-lookup"><span data-stu-id="f6613-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="f6613-117">Cela peut prendre jusqu'à tooan heures ou des cas.</span><span class="sxs-lookup"><span data-stu-id="f6613-117">This may take up tooan hour or so.</span></span>

![En attente](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="f6613-119">Une fois le processus de hello est terminé, il ressemble à ceci.</span><span class="sxs-lookup"><span data-stu-id="f6613-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="f6613-120">Si vous cliquez sur **Publication** , vous voyez que la plupart des applications Office ont déjà été publiées.</span><span class="sxs-lookup"><span data-stu-id="f6613-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="f6613-121">![La collection a été créée](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="f6613-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Applications publiées](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="f6613-123">À ce stade, vous pouvez également ajouter des utilisateurs qui ont accès toothis collection en cliquant sur **accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f6613-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="f6613-124">![Configuration de l'accès utilisateur](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="f6613-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="f6613-125">Maintenant nous allons tester la connexion tooOffice 365 !</span><span class="sxs-lookup"><span data-stu-id="f6613-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="f6613-126">Se connecter tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="f6613-126">Connect tooOffice 365</span></span>
<span data-ttu-id="f6613-127">Nous allons head sur trop[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), faites défiler la liste et cliquez sur **télécharger des clients** client de Azure RemoteApp tooinstall hello sur périphérique hello sur.</span><span class="sxs-lookup"><span data-stu-id="f6613-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="f6613-128">captures d’écran Hello ci-dessous sont pour Windows.</span><span class="sxs-lookup"><span data-stu-id="f6613-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="f6613-129">Une fois que l’application hello démarre vous serez invité à indiquer toosign avec votre compte Microsoft (anciennement appelé « Live ID »), utilisez hello identique à celui que votre compte Azure pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="f6613-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="f6613-130">Une fois connecté, vous devriez voir une notification vous indiquant de nouvelles invitations. Cliquez dessus pour afficher une liste comme celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f6613-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="f6613-131">Accepter l’invitation hello qui correspond à votre adresse de messagerie du propriétaire du compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f6613-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Nouvelle invitation](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="f6613-133">Ce que vous voyez lorsque de nouvelles invitations sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6613-133">What it looks like when there are new invitations.</span></span>

![Accepter une application](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="f6613-135">Une fois que vous acceptez hello invitation, vous devez voir toutes les applications d’Office hello dans le client d’Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="f6613-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Liste des applications](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="f6613-137">Lorsque vous cliquez sur une de ces applications, hello doit commencer sur hello de machine virtuelle Azure, vous devez être définis !</span><span class="sxs-lookup"><span data-stu-id="f6613-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="f6613-138">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="f6613-138">Enjoy!</span></span>

![démarrage en cours](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

