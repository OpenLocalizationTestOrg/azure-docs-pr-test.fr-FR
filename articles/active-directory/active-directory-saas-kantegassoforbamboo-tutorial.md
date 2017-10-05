---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Bamboo | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kantega SSO pour Bamboo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: cc259bb6f9bdb2293b6935e45e2df52b9fee6873
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="2ba34-103">Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour Bamboo</span><span class="sxs-lookup"><span data-stu-id="2ba34-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="2ba34-104">Dans ce didacticiel, vous allez apprendre à intégrer Kantega SSO pour Bamboo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ba34-104">In this tutorial, you learn how to integrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ba34-105">L’intégration de Kantega SSO pour Bamboo avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2ba34-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2ba34-106">Vous pouvez contrôler dans Azure AD qui a accès à Kantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-106">You can control in Azure AD who has access to Kantega SSO for Bamboo</span></span>
- <span data-ttu-id="2ba34-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Kantega SSO pour Bamboo (authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba34-107">You can enable your users to automatically get signed-on to Kantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ba34-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2ba34-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2ba34-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ba34-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ba34-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2ba34-110">Prerequisites</span></span>

<span data-ttu-id="2ba34-111">Pour configurer l’intégration d’Azure AD avec Kantega SSO pour Bamboo, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ba34-111">To configure Azure AD integration with Kantega SSO for Bamboo, you need the following items:</span></span>

- <span data-ttu-id="2ba34-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ba34-113">Un abonnement Kantega SSO pour Bamboo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2ba34-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ba34-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2ba34-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ba34-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2ba34-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ba34-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2ba34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ba34-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ba34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ba34-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2ba34-118">Scenario description</span></span>
<span data-ttu-id="2ba34-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2ba34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ba34-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ba34-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ba34-121">Ajout de Kantega SSO pour Bamboo à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2ba34-121">Adding Kantega SSO for Bamboo from the gallery</span></span>
2. <span data-ttu-id="2ba34-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-the-gallery"></a><span data-ttu-id="2ba34-123">Ajout de Kantega SSO pour Bamboo à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2ba34-123">Adding Kantega SSO for Bamboo from the gallery</span></span>
<span data-ttu-id="2ba34-124">Pour configurer l’intégration de Kantega SSO pour Bamboo dans Azure AD, vous devez ajouter Kantega SSO pour Bamboo à partir de la galerie à la liste des applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="2ba34-124">To configure the integration of Kantega SSO for Bamboo into Azure AD, you need to add Kantega SSO for Bamboo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ba34-125">**Pour ajouter Kantega SSO pour Bamboo à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ba34-125">**To add Kantega SSO for Bamboo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ba34-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ba34-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2ba34-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2ba34-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2ba34-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2ba34-133">Dans la zone de recherche, tapez **Kantega SSO pour Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-133">In the search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="2ba34-135">Dans le volet de résultats, sélectionnez **Kantega SSO pour Bamboo**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2ba34-135">In the results panel, select **Kantega SSO for Bamboo**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ba34-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ba34-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kantega SSO pour Bamboo sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2ba34-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ba34-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur équivalent à l’utilisateur Azure AD dans Kantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bamboo is to a user in Azure AD.</span></span> <span data-ttu-id="2ba34-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Kantega SSO pour Bamboo associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2ba34-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bamboo needs to be established.</span></span>

