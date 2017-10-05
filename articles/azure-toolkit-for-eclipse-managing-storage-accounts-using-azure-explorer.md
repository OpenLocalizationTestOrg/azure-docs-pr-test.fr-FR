---
title: "Gestion des comptes de stockage avec l’Explorateur Azure pour Eclipse | Microsoft Docs"
description: "Découvrez comment gérer vos comptes de stockage Azure à l’aide de l’Explorateur Azure pour Eclipse."
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="6030a-103">Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="6030a-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="6030a-104">L’Explorateur Azure, qui fait partie du kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer les comptes de stockage de leur compte Azure à partir de l’environnement de développement intégré (IDE) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6030a-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="6030a-105">Créer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="6030a-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="6030a-106">Pour créer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6030a-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6030a-107">Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le kit de ressources Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="6030a-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="6030a-108">Dans la vue **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Comptes de stockage** puis cliquez sur **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="6030a-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Commande Créer un compte de stockage][CS01]

3. <span data-ttu-id="6030a-110">Dans la boîte de dialogue **Créer un compte de stockage**, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6030a-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * <span data-ttu-id="6030a-112">**Nom** : spécifie le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6030a-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="6030a-113">**Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6030a-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="6030a-114">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6030a-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="6030a-115">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6030a-115">Select one of the following options:</span></span>
      * <span data-ttu-id="6030a-116">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6030a-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="6030a-117">**Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6030a-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="6030a-118">**Région** : spécifie l’emplacement où votre compte de stockage sera créé, par exemple « États-Unis de l’Ouest ».</span><span class="sxs-lookup"><span data-stu-id="6030a-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="6030a-119">**Type de compte** : spécifie le type de compte de stockage à créer, par exemple « Stockage Blob ».</span><span class="sxs-lookup"><span data-stu-id="6030a-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="6030a-120">Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="6030a-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="6030a-121">**Performances** : spécifie l’offre de compte de stockage de l’éditeur sélectionné qu’il faut utiliser (par exemple « Premium »).</span><span class="sxs-lookup"><span data-stu-id="6030a-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="6030a-122">Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="6030a-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="6030a-123">**Réplication** : spécifie la réplication pour le compte de stockage (par exemple, « Redondant dans une zone »).</span><span class="sxs-lookup"><span data-stu-id="6030a-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="6030a-124">Pour plus d’informations, consultez [Réplication de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="6030a-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="6030a-125">Après avoir spécifié toutes les options ci-dessus, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6030a-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="6030a-126">Créer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="6030a-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="6030a-127">Pour créer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6030a-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6030a-128">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage où vous voulez créer un conteneur puis cliquez sur **Créer un conteneur d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="6030a-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Commande Créer un conteneur d’objets blob][CC01]

2. <span data-ttu-id="6030a-130">Dans la boîte de dialogue **Créer un conteneur d’objets blob**, spécifiez le nom de votre conteneur puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6030a-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="6030a-131">Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées].</span><span class="sxs-lookup"><span data-stu-id="6030a-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Boîte de dialogue Créer un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="6030a-133">Supprimer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="6030a-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="6030a-134">Pour supprimer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6030a-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6030a-135">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le conteneur de stockage puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6030a-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Commande Supprimer un conteneur de stockage][DC01]

2. <span data-ttu-id="6030a-137">Dans la fenêtre de confirmation, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6030a-137">In the confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="6030a-139">Supprimer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="6030a-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="6030a-140">Pour supprimer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6030a-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6030a-141">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6030a-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Commande Supprimer un compte de stockage][DS01]

2. <span data-ttu-id="6030a-143">Dans la fenêtre de confirmation, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6030a-143">In the confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a><span data-ttu-id="6030a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6030a-145">Next steps</span></span>
<span data-ttu-id="6030a-146">Pour plus d’informations sur les comptes de stockage Azure, leurs tailles et leurs tarifications, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="6030a-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="6030a-147">[Introduction à Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="6030a-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="6030a-148">[À propos des comptes de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="6030a-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="6030a-149">Tailles des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6030a-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="6030a-150">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="6030a-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="6030a-151">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="6030a-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="6030a-152">Tarification des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6030a-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="6030a-153">[Tarification des comptes de stockage Windows]</span><span class="sxs-lookup"><span data-stu-id="6030a-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="6030a-154">[Tarification des comptes de stockage Linux]</span><span class="sxs-lookup"><span data-stu-id="6030a-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="6030a-155">Pour plus d’informations sur les kits de ressources Azure pour les environnements de développement intégré Java, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="6030a-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="6030a-156">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6030a-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6030a-157">[Nouveautés du Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6030a-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6030a-158">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6030a-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6030a-159">[Instructions de connexion pour le kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6030a-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6030a-160">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6030a-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="6030a-161">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6030a-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6030a-162">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6030a-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6030a-163">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6030a-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6030a-164">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6030a-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6030a-165">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6030a-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="6030a-166">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="6030a-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="6030a-167">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="6030a-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="6030a-168">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="6030a-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="6030a-169">[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6030a-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6030a-170">[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6030a-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6030a-171">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="6030a-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="6030a-172">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="6030a-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="6030a-173">[Instructions de connexion pour le kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6030a-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="6030a-174">[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6030a-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="6030a-175">[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6030a-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="6030a-176">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6030a-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="6030a-177">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="6030a-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="6030a-178">[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="6030a-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="6030a-179">[Introduction à Microsoft Azure Storage]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="6030a-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="6030a-180">[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="6030a-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="6030a-181">[Réplication de Stockage Azure]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="6030a-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="6030a-182">[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="6030a-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="6030a-183">[Affectation de noms et références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="6030a-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="6030a-184">[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="6030a-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="6030a-185">[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="6030a-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="6030a-186">[Tarification des comptes de stockage Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="6030a-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="6030a-187">[Tarification des comptes de stockage Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="6030a-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
