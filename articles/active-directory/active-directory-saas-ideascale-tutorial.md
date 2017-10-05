---
title: "Didacticiel : Intégration d’Azure Active Directory avec IdeaScale | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="3020a-103">Didacticiel : Intégration d’Azure Active Directory à IdeaScale</span><span class="sxs-lookup"><span data-stu-id="3020a-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="3020a-104">Dans ce didacticiel, vous allez apprendre à intégrer IdeaScale à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3020a-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3020a-105">L’intégration d’IdeaScale à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3020a-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3020a-106">Dans Azure AD, vous pouvez contrôler qui a accès à IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="3020a-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="3020a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à IdeaScale (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3020a-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3020a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3020a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3020a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3020a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3020a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3020a-110">Prerequisites</span></span>

<span data-ttu-id="3020a-111">Pour configurer l’intégration d’Azure AD à IdeaScale, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3020a-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="3020a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3020a-113">Un abonnement IdeaScale pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3020a-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3020a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3020a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3020a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3020a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3020a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3020a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3020a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3020a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3020a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3020a-118">Scenario description</span></span>
<span data-ttu-id="3020a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3020a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3020a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3020a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3020a-121">Ajout d’IdeaScale à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3020a-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="3020a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="3020a-123">Ajout d’IdeaScale à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3020a-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="3020a-124">Pour configurer l’intégration d’IdeaScale à Azure AD, vous devez ajouter IdeaScale à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3020a-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3020a-125">**Pour ajouter IdeaScale à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3020a-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3020a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3020a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3020a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3020a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3020a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3020a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3020a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3020a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3020a-133">Dans la zone de recherche, tapez **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="3020a-133">In the search box, type **IdeaScale**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="3020a-135">Dans le panneau de résultats, sélectionnez **IdeaScale**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3020a-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3020a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3020a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IdeaScale à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3020a-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3020a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur IdeaScale équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3020a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="3020a-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur IdeaScale associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="3020a-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="3020a-141">Dans IdeaScale, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="3020a-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3020a-142">Pour configurer et tester l’authentification unique Azure AD avec IdeaScale, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="3020a-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3020a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3020a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3020a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3020a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3020a-145">**[Création d’un utilisateur de test IdeaScale](#creating-an-ideascale-test-user)** pour avoir un équivalent de Britta Simon dans IdeaScale lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3020a-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3020a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3020a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3020a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3020a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3020a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3020a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="3020a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="3020a-150">**Pour configurer l’authentification unique Azure AD avec IdeaScale, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3020a-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="3020a-151">Dans le portail Azure, sur la page d’intégration de l’application **IdeaScale**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3020a-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3020a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3020a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="3020a-155">Dans la section **IdeaScale Domain and URLs** (Domaine et URL IdeaScale), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3020a-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="3020a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3020a-157">a.</span></span> <span data-ttu-id="3020a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="3020a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="3020a-159">b.</span><span class="sxs-lookup"><span data-stu-id="3020a-159">b.</span></span> <span data-ttu-id="3020a-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3020a-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="3020a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3020a-161">These values are not real.</span></span> <span data-ttu-id="3020a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="3020a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3020a-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique IdeaScale](http://support.ideascale.com/).</span><span class="sxs-lookup"><span data-stu-id="3020a-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="3020a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3020a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="3020a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3020a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3020a-168">Dans la section **IdeaScale Configuration** (Configuration d’IdeaScale), cliquez sur **Configure IdeaScale** (Configurer IdeaScale) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="3020a-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3020a-169">Copiez **l’URL de déconnexion et l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="3020a-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="3020a-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise IdeaScale en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3020a-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="3020a-172">Accédez à **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="3020a-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="3020a-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="3020a-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="3020a-174">Accédez à **Security \> Single Signon Settings**.</span><span class="sxs-lookup"><span data-stu-id="3020a-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="3020a-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="3020a-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="3020a-176">Pour **Single-Signon Type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="3020a-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="3020a-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="3020a-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="3020a-178">Dans la page de boîte de dialogue **Paramètres de l’authentification unique** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3020a-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3020a-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="3020a-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="3020a-180">a.</span><span class="sxs-lookup"><span data-stu-id="3020a-180">a.</span></span> <span data-ttu-id="3020a-181">Dans la zone de texte **SAML IdP Entity ID** (ID d’entité du fournisseur d’identité SAML), collez la valeur de **l’ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3020a-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3020a-182">b.</span><span class="sxs-lookup"><span data-stu-id="3020a-182">b.</span></span> <span data-ttu-id="3020a-183">Copiez le contenu de votre fichier de métadonnées téléchargé depuis le portail Azure et collez-le dans la zone de texte **SAML IdP Metadata** (Métadonnées du fournisseur d’identité SAML).</span><span class="sxs-lookup"><span data-stu-id="3020a-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="3020a-184">c.</span><span class="sxs-lookup"><span data-stu-id="3020a-184">c.</span></span> <span data-ttu-id="3020a-185">Dans la zone de texte **Logout Success URL** (URL de déconnexion réussie), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3020a-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3020a-186">d.</span><span class="sxs-lookup"><span data-stu-id="3020a-186">d.</span></span> <span data-ttu-id="3020a-187">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="3020a-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3020a-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="3020a-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3020a-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="3020a-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3020a-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3020a-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3020a-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="3020a-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3020a-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3020a-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3020a-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3020a-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3020a-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3020a-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3020a-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3020a-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3020a-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3020a-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3020a-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3020a-203">a.</span><span class="sxs-lookup"><span data-stu-id="3020a-203">a.</span></span> <span data-ttu-id="3020a-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3020a-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3020a-205">b.</span><span class="sxs-lookup"><span data-stu-id="3020a-205">b.</span></span> <span data-ttu-id="3020a-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3020a-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3020a-207">c.</span><span class="sxs-lookup"><span data-stu-id="3020a-207">c.</span></span> <span data-ttu-id="3020a-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3020a-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3020a-209">d.</span><span class="sxs-lookup"><span data-stu-id="3020a-209">d.</span></span> <span data-ttu-id="3020a-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3020a-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="3020a-211">Création d’un utilisateur de test IdeaScale</span><span class="sxs-lookup"><span data-stu-id="3020a-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="3020a-212">Pour permettre aux utilisateurs Azure AD de se connecter à IdeaScale, vous devez les approvisionner dans IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="3020a-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="3020a-213">Dans le cas d’IdeaScale, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="3020a-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="3020a-214">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3020a-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3020a-215">Connectez-vous à votre site d’entreprise **IdeaScale** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3020a-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="3020a-216">Accédez à **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="3020a-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="3020a-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="3020a-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="3020a-218">Accédez à **Basic Settings \> Member Management**.</span><span class="sxs-lookup"><span data-stu-id="3020a-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="3020a-219">Cliquez sur **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="3020a-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="3020a-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="3020a-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="3020a-221">Dans la section Add New Member, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3020a-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="3020a-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="3020a-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="3020a-223">a.</span><span class="sxs-lookup"><span data-stu-id="3020a-223">a.</span></span> <span data-ttu-id="3020a-224">Indiquez l’adresse de messagerie d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans la zone de texte **Email Addresses** .</span><span class="sxs-lookup"><span data-stu-id="3020a-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="3020a-225">b.</span><span class="sxs-lookup"><span data-stu-id="3020a-225">b.</span></span> <span data-ttu-id="3020a-226">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="3020a-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="3020a-227">Le titulaire du compte Azure Active Directory reçoit un message électronique avec un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="3020a-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="3020a-228">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par IdeaScale pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3020a-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3020a-229">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3020a-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3020a-230">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="3020a-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3020a-232">**Pour affecter Britta Simon à IdeaScale, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3020a-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="3020a-233">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3020a-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3020a-235">Dans la liste des applications, sélectionnez **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="3020a-235">In the applications list, select **IdeaScale**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="3020a-237">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3020a-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3020a-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3020a-239">Click **Add** button.</span></span> <span data-ttu-id="3020a-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3020a-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3020a-242">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3020a-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3020a-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3020a-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3020a-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3020a-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3020a-245">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3020a-245">Testing single sign-on</span></span>


<span data-ttu-id="3020a-246">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3020a-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3020a-247">Si vous cliquez sur la vignette IdeaScale dans le panneau d’accès, vous devez vous connecter automatiquement à votre application IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="3020a-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3020a-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3020a-248">Additional resources</span></span>

* [<span data-ttu-id="3020a-249">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3020a-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3020a-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3020a-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

