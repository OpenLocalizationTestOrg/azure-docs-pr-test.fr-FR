---
title: aaaAzure points de terminaison de Service
description: "Décrit les paramètres de point de terminaison de Service Azure hello Bonjour boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="25357-103">Points de terminaison de service Azure</span><span class="sxs-lookup"><span data-stu-id="25357-103">Azure Service Endpoints</span></span>
<span data-ttu-id="25357-104">Points de terminaison de service Azure déterminent que si votre application est déployée tooand géré par la plateforme Azure globale de hello, Azure géré par 21Vianet en Chine ou privée plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="25357-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="25357-105">Hello **points de terminaison de Service** boîte de dialogue vous permet de toospecify dont vous souhaitez toouse des points de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="25357-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="25357-106">tooopen hello **points de terminaison de Service** boîte de dialogue, dans Eclipse, cliquez sur **fenêtre**, cliquez sur **préférences**, développez **Azure**, puis cliquez sur **Points de terminaison de service**.</span><span class="sxs-lookup"><span data-stu-id="25357-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="25357-107">Hello du paramètre **ensemble actif** champ détermine le service Azure qui seront utilisés pour hello points de terminaison Azure projets dans votre espace de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="25357-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="25357-108">Hello Voici hello **points de terminaison de Service** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25357-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="25357-109">points de terminaison de service tooset hello</span><span class="sxs-lookup"><span data-stu-id="25357-109">tooset hello service endpoints</span></span>
<span data-ttu-id="25357-110">Bonjour **points de terminaison de Service** boîte de dialogue, effectuez l’une de hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="25357-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="25357-111">Si vous souhaitez toouse hello plateforme Azure globale, à partir de hello **ensemble actif** liste déroulante, sélectionnez **windowsazure.com** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="25357-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="25357-112">Si vous souhaitez toouse Azure géré par 21Vianet en Chine, à partir de hello **ensemble actif** liste déroulante, sélectionnez **windowsazure.cn (China)** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="25357-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="25357-113">Si vous souhaitez toouse une plateforme Azure privée :</span><span class="sxs-lookup"><span data-stu-id="25357-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="25357-114">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="25357-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="25357-115">Une boîte de dialogue s’ouvre, vous informant que hello **points de terminaison de Service** boîte de dialogue va être fermée et hello préférence jeux de fichier s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="25357-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="25357-116">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="25357-116">Click **OK**.</span></span>

  3. <span data-ttu-id="25357-117">Dans le fichier preferencesets.xml de hello, créez un `preferenceset` élément.</span><span class="sxs-lookup"><span data-stu-id="25357-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="25357-118">Pour ce nouvel élément, créer `name`, `blob`, `management`, `portalURL` et `publishsettings` des attributs et ajouter des valeurs qui correspondent tooyour de plateforme Azure privée.</span><span class="sxs-lookup"><span data-stu-id="25357-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="25357-119">Vous pouvez utiliser les valeurs hello fournis hello existantes `preferenceset` éléments en tant que modèles.</span><span class="sxs-lookup"><span data-stu-id="25357-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="25357-120">**Remarque**: hello valeur utilisée pour hello `blob` attribut doit contenir le texte hello « blob » dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="25357-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="25357-121">Enregistrez et fermez preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="25357-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="25357-122">Rouvrez hello **points de terminaison de Service** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25357-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="25357-123">À partir de hello **ensemble actif** liste déroulante, sélectionnez hello actif défini que vous créé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="25357-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="25357-124">Une fois que vous avez créé votre plateforme Azure privée `preferenceset` élément, vous pouvez modifier tooit de valeurs affectées hello en cliquant sur hello **modifier** bouton Bonjour **point de terminaison de Services** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25357-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="25357-125">Vous pouvez également créer plusieurs éléments de plateforme Azure privée `preferenceset` si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="25357-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="25357-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="25357-126">See Also</span></span>
<span data-ttu-id="25357-127">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="25357-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="25357-128">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="25357-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="25357-129">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="25357-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="25357-130">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="25357-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
