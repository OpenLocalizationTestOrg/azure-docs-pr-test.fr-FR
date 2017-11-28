---
title: "aaaAdd stockage Azure à l’aide des Services connectés dans Visual Studio | Documents Microsoft"
description: "Ajouter une application de tooyour de stockage Azure en utilisant la boîte de dialogue hello Visual Studio ajouter des Services connectés"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="8e50d-103">Ajout de stockage Azure à l’aide des services connectés de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e50d-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="8e50d-104">Avec Visual Studio, vous pouvez connecter des hello suivant tooAzure stockage à l’aide de hello **ajouter des Services connectés** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="8e50d-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="8e50d-105">Service cloud C#</span><span class="sxs-lookup"><span data-stu-id="8e50d-105">C# cloud service</span></span>
- <span data-ttu-id="8e50d-106">Service mobile principal .NET</span><span class="sxs-lookup"><span data-stu-id="8e50d-106">.NET backend mobile service</span></span>
- <span data-ttu-id="8e50d-107">Service ou site web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8e50d-107">ASP.NET website or service</span></span>
- <span data-ttu-id="8e50d-108">Service Core ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8e50d-108">ASP.NET Core service</span></span>
- <span data-ttu-id="8e50d-109">Service de tâche web Azure</span><span class="sxs-lookup"><span data-stu-id="8e50d-109">Azure WebJob service</span></span> 

<span data-ttu-id="8e50d-110">Hello service connecté fonctionnalité ajoute toutes les références de hello nécessité et projet de tooyour de code de connexion et modifie vos fichiers de configuration de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="8e50d-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="8e50d-111">Une fois terminé, hello **ajouter des Services connectés** boîte de dialogue affiche automatiquement la documentation détaillant les toostart requis étapes hello fonctionne avec le stockage d’objets blob, files d’attente et les tables.</span><span class="sxs-lookup"><span data-stu-id="8e50d-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="8e50d-112">Se connecter tooAzure stockage à l’aide des Services connectés hello boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="8e50d-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="8e50d-113">Ouvrez votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e50d-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="8e50d-114">Dans **l’Explorateur de solutions**, avec le bouton hello **Services connectés** nœud et, dans le menu contextuel de hello, sélectionnez **ajouter un Service connecté**.</span><span class="sxs-lookup"><span data-stu-id="8e50d-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Ajouter un service connecté Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="8e50d-116">Bonjour **Services connectés** page, sélectionnez **stockage en Cloud avec le stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e50d-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Ajouter le Stockage Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="8e50d-118">Bonjour **Azure Storage** boîte de dialogue, sélectionnez un compte de stockage existant et sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e50d-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="8e50d-119">Si vous avez besoin de toocreate un compte de stockage, accédez toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="8e50d-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="8e50d-120">Sinon, passez toostep 6.</span><span class="sxs-lookup"><span data-stu-id="8e50d-120">Otherwise, skip toostep 6.</span></span>
    
    ![Ajouter tooproject de compte de stockage existant](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="8e50d-122">toocreate un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="8e50d-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="8e50d-123">Sélectionnez **créer un nouveau compte de stockage** bas hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8e50d-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="8e50d-124">Remplir hello **créer un compte de stockage** boîte de dialogue, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="8e50d-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nouveau compte de stockage Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="8e50d-126">Hello lorsque **Azure Storage** boîte de dialogue s’affiche, le nouveau compte de stockage hello s’affiche dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="8e50d-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="8e50d-127">Sélectionnez le nouveau compte de stockage hello dans la liste de hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e50d-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="8e50d-128">Hello stockage service connecté s’affiche sous hello **références de Service** nœud de votre projet.</span><span class="sxs-lookup"><span data-stu-id="8e50d-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="8e50d-129">Modifications apportées à votre projet</span><span class="sxs-lookup"><span data-stu-id="8e50d-129">How your project is modified</span></span>
<span data-ttu-id="8e50d-130">Lorsque vous avez terminé la boîte de dialogue hello, Visual Studio ajoute des références et modifie certains fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="8e50d-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="8e50d-131">modifications Hello varient selon le type de projet hello :</span><span class="sxs-lookup"><span data-stu-id="8e50d-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="8e50d-132">Projet ASP.NET : [Que s’est-il passé ? – Projets ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="8e50d-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="8e50d-133">Projet Core ASP.NET : [Que s’est-il passé ? – Projets ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="8e50d-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="8e50d-134">Projet de service cloud (rôles web et de travail) : [Que s’est-il passé ? – Projets de service cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="8e50d-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="8e50d-135">Projets de tâche web - [Que s’est-il passé ? – Projets de tâche web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="8e50d-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e50d-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e50d-136">Next steps</span></span>
- [<span data-ttu-id="8e50d-137">Forum MSDN : Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8e50d-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="8e50d-138">Blog de l’équipe Stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8e50d-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="8e50d-139">Documentation d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8e50d-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
