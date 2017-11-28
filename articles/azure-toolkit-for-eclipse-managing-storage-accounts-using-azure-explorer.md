---
title: "les comptes de stockage aaaManage à l’aide de hello Explorateur Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toomanage votre stockage Azure des comptes à l’aide de hello Explorateur Azure pour Eclipse."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="dcdd8-103">Gérer les comptes de stockage à l’aide de hello Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="dcdd8-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="dcdd8-104">Hello Explorateur Azure, qui fait partie de hello boîte à outils Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour la gestion des comptes de stockage de leur compte Azure à partir d’à l’intérieur de hello Eclipse environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="dcdd8-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="dcdd8-105">Créer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="dcdd8-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="dcdd8-106">toocreate un compte de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="dcdd8-107">Se connecter à l’aide de hello tooyour compte Azure [instructions connectez-vous pour hello boîte à outils Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="dcdd8-108">Bonjour **Explorateur Azure** afficher, développez hello **Azure** nœud, avec le bouton droit **comptes de stockage**, puis cliquez sur **créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Commande Créer un compte de stockage][CS01]

3. <span data-ttu-id="dcdd8-110">Bonjour **créer un compte de stockage** boîte de dialogue, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * <span data-ttu-id="dcdd8-112">**Nom**: Spécifie le nom hello hello nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="dcdd8-113">**Abonnement**: Spécifie hello abonnement Azure que vous souhaitez toouse hello nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="dcdd8-114">**Groupe de ressources**: Spécifie le groupe de ressources hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="dcdd8-115">Sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="dcdd8-116">**Créer nouveau**: Spécifie que vous souhaitez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="dcdd8-117">**Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="dcdd8-118">**Région**: Spécifie l’emplacement de hello où votre compte de stockage sera créé (par exemple, « Ouest des États-Unis »).</span><span class="sxs-lookup"><span data-stu-id="dcdd8-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="dcdd8-119">**Type de compte**: Spécifie le type hello de toocreate de compte de stockage (par exemple, « stockage d’objets Blob »).</span><span class="sxs-lookup"><span data-stu-id="dcdd8-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="dcdd8-120">Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="dcdd8-121">**Performances**: Spécifie le compte de stockage de l’offre toouse à partir du serveur de publication sélectionné hello (par exemple, « Premium »).</span><span class="sxs-lookup"><span data-stu-id="dcdd8-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="dcdd8-122">Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="dcdd8-123">**Réplication**: Spécifie la réplication hello hello compte de stockage (par exemple, « redondance de Zone »).</span><span class="sxs-lookup"><span data-stu-id="dcdd8-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="dcdd8-124">Pour plus d’informations, consultez [Réplication de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="dcdd8-125">Lorsque vous avez spécifié toutes hello précédant options, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="dcdd8-126">Créer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="dcdd8-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="dcdd8-127">toocreate un conteneur de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="dcdd8-128">Bonjour **Explorateur Azure** afficher, cliquez sur le compte de stockage hello où vous souhaitez toocreate un conteneur, puis cliquez sur **créer un conteneur blob**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Commande Créer un conteneur d’objets blob][CC01]

2. <span data-ttu-id="dcdd8-130">Bonjour **créer un conteneur blob** boîte de dialogue, spécifiez hello votre conteneur, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="dcdd8-131">Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Boîte de dialogue Créer un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="dcdd8-133">Supprimer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="dcdd8-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="dcdd8-134">toodelete un conteneur de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="dcdd8-135">Bonjour **Explorateur Azure** afficher, cliquez sur le conteneur de stockage hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Commande Supprimer un conteneur de stockage][DC01]

2. <span data-ttu-id="dcdd8-137">Dans la fenêtre de confirmation hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-137">In hello confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="dcdd8-139">Supprimer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="dcdd8-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="dcdd8-140">toodelete un compte de stockage à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="dcdd8-141">Bonjour **Explorateur Azure** afficher, cliquez sur le compte de stockage hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Commande Supprimer un compte de stockage][DS01]

2. <span data-ttu-id="dcdd8-143">Dans la fenêtre de confirmation hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcdd8-143">In hello confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a><span data-ttu-id="dcdd8-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcdd8-145">Next steps</span></span>
<span data-ttu-id="dcdd8-146">Pour plus d’informations sur les comptes de stockage Azure, la taille et la tarification, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="dcdd8-147">[Introduction tooMicrosoft stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="dcdd8-148">[À propos des comptes de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="dcdd8-149">Tailles des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="dcdd8-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="dcdd8-150">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="dcdd8-151">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="dcdd8-152">Tarification des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="dcdd8-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="dcdd8-153">[Tarification des comptes de stockage Windows]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="dcdd8-154">[Tarification des comptes de stockage Linux]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="dcdd8-155">Pour plus d’informations sur les boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="dcdd8-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="dcdd8-156">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dcdd8-157">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dcdd8-158">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dcdd8-159">[instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="dcdd8-160">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="dcdd8-161">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dcdd8-162">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dcdd8-163">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dcdd8-164">[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="dcdd8-165">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="dcdd8-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="dcdd8-166">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="dcdd8-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[Introduction tooMicrosoft stockage Azure]: /azure/storage/storage-introduction
[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account
[Réplication de Stockage Azure]: /azure/storage/storage-redundancy
[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets
[Affectation de noms et références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des comptes de stockage Windows]: /pricing/details/virtual-machines/windows/
[Tarification des comptes de stockage Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png