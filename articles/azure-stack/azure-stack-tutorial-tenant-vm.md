---
title: "utilisateurs d’Azure pile aaaMake machines virtuelles disponibles tooyour | Documents Microsoft"
description: Didacticiel toomake virtuels disponibles sur la pile de Azure
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a><span data-ttu-id="af101-103">Rendre tooyour disponible des ordinateurs virtuels aux utilisateurs de pile de Azure</span><span class="sxs-lookup"><span data-stu-id="af101-103">Make virtual machines available tooyour Azure Stack users</span></span>
<span data-ttu-id="af101-104">En tant qu’un administrateur de cloud Azure pile, vous pouvez créer vos utilisateurs (clients tooas parfois visés) peuvent s’abonner à des offres.</span><span class="sxs-lookup"><span data-stu-id="af101-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred tooas tenants) can subscribe to.</span></span> <span data-ttu-id="af101-105">Avec leur abonnement, les utilisateurs peuvent utiliser les services Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="af101-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="af101-106">Cet article vous montre comment toocreate une offre, puis du tester.</span><span class="sxs-lookup"><span data-stu-id="af101-106">This article shows you how toocreate an offer, and then test it.</span></span> <span data-ttu-id="af101-107">Pour le test de hello, vous connectez-vous au portail toohello en tant qu’utilisateur, s’abonner toohello offre et ensuite créer un ordinateur virtuel à l’aide d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="af101-107">For hello test, you will log in toohello portal as a user, subscribe toohello offer, and then create a virtual machine using hello subscription.</span></span>

<span data-ttu-id="af101-108">Contenu :</span><span class="sxs-lookup"><span data-stu-id="af101-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af101-109">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="af101-109">Create an offer</span></span>
> * <span data-ttu-id="af101-110">Ajouter une image</span><span class="sxs-lookup"><span data-stu-id="af101-110">Add an image</span></span>
> * <span data-ttu-id="af101-111">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="af101-111">Test hello offer</span></span>


<span data-ttu-id="af101-112">Dans la pile d’Azure, les services sont remis toousers à l’aide d’abonnements, les offres et les plans.</span><span class="sxs-lookup"><span data-stu-id="af101-112">In Azure Stack, services are delivered toousers using subscriptions, offers, and plans.</span></span> <span data-ttu-id="af101-113">Les utilisateurs peuvent s’abonner à des offres toomultiple.</span><span class="sxs-lookup"><span data-stu-id="af101-113">Users can subscribe toomultiple offers.</span></span> <span data-ttu-id="af101-114">Les offres peuvent contenir un ou plusieurs plans, et les plans peuvent contenir un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="af101-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![Abonnements, offres et plans](media/azure-stack-key-features/image4.png)

<span data-ttu-id="af101-116">toolearn, voir [principales fonctionnalités et les concepts dans Azure pile](azure-stack-key-features.md).</span><span class="sxs-lookup"><span data-stu-id="af101-116">toolearn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="af101-117">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="af101-117">Create an offer</span></span>

