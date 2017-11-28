---
title: "Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure | Microsoft Docs"
description: "Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="ea2ee-103">Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure</span><span class="sxs-lookup"><span data-stu-id="ea2ee-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="ea2ee-104">Cet article explique comment déployer un système SAP IDES exécuté avec SQL Server et le système d’exploitation Windows sur Azure via SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="ea2ee-105">Les captures d’écran montrent la procédure étape par étape.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="ea2ee-106">Pour déployer une autre solution, suivez la même procédure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="ea2ee-107">Pour démarrer avec SAP CAL, accédez au site web [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="ea2ee-108">Il existe également un blog SAP sur le nouveau [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="ea2ee-109">Depuis le 29 mai 2017, vous pouvez utiliser le modèle de déploiement Azure Resource Manager en plus du modèle de déploiement classique pour déployer SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="ea2ee-110">Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager et d’ignorer le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="ea2ee-111">Si vous avez déjà créé un compte SAP CAL qui utilise le modèle classique, *vous devez créer un autre compte SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="ea2ee-112">Ce compte doit être destiné exclusivement au déploiement dans Azure à l’aide du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="ea2ee-113">Après vous être connecté à SAP CAL, la première page vous conduit généralement à la page **Solutions**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="ea2ee-114">Les solutions proposées sur SAP CAL sont toujours plus nombreuses, si bien que vous devrez peut-être en faire défiler plusieurs avant de trouver celle souhaitée.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="ea2ee-115">La solution SAP IDES basée sur Windows mise en surbrillance disponible exclusivement sur Azure montre le processus de déploiement :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![Solutions SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="ea2ee-117">Création d’un compte dans SAP CAL</span><span class="sxs-lookup"><span data-stu-id="ea2ee-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="ea2ee-118">Lorsque vous vous connectez à SAP CAL pour la première fois, utilisez votre identifiant SAP S-User ou un autre identifiant utilisateur enregistré auprès de SAP.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="ea2ee-119">Ensuite, définissez un compte SAP CAL utilisé par SAP CAL pour déployer des appliances sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="ea2ee-120">Dans la définition du compte, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="ea2ee-121">a.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-121">a.</span></span> <span data-ttu-id="ea2ee-122">Sélectionnez le modèle de déploiement sur Azure (Resource Manager ou Classic).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="ea2ee-123">b.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-123">b.</span></span> <span data-ttu-id="ea2ee-124">Entrez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-124">Enter your Azure subscription.</span></span> <span data-ttu-id="ea2ee-125">Un compte SAP CAL ne peut être assigné qu’à un seul abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="ea2ee-126">Si vous avez besoin de plusieurs abonnements, vous devez créer un autre compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="ea2ee-127">c.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-127">c.</span></span> <span data-ttu-id="ea2ee-128">Accordez à SAP CAL l’autorisation d’effectuer des déploiements dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="ea2ee-129">Les étapes suivantes montrent comment créer un compte SAP CAL pour les déploiements Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="ea2ee-130">Si vous disposez déjà d’un compte SAP CAL lié au modèle de déploiement Classic, vous *devez* suivre ces étapes pour créer un nouveau compte SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="ea2ee-131">Le nouveau compte SAP CAL doit être déployé dans le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="ea2ee-132">Pour créer un nouveau compte SAP CAL, vous disposez de deux choix dans la page **Compte** pour Azure :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="ea2ee-133">a.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-133">a.</span></span> <span data-ttu-id="ea2ee-134">**Microsoft Azure (Classic)** est le modèle de déploiement classique et n’est plus recommandé.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="ea2ee-135">b.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-135">b.</span></span> <span data-ttu-id="ea2ee-136">**Microsoft Azure** est le nouveau modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="ea2ee-138">Pour déployer dans le modèle Resource Manager, sélectionnez **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="ea2ee-140">Entrez **l’ID d’abonnement** Azure qui se trouve sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![ID d’abonnement SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="ea2ee-142">Pour autoriser le déploiement de SAP CAL dans l’abonnement Azure que vous avez défini, cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="ea2ee-143">La page suivante s’affiche dans l’onglet du navigateur :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-143">The following page appears in the browser tab:</span></span>

    ![Connexion aux services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="ea2ee-145">Si plusieurs utilisateurs sont répertoriés, choisissez le compte Microsoft lié en tant que coadministrateur de l’abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="ea2ee-146">La page suivante s’affiche dans l’onglet du navigateur :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-146">The following page appears in the browser tab:</span></span>

    ![Confirmation des services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="ea2ee-148">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-148">Click **Accept**.</span></span> <span data-ttu-id="ea2ee-149">Si l’autorisation est accordée, la définition du compte SAP CAL s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="ea2ee-150">Après une courte période, un message confirme que le processus d’autorisation a réussi.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="ea2ee-151">Pour assigner le compte SAP CAL nouvellement créé à votre utilisateur, entrez votre identifiant utilisateur dans la zone de texte **User ID** (Identifiant utilisateur) à droite, puis cliquez sur **Add** (Ajouter).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![Association du compte à l’utilisateur](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="ea2ee-153">Pour associer votre compte à l’utilisateur que vous utilisez pour vous connecter à SAP CAL, cliquez sur **Review** (Revoir).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="ea2ee-154">Pour créer l’association entre votre utilisateur et le compte SAP CAL nouvellement créé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![Association d’un utilisateur au compte](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="ea2ee-156">Vous avez correctement créé un compte SAP CAL capable d’effectuer ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="ea2ee-157">Utiliser le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="ea2ee-158">Déployer des systèmes SAP dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="ea2ee-159">Avant de pouvoir déployer la solution SAP IDES basée sur Windows et SQL Server, vous devrez peut-être souscrire à un abonnement SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="ea2ee-160">Sinon, la solution risque d’apparaître comme **Verrouillée** dans la page de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="ea2ee-161">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="ea2ee-161">Deploy a solution</span></span>
1. <span data-ttu-id="ea2ee-162">Après avoir configuré un compte SAP CAL, sélectionnez la solution **Solution SAP IDES sur Windows et SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="ea2ee-163">Cliquez sur **Créer une instance** et vérifiez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="ea2ee-164">Sur la page **Basic Mode: Create Instance** (Mode de base : Créer une instance), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="ea2ee-165">a.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-165">a.</span></span> <span data-ttu-id="ea2ee-166">Entrez une instance **Nom**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="ea2ee-167">b.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-167">b.</span></span> <span data-ttu-id="ea2ee-168">Sélectionnez une **Région** Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-168">Select an Azure **Region**.</span></span> <span data-ttu-id="ea2ee-169">Vous aurez peut-être besoin d’un abonnement SAP CAL pour avoir le choix entre plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="ea2ee-170">c.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-170">c.</span></span>  <span data-ttu-id="ea2ee-171">Entrez le **Mot de passe** maître pour la solution, comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![SAP CAL - Mode de base : Créer une instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="ea2ee-173">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-173">Click **Create**.</span></span> <span data-ttu-id="ea2ee-174">Après un délai variable en fonction de la taille et de la complexité de la solution (SAP CAL en donne une estimation), la solution apparaît comme active et prête à être utilisée :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![Instances de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="ea2ee-176">Pour trouver le groupe de ressources et tous ses objets créés par SAP CAL, accédez au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="ea2ee-177">Les machines virtuelles sont repérables car elles commencent par le nom d’instance qui a été spécifié dans SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![Objets du groupe de ressources](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="ea2ee-179">Dans le portail SAP CAL, accédez aux instances déployées, puis cliquez sur **Connect** (Connexion).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="ea2ee-180">La fenêtre indépendante suivante apparaît :</span><span class="sxs-lookup"><span data-stu-id="ea2ee-180">The following pop-up window appears:</span></span> 

    ![Connexion à l’instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="ea2ee-182">Avant de pouvoir utiliser l’une des options de connexion aux systèmes déployés, cliquez sur **Getting Started Guide** (Guide de prise en main).</span><span class="sxs-lookup"><span data-stu-id="ea2ee-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="ea2ee-183">La documentation désigne les utilisateurs pour chacune des méthodes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="ea2ee-184">Le mot de passe principal défini au début du processus de déploiement définit les mots de passe de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="ea2ee-185">Dans la documentation, d’autres utilisateurs plus fonctionnels sont répertoriés avec leurs mots de passe, que vous pouvez utiliser pour vous connecter au système déployé.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![Documentation de présentation de SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="ea2ee-187">En quelques heures, un système SAP IDES sain est déployé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="ea2ee-188">Si vous avez acheté un abonnement SAP CAL, SAP prend entièrement en charge les déploiements via SAP CAL sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="ea2ee-189">La file d’attente de prise en charge est BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="ea2ee-189">The support queue is BC-VCM-CAL.</span></span>

