---
title: "aaaDebugging un rapport publié un Azure cloud service avec Visual Studio et IntelliTrace | Documents Microsoft"
description: "Découvrez comment toodebug un cloud service avec Visual Studio et d’IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="95c9d-103">Débogage d’un service cloud Azure publié avec Visual Studio et IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="95c9d-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="95c9d-104">Avec IntelliTrace, vous pouvez enregistrer des informations de débogage détaillées pour une instance de rôle exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="95c9d-105">Si vous avez besoin d’origine de hello toofind d’un problème, vous pouvez utiliser toostep de journaux IntelliTrace hello dans votre code à partir de Visual Studio comme s’il s’exécutait dans Azure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="95c9d-106">En effet, IntelliTrace enregistre code de touche d’exécution et l’environnement les données lorsque votre application Azure s’exécute comme un service cloud dans Azure et vous permet de relire les données de hello enregistrée à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95c9d-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="95c9d-107">Vous pouvez utiliser IntelliTrace si Visual Studio Enterprise est installé et que votre application Azure cible .NET Framework 4 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="95c9d-108">IntelliTrace collecte des informations pour vos rôles Azure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="95c9d-109">machines virtuelles de Hello pour ces rôles s’exécutent toujours des systèmes d’exploitation 64 bits.</span><span class="sxs-lookup"><span data-stu-id="95c9d-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="95c9d-110">En guise d’alternative, vous pouvez utiliser [débogage distant](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directement les service de cloud de tooa qui s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95c9d-111">IntelliTrace est conçu uniquement pour des scénarios de débogage et ne doit pas être utilisé dans le cadre d’un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="95c9d-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="95c9d-112">Configurer une application Azure pour IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="95c9d-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="95c9d-113">tooenable IntelliTrace pour une application Windows Azure, vous devez créer et publier l’application hello à partir d’un projet Windows Azure Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95c9d-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="95c9d-114">Avant de le publier tooAzure, vous devez configurer IntelliTrace pour votre application Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="95c9d-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="95c9d-115">Si vous publiez votre application sans configurer IntelliTrace, vous devez le projet de hello toorepublish.</span><span class="sxs-lookup"><span data-stu-id="95c9d-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="95c9d-116">Pour plus d’informations, voir [Publication d’un projet Azure Cloud Services à l’aide de Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="95c9d-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="95c9d-117">Lorsque vous êtes prêt à toodeploy votre application Windows Azure, vérifiez que votre projet cible de build est trop**déboguer**.</span><span class="sxs-lookup"><span data-stu-id="95c9d-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="95c9d-118">Dans **l’Explorateur de solutions**, cliquez sur le projet et, dans le menu contextuel de hello, sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="95c9d-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="95c9d-119">Bonjour **publier l’Application Azure** boîte de dialogue, sélectionnez hello abonnement Azure, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95c9d-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="95c9d-120">Bonjour **paramètres** page, sélectionnez hello **paramètres avancés** onglet.</span><span class="sxs-lookup"><span data-stu-id="95c9d-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="95c9d-121">Activer hello **activer IntelliTrace** option toocollect les fichiers journaux IntelliTrace pour votre application lorsqu’elle est publiée dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="95c9d-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="95c9d-122">toocustomize hello IntelliTrace configuration de base, sélectionnez **paramètres** suivant trop**activer IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="95c9d-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Lien Paramètres IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="95c9d-124">Bonjour **paramètres IntelliTrace** boîte de dialogue, vous pouvez spécifier le toolog d’événements, si toocollect informations sur les appels, le toocollect modules et processus ouvre une session, la quantité d’espace tooallocate toohello enregistrement et.</span><span class="sxs-lookup"><span data-stu-id="95c9d-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="95c9d-125">Pour plus d’informations sur IntelliTrace, consultez [Débogage avec IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="95c9d-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Paramètres IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="95c9d-127">fichier journal IntelliTrace Hello est un fichier journal circulaire de taille maximale de hello spécifié dans les paramètres IntelliTrace hello (taille de hello par défaut est 250 Mo).</span><span class="sxs-lookup"><span data-stu-id="95c9d-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="95c9d-128">Les fichiers journaux IntelliTrace sont collectés tooa fichier hello système de fichiers d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="95c9d-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="95c9d-129">Lorsque vous demandez les journaux hello, un instantané est effectuée à ce stade dans le temps et téléchargé tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="95c9d-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="95c9d-130">Une fois hello service cloud Azure a été publiée tooAzure, vous pouvez déterminer si IntelliTrace a été activé à partir de hello Azure nœud dans **l’Explorateur de serveurs**, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="95c9d-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Explorateur de serveurs - IntelliTrace activé](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="95c9d-132">Télécharger les journaux IntelliTrace pour une instance de rôle</span><span class="sxs-lookup"><span data-stu-id="95c9d-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="95c9d-133">À l’aide de Visual Studio, vous pouvez télécharger les journaux IntelliTrace pour une instance de rôle en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="95c9d-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="95c9d-134">Dans **l’Explorateur de serveurs**, développez hello **Services de cloud computing** nœud, puis recherchez l’instance de rôle dont vous souhaitez toodownload les journaux.</span><span class="sxs-lookup"><span data-stu-id="95c9d-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="95c9d-135">Droit d’instance de rôle hello sur, puis dans le menu contextuel de hello s, sélectionnez **afficher les journaux IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="95c9d-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Option de menu Afficher les fichiers journaux IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="95c9d-137">les fichiers journaux IntelliTrace Hello sont tooa téléchargé les fichiers dans un répertoire sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="95c9d-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="95c9d-138">Chaque fois que vous demandez les journaux IntelliTrace hello, un nouvel instantané est créé.</span><span class="sxs-lookup"><span data-stu-id="95c9d-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="95c9d-139">Pendant le téléchargement des journaux de hello, Visual Studio affiche la progression de hello d’opération de hello dans hello **journal des activités Azure** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="95c9d-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="95c9d-140">Comme indiqué dans la figure suivante de hello, vous pouvez développer hello élément hello opération toosee plus en détail.</span><span class="sxs-lookup"><span data-stu-id="95c9d-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="95c9d-142">Vous pouvez continuer toowork dans Visual Studio pendant le téléchargement des fichiers journaux IntelliTrace hello.</span><span class="sxs-lookup"><span data-stu-id="95c9d-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="95c9d-143">Lorsque le journal de hello a terminé le téléchargement, il s’ouvre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95c9d-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="95c9d-144">Hello les fichiers journaux IntelliTrace peuvent contenir des exceptions qui framework hello génère et gère par la suite.</span><span class="sxs-lookup"><span data-stu-id="95c9d-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="95c9d-145">Le code de l’infrastructure interne génère ces exceptions dans le cadre normal du démarrage d’un rôle. Vous pouvez donc les ignorer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="95c9d-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="95c9d-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95c9d-146">Next steps</span></span>
- [<span data-ttu-id="95c9d-147">Options de débogage d’Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="95c9d-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="95c9d-148">Publication d’un service cloud Azure à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95c9d-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)