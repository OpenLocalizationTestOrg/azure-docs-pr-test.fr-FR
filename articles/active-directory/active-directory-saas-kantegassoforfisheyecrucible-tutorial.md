---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour FishEye/Crucible | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kantega SSO pour FishEye/Crucible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9eaa2ec661a3488b0bef1f6b7cc7a82290720054
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="871b6-103">Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="871b6-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="871b6-104">Ce didacticiel explique comment intégrer Kantega SSO pour FishEye/Crucible avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="871b6-104">In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="871b6-105">L’intégration de Kantega SSO pour FishEye/Crucible avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="871b6-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="871b6-106">Vous pouvez contrôler dans Azure AD qui a accès à Kantega SSO pour FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-106">You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="871b6-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement connectés à Kantega SSO pour FishEye/Crucible (authentification unique) avec leur comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="871b6-107">You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="871b6-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="871b6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="871b6-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="871b6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="871b6-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="871b6-110">Prerequisites</span></span>

<span data-ttu-id="871b6-111">Pour configurer l’intégration d’Azure AD avec Kantega SSO pour FishEye/Crucible, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="871b6-111">To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:</span></span>

- <span data-ttu-id="871b6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="871b6-113">Un abonnement Kantega SSO pour FishEye/Crucible pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="871b6-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="871b6-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="871b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="871b6-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="871b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="871b6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="871b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="871b6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="871b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="871b6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="871b6-118">Scenario description</span></span>
<span data-ttu-id="871b6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="871b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="871b6-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="871b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="871b6-121">Ajout de Kantega SSO pour FishEye/Crucible à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="871b6-121">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
2. <span data-ttu-id="871b6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a><span data-ttu-id="871b6-123">Ajout de Kantega SSO pour FishEye/Crucible à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="871b6-123">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
<span data-ttu-id="871b6-124">Pour configurer l’intégration de Kantega SSO pour FishEye/Crucible dans Azure AD, vous devez ajouter Kantega SSO pour FishEye/Crucible à partir de la galerie à la liste de vos applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="871b6-124">To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="871b6-125">**Pour ajouter Kantega SSO pour FishEye/Crucible à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="871b6-125">**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="871b6-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="871b6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="871b6-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="871b6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="871b6-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="871b6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="871b6-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="871b6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="871b6-133">Dans la zone de recherche, tapez **Kantega SSO pour FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="871b6-133">In the search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="871b6-135">Dans le volet de résultats, sélectionnez **Kantega SSO pour FishEye/Crucible**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="871b6-135">In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="871b6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="871b6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kantega SSO pour FishEye/Crucible sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="871b6-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="871b6-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur équivalent à l’utilisateur Azure AD dans Kantega SSO pour FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD.</span></span> <span data-ttu-id="871b6-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Kantega SSO pour FishEye/Crucible associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="871b6-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.</span></span>

