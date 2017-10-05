---
title: "Didacticiel : Intégration d’Azure Active Directory à Wingspan eTMF | Microsoft Azure"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 8c76fb64229abcad0cabb910e7c170979a79d839
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="f63f9-103">Didacticiel : Intégration d’Azure Active Directory à Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="f63f9-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="f63f9-104">Dans ce didacticiel, vous découvrez comment intégrer Wingspan eTMF à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f63f9-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f63f9-105">L’intégration de Wingspan eTMF à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f63f9-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f63f9-106">Dans Azure AD, vous pouvez contrôler qui a accès à Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="f63f9-107">Vous pouvez permettre aux utilisateurs de se connecter automatiquement à Wingspan eTMF (par le biais de l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f63f9-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f63f9-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f63f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f63f9-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f63f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f63f9-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f63f9-110">Prerequisites</span></span>

<span data-ttu-id="f63f9-111">Pour configurer l’intégration d’Azure AD à Wingspan eTMF, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f63f9-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="f63f9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f63f9-113">Un abonnement Wingspan eTMF pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f63f9-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f63f9-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f63f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f63f9-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f63f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f63f9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f63f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f63f9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f63f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f63f9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f63f9-118">Scenario description</span></span>
<span data-ttu-id="f63f9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f63f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f63f9-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f63f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f63f9-121">Ajout de Wingspan eTMF à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f63f9-121">Adding Wingspan eTMF from the gallery</span></span>
2. <span data-ttu-id="f63f9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="f63f9-123">Ajout de Wingspan eTMF à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f63f9-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="f63f9-124">Pour configurer l’intégration de Wingspan eTMF à Azure AD, vous devez ajouter Wingspan eTMF à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f63f9-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f63f9-125">**Pour ajouter Wingspan eTMF à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f63f9-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f63f9-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f63f9-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f63f9-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f63f9-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f63f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f63f9-133">Dans la zone de recherche, tapez **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="f63f9-135">Dans le volet de résultats, sélectionnez **Wingspan eTMF** puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f63f9-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f63f9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f63f9-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec Wingspan eTMF, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f63f9-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f63f9-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Wingspan eTMF équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f63f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="f63f9-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Wingspan eTMF associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="f63f9-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="f63f9-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="f63f9-142">Pour configurer et tester l’authentification unique Azure AD avec Wingspan eTMF, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f63f9-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f63f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f63f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f63f9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f63f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f63f9-145">**[Création d’un utilisateur de test Wingspan eTMF](#creating-a-wingspan-etmf-test-user)** pour avoir un équivalent de Britta Simon dans Wingspan eTMF lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f63f9-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f63f9-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f63f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f63f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f63f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f63f9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f63f9-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et vous configurez l’authentification unique dans votre application Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="f63f9-150">**Pour configurer l’authentification unique Azure AD avec Wingspan eTMF, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f63f9-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="f63f9-151">Dans le portail Azure, sur la page d’intégration de l’application **Wingspan eTMF**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f63f9-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f63f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="f63f9-155">Dans la section **Domaine et URL Wingspan eTMF**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f63f9-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="f63f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="f63f9-157">a.</span></span> <span data-ttu-id="f63f9-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="f63f9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="f63f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="f63f9-159">b.</span></span> <span data-ttu-id="f63f9-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="f63f9-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="f63f9-161">c.</span><span class="sxs-lookup"><span data-stu-id="f63f9-161">c.</span></span> <span data-ttu-id="f63f9-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="f63f9-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f63f9-163">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f63f9-163">These values are not the real.</span></span> <span data-ttu-id="f63f9-164">Mettre à jour ces valeurs avec l’URL d’ouverture de session réelle, un identificateur et une URL de réponse, avec notamment les noms réels du client et de l’instance.</span><span class="sxs-lookup"><span data-stu-id="f63f9-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="f63f9-165">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Wingspan eTMF](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="f63f9-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="f63f9-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f63f9-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="f63f9-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f63f9-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f63f9-170">Pour configurer l’authentification unique du côté **Wingspan eTMF**, vous devez envoyer le fichier **XML des métadonnées** téléchargé au [support technique de Wingspan eTMF](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="f63f9-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="f63f9-171">Ils configurent les éléments pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="f63f9-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f63f9-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="f63f9-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f63f9-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="f63f9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f63f9-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f63f9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f63f9-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="f63f9-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f63f9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f63f9-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f63f9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f63f9-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f63f9-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f63f9-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f63f9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f63f9-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f63f9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f63f9-187">a.</span><span class="sxs-lookup"><span data-stu-id="f63f9-187">a.</span></span> <span data-ttu-id="f63f9-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f63f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="f63f9-189">b.</span></span> <span data-ttu-id="f63f9-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f63f9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f63f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="f63f9-191">c.</span></span> <span data-ttu-id="f63f9-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f63f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="f63f9-193">d.</span></span> <span data-ttu-id="f63f9-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="f63f9-195">Création d’un utilisateur de test de Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="f63f9-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="f63f9-196">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="f63f9-197">Collaborez avec le [support technique de Wingspan eTMF](http://www.wingspan.com/contact-us/) pour ajouter des utilisateurs dans l’application Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="f63f9-198">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f63f9-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f63f9-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f63f9-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f63f9-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f63f9-202">**Pour affecter Britta Simon à Wingspan eTMF, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f63f9-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="f63f9-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f63f9-205">Dans la liste des applications, sélectionnez **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="f63f9-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f63f9-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-209">Click **Add** button.</span></span> <span data-ttu-id="f63f9-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f63f9-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f63f9-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f63f9-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f63f9-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f63f9-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f63f9-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f63f9-215">Testing single sign-on</span></span>

<span data-ttu-id="f63f9-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f63f9-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="f63f9-217">Cliquez sur la vignette Wingspan eTMF dans le volet d’accès. Vous êtes redirigé vers la page d’authentification d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="f63f9-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="f63f9-218">Une fois authentifié, vous êtes connecté à votre application Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f63f9-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="f63f9-219">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f63f9-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f63f9-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f63f9-220">Additional resources</span></span>

* [<span data-ttu-id="f63f9-221">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f63f9-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f63f9-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f63f9-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

