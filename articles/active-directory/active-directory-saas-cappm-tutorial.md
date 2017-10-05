---
title: "Didacticiel : Intégration d’Azure Active Directory à CA PPM | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et CA PPM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 4ca9268c26f681fcc96955b6161fe4a119b2dcf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="244f1-103">Didacticiel : Intégration d’Azure Active Directory à CA PPM</span><span class="sxs-lookup"><span data-stu-id="244f1-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="244f1-104">Dans ce didacticiel, vous allez apprendre à intégrer CA PPM à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="244f1-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="244f1-105">L’intégration de CA PPM à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="244f1-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="244f1-106">Dans Azure AD, vous pouvez contrôler qui a accès à CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-106">You can control in Azure AD who has access to CA PPM</span></span>
- <span data-ttu-id="244f1-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à CA PPM (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="244f1-107">You can enable your users to automatically get signed-on to CA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="244f1-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="244f1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="244f1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="244f1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="244f1-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="244f1-110">Prerequisites</span></span>

<span data-ttu-id="244f1-111">Pour configurer l’intégration d’Azure AD avec CA PPM, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="244f1-111">To configure Azure AD integration with CA PPM, you need the following items:</span></span>

- <span data-ttu-id="244f1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="244f1-113">Un abonnement CA PPM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="244f1-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="244f1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="244f1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="244f1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="244f1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="244f1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="244f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="244f1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="244f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="244f1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="244f1-118">Scenario description</span></span>
<span data-ttu-id="244f1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="244f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="244f1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="244f1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="244f1-121">Ajout de CA PPM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="244f1-121">Adding CA PPM from the gallery</span></span>
2. <span data-ttu-id="244f1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-the-gallery"></a><span data-ttu-id="244f1-123">Ajout de CA PPM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="244f1-123">Adding CA PPM from the gallery</span></span>
<span data-ttu-id="244f1-124">Pour configurer l’intégration de CA PPM avec Azure AD, vous devez ajouter CA PPM disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="244f1-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="244f1-125">**Pour ajouter CA PPM à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="244f1-125">**To add CA PPM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="244f1-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="244f1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="244f1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="244f1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="244f1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="244f1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="244f1-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="244f1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="244f1-133">Dans la zone de recherche, tapez **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="244f1-133">In the search box, type **CA PPM**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="244f1-135">Dans le volet de résultats, sélectionnez **CA PPM**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="244f1-135">In the results panel, select **CA PPM**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="244f1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="244f1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec CA PPM avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="244f1-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="244f1-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur CA PPM équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="244f1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span></span> <span data-ttu-id="244f1-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur CA PPM associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="244f1-140">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span></span>

<span data-ttu-id="244f1-141">Dans CA PPM, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="244f1-141">In CA PPM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="244f1-142">Pour configurer et tester l’authentification unique Azure AD avec CA PPM, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="244f1-142">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="244f1-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="244f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="244f1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="244f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="244f1-145">**[Création d’un utilisateur de test CA PPM](#creating-a-ca-ppm-test-user)** pour avoir un équivalent de Britta Simon dans CA PPM lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="244f1-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="244f1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="244f1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="244f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="244f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="244f1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="244f1-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="244f1-150">**Pour configurer l’authentification unique Azure AD avec CA PPM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="244f1-150">**To configure Azure AD single sign-on with CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="244f1-151">Dans le portail Azure, dans la page d’intégration de l’application **CA PPM**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="244f1-151">In the Azure portal, on the **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="244f1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="244f1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="244f1-155">Dans la section **Domaine et URL CA PPM**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="244f1-155">On the **CA PPM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="244f1-157">a.</span><span class="sxs-lookup"><span data-stu-id="244f1-157">a.</span></span> <span data-ttu-id="244f1-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="244f1-158">In the **Identifier** textbox, type a URL using the following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="244f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="244f1-159">b.</span></span> <span data-ttu-id="244f1-160">Dans la zone de texte **URL de réponse**, tapez : `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="244f1-160">In the **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="244f1-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="244f1-161">This value is not real.</span></span> <span data-ttu-id="244f1-162">Mettez à jour cette valeur avec l’identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="244f1-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="244f1-163">Contactez l’[équipe de support technique CA PPM](mailto:catechnicalsupport@ca.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="244f1-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) to get this value.</span></span>
 
4. <span data-ttu-id="244f1-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="244f1-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="244f1-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="244f1-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="244f1-168">Dans la section **Configuration de CA PPM**, cliquez sur **Configurer CA PPM** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="244f1-168">On the **CA PPM Configuration** section, click **Configure CA PPM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="244f1-169">Copiez l’**ID d’entité SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="244f1-169">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="244f1-171">Pour configurer l’authentification unique du côté **CA PPM**, vous devez envoyer le **Certificat (Base64)** téléchargé et l’**ID d’entité SAML** à l’[équipe de support technique de CA PPM](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="244f1-171">To configure single sign-on on **CA PPM** side, you need to send the downloaded **Certificate(Base64)** and **SAML Entity ID** to [CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="244f1-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="244f1-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="244f1-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="244f1-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="244f1-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="244f1-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="244f1-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="244f1-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="244f1-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="244f1-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="244f1-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="244f1-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="244f1-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="244f1-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="244f1-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="244f1-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="244f1-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="244f1-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="244f1-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="244f1-187">a.</span><span class="sxs-lookup"><span data-stu-id="244f1-187">a.</span></span> <span data-ttu-id="244f1-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="244f1-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="244f1-189">b.</span><span class="sxs-lookup"><span data-stu-id="244f1-189">b.</span></span> <span data-ttu-id="244f1-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="244f1-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="244f1-191">c.</span><span class="sxs-lookup"><span data-stu-id="244f1-191">c.</span></span> <span data-ttu-id="244f1-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="244f1-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="244f1-193">d.</span><span class="sxs-lookup"><span data-stu-id="244f1-193">d.</span></span> <span data-ttu-id="244f1-194">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="244f1-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="244f1-195">Création d’un utilisateur de test CA PPM</span><span class="sxs-lookup"><span data-stu-id="244f1-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="244f1-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="244f1-197">Collaborez avec l’[équipe du support technique CA PPM](mailto:catechnicalsupport@ca.com) pour ajouter des utilisateurs sur la plateforme CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) to add the users in the CA PPM platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="244f1-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="244f1-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="244f1-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CA PPM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="244f1-201">**Pour affecter Britta Simon à CA PPM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="244f1-201">**To assign Britta Simon to CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="244f1-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="244f1-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="244f1-204">Dans la liste des applications, sélectionnez **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="244f1-204">In the applications list, select **CA PPM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="244f1-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="244f1-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="244f1-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="244f1-208">Click **Add** button.</span></span> <span data-ttu-id="244f1-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="244f1-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="244f1-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="244f1-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="244f1-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="244f1-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="244f1-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="244f1-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="244f1-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="244f1-214">Testing single sign-on</span></span>

<span data-ttu-id="244f1-215">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="244f1-215">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="244f1-216">Lorsque vous cliquez sur la mosaïque CA PPM dans le volet d’accès, vous devez être connecté automatiquement à votre application CA PPM.</span><span class="sxs-lookup"><span data-stu-id="244f1-216">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="244f1-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="244f1-217">Additional resources</span></span>

* [<span data-ttu-id="244f1-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="244f1-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="244f1-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="244f1-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

