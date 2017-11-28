---
title: "rôles aaaManaging dans Azure cloud services avec Visual Studio | Documents Microsoft"
description: "Découvrez comment tooadd et supprimer des rôles dans Azure cloud services avec Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="1ff2c-103">Gestion des rôles dans Azure Cloud Services avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ff2c-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="1ff2c-104">Après avoir créé votre service cloud Azure, vous pouvez ajouter de nouveaux rôles tooit ou supprimer des rôles existants.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="1ff2c-105">Vous pouvez également importer un projet existant et convertissez-le tooa rôle.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="1ff2c-106">Par exemple, vous pouvez importer une application web ASP.NET et la désigner comme rôle web.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="1ff2c-107">Ajout d’un rôle de tooan service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="1ff2c-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="1ff2c-108">Hello suit vous guide tout au long de l’ajout d’un web ou travail tooan Azure cloud service projet de rôle dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1ff2c-109">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1ff2c-110">Dans **l’Explorateur de solutions**, développez le nœud de projet hello</span><span class="sxs-lookup"><span data-stu-id="1ff2c-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="1ff2c-111">Avec le bouton hello **rôles** menu contextuel du nœud toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="1ff2c-112">Dans le menu contextuel de hello, sélectionnez **ajouter**, puis sélectionnez un rôle web existant ou un rôle de travail à partir de la solution actuelle de hello ou créer un projet de rôle web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="1ff2c-113">Vous pouvez également sélectionner un projet approprié, par exemple un projet d’application web ASP.NET, et l’associer à un projet de rôle.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Options de menu tooadd un projet de service cloud Azure rôle tooan](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="1ff2c-115">Suppression d’un rôle à partir d’un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="1ff2c-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="1ff2c-116">Hello étapes suivantes vous guident suppression d’un rôle web ou de travail à partir d’un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1ff2c-117">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1ff2c-118">Dans **l’Explorateur de solutions**, développez le nœud de projet hello</span><span class="sxs-lookup"><span data-stu-id="1ff2c-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="1ff2c-119">Développez hello **rôles** nœud.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="1ff2c-120">Nœud de hello contextuel vous souhaitez tooremove et, dans le menu contextuel de hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Options de menu tooadd un tooan de rôle service de cloud computing Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="1ff2c-122">Readding d’un projet de service cloud Azure rôle tooan</span><span class="sxs-lookup"><span data-stu-id="1ff2c-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="1ff2c-123">Si vous supprimez un rôle à partir de votre projet de service cloud, mais décidez ultérieurement de rôle hello tooadd toohello project, seuls déclaration de rôle hello et les attributs de base, tels que les points de terminaison et de diagnostics, sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="1ff2c-124">Aucune des ressources supplémentaires ou des références ne sont ajoutées toohello `ServiceDefinition.csdef` fichier ou toohello `ServiceConfiguration.cscfg` fichier.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="1ff2c-125">Si vous souhaitez tooadd ces informations, vous devez toomanually ajouter à nouveau à ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="1ff2c-126">Par exemple, vous pouvez supprimer un rôle de service web et décider ultérieurement de tooadd sauvegarde de ce rôle dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="1ff2c-127">Dans ce cas, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-127">If you do this, an error occurs.</span></span> <span data-ttu-id="1ff2c-128">tooprevent cette erreur, vous avez tooadd hello `<LocalResources>` élément présenté dans hello suivant XML soit de nouveau hello `ServiceDefinition.csdef` fichier.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="1ff2c-129">Utiliser le nom de rôle du service web hello que vous avez ajouté au projet de hello dans le cadre de l’attribut de nom hello pour hello hello  **<LocalStorage>**  élément.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="1ff2c-130">Dans cet exemple, le nom hello du rôle de service web hello est **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="1ff2c-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="1ff2c-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ff2c-131">Next steps</span></span>
- [<span data-ttu-id="1ff2c-132">Configurer des rôles de hello pour un service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ff2c-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
