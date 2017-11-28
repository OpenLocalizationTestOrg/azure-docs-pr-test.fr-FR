---
title: aaaConfigure un projet de service cloud Azure avec Visual Studio | Documents Microsoft
description: "Découvrez comment tooconfigure Azure cloud projet de service dans Visual Studio, selon vos spécifications pour ce projet."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="d4c11-103">Configurer un projet de service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4c11-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="d4c11-104">Vous pouvez configurer un projet de service cloud Azure selon vos spécifications pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="d4c11-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="d4c11-105">Vous pouvez définir des propriétés de projet hello pour hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="d4c11-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="d4c11-106">**Publier un tooAzure de service cloud** -vous pouvez définir un toomake propriété sûr qu’un tooAzure de déployé le service cloud existant n’est pas supprimé par inadvertance.</span><span class="sxs-lookup"><span data-stu-id="d4c11-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="d4c11-107">**Exécuter ou déboguer un service cloud sur l’ordinateur local de hello** -vous pouvez sélectionner un toouse de configuration de service et indiquer si vous souhaitez que l’émulateur de stockage Azure toostart hello.</span><span class="sxs-lookup"><span data-stu-id="d4c11-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="d4c11-108">**Valider un package de service cloud lors de sa création** -vous pouvez décider tootreat tous les avertissements comme des erreurs afin que vous pouvez vous assurer de ce package de service cloud hello déploie sans problème.</span><span class="sxs-lookup"><span data-stu-id="d4c11-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="d4c11-109">Étapes tooconfigure un projet de service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="d4c11-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="d4c11-110">Ouvrir ou créer un projet de service cloud dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4c11-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="d4c11-111">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="d4c11-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="d4c11-112">Dans la page de propriétés du projet hello, sélectionnez hello **développement** onglet.</span><span class="sxs-lookup"><span data-stu-id="d4c11-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menu des propriétés du projet](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="d4c11-114">Définissez **demander confirmation avant de supprimer un déploiement existant** trop**True**.</span><span class="sxs-lookup"><span data-stu-id="d4c11-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="d4c11-115">Ce paramètre permet de tooensure vous ne supprimez accidentellement un déploiement existant dans Azure</span><span class="sxs-lookup"><span data-stu-id="d4c11-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="d4c11-116">Sélectionnez hello souhaité **configuration du Service** tooindicate la configuration de service que vous souhaitez toouse lorsque vous exécutez ou déboguez votre service cloud localement.</span><span class="sxs-lookup"><span data-stu-id="d4c11-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="d4c11-117">Pour plus d’informations sur la façon de toomodify une configuration de service pour un rôle, consultez [tooconfigure les rôles de hello pour Azure cloud service avec Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="d4c11-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="d4c11-118">Définissez **émulateur de stockage Azure de démarrer** trop**True** toostart l’émulateur de stockage Azure hello lorsque vous exécutez ou déboguez votre service cloud localement.</span><span class="sxs-lookup"><span data-stu-id="d4c11-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="d4c11-119">Définissez **considérer les avertissements comme des erreurs** trop**True** toomake que vous ne pouvez pas publier s’il existe des erreurs de validation de package.</span><span class="sxs-lookup"><span data-stu-id="d4c11-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="d4c11-120">Définissez **utiliser des ports du projet web** trop**True** toomake sûr que votre rôle web utilise hello même port à chaque démarrage local dans IIS Express.</span><span class="sxs-lookup"><span data-stu-id="d4c11-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="d4c11-121">Dans la barre d’outils de Visual Studio hello, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d4c11-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4c11-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4c11-122">Next steps</span></span>
- [<span data-ttu-id="d4c11-123">Configurer un projet Azure à l'aide de plusieurs configurations de service</span><span class="sxs-lookup"><span data-stu-id="d4c11-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

