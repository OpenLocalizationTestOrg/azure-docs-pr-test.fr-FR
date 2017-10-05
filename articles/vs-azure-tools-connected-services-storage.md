---
title: "Ajouter Azure Storage à l’aide des services connectés dans Visual Studio | Microsoft Docs"
description: "Ajouter le stockage Azure à votre application à l’aide de la boîte de dialogue Ajouter des services connectés de Visual Studio"
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
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="0fa6c-103">Ajout de stockage Azure à l’aide des services connectés de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0fa6c-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="0fa6c-104">Avec Visual Studio, vous pouvez connecter les éléments suivants au Stockage Azure à l’aide de la boîte de dialogue **Ajouter des services connectés** :</span><span class="sxs-lookup"><span data-stu-id="0fa6c-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="0fa6c-105">Service cloud C#</span><span class="sxs-lookup"><span data-stu-id="0fa6c-105">C# cloud service</span></span>
- <span data-ttu-id="0fa6c-106">Service mobile principal .NET</span><span class="sxs-lookup"><span data-stu-id="0fa6c-106">.NET backend mobile service</span></span>
- <span data-ttu-id="0fa6c-107">Service ou site web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0fa6c-107">ASP.NET website or service</span></span>
- <span data-ttu-id="0fa6c-108">Service Core ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0fa6c-108">ASP.NET Core service</span></span>
- <span data-ttu-id="0fa6c-109">Service de tâche web Azure</span><span class="sxs-lookup"><span data-stu-id="0fa6c-109">Azure WebJob service</span></span> 

<span data-ttu-id="0fa6c-110">La fonctionnalité de service connecté ajoute l’ensemble des références et du code de connexion nécessaires à votre projet, et modifie vos fichiers de configuration de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="0fa6c-111">Une fois cette opération terminée, la boîte de dialogue **Ajouter des services connectés** affiche automatiquement une documentation décrivant les étapes nécessaires pour commencer à travailler avec le Stockage Blob, les files d’attente et les tables.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="0fa6c-112">Connexion au stockage Azure à l’aide de la boîte de dialogue Services connectés</span><span class="sxs-lookup"><span data-stu-id="0fa6c-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="0fa6c-113">Ouvrez votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="0fa6c-114">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud **Services connectés**, puis sélectionnez **Ajouter un service connecté** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Ajouter un service connecté Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="0fa6c-116">Sur la page **Services connectés**, sélectionnez **Stockage cloud avec le Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Ajouter le Stockage Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="0fa6c-118">Dans la boîte de dialogue **Stockage Azure**, sélectionnez un compte de stockage existant, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="0fa6c-119">Si vous devez créer un compte de stockage, passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="0fa6c-120">Sinon, passez à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-120">Otherwise, skip to step 6.</span></span>
    
    ![Ajouter un compte de stockage existant au projet](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="0fa6c-122">Pour créer un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="0fa6c-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="0fa6c-123">Sélectionnez **Créer un compte de stockage** au bas de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="0fa6c-124">Renseignez les informations demandées dans la boîte de dialogue **Créer un compte de stockage**, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nouveau compte de stockage Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="0fa6c-126">Lorsque la boîte de dialogue **Stockage Azure** apparaît, le nouveau compte de stockage s’affiche dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="0fa6c-127">Sélectionnez le nouveau compte de stockage dans la liste, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="0fa6c-128">Le service connecté de stockage s’affiche sous le nœud **Références de service** de votre projet.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="0fa6c-129">Modifications apportées à votre projet</span><span class="sxs-lookup"><span data-stu-id="0fa6c-129">How your project is modified</span></span>
<span data-ttu-id="0fa6c-130">Quand vous avez terminé la boîte de dialogue, Visual Studio ajoute des références et modifie certains fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="0fa6c-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="0fa6c-131">Les modifications spécifiques varient selon le type de projet :</span><span class="sxs-lookup"><span data-stu-id="0fa6c-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="0fa6c-132">Projet ASP.NET : [Que s’est-il passé ? – Projets ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="0fa6c-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="0fa6c-133">Projet Core ASP.NET : [Que s’est-il passé ? – Projets ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="0fa6c-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="0fa6c-134">Projet de service cloud (rôles web et de travail) : [Que s’est-il passé ? – Projets de service cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="0fa6c-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="0fa6c-135">Projets de tâche web - [Que s’est-il passé ? – Projets de tâche web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="0fa6c-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa6c-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0fa6c-136">Next steps</span></span>
- [<span data-ttu-id="0fa6c-137">Forum MSDN : Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0fa6c-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="0fa6c-138">Blog de l’équipe Stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0fa6c-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="0fa6c-139">Documentation d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0fa6c-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