<span data-ttu-id="af101-118">Il est maintenant possible d’effectuer toutes les étapes de préparation pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="af101-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="af101-119">Lorsque vous démarrez le processus de hello, vous êtes première offre de hello toocreate demandées, un plan et les quotas.</span><span class="sxs-lookup"><span data-stu-id="af101-119">When you start hello process, you are first prompted toocreate hello offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="af101-120">**Créer une offre**</span><span class="sxs-lookup"><span data-stu-id="af101-120">**Create an offer**</span></span>

   <span data-ttu-id="af101-121">Offres sont des groupes d’un ou plusieurs plans que toopurchase de toousers fournisseurs présents ou s’y abonner.</span><span class="sxs-lookup"><span data-stu-id="af101-121">Offers are groups of one or more plans that providers present toousers toopurchase or subscribe to.</span></span>

   <span data-ttu-id="af101-122">a.</span><span class="sxs-lookup"><span data-stu-id="af101-122">a.</span></span> <span data-ttu-id="af101-123">[Connectez-vous](azure-stack-connect-azure-stack.md) portal toohello comme un administrateur du cloud puis cliquez sur **nouveau** > **client offre + Plans** > **offrent**.</span><span class="sxs-lookup"><span data-stu-id="af101-123">[Sign in](azure-stack-connect-azure-stack.md) toohello portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="af101-124">![Nouvelle offre](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="af101-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="af101-125">b.</span><span class="sxs-lookup"><span data-stu-id="af101-125">b.</span></span> <span data-ttu-id="af101-126">Bonjour **offrent de nouveaux** section, renseignez **nom d’affichage** et **nom de la ressource**, puis sélectionnez un nouveau ou existant **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="af101-126">In hello **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="af101-127">Hello nom complet est le nom convivial de l’offre de hello.</span><span class="sxs-lookup"><span data-stu-id="af101-127">hello Display Name is hello offer's friendly name.</span></span> <span data-ttu-id="af101-128">Seul l’opérateur hello cloud peut voir hello nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="af101-128">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="af101-129">Son nom hello qu’administrateurs utiliser toowork hello offre une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af101-129">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![Nom complet](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="af101-131">c.</span><span class="sxs-lookup"><span data-stu-id="af101-131">c.</span></span> <span data-ttu-id="af101-132">Cliquez sur **plans de Base**et Bonjour **Plan** , cliquez sur **ajouter** tooadd une nouvelle offre de toohello de plan.</span><span class="sxs-lookup"><span data-stu-id="af101-132">Click **Base plans**, and in hello **Plan** section, click **Add** tooadd a new plan toohello offer.</span></span>

   ![Ajouter un plan](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="af101-134">d.</span><span class="sxs-lookup"><span data-stu-id="af101-134">d.</span></span> <span data-ttu-id="af101-135">Bonjour **nouveau Plan** section, renseignez **nom d’affichage** et **nom de la ressource**.</span><span class="sxs-lookup"><span data-stu-id="af101-135">In hello **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="af101-136">Hello nom complet est le nom convivial du plan hello que les utilisateurs voient.</span><span class="sxs-lookup"><span data-stu-id="af101-136">hello Display Name is hello plan's friendly name that users see.</span></span> <span data-ttu-id="af101-137">Seul l’opérateur hello cloud peut voir hello nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="af101-137">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="af101-138">Son nom hello que les opérateurs cloud utilisent toowork avec hello plan comme une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af101-138">It's hello name that cloud operators use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![Nom d’affichage du plan](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="af101-140">e.</span><span class="sxs-lookup"><span data-stu-id="af101-140">e.</span></span> <span data-ttu-id="af101-141">Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="af101-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![Services du plan](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="af101-143">f.</span><span class="sxs-lookup"><span data-stu-id="af101-143">f.</span></span> <span data-ttu-id="af101-144">Cliquez sur **Quotas**, puis sélectionnez hello premier service pour lequel vous souhaitez toocreate un quota.</span><span class="sxs-lookup"><span data-stu-id="af101-144">Click **Quotas**, and then select hello first service for which you want toocreate a quota.</span></span> <span data-ttu-id="af101-145">Pour un quota IaaS, suivez ces étapes pour les services de calcul, réseau et stockage hello.</span><span class="sxs-lookup"><span data-stu-id="af101-145">For an IaaS quota, follow these steps for hello Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="af101-146">Dans cet exemple, nous créons d’abord un quota pour le service de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="af101-146">In this example, we first create a quota for hello Compute service.</span></span> <span data-ttu-id="af101-147">Dans la liste d’espace de noms hello, sélectionnez hello **Microsoft.Compute** espace de noms, puis **créer nouveau quota**.</span><span class="sxs-lookup"><span data-stu-id="af101-147">In hello namespace list, select hello **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![Créer un quota](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="af101-149">g.</span><span class="sxs-lookup"><span data-stu-id="af101-149">g.</span></span> <span data-ttu-id="af101-150">Sur hello **créer quota** , tapez un nom pour le quota de hello et le jeu de paramètres souhaités pour le quota de hello et cliquez sur hello **OK**.</span><span class="sxs-lookup"><span data-stu-id="af101-150">On hello **Create quota** section, type a name for hello quota and set hello desired parameters for hello quota and click **OK**.</span></span>

   ![Nom du quota](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="af101-152">h.</span><span class="sxs-lookup"><span data-stu-id="af101-152">h.</span></span> <span data-ttu-id="af101-153">À présent, pour **Microsoft.Compute**, sélectionnez quota hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="af101-153">Now, for **Microsoft.Compute**, select hello quota that you created.</span></span>

   ![Sélectionner un quota](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="af101-155">Répétez ces étapes pour les services réseau et de stockage hello, puis cliquez sur **OK** sur hello **Quotas** section.</span><span class="sxs-lookup"><span data-stu-id="af101-155">Repeat these steps for hello Network and Storage services, and then click **OK** on hello **Quotas** section.</span></span>

   <span data-ttu-id="af101-156">i.</span><span class="sxs-lookup"><span data-stu-id="af101-156">i.</span></span> <span data-ttu-id="af101-157">Cliquez sur **OK** sur hello **nouveau plan** section.</span><span class="sxs-lookup"><span data-stu-id="af101-157">Click **OK** on hello **New plan** section.</span></span>

   <span data-ttu-id="af101-158">j.</span><span class="sxs-lookup"><span data-stu-id="af101-158">j.</span></span> <span data-ttu-id="af101-159">Sur hello **Plan** , sélectionnez le nouveau plan de hello et cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="af101-159">On hello **Plan** section, select hello new plan and click **Select**.</span></span>

   <span data-ttu-id="af101-160">k.</span><span class="sxs-lookup"><span data-stu-id="af101-160">k.</span></span> <span data-ttu-id="af101-161">Sur hello **nouvelle offre** , cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="af101-161">On hello **New offer** section, click **Create**.</span></span> <span data-ttu-id="af101-162">Vous voyez une notification lors de l’offre de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="af101-162">You see a notification when hello offer has been created.</span></span>

   <span data-ttu-id="af101-163">l.</span><span class="sxs-lookup"><span data-stu-id="af101-163">l.</span></span> <span data-ttu-id="af101-164">Cliquez sur tableau de bord hello, **offre** puis cliquez sur offre hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="af101-164">On hello dashboard menu, click **Offers** and then click hello offer you created.</span></span>

   <span data-ttu-id="af101-165">m.</span><span class="sxs-lookup"><span data-stu-id="af101-165">m.</span></span> <span data-ttu-id="af101-166">Cliquez sur **Changer l’état**, puis sur **Public**.</span><span class="sxs-lookup"><span data-stu-id="af101-166">Click **Change State**, and then click **Public**.</span></span>

   ![État Public](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="af101-168">Ajouter une image</span><span class="sxs-lookup"><span data-stu-id="af101-168">Add an image</span></span>

<span data-ttu-id="af101-169">Vous pouvez configurer des machines virtuelles, vous devez ajouter un marketplace d’Azure pile toohello image.</span><span class="sxs-lookup"><span data-stu-id="af101-169">Before you can provision virtual machines, you must add an image toohello Azure Stack marketplace.</span></span> <span data-ttu-id="af101-170">Vous pouvez ajouter l’image hello de votre choix, y compris les images Linux, à partir de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af101-170">You can add hello image of your choice, including Linux images, from hello Azure Marketplace.</span></span>

<span data-ttu-id="af101-171">Si vous opérez dans un scénario connecté et si vous avez enregistré votre instance de la pile d’Azure avec Azure, vous pouvez télécharger image de machine virtuelle de Windows Server 2016 hello de hello Azure Marketplace à l’aide des étapes hello Bonjour [télécharger éléments du Marketplace à partir d’Azure tooAzure pile](azure-stack-download-azure-marketplace-item.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="af101-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download hello Windows Server 2016 VM image from hello Azure Marketplace by using hello steps described in hello [Download marketplace items from Azure tooAzure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="af101-172">Pour plus d’informations sur l’ajout d’éléments différents toohello marketplace, consultez [hello Azure Marketplace de pile](azure-stack-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="af101-172">For information about adding different items toohello marketplace, see [hello Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="af101-173">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="af101-173">Test hello offer</span></span>

<span data-ttu-id="af101-174">Maintenant que vous avez créé une offre, vous pouvez le tester.</span><span class="sxs-lookup"><span data-stu-id="af101-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="af101-175">Connectez-vous en tant qu’utilisateur et vous abonner toohello offre et puis ajoutez un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="af101-175">Log in as a user and subscribe toohello offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="af101-176">**S’abonner tooan offre**</span><span class="sxs-lookup"><span data-stu-id="af101-176">**Subscribe tooan offer**</span></span>

   <span data-ttu-id="af101-177">Maintenant, vous pouvez consigner dans le portail de toohello en tant qu’une offre de tooan toosubscribe utilisateur.</span><span class="sxs-lookup"><span data-stu-id="af101-177">Now you can log in toohello portal as a user toosubscribe tooan offer.</span></span>

   <span data-ttu-id="af101-178">a.</span><span class="sxs-lookup"><span data-stu-id="af101-178">a.</span></span> <span data-ttu-id="af101-179">Sur l’ordinateur du Kit de déploiement de pile Azure hello, connectez-vous trop`https://portal.local.azurestack.external` comme utilisateur et cliquez sur **obtenir un abonnement**.</span><span class="sxs-lookup"><span data-stu-id="af101-179">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![Prendre un abonnement](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="af101-181">b.</span><span class="sxs-lookup"><span data-stu-id="af101-181">b.</span></span> <span data-ttu-id="af101-182">Bonjour **nom d’affichage** , tapez un nom pour votre abonnement, cliquez sur **offrent**, cliquez sur une des offres hello Bonjour **choisissez une offre** section, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="af101-182">In hello **Display Name** field, type a name for your subscription, click **Offer**, click one of hello offers in hello **Choose an offer** section, and then click **Create**.</span></span>

   ![Créer une offre](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="af101-184">c.</span><span class="sxs-lookup"><span data-stu-id="af101-184">c.</span></span> <span data-ttu-id="af101-185">abonnement de hello tooview que vous avez créé, cliquez sur **davantage de services**, cliquez sur **abonnements**, puis cliquez sur votre nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="af101-185">tooview hello subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="af101-186">Après que vous être abonné tooan offre, actualiser les toosee portail hello les services qui font partie d’un nouvel abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="af101-186">After you subscribe tooan offer, refresh hello portal toosee which services are part of hello new subscription.</span></span>

2. <span data-ttu-id="af101-187">**Approvisionner une machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="af101-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="af101-188">Maintenant vous pouvez vous connecter toohello portal comme une tooprovision utilisateur un ordinateur virtuel à l’aide d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="af101-188">Now you can log in toohello portal as a user tooprovision a virtual machine using hello subscription.</span></span> 

   <span data-ttu-id="af101-189">a.</span><span class="sxs-lookup"><span data-stu-id="af101-189">a.</span></span> <span data-ttu-id="af101-190">Sur l’ordinateur du Kit de déploiement de pile Azure hello, connectez-vous trop`https://portal.local.azurestack.external` en tant qu’utilisateur, puis cliquez sur **nouveau** > **de calcul** > **Datacenter de Windows Server 2016 Eval**.</span><span class="sxs-lookup"><span data-stu-id="af101-190">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="af101-191">b.</span><span class="sxs-lookup"><span data-stu-id="af101-191">b.</span></span> <span data-ttu-id="af101-192">Bonjour **notions de base** , tapez un **nom**, **nom d’utilisateur**, et **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="af101-192">In hello **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="af101-193">Pour **Type de disque de machine virtuelle**, choisissez **HDD**.</span><span class="sxs-lookup"><span data-stu-id="af101-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="af101-194">Choisissez un **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="af101-194">Choose a **Subscription**.</span></span> <span data-ttu-id="af101-195">Créez un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af101-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="af101-196">c.</span><span class="sxs-lookup"><span data-stu-id="af101-196">c.</span></span> <span data-ttu-id="af101-197">Bonjour **choisir une taille** , cliquez sur **base A1**, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="af101-197">In hello **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="af101-198">d.</span><span class="sxs-lookup"><span data-stu-id="af101-198">d.</span></span> <span data-ttu-id="af101-199">Bonjour **paramètres** , cliquez sur **réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="af101-199">In hello **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="af101-200">Bonjour **réseau virtuel de choisir** , cliquez sur **nouvel**.</span><span class="sxs-lookup"><span data-stu-id="af101-200">In hello **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="af101-201">Bonjour **créer un réseau virtuel** , acceptez toutes les valeurs par défaut de hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af101-201">In hello **Create virtual network** section, accept all hello defaults, and click **OK**.</span></span> <span data-ttu-id="af101-202">Bonjour **paramètres** , cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af101-202">In hello **Settings** section, click **OK**.</span></span>

   ![Création d’un réseau virtuel](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="af101-204">e.</span><span class="sxs-lookup"><span data-stu-id="af101-204">e.</span></span> <span data-ttu-id="af101-205">Bonjour **Résumé** , cliquez sur **OK** toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="af101-205">In hello **Summary** section, click **OK** toocreate hello virtual machine.</span></span>  

   <span data-ttu-id="af101-206">f.</span><span class="sxs-lookup"><span data-stu-id="af101-206">f.</span></span> <span data-ttu-id="af101-207">toosee votre nouvel ordinateur virtuel, cliquez sur **toutes les ressources**, puis recherchez l’ordinateur virtuel de hello et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="af101-207">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>

    ![Toutes les ressources](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="af101-209">Ce que vous avez appris dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="af101-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af101-210">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="af101-210">Create an offer</span></span>
> * <span data-ttu-id="af101-211">Ajouter une image</span><span class="sxs-lookup"><span data-stu-id="af101-211">Add an image</span></span>
> * <span data-ttu-id="af101-212">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="af101-212">Test hello offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af101-213">Rendre web, mobiles et utilisateurs d’Azure pile API apps tooyour disponibles</span><span class="sxs-lookup"><span data-stu-id="af101-213">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)
