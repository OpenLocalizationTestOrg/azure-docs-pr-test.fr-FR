---
title: "Accès à des clouds Azure privés avec Visual Studio | Microsoft Docs"
description: "Découvrez comment accéder aux ressources de cloud privé à l'aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: b2578c837732ab05d538e9b896ed3a3035075a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="795f5-103">Accès à des clouds privés Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="795f5-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="795f5-104">Par défaut, Visual Studio prend en charge les points de terminaison REST du cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="795f5-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="795f5-105">Cette rubrique explique comment utiliser votre certificat de cloud privé pour accéder au cloud privé et y interagir à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="795f5-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="795f5-106">Pour accéder à un cloud privé Azure dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="795f5-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="795f5-107">Dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885) du cloud privé, téléchargez votre fichier de paramètres de publication ou contactez votre administrateur pour obtenir un fichier de paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="795f5-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="795f5-108">Sur la version publique d'Azure, le lien de téléchargement est [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="795f5-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="795f5-109">(Le fichier téléchargé doit porter l’extension `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="795f5-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="795f5-110">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="795f5-110">Open Visual Studio</span></span>

1. <span data-ttu-id="795f5-111">Dans l’**Explorateur de recherche**, cliquez avec le bouton droit sur le nœud **Azure**, puis dans le menu contextuel, cliquez sur **Gérer et filtrer les abonnements**.</span><span class="sxs-lookup"><span data-stu-id="795f5-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Commande Gérer les abonnements](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="795f5-113">Dans la boîte de dialogue **Gérer les abonnements Microsoft Azure**, sélectionnez l’onglet **Certificats**, puis le bouton **Importer**.</span><span class="sxs-lookup"><span data-stu-id="795f5-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importation de certificats Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="795f5-115">Dans la boîte de dialogue **Importer les abonnements Microsoft Azure**, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="795f5-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Bouton Parcourir dans la boîte de dialogue Importer les abonnements Microsoft Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="795f5-117">Dans la boîte de dialogue **Ouvrir**, parcourez le répertoire dans lequel vous avez enregistré le fichier de paramètres de publication, sélectionnez ce dernier, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="795f5-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Sélection du fichier de paramètres de publication](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="795f5-119">Lorsque vous revenez à la boîte de dialogue **Importer les abonnements Microsoft Azure**, sélectionnez **Importer**.</span><span class="sxs-lookup"><span data-stu-id="795f5-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importation du fichier de paramètres de publication](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="795f5-121">Les certificats sont importés du fichier de paramètres de publication vers Visual Studio. Vous pouvez maintenant interagir avec vos ressources de cloud privé.</span><span class="sxs-lookup"><span data-stu-id="795f5-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="795f5-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="795f5-122">Next steps</span></span>
- [<span data-ttu-id="795f5-123">Publication d’un service cloud Azure depuis Visual Studio</span><span class="sxs-lookup"><span data-stu-id="795f5-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="795f5-124">[Téléchargement et importation des paramètres de publication et des informations d’abonnement](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="795f5-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
