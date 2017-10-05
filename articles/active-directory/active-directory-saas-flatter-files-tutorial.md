---
title: "Didacticiel : Intégration d’Azure AD à Flatter Files | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Flatter Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="fbf39-103">Didacticiel : Intégration d’Azure Active Directory à Flatter Files</span><span class="sxs-lookup"><span data-stu-id="fbf39-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="fbf39-104">Dans ce didacticiel, vous allez apprendre à intégrer Flatter Files à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbf39-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbf39-105">L’intégration de Flatter Files dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fbf39-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbf39-106">Dans Azure AD, vous pouvez contrôler qui a accès à Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="fbf39-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="fbf39-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Flatter Files (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf39-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbf39-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbf39-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbf39-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbf39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf39-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fbf39-110">Prerequisites</span></span>

<span data-ttu-id="fbf39-111">Pour configurer l’intégration d’Azure AD avec Flatter Files, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fbf39-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="fbf39-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbf39-113">Un abonnement Flatter Files pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fbf39-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbf39-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fbf39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbf39-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fbf39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbf39-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fbf39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbf39-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbf39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbf39-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fbf39-118">Scenario description</span></span>
<span data-ttu-id="fbf39-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fbf39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbf39-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbf39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbf39-121">Ajout de Flatter Files à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbf39-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="fbf39-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="fbf39-123">Ajout de Flatter Files à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbf39-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="fbf39-124">Pour configurer l’intégration de Flatter Files avec Azure AD, vous devez ajouter Flatter Files à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fbf39-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbf39-125">**Pour ajouter Flatter Files à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbf39-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf39-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbf39-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbf39-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fbf39-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbf39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fbf39-133">Dans la zone de recherche, entrez **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-133">In the search box, type **Flatter Files**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="fbf39-135">Dans le volet de résultats, sélectionnez **Flatter Files**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="fbf39-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbf39-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbf39-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Flatter Files avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fbf39-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbf39-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Flatter Files équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf39-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="fbf39-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Flatter Files associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="fbf39-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="fbf39-141">Dans Flatter Files, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="fbf39-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fbf39-142">Pour configurer et tester l’authentification unique Azure AD avec Flatter Files, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbf39-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbf39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fbf39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbf39-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbf39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbf39-145">**[Création d’un utilisateur de test Flatter Files](#creating-a-flatter-files-test-user)** pour avoir un équivalent de Britta Simon dans Flatter Files lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="fbf39-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbf39-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbf39-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbf39-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fbf39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbf39-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbf39-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="fbf39-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="fbf39-150">**Pour configurer l’authentification unique Azure AD avec Flatter Files, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbf39-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf39-151">Dans le portail Azure, sur la page d’intégration de l’application **Flatter Files**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fbf39-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fbf39-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="fbf39-155">Dans la section **Domaine et URL Flatter Files**, l’utilisateur n’aura pas à effectuer les étapes que l’application a déjà intégrées préalablement avec Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf39-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="fbf39-157">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fbf39-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="fbf39-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fbf39-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbf39-161">Dans la section **Configuration de Flatter Files**, cliquez sur **Configurer Flatter Files** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fbf39-162">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="fbf39-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="fbf39-164">Connectez-vous à votre application Flatter Files en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fbf39-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="fbf39-165">Cliquez sur **TABLEAU DE BORD**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="fbf39-167">Cliquez sur **Settings**, puis procédez comme suit dans l’onglet **Company** :</span><span class="sxs-lookup"><span data-stu-id="fbf39-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="fbf39-169">a.</span><span class="sxs-lookup"><span data-stu-id="fbf39-169">a.</span></span> <span data-ttu-id="fbf39-170">Sélectionnez **Use SAML 2.0 for Authentication**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="fbf39-171">b.</span><span class="sxs-lookup"><span data-stu-id="fbf39-171">b.</span></span> <span data-ttu-id="fbf39-172">Cliquez sur **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="fbf39-173">Dans la boîte de dialogue **SAML Configuration** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbf39-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="fbf39-175">a.</span><span class="sxs-lookup"><span data-stu-id="fbf39-175">a.</span></span> <span data-ttu-id="fbf39-176">Dans la zone de texte **Domaine**, entrez votre domaine enregistré.</span><span class="sxs-lookup"><span data-stu-id="fbf39-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="fbf39-177">Si vous n’avez pas encore de domaine enregistré, contactez votre équipe de support Flatter Files via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="fbf39-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="fbf39-178">b.</span><span class="sxs-lookup"><span data-stu-id="fbf39-178">b.</span></span> <span data-ttu-id="fbf39-179">Dans la zone de texte **URL du fournisseur d’identité**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf39-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="fbf39-180">c.</span><span class="sxs-lookup"><span data-stu-id="fbf39-180">c.</span></span>  <span data-ttu-id="fbf39-181">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Identity provider certificate (Certificat du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="fbf39-182">d.</span><span class="sxs-lookup"><span data-stu-id="fbf39-182">d.</span></span> <span data-ttu-id="fbf39-183">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="fbf39-184">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="fbf39-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fbf39-185">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="fbf39-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fbf39-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbf39-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbf39-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbf39-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf39-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fbf39-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbf39-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf39-191">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbf39-193">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbf39-195">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbf39-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbf39-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbf39-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbf39-199">a.</span><span class="sxs-lookup"><span data-stu-id="fbf39-199">a.</span></span> <span data-ttu-id="fbf39-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbf39-201">b.</span><span class="sxs-lookup"><span data-stu-id="fbf39-201">b.</span></span> <span data-ttu-id="fbf39-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbf39-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbf39-203">c.</span><span class="sxs-lookup"><span data-stu-id="fbf39-203">c.</span></span> <span data-ttu-id="fbf39-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbf39-205">d.</span><span class="sxs-lookup"><span data-stu-id="fbf39-205">d.</span></span> <span data-ttu-id="fbf39-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="fbf39-207">Création d’un utilisateur de test Flatter Files</span><span class="sxs-lookup"><span data-stu-id="fbf39-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="fbf39-208">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="fbf39-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="fbf39-209">**Pour créer un utilisateur appelé Britta Simon dans Flatter Files, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbf39-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf39-210">Connectez-vous à votre site d’entreprise **Flatter Files** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fbf39-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="fbf39-211">Dans le volet de navigation situé à gauche, cliquez sur **Paramètres**, puis sur l’onglet **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Créer un utilisateur Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="fbf39-213">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="fbf39-214">Dans la boîte de dialogue **Ajouter un utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbf39-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Créer un utilisateur Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="fbf39-216">a.</span><span class="sxs-lookup"><span data-stu-id="fbf39-216">a.</span></span> <span data-ttu-id="fbf39-217">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="fbf39-218">b.</span><span class="sxs-lookup"><span data-stu-id="fbf39-218">b.</span></span> <span data-ttu-id="fbf39-219">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="fbf39-220">c.</span><span class="sxs-lookup"><span data-stu-id="fbf39-220">c.</span></span> <span data-ttu-id="fbf39-221">Dans la zone de texte **Adresse e-mail**, tapez l’adresse de messagerie de Britta indiquée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf39-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="fbf39-222">d.</span><span class="sxs-lookup"><span data-stu-id="fbf39-222">d.</span></span> <span data-ttu-id="fbf39-223">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbf39-224">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbf39-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbf39-225">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="fbf39-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fbf39-227">**Pour affecter Britta Simon à Flatter Files, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbf39-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf39-228">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fbf39-230">Dans la liste des applications, sélectionnez **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-230">In the applications list, select **Flatter Files**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="fbf39-232">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fbf39-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-234">Click **Add** button.</span></span> <span data-ttu-id="fbf39-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fbf39-237">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fbf39-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbf39-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbf39-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbf39-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbf39-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fbf39-240">Testing single sign-on</span></span>

<span data-ttu-id="fbf39-241">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="fbf39-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fbf39-242">Lorsque vous cliquez sur la vignette Flatter Files dans le volet d’accès, vous devez être connecté automatiquement à votre application Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="fbf39-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="fbf39-243">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbf39-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbf39-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fbf39-244">Additional resources</span></span>

* [<span data-ttu-id="fbf39-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbf39-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbf39-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fbf39-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

