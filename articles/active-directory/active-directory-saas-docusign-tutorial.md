---
title: "Didacticiel : Intégration d’Azure Active Directory avec DocuSign | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="aa33c-103">Didacticiel : Intégration d’Azure Active Directory avec DocuSign</span><span class="sxs-lookup"><span data-stu-id="aa33c-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="aa33c-104">Dans ce didacticiel, vous allez apprendre à intégrer DocuSign à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa33c-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa33c-105">L’intégration de DocuSign à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="aa33c-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa33c-106">Dans Azure AD, vous pouvez contrôler qui a accès à DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="aa33c-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à DocuSign (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa33c-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa33c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="aa33c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa33c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa33c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa33c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aa33c-110">Prerequisites</span></span>

<span data-ttu-id="aa33c-111">Pour configurer l’intégration d’Azure AD avec DocuSign, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa33c-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="aa33c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa33c-113">Un abonnement DocuSign pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="aa33c-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa33c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="aa33c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa33c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="aa33c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa33c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="aa33c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa33c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa33c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa33c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="aa33c-118">Scenario description</span></span>
<span data-ttu-id="aa33c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="aa33c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa33c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa33c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa33c-121">Ajout de DocuSign à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="aa33c-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="aa33c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="aa33c-123">Ajout de DocuSign à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="aa33c-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="aa33c-124">Pour configurer l’intégration de DocuSign à Azure AD, vous devez ajouter DocuSign à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="aa33c-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa33c-125">**Pour ajouter DocuSign à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="aa33c-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa33c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa33c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa33c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="aa33c-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="aa33c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="aa33c-133">Dans la zone de recherche, tapez **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-133">In the search box, type **DocuSign**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="aa33c-135">Dans le volet de résultats, sélectionnez **DocuSign**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="aa33c-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa33c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa33c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec DocuSign, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="aa33c-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa33c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur DocuSign correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa33c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="aa33c-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur associé dans DocuSign doit être établie.</span><span class="sxs-lookup"><span data-stu-id="aa33c-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="aa33c-141">Pour cela, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="aa33c-142">Pour configurer et tester l’authentification unique Azure AD avec DocuSign, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa33c-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa33c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="aa33c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa33c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa33c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa33c-145">**[Création d’un utilisateur test DocuSign](#creating-a-docusign-test-user)** pour avoir un équivalent de Britta Simon dans DocuSign lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="aa33c-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa33c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa33c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa33c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="aa33c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa33c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa33c-149">Dans cette section, vous allez activer l’authentification unique Azure AD sur le portail Azure et configurer l’authentification unique dans votre application DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="aa33c-150">**Pour configurer l’authentification unique Azure AD avec DocuSign, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="aa33c-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="aa33c-151">Sur le portail Azure, à la page d’intégration de l’application **DocuSign**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="aa33c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="aa33c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="aa33c-155">Dans la section **Certificat de signature SAML**, cliquez sur **Télécharger le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="aa33c-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="aa33c-157">Dans la section **Configuration de DocuSign** du portail Azure, cliquez sur **Configurer DocuSign** pour ouvrir la fenêtre Configurer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="aa33c-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="aa33c-158">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="aa33c-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="aa33c-160">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration DocuSign** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="aa33c-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="aa33c-161">Dans le menu de navigation à gauche, cliquez sur **Domaines**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configuration de l'authentification unique][51]

7. <span data-ttu-id="aa33c-163">Dans le volet droit, cliquez sur **Claim Domain**(Revendiquer un domaine).</span><span class="sxs-lookup"><span data-stu-id="aa33c-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configuration de l'authentification unique][52]

8. <span data-ttu-id="aa33c-165">Dans la boîte de dialogue **Claim a domain** (Revendiquer un domaine), dans la zone de texte **Nom du domaine**, indiquez votre domaine d’entreprise, puis cliquez sur **Revendication**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="aa33c-166">Veillez à vérifier le domaine et assurez-vous que son état est actif.</span><span class="sxs-lookup"><span data-stu-id="aa33c-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configuration de l'authentification unique][53]

9. <span data-ttu-id="aa33c-168">Dans le menu de gauche, cliquez sur **Fournisseurs d’identité**</span><span class="sxs-lookup"><span data-stu-id="aa33c-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configuration de l'authentification unique][54]
10. <span data-ttu-id="aa33c-170">Dans le volet de droite, cliquez sur **Add Identity Provider**(Ajouter un fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="aa33c-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuration de l'authentification unique][55]

11. <span data-ttu-id="aa33c-172">Dans la page **Identity Provider Settings** (Paramètres du fournisseur d’identité), effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa33c-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configuration de l'authentification unique][56]

    <span data-ttu-id="aa33c-174">a.</span><span class="sxs-lookup"><span data-stu-id="aa33c-174">a.</span></span> <span data-ttu-id="aa33c-175">Dans la zone de texte **Nom** , entrez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="aa33c-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="aa33c-176">N’utilisez pas d’espaces.</span><span class="sxs-lookup"><span data-stu-id="aa33c-176">Do not use spaces.</span></span>

    <span data-ttu-id="aa33c-177">b.</span><span class="sxs-lookup"><span data-stu-id="aa33c-177">b.</span></span> <span data-ttu-id="aa33c-178">Collez l’**ID d’entité SAML** dans la zone de texte **Émetteur du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="aa33c-179">c.</span><span class="sxs-lookup"><span data-stu-id="aa33c-179">c.</span></span> <span data-ttu-id="aa33c-180">Collez l’**URL du service d’authentification unique SAML** dans la zone de texte **URL de connexion du fournisseur identité**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="aa33c-181">d.</span><span class="sxs-lookup"><span data-stu-id="aa33c-181">d.</span></span> <span data-ttu-id="aa33c-182">Collez l’**URL de déconnexion** dans la zone de texte **URL de déconnexion du fournisseur identité**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="aa33c-183">e.</span><span class="sxs-lookup"><span data-stu-id="aa33c-183">e.</span></span> <span data-ttu-id="aa33c-184">Sélectionnez **Sign AuthN Request**(Signer la demande d’authentification).</span><span class="sxs-lookup"><span data-stu-id="aa33c-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="aa33c-185">f.</span><span class="sxs-lookup"><span data-stu-id="aa33c-185">f.</span></span> <span data-ttu-id="aa33c-186">Sous **Send AuthN request by** (Envoyer la demande d’authentification par), sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="aa33c-187">g.</span><span class="sxs-lookup"><span data-stu-id="aa33c-187">g.</span></span> <span data-ttu-id="aa33c-188">Sous **Send logout request by** (Envoyer la demande de déconnexion par), sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="aa33c-189">Dans la section **Custom Attribute Mapping** (Mappage d’attributs personnalisé), choisissez le champ à mapper avec la revendication Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa33c-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="aa33c-190">Dans cet exemple, la revendication **emailaddress** est mappée sur la valeur de **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="aa33c-191">Il s’agit du nom de revendication par défaut d’Azure AD pour la revendication de courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="aa33c-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="aa33c-192">Utilisez l’**identificateur d’utilisateur** approprié pour mapper l’utilisateur d’Azure AD au mappage utilisateur DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="aa33c-193">Sélectionnez le champ correct et entrez la valeur appropriée en fonction des paramètres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="aa33c-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Configuration de l'authentification unique][57]

13. <span data-ttu-id="aa33c-195">Dans la section **Identity Provider Certificate** (Certificat du fournisseur d’identité), cliquez sur **Ajouter un certificat**, puis chargez le certificat que vous avez téléchargé à partir du portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa33c-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configuration de l'authentification unique][58]

14. <span data-ttu-id="aa33c-197">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-197">Click **Save**.</span></span>

15. <span data-ttu-id="aa33c-198">Dans la section **Identity Providers** (Fournisseurs d’identité), cliquez **Actions**, puis cliquez sur **Endpoints** (Points de terminaison).</span><span class="sxs-lookup"><span data-stu-id="aa33c-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuration de l'authentification unique][59]
 
16. <span data-ttu-id="aa33c-200">Dans la section **View SAML 2.0 Endpoints** (Afficher les points de terminaison SAML 2.0) du **portail d’administration DocuSign**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa33c-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Configuration de l'authentification unique][60]
   
    <span data-ttu-id="aa33c-202">a.</span><span class="sxs-lookup"><span data-stu-id="aa33c-202">a.</span></span> <span data-ttu-id="aa33c-203">Copiez la valeur **Service Provider Issuer URL** (URL de l’émetteur du fournisseur de service), puis collez-la dans la zone de texte **Identificateur** dans la section du portail Azure **DocuSign Domain and URLs** (Domaine et URL DocuSign), suivant le modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="aa33c-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="aa33c-204">b.</span><span class="sxs-lookup"><span data-stu-id="aa33c-204">b.</span></span> <span data-ttu-id="aa33c-205">Copiez la valeur **Service Provider Login URL** (URL de connexion du fournisseur d’identité), puis collez-la dans la zone de texte **URL d’authentification** dans la section du portail Azure **DocuSign Domain and URLs** (Domaine et URL DocuSign), suivant le modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="aa33c-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="aa33c-207">c.</span><span class="sxs-lookup"><span data-stu-id="aa33c-207">c.</span></span>  <span data-ttu-id="aa33c-208">Cliquez sur **Fermer**</span><span class="sxs-lookup"><span data-stu-id="aa33c-208">Click **Close**</span></span>
    
17. <span data-ttu-id="aa33c-209">Sur le portail Azure, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-209">On the Azure portal, click **Save**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="aa33c-211">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="aa33c-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa33c-212">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="aa33c-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa33c-213">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa33c-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa33c-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa33c-215">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aa33c-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="aa33c-217">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="aa33c-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa33c-218">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa33c-220">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa33c-222">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa33c-224">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="aa33c-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa33c-226">a.</span><span class="sxs-lookup"><span data-stu-id="aa33c-226">a.</span></span> <span data-ttu-id="aa33c-227">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa33c-228">b.</span><span class="sxs-lookup"><span data-stu-id="aa33c-228">b.</span></span> <span data-ttu-id="aa33c-229">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa33c-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa33c-230">c.</span><span class="sxs-lookup"><span data-stu-id="aa33c-230">c.</span></span> <span data-ttu-id="aa33c-231">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa33c-232">d.</span><span class="sxs-lookup"><span data-stu-id="aa33c-232">d.</span></span> <span data-ttu-id="aa33c-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="aa33c-234">Création d’un utilisateur de test DocuSign</span><span class="sxs-lookup"><span data-stu-id="aa33c-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="aa33c-235">L’application prend en charge l’**approvisionnement juste-à-temps des utilisateurs** et, après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="aa33c-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aa33c-236">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa33c-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aa33c-237">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="aa33c-239">**Pour assigner Britta Simon à DocuSign, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="aa33c-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="aa33c-240">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="aa33c-242">Dans la liste des applications, sélectionnez **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-242">In the applications list, select **DocuSign**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="aa33c-244">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="aa33c-246">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-246">Click **Add** button.</span></span> <span data-ttu-id="aa33c-247">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="aa33c-249">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="aa33c-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa33c-250">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa33c-251">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="aa33c-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa33c-252">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="aa33c-252">Testing single sign-on</span></span>

<span data-ttu-id="aa33c-253">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="aa33c-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aa33c-254">Lorsque vous cliquez sur la vignette DocuSign dans le volet d’accès, vous devez être connecté automatiquement à votre application DocuSign.</span><span class="sxs-lookup"><span data-stu-id="aa33c-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="aa33c-255">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa33c-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aa33c-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="aa33c-256">Additional resources</span></span>

* [<span data-ttu-id="aa33c-257">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa33c-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa33c-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="aa33c-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="aa33c-259">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="aa33c-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

