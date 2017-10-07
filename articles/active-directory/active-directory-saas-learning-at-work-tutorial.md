---
title: "Didacticiel : Intégration d’Azure Active Directory avec Learning at Work | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Learning at Work."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 941832740689c583a8e857d706c35f3076fa754f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="c715b-103">Didacticiel : Intégration d’Azure Active Directory à Learning at Work</span><span class="sxs-lookup"><span data-stu-id="c715b-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="c715b-104">Dans ce didacticiel, vous allez apprendre à intégrer Learning at Work à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c715b-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c715b-105">L’intégration de Learning at Work dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c715b-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c715b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Learning at Work</span><span class="sxs-lookup"><span data-stu-id="c715b-106">You can control in Azure AD who has access to Learning at Work</span></span>
- <span data-ttu-id="c715b-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Learning at Work (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c715b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c715b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c715b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c715b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c715b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c715b-110">Prerequisites</span></span>

<span data-ttu-id="c715b-111">Pour configurer l’intégration d’Azure AD à Learning at Work, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c715b-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

- <span data-ttu-id="c715b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c715b-113">Un abonnement Learning at Work pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c715b-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c715b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c715b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c715b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c715b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c715b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c715b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c715b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c715b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c715b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c715b-118">Scenario description</span></span>
<span data-ttu-id="c715b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c715b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c715b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c715b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c715b-121">Ajout de Learning at Work à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c715b-121">Adding Learning at Work from the gallery</span></span>
2. <span data-ttu-id="c715b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-the-gallery"></a><span data-ttu-id="c715b-123">Ajout de Learning at Work à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c715b-123">Adding Learning at Work from the gallery</span></span>
<span data-ttu-id="c715b-124">Pour configurer l’intégration de Learning at Work avec Azure AD, vous devez ajouter Learning at Work à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c715b-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c715b-125">**Pour ajouter Learning at Work à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c715b-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c715b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c715b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c715b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c715b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c715b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c715b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c715b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c715b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c715b-133">Dans la zone de recherche, entrez **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="c715b-133">In the search box, type **Learning at Work**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="c715b-135">Dans le panneau de résultats, sélectionnez **Learning at Work**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c715b-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c715b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c715b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Learning at Work à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c715b-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c715b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Learning at Work équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c715b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="c715b-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Learning at Work associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c715b-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="c715b-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="c715b-142">Pour configurer et tester l'authentification unique Azure AD avec Learning at Work, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="c715b-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c715b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c715b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c715b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c715b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c715b-145">**[Création d’un utilisateur de test Learning at Work](#creating-a-learning-at-work-test-user)** pour avoir un équivalent de Britta Simon dans Learning at Work lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c715b-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c715b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c715b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c715b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c715b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c715b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c715b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="c715b-150">**Pour configurer l’authentification unique Azure AD avec Learning at Work, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c715b-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="c715b-151">Dans le portail Azure, sur la page d’intégration de l’application **Learning at Work**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c715b-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c715b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c715b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="c715b-155">Dans la section **Learning at Work Domain and URLs** (Domaine et URL Learning at Work), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c715b-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="c715b-157">a.</span><span class="sxs-lookup"><span data-stu-id="c715b-157">a.</span></span> <span data-ttu-id="c715b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="c715b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="c715b-159">b.</span><span class="sxs-lookup"><span data-stu-id="c715b-159">b.</span></span> <span data-ttu-id="c715b-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="c715b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c715b-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c715b-161">These values are not the real.</span></span> <span data-ttu-id="c715b-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="c715b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c715b-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Learning at Work](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="c715b-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c715b-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c715b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="c715b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c715b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c715b-168">Dans la section **Learning at Work Configuration** (Configuration de Learning at Work), cliquez sur **Configure Learning at Work** (Configurer Learning at Work) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="c715b-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c715b-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c715b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="c715b-171">Pour configurer l’authentification unique côté **Learning at Work**, vous devez envoyer le fichier **XML des métadonnées** téléchargé, **l’ID d’entité SAML**, **l’URL du service d’authentification unique SAML** et **l’URL de déconnexion** au [support technique Learning at Work](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="c715b-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="c715b-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c715b-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c715b-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c715b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c715b-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c715b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c715b-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c715b-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c715b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c715b-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c715b-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c715b-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c715b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c715b-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c715b-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c715b-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c715b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c715b-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c715b-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c715b-187">a.</span><span class="sxs-lookup"><span data-stu-id="c715b-187">a.</span></span> <span data-ttu-id="c715b-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c715b-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c715b-189">b.</span><span class="sxs-lookup"><span data-stu-id="c715b-189">b.</span></span> <span data-ttu-id="c715b-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c715b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c715b-191">c.</span><span class="sxs-lookup"><span data-stu-id="c715b-191">c.</span></span> <span data-ttu-id="c715b-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c715b-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c715b-193">d.</span><span class="sxs-lookup"><span data-stu-id="c715b-193">d.</span></span> <span data-ttu-id="c715b-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c715b-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="c715b-195">Création d’un utilisateur de test Learning at Work</span><span class="sxs-lookup"><span data-stu-id="c715b-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="c715b-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="c715b-197">Travaillez avec le [support technique de Learning at Work](https://www.learninga-z.com/site/contact/support) pour ajouter les utilisateurs à la plateforme Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c715b-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c715b-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c715b-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c715b-201">**Pour affecter Britta Simon à Learning at Work, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c715b-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="c715b-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c715b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c715b-204">Dans la liste des applications, sélectionnez **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="c715b-204">In the applications list, select **Learning at Work**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="c715b-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c715b-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c715b-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c715b-208">Click **Add** button.</span></span> <span data-ttu-id="c715b-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c715b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c715b-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c715b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c715b-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c715b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c715b-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c715b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c715b-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c715b-214">Testing single sign-on</span></span>

<span data-ttu-id="c715b-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c715b-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c715b-216">Quand vous cliquez sur la vignette Learning at Work dans le volet d’accès, vous devez être connecté automatiquement à votre application Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="c715b-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>
<span data-ttu-id="c715b-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c715b-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c715b-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c715b-218">Additional resources</span></span>

* [<span data-ttu-id="c715b-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c715b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c715b-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c715b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png
