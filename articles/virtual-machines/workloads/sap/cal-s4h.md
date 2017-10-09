---
title: aaaDeploy SAP S/4HANA ou BW/4HANA sur une machine virtuelle Azure | Documents Microsoft
description: "Déploiement de SAP S/4HANA ou BW/4HANA sur une machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="017e9-103">Déploiement de SAP S/4HANA ou BW/4HANA sur Azure</span><span class="sxs-lookup"><span data-stu-id="017e9-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="017e9-104">Cet article décrit comment toodeploy S/4HANA sur Azure à l’aide de hello bibliothèque de matériel du Cloud SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="017e9-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="017e9-105">toodeploy autres solutions SAP HANA, telles que BW/4HANA, suivent hello mêmes étapes.</span><span class="sxs-lookup"><span data-stu-id="017e9-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="017e9-106">Pour plus d’informations sur hello SAP licences d’accès client, accédez à toohello [SAP Cloud application bibliothèque](https://cal.sap.com/) site Web.</span><span class="sxs-lookup"><span data-stu-id="017e9-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="017e9-107">SAP possède également un blog sur hello [SAP Cloud Appliance bibliothèque 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="017e9-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="017e9-108">Comme de 29 mai 2017, vous pouvez utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello en outre toohello préféré au moins un déploiement classique de modèle toodeploy hello licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="017e9-109">Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager hello et de ne pas tenir compte de modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="017e9-110">Solution de hello toodeploy étape par étape</span><span class="sxs-lookup"><span data-stu-id="017e9-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="017e9-111">Hello suivant la séquence de captures d’écran montre comment toodeploy S/4HANA sur Azure à l’aide de hello des licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="017e9-112">hello se déroulent Hello identique pour d’autres solutions, telles que BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="017e9-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="017e9-113">Hello **Solutions** page répertorie quelques-unes des hello basée sur les licences d’accès client de SAP HANA les solutions disponibles sur Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="017e9-114">**SAP S/4HANA 1610 FPS01, Fully-Activated équipement** est en ligne au milieu de hello :</span><span class="sxs-lookup"><span data-stu-id="017e9-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Solutions SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="017e9-116">Créer un compte dans hello licences d’accès client SAP</span><span class="sxs-lookup"><span data-stu-id="017e9-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="017e9-117">toosign dans toohello SAP CAL pour hello première fois, utilisez votre utilisateur S SAP ou autre utilisateur enregistré dans SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="017e9-118">Définissez ensuite un compte d’accès client SAP qui est utilisé par les appareils de toodeploy hello licences d’accès client SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="017e9-119">Dans la définition du compte de hello, vous devez :</span><span class="sxs-lookup"><span data-stu-id="017e9-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="017e9-120">a.</span><span class="sxs-lookup"><span data-stu-id="017e9-120">a.</span></span> <span data-ttu-id="017e9-121">Sélectionnez le modèle de déploiement hello sur Azure (Gestionnaire de ressources ou classique).</span><span class="sxs-lookup"><span data-stu-id="017e9-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="017e9-122">b.</span><span class="sxs-lookup"><span data-stu-id="017e9-122">b.</span></span> <span data-ttu-id="017e9-123">Entrez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-123">Enter your Azure subscription.</span></span> <span data-ttu-id="017e9-124">Abonnement tooone uniquement peut être affecté à un compte de la licence d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="017e9-125">Si vous avez besoin de plus d’un abonnement, vous devez toocreate un autre compte de licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="017e9-126">c.</span><span class="sxs-lookup"><span data-stu-id="017e9-126">c.</span></span> <span data-ttu-id="017e9-127">Donnez à hello SAP CAL autorisation toodeploy dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="017e9-128">les étapes suivantes Hello montrent comment toocreate une licence d’accès client SAP compte pour les déploiements de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="017e9-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="017e9-129">Si vous avez déjà un compte de licence d’accès client SAP qui est le modèle de déploiement classique toohello lié, vous *devez* toofollow ces toocreate étapes un nouveau compte de licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="017e9-130">nouveau compte de licences d’accès client SAP Hello doit toodeploy dans le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="017e9-131">Créez un compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="017e9-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="017e9-132">Hello **comptes** page affiche les trois possibilités pour Azure :</span><span class="sxs-lookup"><span data-stu-id="017e9-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="017e9-133">a.</span><span class="sxs-lookup"><span data-stu-id="017e9-133">a.</span></span> <span data-ttu-id="017e9-134">**Microsoft Azure (classique)** est le modèle de déploiement classique hello et n’est plus recommandée.</span><span class="sxs-lookup"><span data-stu-id="017e9-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="017e9-135">b.</span><span class="sxs-lookup"><span data-stu-id="017e9-135">b.</span></span> <span data-ttu-id="017e9-136">**Microsoft Azure** est le nouveau modèle de déploiement Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="017e9-137">c.</span><span class="sxs-lookup"><span data-stu-id="017e9-137">c.</span></span> <span data-ttu-id="017e9-138">**Windows Azure géré par 21Vianet** est une option en Chine qui utilise le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="017e9-139">toodeploy dans le modèle de gestionnaire de ressources hello, sélectionnez **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="017e9-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Détails du compte SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="017e9-141">Entrez hello Azure **ID d’abonnement** qui se trouvent sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Comptes SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="017e9-143">toodeploy de licences d’accès client SAP tooauthorize hello en hello abonnement Azure que vous avez définies, cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="017e9-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="017e9-144">Hello suivant page s’affiche dans l’onglet du navigateur hello :</span><span class="sxs-lookup"><span data-stu-id="017e9-144">hello following page appears in hello browser tab:</span></span>

   ![Connexion aux services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="017e9-146">Si plusieurs utilisateurs est répertorié, choisissez le compte Microsoft hello coadministrator de hello toobe lié Hello abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="017e9-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="017e9-147">Hello suivant page s’affiche dans l’onglet du navigateur hello :</span><span class="sxs-lookup"><span data-stu-id="017e9-147">hello following page appears in hello browser tab:</span></span>

   ![Confirmation des services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="017e9-149">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="017e9-149">Click **Accept**.</span></span> <span data-ttu-id="017e9-150">Si l’autorisation de hello est réussie, hello définition du compte de licences d’accès client SAP s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="017e9-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="017e9-151">Après une courte période, un message confirme que le processus d’autorisation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="017e9-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="017e9-152">tooassign hello nouvellement créée tooyour utilisateur du compte de licences d’accès client SAP, entrez votre **ID utilisateur** dans hello de zone de texte hello droit et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="017e9-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Association de compte toouser](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="017e9-154">Cliquez sur votre compte utilisateur de hello utiliser toosign dans toohello SAP licences d’accès client, de tooassociate **révision**.</span><span class="sxs-lookup"><span data-stu-id="017e9-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="017e9-155">association de hello toocreate entre votre utilisateur et le compte de licences d’accès client SAP hello nouvellement créé, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="017e9-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Association de compte utilisateur tooSAP licence d’accès client](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="017e9-157">Vous avez correctement créé un compte SAP CAL capable d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="017e9-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="017e9-158">Utilisez le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="017e9-159">Déployer des systèmes SAP dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="017e9-160">Vous pouvez maintenant démarrer toodeploy S/4HANA dans votre abonnement de l’utilisateur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="017e9-161">Avant de poursuivre, déterminez si vous êtes lié à des quotas de cœurs pour les machines virtuelles Azure série H.</span><span class="sxs-lookup"><span data-stu-id="017e9-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="017e9-162">Au moment de hello, hello SAP CAL utilise H-Series machines virtuelles de Azure toodeploy parmi les solutions SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="017e9-163">Il se peut que votre abonnement Azure ne soit pas associé à des quotas de cœurs pour la série H.</span><span class="sxs-lookup"><span data-stu-id="017e9-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="017e9-164">Dans ce cas, vous devrez peut-être toocontact prise en charge Azure tooget un quota de cœurs de série H au moins 16.</span><span class="sxs-lookup"><span data-stu-id="017e9-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="017e9-165">Lorsque vous déployez une solution sur Azure Bonjour licences d’accès client SAP, vous constaterez peut-être que vous pouvez choisir qu’une seule région Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="017e9-166">toodeploy dans des régions Azure autre que hello une suggéré par hello licences d’accès client SAP, vous devez toopurchase un abonnement de licence d’accès client à partir de SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="017e9-167">Vous aussi avoir besoin tooopen un message avec SAP toohave votre toodeliver compte activé de licences d’accès client dans des régions Azure autre que hello celles suggérées initialement.</span><span class="sxs-lookup"><span data-stu-id="017e9-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="017e9-168">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="017e9-168">Deploy a solution</span></span>

<span data-ttu-id="017e9-169">Nous allons déployer une solution à partir de hello **Solutions** page Hello licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="017e9-170">Hello licences d’accès client SAP a deux séquences toodeploy :</span><span class="sxs-lookup"><span data-stu-id="017e9-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="017e9-171">Une séquence de base qui utilise une page toodefine hello système toobe déployé</span><span class="sxs-lookup"><span data-stu-id="017e9-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="017e9-172">Une séquence avancée qui vous offre différents choix en termes de tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="017e9-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="017e9-173">Nous allons montrer toodeployment de chemin d’accès de base hello ici.</span><span class="sxs-lookup"><span data-stu-id="017e9-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="017e9-174">Sur hello **détails du compte** page, vous devez :</span><span class="sxs-lookup"><span data-stu-id="017e9-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="017e9-175">a.</span><span class="sxs-lookup"><span data-stu-id="017e9-175">a.</span></span> <span data-ttu-id="017e9-176">Sélectionnez un compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="017e9-176">Select an SAP CAL account.</span></span> <span data-ttu-id="017e9-177">(Utiliser un compte qui est associé toodeploy avec modèle de déploiement du Gestionnaire de ressources hello.)</span><span class="sxs-lookup"><span data-stu-id="017e9-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="017e9-178">b.</span><span class="sxs-lookup"><span data-stu-id="017e9-178">b.</span></span> <span data-ttu-id="017e9-179">Entrez le nom de l’instance dans le champ **Name** (Nom).</span><span class="sxs-lookup"><span data-stu-id="017e9-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="017e9-180">c.</span><span class="sxs-lookup"><span data-stu-id="017e9-180">c.</span></span> <span data-ttu-id="017e9-181">Sélectionnez une région Azure dans le champ **Region** (Région).</span><span class="sxs-lookup"><span data-stu-id="017e9-181">Select an Azure **Region**.</span></span> <span data-ttu-id="017e9-182">Hello SAP CAL suggère une région.</span><span class="sxs-lookup"><span data-stu-id="017e9-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="017e9-183">Si vous avez besoin d’une autre région Azure et que vous n’avez pas d’abonnement de licence d’accès client SAP, vous avez besoin d’abonnement de tooorder une licence d’accès client avec SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="017e9-184">d.</span><span class="sxs-lookup"><span data-stu-id="017e9-184">d.</span></span> <span data-ttu-id="017e9-185">Entrez un masque de **mot de passe** pour la solution hello de huit ou neuf caractères.</span><span class="sxs-lookup"><span data-stu-id="017e9-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="017e9-186">mot de passe Hello est utilisé pour les administrateurs de hello des différents composants de hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Mode de base SAP CAL : créer une instance](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="017e9-188">Cliquez sur **créer**et dans la boîte de message de salutation qui s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="017e9-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![Tailles de machine virtuelle prises en charge par SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="017e9-190">Bonjour **clé privée** boîte de dialogue, cliquez sur **magasin** clé privée de hello toostore Bonjour licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="017e9-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="017e9-191">toouse mot de passe de clé privée de hello, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="017e9-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Clé privée SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="017e9-193">Hello de lecture SAP CAL **avertissement** de message, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="017e9-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Avertissement SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="017e9-195">Maintenant le déploiement de hello a lieu.</span><span class="sxs-lookup"><span data-stu-id="017e9-195">Now hello deployment takes place.</span></span> <span data-ttu-id="017e9-196">Après un certain temps, selon la taille de hello et la complexité de la solution de hello (licence d’accès client SAP fournit une estimation hello), hello état est affiché comme actif et opérationnel.</span><span class="sxs-lookup"><span data-stu-id="017e9-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="017e9-197">machines virtuelles de toofind hello collectées avec hello autres ressources associées dans un groupe de ressources, consultez les toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="017e9-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Objets de licences d’accès client SAP déployés dans le nouveau portail de hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="017e9-199">Sur le portail SAP CAL hello, état de hello s’affiche en tant que **Active**.</span><span class="sxs-lookup"><span data-stu-id="017e9-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="017e9-200">solution de toohello tooconnect, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="017e9-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="017e9-201">Différentes options tooconnect toohello différents composants sont déployés au sein de cette solution.</span><span class="sxs-lookup"><span data-stu-id="017e9-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Instances SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="017e9-203">Avant de pouvoir utiliser un des systèmes de toohello déployé tooconnect hello options, cliquez sur **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="017e9-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Se connecter toohello Instance](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="017e9-205">noms de documentation Hello hello utilisateurs pour chacune des méthodes de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="017e9-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="017e9-206">les mots de passe Hello pour les utilisateurs sont définies de mot de passe principal toohello que vous avez défini au début de hello hello du processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="017e9-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="017e9-207">Dans la documentation de hello, les autres utilisateurs plus fonctionnelles sont répertoriés avec leur mot de passe, vous pouvez utiliser toosign dans toohello déployé le système.</span><span class="sxs-lookup"><span data-stu-id="017e9-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="017e9-208">Par exemple, si vous utilisez hello interface GUI SAP préinstallé sur l’ordinateur de bureau à distance Windows hello, hello système de S/4 peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="017e9-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 Bonjour préinstallé interface GUI SAP](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="017e9-210">Ou, si vous utilisez hello DBACockpit, instance de hello peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="017e9-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 Bonjour DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="017e9-212">En quelques heures, une appliance SAP S/4 intègre est déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="017e9-213">Si vous avez acheté un abonnement de licence d’accès client SAP, SAP prend entièrement en charge déploiements au travers de hello licences d’accès client SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="017e9-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="017e9-214">file d’attente de la prise en charge Hello est BC-VCM-licences d’accès client.</span><span class="sxs-lookup"><span data-stu-id="017e9-214">hello support queue is BC-VCM-CAL.</span></span>