<span data-ttu-id="2ba34-141">Dans Kantega SSO pour Bamboo, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2ba34-141">In Kantega SSO for Bamboo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2ba34-142">Pour configurer et tester l’authentification unique Azure AD avec Kantega SSO pour Bamboo, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ba34-142">To configure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ba34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2ba34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ba34-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ba34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ba34-145">**[Création d’un utilisateur de test Kantega SSO pour Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)** pour avoir un équivalent de Britta Simon dans Kantega SSO pour Bamboo qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2ba34-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ba34-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba34-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ba34-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2ba34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ba34-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ba34-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="2ba34-150">**Pour configurer l’authentification unique Azure AD avec Kantega SSO pour Bamboo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ba34-150">**To configure Azure AD single sign-on with Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="2ba34-151">Sur le portail Azure, dans la page d’intégration de l’application **Kantega SSO pour Bamboo**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-151">In the Azure portal, on the **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2ba34-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2ba34-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="2ba34-155">En mode initié **IDP**, dans la section **Domaine et URL Kantega SSO pour Bamboo**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-155">In **IDP** initiated mode, on the **Kantega SSO for Bamboo Domain and URLs** section perform the following step :</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="2ba34-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-157">a.</span></span> <span data-ttu-id="2ba34-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ba34-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2ba34-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-159">b.</span></span> <span data-ttu-id="2ba34-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ba34-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2ba34-161">En mode initié **SP**, activez **Afficher les paramètres d’URL avancés**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step :</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="2ba34-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ba34-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2ba34-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2ba34-164">These values are not real.</span></span> <span data-ttu-id="2ba34-165">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="2ba34-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2ba34-166">Ces valeurs sont reçues durant la configuration du plug-in Bamboo qui est décrite plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2ba34-166">These values are recieved during the configuration of Bamboo plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="2ba34-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2ba34-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="2ba34-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2ba34-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2ba34-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre serveur local Bamboo en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2ba34-171">In a different web browser window, log in to your Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="2ba34-172">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="2ba34-174">Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="2ba34-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="2ba34-175">Recherchez **Kantega SSO pour Bamboo (SAML & Kerberos)**, puis cliquez sur le bouton **Installer** pour installer le nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="2ba34-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="2ba34-177">L’installation du plug-in démarre.</span><span class="sxs-lookup"><span data-stu-id="2ba34-177">The plugin installation will start.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="2ba34-179">Une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="2ba34-179">Once the installation is complete.</span></span> <span data-ttu-id="2ba34-180">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-180">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="2ba34-182">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-182">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="2ba34-184">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="2ba34-184">Click **Configure** to configure the new plugin.</span></span>    

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="2ba34-186">Dans la section **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-186">In the **SAML** section.</span></span> <span data-ttu-id="2ba34-187">Dans le menu déroulant **Ajouter le fournisseur d’identité**, sélectionnez **Azure Active Directory (Azure AD)**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-187">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="2ba34-189">Sélectionnez le niveau d’abonnement **De base**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-189">Select subscription level as **Basic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="2ba34-191">Dans la section **Propriétés de l’application**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-191">On the **App properties** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="2ba34-193">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-193">a.</span></span> <span data-ttu-id="2ba34-194">Copiez la valeur **URI ID d'application** et utilisez-la en tant que **Identifier, Reply URL, and Sign-On URL** (Identificateur, URL de réponse et URL de connexion) dans la section **Domaine et URL Kantega SSO pour Bamboo** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba34-194">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2ba34-195">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-195">b.</span></span> <span data-ttu-id="2ba34-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-196">Click **Next**.</span></span>

17. <span data-ttu-id="2ba34-197">Dans la section **Metadata import** (Importation des métadonnées), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-197">On the **Metadata import** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="2ba34-199">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-199">a.</span></span> <span data-ttu-id="2ba34-200">Sélectionnez **Metadata file on my computer** (Fichier de métadonnées sur mon ordinateur), puis chargez le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba34-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2ba34-201">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-201">b.</span></span> <span data-ttu-id="2ba34-202">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-202">Click **Next**.</span></span>

18. <span data-ttu-id="2ba34-203">Dans la section **Name and SSO location** (Nom et emplacement de l’authentification unique), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-203">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="2ba34-205">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-205">a.</span></span> <span data-ttu-id="2ba34-206">Ajoutez le nom du fournisseur d’identité dans la zone de texte **Identity provider name** (Nom du fournisseur d’identité) (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ba34-206">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2ba34-207">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-207">b.</span></span> <span data-ttu-id="2ba34-208">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-208">Click **Next**.</span></span>

19. <span data-ttu-id="2ba34-209">Vérifiez le certificat de signature, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-209">Verify the Signing certificate and click **Next**.</span></span>  

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="2ba34-211">Dans la section **Bamboo user accounts** (Comptes d’utilisateur Bamboo), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-211">On the **Bamboo user accounts** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="2ba34-213">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-213">a.</span></span> <span data-ttu-id="2ba34-214">Sélectionnez **Create users in Bamboo's internal Directory if needed** (Créer des utilisateurs dans l’annuaire interne de Bamboo si nécessaire) et entrez le nom de groupe approprié pour les utilisateurs (peut être plusieurs</span><span class="sxs-lookup"><span data-stu-id="2ba34-214">Select **Create users in Bamboo's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="2ba34-215">groupes séparés par des virgules).</span><span class="sxs-lookup"><span data-stu-id="2ba34-215">of groups separated by comma).</span></span>

    <span data-ttu-id="2ba34-216">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-216">b.</span></span> <span data-ttu-id="2ba34-217">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-217">Click **Next**.</span></span>

