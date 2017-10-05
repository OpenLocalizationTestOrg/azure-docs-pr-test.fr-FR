---
title: "Déploiement de SAP S/4HANA ou BW/4HANA sur une machine virtuelle Azure | Microsoft Docs"
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
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="638a2-103">Déploiement de SAP S/4HANA ou BW/4HANA sur Azure</span><span class="sxs-lookup"><span data-stu-id="638a2-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="638a2-104">Cet article explique comment déployer S/4HANA sur Azure en utilisant SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="638a2-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="638a2-105">Procédez de la même façon pour déployer d’autres solutions SAP HANA, comme BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="638a2-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="638a2-106">Pour plus d’informations sur SAP CAL, accédez au site web [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="638a2-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="638a2-107">Il existe également un blog SAP sur [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="638a2-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="638a2-108">Depuis le 29 mai 2017, vous pouvez utiliser le modèle de déploiement Azure Resource Manager en plus du modèle de déploiement Classic (moins recommandé) pour déployer SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="638a2-109">Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager et d’ignorer le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="638a2-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="638a2-110">Procédure pas à pas de déploiement de la solution</span><span class="sxs-lookup"><span data-stu-id="638a2-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="638a2-111">La séquence de captures d’écran suivante montre comment déployer S/4HANA sur Azure à l’aide de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="638a2-112">Le processus fonctionne de la même façon pour les autres solutions, comme BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="638a2-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="638a2-113">La page **Solutions** montre certaines solutions SAP CAL HANA disponibles sur Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="638a2-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** figure sur la ligne centrale :</span><span class="sxs-lookup"><span data-stu-id="638a2-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![Solutions SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="638a2-116">Création d’un compte dans SAP CAL</span><span class="sxs-lookup"><span data-stu-id="638a2-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="638a2-117">Lorsque vous vous connectez à SAP CAL pour la première fois, utilisez votre identifiant SAP S-User ou un autre identifiant utilisateur enregistré auprès de SAP.</span><span class="sxs-lookup"><span data-stu-id="638a2-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="638a2-118">Ensuite, définissez un compte SAP CAL utilisé par SAP CAL pour déployer des appliances sur Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="638a2-119">Dans la définition du compte, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="638a2-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="638a2-120">a.</span><span class="sxs-lookup"><span data-stu-id="638a2-120">a.</span></span> <span data-ttu-id="638a2-121">Sélectionnez le modèle de déploiement sur Azure (Resource Manager ou Classic).</span><span class="sxs-lookup"><span data-stu-id="638a2-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="638a2-122">b.</span><span class="sxs-lookup"><span data-stu-id="638a2-122">b.</span></span> <span data-ttu-id="638a2-123">Entrez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-123">Enter your Azure subscription.</span></span> <span data-ttu-id="638a2-124">Un compte SAP CAL ne peut être assigné qu’à un seul abonnement.</span><span class="sxs-lookup"><span data-stu-id="638a2-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="638a2-125">Si vous avez besoin de plusieurs abonnements, vous devez créer un autre compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="638a2-126">c.</span><span class="sxs-lookup"><span data-stu-id="638a2-126">c.</span></span> <span data-ttu-id="638a2-127">Accordez à SAP CAL l’autorisation d’effectuer des déploiements dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="638a2-128">Les étapes suivantes montrent comment créer un compte SAP CAL pour les déploiements Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="638a2-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="638a2-129">Si vous disposez déjà d’un compte SAP CAL lié au modèle de déploiement Classic, vous *devez* suivre ces étapes pour créer un nouveau compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="638a2-130">Le nouveau compte SAP CAL doit être déployé dans le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="638a2-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="638a2-131">Créez un compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="638a2-132">La page **Accounts** (Comptes) affiche trois possibilités pour Azure :</span><span class="sxs-lookup"><span data-stu-id="638a2-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="638a2-133">a.</span><span class="sxs-lookup"><span data-stu-id="638a2-133">a.</span></span> <span data-ttu-id="638a2-134">**Microsoft Azure (Classic)** est le modèle de déploiement classique et n’est plus recommandé.</span><span class="sxs-lookup"><span data-stu-id="638a2-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="638a2-135">b.</span><span class="sxs-lookup"><span data-stu-id="638a2-135">b.</span></span> <span data-ttu-id="638a2-136">**Microsoft Azure** est le nouveau modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="638a2-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="638a2-137">c.</span><span class="sxs-lookup"><span data-stu-id="638a2-137">c.</span></span> <span data-ttu-id="638a2-138">**Windows Azure operated by 21Vianet** (Windows Azure géré par 21Vianet) est une option pour la Chine, qui utilise le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="638a2-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="638a2-139">Pour effectuer un déploiement dans le modèle Resource Manager, sélectionnez **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="638a2-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Détails du compte SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="638a2-141">Dans le champ **Subscription ID** (ID d’abonnement), entrez l’ID d’abonnement Azure indiqué dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![Comptes SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="638a2-143">Pour autoriser le déploiement de SAP CAL dans l’abonnement Azure que vous avez défini, cliquez sur **Authorize** (Autoriser).</span><span class="sxs-lookup"><span data-stu-id="638a2-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="638a2-144">La page suivante s’affiche dans l’onglet du navigateur :</span><span class="sxs-lookup"><span data-stu-id="638a2-144">The following page appears in the browser tab:</span></span>

   ![Connexion aux services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="638a2-146">Si plusieurs utilisateurs sont répertoriés, choisissez le compte Microsoft lié en tant que coadministrateur de l’abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="638a2-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="638a2-147">La page suivante s’affiche dans l’onglet du navigateur :</span><span class="sxs-lookup"><span data-stu-id="638a2-147">The following page appears in the browser tab:</span></span>

   ![Confirmation des services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="638a2-149">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="638a2-149">Click **Accept**.</span></span> <span data-ttu-id="638a2-150">Si l’autorisation est accordée, la définition du compte SAP CAL s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="638a2-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="638a2-151">Après une courte période, un message confirme que le processus d’autorisation a réussi.</span><span class="sxs-lookup"><span data-stu-id="638a2-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="638a2-152">Pour assigner le compte SAP CAL nouvellement créé à votre utilisateur, entrez votre identifiant utilisateur dans la zone de texte **User ID** (Identifiant utilisateur) à droite, puis cliquez sur **Add** (Ajouter).</span><span class="sxs-lookup"><span data-stu-id="638a2-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![Association du compte à l’utilisateur](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="638a2-154">Pour associer votre compte à l’utilisateur que vous utilisez pour vous connecter à SAP CAL, cliquez sur **Review** (Revoir).</span><span class="sxs-lookup"><span data-stu-id="638a2-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="638a2-155">Pour créer l’association entre votre utilisateur et le compte SAP CAL nouvellement créé, cliquez sur **Create** (Créer).</span><span class="sxs-lookup"><span data-stu-id="638a2-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![Association d’un utilisateur au compte SAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="638a2-157">Vous avez correctement créé un compte SAP CAL capable d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="638a2-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="638a2-158">Utiliser le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="638a2-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="638a2-159">Déployer des systèmes SAP dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="638a2-160">Vous pouvez à présent commencer à déployer S/4HANA dans votre abonnement utilisateur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="638a2-161">Avant de poursuivre, déterminez si vous êtes lié à des quotas de cœurs pour les machines virtuelles Azure série H.</span><span class="sxs-lookup"><span data-stu-id="638a2-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="638a2-162">Pour le moment, SAP CAL utilise des machines virtuelles Azure série H pour déployer certaines solutions SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="638a2-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="638a2-163">Il se peut que votre abonnement Azure ne soit pas associé à des quotas de cœurs pour la série H.</span><span class="sxs-lookup"><span data-stu-id="638a2-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="638a2-164">Dans ce cas, vous devrez peut-être contacter le support Azure pour obtenir un quota d’au moins 16 cœurs de série H.</span><span class="sxs-lookup"><span data-stu-id="638a2-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="638a2-165">Lorsque vous déployez une solution sur Azure dans SAP CAL, vous constaterez peut-être que vous ne pouvez choisir qu’une seule région Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="638a2-166">Pour effectuer un déploiement dans des régions Azure autres que celle suggérée par SAP CAL, vous devez acheter un abonnement CAL auprès de SAP.</span><span class="sxs-lookup"><span data-stu-id="638a2-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="638a2-167">Vous devrez peut-être également ouvrir un message avec SAP pour que votre compte CAL puisse déployer dans des régions Azure autres que celles suggérées initialement.</span><span class="sxs-lookup"><span data-stu-id="638a2-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="638a2-168">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="638a2-168">Deploy a solution</span></span>

<span data-ttu-id="638a2-169">Nous allons à présent déployer une solution à partir de la page **Solutions** de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="638a2-170">SAP CAL offre deux séquences de déploiement :</span><span class="sxs-lookup"><span data-stu-id="638a2-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="638a2-171">Une séquence de base qui utilise une page pour définir le système à déployer</span><span class="sxs-lookup"><span data-stu-id="638a2-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="638a2-172">Une séquence avancée qui vous offre différents choix en termes de tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="638a2-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="638a2-173">Nous présentons ici la séquence de déploiement de base.</span><span class="sxs-lookup"><span data-stu-id="638a2-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="638a2-174">Sur la page **Account Details** (Détails du compte), effectuez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="638a2-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="638a2-175">a.</span><span class="sxs-lookup"><span data-stu-id="638a2-175">a.</span></span> <span data-ttu-id="638a2-176">Sélectionnez un compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-176">Select an SAP CAL account.</span></span> <span data-ttu-id="638a2-177">(Utilisez un compte associé au déploiement avec le modèle de déploiement Resource Manager.)</span><span class="sxs-lookup"><span data-stu-id="638a2-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="638a2-178">b.</span><span class="sxs-lookup"><span data-stu-id="638a2-178">b.</span></span> <span data-ttu-id="638a2-179">Entrez le nom de l’instance dans le champ **Name** (Nom).</span><span class="sxs-lookup"><span data-stu-id="638a2-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="638a2-180">c.</span><span class="sxs-lookup"><span data-stu-id="638a2-180">c.</span></span> <span data-ttu-id="638a2-181">Sélectionnez une région Azure dans le champ **Region** (Région).</span><span class="sxs-lookup"><span data-stu-id="638a2-181">Select an Azure **Region**.</span></span> <span data-ttu-id="638a2-182">SAP CAL suggère une région.</span><span class="sxs-lookup"><span data-stu-id="638a2-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="638a2-183">Si vous avez besoin d’une autre région Azure et que vous ne possédez pas d’abonnement SAP CAL, vous devez vous procurer un abonnement CAL auprès de SAP.</span><span class="sxs-lookup"><span data-stu-id="638a2-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="638a2-184">d.</span><span class="sxs-lookup"><span data-stu-id="638a2-184">d.</span></span> <span data-ttu-id="638a2-185">Entrez un mot de passe principal pour la solution dans le champ **Password** (Mot de passe). Celui-ci doit comprendre huit ou neuf caractères.</span><span class="sxs-lookup"><span data-stu-id="638a2-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="638a2-186">Le mot de passe est utilisé pour les administrateurs des différents composants.</span><span class="sxs-lookup"><span data-stu-id="638a2-186">The password is used for the administrators of the different components.</span></span>

   ![Mode de base SAP CAL : créer une instance](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="638a2-188">Cliquez sur **Create** (Créer), puis, dans la boîte de message qui s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="638a2-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![Tailles de machine virtuelle prises en charge par SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="638a2-190">Dans la boîte de dialogue **Private Key** (Clé privée), cliquez sur **Store** (Stocker) pour stocker la clé privée dans SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="638a2-191">Pour protéger la clé privée par mot de passe, cliquez sur **Download** (Télécharger).</span><span class="sxs-lookup"><span data-stu-id="638a2-191">To use password protection for the private key, click **Download**.</span></span> 

   ![Clé privée SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="638a2-193">Lisez le **message d’avertissement** SAP CAL, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="638a2-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Avertissement SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="638a2-195">Le déploiement s’effectue.</span><span class="sxs-lookup"><span data-stu-id="638a2-195">Now the deployment takes place.</span></span> <span data-ttu-id="638a2-196">Après un délai variable en fonction de la taille et de la complexité de la solution (SAP CAL en donne une estimation), la solution apparaît comme active et prête à être utilisée.</span><span class="sxs-lookup"><span data-stu-id="638a2-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="638a2-197">Pour trouver les machines virtuelles collectées avec les autres ressources associées dans un groupe de ressources, accédez au Portail Azure :</span><span class="sxs-lookup"><span data-stu-id="638a2-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![Objets SAP CAL déployés dans le nouveau portail](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="638a2-199">Sur le portail SAP CAL, l’état affiché est **Active**.</span><span class="sxs-lookup"><span data-stu-id="638a2-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="638a2-200">Pour vous connecter à la solution, cliquez sur **Connect** (Connexion).</span><span class="sxs-lookup"><span data-stu-id="638a2-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="638a2-201">Plusieurs options de connexion aux différents composants sont déployées au sein de cette solution.</span><span class="sxs-lookup"><span data-stu-id="638a2-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![Instances SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="638a2-203">Pour pouvoir utiliser l’une des options de connexion aux systèmes déployés, cliquez sur **Getting Started Guide** (Guide de prise en main).</span><span class="sxs-lookup"><span data-stu-id="638a2-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![Connexion à l’instance](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="638a2-205">La documentation désigne les utilisateurs pour chacune des méthodes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="638a2-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="638a2-206">Le mot de passe principal défini au début du processus de déploiement définit les mots de passe de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="638a2-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="638a2-207">La documentation répertorie d’autres utilisateurs plus fonctionnels avec leurs mots de passe. Vous pouvez les utiliser pour vous connecter au système déployé.</span><span class="sxs-lookup"><span data-stu-id="638a2-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="638a2-208">Par exemple, si vous utilisez l’interface graphique utilisateur SAP pré-installée sur l’ordinateur Bureau à distance Windows, le système S/4 peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="638a2-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![SM50 dans l’interface graphique utilisateur SAP pré-installée](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="638a2-210">Si vous utilisez DBACockpit, l’instance peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="638a2-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![SM50 dans l’interface graphique utilisateur SAP DBACockpit](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="638a2-212">En quelques heures, une appliance SAP S/4 intègre est déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="638a2-213">Si vous avez acheté un abonnement SAP CAL, SAP prend entièrement en charge les déploiements par le biais de SAP CAL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="638a2-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="638a2-214">La file d’attente de prise en charge est BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="638a2-214">The support queue is BC-VCM-CAL.</span></span>







