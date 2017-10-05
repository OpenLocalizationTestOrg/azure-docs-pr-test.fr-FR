---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Confluence | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kantega SSO pour Confluence."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ec11decbff4cf2f6c39b40228e349312fd86da00
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="16c7b-103">Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Confluence</span><span class="sxs-lookup"><span data-stu-id="16c7b-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="16c7b-104">Dans ce didacticiel, vous allez apprendre à intégrer Kantega SSO pour Confluence avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16c7b-104">In this tutorial, you learn how to integrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16c7b-105">L’intégration de Kantega SSO pour Confluence avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="16c7b-105">Integrating Kantega SSO for Confluence with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16c7b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Kantega SSO pour Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-106">You can control in Azure AD who has access to Kantega SSO for Confluence</span></span>
- <span data-ttu-id="16c7b-107">Vous pouvez autoriser vos utilisateurs à s’authentifier automatiquement auprès de Kantega SSO pour Confluence (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16c7b-107">You can enable your users to automatically get signed-on to Kantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16c7b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16c7b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16c7b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16c7b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16c7b-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="16c7b-110">Prerequisites</span></span>

<span data-ttu-id="16c7b-111">Pour configurer l’intégration d’Azure AD avec Kantega SSO pour Confluence, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="16c7b-111">To configure Azure AD integration with Kantega SSO for Confluence, you need the following items:</span></span>

- <span data-ttu-id="16c7b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16c7b-113">Un abonnement Kantega SSO pour Confluence pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="16c7b-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16c7b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="16c7b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16c7b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="16c7b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16c7b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="16c7b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16c7b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16c7b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16c7b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="16c7b-118">Scenario description</span></span>
<span data-ttu-id="16c7b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="16c7b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16c7b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="16c7b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16c7b-121">Ajout de Kantega SSO pour Confluence à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="16c7b-121">Adding Kantega SSO for Confluence from the gallery</span></span>
2. <span data-ttu-id="16c7b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-the-gallery"></a><span data-ttu-id="16c7b-123">Ajout de Kantega SSO pour Confluence à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="16c7b-123">Adding Kantega SSO for Confluence from the gallery</span></span>
<span data-ttu-id="16c7b-124">Pour configurer l’intégration de Kantega SSO pour Confluence dans Azure AD, vous devez ajouter Kantega SSO pour Confluence à partir de la galerie à la liste des applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="16c7b-124">To configure the integration of Kantega SSO for Confluence into Azure AD, you need to add Kantega SSO for Confluence from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16c7b-125">**Pour ajouter Kantega SSO pour Confluence à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16c7b-125">**To add Kantega SSO for Confluence from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16c7b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16c7b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16c7b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="16c7b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16c7b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="16c7b-133">Dans la zone de recherche, tapez **Kantega SSO pour Confluence**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-133">In the search box, type **Kantega SSO for Confluence**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. <span data-ttu-id="16c7b-135">Dans le volet de résultats, sélectionnez **Kantega SSO pour Confluence**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="16c7b-135">In the results panel, select **Kantega SSO for Confluence**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16c7b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16c7b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kantega SSO pour Confluence sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="16c7b-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16c7b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur équivalent à l’utilisateur Azure AD dans Kantega SSO pour Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Confluence is to a user in Azure AD.</span></span> <span data-ttu-id="16c7b-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Kantega SSO pour Confluence associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="16c7b-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Confluence needs to be established.</span></span>

<span data-ttu-id="16c7b-141">Dans Kantega SSO pour Confluence, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="16c7b-141">In Kantega SSO for Confluence, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16c7b-142">Pour configurer et tester l’authentification unique Azure AD avec Kantega SSO pour Confluence, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="16c7b-142">To configure and test Azure AD single sign-on with Kantega SSO for Confluence, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16c7b-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="16c7b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16c7b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16c7b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16c7b-145">**[Création d’un utilisateur de test Kantega SSO pour Confluence](#creating-a-kantega-sso-for-confluence-test-user)** pour avoir un équivalent de Britta Simon dans Kantega SSO pour Confluence qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="16c7b-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Confluence that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16c7b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16c7b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16c7b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="16c7b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16c7b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16c7b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kantega SSO pour Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="16c7b-150">**Pour configurer l’authentification unique Azure AD avec Kantega SSO pour Confluence, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16c7b-150">**To configure Azure AD single sign-on with Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="16c7b-151">Sur le portail Azure, dans la page d’intégration de l’application **Kantega SSO pour Confluence**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-151">In the Azure portal, on the **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="16c7b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="16c7b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. <span data-ttu-id="16c7b-155">En mode initié **IDP**, dans la section **Domaine et URL Kantega SSO pour Confluence**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-155">In **IDP** initiated mode, on the **Kantega SSO for Confluence Domain and URLs** section perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="16c7b-157">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-157">a.</span></span> <span data-ttu-id="16c7b-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="16c7b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="16c7b-159">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-159">b.</span></span> <span data-ttu-id="16c7b-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="16c7b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="16c7b-161">En mode initié **SP**, activez **Afficher les paramètres d’URL avancés**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="16c7b-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="16c7b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16c7b-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="16c7b-164">These values are not real.</span></span> <span data-ttu-id="16c7b-165">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="16c7b-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="16c7b-166">Ces valeurs sont reçues durant la configuration du plug-in Confluence qui est décrite plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="16c7b-166">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="16c7b-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="16c7b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. <span data-ttu-id="16c7b-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="16c7b-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="16c7b-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration Confluence** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="16c7b-171">In a different web browser window, log in to your **Confluence admin portal** as an administrator.</span></span>

8. <span data-ttu-id="16c7b-172">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-172">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. <span data-ttu-id="16c7b-174">Sous **ATLASSIAN MARKETPLACE**, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="16c7b-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. <span data-ttu-id="16c7b-176">Recherchez **Kerberos SAML Kantega SSO pour Confluence**, puis cliquez sur le bouton **Installer** pour installer le nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="16c7b-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. <span data-ttu-id="16c7b-178">L’installation du plug-in démarre.</span><span class="sxs-lookup"><span data-stu-id="16c7b-178">The plugin installation starts.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. <span data-ttu-id="16c7b-180">Une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="16c7b-180">Once the installation is complete.</span></span> <span data-ttu-id="16c7b-181">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-181">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. <span data-ttu-id="16c7b-183">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-183">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. <span data-ttu-id="16c7b-185">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="16c7b-185">Click **Configure** to configure the new plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. <span data-ttu-id="16c7b-187">Ce nouveau plug-in figure également sous l’onglet **UTILISATEURS ET SÉCURITÉ**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. <span data-ttu-id="16c7b-189">Dans la section **SAML**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-189">In the **SAML** section.</span></span> <span data-ttu-id="16c7b-190">Dans le menu déroulant **Ajouter le fournisseur d’identité**, sélectionnez **Azure Active Directory (Azure AD)**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-190">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. <span data-ttu-id="16c7b-192">Sélectionnez le niveau d’abonnement **De base**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-192">Select subscription level as **Basic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. <span data-ttu-id="16c7b-194">Dans la section **Propriétés de l’application**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-194">On the **App properties** section, perform following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="16c7b-196">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-196">a.</span></span> <span data-ttu-id="16c7b-197">Copiez la valeur **URI ID d’application** et utilisez-la en tant que **Identifier, Reply URL, and Sign-On URL** (Identificateur, URL de réponse et URL de connexion) dans la section **Domaine et URL Kantega SSO pour Confluence** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16c7b-197">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="16c7b-198">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-198">b.</span></span> <span data-ttu-id="16c7b-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-199">Click **Next**.</span></span>

19. <span data-ttu-id="16c7b-200">Dans la section **Metadata import** (Importation des métadonnées), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-200">On the **Metadata import** section, perform following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="16c7b-202">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-202">a.</span></span> <span data-ttu-id="16c7b-203">Sélectionnez **Metadata file on my computer** (Fichier de métadonnées sur mon ordinateur), puis chargez le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16c7b-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="16c7b-204">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-204">b.</span></span> <span data-ttu-id="16c7b-205">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-205">Click **Next**.</span></span>

20. <span data-ttu-id="16c7b-206">Dans la section **Name and SSO location** (Nom et emplacement de l’authentification unique), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-206">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="16c7b-208">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-208">a.</span></span> <span data-ttu-id="16c7b-209">Ajoutez le nom du fournisseur d’identité dans la zone de texte **Identity provider name** (Nom du fournisseur d’identité) (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16c7b-209">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="16c7b-210">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-210">b.</span></span> <span data-ttu-id="16c7b-211">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-211">Click **Next**.</span></span>

21. <span data-ttu-id="16c7b-212">Vérifiez le certificat de signature, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-212">Verify the Signing certificate and click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. <span data-ttu-id="16c7b-214">Dans la section **Confluence user accounts** (Comptes d’utilisateur Confluence), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-214">On the **Confluence user accounts** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="16c7b-216">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-216">a.</span></span> <span data-ttu-id="16c7b-217">Sélectionnez **créer des utilisateurs dans l’annuaire interne de Confluence si nécessaire** et entrez le nom du groupe approprié pour les utilisateurs (peut être non plusieurs.</span><span class="sxs-lookup"><span data-stu-id="16c7b-217">Select **Create users in Confluence's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="16c7b-218">groupes séparés par des virgules).</span><span class="sxs-lookup"><span data-stu-id="16c7b-218">of groups separated by comma).</span></span>

    <span data-ttu-id="16c7b-219">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-219">b.</span></span> <span data-ttu-id="16c7b-220">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-220">Click **Next**.</span></span>

23. <span data-ttu-id="16c7b-221">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-221">Click **Finish**.</span></span>   

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. <span data-ttu-id="16c7b-223">Dans la section **Known domains for Azure AD** (Domaines connus pour Azure AD), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-223">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="16c7b-225">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-225">a.</span></span> <span data-ttu-id="16c7b-226">Sélectionnez **Known domains** (Domaines connus) dans le volet gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="16c7b-226">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="16c7b-227">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-227">b.</span></span> <span data-ttu-id="16c7b-228">Entrez le nom de domaine dans la zone de texte **Known domains** (Domaines connus).</span><span class="sxs-lookup"><span data-stu-id="16c7b-228">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="16c7b-229">c.</span><span class="sxs-lookup"><span data-stu-id="16c7b-229">c.</span></span> <span data-ttu-id="16c7b-230">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="16c7b-231">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="16c7b-231">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16c7b-232">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="16c7b-232">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16c7b-233">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16c7b-233">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16c7b-234">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="16c7b-235">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16c7b-235">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="16c7b-237">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16c7b-237">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16c7b-238">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-238">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16c7b-240">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-240">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16c7b-242">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16c7b-242">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16c7b-244">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-244">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16c7b-246">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-246">a.</span></span> <span data-ttu-id="16c7b-247">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-247">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16c7b-248">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-248">b.</span></span> <span data-ttu-id="16c7b-249">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16c7b-249">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16c7b-250">c.</span><span class="sxs-lookup"><span data-stu-id="16c7b-250">c.</span></span> <span data-ttu-id="16c7b-251">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-251">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16c7b-252">d.</span><span class="sxs-lookup"><span data-stu-id="16c7b-252">d.</span></span> <span data-ttu-id="16c7b-253">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="16c7b-254">Création d’un utilisateur de test Kantega SSO pour Confluence</span><span class="sxs-lookup"><span data-stu-id="16c7b-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="16c7b-255">Pour permettre aux utilisateurs Azure AD de se connecter à Confluence, vous devez les approvisionner dans Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-255">To enable Azure AD users to log in to Confluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="16c7b-256">Dans le cas de Kantega SSO pour Confluence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="16c7b-256">In the case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="16c7b-257">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16c7b-257">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="16c7b-258">Connectez-vous à votre site d’entreprise Kantega SSO pour Confluence en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="16c7b-258">Log in to your Kantega SSO for Confluence company site as an administrator.</span></span>

2. <span data-ttu-id="16c7b-259">Pointez sur la roue dentée, puis cliquez sur **Gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-259">Hover on cog and click the **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. <span data-ttu-id="16c7b-261">Dans la section Utilisateurs, cliquez sur l’onglet **Add users** (Ajouter des utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="16c7b-261">Under Users section, click **Add Users** tab.</span></span> <span data-ttu-id="16c7b-262">Dans la page de boîte de dialogue **Add a User** (Ajouter un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16c7b-262">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="16c7b-264">a.</span><span class="sxs-lookup"><span data-stu-id="16c7b-264">a.</span></span> <span data-ttu-id="16c7b-265">Dans la zone de texte **Username** (Nom d’utilisateur), tapez l’e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="16c7b-265">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="16c7b-266">b.</span><span class="sxs-lookup"><span data-stu-id="16c7b-266">b.</span></span> <span data-ttu-id="16c7b-267">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16c7b-267">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="16c7b-268">c.</span><span class="sxs-lookup"><span data-stu-id="16c7b-268">c.</span></span> <span data-ttu-id="16c7b-269">Dans la zone de texte **Email** (E-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="16c7b-269">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="16c7b-270">d.</span><span class="sxs-lookup"><span data-stu-id="16c7b-270">d.</span></span> <span data-ttu-id="16c7b-271">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="16c7b-271">In the **Password** textbox, type the password for user.</span></span>

    <span data-ttu-id="16c7b-272">e.</span><span class="sxs-lookup"><span data-stu-id="16c7b-272">e.</span></span> <span data-ttu-id="16c7b-273">Cliquez sur **Confirm Password** (Confirmer le mot de passe), puis entrez de nouveau le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="16c7b-273">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="16c7b-274">f.</span><span class="sxs-lookup"><span data-stu-id="16c7b-274">f.</span></span> <span data-ttu-id="16c7b-275">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-275">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16c7b-276">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="16c7b-276">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16c7b-277">Dans cette section, vous permettez à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Kantega SSO pour Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-277">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Confluence.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="16c7b-279">**Pour affecter Britta Simon à Kantega SSO pour Confluence, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16c7b-279">**To assign Britta Simon to Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="16c7b-280">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-280">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="16c7b-282">Dans la liste des applications, sélectionnez **Kantega SSO pour Confluence**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-282">In the applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. <span data-ttu-id="16c7b-284">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-284">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="16c7b-286">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-286">Click **Add** button.</span></span> <span data-ttu-id="16c7b-287">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-287">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="16c7b-289">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="16c7b-289">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16c7b-290">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-290">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16c7b-291">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16c7b-291">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16c7b-292">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="16c7b-292">Testing single sign-on</span></span>

<span data-ttu-id="16c7b-293">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="16c7b-293">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="16c7b-294">Lorsque vous cliquez sur la vignette Kantega SSO pour Confluence dans le volet d’accès, vous devez être automatiquement connecté à votre application Kantega SSO pour Confluence.</span><span class="sxs-lookup"><span data-stu-id="16c7b-294">When you click the Kantega SSO for Confluence tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="16c7b-295">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16c7b-295">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16c7b-296">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="16c7b-296">Additional resources</span></span>

* [<span data-ttu-id="16c7b-297">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16c7b-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16c7b-298">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="16c7b-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