21. <span data-ttu-id="2ba34-218">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-218">Click **Finish**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="2ba34-220">Dans la section **Known domains for Azure AD** (Domaines connus pour Azure AD), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-220">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="2ba34-222">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-222">a.</span></span> <span data-ttu-id="2ba34-223">Sélectionnez **Known domains** (Domaines connus) dans le volet gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="2ba34-223">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="2ba34-224">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-224">b.</span></span> <span data-ttu-id="2ba34-225">Entrez le nom de domaine dans la zone de texte **Known domains** (Domaines connus).</span><span class="sxs-lookup"><span data-stu-id="2ba34-225">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="2ba34-226">c.</span><span class="sxs-lookup"><span data-stu-id="2ba34-226">c.</span></span> <span data-ttu-id="2ba34-227">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2ba34-228">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2ba34-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2ba34-229">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2ba34-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2ba34-230">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ba34-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ba34-231">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ba34-232">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba34-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2ba34-234">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ba34-234">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ba34-235">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-235">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ba34-237">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-237">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ba34-239">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2ba34-239">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ba34-241">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-241">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ba34-243">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-243">a.</span></span> <span data-ttu-id="2ba34-244">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-244">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ba34-245">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-245">b.</span></span> <span data-ttu-id="2ba34-246">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ba34-246">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ba34-247">c.</span><span class="sxs-lookup"><span data-stu-id="2ba34-247">c.</span></span> <span data-ttu-id="2ba34-248">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-248">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2ba34-249">d.</span><span class="sxs-lookup"><span data-stu-id="2ba34-249">d.</span></span> <span data-ttu-id="2ba34-250">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="2ba34-251">Création d’un utilisateur de test Kantega SSO pour Bamboo</span><span class="sxs-lookup"><span data-stu-id="2ba34-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="2ba34-252">Pour permettre aux utilisateurs Azure AD de se connecter à Bamboo, vous devez les attribuer dans Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-252">To enable Azure AD users to log in to Bamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="2ba34-253">Dans Kantega SSO pour Bamboo, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2ba34-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="2ba34-254">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ba34-254">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2ba34-255">Connectez-vous à votre serveur local Bamboo en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2ba34-255">Log in to your Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="2ba34-256">Pointez sur la roue dentée, puis cliquez sur **Gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-256">Hover on cog and click the **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="2ba34-258">Cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-258">Click **Users**.</span></span> <span data-ttu-id="2ba34-259">Sous la section **Add User** (Ajouter un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2ba34-259">Under the **Add user** section, Perform follwing steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="2ba34-261">a.</span><span class="sxs-lookup"><span data-stu-id="2ba34-261">a.</span></span> <span data-ttu-id="2ba34-262">Dans la zone de texte **Username** (Nom d’utilisateur), tapez l’e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ba34-262">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2ba34-263">b.</span><span class="sxs-lookup"><span data-stu-id="2ba34-263">b.</span></span> <span data-ttu-id="2ba34-264">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ba34-264">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="2ba34-265">c.</span><span class="sxs-lookup"><span data-stu-id="2ba34-265">c.</span></span> <span data-ttu-id="2ba34-266">Dans la zone de texte **Confirm Password** (Confirmer le mot de passe), entrez à nouveau le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ba34-266">In the **Confirm Password** textbox, reenter the password of user.</span></span>
    
    <span data-ttu-id="2ba34-267">d.</span><span class="sxs-lookup"><span data-stu-id="2ba34-267">d.</span></span> <span data-ttu-id="2ba34-268">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ba34-268">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="2ba34-269">e.</span><span class="sxs-lookup"><span data-stu-id="2ba34-269">e.</span></span> <span data-ttu-id="2ba34-270">Dans la zone de texte **Email** (E-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ba34-270">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2ba34-271">f.</span><span class="sxs-lookup"><span data-stu-id="2ba34-271">f.</span></span> <span data-ttu-id="2ba34-272">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-272">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2ba34-273">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ba34-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2ba34-274">Dans cette section, vous permettez à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Kantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bamboo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2ba34-276">**Pour affecter Britta Simon à Kantega SSO pour Bamboo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2ba34-276">**To assign Britta Simon to Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="2ba34-277">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2ba34-279">Dans la liste des applications, sélectionnez **Kantega SSO pour Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-279">In the applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="2ba34-281">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2ba34-283">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-283">Click **Add** button.</span></span> <span data-ttu-id="2ba34-284">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2ba34-286">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2ba34-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2ba34-287">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ba34-288">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2ba34-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ba34-289">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2ba34-289">Testing single sign-on</span></span>

<span data-ttu-id="2ba34-290">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2ba34-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2ba34-291">Lorsque vous cliquez sur la vignette Kantega SSO pour Bamboo dans le Panneau d'accès, vous devriez être automatiquement connecté à votre application Kantega SSO pour Bamboo.</span><span class="sxs-lookup"><span data-stu-id="2ba34-291">When you click the Kantega SSO for Bamboo tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="2ba34-292">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ba34-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2ba34-293">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2ba34-293">Additional resources</span></span>

* [<span data-ttu-id="2ba34-294">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ba34-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ba34-295">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2ba34-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

