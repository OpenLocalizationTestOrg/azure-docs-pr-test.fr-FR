---
title: "Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="62d4f-103">Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="62d4f-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="62d4f-104">Dans ce didacticiel, vous allez apprendre à intégrer ScaleX Enterprise à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62d4f-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62d4f-105">L’intégration du logiciel ScaleX Enterprise à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="62d4f-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62d4f-106">Dans Azure AD, vous pouvez contrôler qui a accès à ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="62d4f-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="62d4f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à ScaleX Enterprise (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62d4f-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="62d4f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62d4f-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="62d4f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="62d4f-110">Qu’est-ce que l’accès aux applications et l’authentification unique avec [Azure Active Directory](active-directory-appssoaccess-whatis.md) ?</span><span class="sxs-lookup"><span data-stu-id="62d4f-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62d4f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="62d4f-111">Prerequisites</span></span>

<span data-ttu-id="62d4f-112">Pour configurer l’intégration d’Azure AD à ScaleX Enterprise, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="62d4f-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="62d4f-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="62d4f-114">Un abonnement ScaleX Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="62d4f-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62d4f-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="62d4f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62d4f-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="62d4f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62d4f-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="62d4f-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="62d4f-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62d4f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62d4f-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="62d4f-119">Scenario description</span></span>
<span data-ttu-id="62d4f-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="62d4f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62d4f-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="62d4f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62d4f-122">Ajout de ScaleX Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="62d4f-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="62d4f-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="62d4f-124">Ajout de ScaleX Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="62d4f-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="62d4f-125">Pour configurer l’intégration de ScaleX Enterprise à Azure AD, vous devez ajouter ScaleX Enterprise depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="62d4f-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62d4f-126">**Pour ajouter ScaleX Enterprise à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62d4f-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62d4f-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62d4f-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62d4f-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="62d4f-132">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="62d4f-132">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="62d4f-134">Dans la zone de recherche, entrez **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="62d4f-136">Dans le volet de résultats, sélectionnez **ScaleX Enterprise**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="62d4f-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62d4f-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62d4f-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ScaleX Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="62d4f-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="62d4f-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ScaleX Enterprise équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62d4f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="62d4f-141">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur ScaleX Enterprise associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="62d4f-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="62d4f-142">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62d4f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="62d4f-143">Pour configurer et tester l’authentification unique Azure AD avec ScaleX Enterprise, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="62d4f-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62d4f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="62d4f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62d4f-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62d4f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62d4f-146">**[Création d’un utilisateur de test ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)** pour avoir un équivalent de Britta Simon dans ScaleX Enterprise, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="62d4f-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62d4f-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62d4f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62d4f-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="62d4f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62d4f-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62d4f-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62d4f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="62d4f-151">**Pour configurer l’authentification unique Azure AD avec ScaleX Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62d4f-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="62d4f-152">Dans le portail Azure, sur la page d’intégration de l’application **ScaleX Enterprise**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="62d4f-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="62d4f-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="62d4f-156">Dans la section **Domaines et URL ScaleX Enterprise**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP**:</span><span class="sxs-lookup"><span data-stu-id="62d4f-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="62d4f-158">a.</span><span class="sxs-lookup"><span data-stu-id="62d4f-158">a.</span></span> <span data-ttu-id="62d4f-159">Dans la zone de texte **Identificateur**, tapez la valeur au format suivant : `https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="62d4f-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="62d4f-160">b.</span><span class="sxs-lookup"><span data-stu-id="62d4f-160">b.</span></span> <span data-ttu-id="62d4f-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="62d4f-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="62d4f-162">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="62d4f-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="62d4f-164">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="62d4f-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="62d4f-165">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="62d4f-165">These are not the real values.</span></span> <span data-ttu-id="62d4f-166">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels et l’URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="62d4f-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="62d4f-167">Pour obtenir ces valeurs, contactez [l’équipe de support technique ScaleX Enterprise](http://info.rescale.com/contact_sales).</span><span class="sxs-lookup"><span data-stu-id="62d4f-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="62d4f-168">Votre application ScaleX s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à modifier des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="62d4f-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="62d4f-169">Cliquez sur la case **Afficher et modifier tous les autres attributs utilisateur** pour ouvrir les attributs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="62d4f-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="62d4f-171">a.</span><span class="sxs-lookup"><span data-stu-id="62d4f-171">a.</span></span> <span data-ttu-id="62d4f-172">Cliquez avec le bouton droit sur l’attribut **name** et cliquez sur Supprimer.</span><span class="sxs-lookup"><span data-stu-id="62d4f-172">Right click the attribute **name** and click delete.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="62d4f-174">b.</span><span class="sxs-lookup"><span data-stu-id="62d4f-174">b.</span></span> <span data-ttu-id="62d4f-175">Cliquez sur l’attribut **emailaddress** pour ouvrir la fenêtre Modifier l’attribut.</span><span class="sxs-lookup"><span data-stu-id="62d4f-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="62d4f-176">Modifiez sa valeur de **user.mail** en **user.userprincipalname** et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="62d4f-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="62d4f-178">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="62d4f-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="62d4f-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="62d4f-180">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="62d4f-182">Dans la section **Configuration de ScaleX Enterprise** , cliquez sur **Configurer ScaleX Enterprise** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="62d4f-183">Copiez **l’ID d’entité SAML** et **l’URL du service d’authentification unique SAML** à partir de la section **Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="62d4f-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="62d4f-185">Pour configurer l’authentification unique sur **ScaleX Enterprise**, connectez-vous au site web ScaleX Enterprise de votre société en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="62d4f-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="62d4f-186">Cliquez sur le menu dans le coin supérieur droit et sélectionnez **Contoso Administration**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62d4f-187">Contoso est simplement un exemple.</span><span class="sxs-lookup"><span data-stu-id="62d4f-187">Contoso is just an example.</span></span> <span data-ttu-id="62d4f-188">Ce doit être le nom réel de votre société.</span><span class="sxs-lookup"><span data-stu-id="62d4f-188">This should be your actual Company Name.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="62d4f-190">Sélectionnez **Intégrations** dans le menu supérieur, puis **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="62d4f-192">Remplissez le formulaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="62d4f-192">Complete the form as follows:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="62d4f-194">a.</span><span class="sxs-lookup"><span data-stu-id="62d4f-194">a.</span></span> <span data-ttu-id="62d4f-195">Sélectionnez **Créer n’importe quel utilisateur pouvant s’authentifier avec l’authentification unique.**</span><span class="sxs-lookup"><span data-stu-id="62d4f-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="62d4f-196">b.</span><span class="sxs-lookup"><span data-stu-id="62d4f-196">b.</span></span> <span data-ttu-id="62d4f-197">**Fournisseur de service SAML** : collez la valeur ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span><span class="sxs-lookup"><span data-stu-id="62d4f-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="62d4f-198">c.</span><span class="sxs-lookup"><span data-stu-id="62d4f-198">c.</span></span> <span data-ttu-id="62d4f-199">**Nom du champ d’adresse de messagerie de fournisseur d’identité dans la réponse ACS** : collez la valeur `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="62d4f-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="62d4f-200">d.</span><span class="sxs-lookup"><span data-stu-id="62d4f-200">d.</span></span> <span data-ttu-id="62d4f-201">**ID entité de EntityDescriptor du fournisseur d’identité :** collez la valeur **ID d’entité SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="62d4f-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="62d4f-202">e.</span><span class="sxs-lookup"><span data-stu-id="62d4f-202">e.</span></span> <span data-ttu-id="62d4f-203">**URL SingleSignOnService du fournisseur d’identité :** collez **l’URL du service d’authentification unique SAML** à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="62d4f-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="62d4f-204">f.</span><span class="sxs-lookup"><span data-stu-id="62d4f-204">f.</span></span> <span data-ttu-id="62d4f-205">**Certificat X509 public du fournisseur d’identité :** ouvrez le certificat X509 téléchargé à partir d’Azure dans le bloc-notes et collez le contenu dans cette zone.</span><span class="sxs-lookup"><span data-stu-id="62d4f-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="62d4f-206">Assurez-vous qu’aucun saut de ligne ne se trouve au milieu du contenu du certificat.</span><span class="sxs-lookup"><span data-stu-id="62d4f-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="62d4f-207">g.</span><span class="sxs-lookup"><span data-stu-id="62d4f-207">g.</span></span> <span data-ttu-id="62d4f-208">Cochez les cases suivantes : **Activé, Chiffrer NameID et Signer AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="62d4f-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="62d4f-209">h.</span><span class="sxs-lookup"><span data-stu-id="62d4f-209">h.</span></span> <span data-ttu-id="62d4f-210">Cliquez sur **Mettre à jour les paramètres de l’authentification unique** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="62d4f-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="62d4f-211">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="62d4f-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62d4f-212">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="62d4f-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62d4f-213">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62d4f-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62d4f-214">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="62d4f-215">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="62d4f-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="62d4f-217">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62d4f-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62d4f-218">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62d4f-220">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="62d4f-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62d4f-222">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62d4f-224">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="62d4f-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62d4f-226">a.</span><span class="sxs-lookup"><span data-stu-id="62d4f-226">a.</span></span> <span data-ttu-id="62d4f-227">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62d4f-228">b.</span><span class="sxs-lookup"><span data-stu-id="62d4f-228">b.</span></span> <span data-ttu-id="62d4f-229">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62d4f-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62d4f-230">c.</span><span class="sxs-lookup"><span data-stu-id="62d4f-230">c.</span></span> <span data-ttu-id="62d4f-231">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62d4f-232">d.</span><span class="sxs-lookup"><span data-stu-id="62d4f-232">d.</span></span> <span data-ttu-id="62d4f-233">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="62d4f-234">Création d’un utilisateur de test ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="62d4f-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="62d4f-235">Pour permettre aux utilisateurs d’Azure AD de se connecter à ScaleX Enterprise, vous devez les configurer dans ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62d4f-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="62d4f-236">Dans le cas de ScaleX Enterprise, cette configuration est une tâche automatique et aucune opération manuelle n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="62d4f-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="62d4f-237">Tout utilisateur authentifié avec des informations d’authentification unique est automatiquement configuré du côté ScaleX.</span><span class="sxs-lookup"><span data-stu-id="62d4f-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62d4f-238">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="62d4f-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62d4f-239">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62d4f-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="62d4f-241">**Pour affecter Britta Simon à ScaleX Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62d4f-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="62d4f-242">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="62d4f-244">Dans la liste des applications, sélectionnez **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="62d4f-246">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="62d4f-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-248">Click **Add** button.</span></span> <span data-ttu-id="62d4f-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="62d4f-251">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="62d4f-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62d4f-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62d4f-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="62d4f-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="62d4f-254">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="62d4f-254">Testing single sign-on</span></span>

<span data-ttu-id="62d4f-255">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="62d4f-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62d4f-256">Cliquez sur la mosaïque ScaleX Enterprise dans le volet d’accès pour vous connecter automatiquement à votre application ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62d4f-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="62d4f-257">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="62d4f-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="62d4f-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="62d4f-258">Additional resources</span></span>

* [<span data-ttu-id="62d4f-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62d4f-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62d4f-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="62d4f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

