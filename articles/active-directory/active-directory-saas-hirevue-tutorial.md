---
title: "Didacticiel : Intégration d’Azure Active Directory à HireVue | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="18c55-103">Didacticiel : Intégration d’Azure AD à HireVue</span><span class="sxs-lookup"><span data-stu-id="18c55-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="18c55-104">Dans ce didacticiel, vous allez apprendre à intégrer HireVue à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18c55-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18c55-105">L’intégration de HireVue dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="18c55-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18c55-106">Dans Azure AD, vous pouvez contrôler qui a accès à HireVue</span><span class="sxs-lookup"><span data-stu-id="18c55-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="18c55-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à HireVue (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18c55-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="18c55-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="18c55-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18c55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18c55-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="18c55-110">Prerequisites</span></span>

<span data-ttu-id="18c55-111">Pour configurer l’intégration d’Azure AD avec HireVue, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="18c55-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="18c55-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18c55-113">Un abonnement HireVue pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="18c55-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18c55-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="18c55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18c55-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="18c55-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18c55-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="18c55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18c55-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18c55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18c55-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="18c55-118">Scenario description</span></span>
<span data-ttu-id="18c55-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="18c55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18c55-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="18c55-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18c55-121">Ajout de HireVue depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="18c55-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="18c55-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="18c55-123">Ajout de HireVue depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="18c55-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="18c55-124">Pour configurer l’intégration de HireVue avec Azure AD, vous devez ajouter HireVue depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="18c55-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18c55-125">**Pour ajouter HireVue à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18c55-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18c55-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18c55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18c55-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="18c55-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18c55-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18c55-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="18c55-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="18c55-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="18c55-133">Dans la zone de recherche, tapez **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="18c55-133">In the search box, type **HireVue**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="18c55-135">Dans le volet de résultats, sélectionnez **HireVue**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="18c55-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18c55-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18c55-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HireVue avec un utilisateur de test appelé "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="18c55-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18c55-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HireVue équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18c55-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="18c55-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur HireVue associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="18c55-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="18c55-141">Dans HireVue, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="18c55-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18c55-142">Pour configurer et tester l’authentification unique Azure AD avec HireVue, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="18c55-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18c55-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="18c55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18c55-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18c55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18c55-145">**[Création d’un utilisateur de test HireVue](#creating-a-hirevue-test-user)** pour avoir un équivalent de Britta Simon dans HireVue lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="18c55-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="18c55-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18c55-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18c55-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="18c55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18c55-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18c55-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HireVue.</span><span class="sxs-lookup"><span data-stu-id="18c55-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="18c55-150">**Pour configurer l’authentification unique Azure AD avec HireVue, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18c55-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="18c55-151">Dans le portail Azure, dans la page d’intégration de l’application **HireVue**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="18c55-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="18c55-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="18c55-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="18c55-155">Dans la section **Domaine et URL HireVue**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18c55-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="18c55-157">a.</span><span class="sxs-lookup"><span data-stu-id="18c55-157">a.</span></span> <span data-ttu-id="18c55-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="18c55-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="18c55-159">Environnement</span><span class="sxs-lookup"><span data-stu-id="18c55-159">Environment</span></span> | <span data-ttu-id="18c55-160">URL</span><span class="sxs-lookup"><span data-stu-id="18c55-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="18c55-161">Production</span><span class="sxs-lookup"><span data-stu-id="18c55-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="18c55-162">Staging</span><span class="sxs-lookup"><span data-stu-id="18c55-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="18c55-163">b.</span><span class="sxs-lookup"><span data-stu-id="18c55-163">b.</span></span> <span data-ttu-id="18c55-164">Dans la zone de texte **Identificateur**, tapez une URL comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="18c55-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="18c55-165">Environnement</span><span class="sxs-lookup"><span data-stu-id="18c55-165">Environment</span></span> | <span data-ttu-id="18c55-166">URN</span><span class="sxs-lookup"><span data-stu-id="18c55-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="18c55-167">Production</span><span class="sxs-lookup"><span data-stu-id="18c55-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="18c55-168">Staging</span><span class="sxs-lookup"><span data-stu-id="18c55-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="18c55-169">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="18c55-169">These values are not real.</span></span> <span data-ttu-id="18c55-170">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="18c55-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="18c55-171">Pour obtenir ces valeurs, contactez [l’équipe du support client HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="18c55-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="18c55-172">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="18c55-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="18c55-174">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="18c55-174">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18c55-176">Dans la section **Configuration de HireVue**, cliquez sur **Configurer HireVue** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="18c55-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="18c55-177">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="18c55-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="18c55-179">Pour configurer l’authentification unique côté **HireVue**, vous devez envoyer le **Certificat (Base64)** téléchargé et **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support technique HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="18c55-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="18c55-180">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="18c55-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="18c55-181">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="18c55-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18c55-182">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="18c55-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18c55-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18c55-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18c55-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="18c55-185">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="18c55-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="18c55-187">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18c55-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18c55-188">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18c55-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18c55-190">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="18c55-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18c55-192">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="18c55-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18c55-194">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18c55-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18c55-196">a.</span><span class="sxs-lookup"><span data-stu-id="18c55-196">a.</span></span> <span data-ttu-id="18c55-197">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18c55-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18c55-198">b.</span><span class="sxs-lookup"><span data-stu-id="18c55-198">b.</span></span> <span data-ttu-id="18c55-199">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18c55-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18c55-200">c.</span><span class="sxs-lookup"><span data-stu-id="18c55-200">c.</span></span> <span data-ttu-id="18c55-201">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="18c55-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="18c55-202">d.</span><span class="sxs-lookup"><span data-stu-id="18c55-202">d.</span></span> <span data-ttu-id="18c55-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="18c55-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="18c55-204">Création d’un utilisateur de test HireVue</span><span class="sxs-lookup"><span data-stu-id="18c55-204">Creating a HireVue test user</span></span>

<span data-ttu-id="18c55-205">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans HireVue.</span><span class="sxs-lookup"><span data-stu-id="18c55-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="18c55-206">Collaborez avec [l’équipe du support technique HireVue](mailto:samlsupport@hirevue.com) pour ajouter les utilisateurs dans la plateforme HireVue.</span><span class="sxs-lookup"><span data-stu-id="18c55-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="18c55-207">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="18c55-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="18c55-208">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HireVue.</span><span class="sxs-lookup"><span data-stu-id="18c55-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="18c55-210">**Pour affecter Britta Simon à HireVue, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18c55-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="18c55-211">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18c55-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="18c55-213">Dans la liste des applications, sélectionnez **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="18c55-213">In the applications list, select **HireVue**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="18c55-215">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18c55-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="18c55-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="18c55-217">Click **Add** button.</span></span> <span data-ttu-id="18c55-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="18c55-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="18c55-220">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="18c55-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18c55-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18c55-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18c55-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="18c55-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18c55-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="18c55-223">Testing single sign-on</span></span>

<span data-ttu-id="18c55-224">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="18c55-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18c55-225">Lorsque vous cliquez sur la vignette HireVue dans le volet d’accès, vous devez être connecté automatiquement à votre application HireVue.</span><span class="sxs-lookup"><span data-stu-id="18c55-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18c55-226">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="18c55-226">Additional resources</span></span>

* [<span data-ttu-id="18c55-227">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18c55-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18c55-228">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="18c55-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

