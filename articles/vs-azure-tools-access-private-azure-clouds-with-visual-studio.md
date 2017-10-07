---
title: "aaaAccessing clouds privés Azure avec Visual Studio | Documents Microsoft"
description: "Découvrez les ressources de cloud privé de tooaccess à l’aide de Visual Studio."
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
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="01ec6-103">Accès à des clouds privés Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01ec6-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="01ec6-104">Par défaut, Visual Studio prend en charge les points de terminaison REST du cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="01ec6-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="01ec6-105">Dans cette rubrique, vous apprendrez comment toouse votre private cloud du certificat tooaccess - et interagir avec - hello cloud privé à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01ec6-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="01ec6-106">tooaccess un privé Azure cloud dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01ec6-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="01ec6-107">Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885) pour le cloud privé de hello, téléchargez votre fichier de paramètres de publication, ou contactez votre administrateur pour un fichier de paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="01ec6-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="01ec6-108">Sur la version publique de hello d’Azure, hello toodownload lien il s’agit de [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="01ec6-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="01ec6-109">(fichier téléchargé de hello doit avoir une extension `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="01ec6-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="01ec6-110">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01ec6-110">Open Visual Studio</span></span>

1. <span data-ttu-id="01ec6-111">Dans **l’Explorateur de serveurs**, avec le bouton hello **Azure** nœud et, dans le menu contextuel de hello, sélectionnez **gérer et filtrer les abonnements**.</span><span class="sxs-lookup"><span data-stu-id="01ec6-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Commande Gérer les abonnements](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="01ec6-113">Bonjour **gérer les abonnements Microsoft Azure** boîte de dialogue, sélectionnez hello **certificats** onglet, puis sélectionnez **importation**.</span><span class="sxs-lookup"><span data-stu-id="01ec6-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importation de certificats Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="01ec6-115">Bonjour **les abonnements Microsoft Azure Import** boîte de dialogue, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="01ec6-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Bouton de boîte de dialogue Importer les abonnements Microsoft Azure hello Parcourir](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="01ec6-117">Bonjour **ouvrir** boîte de dialogue Parcourir toohello répertoire dans lequel vous hello enregistré fichier publish-settings, sélectionnez hello fichier et sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="01ec6-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Sélectionnez le fichier de paramètres de publication hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="01ec6-119">Lorsque retourné toohello **les abonnements Microsoft Azure Import** boîte de dialogue, sélectionnez **importation**.</span><span class="sxs-lookup"><span data-stu-id="01ec6-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Fichier d’importation de paramètres de publication hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="01ec6-121">certificats de Hello sont importées à partir du fichier de paramètres de publication hello dans Visual Studio, et vous pouvez maintenant interagir avec vos ressources de cloud privé.</span><span class="sxs-lookup"><span data-stu-id="01ec6-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="01ec6-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01ec6-122">Next steps</span></span>
- [<span data-ttu-id="01ec6-123">Publication tooan Azure Cloud Service à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01ec6-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="01ec6-124">[Téléchargement et importation des paramètres de publication et des informations d’abonnement](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="01ec6-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
