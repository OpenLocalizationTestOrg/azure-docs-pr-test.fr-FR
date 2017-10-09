---
title: aaaDeploy SAP IDE EHP7 SP3 pour la version 6.0 de ERP SAP sur Azure | Documents Microsoft
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
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="be836-103">Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure</span><span class="sxs-lookup"><span data-stu-id="be836-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="be836-104">Cet article décrit comment toodeploy un SAP IDE fonctionnant avec SQL Server et le système d’exploitation de Windows hello sur Azure via hello bibliothèque de matériel du Cloud SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="be836-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="be836-105">captures d’écran Hello montrent étape par étape hello.</span><span class="sxs-lookup"><span data-stu-id="be836-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="be836-106">toodeploy une autre solution, suivez hello les mêmes étapes.</span><span class="sxs-lookup"><span data-stu-id="be836-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="be836-107">toostart avec hello SAP licences d’accès client, accédez toohello [SAP Cloud application bibliothèque](https://cal.sap.com/) site Web.</span><span class="sxs-lookup"><span data-stu-id="be836-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="be836-108">SAP possède également un blog sur hello nouvelle [SAP Cloud Appliance bibliothèque 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="be836-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="be836-109">Comme de 29 mai 2017, vous pouvez utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello en outre toohello préféré au moins un déploiement classique de modèle toodeploy hello licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="be836-110">Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager hello et de ne pas tenir compte de modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="be836-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="be836-111">Si vous déjà créé un compte SAP licences d’accès client qui utilise le modèle classique de hello, *vous devez toocreate un autre compte de licences d’accès client SAP*.</span><span class="sxs-lookup"><span data-stu-id="be836-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="be836-112">Ce compte doit tooexclusively déployer dans Azure à l’aide du modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="be836-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="be836-113">Après vous être connecté toohello licence d’accès client SAP, première page de hello vous conduit généralement toohello **Solutions** page.</span><span class="sxs-lookup"><span data-stu-id="be836-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="be836-114">solutions Hello proposées sur hello SAP licences d’accès client sont en augmentation, donc vous devrez peut-être tooscroll mal les solutions hello toofind vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="be836-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="be836-115">solution IDE de SAP basés sur Windows Hello mis en surbrillance est exclusivement disponible sur Azure décrit les processus de déploiement hello :</span><span class="sxs-lookup"><span data-stu-id="be836-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Solutions SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="be836-117">Créer un compte dans hello licences d’accès client SAP</span><span class="sxs-lookup"><span data-stu-id="be836-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="be836-118">toosign dans toohello SAP CAL pour hello première fois, utilisez votre utilisateur S SAP ou autre utilisateur enregistré dans SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="be836-119">Définissez ensuite un compte d’accès client SAP qui est utilisé par les appareils de toodeploy hello licences d’accès client SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="be836-120">Dans la définition du compte de hello, vous devez :</span><span class="sxs-lookup"><span data-stu-id="be836-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="be836-121">a.</span><span class="sxs-lookup"><span data-stu-id="be836-121">a.</span></span> <span data-ttu-id="be836-122">Sélectionnez le modèle de déploiement hello sur Azure (Gestionnaire de ressources ou classique).</span><span class="sxs-lookup"><span data-stu-id="be836-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="be836-123">b.</span><span class="sxs-lookup"><span data-stu-id="be836-123">b.</span></span> <span data-ttu-id="be836-124">Entrez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-124">Enter your Azure subscription.</span></span> <span data-ttu-id="be836-125">Abonnement tooone uniquement peut être affecté à un compte de la licence d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="be836-126">Si vous avez besoin de plus d’un abonnement, vous devez toocreate un autre compte de licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="be836-127">c.</span><span class="sxs-lookup"><span data-stu-id="be836-127">c.</span></span> <span data-ttu-id="be836-128">Donnez à hello SAP CAL autorisation toodeploy dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="be836-129">les étapes suivantes Hello montrent comment toocreate une licence d’accès client SAP compte pour les déploiements de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="be836-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="be836-130">Si vous avez déjà un compte de licence d’accès client SAP qui est le modèle de déploiement classique toohello lié, vous *devez* toofollow ces toocreate étapes un nouveau compte de licences d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="be836-131">nouveau compte de licences d’accès client SAP Hello doit toodeploy dans le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="be836-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="be836-132">toocreate une licence d’accès client SAP nouveau compte, hello **comptes** page affiche deux possibilités pour Azure :</span><span class="sxs-lookup"><span data-stu-id="be836-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="be836-133">a.</span><span class="sxs-lookup"><span data-stu-id="be836-133">a.</span></span> <span data-ttu-id="be836-134">**Microsoft Azure (classique)** est le modèle de déploiement classique hello et n’est plus recommandée.</span><span class="sxs-lookup"><span data-stu-id="be836-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="be836-135">b.</span><span class="sxs-lookup"><span data-stu-id="be836-135">b.</span></span> <span data-ttu-id="be836-136">**Microsoft Azure** est le nouveau modèle de déploiement Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="be836-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="be836-138">toodeploy dans le modèle de gestionnaire de ressources hello, sélectionnez **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="be836-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="be836-140">Entrez hello Azure **ID d’abonnement** qui se trouvent sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![ID d’abonnement SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="be836-142">toodeploy de licences d’accès client SAP tooauthorize hello en hello abonnement Azure que vous avez définies, cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="be836-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="be836-143">Hello suivant page s’affiche dans l’onglet du navigateur hello :</span><span class="sxs-lookup"><span data-stu-id="be836-143">hello following page appears in hello browser tab:</span></span>

    ![Connexion aux services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="be836-145">Si plusieurs utilisateurs est répertorié, choisissez le compte Microsoft hello coadministrator de hello toobe lié Hello abonnement Azure que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="be836-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="be836-146">Hello suivant page s’affiche dans l’onglet du navigateur hello :</span><span class="sxs-lookup"><span data-stu-id="be836-146">hello following page appears in hello browser tab:</span></span>

    ![Confirmation des services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="be836-148">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="be836-148">Click **Accept**.</span></span> <span data-ttu-id="be836-149">Si l’autorisation de hello est réussie, hello définition du compte de licences d’accès client SAP s’affiche à nouveau.</span><span class="sxs-lookup"><span data-stu-id="be836-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="be836-150">Après une courte période, un message confirme que le processus d’autorisation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="be836-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="be836-151">tooassign hello nouvellement créée tooyour utilisateur du compte de licences d’accès client SAP, entrez votre **ID utilisateur** dans hello de zone de texte hello droit et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="be836-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Association de compte toouser](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="be836-153">Cliquez sur votre compte utilisateur de hello utiliser toosign dans toohello SAP licences d’accès client, de tooassociate **révision**.</span><span class="sxs-lookup"><span data-stu-id="be836-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="be836-154">association de hello toocreate entre votre utilisateur et le compte de licences d’accès client SAP hello nouvellement créé, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="be836-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Association tooaccount utilisateur](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="be836-156">Vous avez correctement créé un compte SAP CAL capable d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="be836-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="be836-157">Utilisez le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="be836-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="be836-158">Déployer des systèmes SAP dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="be836-159">Avant de pouvoir déployer des solutions SAP IDE hello basée sur Windows et SQL Server, vous devrez peut-être toosign pour un abonnement de licence d’accès client SAP.</span><span class="sxs-lookup"><span data-stu-id="be836-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="be836-160">Dans le cas contraire, les solutions hello risquent d’apparaître en tant que **verrouillé** sur la page de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="be836-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="be836-161">Déployer une solution</span><span class="sxs-lookup"><span data-stu-id="be836-161">Deploy a solution</span></span>
1. <span data-ttu-id="be836-162">Après avoir configuré un compte de la licence d’accès client SAP, sélectionnez **hello solution SAP IDE sur Windows et SQL Server** solution.</span><span class="sxs-lookup"><span data-stu-id="be836-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="be836-163">Cliquez sur **création d’une Instance**et vérifiez les conditions d’utilisation et les termes du contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="be836-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="be836-164">Sur hello **Mode de base : création d’une Instance** page, vous devez :</span><span class="sxs-lookup"><span data-stu-id="be836-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="be836-165">a.</span><span class="sxs-lookup"><span data-stu-id="be836-165">a.</span></span> <span data-ttu-id="be836-166">Entrez une instance **Nom**.</span><span class="sxs-lookup"><span data-stu-id="be836-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="be836-167">b.</span><span class="sxs-lookup"><span data-stu-id="be836-167">b.</span></span> <span data-ttu-id="be836-168">Sélectionnez une région Azure dans le champ **Region** (Région).</span><span class="sxs-lookup"><span data-stu-id="be836-168">Select an Azure **Region**.</span></span> <span data-ttu-id="be836-169">Vous devrez peut-être une tooget d’abonnement de licence d’accès client SAP plusieurs régions Azure proposées.</span><span class="sxs-lookup"><span data-stu-id="be836-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="be836-170">c.</span><span class="sxs-lookup"><span data-stu-id="be836-170">c.</span></span>  <span data-ttu-id="be836-171">Entrez le masque de hello **mot de passe** solution hello, comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="be836-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![Mode de base SAP CAL : créer une instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="be836-173">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="be836-173">Click **Create**.</span></span> <span data-ttu-id="be836-174">Après un certain temps, selon la taille de hello et la complexité de la solution de hello (licence d’accès client SAP fournit une estimation hello), hello état est affiché comme actif et prêt à être utilisé :</span><span class="sxs-lookup"><span data-stu-id="be836-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Instances SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="be836-176">groupe de ressources toofind hello et tous ses objets qui ont été créés par hello des licences d’accès client SAP, accédez toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="be836-177">machine virtuelle de Hello sont accessibles en commençant par le même nom qui a été fourni en hello SAP licences d’accès client de l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="be836-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Objets du groupe de ressources](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="be836-179">Sur le portail de licences d’accès client SAP hello, accédez toohello déployé instances, puis cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="be836-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="be836-180">Hello suivant la fenêtre contextuelle s’affiche :</span><span class="sxs-lookup"><span data-stu-id="be836-180">hello following pop-up window appears:</span></span> 

    ![Se connecter toohello Instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="be836-182">Avant de pouvoir utiliser un des systèmes de toohello déployé tooconnect hello options, cliquez sur **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="be836-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="be836-183">noms de documentation Hello hello utilisateurs pour chacune des méthodes de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="be836-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="be836-184">les mots de passe Hello pour les utilisateurs sont définies de mot de passe principal toohello que vous avez défini au début de hello hello du processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="be836-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="be836-185">Dans la documentation de hello, les autres utilisateurs plus fonctionnelles sont répertoriés avec leur mot de passe, vous pouvez utiliser toosign dans toohello déployé le système.</span><span class="sxs-lookup"><span data-stu-id="be836-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![Documentation de présentation de SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="be836-187">En quelques heures, un système SAP IDES sain est déployé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="be836-188">Si vous avez acheté un abonnement de licence d’accès client SAP, SAP prend entièrement en charge déploiements au travers de hello licences d’accès client SAP sur Azure.</span><span class="sxs-lookup"><span data-stu-id="be836-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="be836-189">file d’attente de la prise en charge Hello est BC-VCM-licences d’accès client.</span><span class="sxs-lookup"><span data-stu-id="be836-189">hello support queue is BC-VCM-CAL.</span></span>