<span data-ttu-id="871b6-141">Dans Kantega SSO pour FishEye/Crucible, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="871b6-141">In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="871b6-142">Pour configurer et tester l’authentification unique Azure AD avec Kantega SSO pour FishEye/Crucible, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="871b6-142">To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="871b6-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="871b6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="871b6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="871b6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="871b6-145">**[Création d’un utilisateur de test Kantega SSO pour FishEye/Crucible](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** pour avoir un équivalent de Britta Simon dans Kantega SSO pour FishEye/Crucible qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="871b6-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="871b6-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="871b6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="871b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="871b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="871b6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="871b6-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kantega SSO pour FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="871b6-150">**Pour configurer l’authentification unique Azure AD avec Kantega SSO pour FishEye/Crucible, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="871b6-150">**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="871b6-151">Sur le portail Azure, dans la page d’intégration de l’application **Kantega SSO pour FishEye/Crucible**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="871b6-151">In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="871b6-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="871b6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="871b6-155">En mode initié **IDP**, dans la section **Domaine et URL Kantega SSO pour FishEye/Crucible**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-155">In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="871b6-157">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-157">a.</span></span> <span data-ttu-id="871b6-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="871b6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="871b6-159">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-159">b.</span></span> <span data-ttu-id="871b6-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="871b6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="871b6-161">En mode initié **SP**, activez **Afficher les paramètres d’URL avancés**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="871b6-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="871b6-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="871b6-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="871b6-164">These values are not real.</span></span> <span data-ttu-id="871b6-165">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="871b6-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="871b6-166">Ces valeurs sont reçues durant la configuration du plug-in FishEye/Crucible qui est décrite plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="871b6-166">These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="871b6-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="871b6-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="871b6-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="871b6-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="871b6-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre serveur local FishEye/Crucible en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="871b6-171">In a different web browser window, log in to your FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="871b6-172">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="871b6-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="871b6-174">Dans la section Paramètres système, cliquez sur **Find new add-ons (Rechercher de nouveaux modules complémentaires)**.</span><span class="sxs-lookup"><span data-stu-id="871b6-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="871b6-176">Recherchez **Kantega SSO pour Crucible**, puis cliquez sur le bouton **Installer** pour installer le nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="871b6-176">Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="871b6-178">L’installation du plug-in démarre.</span><span class="sxs-lookup"><span data-stu-id="871b6-178">The plugin installation starts.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="871b6-180">Une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="871b6-180">Once the installation is complete.</span></span> <span data-ttu-id="871b6-181">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="871b6-181">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="871b6-183">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="871b6-183">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="871b6-185">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="871b6-185">Click **Configure** to configure the new plugin.</span></span>    

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="871b6-187">Dans la section **SAML**.</span><span class="sxs-lookup"><span data-stu-id="871b6-187">In the **SAML** section.</span></span> <span data-ttu-id="871b6-188">Dans le menu déroulant **Ajouter le fournisseur d’identité**, sélectionnez **Azure Active Directory (Azure AD)**.</span><span class="sxs-lookup"><span data-stu-id="871b6-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="871b6-190">Sélectionnez le niveau d’abonnement **De base**.</span><span class="sxs-lookup"><span data-stu-id="871b6-190">Select subscription level as **Basic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="871b6-192">Dans la section **Propriétés de l’application**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-192">On the **App properties** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="871b6-194">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-194">a.</span></span> <span data-ttu-id="871b6-195">Copiez la valeur **URI ID d'application** et utilisez-la en tant que **Identifier, Reply URL, and Sign-On URL** (Identificateur, URL de réponse et URL de connexion) dans la section **Domaine et URL Kantega SSO pour FishEye/Crucible** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="871b6-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="871b6-196">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-196">b.</span></span> <span data-ttu-id="871b6-197">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="871b6-197">Click **Next**.</span></span>

18. <span data-ttu-id="871b6-198">Dans la section **Metadata import** (Importation des métadonnées), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-198">On the **Metadata import** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="871b6-200">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-200">a.</span></span> <span data-ttu-id="871b6-201">Sélectionnez **Metadata file on my computer** (Fichier de métadonnées sur mon ordinateur), puis chargez le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="871b6-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="871b6-202">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-202">b.</span></span> <span data-ttu-id="871b6-203">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="871b6-203">Click **Next**.</span></span>

19. <span data-ttu-id="871b6-204">Dans la section **Name and SSO location** (Nom et emplacement de l’authentification unique), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="871b6-206">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-206">a.</span></span> <span data-ttu-id="871b6-207">Ajoutez le nom du fournisseur d’identité dans la zone de texte **Identity provider name** (Nom du fournisseur d’identité) (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="871b6-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="871b6-208">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-208">b.</span></span> <span data-ttu-id="871b6-209">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="871b6-209">Click **Next**.</span></span>

20. <span data-ttu-id="871b6-210">Vérifiez le certificat de signature, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="871b6-210">Verify the Signing certificate and click **Next**.</span></span>  

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="871b6-212">Dans la section **FishEye user accounts** (Comptes d’utilisateur FishEye), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-212">On the **FishEye user accounts** section, perform following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="871b6-214">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-214">a.</span></span> <span data-ttu-id="871b6-215">Sélectionnez **créer des utilisateurs dans l’annuaire interne de FishEye si nécessaire** et entrez le nom du groupe approprié pour les utilisateurs (peut être non plusieurs.</span><span class="sxs-lookup"><span data-stu-id="871b6-215">Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="871b6-216">groupes séparés par des virgules).</span><span class="sxs-lookup"><span data-stu-id="871b6-216">of groups separated by comma).</span></span>

    <span data-ttu-id="871b6-217">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-217">b.</span></span> <span data-ttu-id="871b6-218">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="871b6-218">Click **Next**.</span></span>

