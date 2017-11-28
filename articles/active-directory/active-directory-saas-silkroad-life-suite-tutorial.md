---
title: "Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SilkRoad Life Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="65972-103">Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="65972-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="65972-104">L’objectif de ce didacticiel est de vous montrer comment intégrer SilkRoad Life Suite à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65972-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="65972-105">L’intégration de SilkRoad Life Suite à Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="65972-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="65972-106">Dans Azure AD, vous pouvez contrôler qui a accès à SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="65972-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SilkRoad Life Suite (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65972-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="65972-108">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65972-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65972-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65972-109">Prerequisites</span></span>
<span data-ttu-id="65972-110">Pour configurer l’intégration d’Azure AD avec SilkRoad Life Suite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="65972-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="65972-111">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-111">An Azure AD subscription</span></span>
* <span data-ttu-id="65972-112">Un abonnement SilkRoad Life Suite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="65972-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="65972-113">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="65972-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="65972-114">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="65972-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="65972-115">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="65972-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="65972-116">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65972-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="65972-117">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="65972-117">Scenario Description</span></span>
<span data-ttu-id="65972-118">Ce didacticiel vise à vous permettre de tester l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="65972-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="65972-119">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="65972-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65972-120">Ajout de SilkRoad Life Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="65972-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="65972-121">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="65972-122">Ajouter SilkRoad Life Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="65972-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="65972-123">Pour configurer l’intégration de SilkRoad Life Suite dans Azure AD, vous devez ajouter SilkRoad Life Suite, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="65972-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65972-124">**Pour ajouter SilkRoad Life Suite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65972-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65972-125">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65972-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="65972-127">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="65972-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="65972-128">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="65972-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="65972-130">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="65972-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="65972-132">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="65972-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="65972-134">Dans la zone de recherche, tapez **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="65972-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="65972-136">Dans le volet de résultats, sélectionnez **SilkRoad Life Suite**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="65972-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65972-138">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="65972-139">L’objectif de cette section est de vous montrer comment configurer et tester l’authentification unique Azure AD avec SilkRoad Life Suite avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="65972-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65972-140">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur SilkRoad Life Suite équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65972-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="65972-141">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur SilkRoad Life Suite associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="65972-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="65972-142">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD en tant que valeur du **nom d’utilisateur** dans SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="65972-143">Pour configurer et tester l’authentification unique Azure AD avec SilkRoad Life Suite, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="65972-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65972-144">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="65972-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65972-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65972-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65972-146">**[Création d’un utilisateur de test SilkRoad Life Suite](#creating-a-silkroad-life-suite-test-user)** pour avoir un équivalent de Britta Simon dans SilkRoad Life Suite qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="65972-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="65972-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65972-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65972-148">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="65972-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65972-149">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="65972-150">Cette section vous indique comment activer l’authentification unique Azure AD dans le Portail Azure Classic et comment configurer l’authentification unique dans votre application SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="65972-151">**Pour configurer l’authentification unique Azure AD avec SilkRoad Life Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65972-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="65972-152">Connectez-vous à votre site d’entreprise SilkRoad en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="65972-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="65972-153">Pour obtenir l’accès à l’application d’authentification SilkRoad Life Suite pour configurer la fédération avec Microsoft Azure AD, contactez le support technique SilkRoad ou votre représentant SilkRoad Services.</span><span class="sxs-lookup"><span data-stu-id="65972-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="65972-154">Accédez à **Service Provider** (Fournisseur de services), puis cliquez sur **Federation Details** (Informations sur la fédération).</span><span class="sxs-lookup"><span data-stu-id="65972-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Authentification unique Azure AD][10] 

3. <span data-ttu-id="65972-156">Cliquez sur **Download Federation Metadata**(Télécharger les métadonnées de fédération), puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="65972-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Authentification unique Azure AD][11] 

4. <span data-ttu-id="65972-158">Dans le portail Azure Classic, dans la page d’intégration d’application **SilkRoad Life Suite**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="65972-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 

5. <span data-ttu-id="65972-160">Dans la page **Comment voulez-vous que les utilisateurs se connectent à SilkRoad Life Suite**, sélectionnez **Authentification unique Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][7] 

6. <span data-ttu-id="65972-162">Sur la page **Configurer les paramètres d’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Authentification unique Azure AD][8]   
 1. <span data-ttu-id="65972-164">Dans la zone de texte **URL de connexion**, tapez l’URL utilisée par vos utilisateurs pour se connecter à votre site SilkRoad Life Suite (par ex. : *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="65972-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="65972-165">Ouvrez le fichier de métadonnées **Silkroad** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="65972-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="65972-166">Recherchez la balise **AssertionConsumerService**, puis copiez l’attribut **Location**.</span><span class="sxs-lookup"><span data-stu-id="65972-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Authentification unique Azure AD][21] 
 4. <span data-ttu-id="65972-168">Collez la valeur dans la zone de texte **URL de réponse** .</span><span class="sxs-lookup"><span data-stu-id="65972-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="65972-169">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-169">Click **Next**.</span></span>

6. <span data-ttu-id="65972-170">Dans la page **Configurer l’authentification unique sur SilkRoad Life Suite** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Authentification unique Azure AD][9]  
 1. <span data-ttu-id="65972-172">Cliquez sur Télécharger le certificat, puis enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="65972-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="65972-173">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-173">Click **Next**.</span></span>

