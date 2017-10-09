---
title: aaaAzure liste des comptes de stockage
description: "Gérer les paramètres de votre compte de stockage à l’aide de hello boîte à outils Azure pour Eclipse"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="13e9f-103">Liste des comptes Azure Storage</span><span class="sxs-lookup"><span data-stu-id="13e9f-103">Azure Storage Account List</span></span>
<span data-ttu-id="13e9f-104">Activer des comptes de stockage Azure télécharger toobe emplacements utilisé pour votre JDK, serveur d’applications et composants arbitraires, ainsi que pour stocker l’état lors de l’utilisation de la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="13e9f-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="13e9f-105">Eclipse conserve une liste des comptes de stockage connus qui sont des projets tooyour disponibles dans votre espace de travail Eclipse.</span><span class="sxs-lookup"><span data-stu-id="13e9f-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="13e9f-106">tooopen hello **comptes de stockage** boîte de dialogue, qui est utilisé toomanage qui répertorient, dans Eclipse, cliquez sur **fenêtre**, cliquez sur **préférences**, développez **Azure** , puis cliquez sur **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="13e9f-107">Hello Voici hello **comptes de stockage** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="13e9f-108">Vous pouvez également ouvrir cette boîte de dialogue à partir d’un **comptes** lien dans les boîtes de dialogue qui utilisent des comptes de stockage, tels que les suivants hello :</span><span class="sxs-lookup"><span data-stu-id="13e9f-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="13e9f-109">Hello **JDK** onglet Hello **Configuration du serveur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="13e9f-110">Hello **Server** onglet Hello **Configuration du serveur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="13e9f-111">Hello **ajouter un composant** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="13e9f-112">Hello **mise en cache** boîte de dialogue Propriétés.</span><span class="sxs-lookup"><span data-stu-id="13e9f-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="13e9f-113">tooimport des comptes de votre stockage en utilisant un fichier de paramètres de publication</span><span class="sxs-lookup"><span data-stu-id="13e9f-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="13e9f-114">Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **importer à partir du fichier de paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="13e9f-115">(Ignorer cette étape si vous avez déjà enregistré un ordinateur local de publier les paramètres fichier tooyour). Bonjour **importation des informations d’abonnement** boîte de dialogue, cliquez sur **télécharger le fichier PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="13e9f-116">Si vous n’êtes pas encore connecté à votre compte Azure, vous serez invité à toolog dans.</span><span class="sxs-lookup"><span data-stu-id="13e9f-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="13e9f-117">Ensuite, vous êtes invité à entrer toosave Azure publier le fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="13e9f-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="13e9f-118">(Vous pouvez ignorer hello instructions sur les pages d’ouverture de session hello - ils sont fournis par hello portail Azure et sont destinées aux utilisateurs de Visual Studio) Enregistrez-le tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="13e9f-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="13e9f-119">Toujours en hello **importation des informations d’abonnement** boîte de dialogue, cliquez sur hello **Parcourir** bouton, hello sélectionnez Publier le fichier de paramètres que vous avez précédemment enregistré localement, puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="13e9f-120">Cliquez sur **OK** tooclose hello **importation des informations d’abonnement** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="13e9f-121">toocreate un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="13e9f-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="13e9f-122">Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="13e9f-123">Au sein de hello **ajouter un compte de stockage** boîte de dialogue, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="13e9f-124">Au sein de hello **nouveau compte de stockage** boîte de dialogue, spécifiez des valeurs pour les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="13e9f-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="13e9f-125">Nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13e9f-125">Storage account name.</span></span>

   * <span data-ttu-id="13e9f-126">Emplacement du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="13e9f-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="13e9f-127">Description du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="13e9f-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="13e9f-128">compte de stockage Hello abonnement toowhich hello appartient.</span><span class="sxs-lookup"><span data-stu-id="13e9f-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="13e9f-129">Cliquez sur **OK** tooclose hello **nouveau compte de stockage** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="13e9f-130">Il peut prendre plusieurs minutes avant que votre toobe de compte de stockage créé.</span><span class="sxs-lookup"><span data-stu-id="13e9f-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="13e9f-131">Après sa création, cliquez sur **OK** tooclose hello **ajouter un compte de stockage** boîte de dialogue et votre compte de stockage seront ajouté toohello la liste des comptes de stockage disponibles.</span><span class="sxs-lookup"><span data-stu-id="13e9f-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="13e9f-132">tooadd une liste de toohello de compte de stockage existant</span><span class="sxs-lookup"><span data-stu-id="13e9f-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="13e9f-133">Si vous ne figure pas un stockage Azure compte, créez-le en suivant les étapes de hello répertoriés dans hello **toocreate une nouvelle section de compte de stockage** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="13e9f-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="13e9f-134">(Vous pouvez également créer un compte de stockage à hello [portail de gestion Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="13e9f-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="13e9f-135">Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="13e9f-136">Au sein de hello **ajouter un compte de stockage** boîte de dialogue, entrez des valeurs pour **nom** et **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="13e9f-137">clé d’accès et de nom de compte Hello doit être d’un compte de stockage Azure existant.</span><span class="sxs-lookup"><span data-stu-id="13e9f-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="13e9f-138">Hello d’utilisation **stockage** section Hello [portail de gestion Azure] [ Azure Management Portal] tooview noms et des clés de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13e9f-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="13e9f-139">Votre **ajouter un compte de stockage** boîte de dialogue recherche similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="13e9f-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="13e9f-140">Cliquez sur **OK** tooclose hello **ajouter un compte de stockage** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="13e9f-141">toomodify un toouse de compte de stockage une nouvelle clé d’accès</span><span class="sxs-lookup"><span data-stu-id="13e9f-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="13e9f-142">Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur le compte de stockage hello que vous souhaitez tooedit, puis sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="13e9f-143">Au sein de hello **modifier compte clé d’accès** boîte de dialogue Modifier hello **clé d’accès** valeur.</span><span class="sxs-lookup"><span data-stu-id="13e9f-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="13e9f-144">Cliquez sur **OK** tooclose hello **clé de l’accès du compte de stockage modifier** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="13e9f-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="13e9f-145">tooremove un compte de stockage à partir de la liste d’Eclipse hello</span><span class="sxs-lookup"><span data-stu-id="13e9f-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="13e9f-146">Au sein de hello **comptes de stockage** boîte de dialogue, cliquez sur le compte de stockage hello que vous souhaitez tooedit, puis sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="13e9f-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="13e9f-147">Cliquez sur **OK** lorsque tooremove demandée hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13e9f-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="13e9f-148">Suppression de compte de stockage hello via hello **comptes de stockage** dialogue supprime uniquement à partir de la liste de hello des comptes de stockage visibles dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="13e9f-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="13e9f-149">Elle ne supprime pas le compte de stockage hello à partir de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="13e9f-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="13e9f-150">En outre, compte de stockage hello peut réapparaître dans votre liste lorsqu’Eclipse recharge les détails hello de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="13e9f-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="13e9f-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="13e9f-151">See Also</span></span>
<span data-ttu-id="13e9f-152">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13e9f-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="13e9f-153">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13e9f-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="13e9f-154">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13e9f-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="13e9f-155">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="13e9f-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
