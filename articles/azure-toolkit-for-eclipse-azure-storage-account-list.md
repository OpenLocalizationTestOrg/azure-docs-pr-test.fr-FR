---
title: Liste des comptes Azure Storage
description: "Gérez les paramètres de votre compte de stockage à l'aide du kit de ressources Azure pour Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="4c260-103">Liste des comptes Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4c260-103">Azure Storage Account List</span></span>
<span data-ttu-id="4c260-104">Les comptes de stockage Azure permettent l'utilisation d'emplacements de téléchargement pour votre JDK, serveur d'applications et composants arbitraires, ainsi que pour stocker l'état lors de l'utilisation de la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="4c260-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="4c260-105">Eclipse conserve une liste des comptes de stockage connus qui sont disponibles pour vos projets dans votre espace de travail Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4c260-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="4c260-106">Pour ouvrir la boîte de dialogue **Comptes de stockage**, qui permet de gérer cette liste, dans Eclipse, cliquez sur **Fenêtre**, sur **Préférences**, développez **Azure**, puis cliquez sur **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="4c260-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="4c260-107">La boîte de dialogue **Comptes de stockage** est illustrée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4c260-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="4c260-108">Vous pouvez également ouvrir cette boîte de dialogue à partir du lien **Comptes** dans les boîtes de dialogue qui utilisent des comptes de stockage, comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4c260-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="4c260-109">Onglet **JDK** de la boîte de dialogue **Configuration du serveur**.</span><span class="sxs-lookup"><span data-stu-id="4c260-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="4c260-110">Onglet **Serveur** de la boîte de dialogue **Configuration du serveur**.</span><span class="sxs-lookup"><span data-stu-id="4c260-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="4c260-111">Boîte de dialogue **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="4c260-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="4c260-112">Boîte de dialogue des propriétés de **mise en cache** .</span><span class="sxs-lookup"><span data-stu-id="4c260-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="4c260-113">Pour importer vos comptes de stockage à l'aide d'un fichier de paramètres de publication</span><span class="sxs-lookup"><span data-stu-id="4c260-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="4c260-114">Dans la boîte de dialogue **Comptes de stockage**, cliquez sur **Importer à partir du fichier PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="4c260-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="4c260-115">(Ignorez cette étape si vous avez déjà enregistré un fichier de paramètres de publication sur votre ordinateur local). Dans la boîte de dialogue **Importer les informations d’abonnement**, cliquez sur **Télécharger le fichier PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="4c260-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="4c260-116">Si vous n’êtes pas encore connecté à votre compte Azure, vous y êtes maintenant invité.</span><span class="sxs-lookup"><span data-stu-id="4c260-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="4c260-117">Vous serez ensuite invité à enregistrer un fichier de paramètres de publication Azure.</span><span class="sxs-lookup"><span data-stu-id="4c260-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="4c260-118">(Vous pouvez ignorer les instructions affichées sur les pages d'ouverture de session ; elles sont fournies par le portail Azure et sont destinées aux utilisateurs de Visual Studio.) Enregistrez-le sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="4c260-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="4c260-119">Toujours dans la boîte de dialogue **Importer les informations d’abonnement**, cliquez sur le bouton **Parcourir**, sélectionnez le fichier de paramètres que vous avez enregistré localement, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="4c260-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="4c260-120">Cliquez sur **OK** pour fermer la boîte de dialogue **Importer les informations d’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4c260-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="4c260-121">Pour créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="4c260-121">To create a new storage account</span></span>
1. <span data-ttu-id="4c260-122">Dans la boîte de dialogue **Comptes de stockage**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4c260-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="4c260-123">Dans la boîte de dialogue **Ajouter un compte de stockage**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4c260-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="4c260-124">Dans la boîte de dialogue **Nouveau compte de stockage** , entrez des valeurs pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4c260-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="4c260-125">Nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-125">Storage account name.</span></span>

   * <span data-ttu-id="4c260-126">Emplacement du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-126">Location of the storage account.</span></span>

   * <span data-ttu-id="4c260-127">Description du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-127">Description of the storage account.</span></span>

   * <span data-ttu-id="4c260-128">Abonnement auquel appartient le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="4c260-129">Cliquez sur **OK** pour fermer la boîte de dialogue **Nouveau compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="4c260-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="4c260-130">La création de votre compte de stockage peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="4c260-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="4c260-131">Après sa création, cliquez sur **OK** pour fermer la boîte de dialogue **Ajouter un compte de stockage** : votre compte de stockage sera ajouté à la liste des comptes de stockage disponibles.</span><span class="sxs-lookup"><span data-stu-id="4c260-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="4c260-132">Pour ajouter un compte de stockage existant à la liste</span><span class="sxs-lookup"><span data-stu-id="4c260-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="4c260-133">Si vous ne disposez pas déjà d'un compte de stockage Azure, créez-en un en suivant les étapes indiquées dans la section **Pour créer un compte de stockage** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4c260-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="4c260-134">(Vous pouvez aussi créer un compte de stockage dans le [portail de gestion Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="4c260-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="4c260-135">Dans la boîte de dialogue **Comptes de stockage**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4c260-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="4c260-136">Dans la boîte de dialogue **Ajouter un compte de stockage**, entrez des valeurs pour le **nom** et la **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="4c260-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="4c260-137">La clé d'accès et le nom de compte doivent être ceux d'un compte de stockage Azure existant.</span><span class="sxs-lookup"><span data-stu-id="4c260-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="4c260-138">Utilisez la section **Stockage** du [portail de gestion Azure][Azure Management Portal] pour afficher les noms et les clés de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="4c260-139">La boîte de dialogue **Ajouter un compte de stockage** doit avoir l'aspect suivant.</span><span class="sxs-lookup"><span data-stu-id="4c260-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="4c260-140">Cliquez sur **OK** pour fermer la boîte de dialogue **Ajouter un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="4c260-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="4c260-141">Pour modifier un compte de stockage pour utiliser une nouvelle clé d'accès</span><span class="sxs-lookup"><span data-stu-id="4c260-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="4c260-142">Dans la boîte de dialogue **Comptes de stockage**, cliquez sur le compte de stockage que vous souhaitez modifier, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="4c260-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="4c260-143">Dans la boîte de dialogue **Modifier la clé d’accès du compte de stockage**, modifiez la valeur **Clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="4c260-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="4c260-144">Cliquez sur **OK** pour fermer la boîte de dialogue **Modifier la clé d’accès du compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="4c260-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="4c260-145">Pour supprimer un compte de stockage dans la liste d'Eclipse</span><span class="sxs-lookup"><span data-stu-id="4c260-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="4c260-146">Dans la boîte de dialogue **Comptes de stockage**, cliquez sur le compte de stockage que vous souhaitez modifier, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="4c260-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="4c260-147">Cliquez sur **OK** lorsque vous êtes invité à supprimer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4c260-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="4c260-148">La suppression du compte de stockage via la boîte de dialogue **Comptes de stockage** supprime uniquement celui-ci de la liste des comptes de stockage dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4c260-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="4c260-149">Elle ne supprime pas le compte de stockage de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4c260-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="4c260-150">En outre, le compte de stockage peut réapparaître dans votre liste si Eclipse recharge les détails de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c260-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="4c260-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4c260-151">See Also</span></span>
<span data-ttu-id="4c260-152">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4c260-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="4c260-153">[Installation du kit de ressources Azure pour Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4c260-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="4c260-154">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4c260-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="4c260-155">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="4c260-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