22. <span data-ttu-id="871b6-219">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="871b6-219">Click **Finish**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="871b6-221">Dans la section **Known domains for Azure AD** (Domaines connus pour Azure AD), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="871b6-223">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-223">a.</span></span> <span data-ttu-id="871b6-224">Sélectionnez **Known domains** (Domaines connus) dans le volet gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="871b6-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="871b6-225">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-225">b.</span></span> <span data-ttu-id="871b6-226">Entrez le nom de domaine dans la zone de texte **Known domains** (Domaines connus).</span><span class="sxs-lookup"><span data-stu-id="871b6-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="871b6-227">c.</span><span class="sxs-lookup"><span data-stu-id="871b6-227">c.</span></span> <span data-ttu-id="871b6-228">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="871b6-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="871b6-229">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="871b6-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="871b6-230">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="871b6-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="871b6-231">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="871b6-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="871b6-232">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="871b6-233">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="871b6-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="871b6-235">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="871b6-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="871b6-236">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="871b6-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="871b6-238">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="871b6-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="871b6-240">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="871b6-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="871b6-242">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="871b6-244">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-244">a.</span></span> <span data-ttu-id="871b6-245">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="871b6-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="871b6-246">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-246">b.</span></span> <span data-ttu-id="871b6-247">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="871b6-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="871b6-248">c.</span><span class="sxs-lookup"><span data-stu-id="871b6-248">c.</span></span> <span data-ttu-id="871b6-249">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="871b6-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="871b6-250">d.</span><span class="sxs-lookup"><span data-stu-id="871b6-250">d.</span></span> <span data-ttu-id="871b6-251">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="871b6-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="871b6-252">Création d’un utilisateur de test Kantega SSO pour FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="871b6-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="871b6-253">Pour permettre aux utilisateurs Azure AD de se connecter à FishEye/Crucible, vous devez les approvisionner dans FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-253">To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="871b6-254">Dans Kantega SSO pour FishEye/Crucible, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="871b6-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="871b6-255">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="871b6-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="871b6-256">Connectez-vous à votre serveur local Crucible en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="871b6-256">Log in to your Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="871b6-257">Pointez sur le roue dentée, puis cliquez sur **Users** (Utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="871b6-257">Hover on cog and click the **Users**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="871b6-259">Dans la section de l’onglet **Users** (Utilisateurs), cliquez sur **Add user** (Ajouter un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="871b6-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="871b6-261">Dans la page de boîte de dialogue **Add New User** (Ajouter un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="871b6-261">On the **Add New User** dialog page, perform the following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="871b6-263">a.</span><span class="sxs-lookup"><span data-stu-id="871b6-263">a.</span></span> <span data-ttu-id="871b6-264">Dans la zone de texte **Username** (Nom d’utilisateur), tapez l’e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="871b6-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="871b6-265">b.</span><span class="sxs-lookup"><span data-stu-id="871b6-265">b.</span></span> <span data-ttu-id="871b6-266">Dans la zone de texte **Display Name** (Nom d’affichage), tapez le nom d’affichage de l’utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="871b6-266">In the **Display Name** textbox, type display name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="871b6-267">c.</span><span class="sxs-lookup"><span data-stu-id="871b6-267">c.</span></span> <span data-ttu-id="871b6-268">Dans la zone de texte **Email address** (Adresse e-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="871b6-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="871b6-269">d.</span><span class="sxs-lookup"><span data-stu-id="871b6-269">d.</span></span> <span data-ttu-id="871b6-270">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="871b6-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="871b6-271">e.</span><span class="sxs-lookup"><span data-stu-id="871b6-271">e.</span></span> <span data-ttu-id="871b6-272">Dans la zone de texte **Confirm Password** (Confirmer le mot de passe), entrez à nouveau le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="871b6-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="871b6-273">f.</span><span class="sxs-lookup"><span data-stu-id="871b6-273">f.</span></span> <span data-ttu-id="871b6-274">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="871b6-274">Click **Add**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="871b6-275">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="871b6-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="871b6-276">Dans cette section, vous permettez à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Kantega SSO pour FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="871b6-278">**Pour affecter Britta Simon à Kantega SSO pour FishEye/Crucible, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="871b6-278">**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="871b6-279">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="871b6-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="871b6-281">Dans la liste des applications, sélectionnez **Kantega SSO pour FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="871b6-281">In the applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="871b6-283">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="871b6-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="871b6-285">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="871b6-285">Click **Add** button.</span></span> <span data-ttu-id="871b6-286">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="871b6-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="871b6-288">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="871b6-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="871b6-289">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="871b6-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="871b6-290">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="871b6-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="871b6-291">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="871b6-291">Testing single sign-on</span></span>

<span data-ttu-id="871b6-292">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="871b6-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="871b6-293">Lorsque vous cliquez sur la vignette Kantega SSO pour FishEye/Crucible dans le panneau d’accès, vous devez être automatiquement connecté à votre application Kantega SSO pour FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="871b6-293">When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="871b6-294">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="871b6-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="871b6-295">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="871b6-295">Additional resources</span></span>

* [<span data-ttu-id="871b6-296">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="871b6-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="871b6-297">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="871b6-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

