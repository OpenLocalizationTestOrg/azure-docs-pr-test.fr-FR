---
title: "Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment gérer vos comptes de stockage Azure à l’aide de l’Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="273f5-103">Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="273f5-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="273f5-104">L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour gérer les comptes de stockage de leur compte Azure à partir de l’environnement de développement intégré (IDE) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="273f5-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="273f5-105">Créer un compte de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="273f5-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="273f5-106">Pour créer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="273f5-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="273f5-107">Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le kit de ressources Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="273f5-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="273f5-108">Dans la vue **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Comptes de stockage** puis cliquez sur **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="273f5-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Commande Créer un compte de stockage][CS01]

3. <span data-ttu-id="273f5-110">Dans la boîte de dialogue **Créer un compte de stockage**, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="273f5-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * <span data-ttu-id="273f5-112">**Nom** : spécifie le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="273f5-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="273f5-113">**Type de compte** : spécifie le type de compte de stockage à créer (par exemple, « Stockage Blob »).</span><span class="sxs-lookup"><span data-stu-id="273f5-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="273f5-114">Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="273f5-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="273f5-115">**Performances** : spécifie l’offre de compte de stockage de l’éditeur sélectionné qu’il faut utiliser (par exemple « Premium »).</span><span class="sxs-lookup"><span data-stu-id="273f5-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="273f5-116">Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="273f5-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="273f5-117">**Réplication** : spécifie la réplication pour le compte de stockage (par exemple, « Redondant dans une zone »).</span><span class="sxs-lookup"><span data-stu-id="273f5-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="273f5-118">Pour plus d’informations, voir [Réplication de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="273f5-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="273f5-119">**Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="273f5-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="273f5-120">**Emplacement** : spécifie l’emplacement où votre compte de stockage sera créé (par exemple « États-Unis de l’Ouest »).</span><span class="sxs-lookup"><span data-stu-id="273f5-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="273f5-121">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="273f5-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="273f5-122">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="273f5-122">Select one of the following options:</span></span>
      * <span data-ttu-id="273f5-123">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="273f5-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="273f5-124">**Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="273f5-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="273f5-125">Après avoir spécifié toutes les options ci-dessus, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="273f5-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="273f5-126">Créer un conteneur de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="273f5-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="273f5-127">Pour créer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="273f5-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="273f5-128">Dans l’Explorateur Azure, cliquez avec le bouton droit sur le compte de stockage dans lequel vous souhaitez créer un conteneur, puis cliquez sur **Créer un conteneur d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="273f5-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Commande de création d’un conteneur d’objets blob][CC01]

2. <span data-ttu-id="273f5-130">Dans la boîte de dialogue **Créer un conteneur d’objets blob**, spécifiez le nom de votre conteneur puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="273f5-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="273f5-131">Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, voir [Affectation de noms et de références aux conteneurs, objets blob et métadonnées].</span><span class="sxs-lookup"><span data-stu-id="273f5-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Boîte de dialogue de création d’un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="273f5-133">Supprimer un conteneur de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="273f5-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="273f5-134">Pour supprimer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="273f5-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="273f5-135">Dans l’Explorateur Azure, cliquez avec le bouton droit sur le conteneur de stockage, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="273f5-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Commande de suppression d’un conteneur de stockage][DC01]

2. <span data-ttu-id="273f5-137">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="273f5-137">In the confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="273f5-139">Supprimer un compte de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="273f5-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="273f5-140">Pour supprimer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="273f5-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="273f5-141">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="273f5-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menu de suppression d’un compte de stockage][DS01]

2. <span data-ttu-id="273f5-143">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="273f5-143">In the confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a><span data-ttu-id="273f5-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="273f5-145">Next steps</span></span>
<span data-ttu-id="273f5-146">Pour plus d’informations sur les comptes de stockage Azure, leurs tailles et leurs tarifications, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="273f5-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="273f5-147">[Introduction à Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="273f5-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="273f5-148">[À propos des comptes de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="273f5-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="273f5-149">Tailles des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="273f5-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="273f5-150">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="273f5-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="273f5-151">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="273f5-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="273f5-152">Tarification des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="273f5-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="273f5-153">[Tarification des comptes de stockage Windows]</span><span class="sxs-lookup"><span data-stu-id="273f5-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="273f5-154">[Tarification des comptes de stockage Linux]</span><span class="sxs-lookup"><span data-stu-id="273f5-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="273f5-155">Pour plus d’informations sur les kits de ressources Azure pour les environnements de développement intégré Java, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="273f5-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="273f5-156">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="273f5-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="273f5-157">[Nouveautés du Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="273f5-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="273f5-158">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="273f5-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="273f5-159">[Instructions de connexion pour le kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="273f5-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="273f5-160">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="273f5-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="273f5-161">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="273f5-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="273f5-162">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="273f5-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="273f5-163">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="273f5-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="273f5-164">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="273f5-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="273f5-165">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="273f5-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="273f5-166">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="273f5-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="273f5-167">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="273f5-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="273f5-168">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="273f5-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="273f5-169">[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="273f5-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="273f5-170">[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="273f5-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="273f5-171">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="273f5-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="273f5-172">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="273f5-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="273f5-173">[Instructions de connexion pour le kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="273f5-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="273f5-174">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="273f5-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="273f5-175">[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="273f5-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="273f5-176">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="273f5-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="273f5-177">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="273f5-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="273f5-178">[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="273f5-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="273f5-179">[Introduction à Microsoft Azure Storage]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="273f5-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="273f5-180">[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="273f5-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="273f5-181">[Réplication de Stockage Azure]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="273f5-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="273f5-182">[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="273f5-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="273f5-183">[Affectation de noms et de références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="273f5-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="273f5-184">[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="273f5-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="273f5-185">[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="273f5-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="273f5-186">[Tarification des comptes de stockage Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="273f5-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="273f5-187">[Tarification des comptes de stockage Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="273f5-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
