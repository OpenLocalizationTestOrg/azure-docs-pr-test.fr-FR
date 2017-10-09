---
title: "toorun d’émulateur Express aaaUsing et debug Azure cloud service sur un ordinateur local | Documents Microsoft"
description: "À l’aide de toorun d’émulateur Express et déboguer un service cloud sur un ordinateur local"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="acbd1-103">L’émulateur Express toorun et debug Azure cloud service sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="acbd1-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="acbd1-104">Avec l’émulateur express, vous testez et déboguez un service cloud sans avoir à exécuter Visual Studio en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="acbd1-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="acbd1-105">Vous pouvez définir votre toouse de paramètres de projet à l’émulateur Express ou hello émulateur complet, selon les spécifications de hello de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="acbd1-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="acbd1-106">Pour plus d’informations sur l’émulateur complet hello, consultez [exécuter une Application Azure dans l’émulateur de calcul de hello](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="acbd1-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="acbd1-107">Utiliser l’émulateur express dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="acbd1-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="acbd1-108">Quand vous créez un projet Azure dans le Kit de développement logiciel (SDK) Azure 2.3 ou une version ultérieure, l’émulateur express est automatiquement utilisé.</span><span class="sxs-lookup"><span data-stu-id="acbd1-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="acbd1-109">Pour les projets existants qui ont été créées avec une version antérieure de hello Azure SDK, utilisez hello suivant tooselect étapes émulateur Express :</span><span class="sxs-lookup"><span data-stu-id="acbd1-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="acbd1-110">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acbd1-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="acbd1-111">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="acbd1-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="acbd1-112">Dans les pages de propriétés de projets hello, sélectionnez hello **Web** onglet.</span><span class="sxs-lookup"><span data-stu-id="acbd1-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Propriétés pour un projet de service cloud Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="acbd1-114">Sous **Serveur de développement local**, sélectionnez **l’option Utiliser IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="acbd1-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="acbd1-115">Sous **Émulateur**, sélectionnez **Utiliser l’émulateur express**.</span><span class="sxs-lookup"><span data-stu-id="acbd1-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="acbd1-116">toolaunch hello émulateur Express, exécutez hello commande à l’invite de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="acbd1-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="acbd1-117">Limitations de l’émulateur express</span><span class="sxs-lookup"><span data-stu-id="acbd1-117">Emulator Express limitations</span></span>
<span data-ttu-id="acbd1-118">restrictions de l’émulateur Express est connue par Hello suivants :</span><span class="sxs-lookup"><span data-stu-id="acbd1-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="acbd1-119">L’émulateur express n’est pas compatible avec le serveur web IIS.</span><span class="sxs-lookup"><span data-stu-id="acbd1-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="acbd1-120">Votre service cloud peut contenir plusieurs rôles, mais chaque rôle est limitée tooone instance.</span><span class="sxs-lookup"><span data-stu-id="acbd1-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="acbd1-121">Vous n’avez pas accès aux numéros de port inférieurs à 1 000.</span><span class="sxs-lookup"><span data-stu-id="acbd1-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="acbd1-122">Si vous utilisez un fournisseur d’authentification qui utilise généralement un port inférieur à 1000, vous devrez peut-être toochange ce numéro de port tooa valeur qui est supérieur à 1000.</span><span class="sxs-lookup"><span data-stu-id="acbd1-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="acbd1-123">Les restrictions qui s’appliquent toohello émulateur de calcul Azure s’appliquent également à tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="acbd1-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="acbd1-124">Par exemple, il ne peut pas y avoir plus de 50 instances de rôle par déploiement.</span><span class="sxs-lookup"><span data-stu-id="acbd1-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="acbd1-125">Pour plus d’informations sur hello émulateur de calcul Azure, consultez [exécuter une Application Azure dans l’émulateur de calcul de hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="acbd1-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="acbd1-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="acbd1-126">Next steps</span></span>
[<span data-ttu-id="acbd1-127">Débogage des services cloud Azure</span><span class="sxs-lookup"><span data-stu-id="acbd1-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
