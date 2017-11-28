---
title: aaaCreating un projet de service cloud Azure avec Visual Studio | Documents Microsoft
description: En savoir plus maintenant toocreate un projet de service cloud Azure avec Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="de7e7-103">Création d’un projet de service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de7e7-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="de7e7-104">Bonjour Azure Tools pour Visual Studio fournit un modèle de projet qui vous permet de créer un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="de7e7-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="de7e7-105">Une fois le projet de hello a été créé, Visual Studio vous permet de tooconfigure, déboguer et déployer hello cloud service tooAzure.</span><span class="sxs-lookup"><span data-stu-id="de7e7-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="de7e7-106">Étapes toocreate un projet de service cloud Azure dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de7e7-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="de7e7-107">Cette section vous guide dans le processus de création d’un projet de service cloud Azure dans Visual Studio avec un ou plusieurs rôles web.</span><span class="sxs-lookup"><span data-stu-id="de7e7-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="de7e7-108">Démarrez Visual Studio en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="de7e7-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="de7e7-109">Dans le menu principal de hello, sélectionnez **fichier** > **nouveau** > **projet**.</span><span class="sxs-lookup"><span data-stu-id="de7e7-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="de7e7-110">Sélectionnez **Cloud** de hello Visual c# ou Visual Basic nœuds du modèle de projet, puis sélectionnez **Azure Cloud Service** de liste hello des modèles.</span><span class="sxs-lookup"><span data-stu-id="de7e7-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Nouveau service cloud Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="de7e7-112">Spécifiez la version de hello .NET Framework vous souhaitez toouse toodevelop votre projet.</span><span class="sxs-lookup"><span data-stu-id="de7e7-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="de7e7-113">Entrez un nom et un emplacement pour votre projet et un nom pour la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="de7e7-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="de7e7-114">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="de7e7-114">Select **OK**.</span></span>

1. <span data-ttu-id="de7e7-115">Bonjour **nouveau Microsoft Azure Cloud Service** boîte de dialogue, les rôles hello select que vous souhaitez tooadd, choisissez tooadd de bouton de flèche droite hello les tooyour solution.</span><span class="sxs-lookup"><span data-stu-id="de7e7-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Sélectionner de nouveaux rôles de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="de7e7-117">toorename un rôle que vous avez ajouté, amenez le pointeur sur le rôle hello Bonjour **nouveau Microsoft Azure Cloud Service** boîte de dialogue et, dans le menu contextuel de hello, sélectionnez **renommer**.</span><span class="sxs-lookup"><span data-stu-id="de7e7-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="de7e7-118">Vous pouvez également renommer un rôle au sein de votre solution (Bonjour **l’Explorateur de solutions**) une fois qu’il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="de7e7-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Renommer un rôle de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="de7e7-120">projet de Visual Studio Azure Hello a des projets de rôle toohello associations de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="de7e7-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="de7e7-121">projet de Hello inclut également hello *fichier de définition de service* et *fichier de configuration de service*:</span><span class="sxs-lookup"><span data-stu-id="de7e7-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="de7e7-122">**Fichier de définition de service** -définit les paramètres d’exécution hello pour votre application, y compris les rôles sont requis, points de terminaison et taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="de7e7-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="de7e7-123">**Fichier de configuration de service** -configure le nombre d’instances d’un rôle est exécuté et hello des valeurs de paramètres hello définis pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="de7e7-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="de7e7-124">Pour plus d’informations sur ces fichiers, consultez [configurer des rôles de hello pour un service cloud Azure avec Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="de7e7-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de7e7-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de7e7-125">Next steps</span></span>
- [<span data-ttu-id="de7e7-126">Gestion des rôles dans les projets de service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de7e7-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
