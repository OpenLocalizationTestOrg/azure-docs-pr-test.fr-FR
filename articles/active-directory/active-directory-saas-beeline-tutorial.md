---
title: "Didacticiel : Intégration d’Azure Active Directory à BeeLine | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="232fd-103">Didacticiel : Intégration d’Azure Active Directory à Beeline</span><span class="sxs-lookup"><span data-stu-id="232fd-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="232fd-104">Dans ce didacticiel, vous allez apprendre à intégrer BeeLine à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="232fd-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="232fd-105">L’intégration de BeeLine à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="232fd-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="232fd-106">Dans Azure AD, vous pouvez contrôler qui a accès à BeeLine</span><span class="sxs-lookup"><span data-stu-id="232fd-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="232fd-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à BeeLine (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="232fd-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="232fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="232fd-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="232fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="232fd-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="232fd-110">Prerequisites</span></span>

<span data-ttu-id="232fd-111">Pour configurer l’intégration d’Azure AD avec BeeLine, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="232fd-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="232fd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="232fd-113">Un abonnement BeeLine pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="232fd-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="232fd-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="232fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="232fd-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="232fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="232fd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="232fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="232fd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="232fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="232fd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="232fd-118">Scenario description</span></span>
<span data-ttu-id="232fd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="232fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="232fd-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="232fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="232fd-121">Ajout de BeeLine à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="232fd-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="232fd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="232fd-123">Ajout de BeeLine à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="232fd-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="232fd-124">Pour configurer l’intégration de BeeLine avec Azure AD, vous devez ajouter BeeLine, à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="232fd-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="232fd-125">**Pour ajouter BeeLine à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="232fd-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="232fd-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="232fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="232fd-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="232fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="232fd-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="232fd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="232fd-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="232fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="232fd-133">Dans la zone de recherche, tapez **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="232fd-133">In the search box, type **BeeLine**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="232fd-135">Dans le volet de résultats, sélectionnez **BeeLine**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="232fd-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="232fd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="232fd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BeeLine avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="232fd-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="232fd-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur BeeLine équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="232fd-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur BeeLine associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="232fd-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="232fd-141">Dans BeeLine, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="232fd-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="232fd-142">Pour configurer et tester l’authentification unique Azure AD avec BeeLine, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="232fd-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="232fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="232fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="232fd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="232fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="232fd-145">**[Création d’un utilisateur de test BeeLine](#creating-a-beeline-test-user)** pour avoir un équivalent de Britta Simon dans BeeLine lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="232fd-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="232fd-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="232fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="232fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="232fd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="232fd-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BeeLine.</span><span class="sxs-lookup"><span data-stu-id="232fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="232fd-150">**Pour configurer l’authentification unique Azure AD avec BeeLine, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="232fd-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="232fd-151">Dans le portail Azure, dans la page d’intégration de l’application **BeeLine**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="232fd-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="232fd-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="232fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="232fd-155">Dans la section **Domaine et URL BeeLine**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="232fd-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="232fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="232fd-157">a.</span></span> <span data-ttu-id="232fd-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="232fd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="232fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="232fd-159">b.</span></span> <span data-ttu-id="232fd-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="232fd-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="232fd-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="232fd-161">These values are not real.</span></span> <span data-ttu-id="232fd-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="232fd-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="232fd-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique de BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="232fd-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="232fd-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="232fd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="232fd-166">Votre application Beeline attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="232fd-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="232fd-167">Collaborez avec l’[équipe de support technique de BeeLine](https://www.beeline.com/contact-us/) pour identifier tout d’abord l’identificateur d’utilisateur correct qui sera mappé à l’application.</span><span class="sxs-lookup"><span data-stu-id="232fd-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="232fd-168">Suivez également les instructions de l’[équipe de support technique de BeeLine](https://www.beeline.com/contact-us/) concernant l’attribut à utiliser pour ce mappage.</span><span class="sxs-lookup"><span data-stu-id="232fd-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="232fd-169">Vous pouvez gérer la valeur de cet attribut à partir de l’onglet **Attributs utilisateur** de l’application.</span><span class="sxs-lookup"><span data-stu-id="232fd-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="232fd-170">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="232fd-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="232fd-171">Ici, nous avons mis en correspondance la revendication **Identificateur d’utilisateur** avec l’attribut **userprincipalname**, qui fournit l’ID utilisateur unique qui sera envoyé à l’application BeeLine dans chaque réponse SAML correcte.</span><span class="sxs-lookup"><span data-stu-id="232fd-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="232fd-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="232fd-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="232fd-175">Dans la section **Configuration de BeeLine**, cliquez sur **Configurer BeeLine** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="232fd-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="232fd-176">Copiez **l’URL de déconnexion** et l’**ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="232fd-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="232fd-178">Pour configurer l’authentification unique côté **BeeLine**, vous devez envoyer le **XML de métadonnées** téléchargé, l’**ID d’entité SAML** et l’**URL de déconnexion** à l’[équipe de support technique BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="232fd-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="232fd-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="232fd-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="232fd-180">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="232fd-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="232fd-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="232fd-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="232fd-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="232fd-183">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="232fd-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="232fd-185">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="232fd-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="232fd-186">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="232fd-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="232fd-188">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="232fd-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="232fd-190">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="232fd-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="232fd-192">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="232fd-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="232fd-194">a.</span><span class="sxs-lookup"><span data-stu-id="232fd-194">a.</span></span> <span data-ttu-id="232fd-195">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="232fd-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="232fd-196">b.</span><span class="sxs-lookup"><span data-stu-id="232fd-196">b.</span></span> <span data-ttu-id="232fd-197">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="232fd-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="232fd-198">c.</span><span class="sxs-lookup"><span data-stu-id="232fd-198">c.</span></span> <span data-ttu-id="232fd-199">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="232fd-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="232fd-200">d.</span><span class="sxs-lookup"><span data-stu-id="232fd-200">d.</span></span> <span data-ttu-id="232fd-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="232fd-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="232fd-202">Création d’un utilisateur de test BeeLine</span><span class="sxs-lookup"><span data-stu-id="232fd-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="232fd-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Beeline.</span><span class="sxs-lookup"><span data-stu-id="232fd-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="232fd-204">Tous les utilisateurs de BeeLine doivent être approvisionnés dans cette application avant de procéder à l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="232fd-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="232fd-205">Vous devez donc collaborer avec l’[équipe de support technique de Beeline](https://www.beeline.com/contact-us/) pour approvisionner ces utilisateurs dans l’application.</span><span class="sxs-lookup"><span data-stu-id="232fd-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="232fd-206">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="232fd-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="232fd-207">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BeeLine.</span><span class="sxs-lookup"><span data-stu-id="232fd-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="232fd-209">**Pour affecter Britta Simon à BeeLine, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="232fd-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="232fd-210">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="232fd-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="232fd-212">Dans la liste des applications, sélectionnez **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="232fd-212">In the applications list, select **BeeLine**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="232fd-214">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="232fd-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="232fd-216">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="232fd-216">Click **Add** button.</span></span> <span data-ttu-id="232fd-217">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="232fd-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="232fd-219">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="232fd-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="232fd-220">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="232fd-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="232fd-221">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="232fd-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="232fd-222">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="232fd-222">Testing single sign-on</span></span>

<span data-ttu-id="232fd-223">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="232fd-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="232fd-224">Lorsque vous cliquez sur la mosaïque Beeline dans le volet d’accès, vous devez être connecté automatiquement à votre application Beeline.</span><span class="sxs-lookup"><span data-stu-id="232fd-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="232fd-225">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="232fd-225">Additional resources</span></span>

* [<span data-ttu-id="232fd-226">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="232fd-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="232fd-227">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="232fd-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

