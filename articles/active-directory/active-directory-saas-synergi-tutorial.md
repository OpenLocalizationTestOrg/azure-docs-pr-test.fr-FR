---
title: "Didacticiel : Intégration d’Azure Active Directory avec Synergi | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Synergi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: dedbe96fbb26bc34c4d7e213892b318f0e6fef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="7c101-103">Didacticiel : Intégration d’Azure Active Directory avec Synergi</span><span class="sxs-lookup"><span data-stu-id="7c101-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="7c101-104">Dans ce didacticiel, vous allez apprendre à intégrer Synergi avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c101-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c101-105">L’intégration de Synergi avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7c101-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c101-106">Dans Azure AD, vous pouvez contrôler qui a accès à Synergi.</span><span class="sxs-lookup"><span data-stu-id="7c101-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="7c101-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Synergi (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c101-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7c101-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7c101-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7c101-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c101-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c101-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7c101-110">Prerequisites</span></span>

<span data-ttu-id="7c101-111">Pour configurer l’intégration d’Azure AD avec Synergi, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7c101-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="7c101-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c101-113">Un abonnement Synergi pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7c101-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c101-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7c101-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c101-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7c101-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c101-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7c101-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c101-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c101-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c101-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7c101-118">Scenario description</span></span>
<span data-ttu-id="7c101-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7c101-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c101-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c101-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c101-121">Ajout de Synergi depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="7c101-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="7c101-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="7c101-123">Ajout de Synergi depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="7c101-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="7c101-124">Pour configurer l’intégration de Synergi avec Azure AD, vous devez ajouter Synergi, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7c101-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c101-125">**Pour ajouter Synergi depuis la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c101-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c101-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c101-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="7c101-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7c101-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c101-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7c101-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="7c101-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7c101-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="7c101-133">Dans la zone de recherche, tapez **Synergi**, sélectionnez **Synergi** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7c101-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi dans la liste des résultats](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7c101-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7c101-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Synergi avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7c101-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c101-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Synergi équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c101-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="7c101-138">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Synergi associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="7c101-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="7c101-139">Dans Synergi, attribuez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="7c101-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c101-140">Pour configurer et tester l’authentification unique Azure AD avec Synergi, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c101-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c101-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7c101-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c101-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c101-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c101-143">**[Création d’un utilisateur de test Synergi](#create-a-synergi-test-user)** pour avoir un équivalent de Britta Simon dans Synergi lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="7c101-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c101-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c101-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c101-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7c101-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7c101-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7c101-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Synergi.</span><span class="sxs-lookup"><span data-stu-id="7c101-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="7c101-148">**Pour configurer l’authentification unique Azure AD avec Synergi, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c101-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="7c101-149">Dans le portail Azure, dans la page d’intégration de l’application **Synergi**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7c101-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="7c101-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7c101-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="7c101-153">Dans la section **Domaine et URL Synergi**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c101-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="7c101-155">a.</span><span class="sxs-lookup"><span data-stu-id="7c101-155">a.</span></span> <span data-ttu-id="7c101-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="7c101-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="7c101-157">b.</span><span class="sxs-lookup"><span data-stu-id="7c101-157">b.</span></span> <span data-ttu-id="7c101-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="7c101-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c101-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7c101-159">These values are not real.</span></span> <span data-ttu-id="7c101-160">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="7c101-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7c101-161">Pour obtenir ces valeurs, contactez [l’équipe du support Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7c101-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="7c101-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7c101-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="7c101-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7c101-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c101-166">Dans la section **Configuration de Synergi**, cliquez sur **Configurer Synergi** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7c101-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c101-167">Copiez **l’URL de déconnexion et l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="7c101-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuration de Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="7c101-169">Pour configurer l’authentification unique du côté **Synergi**, vous devez envoyer le **Certificat (Base64) téléchargé, l’URL de déconnexion et l’ID d’entité SAML** à [l’équipe du support Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7c101-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="7c101-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7c101-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c101-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7c101-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c101-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c101-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7c101-173">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-173">Create an Azure AD test user</span></span>

<span data-ttu-id="7c101-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7c101-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="7c101-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c101-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c101-177">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c101-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7c101-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7c101-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7c101-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7c101-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7c101-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c101-183">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7c101-185">a.</span><span class="sxs-lookup"><span data-stu-id="7c101-185">a.</span></span> <span data-ttu-id="7c101-186">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c101-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c101-187">b.</span><span class="sxs-lookup"><span data-stu-id="7c101-187">b.</span></span> <span data-ttu-id="7c101-188">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c101-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7c101-189">c.</span><span class="sxs-lookup"><span data-stu-id="7c101-189">c.</span></span> <span data-ttu-id="7c101-190">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7c101-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7c101-191">d.</span><span class="sxs-lookup"><span data-stu-id="7c101-191">d.</span></span> <span data-ttu-id="7c101-192">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7c101-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="7c101-193">Créer un utilisateur de test Synergi</span><span class="sxs-lookup"><span data-stu-id="7c101-193">Create a Synergi test user</span></span>

<span data-ttu-id="7c101-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Synergi.</span><span class="sxs-lookup"><span data-stu-id="7c101-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="7c101-195">Pour ajouter des utilisateurs dans la plateforme Synergi, contactez [l’équipe du support Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7c101-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="7c101-196">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7c101-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7c101-197">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c101-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="7c101-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Synergi.</span><span class="sxs-lookup"><span data-stu-id="7c101-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="7c101-200">**Pour affecter Britta Simon à Synergi, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c101-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="7c101-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7c101-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7c101-203">Dans la liste des applications, sélectionnez **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="7c101-203">In the applications list, select **Synergi**.</span></span>

    ![Lien Synergi dans la liste des applications](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="7c101-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7c101-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="7c101-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7c101-207">Click **Add** button.</span></span> <span data-ttu-id="7c101-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7c101-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="7c101-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7c101-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c101-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7c101-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c101-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7c101-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7c101-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7c101-213">Test single sign-on</span></span>

<span data-ttu-id="7c101-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7c101-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7c101-215">Lorsque vous cliquez sur la mosaïque Synergi dans le volet d’accès, vous devez être connecté automatiquement à votre application Synergi.</span><span class="sxs-lookup"><span data-stu-id="7c101-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="7c101-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c101-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7c101-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7c101-217">Additional resources</span></span>

* [<span data-ttu-id="7c101-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c101-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c101-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7c101-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