7. <span data-ttu-id="65972-174">Dans votre application **SilkRoad**, cliquez sur **Authentication Sources** (Sources d’authentification).</span><span class="sxs-lookup"><span data-stu-id="65972-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Authentification unique Azure AD][12] 

8. <span data-ttu-id="65972-176">Cliquez sur **Add Authentication Source**(Ajouter une source d’authentification).</span><span class="sxs-lookup"><span data-stu-id="65972-176">Click **Add Authentication Source**.</span></span> 
   
    ![Authentification unique Azure AD][13] 

9. <span data-ttu-id="65972-178">Dans la section **Add Authentication Source** (Ajouter une source d’authentification), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Authentification unique Azure AD][14]  
 1. <span data-ttu-id="65972-180">Sous **Option 2 - Metadata File**, cliquez sur **Browse** pour charger le fichier de métadonnées que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="65972-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="65972-181">Cliquez sur **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="65972-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="65972-182">Dans la section **Authentication Sources** (Sources d’authentification), cliquez sur **Edit** (Modifier).</span><span class="sxs-lookup"><span data-stu-id="65972-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Authentification unique Azure AD][15] 

11. <span data-ttu-id="65972-184">Dans la boîte de dialogue **Edit Authentication Source** (Modifier la source d’authentification), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Authentification unique Azure AD][16] 
 1. <span data-ttu-id="65972-186">Pour l’option **Enabled**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="65972-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="65972-187">Dans la zone de texte **IdP Description** , entrez une description de votre configuration (par exemple : *Authentification unique Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="65972-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="65972-188">Dans la zone de texte **IdP Name** , entrez un nom spécifique de votre configuration (par exemple : *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="65972-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="65972-189">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="65972-189">Click **Save**.</span></span>

12. <span data-ttu-id="65972-190">Désactivez toutes les autres sources d’authentification.</span><span class="sxs-lookup"><span data-stu-id="65972-190">Disable all other authentication sources.</span></span> 
    
     ![Authentification unique Azure AD][17]

13. <span data-ttu-id="65972-192">Dans le portail Azure Classic, dans la page **Confirmation de l’authentification unique**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Authentification unique Azure AD][18]

14. <span data-ttu-id="65972-194">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="65972-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Authentification unique Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65972-196">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-196">Create an Azure AD test user</span></span>
<span data-ttu-id="65972-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="65972-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="65972-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65972-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65972-200">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65972-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="65972-202">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="65972-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="65972-203">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="65972-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65972-205">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="65972-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="65972-207">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="65972-209">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="65972-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="65972-210">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65972-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="65972-211">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-211">Click **Next**.</span></span>

6. <span data-ttu-id="65972-212">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="65972-214">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="65972-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="65972-215">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="65972-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="65972-216">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="65972-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="65972-217">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="65972-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="65972-218">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="65972-218">Click **Next**.</span></span>

7. <span data-ttu-id="65972-219">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="65972-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="65972-221">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65972-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="65972-223">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="65972-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="65972-224">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="65972-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="65972-225">Créer un utilisateur de test SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="65972-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="65972-226">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="65972-227">Britta doit disposer d’un identifiant d’authentification unique (parfois appelé *AuthParam*) correspondant à son **adresse e-mail** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65972-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="65972-228">**Pour créer un utilisateur appelé Britta Simon dans SilkRoad Life Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65972-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="65972-229">Demandez à votre équipe de support SilkRoad Life Suite de créer un utilisateur qui a comme attribut **SSO ID** l’**adresse e-mail** de Britta Simon dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65972-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="65972-230">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="65972-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="65972-231">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="65972-233">**Pour attribuer Britta Simon à SilkRoad Life Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65972-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="65972-234">Pour ouvrir l’affichage des applications dans le portail Azure Classic, cliquez dans la vue de répertoire sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="65972-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="65972-236">Dans la liste des applications, sélectionnez **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="65972-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Affecter des utilisateurs][202] 

3. <span data-ttu-id="65972-238">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="65972-238">In the menu on the top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203] 

4. <span data-ttu-id="65972-240">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="65972-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="65972-241">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="65972-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="65972-243">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="65972-243">Test single sign-on</span></span>
<span data-ttu-id="65972-244">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="65972-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="65972-245">Lorsque vous cliquez sur la vignette SilkRoad Life Suite dans le panneau d’accès, vous devez être connecté automatiquement à votre application SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="65972-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65972-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="65972-246">Additional Resources</span></span>
* [<span data-ttu-id="65972-247">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65972-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65972-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="65972-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





