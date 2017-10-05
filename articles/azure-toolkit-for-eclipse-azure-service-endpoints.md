---
title: Points de terminaison de service Azure
description: "Décrit les paramètres de point de terminaison de Service Azure dans la boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="f00ee-103">Points de terminaison de service Azure</span><span class="sxs-lookup"><span data-stu-id="f00ee-103">Azure Service Endpoints</span></span>
<span data-ttu-id="f00ee-104">Les points de terminaison de service Azure déterminent si votre application est déployée et gérée par la plateforme globale Azure, si elle fonctionne sur Azure géré par 21Vianet en Chine ou sur une plateforme Azure privée.</span><span class="sxs-lookup"><span data-stu-id="f00ee-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="f00ee-105">La boîte de dialogue **Points de terminaison de service** vous permet de spécifier les points de terminaison du service à utiliser.</span><span class="sxs-lookup"><span data-stu-id="f00ee-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="f00ee-106">Pour ouvrir la boîte de dialogue **Points de terminaison de service** dans Eclipse, cliquez sur **Fenêtre**, puis sur **Préférences**, développez **Azure**, puis cliquez sur **Points de terminaison de service**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="f00ee-107">La définition du champ **Ensemble actif** détermine les points de terminaison de service Azure qui seront utilisés pour les projets Azure dans votre espace de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="f00ee-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="f00ee-108">Le schéma qui suit représente la boîte de dialogue **Points de terminaison de Service** .</span><span class="sxs-lookup"><span data-stu-id="f00ee-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="f00ee-109">Pour définir les points de terminaison de service Azure</span><span class="sxs-lookup"><span data-stu-id="f00ee-109">To set the service endpoints</span></span>
<span data-ttu-id="f00ee-110">Dans la boîte de dialogue **Points de terminaison de service** , effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f00ee-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="f00ee-111">Si vous souhaitez utiliser la plateforme Azure globale, à partir de la liste déroulante **Ensemble actif**, sélectionnez **windowsazure.com**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="f00ee-112">Si vous souhaitez utiliser Azure sous 21Vianet en Chine, dans la liste déroulante **Ensemble actif**, sélectionnez **windowsazure.cn (Chine)**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="f00ee-113">Si vous souhaitez utiliser une plateforme Azure privée :</span><span class="sxs-lookup"><span data-stu-id="f00ee-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="f00ee-114">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="f00ee-115">Une boîte de dialogue s’ouvre, vous informant que la boîte de dialogue **Points de terminaison de service** va être fermée et le fichier d’ensemble de préférences s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="f00ee-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="f00ee-116">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-116">Click **OK**.</span></span>

  3. <span data-ttu-id="f00ee-117">Dans le fichier preferencesets.xml, créez un nouvel élément `preferenceset` .</span><span class="sxs-lookup"><span data-stu-id="f00ee-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="f00ee-118">Pour ce nouvel élément, créez les attributs `name`, `blob`, `management`, `portalURL` et `publishsettings`, puis ajoutez à ces dernières des valeurs qui correspondent à votre plateforme Azure privée.</span><span class="sxs-lookup"><span data-stu-id="f00ee-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="f00ee-119">Vous pouvez utiliser les valeurs fournies pour les éléments `preferenceset` existants en tant que modèles.</span><span class="sxs-lookup"><span data-stu-id="f00ee-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="f00ee-120">**Remarque** : la valeur utilisée pour l’attribut `blob` doit contenir le texte « blob » dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="f00ee-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="f00ee-121">Enregistrez et fermez preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="f00ee-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="f00ee-122">Rouvrez la boîte de dialogue **Points de terminaison de service** .</span><span class="sxs-lookup"><span data-stu-id="f00ee-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="f00ee-123">À partir de la liste déroulante **Ensemble actif**, sélectionnez l’ensemble actif que vous avez créé, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="f00ee-124">Une fois que vous avez créé votre élément de plateforme Azure privée `preferenceset`, vous pouvez modifier les valeurs qui lui sont affectées en cliquant sur le bouton **Modifier** situé dans la boîte de dialogue **Point de terminaison de service**.</span><span class="sxs-lookup"><span data-stu-id="f00ee-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="f00ee-125">Vous pouvez également créer plusieurs éléments de plateforme Azure privée `preferenceset` si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="f00ee-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="f00ee-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f00ee-126">See Also</span></span>
<span data-ttu-id="f00ee-127">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f00ee-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f00ee-128">[Installation du kit de ressources Azure pour Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f00ee-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="f00ee-129">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f00ee-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="f00ee-130">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f00ee-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
