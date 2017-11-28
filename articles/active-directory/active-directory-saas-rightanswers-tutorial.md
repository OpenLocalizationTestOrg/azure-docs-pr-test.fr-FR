---
title: "Didacticiel : Intégration d’Azure Active Directory à RightAnswers | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RightAnswers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e5985831598a0e5b1277d2c6cd02b03c919aad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="9efbe-103">Didacticiel : Intégration d’Azure Active Directory à RightAnswers</span><span class="sxs-lookup"><span data-stu-id="9efbe-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="9efbe-104">Dans ce didacticiel, vous allez apprendre à intégrer RightAnswers à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9efbe-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9efbe-105">L’intégration de RightAnswers à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9efbe-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9efbe-106">Dans Azure AD, vous pouvez contrôler qui a accès à RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="9efbe-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="9efbe-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à RightAnswers (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbe-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9efbe-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9efbe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9efbe-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9efbe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9efbe-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9efbe-110">Prerequisites</span></span>

<span data-ttu-id="9efbe-111">Pour configurer l’intégration d’Azure AD à RightAnswers, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9efbe-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="9efbe-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9efbe-113">Un abonnement RightAnswers pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9efbe-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9efbe-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9efbe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9efbe-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9efbe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9efbe-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9efbe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9efbe-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9efbe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9efbe-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9efbe-118">Scenario description</span></span>
<span data-ttu-id="9efbe-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9efbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9efbe-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9efbe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9efbe-121">Ajout de RightAnswers à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9efbe-121">Adding RightAnswers from the gallery</span></span>
2. <span data-ttu-id="9efbe-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="9efbe-123">Ajout de RightAnswers à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9efbe-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="9efbe-124">Pour configurer l’intégration de RightAnswers à Azure AD, vous devez ajouter RightAnswers à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9efbe-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9efbe-125">**Pour ajouter RightAnswers à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9efbe-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbe-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9efbe-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9efbe-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9efbe-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9efbe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9efbe-133">Dans la zone de recherche, tapez **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-133">In the search box, type **RightAnswers**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="9efbe-135">Dans le panneau de résultats, sélectionnez **RightAnswers**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9efbe-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9efbe-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9efbe-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RightAnswers à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9efbe-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9efbe-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RightAnswers équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="9efbe-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur RightAnswers associé.</span><span class="sxs-lookup"><span data-stu-id="9efbe-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="9efbe-141">Dans RightAnswers, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="9efbe-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9efbe-142">Pour configurer et tester l’authentification unique Azure AD avec RightAnswers, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9efbe-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9efbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9efbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9efbe-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9efbe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9efbe-145">**[Création d’un utilisateur de test RightAnswers](#creating-a-rightanswers-test-user)** pour avoir un équivalent de Britta Simon dans RightAnswers lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9efbe-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9efbe-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9efbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9efbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9efbe-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9efbe-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="9efbe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="9efbe-150">**Pour configurer l’authentification unique Azure AD avec RightAnswers, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9efbe-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbe-151">Dans le portail Azure, sur la page d’intégration de l’application **RightAnswers**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9efbe-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9efbe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="9efbe-155">Dans la section **RightAnswers Domain and URLs** (Domaine et URL RightAnswers), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9efbe-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="9efbe-157">a.</span><span class="sxs-lookup"><span data-stu-id="9efbe-157">a.</span></span> <span data-ttu-id="9efbe-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="9efbe-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="9efbe-159">b.</span><span class="sxs-lookup"><span data-stu-id="9efbe-159">b.</span></span> <span data-ttu-id="9efbe-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="9efbe-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9efbe-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9efbe-161">These values are not real.</span></span> <span data-ttu-id="9efbe-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="9efbe-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9efbe-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique RightAnswers](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="9efbe-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="9efbe-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9efbe-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="9efbe-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9efbe-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9efbe-168">Pour configurer l’authentification unique côté **RightAnswers**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique RightAnswers](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="9efbe-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="9efbe-169">Votre équipe de support technique RightAnswers doit se charger de la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9efbe-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="9efbe-170">Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9efbe-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="9efbe-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9efbe-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9efbe-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9efbe-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9efbe-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9efbe-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9efbe-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9efbe-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9efbe-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9efbe-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9efbe-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbe-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9efbe-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9efbe-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9efbe-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9efbe-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9efbe-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9efbe-186">a.</span><span class="sxs-lookup"><span data-stu-id="9efbe-186">a.</span></span> <span data-ttu-id="9efbe-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9efbe-188">b.</span><span class="sxs-lookup"><span data-stu-id="9efbe-188">b.</span></span> <span data-ttu-id="9efbe-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9efbe-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9efbe-190">c.</span><span class="sxs-lookup"><span data-stu-id="9efbe-190">c.</span></span> <span data-ttu-id="9efbe-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9efbe-192">d.</span><span class="sxs-lookup"><span data-stu-id="9efbe-192">d.</span></span> <span data-ttu-id="9efbe-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="9efbe-194">Création d’un utilisateur de test RightAnswers</span><span class="sxs-lookup"><span data-stu-id="9efbe-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="9efbe-195">Pour permettre aux utilisateurs Azure AD de se connecter à RightAnswers, vous devez les approvisionner dans RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="9efbe-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="9efbe-196">Dans le cas de RightAnswers, l’approvisionnement est une tâche automatisée : aucune action de votre part n’est donc nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9efbe-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="9efbe-197">Au besoin, les utilisateurs sont automatiquement créés lors de la première tentative d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9efbe-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="9efbe-198">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par RightAnswers, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="9efbe-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9efbe-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbe-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9efbe-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="9efbe-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9efbe-202">**Pour affecter Britta Simon à RightAnswers, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9efbe-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbe-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9efbe-205">Dans la liste des applications, sélectionnez **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-205">In the applications list, select **RightAnswers**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="9efbe-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9efbe-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-209">Click **Add** button.</span></span> <span data-ttu-id="9efbe-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9efbe-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9efbe-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9efbe-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9efbe-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9efbe-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9efbe-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9efbe-215">Testing single sign-on</span></span>

<span data-ttu-id="9efbe-216">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9efbe-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="9efbe-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9efbe-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="9efbe-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9efbe-218">Additional resources</span></span>

* [<span data-ttu-id="9efbe-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9efbe-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9efbe-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9efbe-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

