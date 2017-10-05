---
title: "Didacticiel : Intégration d’Azure Active Directory à Insperity ExpensAble | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="89e50-103">Didacticiel : Intégration d’Azure Active Directory à Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="89e50-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="89e50-104">Dans ce didacticiel, vous allez apprendre à intégrer Insperity ExpensAble à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89e50-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89e50-105">L’intégration d’Insperity ExpensAble dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="89e50-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89e50-106">Dans Azure AD, vous pouvez contrôler qui a accès à Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="89e50-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Insperity ExpensAble (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e50-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89e50-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="89e50-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="89e50-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89e50-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e50-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89e50-110">Prerequisites</span></span>

<span data-ttu-id="89e50-111">Pour configurer l'intégration d'Azure AD avec Insperity ExpensAble, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89e50-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="89e50-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89e50-113">Un abonnement Insperity ExpensAble pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="89e50-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89e50-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="89e50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89e50-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="89e50-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89e50-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="89e50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89e50-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89e50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89e50-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="89e50-118">Scenario description</span></span>
<span data-ttu-id="89e50-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="89e50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89e50-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e50-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89e50-121">Ajout d’Insperity ExpensAble à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="89e50-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="89e50-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="89e50-123">Ajout d’Insperity ExpensAble à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="89e50-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="89e50-124">Pour configurer l'intégration d’Insperity ExpensAble avec Azure AD, vous devez ajouter Insperity ExpensAble, disponible dans la galerie, à votre liste d'applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="89e50-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89e50-125">**Pour ajouter Insperity ExpensAble à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89e50-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89e50-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89e50-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89e50-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="89e50-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89e50-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89e50-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="89e50-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="89e50-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="89e50-133">Dans la zone de recherche, tapez **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="89e50-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="89e50-135">Dans le volet de résultats, sélectionnez **Insperity ExpensAble**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="89e50-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89e50-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89e50-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Insperity ExpensAble avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="89e50-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89e50-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Insperity ExpensAble équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e50-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="89e50-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Insperity ExpensAble associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="89e50-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="89e50-141">Dans Insperity ExpensAble, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="89e50-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89e50-142">Pour configurer et tester l’authentification unique Azure AD avec Insperity ExpensAble, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="89e50-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89e50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="89e50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89e50-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89e50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89e50-145">**[Création d’un utilisateur de test Insperity ExpensAble](#creating-an-insperity-expensable-test-user)** - pour avoir un équivalent de Britta Simon dans Insperity ExpensAble lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e50-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89e50-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e50-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89e50-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="89e50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89e50-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89e50-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="89e50-150">**Pour configurer l’authentification unique Azure AD avec Insperity ExpensAble, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89e50-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="89e50-151">Dans le portail Azure, sur la page d’intégration de l’application **Insperity ExpensAble**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="89e50-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="89e50-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89e50-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="89e50-155">Dans la section **Domaine et URL Insperity ExpensAble**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e50-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="89e50-157">a.</span><span class="sxs-lookup"><span data-stu-id="89e50-157">a.</span></span> <span data-ttu-id="89e50-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="89e50-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89e50-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="89e50-159">This value is not real.</span></span> <span data-ttu-id="89e50-160">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="89e50-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="89e50-161">Contactez l’[équipe de support technique Insperity ExpensAble](http://expensable.com/support/support-overview) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="89e50-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="89e50-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="89e50-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="89e50-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="89e50-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89e50-166">Dans la section **Configuration d’Insperity ExpensAble**, cliquez sur **Configurer Insperity ExpensAble** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="89e50-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="89e50-167">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="89e50-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="89e50-169">Pour configurer l’authentification unique côté **Insperity ExpensAble**, vous devez envoyer le fichier **XML des métadonnées** téléchargé, **l’URL du service d’authentification unique SAML** et **l’ID d’entité SAML** à [l’équipe de support d’Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="89e50-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="89e50-170">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="89e50-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="89e50-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="89e50-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89e50-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="89e50-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89e50-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89e50-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89e50-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="89e50-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89e50-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="89e50-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89e50-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89e50-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89e50-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89e50-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="89e50-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89e50-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="89e50-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89e50-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89e50-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89e50-186">a.</span><span class="sxs-lookup"><span data-stu-id="89e50-186">a.</span></span> <span data-ttu-id="89e50-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89e50-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89e50-188">b.</span><span class="sxs-lookup"><span data-stu-id="89e50-188">b.</span></span> <span data-ttu-id="89e50-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89e50-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89e50-190">c.</span><span class="sxs-lookup"><span data-stu-id="89e50-190">c.</span></span> <span data-ttu-id="89e50-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="89e50-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="89e50-192">d.</span><span class="sxs-lookup"><span data-stu-id="89e50-192">d.</span></span> <span data-ttu-id="89e50-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="89e50-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="89e50-194">Création d’un utilisateur de test Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="89e50-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="89e50-195">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="89e50-196">Collaborez avec [l’équipe du support technique d’Insperity ExpensAble](http://expensable.com/support/support-overview) pour ajouter des utilisateurs dans le compte Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="89e50-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e50-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="89e50-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="89e50-200">**Pour affecter Britta Simon à Insperity ExpensAble, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89e50-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="89e50-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89e50-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="89e50-203">Dans la liste des applications, sélectionnez **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="89e50-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="89e50-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89e50-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="89e50-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="89e50-207">Click **Add** button.</span></span> <span data-ttu-id="89e50-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="89e50-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="89e50-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="89e50-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89e50-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89e50-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89e50-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="89e50-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89e50-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="89e50-213">Testing single sign-on</span></span>

<span data-ttu-id="89e50-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="89e50-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="89e50-215">Quand vous cliquez sur la vignette Insperity ExpensAble dans le volet d’accès, vous devez être connecté automatiquement à votre application Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="89e50-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="89e50-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89e50-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89e50-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="89e50-217">Additional resources</span></span>

* [<span data-ttu-id="89e50-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89e50-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89e50-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="89e50-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

