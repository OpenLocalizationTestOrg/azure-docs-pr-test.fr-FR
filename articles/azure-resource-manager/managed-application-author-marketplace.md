---
title: "aaaAzure gérés applications Bonjour Marketplace | Documents Microsoft"
description: "Décrit les Azure applications managées qui sont disponibles via hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="204aa-103">Azure géré applications Bonjour Marketplace</span><span class="sxs-lookup"><span data-stu-id="204aa-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="204aa-104">MSP, éditeurs de logiciels indépendants et les intégrateurs système (SIs) peuvent utiliser Azure géré applications toooffer leurs clients d’Azure Marketplace de tooall solutions.</span><span class="sxs-lookup"><span data-stu-id="204aa-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="204aa-105">Ces solutions réduisent la maintenance de hello et surcharge de maintenance pour les clients.</span><span class="sxs-lookup"><span data-stu-id="204aa-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="204aa-106">Serveurs de publication peuvent vendre infrastructure et les logiciels via hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="204aa-107">Elles peuvent attacher support opérationnel toomanaged applications et services.</span><span class="sxs-lookup"><span data-stu-id="204aa-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="204aa-108">Pour plus d’informations, consultez [Vue d’ensemble des applications gérées](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="204aa-109">Cet article explique comment un MSP, éditeurs de logiciels ou SI peut publier un toohello application Marketplace et le rendre disponible toocustomers.</span><span class="sxs-lookup"><span data-stu-id="204aa-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="204aa-110">Conditions préalables à la publication d’une application gérée</span><span class="sxs-lookup"><span data-stu-id="204aa-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="204aa-111">Conditions préalables des toolisting Bonjour Marketplace :</span><span class="sxs-lookup"><span data-stu-id="204aa-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="204aa-112">Techniques</span><span class="sxs-lookup"><span data-stu-id="204aa-112">Technical</span></span>

    *  <span data-ttu-id="204aa-113">Pour plus d’informations sur la structure de base de hello et syntaxe des modèles Azure Resource Manager, consultez [modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="204aa-114">solutions de modèle complète tooview, consultez [modèles de démarrage rapide d’Azure](https://azure.microsoft.com/en-us/documentation/templates/) ou hello [référentiel de modèle de démarrage rapide](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="204aa-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="204aa-115">Pour plus d’informations sur comment toocreate hello interface pour les clients qui déploient votre application via hello Marketplace, consultez [créer un fichier de définition d’interface utilisateur](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="204aa-116">Non techniques (critères de l’entreprise)</span><span class="sxs-lookup"><span data-stu-id="204aa-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="204aa-117">Votre entreprise ou ses filiales doit se trouver dans un pays où les ventes sont pris en charge par hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="204aa-118">Votre produit doit avoir une licence d’une manière qui est compatible avec les modèles de facturation pris en charge par hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="204aa-119">Vous êtes responsable de la toocustomers disponibles du support technique de façon commercialement raisonnable.</span><span class="sxs-lookup"><span data-stu-id="204aa-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="204aa-120">prise en charge Hello peut être gratuit, payé, ou via la Communauté prend en charge.</span><span class="sxs-lookup"><span data-stu-id="204aa-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="204aa-121">Il vous incombe de gérer les licences de vos logiciels et de toutes les dépendances de logiciels tiers.</span><span class="sxs-lookup"><span data-stu-id="204aa-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="204aa-122">Vous devez fournir le contenu qui répond aux critères de votre toobe offre répertoriés dans hello Marketplace et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="204aa-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="204aa-123">Vous devez accepter les termes du contrat de toohello de stratégies de Participation hello Azure Marketplace et le contrat d’éditeur.</span><span class="sxs-lookup"><span data-stu-id="204aa-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="204aa-124">Vous devez accepter toocomply avec Microsoft Azure Certified accord hello les conditions d’utilisation et déclaration de confidentialité de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="204aa-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="204aa-125">Création d’une offre d’application Azure</span><span class="sxs-lookup"><span data-stu-id="204aa-125">Create a new Azure application offer</span></span>

<span data-ttu-id="204aa-126">Une fois les conditions préalables hello, vous êtes prêt toocreate votre offre de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="204aa-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="204aa-127">Voici une brève présentation de ce que sont une offre et une référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="204aa-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="204aa-128">Offer</span><span class="sxs-lookup"><span data-stu-id="204aa-128">Offer</span></span>

<span data-ttu-id="204aa-129">offre Hello pour une application managée correspond classe tooa du produit à partir d’un serveur de publication de l’offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="204aa-130">Si vous avez un nouveau type de solution / l’application que vous souhaitez toomake disponible dans hello Marketplace, vous pouvez le configurer en tant qu’une offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="204aa-131">Une offre est une collection de références (SKU).</span><span class="sxs-lookup"><span data-stu-id="204aa-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="204aa-132">Toutes les offres apparaît comme son propre entité Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="204aa-133">SKU</span><span class="sxs-lookup"><span data-stu-id="204aa-133">SKU</span></span>

<span data-ttu-id="204aa-134">Une référence (SKU) est hello plus petite être achetée unité d’une offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="204aa-135">Vous pouvez utiliser une référence (SKU) au sein de hello même toodifferentiate de classe (offre) produit entre :</span><span class="sxs-lookup"><span data-stu-id="204aa-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="204aa-136">Les différentes fonctionnalités prises en charge.</span><span class="sxs-lookup"><span data-stu-id="204aa-136">Different features that are supported.</span></span>
* <span data-ttu-id="204aa-137">Indique si les offre hello sont gérée ou non gérée.</span><span class="sxs-lookup"><span data-stu-id="204aa-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="204aa-138">Les modèles de facturation pris en charge.</span><span class="sxs-lookup"><span data-stu-id="204aa-138">Billing models that are supported.</span></span>

<span data-ttu-id="204aa-139">Une référence (SKU) s’affiche sous l’offre de parent hello Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="204aa-140">Il apparaît comme son propre entité être achetée Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="204aa-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="204aa-141">Configuration d’une offre</span><span class="sxs-lookup"><span data-stu-id="204aa-141">Set up an offer</span></span>

1. <span data-ttu-id="204aa-142">Connectez-vous à toohello [portail du partenaire de nuage](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="204aa-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="204aa-143">Dans le volet de navigation hello hello gauche, sélectionnez **+ nouvelle offre** > **des Applications Azure**.</span><span class="sxs-lookup"><span data-stu-id="204aa-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nouvelle offre](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="204aa-145">Remplir des formulaires hello apparaissant sur hello restant dans hello **éditeur** vue.</span><span class="sxs-lookup"><span data-stu-id="204aa-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="204aa-146">Les champs obligatoires sont indiqués par un astérisque rouge (*).</span><span class="sxs-lookup"><span data-stu-id="204aa-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Paramètres de l’offre](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="204aa-148">Quatre formes principales sont toocreate utilisé une application managée :</span><span class="sxs-lookup"><span data-stu-id="204aa-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="204aa-149">a.</span><span class="sxs-lookup"><span data-stu-id="204aa-149">a.</span></span> <span data-ttu-id="204aa-150">Paramètres de l’offre</span><span class="sxs-lookup"><span data-stu-id="204aa-150">Offer Settings</span></span>

    <span data-ttu-id="204aa-151">b.</span><span class="sxs-lookup"><span data-stu-id="204aa-151">b.</span></span> <span data-ttu-id="204aa-152">Références (SKU)</span><span class="sxs-lookup"><span data-stu-id="204aa-152">SKUs</span></span>

    <span data-ttu-id="204aa-153">c.</span><span class="sxs-lookup"><span data-stu-id="204aa-153">c.</span></span> <span data-ttu-id="204aa-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="204aa-154">Marketplace</span></span>

    <span data-ttu-id="204aa-155">d.</span><span class="sxs-lookup"><span data-stu-id="204aa-155">d.</span></span> <span data-ttu-id="204aa-156">Support</span><span class="sxs-lookup"><span data-stu-id="204aa-156">Support</span></span>

<span data-ttu-id="204aa-157">Ces formes sont décrites en détail dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="204aa-158">Formulaire des paramètres de l’offre</span><span class="sxs-lookup"><span data-stu-id="204aa-158">Offer Settings form</span></span>
<span data-ttu-id="204aa-159">Utiliser ce paramètres de l’offre de base toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="204aa-160">Renseignez hello **offrent des paramètres** formulaire.</span><span class="sxs-lookup"><span data-stu-id="204aa-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="204aa-161">les champs différents Hello sont :</span><span class="sxs-lookup"><span data-stu-id="204aa-161">hello different fields are:</span></span>

    <span data-ttu-id="204aa-162">a.</span><span class="sxs-lookup"><span data-stu-id="204aa-162">a.</span></span> <span data-ttu-id="204aa-163">**ID offre**: cet identificateur unique identifie offre hello dans un profil de serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="204aa-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="204aa-164">Cet ID est visible dans les URL de produit, les modèles Resource Manager et les états de facturation.</span><span class="sxs-lookup"><span data-stu-id="204aa-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="204aa-165">Il ne peut comprendre que des caractères alphanumériques en minuscules ou des tirets (-).</span><span class="sxs-lookup"><span data-stu-id="204aa-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="204aa-166">Hello ID ne peut pas se terminer dans un tiret.</span><span class="sxs-lookup"><span data-stu-id="204aa-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="204aa-167">Il est limité tooa jusqu'à 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="204aa-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="204aa-168">Ce champ est verrouillé une fois l’offre publiée.</span><span class="sxs-lookup"><span data-stu-id="204aa-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="204aa-169">b.</span><span class="sxs-lookup"><span data-stu-id="204aa-169">b.</span></span> <span data-ttu-id="204aa-170">**ID de l’éditeur**: utiliser ce profil de serveur de publication de liste déroulante toochoose hello souhaité toopublish cette offre sous.</span><span class="sxs-lookup"><span data-stu-id="204aa-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="204aa-171">Ce champ est verrouillé une fois l’offre publiée.</span><span class="sxs-lookup"><span data-stu-id="204aa-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="204aa-172">c.</span><span class="sxs-lookup"><span data-stu-id="204aa-172">c.</span></span> <span data-ttu-id="204aa-173">**Nom**: ce nom d’affichage pour votre offre apparaît dans hello Marketplace et dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="204aa-174">Il ne peut pas comprendre plus de 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="204aa-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="204aa-175">Incluez un nom de marque reconnaissable pour votre produit.</span><span class="sxs-lookup"><span data-stu-id="204aa-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="204aa-176">N’incluez pas ici le nom de votre entreprise, sauf si c’est le nom sous lequel l’offre est commercialisée.</span><span class="sxs-lookup"><span data-stu-id="204aa-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="204aa-177">Si vous êtes marketing cette offre sur votre propre site Web, assurez-vous que ce nom hello est exactement comment il apparaît sur votre site Web.</span><span class="sxs-lookup"><span data-stu-id="204aa-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="204aa-178">Sélectionnez **enregistrer** toosave votre progression.</span><span class="sxs-lookup"><span data-stu-id="204aa-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="204aa-179">Formulaire de références (SKU)</span><span class="sxs-lookup"><span data-stu-id="204aa-179">SKUs form</span></span>
<span data-ttu-id="204aa-180">étape suivante de Hello est SKU tooadd pour votre offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="204aa-181">Sélectionnez **Références** > **Nouvelle référence**.</span><span class="sxs-lookup"><span data-stu-id="204aa-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Sélectionner option de nouvelle référence](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="204aa-183">Saisissez un **ID de référence**.</span><span class="sxs-lookup"><span data-stu-id="204aa-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="204aa-184">Un ID de référence (SKU) est un identificateur unique pour hello référence (SKU) au sein d’une offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="204aa-185">Cet ID est visible dans les URL de produit, les modèles Resource Manager et les états de facturation.</span><span class="sxs-lookup"><span data-stu-id="204aa-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="204aa-186">Il ne peut comprendre que des caractères alphanumériques en minuscules ou des tirets (-).</span><span class="sxs-lookup"><span data-stu-id="204aa-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="204aa-187">Hello ID ne peut pas se terminer par un tiret, et il est limité tooa jusqu'à 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="204aa-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="204aa-188">Ce champ est verrouillé une fois l’offre publiée.</span><span class="sxs-lookup"><span data-stu-id="204aa-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="204aa-189">Vous pouvez avoir plusieurs références (SKU) au sein d’une même offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="204aa-190">Vous avez besoin d’une référence (SKU) pour chaque image que vous prévoyez toopublish.</span><span class="sxs-lookup"><span data-stu-id="204aa-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="204aa-191">Remplir hello **détails de la référence (SKU)** section hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="204aa-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Fournir une nouvelle référence (SKU)](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="204aa-193">Renseignez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="204aa-194">a.</span><span class="sxs-lookup"><span data-stu-id="204aa-194">a.</span></span> <span data-ttu-id="204aa-195">**Titre** : saisissez un titre pour cette référence.</span><span class="sxs-lookup"><span data-stu-id="204aa-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="204aa-196">Ce titre s’affiche dans la galerie de hello pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="204aa-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="204aa-197">b.</span><span class="sxs-lookup"><span data-stu-id="204aa-197">b.</span></span> <span data-ttu-id="204aa-198">**Summary** (Résumé) : saisissez un bref résumé décrivant cette référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="204aa-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="204aa-199">Ce texte s’affiche sous le titre de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="204aa-200">c.</span><span class="sxs-lookup"><span data-stu-id="204aa-200">c.</span></span> <span data-ttu-id="204aa-201">**Description**: entrez une description détaillée hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="204aa-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="204aa-202">d.</span><span class="sxs-lookup"><span data-stu-id="204aa-202">d.</span></span> <span data-ttu-id="204aa-203">**Type de référence (SKU)**: hello valeurs autorisées sont **Application managée** et **des modèles de Solution**.</span><span class="sxs-lookup"><span data-stu-id="204aa-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="204aa-204">Dans le cas présent, sélectionnez **Managed Application** (Application gérée).</span><span class="sxs-lookup"><span data-stu-id="204aa-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="204aa-205">Remplir hello **détails du Package** section hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="204aa-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="204aa-207">Renseignez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="204aa-208">a.</span><span class="sxs-lookup"><span data-stu-id="204aa-208">a.</span></span> <span data-ttu-id="204aa-209">**Version actuelle**: entrez une version de package hello vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="204aa-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="204aa-210">Il doit être au format de hello `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="204aa-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="204aa-211">b.</span><span class="sxs-lookup"><span data-stu-id="204aa-211">b.</span></span> <span data-ttu-id="204aa-212">**Sélectionnez un fichier de package**: hello suivant des fichiers qui sont compressés dans un fichier .zip contient :</span><span class="sxs-lookup"><span data-stu-id="204aa-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="204aa-213">**applianceMainTemplate.json**: fichier de modèle de déploiement hello qui a utilisé l’application toodeploy hello solution.</span><span class="sxs-lookup"><span data-stu-id="204aa-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="204aa-214">Pour plus d’informations sur la façon de fichiers de modèle de déploiement toocreate, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="204aa-215">**appliancecreateUIDefinition.json**: ce fichier est utilisé par hello toogenerate portail Azure hello interface utilisateur qui a utilisé tooprovision cette solution/application.</span><span class="sxs-lookup"><span data-stu-id="204aa-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="204aa-216">Pour plus d’informations, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="204aa-217">**mainTemplate.json**: ce fichier de modèle contient uniquement des ressources Microsoft.Solution/appliances hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="204aa-218">fichier de mainTemplate Hello inclut hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="204aa-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="204aa-219">**type**: utilisez **Marketplace** pour les applications managées Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="204aa-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="204aa-220">**ManagedResourceGroupId**: ce groupe de ressources dans l’abonnement du client hello est où toutes les ressources hello définis dans applianceMainTemplate.json sont déployés.</span><span class="sxs-lookup"><span data-stu-id="204aa-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="204aa-221">**PublisherPackageId**: cette chaîne identifie de façon unique le package de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="204aa-222">Fournir la valeur hello format hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="204aa-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="204aa-223">Obtenir hello **ID d’offre** et **ID de l’éditeur** de hello publication portail, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="204aa-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![ID de l’offre](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="204aa-225">Obtenir hello **ID de référence (SKU)**, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="204aa-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![RÉFÉRENCE (SKU)](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="204aa-227">Obtenir le package de hello **Version**, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="204aa-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Version du package](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="204aa-229">En fonction de hello précédents exemples, hello valeur de **PublisherPackageId** est `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="204aa-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="204aa-230">Exemple de fichier mainTemplate.json :</span><span class="sxs-lookup"><span data-stu-id="204aa-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="204aa-231">Ce package doit contenir tous les autres modèles imbriqués ou des scripts qui sont requis toosuccessfully configurer cette application.</span><span class="sxs-lookup"><span data-stu-id="204aa-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="204aa-232">Hello mainTemplate.json, applianceMainTemplate.json et applianceCreateUIDefinition.json fichiers doivent être présents dans le dossier racine hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="204aa-233">**Autorisations**: cette propriété définit qui obtient un niveau d’accès et hello d’accès toohello des ressources dans les abonnements des clients.</span><span class="sxs-lookup"><span data-stu-id="204aa-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="204aa-234">serveur de publication Hello peut utiliser application hello de toomanage au nom de client de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="204aa-235">**PrincipalId**: cette propriété est l’identificateur d’Azure Active Directory (Azure AD) hello d’un utilisateur, un groupe d’utilisateurs ou une application qui a attribué certaines autorisations sur les ressources hello hello l’abonnement du client.</span><span class="sxs-lookup"><span data-stu-id="204aa-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="204aa-236">Hello définition de rôle décrit les autorisations de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="204aa-237">**Définition de rôle**: cette propriété est une liste de tous les hello contrôle d’accès en fonction du rôle (RBAC) rôles intégrés fournis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204aa-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="204aa-238">Vous pouvez sélectionner le rôle hello qui des ressources hello toomanage toouse plus appropriés pour le compte du client de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="204aa-239">Vous pouvez ajouter plusieurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="204aa-239">You can add multiple authorizations.</span></span> <span data-ttu-id="204aa-240">Nous vous recommandons de créer un groupe d’utilisateurs AD et de spécifier son ID dans **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="204aa-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="204aa-241">De cette manière, vous pouvez ajouter le groupe d’utilisateurs plus d’utilisateurs toohello sans Bonjour besoin tooupdate Bonjour référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="204aa-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="204aa-242">Pour plus d’informations sur RBAC, consultez [prise en main RBAC Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="204aa-243">Formulaire Marketplace</span><span class="sxs-lookup"><span data-stu-id="204aa-243">Marketplace form</span></span>

<span data-ttu-id="204aa-244">demande de Hello formulaire de Marketplace pour les champs qui apparaissent sur hello [Azure Marketplace](https://azuremarketplace.microsoft.com) et hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="204aa-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="204aa-245">ID d’abonnement pour version préliminaire</span><span class="sxs-lookup"><span data-stu-id="204aa-245">Preview subscription IDs</span></span>

<span data-ttu-id="204aa-246">Entrez une liste d’ID qui peuvent accéder à hello offre après sa publication d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="204aa-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="204aa-247">Vous pouvez utiliser ces offre de hello prévisualisé tootest blanc dans la liste des abonnements avant de le rendre live.</span><span class="sxs-lookup"><span data-stu-id="204aa-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="204aa-248">Vous pouvez compiler une liste blanche d’abonnements too100 dans le portail du partenaire hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="204aa-249">Catégories suggérées</span><span class="sxs-lookup"><span data-stu-id="204aa-249">Suggested categories</span></span>

<span data-ttu-id="204aa-250">Sélectionnez les catégories de toofive à partir de la liste hello associé à votre offre permettre être mieux.</span><span class="sxs-lookup"><span data-stu-id="204aa-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="204aa-251">Ces catégories est utilisée toomap vos catégories de produit toohello offre qui sont disponibles dans hello [Azure Marketplace](https://azuremarketplace.microsoft.com) et hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="204aa-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="204aa-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="204aa-252">Azure Marketplace</span></span>

<span data-ttu-id="204aa-253">Résumé de Hello de votre application managée affiche hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-253">hello summary of your managed application displays hello following fields:</span></span>

![Résumé sur la place de marché](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="204aa-255">Hello **vue d’ensemble** onglet pour votre application managée affiche hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Présentation de la Place de marché](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="204aa-257">Hello **Plans + tarification** onglet pour votre application managée affiche hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Plans sur la place de marché](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="204aa-259">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="204aa-259">Azure portal</span></span>

<span data-ttu-id="204aa-260">Résumé de Hello de votre application managée affiche hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-260">hello summary of your managed application displays hello following fields:</span></span>

![Résumé sur le portail](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="204aa-262">vue d’ensemble de Hello pour votre application managée affiche hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="204aa-262">hello overview for your managed application displays hello following fields:</span></span>

![Présentation du portail](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="204aa-264">Instructions concernant le logo</span><span class="sxs-lookup"><span data-stu-id="204aa-264">Logo guidelines</span></span>

<span data-ttu-id="204aa-265">Suivez ces instructions pour un logo que vous téléchargez dans le portail du partenaire de Cloud hello :</span><span class="sxs-lookup"><span data-stu-id="204aa-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="204aa-266">Hello conception Azure a une palette de couleurs simple.</span><span class="sxs-lookup"><span data-stu-id="204aa-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="204aa-267">Limiter le nombre des principaux hello et les couleurs de base de données secondaire sur votre logo.</span><span class="sxs-lookup"><span data-stu-id="204aa-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="204aa-268">couleurs du thème Hello du portail de hello sont blancs et noir.</span><span class="sxs-lookup"><span data-stu-id="204aa-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="204aa-269">N’utilisez pas ces couleurs comme couleur d’arrière-plan hello pour votre logo.</span><span class="sxs-lookup"><span data-stu-id="204aa-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="204aa-270">Utilisez une couleur qui rend votre logo dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="204aa-271">Nous vous recommandons d’utiliser des couleurs primaires simples.</span><span class="sxs-lookup"><span data-stu-id="204aa-271">We recommend simple primary colors.</span></span> <span data-ttu-id="204aa-272">*Si vous utilisez un arrière-plan transparent, assurez-vous que le logo de hello et le texte ne sont pas blancs, noir, ou en bleu.*</span><span class="sxs-lookup"><span data-stu-id="204aa-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="204aa-273">N’utilisez pas un arrière-plan dégradé sur le logo de hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="204aa-274">Ne pas placer du texte sur le logo de hello, même pas votre entreprise ou le nom de marque.</span><span class="sxs-lookup"><span data-stu-id="204aa-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="204aa-275">Hello apparence de votre logo doit être plat et éviter des dégradés.</span><span class="sxs-lookup"><span data-stu-id="204aa-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="204aa-276">Assurez-vous que le logo de hello n’est pas étirée.</span><span class="sxs-lookup"><span data-stu-id="204aa-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="204aa-277">Bannière</span><span class="sxs-lookup"><span data-stu-id="204aa-277">Hero logo</span></span>

<span data-ttu-id="204aa-278">logo de héros Hello est facultative.</span><span class="sxs-lookup"><span data-stu-id="204aa-278">hello hero logo is optional.</span></span> <span data-ttu-id="204aa-279">serveur de publication Hello peut choisir tooupload pas un logo héros.</span><span class="sxs-lookup"><span data-stu-id="204aa-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="204aa-280">Une fois que l’icône de héros hello est téléchargé, il ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="204aa-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="204aa-281">À ce stade, les partenaires hello doivent respecter les règles de Marketplace de hello pour les icônes de héros.</span><span class="sxs-lookup"><span data-stu-id="204aa-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="204aa-282">Suivez ces instructions pour l’icône du logo héros hello :</span><span class="sxs-lookup"><span data-stu-id="204aa-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="204aa-283">nom complet de l’éditeur Hello, titre de plan hello et offre hello résumée s’affichent en blanc.</span><span class="sxs-lookup"><span data-stu-id="204aa-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="204aa-284">Par conséquent, n’utilisez une couleur claire pour l’arrière-plan hello d’icône de héros hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="204aa-285">Les arrière-plans noirs, blancs et transparents ne sont pas autorisés pour les icônes.</span><span class="sxs-lookup"><span data-stu-id="204aa-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="204aa-286">Une fois que l’offre de hello est répertorié, serveur de publication hello le nom complet, titre de plan hello, offre hello résumée et hello **créer** bouton sont incorporés par programmation à l’intérieur du logo de héros hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="204aa-287">Par conséquent, n’entrez pas de texte lorsque vous concevez le logo de héros hello.</span><span class="sxs-lookup"><span data-stu-id="204aa-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="204aa-288">Laisser un espace vide sur hello droite, car le texte hello est inclus par programme dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="204aa-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="204aa-289">espace vide Hello texte hello doit être hello droite 415 x 100 pixels.</span><span class="sxs-lookup"><span data-stu-id="204aa-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="204aa-290">Elle est décalée par 370 pixels de hello gauche.</span><span class="sxs-lookup"><span data-stu-id="204aa-290">It's offset by 370 pixels from hello left.</span></span>

    ![Exemple d’icône de bannière](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="204aa-292">Formulaire de prise en charge</span><span class="sxs-lookup"><span data-stu-id="204aa-292">Support form</span></span>

<span data-ttu-id="204aa-293">Remplir hello **prennent en charge** formulaire avec prise en charge des contacts à partir de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="204aa-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="204aa-294">Ces informations peuvent être les contacts de support d’ingénierie et client.</span><span class="sxs-lookup"><span data-stu-id="204aa-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="204aa-295">Publication d’une offre</span><span class="sxs-lookup"><span data-stu-id="204aa-295">Publish an offer</span></span>

<span data-ttu-id="204aa-296">Une fois que vous remplissez toutes les sections hello, sélectionnez **publier** processus hello toostart qui rend votre toocustomers disponible offre.</span><span class="sxs-lookup"><span data-stu-id="204aa-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="204aa-297">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="204aa-297">Next steps</span></span>

* <span data-ttu-id="204aa-298">Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="204aa-299">Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="204aa-300">Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="204aa-301">Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="204aa-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
