---
title: "Délégation des offres dans Azure Stack | Microsoft Docs"
description: "Découvrez comment placer d’autres personnes en charge de la création d’offres et de l’inscription des utilisateurs."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: c56c0669cbcd66fe1d7177846e02ba28838c0544
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="082f8-103">Délégation des offres dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="082f8-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="082f8-104">En tant qu’opérateur cloud Azure Stack, vous souhaitez souvent placer d’autres personnes en charge de la création d’offres et de l’inscription des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="082f8-104">As the Azure Stack cloud operator, you often want to put other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="082f8-105">Par exemple, si vous êtes un fournisseur de services et souhaitez que les revendeurs inscrivent les clients et les gèrent à votre place.</span><span class="sxs-lookup"><span data-stu-id="082f8-105">For example, if you are a service provider and you want resellers to sign up customers and manage them on your behalf.</span></span> <span data-ttu-id="082f8-106">Cela peut également être le cas dans une entreprise si vous faites partie d’un groupe informatique centralisé et souhaitez que des départements ou des filiales inscrivent les utilisateurs sans votre intervention.</span><span class="sxs-lookup"><span data-stu-id="082f8-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries to sign up users without your intervention.</span></span>

<span data-ttu-id="082f8-107">La délégation vous aide dans ces tâches, ce qui vous permet d’atteindre et de gérer plus d’utilisateurs que vous ne pourriez le faire directement.</span><span class="sxs-lookup"><span data-stu-id="082f8-107">Delegation helps you with these tasks, helping you to reach and manage more users than you would be able to do directly.</span></span> <span data-ttu-id="082f8-108">L’illustration suivante montre un niveau de délégation, mais Azure Stack prend en charge plusieurs niveaux.</span><span class="sxs-lookup"><span data-stu-id="082f8-108">The following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="082f8-109">Les fournisseurs délégués peuvent à leur tour déléguer à d’autres fournisseurs, et ce sur jusqu’à cinq niveaux.</span><span class="sxs-lookup"><span data-stu-id="082f8-109">Delegated providers can in turn delegate to other providers, up to five levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="082f8-110">Les opérateurs cloud Azure Stack peuvent déléguer la création d’offres et de locataires à d’autres utilisateurs à l’aide de la fonctionnalité de délégation.</span><span class="sxs-lookup"><span data-stu-id="082f8-110">Azure Stack cloud operators can delegate the creation of offers and tenants to other users by using the delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="082f8-111">Rôles et étapes de la délégation</span><span class="sxs-lookup"><span data-stu-id="082f8-111">Roles and steps in delegation</span></span>
<span data-ttu-id="082f8-112">Pour comprendre la délégation, gardez à l’esprit qu’elle comprend trois rôles :</span><span class="sxs-lookup"><span data-stu-id="082f8-112">To understand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="082f8-113">**L’opérateur cloud** gère l’infrastructure Azure Stack, crée un modèle d’offre et délègue à d’autres la responsabilité de proposer l’offre à leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="082f8-113">The **cloud operator** manages the Azure Stack infrastructure, creates an offer template, and delegates others to offer it to their users.</span></span>
* <span data-ttu-id="082f8-114">Les administrateurs délégués cloud sont appelés **déléguée fournisseurs**.</span><span class="sxs-lookup"><span data-stu-id="082f8-114">The delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="082f8-115">Ils peuvent appartenir à d’autres organisations (comme d’autres locataires Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="082f8-115">They can belong to other organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="082f8-116">Les **utilisateurs** s’inscrivent aux offres et les utilisent pour gérer leurs charges de travail, la création de machines virtuelles, le stockage des données, etc.</span><span class="sxs-lookup"><span data-stu-id="082f8-116">**Users** sign up for the offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="082f8-117">Comme indiqué dans l’illustration suivante, la configuration de la délégation inclut deux étapes.</span><span class="sxs-lookup"><span data-stu-id="082f8-117">As shown in the following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="082f8-118">**Identifier les fournisseurs délégués** en les abonnant à une offre basée sur un plan qui contient uniquement le service d’abonnements.</span><span class="sxs-lookup"><span data-stu-id="082f8-118">**Identify the delegated providers** by subscribing them to an offer based on a plan that contains only the subscriptions service.</span></span>
   <span data-ttu-id="082f8-119">D’acquérir certaines des fonctionnalités de l’administrateur du cloud, y compris la possibilité d’étendre les offres et de déconnecter des utilisateurs pour les utilisateurs de s’abonner à cette offre.</span><span class="sxs-lookup"><span data-stu-id="082f8-119">Users who subscribe to this offer acquire some of the cloud administrator’s capabilities, including the ability to extend offers and sign users up for them.</span></span>
2. <span data-ttu-id="082f8-120">**Déléguer une offre au fournisseur délégué**, cette offre fonctionne comme un modèle concernant ce que le fournisseur délégué peut offrir.</span><span class="sxs-lookup"><span data-stu-id="082f8-120">**Delegate an offer to the delegated provider**, this offer functions as a template for what the delegated provider can offer.</span></span> <span data-ttu-id="082f8-121">Le fournisseur délégué est désormais en mesure de prendre l’offre, de choisir un nom pour celle-ci (mais pas d’en modifier les services et les quotas) et de la proposer aux clients.</span><span class="sxs-lookup"><span data-stu-id="082f8-121">The delegated provider is now able to take the offer, choose a name for it (but not change its services and quotas), and offer it to customers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="082f8-122">Pour agir en tant que fournisseurs délégués, les utilisateurs doivent établir une relation avec le fournisseur principal ; en d’autres termes, ils doivent créer un abonnement.</span><span class="sxs-lookup"><span data-stu-id="082f8-122">To act as delegated providers, users need to establish a relationship with the main provider; in other words, they need to create a subscription.</span></span> <span data-ttu-id="082f8-123">Dans ce scénario, cet abonnement identifie les fournisseurs délégués comme ayant le droit de présenter des offres pour le compte du fournisseur principal.</span><span class="sxs-lookup"><span data-stu-id="082f8-123">In this scenario, this subscription identifies the delegated providers as having the right to present offers on behalf of the main provider.</span></span>

<span data-ttu-id="082f8-124">Une fois que cette relation est établie, l’opérateur cloud peut déléguer une offre au fournisseur délégué.</span><span class="sxs-lookup"><span data-stu-id="082f8-124">Once this relationship is established, the cloud operator can delegate an offer to the delegated provider.</span></span> <span data-ttu-id="082f8-125">Le fournisseur délégué est désormais en mesure de prendre l’offre, de la renommer (sans en modifier la substance) et de la proposer à ses clients.</span><span class="sxs-lookup"><span data-stu-id="082f8-125">The delegated provider is now able to take the offer, rename it (but not change its substance), and offer it to its customers.</span></span>

<span data-ttu-id="082f8-126">Les sections suivantes expliquent comment établir un fournisseur délégué, déléguer une offre et vérifier que les utilisateurs peuvent s’y inscrire.</span><span class="sxs-lookup"><span data-stu-id="082f8-126">The following sections describe how to establish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="082f8-127">Configurer les rôles</span><span class="sxs-lookup"><span data-stu-id="082f8-127">Set up roles</span></span>

<span data-ttu-id="082f8-128">Pour voir un fournisseur délégué au travail, vous avez besoin de comptes Azure Active Directory supplémentaires en plus de votre compte d’opérateur cloud.</span><span class="sxs-lookup"><span data-stu-id="082f8-128">To see a delegated provider at work, you need additional Azure Active Directory accounts in addition to your cloud operator account.</span></span> <span data-ttu-id="082f8-129">Si vous n’en avez pas, créez les deux comptes.</span><span class="sxs-lookup"><span data-stu-id="082f8-129">If you do not have them, create the two accounts.</span></span> <span data-ttu-id="082f8-130">Les comptes peuvent appartenir à n’importe quel client AAD.</span><span class="sxs-lookup"><span data-stu-id="082f8-130">The accounts can belong to any AAD tenant.</span></span> <span data-ttu-id="082f8-131">Nous les appelons le fournisseur délégué (DP) et l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="082f8-131">We refer to them as the delegated provider (DP) and the user.</span></span>

| <span data-ttu-id="082f8-132">**Rôle**</span><span class="sxs-lookup"><span data-stu-id="082f8-132">**Role**</span></span> | <span data-ttu-id="082f8-133">**Droits d’organisation**</span><span class="sxs-lookup"><span data-stu-id="082f8-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="082f8-134">Fournisseur délégué</span><span class="sxs-lookup"><span data-stu-id="082f8-134">Delegated Provider</span></span> |<span data-ttu-id="082f8-135">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="082f8-135">User</span></span> |
| <span data-ttu-id="082f8-136">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="082f8-136">User</span></span> |<span data-ttu-id="082f8-137">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="082f8-137">User</span></span> |

## <a name="identify-the-delegated-providers"></a><span data-ttu-id="082f8-138">Identifier les fournisseurs délégués</span><span class="sxs-lookup"><span data-stu-id="082f8-138">Identify the delegated providers</span></span>
1. <span data-ttu-id="082f8-139">Connectez-vous en tant qu’opérateur cloud.</span><span class="sxs-lookup"><span data-stu-id="082f8-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="082f8-140">Créez l’offre qui permet aux utilisateurs de devenir des fournisseurs délégués.</span><span class="sxs-lookup"><span data-stu-id="082f8-140">Create the offer that enables users to become delegated providers.</span></span> <span data-ttu-id="082f8-141">Pour ce faire, vous devez créer un plan et une offre basée sur celui-ci :</span><span class="sxs-lookup"><span data-stu-id="082f8-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="082f8-142">a.</span><span class="sxs-lookup"><span data-stu-id="082f8-142">a.</span></span>  <span data-ttu-id="082f8-143">[Créer un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="082f8-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="082f8-144">Ce plan doit inclure uniquement le service d’abonnements.</span><span class="sxs-lookup"><span data-stu-id="082f8-144">This plan should include only the subscriptions service.</span></span> <span data-ttu-id="082f8-145">Dans cet article, nous utilisons un plan appelé PlanForDelegation.</span><span class="sxs-lookup"><span data-stu-id="082f8-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="082f8-146">b.</span><span class="sxs-lookup"><span data-stu-id="082f8-146">b.</span></span>  <span data-ttu-id="082f8-147">[Créer une offre](azure-stack-create-offer.md) basée sur ce plan.</span><span class="sxs-lookup"><span data-stu-id="082f8-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="082f8-148">Dans cet article, nous utilisons une offre appelée OfferToDP.</span><span class="sxs-lookup"><span data-stu-id="082f8-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="082f8-149">c.</span><span class="sxs-lookup"><span data-stu-id="082f8-149">c.</span></span>  <span data-ttu-id="082f8-150">Une fois la création de l’offre terminée, ajoutez le fournisseur délégué en tant qu’abonné à cette offre en cliquant sur **Abonnements** &gt; **Ajouter** &gt; **Nouvel abonnement client**.</span><span class="sxs-lookup"><span data-stu-id="082f8-150">Once the creation of the offer is complete, add the delegated provider as a subscriber to this offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="082f8-151">Comme avec toutes les offres Azure Stack, vous avez la possibilité de rendre l’offre publique et de laisser les utilisateurs y souscrire, ou de conserver l’offre comme privée et demander à l’opérateur cloud de gérer l’inscription.</span><span class="sxs-lookup"><span data-stu-id="082f8-151">As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and have the cloud operator manage the sign-up.</span></span> <span data-ttu-id="082f8-152">Les fournisseurs délégués appartiennent généralement à un petit groupe et vous souhaitez contrôler qui y est admis, donc le fait de conserver cette offre privée est logique dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="082f8-152">Delegated providers are usually a small group and you want to control who is admitted to it, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-the-delegated-offer"></a><span data-ttu-id="082f8-153">L’opérateur cloud crée l’offre déléguée</span><span class="sxs-lookup"><span data-stu-id="082f8-153">Cloud operator creates the delegated offer</span></span>

<span data-ttu-id="082f8-154">Vous avez désormais établi votre fournisseur délégué.</span><span class="sxs-lookup"><span data-stu-id="082f8-154">You have now established your delegated provider.</span></span> <span data-ttu-id="082f8-155">L’étape suivante consiste à créer le plan et l’offre que vous allez déléguer et que vos clients utiliseront.</span><span class="sxs-lookup"><span data-stu-id="082f8-155">The next step is to create the plan and offer that you are going to delegate, and which your customers will use.</span></span> <span data-ttu-id="082f8-156">Vous devez définir cette offre telle que vous souhaitez que les clients la voient, car le fournisseur délégué ne sera pas en mesure d’en modifier les plans et les quotas.</span><span class="sxs-lookup"><span data-stu-id="082f8-156">You should define this offer exactly as you want the customers to see it, because the delegated provider will not be able to change the plans and quotas it includes.</span></span>

1. <span data-ttu-id="082f8-157">En tant qu’opérateur cloud, [créez un plan](azure-stack-create-plan.md) et [une offre](azure-stack-create-offer.md) basée sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="082f8-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="082f8-158">Dans cet article, nous utilisons une offre appelée DelegatedOffer.</span><span class="sxs-lookup"><span data-stu-id="082f8-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="082f8-159">Cette offre ne doit pas nécessairement être publique.</span><span class="sxs-lookup"><span data-stu-id="082f8-159">This offer does not have to be public.</span></span> <span data-ttu-id="082f8-160">Elle peut être rendue publique si vous le souhaitez, mais, dans la plupart des cas, vous souhaitez que seuls les fournisseurs délégués y aient accès.</span><span class="sxs-lookup"><span data-stu-id="082f8-160">It can be made public if you choose, but, in most cases, you only want delegated providers to have access to it.</span></span> <span data-ttu-id="082f8-161">Une fois que vous déléguez une offre privée comme décrit dans les étapes suivantes, le fournisseur délégué y a accès.</span><span class="sxs-lookup"><span data-stu-id="082f8-161">Once you delegate a private offer as described in the following steps, the delegated provider has access to it.</span></span>
   > 
   > 
1. <span data-ttu-id="082f8-162">Déléguez l’offre.</span><span class="sxs-lookup"><span data-stu-id="082f8-162">Delegate the offer.</span></span> <span data-ttu-id="082f8-163">Accédez à DelegatedOffer et, dans le volet Paramètres, cliquez sur **Fournisseurs délégués** &gt; **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="082f8-163">Go to DelegatedOffer, and in the Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="082f8-164">Sélectionnez l’abonnement du fournisseur délégué dans la zone de liste déroulante et cliquez sur **Déléguer**.</span><span class="sxs-lookup"><span data-stu-id="082f8-164">Select the delegated provider’s subscription from the drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-the-offer"></a><span data-ttu-id="082f8-165">Le fournisseur délégué personnalise l’offre</span><span class="sxs-lookup"><span data-stu-id="082f8-165">Delegated provider customizes the offer</span></span>

<span data-ttu-id="082f8-166">Connectez-vous au **portail du locataire** en tant que fournisseur délégué et créez une offre en utilisant l’offre déléguée comme modèle.</span><span class="sxs-lookup"><span data-stu-id="082f8-166">Sign in to the **tenant portal** as the delegated provider and create a new offer using the delegated offer as a template.</span></span>

1. <span data-ttu-id="082f8-167">Cliquez sur **Nouveau** &gt; **Offres + Plans clients** &gt; **Offre**.</span><span class="sxs-lookup"><span data-stu-id="082f8-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="082f8-168">Attribuez un nom à l’offre.</span><span class="sxs-lookup"><span data-stu-id="082f8-168">Assign a name to the offer.</span></span> <span data-ttu-id="082f8-169">Ici, nous avons choisi le nom ResellerOffer.</span><span class="sxs-lookup"><span data-stu-id="082f8-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="082f8-170">Sélectionnez l’offre déléguée sur laquelle baser cette offre, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="082f8-170">Select the delegated offer to base it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="082f8-171">Notez la différence par rapport à la création d’offre telle qu’elle est vécue par l’opérateur cloud.</span><span class="sxs-lookup"><span data-stu-id="082f8-171">Note the difference compared to offer creation as experienced by the cloud operator.</span></span> <span data-ttu-id="082f8-172">Le fournisseur délégué ne construit pas l’offre à partir de plans de base et de plans d’extension ; il ne peut choisir que parmi des offres qui lui ont été déléguées et ne peut pas apporter des modifications à ces offres.</span><span class="sxs-lookup"><span data-stu-id="082f8-172">The delegated provider does not construct the offer from base plans and add-on plans; they can only choose from offers that have been delegated to them, and can't make changes to those offers.</span></span>

1. <span data-ttu-id="082f8-173">Rendez l’offre publique en cliquant sur **Parcourir** &gt; **Offres**, en sélectionnant l’offre et en cliquant sur **Modifier l’état**.</span><span class="sxs-lookup"><span data-stu-id="082f8-173">Make the offer public by clicking **Browse** &gt; **Offers**, selecting the offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="082f8-174">Le fournisseur délégué expose ces offres via l’URL de son propre portail.</span><span class="sxs-lookup"><span data-stu-id="082f8-174">The delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="082f8-175">Ces offres sont visibles uniquement via le portail délégué.</span><span class="sxs-lookup"><span data-stu-id="082f8-175">These offers are visible only through the delegated portal.</span></span> <span data-ttu-id="082f8-176">Pour rechercher et modifier cette URL :</span><span class="sxs-lookup"><span data-stu-id="082f8-176">To find and change this URL:</span></span>
   
    <span data-ttu-id="082f8-177">a.</span><span class="sxs-lookup"><span data-stu-id="082f8-177">a.</span></span>  <span data-ttu-id="082f8-178">Cliquez sur **Parcourir**&gt; **Plus de services**&gt; **Abonnements**&gt; Sélectionnez l’abonnement du fournisseur délégué, dans notre cas il s’agit de *DPSubscription*&gt; **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="082f8-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select the delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="082f8-179">b.</span><span class="sxs-lookup"><span data-stu-id="082f8-179">b.</span></span>  <span data-ttu-id="082f8-180">Copiez l’URL du portail vers un autre emplacement, comme le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="082f8-180">Copy the portal URL to a separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="082f8-181">Vous avez maintenant terminé la création d’une offre déléguée en tant que fournisseur délégué.</span><span class="sxs-lookup"><span data-stu-id="082f8-181">You have now completed the creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="082f8-182">Déconnectez-vous en tant que fournisseur délégué.</span><span class="sxs-lookup"><span data-stu-id="082f8-182">Sign out as the delegated provider.</span></span> <span data-ttu-id="082f8-183">Fermez l’onglet de navigateur que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="082f8-183">Close the browser tab you have been using.</span></span>

## <a name="sign-up-for-the-offer"></a><span data-ttu-id="082f8-184">S’inscrire à l’offre</span><span class="sxs-lookup"><span data-stu-id="082f8-184">Sign up for the offer</span></span>
1. <span data-ttu-id="082f8-185">Dans une nouvelle fenêtre de navigateur, accédez à l’URL du portail délégué que vous avez enregistrée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="082f8-185">In a new browser window, go to the delegated portal URL you saved in the previous step.</span></span> <span data-ttu-id="082f8-186">Connectez-vous au portail en tant qu’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="082f8-186">Sign in to the portal as user.</span></span> <span data-ttu-id="082f8-187">Remarque : utilisez le portail délégué pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="082f8-187">Note: Use the delegated portal for this step.</span></span> <span data-ttu-id="082f8-188">Sinon, l’offre déléguée ne s’affiche pas.</span><span class="sxs-lookup"><span data-stu-id="082f8-188">The delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="082f8-189">Dans le tableau de bord, cliquez sur **Prendre un abonnement**.</span><span class="sxs-lookup"><span data-stu-id="082f8-189">In the dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="082f8-190">Vous verrez que seules les offres déléguées créés par le fournisseur délégué sont présentées à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="082f8-190">You will see that only the delegated offers created by the delegated provider are presented to the user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="082f8-191">Ceci conclut le processus de délégation de l’offre.</span><span class="sxs-lookup"><span data-stu-id="082f8-191">This concludes the process of offer delegation.</span></span> <span data-ttu-id="082f8-192">L’utilisateur peut désormais s’inscrire à cette offre en prenant un abonnement à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="082f8-192">The user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="082f8-193">Délégation à plusieurs niveaux</span><span class="sxs-lookup"><span data-stu-id="082f8-193">Multiple-tier delegation</span></span>

<span data-ttu-id="082f8-194">La délégation à plusieurs niveaux permet au fournisseur délégué de déléguer l’offre à d’autres entités.</span><span class="sxs-lookup"><span data-stu-id="082f8-194">Multiple-tier delegation allows the delegated provider to delegate the offer to other entities.</span></span> <span data-ttu-id="082f8-195">Cela permet, par exemple, la création de réseaux de revendeurs plus approfondis, dans lesquels le fournisseur qui gère Azure Stack délègue une offre à un distributeur, qui à son tour délègue au revendeur.</span><span class="sxs-lookup"><span data-stu-id="082f8-195">This allows, for example, the creation of deeper reseller channels, in which the provider managing Azure Stack delegates an offer to a distributor, who in turn delegates to reseller.</span></span>
<span data-ttu-id="082f8-196">Azure Stack prend en charge jusqu’à cinq niveaux de délégation.</span><span class="sxs-lookup"><span data-stu-id="082f8-196">Azure Stack supports up to five levels of delegation.</span></span>

<span data-ttu-id="082f8-197">Pour créer plusieurs niveaux de délégation de l’offre, le fournisseur délégué délègue à son tour l’offre au fournisseur suivant.</span><span class="sxs-lookup"><span data-stu-id="082f8-197">To create multiple tiers of offer delegation, the delegated provider in turn delegates the offer to the next provider.</span></span> <span data-ttu-id="082f8-198">Le processus pour le fournisseur délégué est similaire à celui pour l’opérateur cloud (consultez [L’opérateur cloud crée l’offre déléguée](#cloud-operator-creates-the-delegated-offer)).</span><span class="sxs-lookup"><span data-stu-id="082f8-198">The process is the same for the delegated provider as it was for the cloud operator (see [Cloud operator creates the delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="082f8-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="082f8-199">Next steps</span></span>
[<span data-ttu-id="082f8-200">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="082f8-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

